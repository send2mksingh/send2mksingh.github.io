---
 layout: post
 title: OpenStack-Team-Discussion
---

```
Open + Stack = Stack of opensource components.
We have 30 components
like: keystone
Cinder
Neutron
Nova

```

**OpenStack** is the open source cloud computing platform where we can create our own private, public or hybrid kind of cloud evn as infrastrure as a service.

Community hardware - is the computers or components that are readily available these are cheap and easily available.

Bare Metal - We are working directly on the Physical system, hardware without installing any OS.
Benefits - complete access of resources, flexibility to choose their own OS.

Iass - [networking, storage, servers and virtualization], creating vm and giving to clients, deploying openstack on raw infra

Pass - [networking, storage, servers and virtualization, OS, middleware, runtime], created any web server giving url to client to access, suppose client having own amazon client or data center we can create app for client and deploy on amazon client's account.

Saas - Pass - [networking, storage, servers and virtualization, OS, middleware, runtime, data and application], we are taking care of everything.


Private cloud - is the cloud that is not shared with any other org. like coredge, yotta and adani we deployed private cloud. eg. on premises, owned by users.

Public cloud - Data center is common to all and hosted in providers premises.

Hybrid - few services from private and few from public. suppose for apps we are using Public cloud and database we can use private on premises servers.


**Why OpenStack**
- Affordable
- large community
- Vendor Nuetral
- Reliable


if any request is coming from horizon to create vm, then nova api , then decides which compute node is available with required resources. 

**Compute Node** is the hardware where our VM provisioned.

**RPC** internal components are using for this to communicate with each other.

**API** for communication with any openstack service like glance, cinder - glance api and cinder api.

**Glance** - interact with api and glance registery (maintains the status of images available and more details)

![Example image](https://camo.githubusercontent.com/5e1100a145123f5ae9643cbdece5f1054e96ac4ab59fa41669f4b93fafef9b0b/687474703a2f2f692e696d6775722e636f6d2f7169594d316e392e706e67)


**Keystone**
- Authentication : verify the identity of the user or service.
- Authorization : Roles or permission related to services access.


**Source openrc** contains users details and when we do source openrc these get stored in the environment, where we are working or executing and used by keystone.