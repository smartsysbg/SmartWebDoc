#

**SmartWEB** can operate in single instance mode and also in multiple instances mode, or the so called `Multitenancy Mode`. In multitenancy mode multiple WEB sites can be launched in one web server, all using the same binaries, but their data is isolated. The different architectures and data flows to external data sources are ilustrated further in this chapter.  

---

## Single Tenant Architecture
This is the simplest architecture that consists of one instance of **SmartWEB** application, one database and optionally `Redis Cache` for caching the rendered content. All components can be installed on the same or separate servers. This architecture does not provide redundancy and is suitable for hosting non-critical applications and also for testing purposes.  

![](./media/architectural-considerations/single-tenant.png)

---

## Multitenancy Architecture

This architecture also does not provide redundancy, but it makes optimal use of the hardware resources. Here we have one instance of **SmartWEB** application and separate databases for each tenant. Again, all components can be installed on a single server or on separate servers and the `Redis Cache` server is optional.  

A `tenant` is a standalone functioning **SmartWEB** site. All tenants running under the same instance of the **SmartWEB** application use the same `binary code`, but their data is isolated. There are two ways to isolate data for individual tenants.  

> -  A separate database is created for each tenant.  
> -  A separate set of tables are created for each tenant with the tenant name prefixed, but all tables for all tenants are stored in a single database.  

We recommend using the first option, because the database in this case is better structured and easier to manage. When the tenants are in separate databases, it can be very easy to back up the individual databases. With the help of such a backup the corresponding **SmartWEB** sites can be easily moved to another server. Also when a tenant needs to be deleted, in the database server we only need to delete the corresponding database and not delete tables in the common database. The following picture shows the architecture of this mode of operation, illustrating separate databases for each tenant.  

![](./media/architectural-considerations/multitenancy.png)

In `Multitenancy` mode, the base tenant `URL` is formed by adding `tepant-id` as an additional segment to the base `URL` of the **SmartWEB** application. There is no limit to the number of tenants running on **SmartWEB** application server. It depends on hosting server performance and tenants load.  


!!!tip "Note" 
    In `Multitenancy` mode, the tenant that is accessed with the base application `URL` is called the `Default` tenant. In this tenant, no user content is normally created and no users are configured. It is only used to manage the other tenants and only the `Super User` has access to it.  

This architecture also provides upgrade convenience because all sites use the same `binary code`. The disadvantage is that when shutting down application server for upgrade or other maintenance tasks, all sites hosted as tenants on a given application server stop working. The architecture is suitable for hosting multiple non-critical cloud based applications, because it optimizes the resources used and hence results in reduced costs. A detailed description of the configuration and management when **SmartWEB** runs in this architecture can be found in the [Multitenancy](/multitenancy) chapter.  

---

## Load Balancing

For `mission-critical` applications, **SmartWEB** offers an architecture that implements redundancy. For this purpose, a `Load Balancer`  is used to route traffic to the different servers in the schema. The following figure shows an architecture that uses `Load Balancer`  in combination with `Multitenancy`  running on three application servers.  

![](./media/architectural-considerations/load-balancing-and-multitenancy.png)

There is no limit to the number of servers that can be included in such a redundant architecture. These are usually `cloud-based` systems running on virtual machines. This is a typical architecture providing redundancy and at the same time good utilization of server resources. At any point in time, any server can be disconnected from the scheme to perform maintenance activities and this will remain transparent to users, because the remaining servers will continue to serve them. In this architecture the `Redis Cache` server is a mandatory component, unlike the other two modes we discussed above. The servers use `Redis Cache` for synchronization. For example, if you create a new tenant on one of the application servers, that tenant will automatically appear on the other servers in the schema. The same tenants running on different servers use the same relational database, and `Load Balancer` using the rules route user requests to tenants on the different application servers.  

!!!attention "Imortant" 
    It is important to note that all requests on a given user session must always be directed to the same tenant. Therefore, `Load Balancer` must support `Client Affinity Preserve Host Header` mode.  

---

#### Summary

In this chapter, we have introduced the basic architectures of **SmartWEB** operation. Everything in this documentation is valid for both single tenant and multitenant sites, unless some feature is explicitly discussed for the corresponding architecture. The [Multitenancy](/multitenancy) chapter describes the configuration and management of the tenants, when the system is running in multitenancy mode. The [Load Balancing](/load-balancing) chapter describes the configuration and management when the system is working with `Load Balancer` at the front.  