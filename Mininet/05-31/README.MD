## 05-31上課

- COPY-TO-CPU實驗  

![](COPY.jpg)
![](0.PNG)

- TCP
    - server
    ```
    import socket
    import sys

    # Create a TCP/IP socket
    sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

    # Bind the socket to the port
    server_address = ('10.0.0.2', 10000)
    print >>sys.stderr, 'starting up on %s port %s' % server_address
    sock.bind(server_address)

    # Listen for incoming connections
    sock.listen(1)

    connection, client_address = sock.accept()
    print >>sys.stderr, 'connection from', client_address
    data = connection.recv(1024)
    print >>sys.stderr, 'received "%s"' % data
    connection.close()
    ```
    - client
    ```
    import socket
    import sys

    # Create a TCP/IP socket
    sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

    # Connect the socket to the port where the server is listening
    server_address = ('10.0.0.2', 10000)
    print >>sys.stderr, 'connecting to %s port %s' % server_address
    sock.connect(server_address)

    # Send data
    message = 'hello world'
    print >>sys.stderr, 'sending "%s"' % message
    sock.sendall(message)
    sock.close()
    ```

![](1.PNG)

- SENT-TO-CPU實驗   

![](2.PNG)
![](3.PNG)

- SENT-TO-CPU2實驗  

![](4.PNG)

![](5.PNG)

### 範例
- p4的broadcast與multicast

![](0.jpg)

- h1 send h2、h3 receive

![](6.PNG)

- 同理，h3 send h1、h2 receive

![](7.PNG)