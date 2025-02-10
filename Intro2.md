# Introduction to PAC Files

## So what exactly can a PAC file do?
A PAC file can have rules which leverage the following information to route traffic:
- IP address of the requested website
- Host of the requested website
- The user IP address*
- The date/time


Additionally, a PAC file can route:

- HTTP, HTTPS, and FTP traffic in a web browser
- Route traffic either direct or via proxy (hostname and port configurable)


## What are the limitations?

- PAC files run in a browser sandbox thus don’t have access to the entire JavaScript programming language. Instead, PAC file functionality is implemented in a browser with a custom sanboxed function set. More information as to the available functions can be found [here](https://github.com/mdriesnj/findproxyforurl/blob/main/Pac_File_Coding/Pac_Functions.md).
- No access to the machine hostname
- No reliable method to determine the user IP address*
- Proxy failover lacks intelligence and operates based on a TCP timeout occurring

* *The myIpAddress() function is inconsistently implemented across the major web browsers and doesn’t support IPv6; this may result in either an IPv6 address being returned unexpectedly, 127.0.0.1 being returned, or the IP address of an unexpected network adapter being returned. As such it’s recommended to avoid use of this function completely. Windows has implemented a new FindProxyForURLEx() function to support IPv6, however, the implementation is complex and support across the major browsers is lacking.*

[Back to ReadME](https://github.com/mdriesnj/findproxyforurl/blob/main/README.md)
