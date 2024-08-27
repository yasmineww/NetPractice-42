# NetPractice-42
This repository is an overview on some networking concepts and basics, that you must know to validate this project.

In order to stay connected to the internet and correctly send your messages or as we say in networking **route your packets**, Internet must have a modular architecture or a design where a this network system is divided into separate layers, each handling a specific function in order support numerous networks and hosts.

# Internet’s architectural model : TCP/IP vs OSI

The Internet’s model is organized in a stack of 5 distinct layers. When Internet protocols first came to life, several models for were being developed. Among them, a model in 7 layers: the **OSI (Open Systems Interconnection)** model. However, the **OSI** was never completely adopted for the Internet. Although the OSI, as a theory, is still used in textbooks and training courses because of its early impact on network education.

<p align="center">
<img src="/media/Internet layers.png" width=50% height=50%>
</p>

Now let's discover how a packet gets transmitted along a network:

## Application layer - Message

This layer is where your message is born and is ready to get wrapped up and sent over many layers to come. This is the last time that a user can directly access a given file or data before it get transmitted. It provides **protocols** that allow software to send and receive information and present meaningful data to users. These protocols form the basis for various services like file transfer, web surfing, email, virtual terminals and much more:

| **Application** | **Protocol** |
| --- | --- |
| Request and transfer Web pages | HTTP, HTTPS |
| File transfer | FTP |
| Email transfer and access | SMTP, IMAP |
| Shell remote access with secure connection | SSH |
| Instant message transfer | IRC, XMPP |
| Clock synchronization to local time | NTP |
| Internet domain name translation into IP address | DNS |
| Streaming audio/video | RMTP, HLS, SRT |
| Peer-to-peer file sharing | BitTorrent, eDonkey |

## Presentation layer : Data format, encryption and compression

This layer performs 3 basic functions : 
  - **Translates** the message received from the application layer to machine understandable binary format.
  - **Reduces** the number of bits that are used to represent the original data, aka **data compression**, thus reduce the size of files. This is helpful to fasten data transmission.
  - **Encrypts or decrypts** the data to enhance the security of sensitive data using SSL protocol (secure socket protocol) ensuring that data is protected from possible eavesdropping.
  - Sets the **data format** to the convenient files types (.html, .jpg, .xml,….)

## Session layer

Responsible for **session management**, **authentication** and finally **authorization**. When two applications (running on different devices) want to communicate, the Session Layer starts the process by establishing a session. This involves setting up the parameters and rules for communication, ensuring both sides are synchronized and agree on how data will be exchanged. During the session, session layer ensures that data is exchanged smoothly, keeps the session organized by implementing mechanisms for recovery checkpoints preventing data loss, and manages the communication's direction. Once the communication is complete, the Session Layer is responsible for properly terminating the session, and releasing the allocated resources. It uses protocols like RTCP and L2TP.

<p align="center">
<img src="/media/Encapsulation.png" width=70% height=70%>
</p>

## Transport layer - Segments : TCP/ UDP, port number and sequence number

This layer is basically the same as when you  hand over a parcel to a certain shipping company, and have to decide which company to choose. Either the fastest or the most reliable, in our case. TCP and UDP protocols are your shipping companies, and both will get your packet delivered but offer different services. Now before we get into the details of both TCP and UDP protocols, let's explore what the transport layer has more to offer.

Packets of the transport layer are called **segments**. The primary focus of the transport layer is to ensure that data packets arrive in the right order, without losses or errors, or can be seamlessly recovered if required. This layer performs **Segmentation**, which ensures that the data is divided into small data units or segments each containing **source** and **destination port number** to direct each segment to the correct destination. While a **sequence number** is used to reassemble the segments into the correct order.

### TCP - Transmission Control Protocol

**TCP** is a **connection-oriented**, reliable transport protocol. This means that it ensures that a connection is established between the sender and the receiver before any data is sent and makes sure that the receiver got the data, otherwise it sends it again. This connction is established thanks to the 3-way-handshake : SYN, SYNACK, ACK. TCP includes built-in flow control mechanisms. Applications that generally use TCP are file, message and Web page transfer services that have to be sent as it is with no scratches or missing pieces.

### UDP - User Datagram Protocol

**UDP** offers a much simpler service with a **connection-less** transmission. Unlike TCP, it does not regulate traffic or its transmission rate (flow control), and does not guarantee message delivery. However, this protocol’s simplicity is useful for rapidly transmitting small segments of data. For example when a server sends data to several clients, or when data loss is preferable to waiting for it to be transmitted again. DNS, voice over IP, video streaming and online gaming are typical uses of UDP.

A real life example is when you are gaming online, your friend is in area A same as you but you're lagging due to your poor connection. When your wifi is becomes stable again, you see that your friend already left area A at this point in time. This is normal UDP. Now imagine if we were using TCP. The segments where your friend was in area A were not delivered. Later, your wifi stabilized and you're back to game, your friend tells you he left area A to go to area B. However, since it's TCP, all packets must be delivered no matter what. So now you see that your friend is still in area A, which is chronologically wrong.

Keep in mind that sometimes both TCP and UDP can be implemented at the same time. For example, when you ty to watch a streaming on a browser, the icons, video suggestions, ads and other elements are sent over TCP. The UDP is then used to stream your video that is loaded in the middle of the browser.

## Network layer - Packets : logical addressing IP

Transport layer passes data segments to the network layer, which transmits data packets from one network to another. This layer adds up sender and receiver ip address header to the segments. **Logical addressing** (IPV4, IPV6 and MASK), routing and path determination are the main functions of this layer. **Routing** is moving data packets from source to destination based on the logical address format. **Path determination** involves choosing the best possible path for data delivery. The network layer uses protocols like OSPF, BGP and IS-IS.

## Data link layer - Frames : physical addressing MAC

This layer handles the physical transmission of data between network nodes (like computers, routers, or switches) on the same network. It uses **physical addressing** of MAC addresses to ensure that data is physically delivered correctly on a local network. **A mac address is a number embedded in the hardware of the computer**. Physical addressing is adding a frame header to the packet that assign mac addresses of sender and receiver to each data packet and form a **frame**. The receiving node's link layer receives the frame and extracts the segment from the frame and then hands it up to the network layer of this node, then determines the **next hop** based on the destination address (read about router's forwarding tables). The link layer protocols are, for the most part, related to the physical transport medium between two nodes in the network. Some of the link-layer protocols are Ethernet, WiFi, DOCSIS and PPP.

## Physical Layer

The physical layer can convert the bits into physical elements, electrical, light, or radio signals, and finally gets to the final destination.

