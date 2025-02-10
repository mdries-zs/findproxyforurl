# Deployment Options

### Comparing Deployments

Web browsers provide several methods for specifying the use of a proxy:

- **Explicit Proxy** – A single proxy is specified in the browser with a literal proxy bypass list.
- **PAC File** – The location of a PAC file is specified (e.g. hosted locally or on a web server) in the browser. The PAC file can provide proxy fail-over support, advanced proxy bypass support , and much more (see below).
- **WPAD** – Only requiring a check box be selected in the browser, the browser may use DHCP or DNS in attempt to guess the location of the PAC file.

| **Deployment** | **Advantages** | **Disadvantages** |
| --- | --- | --- |
| **Explicit** | • Simple to deploy, does not require additional infrastructure.• Doesn’t require JavaScript knowledge.• Supported in all major browsers. | • No fail-over functionality.• Proxy bypass lists are literal, browsers do not resolve host to IP and vice versa. Both the IP and host may need to be specified in the bypass list. |
| **PAC** | • Proxy fail-over support.• Supported in all major browsers.• Ability to bypass proxy for specific hosts or IP addresses seamlessly. | • Most deployments will require web server infrastructure.• Requires JavaScript knowledge.• Some browsers may fail closed if the PAC file is unavailable (e.g. when off-network). |
| **WPAD** | • Includes all PAC advantages.• Deployment only requires a check box be selected.• Browser fails open if WPAD cannot locate a PAC file (e.g. when off-network). | • Includes all PAC disadvantages.• Requires DNS or DHCP infrastructure changes. |
