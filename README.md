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

### Overview:
Network Forensics is a crucial part of digital forensics and its importance continues to grow everyday.
Almost all personal computers and servers are going to have builtin networking capabilities such as wifi or ethernet allowing to commuticate with other devices or the internet.                                                                                                              
These connections can be used to transfer illegal files, deny normal service, and allow malware to go become viral.                                                                                                                                                           
Network data can also be difficult to track due to the large volume and voliticity of the conversations.                                                                                                                                                                      
Usually networking data has to be deliberatly listened to and saved for analysis in order to extract evidence.                                                                                                                                                                
In our overview of network forensics, we will first cover the most common language that computers communicate with, the TCP/IP packet structure.                                                                                                                              
After we learn how to read these, we will dive into how to aquire and analyse network information with one of the most common tools in the field: Wireshark!                                                                                                                  
Once we have the basics down, we'll take a look at some more advanced topics dealing with Wireshark and tshark.



### TCP/IP packet structure and An Overview/Introduction to Wireshark




### Basic Packet Analysis in Wireshark



### Advanced Packet Analysis in Wireshark



### An Overview/Introduction to TShark



### References
