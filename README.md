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

[More about PAC Files](https://github.com/mdriesnj/findproxyforurl/blob/main/1_Pac_Intro.md)

## How to use this site

You can navigate the file structure on the left or use the links below...

- [Introduction to PAC Files](https://github.com/mdriesnj/findproxyforurl/blob/main/1_Pac_Intro.md)
- [Introduction to WPAD Files](https://github.com/mdriesnj/findproxyforurl/blob/main/2_Wpad_Intro.md)

# PAC File Coding

- [PAC Functions](https://github.com/mdriesnj/findproxyforurl/blob/main/Pac_File_Coding/Pac_Functions.md)
- [Code Snippets](https://github.com/mdriesnj/findproxyforurl/blob/main/Pac_File_Coding/Code_Snippets.md)
- [PAC File Example](https://github.com/mdriesnj/findproxyforurl/blob/main/Pac_File_Coding/Example.md)
- [Misconceptions](https://github.com/mdriesnj/findproxyforurl/blob/main/Pac_File_Coding/Misconceptions.md)

# Deployment

- [Deployment Options](https://github.com/mdriesnj/findproxyforurl/blob/main/Deployment/Deployment_Options.md)
- [PAC File Deployment](https://github.com/mdriesnj/findproxyforurl/blob/main/Deployment/PAC_Deployment.md)
- [WPAD Deployment](https://github.com/mdriesnj/findproxyforurl/blob/main/Deployment/WPAD_Deployment.md)
- [Browser Support](https://github.com/mdriesnj/findproxyforurl/blob/main/Deployment/Browser_Support.md)

# Support

- [Common PAC File Issues](https://github.com/mdriesnj/findproxyforurl/blob/main/Support/Common_PAC_File_Issues.md)
- [Common WPAD Issues](https://github.com/mdriesnj/findproxyforurl/blob/main/Support/Common_WPAD_Issues.md)
- [Troubleshooting](https://github.com/mdriesnj/findproxyforurl/blob/main/Support/Troubleshooting.md)
- [Netscape Documentation 'legacy'](https://github.com/mdriesnj/findproxyforurl/blob/main/Support/netscape_documentation.md)

# Helpful Tools

- [PAC File tester/parser](https://thorsenlabs.com/pac)
