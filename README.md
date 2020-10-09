# Digital Forensics Network Forensics Challenge
## Created by: Tom Danner, Devin Ingresoll, Jesse Reed, Vitaliy Tsytsyk

### Software/Tools Used:
<p align="center">
  <img src="https://github.com/tsytsykvitaliy/digital-forensics-network-forensics-challenge/blob/main/Wireshark_Logo.png" width="800" height="221" />
</p>

#### Overview

Wireshark is a tool used for capturing/sniffing packets and analyzing packet captures.

#### Installing Wireshark
Windows/macOS: You can download the installer from their website here: https://www.wireshark.org/

Linux: Search for wireshark-qt using your respective distro's methods and select the most up to date version. A few have been included here.

Ubuntu

`sudo apt-get install wireshark`

Arch

`sudo pacman -S wireshark-qt`

Redhat/CentOS
```
sudo yum install gcc gcc-c++ bison flex libpcap-devel qt-devel gtk3-devel rpm-build libtool c-ares-devel qt5-qtbase-devel qt5-qtmultimedia-devel qt5-linguist desktop-file-utils
sudo yum install wireshark wireshark-qt
```

<p align="center">
  <img src="https://github.com/tsytsykvitaliy/digital-forensics-network-forensics-challenge/blob/main/tshark_logo.png">
</p>

#### Overview

TShark is the CLI counterpart of Wireshark. It enables the user to perform many of the same tasks they can do in Wireshark through the CLI instead. It also allows users to create scripts to automate the packet capture analysis process.

#### Installing TShark
Windows: (Requires choclatey to be installed) `choco install wireshark`

macOS: (Requires brew to be installed) `brew cask install wireshark`

Linux: By default it is included when installing Wireshark. Refer to the Wireshark installation steps for your respective distro.

### Topics Covered:
1. TCP/IP packet structure. An Overview/Introduction to Wireshark.
2. Basic Packet Analysis in Wireshark.
3. Advanced Packet Analysis in Wireshark.
4. An Overview/Introduction to TShark.

## Overview:
Network Forensics is a crucial part of digital forensics and its importance continues to grow everyday.
Almost all personal computers and servers are going to have built-in networking capabilities, such as wi-fi or ethernet, allowing them to communicate with other devices across the internet.
These connections can be used to transfer illegal files, deny normal service, and allow malware to go on and become viral.                                                                                                                                                           

Network data can also be difficult to track due to the huge volume and voliticity of conversations between devices.                                                                                                                                                                      
As a result of this, networking data has to be deliberatly listened to and saved for analysis in order to extract evidence. This is called "sniffing."                                                                                                                                                                

In our overview of network forensics we will first cover the most common language that computers communicate with: the TCP/IP packet structure.                                                                                                                              
After we learn how to read these, we'll dive into how you can aquire and analyse network information with one of the most common tools in the field: Wireshark!                                                                                                                  
Once we have the basics down, we'll lastly take a look at some more advanced topics dealing with Wireshark and TShark.



## TCP/IP packet structure and An Overview/Introduction to Wireshark




## Basic Packet Analysis and Filtering in Wireshark

### The Tip of The Iceberg

Packets (also referred to as frames) contain a large amount of information, so it's always best to start with what we can see easily. Let's take a look at the _Packet Listing_ window and gather the information from there first. We are going to use `Basics.pcap` in this section.

![](DNS_listing.png)  
_Screenshot of the Packet Listing window_  

We will be analyzing packet #3.
Just by looking at all the columns that correspond to our packet (row), we can gather the following information:

- **Number**: 3  
_The number of the packet in the capture file_
- **Time**: 0.000041  
_Absolute time since the beginning of the capture (in seconds)_
- **Source**: 10.0.0.132  
_The system that sent the packet. In most cases, the IPv4 address_
- **Destination**: 10.0.0.2  
_The system that received the packet. In most cases, the IPv4 address_
- **Protocol**: DNS  
_An application layer protocol that the packet used_
- **Length**: 86  
_Number of bytes in this packet_
- **Info**: Standard query 0x332e A www.offensive-security.com  
_Summary of the information in the highest layer protocol_

This is the easiest way to see the most common information about the packets. However, there is much more that can be uncovered.

### Digging Deeper

Glancing at the _Packet Listing_ is always nice, but it's rarely enough. If we want to learn more about the packet, we should click on it and explore the _Packet Details_. We have already discussed what information goes in each one of the layers (drop down rows) in the previous section so it will be easier to analyze our specific DNS packet, knowing that information. We will start from the top of the list with the physical layer, and work our way to the bottom - the "highest" protocol.

#### Physical Layer

![](physical.png)  
_Screenshot of the physical layer information we have about the DNS packet._  

There is plenty of rows to look at and there are lots of resources out there that break them all down, but right now we are just going to focus on the most important information:

- **Arrival Time**: Feb 3, 2010 16:26:52.129870000 Central Standard Time  
_Time of the packet arrival at the destination_
- **Epoch Time**: 1265236012.129870000  
_Also called UNIX time, this is a number of seconds since January 1, 1970_
- **Frame Number**: 3  
_Packet number in this capture_
- **Frame Length**: 86 bytes (688 bits)  
_Packet length_
- **Protocols in frame**: eth:ethertype:ip:udp:dns  
_All protocols used by the packet (by layer)_  

#### Data Link Layer

