# Introduction to PAC files

## What is a PAC file?
A Proxy Auto-Configuration (PAC) file contains a set of rules coded in JavaScript which allows a web browser to determine whether to send web traffic direct to the Internet or be sent via a proxy server.

PAC files can control how a web browser handles HTTP, HTTPS, and FTP traffic.

## OK, tell me more
Sure! PAC files provide flexibility and redundancy in a manner which isn’t currently possible when configuring an explicit proxy.

It’s possible to leverage many benefits when using PAC files:
- Supported by all major operating systems and browsers
- Able to automatically route traffic correctly regardless of whether the user enters a domain or IP address
- Automatic proxy failover

## What does all this mean to me?
Let’s say you’re deploying a cloud security service…

With a PAC file your internal traffic will go direct, your traffic destined for the Internet will go via the cloud service, and any exceptions to that logic can be accounted for and routed as necessary.

Once the PAC file is designed and deployed any ongoing maintenance will be straightforward.

[Next Page](https://github.com/mdriesnj/findproxyforurl/blob/main/Intro2.md)
