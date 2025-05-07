# Definition of EAASI User Types

## Purpose
In order to properly define user stories and feature development for the EAASI roadmap, common understanding and definition is needed for the types of users that interact with an EAASI system and the level of control they are intended to have over resources and permissions in the application. These definitions are symbolic and are intended to give a common vocabulary for further defining and scoping implementation in the stack.

## Type and Role Definition

There are seven types of user who may interact with or within any given EAASI deployment. In order of highest level of control and access over the system to lowest:

- [System Administrator](#system-administrator)
- [Deployment Administrator](#deployment-administrator)
- [Organization Administrator](#organization-administrator)
- [Configuration User](#configuration-user)
- [Access User](#access-user)
- [Public User](#public-user)
- [Share-Link User](#share-link-user)

### System Administrator
A System Administrator refers to a user with control over the host server itself. They install, configure, and maintain smooth operation of the EAASI deployment and related computing infrastructure (compute power and storage), but are not explicitly or automatically assigned any role(s) within the application.

Security and access control for System Administrators to data on-disk is handled and configured by the server operating system, network, and/or storage provider, **not** managed by EAASI.

(This user type may be referred to in shorthand as "System Admin" or "sysadmin")

### Deployment Administrator
A Deployment Administrator has power over user management and related, account-dependent usage within an EAASI deployment. They have oversight in the EAASI application over, e.g.: 

- the creation of Organizations
- creation of initial Organization Admin accounts for each Organization
- the definition of any infrastructural quotas or restrictions per-Organization 

Deployment Administrators *may be* (but are not *limited to*) the same person/individual as the System Administrator. An initial Deployment Administrator is set by a System Administrator during [server configuration and deployment](https://EAASI.gitlab.io/EAASI_user_handbook/overview/install/setup.html#configuring-EAASI-installer).

Deployment Administrators require the ability to at least temporarily access and manage individual Organizations and/or user accounts and their associated resources for the purposes of troubleshooting and service management. The precise mechanisms for this power should be transparently designed and communicated to address potential concerns of privacy and security in situations where an EAASI deployment is offered as a service. 

(This user type should be considered equivalent to any discussion or reference to "superadmins" in legacy development documentation or in deployment instructions. This role may be referred to in shorthand as "Deployment Admin")

### Organization Administrator
An Organization Adminstrator has power over user and resource management for a single Organization within an EAASI deployment. They have oversight in the EAASI application over, e.g.:

- adding additional user accounts (including more Organization Administrators) to an Organization
- adjusting the permission level of existing user accounts within their Organization
- sharing of any Organization resources to users in another Organization

Organization Administrators should also have, at a minimum and within the abilities and/or limitations of the system, *influence* (if not direct *control*) over other user accounts and resources within their Organization insofar as they may affect Organization-level quotas on computing infrastructure or deployment administration (storage space, CPU/RAM, total number of user accounts, etc.) The precise mechanisms for this power should be transparently designed and communicated to address potential concerns of privacy and security in situations where an EAASI deployment is offered as a service.

Organization Administrators should also wield some measure of ability to edit (including application metadata, as well as access/permissions/visibility) any and all resources that have been shared to an entire Organization.

(This user type may be referred to in shorthand as "Organization Admin" or "Org Admin")

### Configuration User
Configuration Users have power over resource creation and management within a single Organization within an EAASI deployment. Unless the same user/account is also an Organization Administrator, they should largely have oversight or power only over resources that their own account specifically created or imported, or that have been shared (by other Configuration Users) to an entire Organization. This includes the ability to share their private resources to any and all other accounts within their Organization (but not to share those resources to another Organization).

Configuration Users have no power or oversight over user accounts other than their own, and can not add further accounts to their Organization.

(This user type may be referred to in shorthand as "Config User")

### Access User
Among authenticated user accounts, Access Users should have the lowest level of power over and visibility within the system. They are assumed to be "end users" whose primary interaction with the system is to consume resources created by Configuration Users to fit an Access User's particular requirements or use case.

They should be limited in the resources they can see and use only those resources that have been specifically shared or assigned to their account (so in some ways they are a member of an Organization but excluded from the pool of resources that Configuration Users in an Organization may want to generally share with each other).

(In some cases of legacy documentation, this role may be equivalent to discussion or references to "guest" users. However, there is potential overlap in features discussed for "guest" users with those defined for non-authenticated Public Users - see [below](#public-user) - so any and all legacy documentation referring to "guest" users should be further scoped or clarified before being placed on the active development roadmap)

### Public User
Public User refers to any user who interacts with the data or metadata present in an EAASI deployment without an authenticated user account. They can not edit or create any resources within the system, and should only be able to view metadata or start Environment sessions for resources that have been so permitted by an Organization Administrator.

(In some cases of legacy documentation, this type of user may be equivalent to discussion or references to "guest" users. However, there is potential overlap in features discussed for "guest" users with those defined for Access Users - see [above](#access-user) - so any and all legacy documentation referring to "guest" users should be further scoped or clarified before being placed on the active development roadmap)

### Share-Link User
A Share-Link User is a particular subset of [Public User](#public-user) who can start Environment sessions and interact with Environments that have been embedded into a third-party system or interface. This user type is unique to this particular functionality and related workflows.

(All Share-Link Users are also Public Users but not all Public Users are necessarily Share-Link Users. In some cases of legacy documentation, this type of user may be equivalent to discussion or ferences to "guest" users. However, there is potential overlap in features discussed for "guest" users with those defined for Access Users or other Public Users - see above - so any and all legacy documentation referring to "guest" users should be further scoped or clarified before being placed on the active development roadmap)
