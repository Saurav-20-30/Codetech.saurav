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
