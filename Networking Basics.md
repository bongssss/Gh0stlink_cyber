#### Troubleshooting commands
examples of utilities are 
- **Ipconfig/ifconfig** Displays IP configuration information.
- **ping(nmap -sn)**- Tests connections to other IP hosts.
- **netstat** - Displays network connections.
- **tracert** - Displays the route taken to the destination.
- **nslookup** - Directly queries the name server for information on a destination domain.





### Network Types 
- Private
- Public
- there are are also two means of identification of hosts or systems on networks namely ip address and MAC address

### IP Addresses

An IP address (or Internet Protocol) address can be used as a way of identifying a host on a network for a period of time, where that IP address can then be associated with another device without the IP address changing.

An IP address is a set of numbers that are divided into **four octets**. IP addresses can change from device to device but cannot be active simultaneously more than once within the same network.

IP Addresses follow a set of standards known as protocols. These protocols are the backbone of networking and force many devices to communicate in the same language. Devices can be on both a private and public network. Depending on where they are will determine what type of IP address they have: a public or private IP address.

A public address is used to identify the device on the Internet, whereas a private address is used to identify a device amongst other devices on a private network. Public IP addresses are given by your ISP at a monthly fee
ip  addresses re divided into the network part (the fitst three octets) and the host part (last octet)

**Two types of IP addresses, IPv4 and IPv6.**
example (`ipv4` 32 bit in 4 octets of 8 bits each) `192.168.1.200`
example (`ipv6` 128 bit in groups of 4 hexadecimal numbers of 16 bits each) `2001:0db8:85a3:0000:0000:8a2e:0370:7334`

### MAC (Media Access Control) Addresses
Devices on a network will all have a physical network interface card (NIC), which is a microchip board found on the device's motherboard. This network interface card is assigned a unique address at the factory it was built at, called a MAC address. The MAC address is a twelve-character hexadecimal number. The first six characters represent the company that made the network interface, and the last six is a unique number.
 example **00:0a:95:9d:68:16.**


### Ping
 A Ping uses ICMP (Internet Control Message Protocol) packets to determine the performance of a connection between devices, for example, if the connection exists or is reliable.
 

# Introduction to LAN 
 A network that spans a small physical area. Usually used by organisations and homes.
There are different topologies (arrangement of hosts and networking devices in a LAN )that can be considered to be Local Area Networks. 


### STAR Topology
all hosts are individually connected to a single central networking device such as a switch, a hub or a router.

### Bus topology 
this type of LAN depends on hosts and network devices being connected to a backbone cable.

### Ring Topology
hosts and network devices are connected to each other in form of a loop.



### Switches
Usually found in larger networks they are used for aggregating/connecting a large number of devices using ethernet ports/cables. they are usually found in larger local area networks some switch ports include. switches keep track of what network device (host or otherwise ) is connected to which port using a **MAC** **address** table. this helps a switch reduce network traffic by routing a packet to the right mac address.

**ethernet** is a networking technology developed in the 1970s that is used to facilitate wired communication between hosts or part of a local area network using protocols/ standards (i.e., fast ethernet) that control the passing of information from one host to another, avoiding  simultaneous transmission data by different hosts.


### Routers

Routers provide a connection between networks and provide an exchange of data between them. An example is the communication between a home (private) network and an **ISP** (public) network which provides access to the wider internet. It does this by finding the path of least resistance between different networks for the effective flow of data.

### IP Subnetting
This is the process of splitting the number of hosts that can fit into a network using a number called a subnet mask. a subnet mask which is also represented as a number of four bytes (32 bits or **four octets**, same as an ip address), ranging from 0 to 255 (0-255). Here, for the `255.255.255.0` Subnet Mask, we can use **/24** at the end of an ip address (in the host part, this is usually done when trying to scan a subnet for the exact number of hosts present). 

Subnets use IP addresses in 3 ways:
- Identify the network address
- Identify the host address
- Identify the default gateway (router address)

Example: A café has two networks:
1. One for employees, cash registers, and other devices for the facility
2. One for the general public to use as a hotspot
    

### Network address
is basically the network part of an IP address with a 0 appended to the host part i.e., for the ip address `192.168.1.200`, the network address would be `192.168.1.0`.

### ARP (Address Resolution Protocol)

is the technology that is responsible for allowing devices to identify themselves on a network. It allows a device to associate its MAC address with an IP address on the network. Each device on a network will keep a log of the MAC addresses associated with other devices. MAC addresses are used as the physical identifiers and IP addresses are used as the logical identifiers for a device on a network.

### DCHP (Dynamic Host Configuration Protocol)

