---
layout: home
author_profile: true
sidebar:
  nav: "docs"
permalink: /PostgreSQL/
title: "About"
toc: true
toc_sticky: true
toc_label: "MYSELF"
---

- Barman Setup 을 위한 접속 

  - 패스워드 없이 접속 할때 key copy 순서..
    1. systemctl stop sshd
    2. /etc/ssh/sshd_config 
       PasswordAuthentication yes (수정)
    3. systemctl start sshd
    4. ssh-copy-id -i ./id_rsa.pub postgres@10.7.224.2 (패스워드 입력)
       - rsa 파일 copy 확인
    5. /etc/ssh/sshd_config 
       PasswordAuthentication no (수정)
    6. 접속 확인

- efm cluster-status  "cluster name"  확인 중 모두 UNKNOW 으로 나올 때.. 
  Requires=edb-efm-4.8.service
  Before=postgresql-16.service


  /etc/systemd/system/postgresql-16.service 및

  /etc/systemd/system/edb-efm-4.8.service 확인



> > - | Source                   | Target (VIP - 10.7.223.6) |
> >   | ------------------------ | ------------------------- |
> >   | DB1 (10.7.223.2)         | ok                        |
> >   | DB2 (10.7.223.3)         | Not Reach                 |
> >   | DB3 (10.7.224.2)         | Not Reach                 |
> >   | Tool Server (10.7.223.4) | Not Reach                 |



[efm@dbserver02 ~]$ efm promote efm_ss_cluster
The primary database will be shut down and a standby will be promoted. Are you sure you want to continue? [y/N]:y
Would you like to attempt to promote the standby anyway [y/N]: y
Forcing this promotion may result in data loss - are you sure you want to continue? This is the last prompt. [y/N]: y
Promote command accepted by local agent. Proceeding with promotion. Run the 'cluster-status' command for information about the new cluster state.
