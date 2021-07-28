# devops-practice
### 1. [Mongo replicaSet](https://github.com/ngonhan2k5/devops-practice/tree/master/replicaSet): Create a replicaSet for mongo using docker composer
#### a, Connect to mongo shell of one node:
```docker run -it --network replicaset_default --rm mongo mongo --host rs1```
#### b, Enable replicaSet:
```
rsconf = { _id: "mdbDefGuide", members: [ {_id:0, host: "rs1:27017"}, {_id:1, host: "rs2:27017"}, {_id:3, host: "rs3:27017"}] }; 
rs.initiate(rsconf);
```
#### b, Add node to replicaSet:
##### b1- Connect to primary node:
Connect to anynode use 
```docker run -it --network replicaset_default --rm mongo mongo --host rs1``` \
Use ```db.hello()``` to know which is primary then connect to that node use above docker command. \
Add node
```rs.addNode({host: "rs4:27017"})```
