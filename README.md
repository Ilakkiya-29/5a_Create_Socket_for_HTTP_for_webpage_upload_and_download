# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download

## AIM :

To write a PYTHON program for socket for HTTP for web page upload and download

## Algorithm

1.Start the program.
<BR>
2.Get the frame size from the user
<BR>
3.To create the frame based on the user request.
<BR>
4.To send frames to server from the client side.
<BR>
5.If your frames reach the server it will send ACK signal to client otherwise it will send NACK signal to client.
<BR>
6.Stop the program
<BR>

## Program
## server.py

```
import socket

s = socket.socket()
s.bind(("localhost",8080))
s.listen(1)

print("Server running...")

while True:
    c,addr = s.accept()
    
    request = c.recv(1024).decode()
    print("Request received")

    if "GET" in request:
        f = open("index.html","r")
        data = f.read()
        f.close()

        response = "HTTP/1.1 200 OK\n\n" + data
        c.send(response.encode())

    elif "POST" in request:
        data = request.split("\n\n")[1]

        f = open("upload.txt","w")
        f.write(data)
        f.close()

        c.send("HTTP/1.1 200 OK\n\nFile Uploaded".encode())

    c.close()
```

## client.py

```
import socket

s = socket.socket()
s.connect(("localhost",8080))

ch = input("1.Download 2.Upload : ")

# Download webpage
if ch == "1":
    req = "GET / HTTP/1.1\nHost: localhost\n\n"
    s.send(req.encode())

    data = s.recv(4096)
    print(data.decode())

# Upload file
else:
    msg = input("Enter data to upload: ")

    req = "POST / HTTP/1.1\nHost: localhost\n\n" + msg
    s.send(req.encode())

    data = s.recv(1024)
    print(data.decode())

s.close()
```

## index.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Welcome Page</title>
</head>
<body>
    <h1>Welcome to the Python HTTP Server!</h1>
    <p>This is the default page served by the server.</p>

</body>
</html>
```

## OUTPUT

## server.py(download)

<img width="422" height="192" alt="image" src="https://github.com/user-attachments/assets/d27846a7-ba94-40dc-ba5f-94e9312ffaf6" />

## client.py(download)

<img width="603" height="467" alt="image" src="https://github.com/user-attachments/assets/c2b60d1d-8350-4b67-bd5b-8142b8f79cae" />

## server.py(upload)

<img width="425" height="162" alt="image" src="https://github.com/user-attachments/assets/8e8c0a3e-e033-4cd2-99d0-c8893c31bd0a" />

## client.py(upload)

<img width="565" height="152" alt="image" src="https://github.com/user-attachments/assets/c6649afa-e4b2-4a2e-8468-c5613522a000" />

<img width="1021" height="422" alt="image" src="https://github.com/user-attachments/assets/7e035e03-2ebd-4620-9afc-0cb2076ec5ab" />

## Result
Thus the socket for HTTP for web page upload and download created and Executed
