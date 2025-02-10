# PAC Functions
A browser supporting PAC provides access to a list of functions as defined in the original Netscape Specification.

Each browser implements PAC in a sandbox, allowing access to only those JavaScript functions required to operate and nothing more. As an example, it isn’t possible to access the browser user agent string in a PAC file, a string available to a normal web page.

The functions supported and allowed by the sandbox environment are documented on this page.

The Functions

<details>
<summary>dnsDomainIs</summary>
Evaluates hostnames and returns true if hostnames match. Used mainly to match and exception individual hostnames.
<br>
<br>
<ins>Example</ins>

    // If the hostname matches google.com or www.google.com
    // send direct to the Internet.
    if (dnsDomainIs(host, "google.com") || dnsDomainIs(host, "www.google.com"))
        return "DIRECT";
    
</details>
<details>
<summary>shExpMatch</summary>
Will attempt to match hostname or URL to a specified shell expression, and returns true if matched.
<br>
<br>
<ins>Example 1</ins>
  
    // Any requests with a hostname ending with the extension .local
    // will be sent direct to the Internet.
    if (shExpMatch(host, "*.local"))
        return "DIRECT";

<ins>Example 2</ins>
      
    // A request for the host vpn.domain.com or any request for a file or folder in the
    // location http://abcdomain.com/folder/ will be sent direct to the Internet.
 
    if (shExpMatch(host, "vpn.domain.com") || 
        shExpMatch(url, "http://abcdomain.com/folder/*"))
            return "DIRECT";
</details>
<details>
<summary>isInNet</summary>
This function evaluates the IP address of a hostname, and if within a specified subnet returns true. If a hostname is passed the function will resolve the hostname to an IP address.
<br>
<br>
<ins>Example</ins>

    // If IP of requested website website falls within IP range, send direct to the Internet.
 
    if (isInNet(dnsResolve(host), "172.16.0.0", "255.240.0.0"))
        return "DIRECT";
</details>
<details>
<summary>myIpAddress</summary>
Returns the IP address of the host machine.
<br>
<br>
<ins>Example</ins>
    
    // If the machine requesting a website falls within IP range,
    // send traffic via proxy 10.10.5.1 running on port 8080.
 
    if (isInNet(myIpAddress(), "10.10.1.0", "255.255.255.0"))
        return "PROXY 10.10.5.1:8080";
</details>
<details>
<summary>dnsResolve</summary>
Resolves hostnames to an IP address. This function can be used to reduce the number of DNS lookups, e.g. below example.
<br>
<br>
<ins>Example</ins>
    
    // If IP of the requested host falls within any of the ranges specified, send direct.
 
    if (isInNet(dnsResolve(host), "10.0.0.0", "255.0.0.0") ||
        isInNet(dnsResolve(host), "172.16.0.0",  "255.240.0.0") ||
        isInNet(dnsResolve(host), "192.168.0.0", "255.255.0.0") ||
        isInNet(dnsResolve(host), "127.0.0.0", "255.255.255.0"))
        return "DIRECT";
</details>
<details>
<summary>isPlainHostName</summary>
This function will return true if the hostname contains no dots, e.g. http://intranet<br>
Useful when applying exceptions for internal websites, e.g. may not require resolution of a hostname to IP address to determine if local.
<br>
<br>
<ins>Example</ins>
    
    // If user requests plain hostnames, e.g. http://intranet/, 
    // http://webserver-name01/, send direct.
 
    if (isPlainHostName(host))
        return "DIRECT";
</details>
<details>
<summary>localHostOrDomainIs</summary>
Evaluates hostname and only returns true if exact hostname match is found.
<br>
<br>
<ins>Example</ins>
    
    // If the Host requested is "www" or "www.google.com", send direct.
 
    if (localHostOrDomainIs(host, "www.google.com"))
        return "DIRECT";
</details>
<details>
<summary>isResolvable</summary>
Attempts to resolve a hostname to an IP address and returns true if successful. WARNING – This may cause a browser to temporarily hang if a domain isn’t resolvable.
<br>
<br>
<ins>Example</ins>
    
    // If the host requested can be resolved by DNS, send via proxy1.example.com.
 
    if (isResolvable(host))
        return "PROXY proxy1.example.com:8080";
</details>
<details>
<summary>dnsDomainLevels</summary>
This function returns the number of DNS domain levels (number of dots) in the hostname. Can be used to exception internal websites which use short DNS names, e.g. http://intranet
<br>
<br>
<ins>Example</ins>
    
    // If hostname contains any dots, send via proxy1.example.com, otherwise send direct.
 
    if (dnsDomainLevels(host) > 0)
        return "PROXY proxy1.example.com:8080";
        else return "DIRECT";
</details>
<details>
<summary>weekdayRange</summary>
Allows rules to be time based, e.g. only return a proxy during specific days.
<br>
<br>
<ins>Example</ins>
    
    // If during the period of Monday to Friday, proxy1.example.com will be returned, otherwise
    // users will go direct for any day outside this period.
 
    if (weekdayRange("MON", "FRI")) return "PROXY proxy1.example.com:8080";
        else return "DIRECT";
</details>
<details>
<summary>dateRange</summary>
Allows rules to be time based, e.g. only return a proxy during specific months.
<br>
<br>
<ins>Example</ins>
    
    // If during the period of January to March, proxy1.example.com will be returned, otherwise
    // users will go direct for any month outside this period.
 
    if (dateRange("JAN", "MAR")) return "PROXY proxy1.example.com:8080";
        else return "DIRECT";
</details>
<details>
<summary>timeRange</summary>
Allows rules to be time based, e.g. only return a proxy during specific hours.
<br>
<br>
<ins>Example</ins>
    
    // If during the period 8am to 6pm, proxy1.example.com will be returned, otherwise
    // users will go direct for any time outside this period.
 
    if (timeRange(8, 18)) return "PROXY proxy1.example.com:8080";
        else return "DIRECT";
</details>
<details>
<summary>alert</summary>
The alert() function is not specified in the original PAC specification, although support was previously supported in several browsers, useful for outputting the value of a variable or result of a function in a manner that is viewable by the end-user and leveraged for troubleshooting PAC file rule issues.<br>
<br>
*This function is now considered unsupported and non-functional in PAC files.*
<br>
<br>
<ins>Example</ins>
    
    // Outputs the resolved IP address of the host in the browser
    // to end-user or error console. 
 
    resolved_host = dnsResolve(host);
    alert(resolved_host);
</details>

[Back to ReadMe](https://github.com/mdries-zs/findproxyforurl/blob/main/README.md)
