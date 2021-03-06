URLQuery: "http://localhost:8086/query?db=monitoring&"

# Retention Policy Requests

retention_policies: 
  - name: "RP1hour"
    query: "q=CREATE RETENTION POLICY RP1hour ON monitoring DURATION 1h REPLICATION 1 DEFAULT"
  - name: "RP6hour"
    query: "q=CREATE RETENTION POLICY RP6hour ON monitoring DURATION 2h REPLICATION 1"
  - name: "RP10hour"
    query: "q=CREATE RETENTION POLICY RP10hour ON monitoring DURATION 3h REPLICATION 1"

# Continuous Queries Requests

continuous_queries: 
  - name: "CQ1"
    query: "q=CREATE CONTINUOUS QUERY CQ10sTo1min on monitoring RESAMPLE EVERY 1h FOR 1h BEGIN SELECT mean(*) INTO RP6hour.:MEASUREMENT FROM /.*/ GROUP BY time(1m), * END"
  - name: "CQ2"
    query: "q=CREATE CONTINUOUS QUERY CQ1minTo10min on monitoring RESAMPLE EVERY 2h FOR 2h BEGIN SELECT mean(*) INTO RP10hour.:MEASUREMENT FROM RP6hour./.*/ GROUP BY time(10m), * END"
