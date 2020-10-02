# OCP-UPI-vSphere
Just stuff for a UPI installation on VMware


DNS:

CLUSTER-NAME is the name of the cluster. This is chosen when writing the install-config.yml file under metadata.name (it is also the name of the folder we will install OpenShift in on vSphere)

BASE-DOMAIN is the cluster base domain that you specify when you install the cluster.

IP - IP-address of the machine.

SERVER-HOSTNAME is the chosen hostname for the machine.

Example:
api.ocp.mille.local. 10.133.99.107 (With ocp being the cluster-name and mille.local being the base-domain and a random IP)
============ CLUSTER ============
A records (LB):

api.<CLUSTER-NAME>.<BASE-DOMAIN>. <IP>
api-int.<CLUSTER-NAME>.<BASE-DOMAIN>. <IP>
*.apps.<CLUSTER-NAME>.<BASE-DOMAIN>. <IP>
  
Hosts:

A record + PTR

<SERVER-HOSTNAME>.<CLUSTER-NAME>.<BASE-DOMAIN>. <IP>  (BOOTSTRAP)

<SERVER-HOSTNAME>.<CLUSTER-NAME>.<BASE-DOMAIN>. <IP>  (MASTER-1)
<SERVER-HOSTNAME>.<CLUSTER-NAME>.<BASE-DOMAIN>. <IP>  (MASTER-2)
<SERVER-HOSTNAME>.<CLUSTER-NAME>.<BASE-DOMAIN>. <IP>  (MASTER-3)

<SERVER-HOSTNAME>.<CLUSTER-NAME>.<BASE-DOMAIN>. <IP>  (WORKER-1)
<SERVER-HOSTNAME>.<CLUSTER-NAME>.<BASE-DOMAIN>. <IP>  (WORKER-2)
<SERVER-HOSTNAME>.<CLUSTER-NAME>.<BASE-DOMAIN>. <IP>  (WORKER-3)
  
ETCD:

A records:

etcd-0.<CLUSTER-NAME>.<BASE-DOMAIN>. <IP>
etcd-1.<CLUSTER-NAME>.<BASE-DOMAIN>. <IP>
etcd-2.<CLUSTER-NAME>.<BASE-DOMAIN>. <IP>

SRV records:

Name                                                |  TTL    | class     | SRV  | Priority   | weight  | port   | target.
_etcd-server-ssl._tcp.<CLUSTER-NAME>.<BASE-DOMAIN>. | 86400   | IN        | SRV  | 0          | 10      | 2380   | etcd-0.<CLUSTER-NAME>.<BASE-DOMAIN>
  
Name                                                |  TTL    | class     | SRV  | Priority   | weight  | port   | target.
_etcd-server-ssl._tcp.<CLUSTER-NAME>.<BASE-DOMAIN>. | 86400   | IN        | SRV  | 0          | 10      | 2380   | etcd-1.<CLUSTER-NAME>.<BASE-DOMAIN>
  
Name                                                |  TTL    | class     | SRV  | Priority   | weight  | port   | target.
_etcd-server-ssl._tcp.<CLUSTER-NAME>.<BASE-DOMAIN>. | 86400   | IN        | SRV  | 0          | 10      | 2380   | etcd-2.<CLUSTER-NAME>.<BASE-DOMAIN>
