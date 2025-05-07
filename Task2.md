import requests
from bs4 import BeautifulSoup

def scan_sql_injection(url):
    payloads = ["'", "' OR '1'='1", '" OR "1"="1']
    vulnerable = False

    print(f"Scanning {url} for SQL Injection...")
    for payload in payloads:
        try:
            response = requests.get(url + payload)
            if "sql" in response.text.lower() or "mysql" in response.text.lower():
                vulnerable = True
                print(f"Potential SQL Injection found with payload: {payload}")
        except:
            pass

    if not vulnerable:
        print("No SQL Injection found.")

def scan_xss(url):
    payload = "<script>alert('XSS')</script>"
    response = requests.get(url + "?q=" + payload)
    if payload in response.text:
        print("XSS vulnerability found!")
    else:
        print("No XSS vulnerability found.")

# Example
target_url = "http://example.com/search"  # replace with your test site
scan_sql_injection(target_url)
scan_xss(target_url)
