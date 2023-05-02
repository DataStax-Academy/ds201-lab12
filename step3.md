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
 <a href='command:katapod.loadPage?[{"step":"step2"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 3 of 3</span>
 <a href='command:katapod.loadPage?[{"step":"finish"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>

</div>

<!-- CONTENT -->

<div class="step-title">Use different consistency levels with all nodes available</div>

✅ Start the node you shut down before:
<details class="katapod-details">
  <summary>Solution</summary>

Make sure that you start the right node!
<table class="katapod-table">
  <tr>
    <th>Node (IP)</th>
    <th>Start command</th>
  </tr>
  <tr>
    <td>127.0.0.1</td>
    <td>

```
./node1/bin/cassandra
``` 
</td>
<tr>

  <tr>
    <td>127.0.0.2</td>
    <td>

```
./node2/bin/cassandra
``` 
</td>
<tr>
    
</table>

</details>
<br>

✅ Verify that all three nodes are running:

<details class="katapod-details">
  <summary>Solution</summary>

```
./node3/bin/nodetool status
```

</details>
<br>

✅ Use *cqlsh* to set the consistency level to `TWO` and retrieve all the rows in the *cassandra* partition:

<details class="katapod-details">
  <summary>Solution</summary>

```cql
./node1/bin/cqlsh

USE killrvideo;

CONSISTENCY TWO;

SELECT * FROM killrvideo.videos_by_tag WHERE tag = 'cassandra';
```

</details>
<br>

The new row should be present. 

---
**Note:** The row was inserted at consistency level `ONE` whn only one replica node was running. This read was at consistency level `TWO` and it succeeded. Somehow when the downed node returned to the cluster it *synced up* and got the new row! Cassandra uses *Hinted Handoff* to inform nodes about changes that occurred when they were not available. More on this in Exercise 13.)

---

</details>
<br>
<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"step2"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
  <a href='command:katapod.loadPage?[{"step":"finish"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>

</div>
