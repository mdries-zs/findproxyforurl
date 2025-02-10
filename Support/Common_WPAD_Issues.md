# Common WPAD Issues

There are many reasons why a WPAD deployment might fail and these issues can range from the obvious to the obscure. This page details some common issues and how they can be resolved.

Click a question or problem in order to view the solution.

<details>
  <summary>I’m unable to resolve the WPAD host despite DNS being correctly configured?</summary>

  Windows 2008, and a subsequent update for Windows 2003 DNS, implemented a DNS block list (globalqueryblocklist) for commonly abused queries which may be blocking resolution of the WPAD host.

In order to allow Windows 2008 DNS to resolve the host WPAD, please see the [Microsoft article](http://technet.microsoft.com/en-us/library/cc995158.aspx) on this issue.

A command line option isn’t available for Windows 2003, thus changes need to be made to the Windows Registry.

1. Open the Windows Registry on each DNS server (e.g. Start > Run > Regedit).
2. Locate the registry key location in the table below.
3. Right-click > **Modify** on the **GlobalQueryBlockList** key.
4. Remove the **wpad** entry and click **OK**.
5. You will need to restart the Windows DNS Server service in order for this change to take effect.

| **Key** | HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DNS\Parameters |
| --- | --- |
| **Name** | GlobalQueryBlockList |
| **Type** | REG_MULTI_SZ |
| **Data** | wpad isatap |

</details>

<details>
  <summary>Firefox doesn’t locate my PAC file when using DHCP WPAD, why is this?
</summary>
  Firefox solely supports DNS WPAD, DHCP WPAD is not supported. Please see the [WPAD Introduction](http://findproxyforurl.com/wpad-introduction/) and [Browser Support](http://findproxyforurl.com/browser-support/) pages for more information.
</details>
