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
<span class="step-count"> Step 1 of 2</span>
 <a href='command:katapod.loadPage?[{"step":"step2"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Configure the nodes</div>

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

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"intro"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
  <a href='command:katapod.loadPage?[{"step":"step2"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>
