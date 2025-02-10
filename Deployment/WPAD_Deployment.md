# Deploying WPAD

# PAC File

In order for the DNS WPAD functionality to detect the PAC file, rename the PAC file to **wpad.dat** and upload to your web server.

# Web Server

The web server should be configured to serve a [PAC file](https://github.com/mdries-zs/findproxyforurl/blob/main/Pac_File_Coding/Example.md), **wpad.dat**, with the correct MIME type.
<details>
  <summary>IIS Server</summary>

  1. Login to the server through Terminal Services or Remote Desktop Connection.
  2. Click **Start**, select **Programs**, and then click **Administrative Tools**.
     1. For IIS 5.0: Open Internet Services Manager.
     2. For IIS 6.0: Open Internet Information Services.
  3. In the left column you will see the Server Name.
     1. In IIS 5.0: expand the Server Name to find the domain name.
     2. In IIS 6.0: expand the Server Name and then Web Sites to find the domain name. 
  4. Right-click on the domain name and select **Properties**.
  5. On the HTTP Headers tab click **MIME Types**.
  6. Click **New**.
  7. Enter the below information:<br>&nbsp;&nbsp;&nbsp;&nbsp;**Extension:** *.dat<br>&nbsp;&nbsp;&nbsp;&nbsp;***MIME Type:** *application/x-ns-proxy-autoconfig*
  8. Click **OK**.
</details>

<details>
  <summary>Apache Web Server</summary>

  1. Create .htaccess file.
  2. Add the below line into the file: <br>&nbsp;&nbsp;&nbsp;&nbsp;*AddType application/x-ns-proxy-autoconfig .dat*
  3. Upload the file to the same location as the wpad.dat file.
 
</details>

# DHCP Server

The DHCP server should be configured to serve a 252 entry in the DHCP information sent to a user. When configured this entry includes a direct link to the **wpad.dat** file.

<details>
  <summary>Windows 2003 DHCP</summary>

  1. Click **Start**, click **Programs**, click **Administrative Tools**, and then click **DHCP**.
  2. In the console tree, right-click on the DHCP server, click **Set Predefined Options**, and then click **Add**.
  3. In **Name** type: *WPAD*
  4. In **Code** type: *252*
  5. In **Data** type, select **String**, and then click **OK**.
  6. In String, type URL of PAC file in format: *http://webserver.example.com/wpad.dat*
  7. Right-click **Server Options** and click **Configure Options**.
  8. Confirm that the **Option 252** option is selected.

Once created we must then enable the option for a DHCP scope.

  1. Click **Start**, click **Programs**, click **Administrative Tools**, and then click **DHCP**.
  2. Right-click **Scope Options** and then click **Configure Options**.
  3. Click **Advanced**, and then in **Vendor Class**, click **Standard Options**.
  4. In **Available Options**, select the **252 Proxy Autodiscovery option** and click OK.
</details>

<details>
  <summary>Lunix DHCP</summary>

1. Edit the DHCP configuration file (usually */etc/dhcp/dhcpd.conf*).
2. Edit and paste the following into the file:  <br>&nbsp;&nbsp;&nbsp;&nbsp;option local-pac-server code 252 = text;option local-pac-server “http://wpad.example.com:80/wpad.dat”;  <br>&nbsp;&nbsp;&nbsp;&nbsp;<br>The first declaration must go in the global section of the configuration file.
3. Restart the DHCP server.
  
</details>

# DNS Server

The DNS server should be configured to serve an A record for the host **wpad**.
<details>
  <summary>Windows 2003 DNS</summary>

1. Click **Start**, click **Programs**, click **Administrative Tools**, and then click **DNS**.
2. In the console tree right-click on the applicable forward lookup zone and click **New Host (A)**.
3. In **Name** type: *wpad*
4. In **IP Address**, enter the IP address of the web server hosting the wpad.dat file.

</details>

# Browser Deployment

Depending on the administrative environment, browsers can be configured automatically using a tool such as Group Policy, or manually for each browser’s connection settings.

<details>
  <summary>Group Policy</summary>
The Group Policy settings will apply to Internet Explorer, Chrome, and Safari. Third party tools may be required for Firefox to adopt these Group Policy settings.

1. Open the **Group Policy Object Editor**.
2. Expand the **User Configuration** > **Windows Settings** > **Internet Explorer Maintenance** tree.
3. Open **Connection** and select **Automatic Browser Configuration**.
4. Check **Automatically detect configuration settings**.
  
</details>

<details>
  <summary>Manual Browser Configuration</summary>

### Internet Explorer

1. Open Internet Explorer.
2. Select **Tools** from the application menu, click **Internet Options**.
3. Click the **Connections** tab, click the **LAN settings** button.
4. Check **Automatically detect settings**, click OK.

### Firefox

1. Open Firefox.
2. Select **Tools** from the application menu, click **Options**.
3. Click the **Advanced** section, click **Settings** under **Connection**.
4. Select **Auto-detect proxy settings for this network**, click OK.

### Safari (Windows)

Safari utilizes the Windows proxy settings as used in Internet Explorer. Please follow the instructions for Internet Explorer.

### Google Chrome (Windows)

Like Safari, Chrome utilizes the Windows proxy settings as used in Internet Explorer. Please follow the instructions for Internet Explorer.

### Opera (Windows)

Opera doesn’t support the WPAD protocol.
</details>

[Back to ReadMe](https://github.com/mdries-zs/findproxyforurl/blob/main/README.md)
