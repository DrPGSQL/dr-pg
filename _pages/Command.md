---
layout: home
author_profile: true
sidebar:
  nav: "docs"
permalink: /Command/
title: "Frequently Command"
toc: true
toc_sticky: true
toc_label: "MYSELF"
---



Initializing the data directory

```bash
/usr/pgsql-16/bin/initdb --data-checksums --auth-local=peer --auth- 
host=scram-sha-256 --encoding=UTF-8 --waldir=/pgwaldata/wal
```

* **Replication**
  - Status of replication (from the **Primary database**)

```
psql -c "SELECT pid, usename, client_addr, sent_lsn, write_lsn, state, sync_state FROM pg_stat_replication"
```

Status of wal receiver (from the **standby server**)

```
psql -c "SELECT pid, status, slot_name, received_lsn, sender_host, sender_port FROM pg_stat_wal_receiver;"
```



Configuration Replication Slots

```
psql -c "SELECT pg_create_physical_replication_slot(''db02_repl_slot'')"
```

Checking status for activation of Slot

```
psql -c "SELECT slot_name, slot_type, active FROM pg_replication_slots;"
```





**Base backup**

Clone the standby from the primary database

```
pg_basebackup -h 10.7.223.2 -p 5432 -U replication -R -P -X stream -D /pgdata/data --waldir=/pgwaldata/wal
```





