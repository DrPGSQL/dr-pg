---
layout: home
author_profile: true
sidebar:
  nav: "docs"
permalink: /Command/
title: "About"
toc: true
toc_sticky: true
toc_label: "MYSELF"
---









**Replication**

Status of replication (from the Primary database)

```
psql -c "SELECT pid, usename, client_addr, sent_lsn, write_lsn, state, sync_state FROM pg_stat_replication"
```

Status of wal receiver (from the standby server)

```
psql -c "SELECT pid, status, slot_name, received_lsn, sender_host, sender_port FROM pg_stat_wal_receiver;"
```





Clone the standby from the primary database

**Base backup**

```
pg_basebackup -h 10.7.223.2 -p 5432 -U replication -R -P -X stream -D /pgdata/data --waldir=/pgwaldata/wal
```



