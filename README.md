# Load balancer

### How does Sw and Hw Load Balancer Work?(Loadbalancer Algorithms)

* Load balancer will distribute the work-load of your system to multiple
individual systems, or group of systems to reduce the amount of load on an
individual system, which in turn increases the reliability, efficiency and
availability.

#### Sw Load Balancers

* Sw LB generally implements a combination of one or more scheduling algos.

##### Weighted Scheduling Algorithm

* Work is assigned to the server according to the weight assigned to the
server.

* For different types of the server in the group different weights are assigned
thus the load gets distributed.

* This is used when there is a considerable difference between the capabilities
and specification of the servers present in the farm or cluster.

* The algorithm stands out to be efficient utilizing the available server
resource at any instant of time.

##### Round Robin Scheduling

* Requests are served by the server sequentially one after another.After
sending the request to the last server, it starts from the first server
again.

##### Least Connection First Scheduling

* Requests are served first to the server which is currently handling least
number of persistent connections.It will be assigned with least no of
connections.

* The algorithm is used when we have large number of persistent connenctions
in the traffic unevenly distributed between servers.It is often coupled
with `Sticky Session` or `Session aware` load balncing

* In this, all the request related to a session is sent to maintain the
session state and synchronization.

#### Hardware Load Balancers

* Load balancing hws are often refered as specialized routers or switches
which are in between the servers and the client.It can also be a dedicated
system btw the client and the server to balance the load.

* The hw load balancers are implemented on Layer4(Transport layer) and layer7
(Application layer) of OSI model so prominent among these hws are l4-l7 routers.

##### Layer4 HW Load Balancing

* These kind of load balancers work on transport layer of OSI model and make
use of TCP, UDP and SCTP transport layer protocol details to make decision
on which server the data is to be sent.

* Layer4 load balancers are mostly the network address translators(NAT) which
shares load to the different servers getting translated to by these loadbalancer

* These routers hide multiple servers behind them and translate every response
data packets coming from the server to be coming from same ipaddress.

* Similarly, when there is a request they reverse translate the request
using the mapping table and distributes it among servers.

`DNS load balancing` -> in dns based load balancing method the Domain Name
Servers are configured to return different ipaddress for different systems.

* This approach creates a load balancing effect whenever there is a dns
lookup.

###### Direct routing
* This is yet another configuration of hw LB where routers are aware of
the server mac addresses and server may be ARP(Address resolution Protocol).

* In direct routing, it is direct in the sense that all the income traffic
is routed by the load balancer however all the outgoing traffic direct
reaches the client which it makes it super fast load balancing config.

###### Tunnel/IP tunneling
* Often looks like Direct routing where response is directly sent to client
however the traffic btw the router and the server can be routed

* In this client sends the request to the virtual IP of LB which further
encapsulates the IP packets, keeps a hash table and distributes it to the
different servers as per the configured load balancing technique.

* When the server is getting back the response, it decapsulates it and send
back to the client directly according to the hash table it has stored.This
record is eventually remeoved from hash table when the connection is closed.

##### Layer7 HW LB

* This type of load balancers makes the decision according to the actual
coontent of the message (URLs, cookies, scripts) since HTTP  exists on layer7.

* These layer7 HW actually form an Application delivery network and they
pass-on request to the servers as per the type of the content.

* LB effect is achieved by distributing load according to the type to content
requested.

* Layer 7 LB uses the following 3 techniques:
1. URL parsing: From this they come to know about different type of contents.
2. Cookie sniffing: Helps them for a session aware routing.
3. HTTP reading: This method looks for http header info.
