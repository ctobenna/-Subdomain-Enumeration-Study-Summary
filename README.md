<h1>🧠 Subdomain Enumeration Study Summary</h1>

Today, I studied **subdomain enumeration** — an essential part of reconnaissance in cybersecurity and penetration testing.

**Subdomain enumeration** is the process of identifying valid subdomains associated with a target domain. This helps **expand the attack surface**, increasing the chances of discovering vulnerable systems or entry points.

---

## 🔍 Techniques Studied

### 1. OSINT - SSL/TLS Certificates

When a domain owner requests an SSL/TLS certificate from a **Certificate Authority (CA)**, it is logged in a publicly accessible system called **Certificate Transparency (CT) logs**. The main goal of CT logs is to prevent misuse of certificates — but they also provide **valuable OSINT data**.

We can search these logs to identify subdomains that may not be visible through standard DNS queries. A popular tool for this is:

- 🔗 [crt.sh](https://crt.sh)

**Example usage on crt.sh**  
Search using: `%domain.com`  
This will return all current and historical subdomains for the domain.

---

### 2. OSINT - Search Engines

Search engines like **Google** and **Bing** index billions of pages, including subdomains. By using **advanced search operators**, we can discover hidden subdomains.

**Examples:**
    
    site:*.domain.com -site:www.domain.com
    site:domain.com -www

The `-` symbol tells the search engine to **exclude** results like `www.domain.com`.

---

### 3. DNS Bruteforce

DNS bruteforce enumeration involves guessing possible subdomains using a predefined list of common names. This method sends multiple DNS queries to try and identify active subdomains.

**Tool Used:** `dnsrecon`

**Example:**
dnsrecon -t brt -d domain.com

### 4. OSINT - Sublist3r
To speed up the enumeration process, we can use Sublist3r, a Python-based tool that automates the discovery of subdomains from public sources.

**Example:**
    ./sublist3r.py -d domain.com

### 5. Virtual Host Enumeration
Some subdomains may not appear in DNS results because they're:

- Hosted on internal systems

- Used for development or administration

- Mapped only in private DNS or host files:

  - /etc/hosts (Linux/macOS)

  - C:\Windows\System32\drivers\etc\hosts (Windows)

**Web servers** can host multiple websites (virtual hosts) on a single IP address. When a browser sends a request, it includes a Host header to tell the server which subdomain it wants. By modifying the Host header, we can discover hidden subdomains — similar to DNS bruteforce.

**Tool Used:** ffuf

*Example:**
    ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt  -H "Host: FUZZ.domain.com" -u http://domain.com  -fs 2395


*Flag Breakdown:*
-  -w: Path to the wordlist
-  -H: Adds or modifies the HTTP header
-  -u: The base URL or IP of the target
-  -fs: Filter by response size (used to ignore standard responses)

### ✅ Conclusion
Subdomain enumeration is a powerful technique for mapping a target’s infrastructure. By combining OSINT, DNS brute-forcing, and virtual host fuzzing, you can uncover hidden assets that might otherwise be missed — a crucial step in any ethical hacking workflow.

