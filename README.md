# Requete_SQL_Sur_Hive


# Script Docker

supprimer les images : docker rm -f $(docker ps -a -q)

sudo docker-compose up   |  sudo docker-compose up -d

sudo docker exec -it namenode bash

sudo docker exec -it hive-server bash,  cd /opt/hive/bin, ./hive


cd /home/useradd/mydocker-hive/docker-hadoop-spark/Requete_SQL_Sur_Hive

# WSL
# Copy all CSV files to HDFS
for file in *.csv; do
    filename="${file%.csv}"
    hdfs_directory="/user/hive/warehouse/data/${filename}/"
    docker cp "$file" namenode:"/tmp/${file}"
    sudo docker exec -it namenode hadoop fs -mkdir -p "$hdfs_directory"
    sudo docker exec -it namenode hadoop fs -copyFromLocal "/tmp/${file}" "$hdfs_directory"
done
