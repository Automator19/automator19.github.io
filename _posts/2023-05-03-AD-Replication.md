---
layout: post
title: AD Replication Types and Configuration
category: [Windows]
---
.
Active Directory Infrastructure is depending on healthy replication. Every domain controller in the network should aware of every change which has made. When domain controller triggers a sync, it passes the data through the physical network to the destination.

In active directory environment, there are mainly two types of replications.

1. Intra-Site Replication 
2. Inter-Site Replication

# Intra-Site Replication

![External](/assets/images/Intra-Site-Replication.png)

As the name confirms, this covers the replication happens with in a site. By default, (according to Microsoft) any domain controller will aware of any directory update within 15 seconds. Within site despite the number of domain controllers, any directory update will be replicate in less than one minute. 
Within the site, the replication connections are performing in ring topology. Which mean an any give domain controller have two replication links (of cause if there is minimum of three domain controllers). this architecture will prevent domain controllers having endless replication loops. As example if there are 5 domain controllers and if all are connected to each other with one-to-one connection each domain controller will have 4 connection and when there is an update in one of the domain controller it will need to advertise it to 4 domain controllers. then the first one to receive update will advertise to its 4 connected domain controllers and its go on and on. It will be too much replication processes to advertise, listen and sort out the conflicts. But in ring topology, despite the number of domain controllers in the site, any given domain controller only need to advertise or listen to two domain controllers in any given time. This replication topology is no need to configure manually and active directory will automatically determine the connections it need to make. When number of domain controllers grow, the replication time can grow as well as its in ring topology. But to avoid the latency active directory will create additional connections. This is also determined automatically and we do not need to worry about these replication connections. 

# Configuring Intra Site replication 

1. Open **Active Directory Sites and Services.**
2. Select a Site (Blue icon)
3. Go down to NTDS Settings.
4. Click on the connection and properties
5. Click on Change Schedule and Adjust accordingly. 


# Inter-Site Replication

![External](/assets/images/Inter-Site-Replication.png)

If active directory infrastructure contains more than one site, a change happens in one site need to replicate over to other sites. This is called as inter-site replication and its topology is different from the intra-site replication. Replication with in site is always benefited from the high-speed links. But when it comes to between sites bandwidth, latency and reliability comes to considerations. In previous section, we discussed about site-links, site costs and replication schedules when we can use to control the inter-site replication. 

When it comes to inter-site, the replication will happen via site links. The replication with in each site still uses the ring topology. In above example let’s assume an object been added to REBEL-DC-02 in London Site. Now based on the topology it will be advertise to REBEL-DC-03 too. But apart from been domain controller, this particular domain controller is bridgehead server as well. So, it is this server’s responsibility to advertise the updates it received in to the bridge server in Canada Site which is REBEL-DC-04. Once it receives the update it will advertise to other domain controllers in the site. The replication between sites still need to obey the rules which is applied to control the replication. Active Directory domain services automatically selects the bridgehead server for a site. But if need we can decide what should act as bridgehead server for site. 

# Configuring Inter Site replication 

1. Open **Active Directory Sites and Services.**
2. Click on Sites --> Inter-Site Transports --> IP
3. Click on the Link
4. Set **Replication Every** e.g 180
5. Set Cost if you have multiple site links setup


# Useful commands

watch replication changes with powershell 

``` 
while (1) {<command>; sleep 5}
```

Show Replication Summary
```
repadmin /replsummary
```

Show replication partner and status
```
repadmin /showrepl (for localhost)
repadmin /showrepl dc1 ( for remote dc)