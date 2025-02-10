# PAC Functions
A browser supporting PAC provides access to a list of functions as defined in the original Netscape Specification.

Each browser implements PAC in a sandbox, allowing access to only those JavaScript functions required to operate and nothing more. As an example, it isn’t possible to access the browser user agent string in a PAC file, a string available to a normal web page.

The functions supported and allowed by the sandbox environment are documented on this page.

The Functions

- dnsDomainIs
