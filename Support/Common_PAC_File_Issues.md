# Common PAC File Issues

There are many reasons why a PAC file deployment might fail and these issues can range from the obvious to the obscure. This page details some common issues and how they can be resolved.

Click a question or problem in order to view the solution.

<details>
  <summary>My web browser doesn’t seem to be using the PAC file despite the PAC URL being configured, what are some possible reasons for this?</summary>

- Ensure that the web server has a MIME type ***application/x-ns-proxy-autoconfig*** configured for the *.pac* file extension. See the [PAC Deployment](https://github.com/mdries-zs/findproxyforurl/blob/main/Deployment/PAC_Deployment.md) page for more information.
- Disable the PAC file location in the browser proxy settings and enter the location of the PAC file in the browser URL bar, it should be accessible. If not, investigate the web server serving the file.
- Confirm that the JavaScript PAC file code is free of syntax errors/failures.
</details>

<details>
  <summary>After updating my PAC file, the change I made don’t seem to have taken effect?</summary>
Browsers will cache a PAC file rather than retrieve it for each request; in some cases a browser restart is insufficient for obtaining an updated version of the file.In order to obtain the latest version it may be necessary to clear the browser cache, close all browser windows, and reopen the browser application.
  
</details>

<details>
  <summary>Why might web browsing performance degrade when using a PAC file?</summary>
A PAC file may leverage several functions which rely on the local DNS server(s) in order to resolve a requested host. These functions are *isInNet()*, *isResolvable()*, and *dnsResolve()*.
<br><br>
Should a DNS server be slow to respond, the initialization of these functions for a new (non-cached) host will result in a delay until the result is provided by the DNS server(s). This will only occur the first time the host is requested, or if the local caching period for the host DNS information has expired.
<br><br>
Such an issue can be isolated by utilizing a DNS application such as DIG which can report how long it took the DNS server to respond. While each environment is unique, response times exceeding 500ms are likely to be noticeable to an end-user. Many websites now use content delivery networks which may provide content from several different hosts, thus the delay could be significant for larger websites; each host is requested in serial rather than parallel (each DNS request must complete before the next begins).
</details>

<details>
  <summary>Why might a browser initially stall/hang when configured with a PAC file and off-network?</summary>
  When using the IP address location of the PAC file, the browser will attempt to connect to this IP address and will wait until the connection attempt times out. The timeout may not occur for several seconds or more, and may result in some browsers hanging until this occurs. This delay will occur when the browser is first loaded and a website accessed.
<br><br>
Given this timeout behavior, if the user machine is to be taken off-network it’s recommended that the browser be configured with the DNS hostname for accessing the PAC file.
<br><br>
When using the DNS hostname for the PAC file, the browser will try to resolve the internal DNS hostname against an external DNS server. This will result in the server informing the web browser that no such DNS record exists. This process will take tenths of a second and is unnoticed by the end-user. The browser, being unable to access the PAC file, will fail open (direct to the Internet).
</details>

<details>
  <summary>I have multiple network adapters and the myIpAddress() function is returning an undesired IP address. Can I reorder the priority?</summary>
When assigning a value to the myIpAddress() function, a browser will use the first network adapter active and offered by the operating. Windows operating systems support re-arranging the network adapter order.

1. Click **Start**, click **Run**, type **ncpa.cpl**, and click **OK**.Available connections can be found in the LAN and High-Speed Internet section of the Network Connections window.
2. Using the **Advanced** menu, click **Advanced Settings**, and click the **Adapters and Bindings** tab.
3. In the **Connections** area, select the connection that you want to reorder. Use the arrow buttons to change the order.

Further instructions and information for configuring the network adapter order can be found in the [Microsoft Support Center](http://support.microsoft.com/kb/894564).
</details>

<details>
  <summary>I’m trying to load balance traffic between proxies using a PAC file, but applications and websites fail to load or produce error messages. How can I fix this?</summary>
There are several code examples available which make attempts at a viable load balancing solution when using a PAC file, unfortunately none of these examples can achieve true load balancing and often result in issues with connection management when using applications or websites requiring persistent connections and/or expecting traffic to traverse the same route. These solutions often depend on randomization in traffic routing using various JavaScript hacks, thus these solutions aren’t even providing true load-based distribution of traffic.
<br><br>
Load balancing across proxies is best achieved using a hardware solution that sits in front of the proxies themselves, which can track the load across each, and distribute this traffic based on current volume.
</details>

[Back to ReadMe](https://github.com/mdries-zs/findproxyforurl/blob/main/README.md)
