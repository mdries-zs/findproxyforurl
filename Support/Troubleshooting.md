# Troubleshooting

It can be difficult to isolate issues with PAC files, a task only complicated when using the WPAD deployment method. It’s recommended that certain steps be followed to isolate an issue in a PAC/WPAD environment and this page attempts to document this process.

These processes focus specifically on an inability to access a PAC file or a failure of the WPAD deployment methods. For other types of issues, please review the common issue sections for [PAC](https://github.com/mdriesnj/findproxyforurl/blob/main/Support/Common_PAC_File_Issues.md) and [WPAD](https://github.com/mdriesnj/findproxyforurl/blob/main/Support/Common_WPAD_Issues.md).

It’s recommended to use the Official [FindProxyForURL.com toolset](insertlink) to aid in a troubleshooting investigation of any PAC or WPAD issues.

Click a deployment in order to view the recommended troubleshooting process.

<details>
  <summary>Explicit PAC</summary>

- Review the PAC file code manually. Syntax issues often arise due to missing commas, parentheses, curly braces, or semi-colons.
- Ensure that the PAC file code validates using a tool such as [pacparser](http://code.google.com/p/pacparser/) or [Proxy Validator](http://luno.org/project/proxyvalidator/).
- Review the PAC file rules for any unintended routing behaviors; common issues include missing proxy return statements and wildcard based rules affecting a larger volume of traffic than intended. Such errors could result in all traffic passing directly to the Internet, making it only *appear* that the file is failing to function.
- Confirm that the PAC file extensions (.pac or .dat) are being served with either of the following content types:<br>&nbsp;&nbsp;&nbsp;&nbsp;**application/x-ns-proxy-autoconfig**<br>&nbsp;&nbsp;&nbsp;&nbsp;**application/x-javascript-config**
- Test the PAC file by hosting the file on the local file system; if the file works, this would isolate the issue to the PAC file web server (e.g. connectivity or configuration). The URL format for local PAC file testing is **file://c:\folder\proxy.pac**

</details>

<details>
  <summary>WPAD DHCP</summary>

  - Follow the steps for troubleshooting an explicit PAC file configuration – WPAD is a means of deploying a PAC file, thus any issues with the web server or the file itself could be overlooked if focusing solely on the WPAD portion.
- Test the PAC file URL being pushed out by DHCP, do so by using the PAC file URL in the browser proxy settings configured as an explicit PAC file. This will verify whether the PAC file or PAC file server itself is the issue.
- Review the Windows Registry to confirm the URL being pushed out by WPAD DHCP.
    1. Click **Start** and Select **Run**.
    2. Type *regedit* and click **OK**.
    3. Navigate the Registry tree to the following location: HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\
    4. In the pane to the right, double click **DefaultConnectionSettings**.
    5. The WPAD DHCP URL will be displayed in the dialog box – [screenshot](https://github.com/mdriesnj/findproxyforurl/blob/main/Images/screenshot.png?raw=true)
  
</details>
