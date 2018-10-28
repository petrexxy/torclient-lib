# torclient-lib
A Simple, Lightweight and Easy To Use, TOR Proxy Library For Python

How To Install:

Download the zip file or clone the repo with:

    git clone http://github.com/petrexxy/torclient-lib

After, run the setup.py installation script with the install argument:

    python setup.py install
    
This will install the dependencies. If not, run:
 
    pip install -r requirements.txt
    
Then all the requirements and the library itself should be ready to use
For more information on how to use it, check out the example.py script.

How to use:

First, create a configuration to control your proxy server via the script:

    import torclient
    my_proxy_config = torclient.ControlConfig()
    my_proxy_config.SetControlPort(9051) #default tor control port
    my_proxy_config.SetAuthentication("my super secret password")
    my_proxy_config.Apply() #apply settings
    
When you're finished, you can check your config with:

    my_proxy_config.ShowConfig()
    
    '{"Control Port": 9051, "Authentication": "my super secret password"}'
    
Next, setup the proxy connections:

    proxy_session = torclient.ProxySocket()
    proxy_socket  = proxy_session.InitProxy("localhost", 9050, False) #localhost = server, 9050 = port, False = not global proxy sockets (more info in example.py)

Now, you can use 'proxy_socket' just like a normal socket object, and it goes through the proxy! You can also set up a non-proxy socket along side it!:

    import socket
    proxy_socket = proxy_sesison.InitProxy("localhost", 9050, False) # as we declared before
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM) # normal socket without proxy!
    
    proxy_socket.close()
    s.close()

