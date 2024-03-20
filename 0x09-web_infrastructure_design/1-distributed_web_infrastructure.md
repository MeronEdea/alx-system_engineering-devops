# Description:
This infrastructure comprises a distributed setup aimed at alleviating traffic on the primary server by offloading some of the load to a replica server, facilitated by a load balancer responsible for balancing the workload between them.

# Specifics About This Infrastructure:

* Load Balancer Distribution Algorithm:
The load balancer, configured with the Round Robin distribution algorithm, cyclically directs requests to each server based on their weights. This dynamic algorithm ensures equitable distribution of processing time among servers, with the flexibility to adjust server weights dynamically.

* Setup Enabled by Load Balancer:
The HAProxy load balancer facilitates an Active-Passive setup rather than Active-Active. In an Active-Passive setup, only one node remains active at any given time, while others are on standby. This setup provides redundancy but may underutilize resources compared to an Active-Active setup.

* Database Primary-Replica (Master-Slave) Cluster:
This configuration designates one server as the Primary, capable of handling both read and write requests, and another as the Replica, restricted to read operations. Data synchronization occurs from Primary to Replica whenever write operations are executed.

* Difference Between Primary and Replica Nodes for Applications:
The Primary node manages write operations while the Replica node handles read operations. This division reduces read traffic on the Primary node, enhancing its performance for write-intensive tasks.

# Issues With This Infrastructure:

* Single Points of Failure (SPOF):
Multiple SPOFs exist, such as the Primary MySQL database server, the server housing the load balancer, and the application server connected to the primary database. Failure of any of these components can disrupt site functionality.

* Security Vulnerabilities:
Lack of SSL encryption exposes transmitted data to potential interception by hackers. Additionally, absence of firewalls leaves the network susceptible to unauthorized access and attacks from unauthorized IPs.

* Lack of Monitoring:
Absence of server monitoring tools hinders the ability to track server health and performance. Monitoring is crucial for identifying issues proactively and ensuring optimal system operation.
