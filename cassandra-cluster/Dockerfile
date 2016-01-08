# Spotify Cassandra 2.0 Cluster Node Image
#
# VERSION               0.1
#
# Expects CASSANDRA_SEEDS and CASSANDRA_TOKEN env variables to be set.
# If CASSANDRA_SEEDS is not set, node acts as its own seed
# If CASSANDRA_TOKEN is not set, startup process is aborted

FROM cakesolutions/cassandra:base

USER root

# Place cluster-node startup-config script
ADD scripts/cassandra-clusternode.sh /usr/local/bin/cassandra-clusternode
RUN echo "deb http://debian.datastax.com/community stable main" | sudo tee -a /etc/apt/sources.list.d/datastax.community.list
RUN curl -L https://debian.datastax.com/debian/repo_key | sudo apt-key add -
RUN apt-get update
RUN apt-get install datastax-agent
RUN echo "stomp_interface: 172.31.1.11" | sudo tee -a /var/lib/datastax-agent/conf/address.yaml

# Start Cassandra
ENTRYPOINT ["cassandra-clusternode"]
