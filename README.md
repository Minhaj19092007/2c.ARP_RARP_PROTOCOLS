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
Client-ARP:
```
import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("ARP Server is listening on port 8000...")
c, addr = s.accept()

address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
}

while True:
    ip = c.recv(1024).decode()
    print(f"Received IP: {ip}")
    mac = address.get(ip, "Not Found")
    c.send(mac.encode())
```
Server-ARP:
```
import socket

s = socket.socket()
s.connect(('localhost', 8000))

while True:
    ip = input("Enter Logical Address (IP): ")
    s.send(ip.encode())
    print("MAC Address:", s.recv(1024).decode())
```
## OUPUT - ARP
Client-ARP:
  <img width="838" height="102" alt="image" src="https://github.com/user-attachments/assets/bedbc237-c9e1-470d-800d-d8862e4a8be6" />

Server-ARP:
 <img width="832" height="130" alt="image" src="https://github.com/user-attachments/assets/dd36dda6-6e7b-4207-8498-4d93c36bb014" />


## PROGRAM - RARP:
Client-RARP:
```
import socket

s = socket.socket()
s.bind(('localhost', 8001))
s.listen(5)
print("RARP Server is listening on port 8001...")
c, addr = s.accept()

address = {
    "6A:08:AA:C2": "165.165.80.80",
    "8A:BC:E3:FA": "165.165.79.1"
}

while True:
    mac = c.recv(1024).decode()
    print(f"Received MAC: {mac}")
    ip = address.get(mac, "Not Found")
    c.send(ip.encode())
```
Server-RARP:
```
import socket

s = socket.socket()
s.connect(('localhost', 8001))

while True:
    mac = input("Enter Physical Address (MAC): ")
    s.send(mac.encode())
    print("IP Address:", s.recv(1024).decode())
```
## OUPUT -RARP:
Client-RARP:
 <img width="842" height="108" alt="image" src="https://github.com/user-attachments/assets/642a1f52-f3ad-40a9-96fd-c86380f2a6e1" />

Server-RARP:
  <img width="834" height="129" alt="image" src="https://github.com/user-attachments/assets/1e42a55b-5157-48ac-bc2b-c0af22d8a44d" />


## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
