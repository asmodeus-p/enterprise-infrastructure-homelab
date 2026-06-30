# Network Topology

                  [ Physical Home Router ]
                    (IP: 192.168.100.1)
                             |
                             | (Physical Wi-Fi/Ethernet)
                             |
             [ Host Machine's Physical NIC ]
                   (IP: 192.168.100.12)
                             |
                +-------------------------+
                | VirtualBox Bridge/Switch|
                +-------------------------+
                             |
                 +-----------+-----------+
                 |                       |
          [ Kali Linux VM ]       [ Ubuntu Server VM ]
       ( IP: 192.168.100.107)     (IP: 192.168.100.105)
                 |                       |
                 +------- SSH Traffic ---+
