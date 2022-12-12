+++
title = "Cloudflare Permanent Redirect"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2022-11-11T05:00:00Z
description = "cloudflare permanent redirect"
categories = ["docker"]
type = "post"

+++
*Login to Cloudflare

*Use the drop-down menu in the upper left of your screen and click your domain that you want the redirect to take place on.

*Click the DNS icon at the top of the screen.

*Select CNAME using the drop-down options

*Add the sub domain in NAME

*Add your domain name in Domain name

*Leave TTL as automatic and Cloudclare enabled, click Add Record button.

*Click Page Rules icon

*Click Create Page Rule button

*Add alexa.example.com/* in the URL match field

*Click + Add a Setting, find Forwarding URL and click it

*Select the status code 301 - Permanent Redirect

*Add the Enter destination URL as http://example.com/alexaSkillDemo

*Click Save and Deploy button.