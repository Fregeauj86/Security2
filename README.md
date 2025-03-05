import requests

def check_security_headers(url):
    try:
        headers_to_check = [
            "Content-Security-Policy",
            "Strict-Transport-Security",
            "X-Frame-Options",
            "X-XSS-Protection",
            "X-Content-Type-Options",
            "Referrer-Policy",
        ]
        
        response = requests.get(url)
        headers = response.headers
        
        print(f"\nSecurity Headers Check for {url}\n" + "-" * 50)
        missing_headers = []
        
        for header in headers_to_check:
            if header in headers:
                print(f"{header}: {headers[header]}")
            else:
                print(f"{header}: MISSING")
                missing_headers.append(header)
        
        print("\nSummary:")
        print(f"Found: {len(headers_to_check) - len(missing_headers)}")
        print(f"Missing: {len(missing_headers)}")
    
    except requests.exceptions.RequestException as e:
        print(f"Error checking security headers: {e}")

if __name__ == "__main__":
    website_url = "https://www.earthkidsacademy.com/careers"
    check_security_headers(website_url)
