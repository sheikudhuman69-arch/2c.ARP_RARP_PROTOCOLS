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
## client.py
```
Client:
import socket
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Waiting for client connection...")
c, addr = s.accept()
print("Connected to:", addr)
address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
}
while True:
    ip = c.recv(1024).decode()
    if not ip:   
        break
    print("Requested IP:", ip)
    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not Found".encode())
c.close()
s.close()
```

## Server.py:
```
import socket
s = socket.socket()
s.connect(('localhost', 8000))
while True:
    ip = input("Enter Logical Address: ")
    if ip.lower() == "exit":
        break
    s.send(ip.encode())
    mac = s.recv(1024).decode()
    print("MAC Address:", mac)
s.close()
```
## OUPUT - ARP
<img width="956" height="415" alt="image" src="https://github.com/user-attachments/assets/6ce3eefa-3736-49b1-b26b-53f82ff5dd3e" />

## PROGRAM - RARP
## client.py
```
import socket
s = socket.socket()
s.bind(('localhost', 9000))
s.listen(5)
print("Waiting for client connection...")
c, addr = s.accept()
print("Connected to:", addr)
address = {
    "6A:08:AA:C2": "192.168.1.100",
    "8A:BC:E3:FA": "192.168.1.99"
}
while True:
    mac = c.recv(1024).decode()
    if not mac: 
        break
    print("Requested MAC:", mac)
    try:
        c.send(address[mac].encode())
    except KeyError:
        c.send("Not Found".encode())
c.close()
s.close()
```

## server.py
```
import socket
s = socket.socket()
s.connect(('localhost', 9000))
while True:
    mac = input("Enter MAC Address: ")
    if mac.lower() == "exit":
        break
    s.send(mac.encode())
    print("Logical Address:", s.recv(1024).decode())
s.close()
```
## OUPUT -RARP
<img width="956" height="263" alt="image" src="https://github.com/user-attachments/assets/ff7bde68-a841-4cc4-aa84-7686345cf15b" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
