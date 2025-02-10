# Deploying PAC Files
Deploying a PAC file explicitly using the browser proxy settings is one of the most straightforward methods for deployment. Once you have a fully formed PAC file, the below steps will aid in deploying a PAC file on a web server.

## Web Server

The web server should be configured to serve a [PAC file](https://github.com/mdriesnj/findproxyforurl/blob/main/Pac_File_Coding/Example.md) with the correct MIME type.

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
  7. Enter the below information:**Extension:** *.pac***MIME Type:** *application/x-ns-proxy-autoconfig*
  8. Click **OK**.
</details>

<details>
  <summary>Apache Web Server</summary>

  1. Create .htaccess file.
  2. Add the below line into the file: <br>&nbsp;&nbsp;&nbsp;&nbsp;*AddType application/x-ns-proxy-autoconfig .pac*
  3. Upload the file to the same location as the PAC file.
 
</details>

## Browser Deployment

Depending on the administrative environment, browsers can be configured automatically using a tool such as Group Policy, or manually for each browser’s connection settings.
<details>
  <summary>Group Policy</summary>

  1. Open the **Group Policy Object Editor**.
  2. Expand the **User Configuration > Windows Settings > Internet Explorer Maintenance tree**.
  3. Open **Connection** and select **Automatic Browser Configuration**.
  4. Check **Enable Automatic Configuration**.
  5. Enter the URL for the PAC file in the **Auto-proxy URL** text box, click **OK**.
 
</details>
<details>
  <summary>Manual Browser Configuration</summary>

### Internet Explorer

1. Open Internet Explorer.
2. Select **Tools** from the application menu, click **Internet Options**.
3. Click the **Connections** tab, click the **LAN settings** button.
4. Check **Use automatic configuration script**, click **OK**.
5. Enter the URL for the PAC file in the **Address** text box, click **OK**.

### Firefox

1. Open Firefox.
2. Select **Tools** from the application menu, click **Options**.
3. Click the **Advanced** section, click **Settings** under **Connection**.
4. Select **Automatic proxy configuration URL**.
5. Enter the URL for the PAC file in the text box, click **OK**.

### Safari (Windows)

Safari utilizes the Windows proxy settings as used in Internet Explorer. Please follow the instructions for Internet Explorer.

### Google Chrome (Windows)

Like Safari, Chrome utilizes the Windows proxy settings as used in Internet Explorer. Please follow the instructions for Internet Explorer.

### Opera (Windows)

1. Open Opera.
2. Click the **Opera** button.
3. Click **Settings > Preferences**section.
4. Click **Advanced**, select **Network**, and click **Proxy Servers**.
5. Select **Use automatic proxy configuration**.
6. Enter the URL for the PAC file in the text box, click **OK**.

</details>
