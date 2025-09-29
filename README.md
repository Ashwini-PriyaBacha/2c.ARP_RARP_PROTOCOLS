# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.
P
## PROGRAM - ARP
# Server
```
import socket
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Server is listening...")

c, addr = s.accept()
print(f"Connection established with {addr}")

address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
}

while True:
    ip = c.recv(1024).decode()

    if not ip:  
        break

    try:
        mac = address[ip]  # Get the MAC address for the IP
        print(f"IP: {ip} -> MAC: {mac}")
        c.send(mac.encode())  
    except KeyError:
        print(f"IP: {ip} not found in ARP table.")
        c.send("Not Found".encode())
c.close()
s.close()
```
# Client
```
import socket
c = socket.socket()
c.connect(('localhost', 8000))

while True:
    ip = input("Enter IP address to find MAC (or type 'exit' to quit): ")

    if ip.lower() == "exit":  
        break

    c.send(ip.encode())
    mac = c.recv(1024).decode()
    print(f"MAC Address for {ip}: {mac}")
c.close()
```
## OUTPUT - ARP
<img width="1920" height="1140" alt="Screenshot 2025-09-29 182128" src="https://github.com/user-attachments/assets/0b75e985-b590-4065-8928-4b17fce2f8b9" />

## PROGRAM - RARP
# server
```
import socket

s = socket.socket()
s.bind(('localhost', 9000)) 
s.listen(5)
print("Server listening on port 9000...")

c, addr = s.accept()
print("Connection established with:", addr)
address = {
    "6A:08:AA:C2": "192.168.1.100",
    "8A:BC:E3:FA": "192.168.1.99"
}

while True:
    mac = c.recv(1024).decode()
    if not mac:
        break
    try:
        c.send(address[mac].encode())
    except KeyError:
        c.send("Not Found".encode())

c.close()
s.close()
```
# Client
```

import socket

s = socket.socket()
s.connect(('localhost', 9000))   # connect to server

while True:
    mac = input("Enter MAC Address : ")
    if mac.lower() == "exit":
        break
    s.send(mac.encode())
    print("Logical Address:", s.recv(1024).decode())

s.close()
```
## OUPUT -RARP
<img width="1920" height="1140" alt="Screenshot 2025-09-29 182112" src="https://github.com/user-attachments/assets/fd06066f-9fe3-49d5-a621-d9c58a2a80d4" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
