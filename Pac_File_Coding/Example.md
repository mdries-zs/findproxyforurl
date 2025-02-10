# Example PAC File

The basic for all good PAC files start with a clear and concise coding methodology. It’s possible to achieve the same result using several different methods, both with the PAC file functions available and the flexibility of the JavaScript language.

This page includes a PAC file example which has been proven to be flexible, easy to update, while still providing accurate results.

### Features

- Proxy bypass rules for private IP networks, internal hostnames, and hosts with .local domain extension.
- - While the other rules in this example may be optional, most deployments should begin with this code block (lines 3-10).
- Example hostname bypass rule.
- Example protocol and URL bypass rule.
- Example machine based IP routing rule.
- Default proxy rule, if all above rules don’t match.

### Example PAC File

	function FindProxyForURL(url, host) {
	 
	// If the hostname matches, send direct.
		if (dnsDomainIs(host, "intranet.domain.com") ||
			shExpMatch(host, "(*.abcdomain.com|abcdomain.com)"))
			return "DIRECT";
	 
	// If the protocol or URL matches, send direct.
		if (url.substring(0, 4)=="ftp:" ||
			shExpMatch(url, "http://abcdomain.com/folder/*"))
			return "DIRECT";
	 
	// If the requested website is hosted within the internal network, send direct.
		if (isPlainHostName(host) ||
			shExpMatch(host, "*.local") ||
			isInNet(dnsResolve(host), "10.0.0.0", "255.0.0.0") ||
			isInNet(dnsResolve(host), "172.16.0.0",  "255.240.0.0") ||
			isInNet(dnsResolve(host), "192.168.0.0",  "255.255.0.0") ||
			isInNet(dnsResolve(host), "127.0.0.0", "255.255.255.0"))
			return "DIRECT";
	 
	// If the IP address of the local machine is within a defined
	// subnet, send to a specific proxy.
		if (isInNet(myIpAddress(), "10.10.5.0", "255.255.255.0"))
			return "PROXY 1.2.3.4:8080";
	 
	// DEFAULT RULE: All other traffic, use below proxies, in fail-over order.
		return "PROXY 4.5.6.7:8080; PROXY 7.8.9.10:8080";
	 
	}
 <br>
 
## Recommendations

When deploying URL and host rules care must be taken to ensure rules are as explicit as possible. The examples below detail how host and URL rules should be implemented.

**Host Example**
      
    if (dnsDomainIs(host, "abcdomain.com") || dnsDomainIs(host, "www.abcdomain.com"))
        return "DIRECT";

**URL Example**

    if (shExpMatch(url, "http://abcdomain.com/folder/*"))
        return "DIRECT";

## Warnings

The following code is an example **which may have unintended consequences** due to the broad interpretation of using the shExpMatch function, wildcards, and hostnames.

Cautionary Example

	// Would send both of the following requests direct to the Internet:
	// 1. www.hotmail.com 2. phishing-scam.com?email=someone@hotmail.com
	 
	if (shExpMatch(url, "*hotmail.com*"))
			return "DIRECT";

Safe Example 

	// Would send only traffic to the the host and subdomains of hotmail.com
	 
	if (shExpMatch(host, "*.hotmail.com"))
			return "DIRECT";
