This error will pop up when the certificate is expired
![[RD Gateway.png]]

-----------------------------------

Instructions on how to check and renew

Log into Server > Open tools > Remote desktop services > License manager > is certificate trusted or expired

If expired, purchase a new trusted certificate, make sure to put your domain in and give it a few minutes for DNS to authenticate

----------------
* Install OpenSSL, sometimes a restart is required or you have to do it locally on your own PC
* This should be a decent guide, made from Grok

### Step 1: Prepare the New SSL Certificate

1. **Verify Certificate Files**:
    - Ensure you have the new certificate (e.g., newcert.crt), private key (e.g., newcert.key), and any intermediate/CA bundle (e.g., ca-bundle.crt).
    - If the certificate is in a different format (e.g., .pem, .cer, or .pfx), use OpenSSL to convert it to the required format (Windows typically uses .pfx for RDS Gateway).
2. **Convert Certificate to PFX (if needed)**: RDS Gateway requires a .pfx file (which includes the certificate, private key, and CA chain). If your certificate is in separate files, combine them using OpenSSL:
    
    bash
    
    Copy
    
    `openssl pkcs12 -export -out newcert.pfx -inkey newcert.key -in newcert.crt -certfile ca-bundle.crt`
    
    - Replace newcert.key, newcert.crt, and ca-bundle.crt with your file names.
    - Enter a password when prompted (remember it for later).
3. **Verify the PFX File**: Ensure the .pfx file is valid:
    
    bash
    
    Copy
    
    `openssl pkcs12 -in newcert.pfx -noout -info`
    
    - Enter the password to check the contents.
4. **Copy Files to the Server**:
    - Transfer the .pfx file (or individual certificate files if you’ll convert them on the server) to the RDS Gateway server (e.g., via RDP or a secure file transfer method).

### Step 2: Install the Certificate on the RDS Gateway

1. **Import the Certificate to Windows Certificate Store**:
    - Log in to the RDS Gateway server.
    - Open the **Microsoft Management Console (MMC)**:
        - Press Win + R, type mmc, and press Enter.
        - Go to File > Add/Remove Snap-in, select **Certificates**, and click **Add**.
        - Choose **Computer account** > **Local computer**, then click **Finish** and **OK**.
    - In the MMC, expand **Certificates (Local Computer)** > **Personal** > **Certificates**.
    - Right-click the **Certificates** folder, select **All Tasks** > **Import**.
    - Browse to the .pfx file, enter the password, and complete the import.
    - Ensure the certificate appears in the store and has a private key (indicated by a key icon).
2. **Verify Certificate Properties**:
    - Double-click the imported certificate in MMC.
    - Check that the **Subject Name** matches the RDS Gateway’s fully qualified domain name (FQDN) (e.g., rdgateway.example.com).
    - Confirm the certificate is valid (not expired) and includes the CA chain under **Certification Path**.

### Step 3: Configure RDS Gateway to Use the New Certificate

1. **Open RDS Gateway Manager**:
    - Open **Server Manager** > **Tools** > **Remote Desktop Services** > **RD Gateway Manager**.
    - Right-click the server name and select **Properties**.
2. **Update the SSL Certificate**:
    - In the **Properties** window, go to the **SSL Certificate** tab.
    - Select **Select an existing certificate** and click **Import Certificate**.
    - Browse to the certificate you imported in the **Personal** store (it should list the new certificate).
    - Select the certificate and click **Apply** > **OK**.
3. **Restart the RDS Gateway Service**:
    - Open **Services** (services.msc).
    - Find **Remote Desktop Gateway**, right-click, and select **Restart**.
    - Alternatively, run in Command Prompt (as admin):
        
        cmd
        
        Copy
        
        `net stop tsgateway && net start tsgateway`
        

### Step 4: Test and Verify

1. **Test Connectivity**:
    - From a client machine, connect to the RDS Gateway using Remote Desktop (ensure the client trusts the new certificate’s CA).
    - Verify that there are no SSL errors or certificate warnings.
2. **Verify Certificate with OpenSSL** (optional):
    - From a machine with OpenSSL, test the RDS Gateway’s SSL configuration:
        
        bash
        
        Copy
        
        `openssl s_client -connect rdgateway.example.com:443 -showcerts`
        
    - Replace rdgateway.example.com with your RDS Gateway’s FQDN.
    - Check the output for the new certificate details and ensure the chain is complete.
3. **Check Event Logs**:
    - On the RDS Gateway server, open **Event Viewer** (eventvwr.msc).
    - Navigate to **Windows Logs** > **Application** or **System** and look for errors related to the RD Gateway service.

### Step 5: Clean Up

- Securely delete any temporary certificate files (e.g., .key, .pfx) from the server.
- Back up the new certificate and private key in a secure location.
- Document the certificate’s expiration date to avoid future issues.

### Troubleshooting

- **Certificate Not Trusted**: Ensure the CA chain is included in the .pfx file and imported correctly. Clients must trust the issuing CA.
- **RDS Gateway Fails to Start**: Verify the certificate’s private key is present and the Subject Name matches the server’s FQDN.
- **OpenSSL Errors**: If OpenSSL commands fail, ensure the certificate files are in the correct format (e.g., PEM or DER) and not corrupted.

### Notes

- OpenSSL is primarily used here for certificate conversion and verification. The actual certificate installation on Windows uses native tools (MMC, RDS Gateway Manager).
- If you’re using a self-signed certificate (not recommended for production), you can generate one with OpenSSL:
    
    bash
    
    Copy
    
    `openssl req -x509 -newkey rsa:2048 -keyout newcert.key -out newcert.crt -days 365 -nodes`
    
    Then convert to .pfx as shown above.
- Ensure the certificate’s Subject Alternative Name (SAN) includes the RDS Gateway’s FQDN to avoid client warnings.

If you encounter specific errors or need help with a particular step, please provide details (e.g., error messages, certificate format, or server configuration), and I can tailor the guidance further.