---
title: "Blog 3"

weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---



# Chỉnh sửa Amazon EBS volumes trên Kubernetes với Volume Attribute Class
<span style="font-size:13px; color: #737070ff;">
by pmm on 05 MAR 2025 in | 
</span>
<small>
<a href="https://aws.amazon.com/blogs/containers/category/containers/">Containers</a>, 
<a href="https://aws.amazon.com/blogs/containers/category/post-types/technical-how-to/" style="color:#0073bb; text-decoration:none;">Technical How-to</a>,  
<a href="https://aws.amazon.com/blogs/containers/modify-amazon-ebs-volumes-on-kubernetes-with-volume-attributes-classes/" style="color:#0073bb; text-decoration:none;">Permalink</a>, 
</small>

*Bài viết này được đồng tác giả bởi Kevin Liu (Senior PMT), Jens-Uwe Walther (Senior STAM-Containers), và Drew Sirenko (Software Dev Engineer).*

## Giới thiệu
Trong bài viết này, chúng ta khám phá cách sửa đổi Amazon Elastic Block Store (Amazon EBS) volumes trên Kubernetes **mà không cần dừng ứng dụng**. Tìm hiểu cách sử dụng VolumeAttributesClass API cùng với Amazon EBS Container Storage Interface (CSI) driver để điều chỉnh hiệu năng provisioned performance, di chuyển sang gp3 volumes, và tự động hóa quy trình sao lưu dữ liệu của bạn.

Các ứng dụng container hóa hiện đại sử dụng bộ nhớ persistent, như phân tích dữ liệu, cơ sở dữ liệu, hoặc mã hóa/giải mã video, cần nhiều đặc tính lưu trữ khác nhau như độ trễ thấp, thông lượng cao, hoặc nhiều hơn nữa. Amazon EBS rất phù hợp cho các workload này. EBS volumes cung cấp nhiều loại lưu trữ khác nhau, các thuộc tính lưu trữ có thể cấu hình như IOPS và throughput, và khả năng thay đổi các thuộc tính này mà không làm gián đoạn.

Nếu bạn triển khai các workload stateful trên Kubernetes, bạn có thể sử dụng Amazon EBS CSI driver để provision và quản lý EBS volumes thay bạn. Khi bạn tạo Persistent Volume Claim (PVC) với kích thước cụ thể và Storage Class (SC), Kubernetes sẽ phối hợp với Amazon EBS CSI driver để triển khai workload với lưu trữ cần thiết bằng cách tạo, attach và format EBS volume.

Việc thay đổi đặc tính lưu trữ của volumes trong Kubernetes trước đây là thao tác offline, yêu cầu operator phải tạo SC mới, và migrate sang PVC và Persistent Volume (PV) mới. Quy trình này cần downtime và ảnh hưởng đến availability. Vì lý do đó, năm 2023, AWS phát hành volume-modifier-for-k8s sidecar, cho phép cập nhật online các đặc điểm volume bằng cách áp dụng annotations lên PVC. Mặc dù đây là giải pháp quan trọng, AWS đã hợp tác với các nhà cung cấp lưu trữ khác để tạo một giải pháp sửa đổi volume được cung cấp dưới dạng native Kubernetes API. Trong năm qua, AWS đã làm việc với cộng đồng Kubernetes để phát hành VolumeAttributesClass Kubernetes Enhancement, đã đạt beta trong Kubernetes 1.31. Dù tính năng bị disable mặc định trong upstream Kubernetes, nó được enable tự động cho bạn trong Amazon Elastic Kubernetes Service (Amazon EKS) 1.31.

Bắt đầu từ Amazon EKS 1.31, bạn có thể sử dụng VolumeAttributesClass (VAC) để sửa đổi volume type, IOPS hoặc throughput của EBS volumes **mà không cần volume-modifier-for-k8s sidecar**. Hơn nữa, bạn có thể dùng VAC để thêm, chỉnh sửa và xóa AWS resource tags từ volumes của bạn. Amazon EBS CSI driver enable tính năng này mặc định khi bạn nâng cấp lên phiên bản 1.35.0 hoặc mới hơn.

