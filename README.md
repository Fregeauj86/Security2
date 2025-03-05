import requests
def check_security_headers(url):
    try:
        response = requests.get(url)
        headers = response.headers
        
        security_headers = [
            "Content-Security-Policy",
            "Strict-Transport-Security",
            "X-Frame-Options",
            "X-XSS-Protection",
            "X-Content-Type-Options",
            "Referrer-Policy"
        ]
        
        print(f"Security Headers Check for {url}\n")
        for header in security_headers:
            if header in headers:
                print(f"{header}: {headers[header]}")
            else:
                print(f"{header}: MISSING")
        
    except requests.exceptions.RequestException as e:
        print(f"Error checking security headers: {e}")

if __name__ == "__main__":
    website_url = input("Enter the website URL (including http/https): ")
    check_security_headers(website_url)
