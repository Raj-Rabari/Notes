# Networking Basics

**Protocols**: Protocols are rules set by standards organizations (like the IETF) on how data will get transferred over a network.

- **TCP**: It guarantees that 100% of the data will get transferred (by retransmitting any lost packets).
- **UDP**: It comes into the picture when you just have to transfer the data and don't care about if it's transferred successfully or not (prioritizes speed over reliability).

---

## Home Networking & IP Addresses

Your home's Wi-Fi router has one global IP address which is connected to the internet. All the devices connected to the home's router will have the same global IP address from the outside perspective. The router will assign local IPs to them using the **DHCP** protocol.

When you make a request to some server (let's say `google.com`), the server will see your router's global IP and will send the response to the router. Now, the router will route the response to the correct device using the local IP using **NAT (Network Address Translation)**. Which specific application made this request on that device is decided using **ports**.

---

## Hardware

- **Modem**: Converts digital signals into analog signals (and vice versa).
- **Router**: Routes data to the correct devices.

OSI model : open Systems interconnection

Application Layer: it is the code from where you start the data transport using protocols like HTTP, HTTPs, FTP, Telnet, SMTP etc.

Presentation Layer: transform data in binary or machine understandable format, perform encryption and compression. SSL protocol is used for securing the data.

Session Layer: Authentication & Authorization

Transport Layer: data segmentaion done on this layer, each segment contains port number and sequence number. It also work on flow control(like if the server can be able to send at 40Mbps but client can't receive it at that speed then it controls that). error control(like in TCP, it does it using acknoledgment, if any segment or package fails then retransmit that)

Network Layer: handles transmission of data on nodes that are in another networks. this is the layer where router is get used. It assigns sender's and receiver's IP address to the data packets.

Data-link Layer:
Physical Layer:
