# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
To write a python program to perform sliding window protocol
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
server.py
```python
import socket
s = socket.socket()
s.bind(('localhost', 9999))
s.listen(1)
print("Server listening...")
conn, addr=s.accept()
print(f"Connected to {addr}")

while True:
    frames = conn.recv(1024).decode()
    if not frames:
        break


    print(f"Received frames: {frames}")
    ack_message = f"ACK for frames: {frames}"
    conn.send(ack_message.encode())
conn.close()
s.close()

```





client.py
```python
import socket

c = socket.socket()
c.connect(('localhost', 9999))

size = int(input("Enter number of frames to send: "))
I = list(range(size))

print("Total frames to send:", len(I))
s = int(input("Enter Window Size: "))

i = 0
while i < len(I):
    st = i + s
    frames_to_send = I[i:st]
    print(f"Sending frames: {frames_to_send}")
    
    c.send(str(frames_to_send).encode())

    ack = c.recv(1024).decode()
    if ack:
        print(f"Acknowledgment received: {ack}")
        i += s  

c.close()


```

## OUPUT

<img width="1055" height="214" alt="image" src="https://github.com/user-attachments/assets/2c5bfeb5-e5e2-4c45-b61f-616f204de848" />

<img width="1053" height="216" alt="image" src="https://github.com/user-attachments/assets/6cb550bc-819d-4a45-b908-d267334a861d" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
