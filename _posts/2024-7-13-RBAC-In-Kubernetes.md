---
 layout: post
 title: RBAC In Kubernetes
---

**RBAC**kubernetes rbac can be broadly divided into two parts so the first part can be 1. users and 2. service or application that you are running.

**User Management**as Devops Engineer or Kubernetes administrators your primary responsibility is to define the access so, if there is any development team and qa team, how do you define which team will have which type of access or rights so that they can impact environment, same we can achieve by using RBAC.

**What is Role Based Access Control**depeding upon the role of the person you would define the access.


**Service/Application**now how are you going to deal with services let's you create a pod, so next question is what access does this pod will have on Kubernetes cluster, should this pod have access to Configmaps or secrets, suppose as part of your application you want to read Configmap or secrets, so two primary responsiblities of RBAC is user management as well as managing the access of the services that are running on the cluster.

```
Important things to keep in mind-
3 things that can define the RBAC in Kubernetes

1. Service Accounts/Users
2. Roles/Cluster Role
3. Role binding/CRB

```


- Kubernetes does not perform user management itself basically it offloads the user management to any identity providers,
eg. if you are using EKS kubernetes then it suggests to use IAM users to manage, we can also user some identity brokers like **Key Clock**its very popular and many people manage their kubernetes identity using.

**Service accounts** its just like yaml file everybody can create.

**Role and Role Bindig**let's you are creating a role and want to assign to a developer so what you say, they should have access to pods and configmaps, they should have access to secrets within the same namespace, to have access within the single namespace you will create a role and if they want to have access across the cluster then you will create cluster role, next you have to attach this role to the users for same you use role binding, simple role is a yaml file where we can write all the terms and conditions.


**Suppose you have service account, user and roles so by using role binding you can bind both of them together.

**Roles/Cluster Role**if you are creating role within the specific namespace then it will be called as Role and if it is created within the scope of cluster then it is called as Cluster Role.

**Role binding/CRB**   
