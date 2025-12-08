---
title: "Blog 3"

weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---


# Modify Amazon EBS volumes on Kubernetes with Volume Attributes Classes
<span style="font-size:13px; color: #737070ff;">
by pmm on 05 MAR 2025 in | 
</span>
<small>
<a href="https://aws.amazon.com/blogs/containers/category/containers/">Containers</a>, 
<a href="https://aws.amazon.com/blogs/containers/category/post-types/technical-how-to/" style="color:#0073bb; text-decoration:none;">Technical How-to</a>,  
<a href="https://aws.amazon.com/blogs/containers/modify-amazon-ebs-volumes-on-kubernetes-with-volume-attributes-classes/" style="color:#0073bb; text-decoration:none;">Permalink</a>, 
</small>

*This post was jointly authored by Kevin Liu (Senior PMT), Jens-Uwe Walther (Senior STAM-Containers), and Drew Sirenko (Software Dev Engineer).*

## Introduction
In this post, we explore how to modify Amazon Elastic Block Store (Amazon EBS) volumes on Kubernetes without application downtime. Learn how to use the VolumeAttributesClass API alongside the Amazon EBS Container Storage Interface (CSI) driver to tune provisioned performance, migrate to gp3 volumes, and automate your data backup workflows.

Modern containerized applications that use persistent storage, such as data analytics, databases, or video encoding and decoding, need a wide variety of storage characteristics such as low latency, high throughput, or more. Amazon EBS is a good fit for these workloads. EBS volumes offer different storage types, configurable storage attributes like IOPS and throughput, and the ability to modify these properties without downtime.

If you deploy your stateful container workloads on Kubernetes, then you can use the Amazon EBS CSI driver to provision and manage EBS volumes on your behalf. When you create Persistent Volume Claim (PVC) resources with a specified size and a Storage Class (SC), Kubernetes works with the Amazon EBS CSI driver to deploy your workloads with the necessary storage by creating, attaching, and formatting EBS volumes on your behalf.

Changing storage characteristics of volumes in Kubernetes used to be an offline action, necessitating that cluster operators create another SC, and migrate to new PVC and Persistent Volume (PV) resources. This process necessitated application downtime and impacted availability. That’s why, in 2023, AWS released the volume-modifier-for-k8s sidecar, enabling online updates of volumes’ types and performance characteristics by applying annotations to PVCs. Although it was important to provide a solution to users, AWS worked with other storage providers to create a volume modification solution that was available as a native Kubernetes API. Over the past year AWS has worked with the Kubernetes community to release the VolumeAttributesClass Kubernetes Enhancement, which has reached beta in Kubernetes 1.31. Although the feature is disabled by default in upstream Kubernetes, it is automatically enabled for you in your Amazon Elastic Kubernetes Service (Amazon EKS) 1.31 clusters.

Starting in Amazon EKS 1.31, you can use the VolumeAttributesClass (VAC) feature to modify the volume type, IOPS, or throughput of your EBS volumes without the volume-modifier-for-k8s sidecar. Moreover, you can use VACs to add, edit, and remove AWS resource tags from your volumes. The Amazon EBS CSI driver enables this feature by default when you upgrade to version 1.35.0 or later.

Using Amazon EKS 1.31 and Amazon EBS CSI driver 1.35.0, you can already start using VACs instead of PVC annotations. In the next two sections, we introduce VolumeAttributesClasses and show you how to enable the feature on your cluster. Then, we walk through three common workflows for modifying your volumes with VACs:
1. Tuning the throughput and input output operations per second (IOPS) performance characteristics of your volumes.
2. Migrating to EBS gp3 volumes for up to 20% lower price per GB as compared to gp2 volumes.
3. Modifying your EBS volume resource tags to automate your data backup workflow with Amazon Data Lifecycle Manager.

## Solution overview
Cluster operators can rely on the Amazon EBS CSI driver to declaratively manage their persistent volumes. You can request persistent storage for your workloads by creating PVC resources with a particular size, SC, and VAC.

A VAC is composed of its name, the driverName of the CSI driver, and a list of mutable parameters specific to a storage-provider such as Amazon EBS.

Mutable EBS volume parameters, such as throughput, IOPS, volume types, and AWS resource tags can be specified in VAC resources:


> *apiVersion: storage.k8s.io/v1beta1  
kind: VolumeAttributesClass  
metadata:  
  name: ebs-blog-gp3-standard-performance  
driverName: ebs.csi.aws.com  
parameters:  
  type: gp3  
  iops: "3000"  
  throughput: "125"  
  tagSpecification_1: "performance=standard"*  

You can add a VAC to a PVC using the spec.volumeAttributesClassName field:
>*apiVersion: v1  
kind: PersistentVolumeClaim  
metadata:  
  name: ebs-blog-overview  
spec: 
  ...  
  volumeAttributesClassName: ebs-blog-gp3-standard-performance*  

The volume is provisioned with the parameters specified in both the VAC and SC, with the VAC parameters taking precedence over any conflicting parameters. A PVC’s VAC also overrides all annotation-based modifications, and prevents future annotation-based modifications.

This separate VAC resource benefits organizations that split responsibilities between teams that operate the cluster and teams that deploy applications to it. Cluster operators can create cluster-wide SC and VAC objects, which then can be consumed by application developers in their name-spaced PVC resources.

