# 2c.SIMULATING ARP /RARP PROTOCOLS
## Name:Aanandha Kannan S
## Rego No: 212224040003
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
```
import socket

s = socket.socket()
s.bind(('localhost', 9000))
s.listen(5)
print("RARP Server listening on port 9000...")

c, addr = s.accept()
print("Connection from:", addr)

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
```
client.py
import socket

s = socket.socket()
s.connect(('localhost', 8000))

while True:
    ip = input("Enter logical Address : ")
    if ip.lower() in ['exit', 'quit']:
        break
    s.send(ip.encode())
    print("MAC Address:", s.recv(1024).decode())

s.close()
```
## Output
<img width="1007" height="386" alt="image" src="https://github.com/user-attachments/assets/bcfac8bf-d474-43cb-9885-a172b684a9f4" />

## PROGRAM - RARP
```
Server.py
import socket

s = socket.socket()
s.bind(('localhost', 9000))
s.listen(5)
print("RARP Server listening on port 9000...")

c, addr = s.accept()
print("Connection from:", addr)

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
```
client.py
import socket

s = socket.socket()
s.connect(('localhost', 9000))

while True:
    mac = input("Enter MAC Address : ")
    if mac.lower() in ['exit', 'quit']:
        break
    s.send(mac.encode())
    print("Logical Address:", s.recv(1024).decode())

s.close()
```
## OUTPUT
<img width="964" height="293" alt="Screenshot 2025-10-28 083517" src="https://github.com/user-attachments/assets/cc096971-8793-4258-b2f0-0caa2f810c95" />


## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
