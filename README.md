# ansible-postgres-pgpool
This playbook is used to install the following cluster build for postgres along with pgpool. 

The versions used for postgres is 9.6 and for pool its pgpool3, in order to have high availability for pgpool we manage two nodes for pgpool one will be active and having VIP address attached it allowing apps to connect through VIP. In event of master pgpool is down the shadow pgpool will take over the connections and VIP will attached to it. On the backend side, the postgres will be running in hotstandby mode allowing all primary and standby for reads and only writes will be sent to primary via pgpool.

# Pre-requisities

- **Cluster**

    This playbook is for cluster using pgpool and postgres replication with two nodes pgpool and two nodes for postgres
    
- **Host files structure**

    SHould be seperate group for each type i.e
        
        [pgpool]
        
        pool01.localdomain
        
        pool02.localdomain
        
        [primary]
        
        psql02.localdomain
        
        [standby]
        
        psql01.localdomain
- **SSL Mode**
    
    Must copy the root.crt and root.key to playbook/install/certs/
    
- **Variables File install/group_vars/postgres_var.yml**

