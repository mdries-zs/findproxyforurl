# Misconceptions

Although widely implemented, the [PAC specification](https://github.com/mdriesnj/findproxyforurl/blob/main/Support/netscape_documentation.md) is not a ratified standard, while the WPAD specification only got as far as being an [IETF draft](http://tools.ietf.org/html/draft-ietf-wrec-wpad-01), a draft which expired December 1999. This lack of standardization has resulted in some inconsistent PAC coding practices which do not reflect the actual implementation of the PAC specification in major browsers.

Despite this ambiguity the implementation of the PAC specification, with the exception of the myIpAddress() function, is consistent across browsers and operating systems.

This page attempts to dispel the reasons behind some common but unnecessary PAC coding practices. Code examples have been provided *as an example of what not to do*.

## Misconceptions

### In order to perform host matching the host variable must be converted to lowercase.

**False.** Implementing such code has been found unnecessary in all major browsers (Internet Explorer, Firefox, Chrome, and Safari).
No browser has been found to require that the host be converted to lowercase in order to prevent case sensitive matching issues. Unlike URLs, hosts are case insensitive therefore any PAC rule mechanism should automatically assume case insensitivity when matching hosts.

It’s possible that early browser implementations of the PAC specification had issues with this functionality, however, browsers as old as Internet Explorer 6 (released 2001) and Firefox 2 (released 2006) do not exhibit these issues.

**Example (of what not to do):**

	host_var = host.toLowerCase();
		if (dnsDomainIs(host_var, "example.com"))
			return "DIRECT";

<br><br>

### When using multiple DNS dependent PAC functions, a browser will perform a new DNS look-up for the same host with each function.
**False.** The PAC implementation by all major browsers (Internet Explorer, Firefox, Chrome, and Safari) has not been found to exhibit any unusual behavior when leveraging the DNS system.
If the browser accessed a host accessed recently, the local DNS cache will provide the DNS result to the browser. If a host hasn’t been accessed recently and is not in the DNS cache, the DNS servers configured for the host machine will be asked to provide the DNS result. This will be performed once and the result cached locally.

**Example (of what not to do):**

	resolved_host = dnsResolve(host);
	if (isInNet(resolved_host, "10.0.0.0", "255.0.0.0") || 
		isInNet(resolved_host, "172.16.0.0",  "255.240.0.0"))
		return "DIRECT";
