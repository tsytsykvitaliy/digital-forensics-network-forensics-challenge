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




## Basic Packet Analysis in Wireshark

### The Tip of The Iceberg

Packets (also referred to as frames) contain a large amount of information, so it's always best to start with what we can see easily. Let's take a look at the _Packet Listing_ window and gather the information from there first. We are going to use `Basics.pcap` in this section.

![](DNS_listing.png)

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
_Specific protocol that the packet used_
- **Length**: 86  
_Number of bytes in this packet_
- **Info**: Standard query 0x332e A www.offensive-security.com  
_Summary of the information in the highest layer protocol_

This is the easiest way to see the most common information about the packets. However, there is much more that can be uncovered.

### Digging Deeper

Glancing at the _Packet Listing_ is always nice, but it's rarely enough. If we want to learn more about the packet, we should click on it and explore the _Packet Details_. We have already discussed what information goes in each one of the layers (drop down rows) in the previous section so it will be easier to analyze our specific DNS packet, knowing that information. We will start from the top of the list with the physical layer, and work our way to the bottom - the "highest" protocol.

![](physical.png)

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