## Prerequisites
On Amazon EKS 1.31 or later, the beta VolumeAttributesClass feature gate and storage.k8s.io/v1beta1 API group are automatically enabled on your cluster’s control plane components. Furthermore, you must use Amazon EBS CSI driver version v1.35.0 or later, which is installed by Amazon EKS Managed add-on v1.35.0-eksbuild.2 or Helm chart v2.35.1.

If you operate a self-managed (for example, kOps) Kubernetes v1.31 cluster, you must enable the VolumeAttributesClass feature gate on the kube-apiserver, kube-scheduler, and kube-controller-manager, as well as enable the storage.k8s.io/v1beta1 API group through the kube-apiserver runtime-config.

Consult the Kubernetes VolumeAttributesClass documentation for the complete list of requirements.

To modify Amazon EBS resource tags through VACs, make sure that you attach the following AWS Identity and Access Management (IAM) Policy to the role used by your Amazon EBS CSI driver:

>*{  
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
## Walkthrough
The following steps walk you through this solution.

#### Provision a volume, and increase its performance
Amazon EKS 1.31 doesn’t come with an SC by default. We must create the following SC:
>$ kubectl apply -f - <<EOF  
apiVersion: storage.k8s.io/v1  
kind: StorageClass  
metadata:  
  name: ebs-blog-sc  
provisioner: ebs.csi.aws.com  
allowVolumeExpansion: true  
EOF  

Here are two example VAC resources, each with different volume quality-of-service parameters:

>$ kubectl apply -f - <<EOF  
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
>apiVersion: storage.k8s.io/v1beta1  
kind: VolumeAttributesClass  
metadata:  
  name: ebs-blog-gp3-increased-performance  
driverName: ebs.csi.aws.com  
parameters:  
  type: gp3  
  iops: "4000"  
  throughput: "130"  
EOF  

Provision a volume with the standard performance VAC:

>$ kubectl apply -f - <<EOF  
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

For higher performance, you can patch the PVC to point to the new ebs-blog-gp3-increased-performance VAC:

>$ kubectl patch pvc ebs-blog-claim -p '{"spec": { "volumeAttributesClassName": "ebs-blog-gp3-increased-performance" }}'

The Amazon EBS CSI driver observes that the PVC’s current and desired VACs differ, modifies the EBS volume, and updates the PV resource to the new VAC.

You may only perform one volume modification per six hour period according to Amazon EBS documentation. Therefore, you should merge PVC storage size increases with VAC changes into one Kubernetes patch:

>$ kubectl patch pvc ebs-blog-claim --type json -p '[{"op": "replace", "path": "/spec/volumeAttributesClassName", "value": "ebs-blog-gp3-increased-performance" }, {"op": "replace", "path": "/spec/resources/requests/storage", "value": "11Gi"}]'

Otherwise, you observe the following failure event on the PVC resource:

>VolumeResizeFailed: "pvc-716766d1-58d5-411b-8d4a-7671ef9894e9" by resizer "ebs.csi.aws.com" failed… VolumeModificationRateExceeded: You've reached the maximum modification rate per volume limit. Wait at least 6 hours between modifications per EBS volume.

#### Save costs by migrating to gp3 volumes

VolumeAttributesClasses can be used with existing PersistentVolumeClaims created without a VAC. This is especially useful for migrating from gp2 to gp3 volumes. EBS gp3 volumes allow you to provision IOPS and throughput independent of storage size. You can migrate to gp3 volumes in any use case where gp2 volumes were used, and may see cost savings of up to 20% because of this independence. If you are looking for even higher performance, then you can scale gp3 volumes up to 1,000 MiB/s, four times higher than the maximum throughput of gp2 volumes.

Here we create a stateful workload that initially relies on a gp2 volume:

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


To migrate this volume to gp3, first apply the VAC resource to your cluster:
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
Then patch its associated PVC:
>$ kubectl patch pvc ebs-blog-migration -p '{"spec": {"volumeAttributesClassName": "ebs-blog-gp3"}}'
Note, as of Kubernetes version 1.31, you cannot modify volumes that reference an in-tree SC via VAC. Ensure that the SC associated with the volume you are modifying references provisioner ebs.csi.aws.com, not kubernetes.io/aws-ebs.

### Workflow modify tags
To ease management of your EBS volumes you can use tags. Tags are key-value pairs that you assign to your AWS resources, enabling you to categorize them by purpose, owner, or environment. If you have many volumes in your account, then tags can help you identify a specific volume, or group related resources. The Amazon EBS CSI driver allows you to add, replace, and clear volume resource tags through the tagSpecification VAC parameter.

Beyond organization, volume tags can be used with Amazon Data Lifecycle Manager policies to safely back up your EBS volumes. Amazon EBS Snapshots capture the state of a volume at a specific point in time, allowing for recovery in case of data loss or corruption. To automate the creation, retention, and deletion of these snapshots, you can create a volume Amazon Data Lifecycle Manager policy targeting volumes with specific resource tags.

For example, the following policy creates a daily snapshot of any volume associated with theebs-blog-daily-backup VAC:
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
## Cleaning up
To avoid incurring further costs, delete any example Kubernetes and AWS resources that you provisioned for these examples.
Delete stateful workload example resources:
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

You can confirm deletion of the EBS volumes through the Amazon Elastic Compute Cloud (Amazon EC2 ) console.


## Conclusion
In this post we explored how to modify Amazon EBS volumes on Kubernetes with VolumeAttributesClasses. This new feature helps you tune the performance characteristics of your stateful workloads by updating volume type, IOPS, and throughput without application downtime. Furthermore, automate your data backup workflows by modifying resource tags to match your Amazon Data Lifecycle Manager policies.