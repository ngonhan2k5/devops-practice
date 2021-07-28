# Mongo Server Works - How to do with docker
### 1. [Mongo replicaSet](https://github.com/ngonhan2k5/devops-practice/tree/master/replicaSet): Create a replicaSet for mongo using docker composer
#### a, Spin up all 4 mongod nodes and 1 mongo admin UI:
```docker-compose up -d``` in replicatSet folder then you can open http://localhost:8081 to access admin UI (client)
#### b, Connect to mongo shell of one node:
```docker run -it --network replicaset_default --rm mongo mongo --host rs1```
#### c, Enable replicaSet with 3 nodes rs1,rs2,rs3:
```
rsconf = { _id: "mdbDefGuide", members: [ {_id:0, host: "rs1:27017"}, {_id:1, host: "rs2:27017"}, {_id:3, host: "rs3:27017"}] }; 
rs.initiate(rsconf);
```
Check replacation status with rs.status(); \
Now you can switch off any 1 node without affect client usage
#### d, Add node rs4 to replicaSet:
##### d1- Connect to primary node:
Connect to anynode use 
```docker run -it --network replicaset_default --rm mongo mongo --host rs1``` \
Use ```db.hello()``` to know which is primary then connect to that node use above docker command. \
Add node
```rs.addNode({host: "rs4:27017"})```
### 2. [Mongo shard]
