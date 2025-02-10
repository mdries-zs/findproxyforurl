# Code Snippets

The majority of PAC files contain many common elements; this page serves as a resource for documenting common PAC file code snippets.

**Local Network Matching**

	if (isPlainHostName(host) ||
		shExpMatch(host, "*.local") ||
		isInNet(dnsResolve(host), "10.0.0.0", "255.0.0.0") || 
		isInNet(dnsResolve(host), "172.16.0.0",  "255.240.0.0") ||
		isInNet(dnsResolve(host), "192.168.0.0",  "255.255.0.0") ||
		isInNet(dnsResolve(host), "173.37.0.0",  "255.255.0.0") ||
		isInNet(dnsResolve(host), "127.0.0.0", "255.255.255.0"))
		return "DIRECT";
    		
**Host Matching**
  
	if (dnsDomainIs(host, "abcdomain.com") || dnsDomainIs(host, "www.abcdomain.com"))
        return "DIRECT";

**URL Matching**

	if (shExpMatch(url, "http://abcdomain.com/folder/*"))
        return "DIRECT";

**Protocol Control**

	// HTTP
	if (url.substring(0,5)=="http:") return "DIRECT";
	// HTTPS
	if (url.substring(0,6)=="https:") return "DIRECT";
	// FTP
	if (url.substring(0,4)=="ftp:") return "DIRECT";

**Defining a connection method**

 	// Direct-to-Internet
	return "DIRECT";
	// Proxy
	return "PROXY proxy.domain.local:8080";
	// Failover
	return "PROXY proxy1.domain.local:8080; PROXY proxy2.domain.local:8080; DIRECT";

**Machine IP Based Routing**

	if (isInNet(myIpAddress(), "10.10.5.0", "255.255.255.0"))
		return "PROXY 1.2.3.4:8080";

[Back to ReadMe](https://github.com/mdries-zs/findproxyforurl/blob/main/README.md)

