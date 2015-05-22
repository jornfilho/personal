Cassandra 2.1 on Ubuntu
http://docs.datastax.com/en/cassandra/2.1/cassandra/gettingStartedCassandraIntro.html

Requirements
Java: It is recommended to use the latest version of Oracle Java 8 on all nodes. (Oracle Java 7 is also supported.)
	sudo add-apt-repository ppa:webupd8team/java
	sudo apt-get update
	sudo apt-get install oracle-java8-installer

1) Add the DataStax Community repository to the /etc/apt/sources.list.d/cassandra.sources.list
echo "deb http://debian.datastax.com/community stable main" | sudo tee -a /etc/apt/sources.list.d/cassandra.sources.list

2) Add the DataStax repository key to your aptitude trusted keys
curl -L http://debian.datastax.com/debian/repo_key | sudo apt-key add -

3) Install the latest package:
sudo apt-get update
sudo apt-get install dsc21
sudo apt-get install cassandra-tools ## Optional utilities

4) Because the Debian packages start the Cassandra service automatically, you must stop the server and clear the data:
Doing this removes the default cluster_name (Test Cluster) from the system table. All nodes must use the same cluster name.
sudo service cassandra stop
sudo rm -rf /var/lib/cassandra/data/system/*

5) Set the properties in the cassandra.yaml file for each node:
http://docs.datastax.com/en/cassandra/2.1/cassandra/initialize/initializeSingleDS.html

6) After you have installed and configured Cassandra on all nodes, start the seed nodes one at a time, and then start the rest of the nodes.
Note: If the node has restarted because of automatic restart, you must first stop the node and clear the data directories, as described above.
sudo service cassandra start

7) To check that the ring is up and running, run:
nodetool status




DataStax DevCenter
Create and run Cassandra Query Language (CQL) queries against Apache Cassandra™ and DataStax Enterprise.
http://www.datastax.com/download-ops-dev#DataStax_DevCenter


DataStax OpsCenter
Visual management and monitoring for Apache Cassandra™ and DataStax Enterprise database clusters
http://docs.datastax.com/en/opscenter/5.1/opsc/install/opscInstallDeb_t.html


Manual deploy agent for DataStax OpsCenter
http://docs.datastax.com/en/opscenter/5.1/opsc/install/opscManualInstallAgentPkgDeb.html


Sample code
https://wiki.apache.org/cassandra/GettingStarted