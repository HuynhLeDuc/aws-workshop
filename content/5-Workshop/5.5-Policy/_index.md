title : "On-premise testing"

weight : 5
chapter : false
pre : " <b> 5.5 </b> "
---

In this section, we will deploy and test the AI ​​model in an **on-premise** environment. This is an important step to evaluate the feasibility and performance of the system in real conditions before putting it into production
1.
- We will connect via python (boto3)
![alt text](/images/5-Workshop/5.5-Policy/onpr.png)

- First we must know our region, Agent ID, Aliases Id

![alt text](/images/5-Workshop/5.5-Policy/onpr1.png)

- Must have accesskey Id, secret key:
> *Note that these 2 keys cannot be revealed, otherwise outsiders will use the service and you will lose money*

![alt text](/images/5-Workshop/5.5-Policy/onpr3.png)

2. Try promt to see if it returns a result or not, if it does, it is considered successful.

![alt text](/images/5-Workshop/5.5-Policy/onpr4.png)