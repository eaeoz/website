+++
title = "CheckMK Network and System Monitoring Tool"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2019-11-16T05:00:00Z
description = "checkmk"
categories = ["technology"]
type = "post"

+++
### Docker CLI:

```
docker container run -dit -p 8080:5000 --tmpfs /opt/omd/sites/cmk/tmp:uid=1000,gid=1000 -v monitoring:/omd/sites --name monitoring -v /etc/localtime:/etc/localtime:ro --restart always checkmk/check-mk-raw:2.0.0-latest
```

```
Username: cmkadmin
Password: check password from logs
```

change password from

`settings > users > cmkadmin`


- for installing agent go to agent 
- right click deb copy link address and paste the machine you want to monitor with wget
- run deb package
- go to hosts add host with hostname,ip and select api not snmp
- it will check host machine which is installent agent.it takes some time
- check from the list monitoring option accept.

https://docs.checkmk.com/latest/en/introduction_docker.html