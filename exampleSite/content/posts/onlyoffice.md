+++
title = "onlyoffice nextcloud integraton docker compose"
image = "/images/post/onlyoffice.jpg"
author = "Sedat"
date = "2025-02-24T00:02:07Z"
description = "onlyoffice nextcloud docker"
categories = ["Docker"]
type = "post"

+++

Integrating ONLYOFFICE with Nextcloud provides a powerful, self-hosted document collaboration solution, enabling users to create, edit, and collaborate on documents, spreadsheets, and presentations directly within Nextcloud. ONLYOFFICE offers full compatibility with Microsoft Office formats and provides real-time co-editing, version history, and access control features. By setting up ONLYOFFICE within Nextcloud, teams can work on documents seamlessly while maintaining data privacy and security on their own server. The integration supports advanced formatting, document sharing, and simultaneous editing, making it ideal for businesses and organizations looking for a cloud-based office suite without relying on third-party services. With Docker or a dedicated server setup, the integration is straightforward, allowing users to maximize productivity within their Nextcloud environment.

***

- [Click here for more information.](https://helpcenter.onlyoffice.com/installation/docs-community-install-docker.aspx)

**Docker commmand:**

```
sudo docker run -i -t -d -p 80:80 --restart=always \
    -v /app/onlyoffice/DocumentServer/logs:/var/log/onlyoffice  \
    -v /app/onlyoffice/DocumentServer/data:/var/www/onlyoffice/Data  \
    -v /app/onlyoffice/DocumentServer/lib:/var/lib/onlyoffice \
    -v /app/onlyoffice/DocumentServer/db:/var/lib/postgresql -e JWT_SECRET=my_jwt_secret onlyoffice/documentserver
```

***

ONLYOFFICE Docs address is *https adress of public nextcloud address"

Secret key *you can leave blank to disable it*

- Advanced server settings (if servers not secured for local)

ONLYOFFICE Docs address for internal requests from the server is *onlyoffice http port (in our case 80)*

Server address for internal requests from ONLYOFFICE Docs is *http port of nextcloud server*

**you can make these changes if you have problem accessing ui:

```
in Nextcloud config file (/nextcloud/config/config.php):

'onlyoffice' => array (
   'verify_peer_off' => true,
),
'allow_local_remote_servers' => true,

and add trusted domains for nextcloud local and onlyoffice local (you can add if you have Additionally)

'trusted_domains' =>
array (
 0 => 'c.sedat.cf',
 1 => '192.168.1.233:3337',
 2 => '192.168.1.233',
),
```

Logs stored in:

`/app/onlyoffice/DocumentServer/logs/documentserver`
