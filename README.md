# Talus Database

Mongodb has been chosen as the database for Talus

# Watching for changes

Monitoring mongodb for changes will be an integral part of
Talus. This will be done using replica sets, which logs all
actions to an operations log (oplog).

See http://stackoverflow.com/questions/9691316/how-to-listen-for-changes-to-a-mongodb-collection
for more details.

After starting talus-db, issue the following command
docker logs talus-db
to ensure that replication has been set up properly.
If you see a connection refused error, simply restart talus-db.

This is what a successful replication log message will look like.

```
root@talus:~# docker logs talus-db
2017-04-24T16:07:39.298+0000 I CONTROL  log file "/talus/logs/mongodb/mongodb.log" exists; moved to "/talus/logs/mongodb/mongodb.log.2017-04-24T16-07-39".
MongoDB shell version: 3.0.14
connecting to: test
{
	"set" : "rs0",
	"date" : ISODate("2017-04-24T16:08:13.979Z"),
	"myState" : 1,
	"members" : [
		{
			"_id" : 0,
			"name" : "talus-db:27017",
			"health" : 1,
			"state" : 1,
			"stateStr" : "PRIMARY",
			"uptime" : 34,
			"optime" : Timestamp(1492966577, 1),
			"optimeDate" : ISODate("2017-04-23T16:56:17Z"),
			"electionTime" : Timestamp(1493050069, 1),
			"electionDate" : ISODate("2017-04-24T16:07:49Z"),
			"configVersion" : 61593,
			"self" : true
		}
	],
	"ok" : 1
}
```

To view mongodb logs:
```
tail -f /var/log/talus/mongodb/mongodb.log

journalctl -u docker.talus-db.service
```