IP addresses can be assigned either manually, by entering them physically into a device, or automatically and most commonly by using a DCHP server. When a device connects to a network, if it has not already been manually assigned an IP address, it sends out a request (DHCP Discover) to see if any DHCP servers are on the network. The DHCP server then replies back with an IP address the device could use (DHCP Offer). The device then sends a reply confirming it wants the offered IP Address (DHCP Request), and then lastly, the DHCP server sends a reply acknowledging this has been completed, and the device can start using the IP Address (DHCP ACK).


---
description: >-
  Learn about how you request content from a web server using the HTTP
  protocol...
---

# HTTP in detail

## What is HTTP(S)?

[<mark style="color:green;">HTTP</mark>](#user-content-fn-1)[^1] is the protocol that <mark style="color:yellow;">specifies how a web browser and a web server communicate</mark>. It is what's used whenever you view a website, developed by Tim Berners-Lee and his team between 1989-1991.

[<mark style="color:green;">HTTPS</mark>](#user-content-fn-2)[^2] is the secure version of HTTP. <mark style="color:yellow;">HTTPS data is encrypted</mark> so it not only stops people from seeing the data you are receiving and sending, but it also gives you assurances that you're talking to the correct web server and not something impersonating it.

***

## Requests & Responses

### What is a URL?

If you’ve used the internet, you’ve used a URL before. <mark style="color:green;">A</mark> [<mark style="color:green;">URL</mark>](#user-content-fn-3)[^3] <mark style="color:green;">is predominantly an instruction on how to access a resource on the internet.</mark>

[<mark style="color:blue;">http</mark>](#user-content-fn-4)[^4]://[<mark style="color:green;">user:password</mark>](#user-content-fn-5)[^5]@[<mark style="color:red;">tryhackme.com</mark>](#user-content-fn-6)[^6]/[<mark style="color:yellow;">80</mark>](#user-content-fn-7)[^7]/[<mark style="color:purple;">view-room</mark>](#user-content-fn-8)[^8][<mark style="color:orange;">?id=1</mark>](#user-content-fn-9)[^9][<mark style="color:blue;">#task3</mark>](#user-content-fn-10)[^10]

**Scheme:** This instructs on what protocol to use for accessing the resource such as HTTP, HTTPS, FTP (File Transfer Protocol).

**User:** Some services require authentication to log in, you can put a username and password into the URL to log in.

**Host:** The domain name or IP address of the server you wish to access.

**Port:** The Port that you are going to connect to, usually 80 for HTTP and 443 for HTTPS, but this can be hosted on any port between 1 - 65535.

**Path:** The file name or location of the resource you are trying to access.

**Query String:** Extra bits of information that can be sent to the requested path. For example, /blog?id=1 would tell the blog path that you wish to receive the blog article with the id of 1.

**Fragment:** This is a reference to a location on the actual page requested. This is commonly used for pages with long content and can have a certain part of the page directly linked to it, so it is viewable to the user as soon as they access the page.

<mark style="color:yellow;">It's possible to make a request to a web server with just one line "GET / HTTP/1.1".</mark>

### Example Request

{% code lineNumbers="true" %}
```http
GET / HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0 Firefox/87.0
Referer: https://tryhackme.com/

```
{% endcode %}

**Line 1:** This request is sending the GET method ( more on this in the HTTP Methods task ), request the home page with / and telling the web server we are using HTTP protocol version 1.1.

**Line 2:** We tell the web server we want the website tryhackme.com

**Line 3:** We tell the web server we are using the Firefox version 87 Browser

**Line 4:** We are telling the web server that the web page that referred us to this one is https://tryhackme.com

**Line 5:** HTTP requests always end with a blank line to inform the web server that the request has finished.

### Example Response

{% code lineNumbers="true" %}
```http
HTTP/1.1 200 OK
Server: nginx/1.15.8
Date: Fri, 09 Apr 2021 13:34:03 GMT
Content-Type: text/html
Content-Length: 98

<html>
<head>
    <title>TryHackMe</title>
</head>
<body>
    Welcome To TryHackMe.com
</body>
</html>
```
{% endcode %}

**Line 1:** HTTP 1.1 is the version of the HTTP protocol the server is using and then followed by the HTTP Status Code in this case "200 OK" which tells us the request has completed successfully.

**Line 2:** This tells us the web server software and version number.

**Line 3:** The current date, time and timezone of the web server.

**Line 4:** The Content-Type header tells the client what sort of information is going to be sent, such as HTML, images, videos, pdf, XML.

**Line 5:** Content-Length tells the client how long the response is, this way we can confirm no data is missing.

**Line 6:** HTTP response contains a blank line to confirm the end of the HTTP response.

**Lines 7-14:** The information that has been requested, in this instance the homepage.

***

## HTTP Methods

### GET Request

<mark style="color:yellow;">This is used for getting information from a web server.</mark>

### POST Request

<mark style="color:yellow;">This is used for submitting data to the web server and potentially creating new records.</mark>

### PUT Request

<mark style="color:yellow;">This is used for submitting data to a web server to update information.</mark>

### DELETE Request

<mark style="color:yellow;">This is used for deleting information/records from a web server.</mark>

***

## HTTP Status Codes

When a HTTP server responds, the first line always contains a status code informing the client of the outcome of their request and also potentially how to handle it. These status codes can be broken down into 5 different ranges:

<details>

<summary>100-199 (Information Response)</summary>

These are sent to tell the client the first part of their request has been accepted and they should continue sending the rest of their request. These codes are no longer very common.

</details>

<details>

<summary>200-299 (Success)</summary>

This range of status codes is used to tell the client their request was successful.

</details>

<details>

<summary>300-399 (Redirection)</summary>

These are used to redirect the client's request to another resource. This can be either to a different webpage or a different website altogether.

</details>

<details>

<summary>400-499 (Client Errors)</summary>

Used to inform the client that there was an error with their request.

</details>

<details>

<summary>500-599 (Server Errors)</summary>

This is reserved for errors happening on the server-side and usually indicate quite a major problem with the server handling the request.

</details>

### Common Codes

```
200 - OK
201 - Created
301 - Moved Permanently
302 - Found
400 - Bad Request
401 - Not Authorised
403 - Forbidden
404 - Page Not Found
405 - Method Not Allowed
500 - Internal Service Error
503 - Service Unavailable
```

***

## Headers

<mark style="color:green;">Headers are additional bits of data you can send to the web server when making requests.</mark>

Although no headers are strictly required when making a HTTP request, you’ll find it difficult to view a website properly.

### Common Request Headers

**Host:** Some web servers host multiple websites so <mark style="color:yellow;">by providing the host headers you can tell it which one you require, otherwise you'll just receive the default website for the server</mark>.

**User-Agent:** This is your <mark style="color:yellow;">browser software and version number</mark>, telling the web server your browser software <mark style="color:yellow;">helps it format the website properly</mark> for your browser and also some elements of HTML, JavaScript and CSS are only available in certain browsers.

**Content-Length:** When sending data to a web server such as in a form, the content length <mark style="color:yellow;">tells the web server how much data to expect in the web request</mark>. This way the server can ensure it isn't missing any data.

**Accept-Encoding:** Tells the web server <mark style="color:yellow;">what types of compression methods the browser supports</mark> so the data can be made smaller for transmitting over the internet.

**Cookie:** Data sent to the server to <mark style="color:yellow;">help remember your information.</mark>

### Common Response Headers

**Set-Cookie:** Information to store which <mark style="color:yellow;">gets sent back to the web server on each request.</mark>

**Cache-Control:** How long to store the content of the response in the browser's cache before it requests it again.

**Content-Type:** This tells the client what type of data is being returned, i.e., HTML, CSS, JavaScript, Images, PDF, Video, etc. Using the content-type header the browser then knows how to process the data.

**Content-Encoding:** What <mark style="color:yellow;">method has been used to compress the data</mark> to make it smaller when sending it over the internet.

***

## Cookies

<mark style="color:green;">They're a small piece of data that is stored on your computer.</mark> Cookies are saved when you receive a "Set-Cookie" header from a web server. Then every further request you make, you'll send the cookie data back to the web server. Because <mark style="color:yellow;">HTTP is stateless</mark> (doesn't keep track of your previous requests), cookies can be used to <mark style="color:yellow;">remind the web server who you are,</mark> some personal settings for the website or whether you've been to the website before. They have other uses, but are most commonly used for website authentication.



<figure><img src="https://1297820784-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FIncHpQE9Q1Ax4cr7Wbpu%2Fuploads%2FJNfHYd3BE2DdYB4odJg1%2Fimage.png?alt=media&#x26;token=edcd5b2a-2e30-44e8-9280-d8b2974eda3f" alt=""><figcaption><p>Example HTTP Request</p></figcaption></figure>

***

## Coded Requests

```http
GET /blog?id=1 HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0 Firefox/87.0
```

```http
DELETE /user/1 HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0 Firefox/87.0
Content-Length: 4

id=1
```

```http
PUT /user/2 HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0 Firefox/87.0
Content-Length: 14

username=admin
```

```http
POST /login HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0 Firefox/87.0
Content-Length: 33

username=thm&password=letmein
```

***