![](data-link.png)  
_Screenshot of the data link layer information we have about the DNS packet._  

- **Destination**: VMware_f9:77:70 (00:50:56:f9:77:70)  
_Destination MAC address_  
- **Source**: VMware_0b:97:ef (00:0c:29:0b:97:ef)  
_Source MAC address_  
- **Type**: IPv4 (0x0800)  
_Indicates which upper layer protocol should be used_  

#### Network Layer

![](network.png)  
_Screenshot of the network layer information we have about the DNS packet._  

- **Total Length**: 72  
_Length of the IP packet (20 bytes - the header, the rest - data)_  
- **Identification**: 0x2807 (10247)  
_A unique ID of the IP packet_  
- **Flags**: 0x4000, Don't fragment  
_Any flags set for the packet. In our case, "Don't fragment" bit is set to 1, which forbids packet fragmentation_  
- **Time to live**: 64  
_The maximum time (in seconds) the packet is allowed to exist on the network_  
- **Protocol**: UDP (17)  
_Indicates which upper layer protocol should be used. Number inside the parentheses indictes an assigned port number for that protocol on the IP layer_  
- **Header checksum**: 0xfe18 \[validation disabled]  
_The header checksum value and its validation status_  
- **Source**: 10.0.0.132  
_An IPv4 address of the system that sent the packet_
- **Destination**: 10.0.0.2  
_An IPv4 address of the system that received the packet_

#### Transport Layer

![](transport.png)  
_Screenshot of the transport layer information we have about the DNS packet._  

- **Source Port**: 35540  
_Port from which the packet has been sent_  
- **Destination Port**: 53  
_Port to which the packet has been sent_  
- **Length**: 52  
_Length of the UDP packet (8 bytes - the header, the rest - data)_  
- **Checksum**: 0x2d94 \[unverified]  
_The checksum value and its verification status_  

#### Application Layer

![](dns.png)  
_Screenshot of the application layer information we have about the DNS packet._  

- **Transaction ID**: 0x332e  
_A unique ID of the query-response pair_  
- **Flags**: 0x0100 Standard query  
_Any flags set to the packet. In our case, this packet is a query (0), a standard one (0), not truncated (0), recursively done (1), Z reserved (0), and doesn't accept non-authenticated data (0)_  
- **Questions**: 1  
_Number of requests_  
- **Answer RRs**: 0  
_Number of answers_  
- **Queries**: www.offensive-security.com: type A, class IN  
_All requests included in this packet. In our case, we only have one_  

As we can see, there is plenty of information about the packets that we can access with Wireshark. All the things we were able to tell about the DNS query packet #3 is visible by just clicking on the packet in the _Packet Listing_ window and paying close attention to the fields. However, this is a single packet. What if we want to search through hundreds of packets to find something specific? This is where our next topic comes in - filtering.

### Filtering

#### Display Filter

The easiest way to filter the packets is by using Wireshark's _Display Filter_ that is located right under the _Command Menu_.

![Display Filter](display-filter.png)  
_Screenshot of the Command Menu and the Display Filter_  

_Display Filter_ doesn't quite work the way `Ctrl + F` does on the web pages, so it's important to understand the correct way to build the expressions.

Let's look at the basic syntax.  

- To only display packets containing a specific protocol - just type in that protocol.  
_For example, `http`_  

- To filter them out further - type in that protocol, period, and further filterign options.  
_For example, to only show the http responses - type in `http.response`_  

- To compare values - use the comparison operators. Wireshark supports both C-like and English syntax for them.  
_For example, to only show packets with the source IP address 10.0.0.2 - type in `ip.src == 10.0.0.2` or `ip.src eq 10.0.0.2`_  

- To combine expressions - use the logical operators. Wireshark supports both C-like and English syntax for them.  
_For example, to only show packets with the source IP address 10.0.0.2 or the source IP address 10.0.0.132 - type in `ip.src == 10.0.0.2 || ip.src == 10.0.0.132` or `ip.src eq 10.0.0.2 or ip.src eq 10.0.0.132`_  

For more detailed explanation and extra content check out the [Wireshark's User Guide on Building Display Filter Expressions](https://www.wireshark.org/docs/wsug_html_chunked/ChWorkBuildDisplayFilterSection.html).

## Advanced Packet Analysis in Wireshark



## An Overview/Introduction to TShark
TShark is the terminal oriented version of Wireshark that can capture and display packets without the need for an interactive user interface. Without having any options set, TShark works in a similar way as a tcpdump. To begin capturing packets with TShark you would use the following syntax within the terminal window: 

`tshark -i wlan0 -w captureOutput.pcap`

To help breakdown the above syntax, it reads as `tshark [-i<capture interface> wlan0 <wifi card> -w <outfile>]`.

After writing to the captureOuput.pcap file you can read the file with the following syntax:

`tshark -r captureOutput.pcap`

TShark offers a plethora of options to help specify any search vectors. A few examples of some options would be as follows.

- `-a| --autostop <capture autostop condition>` which tells TShark when to stop writing to the capture file. 

- `-c <capture packet count>` which sets the maximum number of packets to read when capturing live data. 

- `-2 <two-pass analysis>` which causes TShark to buffer an output until the entire first pass is done. 

These are just a few of the options that TShark allows. If you have questions feel free to reference `tshark -h` or `tshark --help` within the terminal window.



### References