Sử dụng Amazon EKS 1.31 và Amazon EBS CSI driver 1.35.0, bạn đã có thể bắt đầu dùng VAC thay cho PVC annotations. Trong hai phần tiếp theo, chúng tôi giới thiệu VolumeAttributesClasses và cách bật tính năng này trên cluster. Sau đó, chúng tôi hướng dẫn ba workflow phổ biến để sửa đổi volumes với VAC:
1. Điều chỉnh throughput và IOPS của volumes.
2. Di chuyển sang EBS gp3 volumes để tiết kiệm đến 20% chi phí mỗi GB so với gp2.
3. Sửa đổi resource tags của EBS volume để tự động hóa workflow backup bằng Amazon Data Lifecycle Manager.

## Tổng quan về giải pháp
Cluster operators có thể dựa vào Amazon EBS CSI driver để quản lý declarative persistent volumes. Bạn có thể yêu cầu persistent storage cho workload bằng PVC với size, SC và VAC cụ thể.

Một VAC bao gồm tên, driverName của CSI driver, và danh sách mutable parameters cụ thể đối với storage provider như Amazon EBS.

Các tham số mutable EBS volume như throughput, IOPS, volume types và resource tags có thể được chỉ định trong VAC:
```bash
*apiVersion: storage.k8s.io/v1beta1  
kind: VolumeAttributesClass  
metadata:  
  name: ebs-blog-gp3-standard-performance  
driverName: ebs.csi.aws.com  
parameters:  
  type: gp3  
  iops: "3000"  
  throughput: "125"  
  tagSpecification_1: "performance=standard"*  
```
Bạn có thể thêm VAC vào PVC bằng trường spec.volumeAttributesClassName:
```bash
*apiVersion: v1  
kind: PersistentVolumeClaim  
metadata:  
  name: ebs-blog-overview  
spec: 
  ...  
  volumeAttributesClassName: ebs-blog-gp3-standard-performance*  
```
Volume được provision với các parameters trong VAC và SC, với VAC **ưu tiên hơn** khi có xung đột. VAC của PVC cũng override mọi thay đổi dựa trên annotations, và ngăn các thay đổi annotation trong tương lai.

Việc tách riêng VAC mang lại lợi ích khi các tổ chức tách biệt vai trò vận hành cluster và triển khai ứng dụng. Operator có thể tạo SC và VAC ở phạm vi cluster, sau đó application developers có thể sử dụng chúng trong PVC thuộc namespace của họ.

## Điều kiện tiên quyết
Trên Amazon EKS 1.31 trở lên, VolumeAttributesClass feature gate và API storage.k8s.io/v1beta1 được enable tự động trên control plane. Ngoài ra, bạn phải sử dụng Amazon EBS CSI driver v1.35.0 hoặc mới hơn, được cài đặt qua Amazon EKS Managed add-on v1.35.0-eksbuild.2 hoặc Helm chart v2.35.1.

Nếu bạn vận hành self-managed Kubernetes v1.31 (như kOps), bạn phải enable VolumeAttributesClass feature gate trên kube-apiserver, kube-scheduler và kube-controller-manager, và enable storage.k8s.io/v1beta1 API qua runtime-config của kube-apiserver.

Tham khảo tài liệu Kubernetes VolumeAttributesClass để xem đầy đủ yêu cầu.

Để sửa đổi Amazon EBS resource tags qua VAC, đảm bảo bạn đính kèm IAM Policy sau vào role của Amazon EBS CSI driver:
```bash
*{  
  "Version": "2012-10-17",  
  "Statement": [  
    {  
      "Effect": "Allow",  
      "Action": [  
        "ec2:CreateTags"  
      ],  
      "Resource": [  
        "arn:aws:ec2:*:*:volume/*",  
        "arn:aws:ec2:*:*:snapshot/*"  
      ]  
    }  
  ]  
}*  
```
## Hướng dẫn

