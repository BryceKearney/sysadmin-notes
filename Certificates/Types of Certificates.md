Can be used to secure a RD Gateway for RDP.

### 🔒 **Standard SSL Certificate**

- **Secures a single domain or subdomain**.
    
- Example: A certificate for `remote.yourdomain.com` will **only** secure that specific FQDN.
    
- It **won’t cover** `www.remote.yourdomain.com` or `mail.yourdomain.com`.
    

---

### 🌟 **Wildcard SSL Certificate**

- **Secures one domain and all of its subdomains** at a single level.
    
- Example: A wildcard cert for `*.yourdomain.com` secures:
    
    - `remote.yourdomain.com`
        
    - `mail.yourdomain.com`
        
    - `vpn.yourdomain.com`
        
    - and so on...
        
- But it **does not cover** sub-subdomains like `sub.mail.yourdomain.com`.
    

---

### ✅ When to Use Each

| Scenario                                       | Use a Standard SSL | Use a Wildcard SSL |
| ---------------------------------------------- | ------------------ | ------------------ |
| You only need to secure one FQDN               | ✔️                 | ❌                  |
| You have many subdomains to secure             | ❌                  | ✔️                 |
| You want simpler certificate management        | ❌                  | ✔️                 |
| Cost is a concern and you only need one domain | ✔️                 | ❌                  |
|                                                |                    |                    |
