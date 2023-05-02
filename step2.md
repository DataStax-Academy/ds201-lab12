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
 <a href='command:katapod.loadPage?[{"step":"step1"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 2 of 3</span>
 <a href='command:katapod.loadPage?[{"step":"step3"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>

</div>

<!-- CONTENT -->

<div class="step-title">Use different consistency levels</div>

✅ Start *cqlsh* from *node3* since it is the only node running in *dc-atlanta*:
```
./node3/bin/cqlsh
```

✅ Switch to the *killrvideo* keyspace, set the consistency level to `TWO`, and run the query again to retrieve the *cassandra* partition:

<details class="katapod-details">
  <summary>Solution</summary>

```cql
USE killrvideo;

CONSISTENCY TWO;

SELECT * FROM killrvideo.videos_by_tag WHERE tag = 'cassandra';
```

</details>
<br>

The query should error out with the message *NoHostAvailable*: because you cannot achieve a consistency level of 'TWO' with only one of the two replica nodes online.

✅ Set the consistency level back to `ONE` and retry the query:

<details class="katapod-details">
  <summary>Solution</summary>

```cql
CONSISTENCY ONE;

SELECT * FROM killrvideo.videos_by_tag WHERE tag = 'cassandra';
```

</details>
<br>

The query should succeed because we still have one replica node available.

✅ Change the consistency level back to `TWO`:
<details class="katapod-details">
  <summary>Solution</summary>

```cql
CONSISTENCY TWO;
```

</details>
<br>

✅ Run the following statement to insert a new row into the *cassandra* partition: 

```cql
INSERT INTO videos_by_tag (tag, added_date, video_id, title)
VALUES ('cassandra', '2020-03-11', uuid(), 'I Love Cassandra');

```
The write should fail with the error *NoHostAvailable*: because we still cannot achieve a consistency level of `TWO`.


✅ Change the consistency level back to `ONE` and try the *INSERT* again:
<details class="katapod-details">
  <summary>Solution</summary>

```cql
CONSISTENCY ONE;

INSERT INTO videos_by_tag (tag, added_date, video_id, title)
VALUES ('cassandra', '2020-03-11', uuid(), 'I Love Cassandra');
```

</details>
<br>

✅ Quit *cqlsh*:
```
QUIT
```

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"step1"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
  <a href='command:katapod.loadPage?[{"step":"step3"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>

</div>
