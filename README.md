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
### Client
```
import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Server is listening...")

c, addr = s.accept()
print("Connection from:", addr)

address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
}

while True:
    ip = c.recv(1024).decode()
    if not ip:
        break
    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not Found".encode())

c.close()
s.close()
```
### Server
```
import socket

s = socket.socket()
s.connect(('localhost', 8000))

while True:
    ip = input("Enter logical address: ")
    if not ip:
        break
    s.send(ip.encode())
    print("MAC Address:", s.recv(1024).decode())

s.close()
```
## OUPUT - ARP
### Client
<img width="842" height="296" alt="image" src="https://github.com/user-attachments/assets/0c6a89aa-e955-454b-bc78-44685fafad95" />


### Server
<img width="839" height="299" alt="image" src="https://github.com/user-attachments/assets/4bebad91-438f-4e03-bc20-65aa023e901a" />

## PROGRAM - RARP
### Server
```
import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Server is listening...")

c, addr = s.accept()
print("Connection from:", addr)

address = {
    "6A:08:AA:C2": "165.165.80.1",
    "8A:BC:E3:FA": "165.165.79.1"
}

while True:
    ip = c.recv(1024).decode()
    if not ip:
        break
    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not Found".encode())

c.close()
s.close()

```
### Client
```
import socket

s = socket.socket()
s.connect(('localhost', 8000))

while True:
    ip = input("Enter MAC address: ")
    if not ip:
        break
    s.send(ip.encode())
    print("Logical Address:", s.recv(1024).decode())

s.close()

```
## OUPUT -RARP
### Client
<img width="1655" height="563" alt="image" src="https://github.com/user-attachments/assets/11d9d420-9d61-4182-bd75-b59b7761b93e" />

### Server
<img width="1670" height="725" alt="image" src="https://github.com/user-attachments/assets/4198ee02-bd4e-442f-ab82-2520e350ccfd" />


## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
