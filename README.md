import requests

def check_security_headers(url):
    try:
        headers_to_check = {
            "Content-Security-Policy": "Defines security policies for the browser.",
            "Strict-Transport-Security": "Forces secure (HTTPS) connections.",
            "X-Frame-Options": "Prevents clickjacking attacks.",
            "X-XSS-Protection": "Mitigates cross-site scripting (XSS) attacks.",
            "X-Content-Type-Options": "Prevents MIME-type sniffing.",
            "Referrer-Policy": "Controls how much referrer info is sent.",
        }
        
        response = requests.get(url, headers={"User-Agent": "Mozilla/5.0"})
        headers = response.headers
        
        print(f"\nSecurity Headers Check for {url}\n" + "-" * 50)
        missing_headers = []
        
        for header, description in headers_to_check.items():
            if header in headers:
                print(f"\033[92m✔ {header}: {headers[header]}\033[0m")
            else:
                print(f"\033[91m✘ {header}: MISSING - {description}\033[0m")
                missing_headers.append(header)
        
        print("\nSummary:")
        print(f"✔ Found: {len(headers_to_check) - len(missing_headers)}")
        print(f"✘ Missing: {len(missing_headers)}")
    
    except requests.exceptions.RequestException as e:
        print(f"\033[91mError checking security headers: {e}\033[0m")

if __name__ == "__main__":
    website_url = "https://www.earthkidsacademy.com/careers"
    check_security_headers(website_url)
