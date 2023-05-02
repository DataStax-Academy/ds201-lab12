<!-- TOP -->
<div class="top">
  <img class="scenario-academy-logo" src="https://datastax-academy.github.io/katapod-shared-assets/images/ds-academy-2023.svg" />
  <div class="scenario-title-section">
    <span class="scenario-title">Consistency</span>
    <span class="scenario-subtitle">ℹ️ For technical support, please contact us via <a href="mailto:academy@datastax.com">email</a>.</span>
  </div>
</div>

<!-- NAVIGATION -->
<div id="navigation-top" class="navigation-top">
 <a href='command:katapod.loadPage?[{"step":"intro"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 1 of 3</span>
 <a href='command:katapod.loadPage?[{"step":"step2"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Explore the consistency level</div>

✅ Check that all three nodes are up and running:

```
./node1/bin/nodetool status
```

✅ Start *cqlsh*:

```
./node1/bin/cqlsh
```

✅ Switch to the *killrvideo* keyspace:

```
USE killrvideo;
```

✅ Use `CONSISTENCY` to check the current consistency level:

```
CONSISTENCY;
```
Verify that the consistency level is set to `ONE`: only one node must acknowledge a write on a write request, and only one node must return a result set to satisfy a read request.

✅ Set your consistency level to `TWO` by executing the following command:

```
CONSISTENCY TWO;
```

In this cluster setup, consistency level `TWO` would work the same way as `ALL` because our current replication settings store one replica per data center, and we have two data centers.

✅ Retrieve the cassandra partition from the videos_by_tag table by executing the following command:

```
SELECT * FROM videos_by_tag WHERE tag = 'cassandra';
```

The query should succeed.

✅ Quit *cqlsh*:
```
QUIT
```

✅ Use `nodetool getendpoints` to determine which nodes hold the replicas for the cassandra partition tag value in the *videos_by_tag* table:
```
./node1/bin/nodetool getendpoints killrvideo videos_by_tag 'cassandra'
```

✅ Use `nodetool stopdaemon` to bring down the replica node for the cassandra partition in the *dc-seattle* datacenter:

---
**Note:** The *dc-seattle* datacenter has nodes listening on:<br>
* 127.0.0.1
* 127.0.0.2
<br>
---
<details class="katapod-details">
  <summary>Solution</summary>

Make sure that you only shut down one node!
<table class="katapod-table">
  <tr>
    <th>Node (IP)</th>
    <th>Shutdown command</th>
  </tr>
  <tr>
    <td>127.0.0.1</td>
    <td>

```
./node1/bin/nodetool stopdaemon
``` 
</td>
<tr>

  <tr>
    <td>127.0.0.2</td>
    <td>

```
./node2/bin/nodetool stopdaemon
``` 
</td>
<tr>
    
</table>

Keep track of which node you  down and also the node number that is still up.

</details>
<br>


<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"intro"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
  <a href='command:katapod.loadPage?[{"step":"step2"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>
