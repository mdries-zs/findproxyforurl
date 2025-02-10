# Browser Support

The technology behind PAC files and the WPAD protocol never became ratified standards, and as such, the implementation of functionality across each browser and operating system can vary. The below tables provide guidance on the support for each PAC/WPAD feature, cross-referencing browser and operating system.

### Windows 10

| **Feature** | **Internet Explorer 11** | **Microsoft Edge** | **Mozilla Firefox** | **Google Chrome** | **Apple Safari** |
| --- | --- | --- | --- | --- | --- |
| **DNS WPAD** | Yes | Yes | Yes | Yes | Yes |
| **DHCP WPAD** | Yes | Yes | No | Yes | Yes |
| **myIpAddress()** | Yes | Yes | Yes | Yes | Yes |
| **IPv6** | Yes | Yes | No | Yes | Yes |

### Mac OS X (El Capitan/10.11.1)

| **Feature** | **Mozilla Firefox** | **Google Chrome** | **Apple Safari** |
| --- | --- | --- | --- |
| **DNS WPAD** | Yes | Yes | Yes |
| **DHCP WPAD** | No | No | No |
| **myIpAddress()** | Yes | Yes | Yes |
| **IPv6** | Yes | Yes | Yes |

### Feature Descriptions

**DNS WPAD** – Support for discovery of a PAC file using DNS

**DHCP WPAD** – Support for discovery of a PAC file using DHCP

**myIpAddress()** – Returns an IP address other than 127.0.0.1

**IPv6** – The ability to handle IPv6 addresses using built-in functions, e.g. using FindProxyForURLEx()