Các bước sau sẽ hướng dẫn qua giải pháp này.

#### Cung cấp một khối lượng và tăng hiệu suất của nó

Amazon EKS 1.31 không có SC mặc định. Chúng ta phải tạo SC sau:
```bash
$ kubectl apply -f - <<EOF  
apiVersion: storage.k8s.io/v1  
kind: StorageClass  
metadata:  
  name: ebs-blog-sc  
provisioner: ebs.csi.aws.com  
allowVolumeExpansion: true  
EOF  
```
Dưới đây là hai VAC ví dụ, mỗi cái có QoS khác nhau:
```bash 
$ kubectl apply -f - <<EOF  
apiVersion: storage.k8s.io/v1beta1  
kind: VolumeAttributesClass  
metadata:  
  name: ebs-blog-gp3-standard-performance  
driverName: ebs.csi.aws.com  
parameters:  
  type: gp3  
  iops: "3000"  
  throughput: "125"  
---  
apiVersion: storage.k8s.io/v1beta1  
kind: VolumeAttributesClass  
metadata:  
  name: ebs-blog-gp3-increased-performance  
driverName: ebs.csi.aws.com  
parameters:  
  type: gp3  
  iops: "4000"  
  throughput: "130"  
EOF  
```
Provision volume với VAC standard:
```bash
$ kubectl apply -f - <<EOF  
apiVersion: v1  
kind: PersistentVolumeClaim  
metadata:  
  name: ebs-blog-claim  
spec: 
  accessModes:  
    - ReadWriteOnce  
  storageClassName: ebs-blog-sc  
  volumeAttributesClassName: ebs-blog-gp3-standard-performance  
  resources:  
    requests: 
      storage: 10Gi  
EOF  
```
Để tăng hiệu năng, bạn patch PVC sang VAC mới:
```bash
$ kubectl patch pvc ebs-blog-claim -p '{"spec": { "volumeAttributesClassName": "ebs-blog-gp3-increased-performance" }}'
```
EBS CSI driver sẽ thấy VAC hiện tại và VAC mong muốn khác nhau, sửa đổi volume và update PV.

Bạn chỉ có thể sửa một volume mỗi 6 giờ theo tài liệu EBS. Vì vậy bạn nên gộp tăng size PVC và VAC update vào một patch:
```bash
$ kubectl patch pvc ebs-blog-claim --type json -p '[{"op": "replace", "path": "/spec/volumeAttributesClassName", "value": "ebs-blog-gp3-increased-performance" }, {"op": "replace", "path": "/spec/resources/requests/storage", "value": "11Gi"}]'
```
Nếu không bạn sẽ thấy lỗi sau trên PVC:
```bash
VolumeResizeFailed: ... VolumeModificationRateExceeded: You've reached the maximum modification rate per volume limit. Wait at least 6 hours between modifications per EBS volume.
```
#### Tiết kiệm chi phí bằng cách di chuyển sang ổ đĩa gp3
VAC có thể dùng với PVC đã tạo từ trước không có VAC, rất hữu ích để migrate từ gp2 sang gp3. EBS gp3 cho phép provision IOPS và throughput độc lập với storage size. Bạn có thể migrate gp2 → gp3 trong mọi use case trước đây, và có thể tiết kiệm đến 20% chi phí.

Dưới đây là ví dụ workload stateful dùng gp2 volume:

<style>
pre, code {
  background: gray !important;
  color: black !important;
}
</style>
```bash
$ kubectl apply -f - <<EOF
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: ebs-blog-migration
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: ebs-blog-migration
  resources:
    requests:
      storage: 1Gi
---
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: ebs-blog-migration
provisioner: ebs.csi.aws.com
allowVolumeExpansion: true
volumeBindingMode: WaitForFirstConsumer
parameters:
  type: gp2
---
apiVersion: v1
kind: Pod
metadata:
  name: ebs-blog-migration-app
spec:
  containers:
  - name: ebs-blog-app
    image: centos
    command: ["/bin/sh"]
    args: ["-c", "while true; do echo $(date -u) >> /data/out.txt; sleep 5; done"]
    volumeMounts:
    - name: persistent-storage
      mountPath: /data
  volumes:
  - name: persistent-storage
    persistentVolumeClaim:
      claimName: ebs-blog-migration
EOF
```

Để migrate volume sang gp3, trước tiên apply VAC:
```bash
$ kubectl apply -f - <<EOF
apiVersion: storage.k8s.io/v1beta1
kind: VolumeAttributesClass
metadata:
  name: ebs-blog-gp3 
driverName: ebs.csi.aws.com
parameters:
  type: gp3
EOF
```

Sau đó patch PVC:
```bash 
$ kubectl patch pvc ebs-blog-migration -p '{"spec": {"volumeAttributesClassName": "ebs-blog-gp3"}}'
```
Lưu ý: tính đến Kubernetes 1.31, bạn không thể sửa đổi volumes tham chiếu SC kiểu in-tree. Hãy đảm bảo SC dùng provisioner ebs.csi.aws.com, không phải kubernetes.io/aws-ebs.

#### Workflow modify tags

Để quản lý dễ dàng hơn EBS volumes, bạn có thể dùng tags. Tags là các cặp key-value gán cho AWS resources, cho phép phân loại tài nguyên theo mục đích, owner hoặc environment. Với nhiều volumes, tags giúp xác định hoặc nhóm tài nguyên.

EBS CSI driver cho phép thêm, thay thế, xóa volume tags qua parameter tagSpecification trong VAC.

Ngoài ra, tags có thể dùng với Amazon Data Lifecycle Manager để tự động backup volumes. EBS Snapshots ghi lại trạng thái volume tại thời điểm cụ thể để khôi phục khi mất dữ liệu. Bạn có thể tạo chính sách DLM backup dựa vào tags.

Ví dụ chính sách sau tạo snapshot mỗi ngày cho các volume dùng VAC ebs-blog-daily-backup:

```bash
$ aws dlm get-lifecycle-policies
{
    "Policies": [
        {
            "PolicyId": "policy-045203fd0b8e2bf79",
            "Description": "This policy creates daily backups of my K8s PVs",
            "State": "ENABLED",
            "Tags": {
                "backup-interval": "daily"
            },
            "PolicyType": "EBS_SNAPSHOT_MANAGEMENT",
            "DefaultPolicy": false
        }
    ]
}
```

## Dọn dẹp

Để tránh phát sinh chi phí, xóa các resources đã tạo:
```bash 
kubectl delete pod ebs-blog-migration-app
kubectl delete pvc ebs-blog-claim
kubectl delete pvc ebs-blog-migration
kubectl delete vac ebs-blog-gp3
kubectl delete vac ebs-blog-gp3-increased-performance
kubectl delete vac ebs-blog-gp3-standard-performance
kubectl delete vac ebs-blog-daily-backup 
kubectl delete sc ebs-blog-sc
kubectl delete sc ebs-blog-migration
```
Bạn có thể kiểm tra việc xóa volumes trong EC2 console.

## Phần kết luận

Trong bài viết này, chúng tôi khám phá cách sửa đổi Amazon EBS volumes trên Kubernetes với VolumeAttributesClasses. Tính năng mới này giúp bạn tinh chỉnh hiệu năng volume bằng cách cập nhật volume type, IOPS và throughput mà không cần downtime. Hơn nữa, bạn có thể tự động hóa backup bằng cách chỉnh sửa resource tags phù hợp với Amazon Data Lifecycle Manager.

