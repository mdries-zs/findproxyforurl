# Introduction to WPAD
Web Proxy Auto-Discovery Protocol, or WPAD, is a technology which aids a web browser in automatically detecting the location of a PAC file using DNS or DHCP.

A browser that supports both DHCP and DNS will first attempt to locate a PAC file using DHCP, and should a DHCP configuration not exist fail-over to DNS WPAD will occur. If neither are configured, a browser will fail open.

## DHCP WPAD

DHCP WPAD is a method of detecting a PAC file location by leveraging the local DHCP infrastructure. A DHCP server may configured with an option storing the PAC file location, which a web browser can query. Once the option is found, the web browser will make a request for the PAC file.

Prerequisites include a PAC file, web server, DHCP server, and for any user computers to be configured to obtain their network IP address information from the DHCP server.

### Example

- In the below example, the network name of the user computer is **laptop01.us.division.company.com**.
- Upon loading, the web browser issues a **DHCPINFORM**, requesting that the DHCP server provide a list of options and their configurations.
- The DHCP server responds with a **DHCP ACK** message, containing the list of options and configurations
- One of these options, **252**, contains the PAC file location. The web browser can perform a request to download the PAC file.

![WPAD_Diagram1!](https://github.com/mdriesnj/findproxyforurl/blob/main/wpad_diagram1.png)

## DNS WPAD

DNS WPAD is a method of detecting a PAC file via discovery by leveraging the network name of the user computer and using a consistent DNS configuration and PAC script file name. DNS WPAD is the most widely supported method, with support across all major browsers and operating systems.

Prerequisites include a PAC file, web server, and a locally access DNS hostname to point to the web server.

*** Example

- In the below example, the network name of the user computer is **laptop01.us.division.company.com**.
- A PAC file with the file name **wpad.dat** is being served by a web server on the host **wpad.company.com**.
- A DNS WPAD enabled browser will remove the machine name **(laptop01)**, apply **wpad** to the network name, and apply as a suffix the file resource **/wpad.dat**, e.g. **http://wpad.us.division.company.com/wpad.dat**.
- The browser will try to download the PAC file from the location **http://wpad.us.division.company.com/wpad.dat**.
- If the web browser is unable to resolve the host **wpad.us.division.company.com**, it will progress through the sub-domain node hierarchy and attempt to download the wpad.dat file from the host **wpad.division.company.com**, and so on until the lowest valid node is reached, **wpad.company.com**.
