# Why this project? 
[![Licence](https://img.shields.io/github/license/ryungmin/protocol-go)](LICENSE)
[![Latest Release](https://img.shields.io/github/v/release/ryungmin/protocol-go)](https://github.com/perimeterx/go-project-structure/releases)
[![Issues](https://img.shields.io/github/issues/ryungmin/protocol-go?logo=github)](https://github.com/perimeterx/go-project-structure/issues)

Protocol is a command-line tool to display ASCII RFC-like protocol header diagrams for both existing network protocols or user-defined ones (using a very simple syntax). Protocol is written in Python and it's open-source software, licensed under the GPLv3 license. 
 
This project re-implements protocol in go-lang. Compiled protocol is very suitable for environments where python is not installed. 
 
## Original Protocol (is written in Python) 
 
[Luis MartinGarcia's Protocol](https://www.luismg.com/protocol/) 
 
github: [A Simple ASCII Header Generator for Network Protocols](https://github.com/luismartingarcia/protocol) 

# Install the protocol-go

```
$ go install github.com/ryungmin/protocol-go/cmd/protocol@latest
```

# Building the protocol-go 

## Building with Makefile

``` 
$ make  
```

## Building with Taskfile

```
$ task
```

## linux 
``` 
$ GOOS=linux go build -o protocol ./cmd/protocol/. 
``` 
 
## windows 
``` 
> SET GOOS=windows & SET GOARCH=amd64 & go.exe build -o protocol.exe .\cmd\protocol\.  
``` 
 
## macos 
``` 
# build for Intel MAC(x64) 
$ GOOS=darwin GOARCH=amd64 go build -o protocol_amd64 ./cmd/protocol/. 
 
# build for Apple Silicon(arm64) 
$ GOOS=darwin GOARCH=arm64 go build -o protocol_arm64 ./cmd/protocol/. 
 
# Create an universal file 
$ lipo -create -output protocol protocol_amd64 protocol_arm64 
``` 
 
# How to use 
[Luis MartinGarcia's Examples](https://www.luismg.com/protocol/#05) 
 
## Usage

``` 
$ protocol "Source:16,TTL:8,Reserved:40" 
 0                   1                   2                   3  
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|            Source             |      TTL      |               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+               +
|                           Reserved                            |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

* Source (16 bits)
* TTL (8 bits)
* Reserved (40 bits)
total 64 bits
``` 
 
``` 
$ protocol "Source:16,Reserved:40,TTL:8" 
 0                   1                   2                   3  
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|            Source             |                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+               +-+-+-+-+-+-+-+-+
|                   Reserved                    |      TTL      |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

* Source (16 bits)
* Reserved (40 bits)
* TTL (8 bits)
total 64 bits
``` 
 
``` 
$ protocol "Reserved:32,Target Address:128" 
 0                   1                   2                   3  
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                           Reserved                            |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                                                               |
+                                                               +
|                                                               |
+                        Target Address                         +
|                                                               |
+                                                               +
|                                                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

* Reserved (32 bits)
* Target Address (128 bits)
total 160 bits
``` 

```
$ protocol --list
Usage: protocol.exe "<protocol>"

+----------------------------------------------------------------------------------------+
| Protocol                                                          | <protocol>         |
+----------------------------------------------------------------------------------------+
| COTP for Connect Confirm                                          | cotp_cc            |
| COTP for Data                                                     | cotp_dt            |
| COTP for Disconnect Request                                       | cotp_dr            |
| Connection-oriented Transport Protocol (COTP) for Connect Request | cotp_cr            |
| Distributed Network Protocol 3.0 (DNP3)                           | dnp3               |
| Dynamic Host Configuration Protocol                               | dhcp               |
| Ethernet                                                          | ethernet           |
| Example                                                           | example            |
| ICMP Destination Unreachable                                      | icmp-destination   |
| ICMP Echo Request/Reply                                           | icmp-echo          |
| ICMP Information Request/Reply                                    | icmp-information   |
| ICMP Parameter Problem                                            | icmp-parameter     |
| ICMP Redirect                                                     | icmp-redirect      |
| ICMP Source Quench                                                | icmp-source        |
| ICMP Time Exceeded                                                | icmp-time          |
| ICMP Timestamp Request/Reply                                      | icmp-timestamp     |
| ICMP for IPv6 (ICMPv6)                                            | icmpv6             |
| ICMPv6 Destination Unreachable                                    | icmpv6-destination |
| ICMPv6 Echo Request/Reply                                         | icmpv6-echo        |
| ICMPv6 Neighbor Advertisement                                     | icmpv6-nadv        |
| ICMPv6 Neighbor Solicitation                                      | icmpv6-nsol        |
| ICMPv6 Packet Too Big                                             | icmpv6-big         |
| ICMPv6 Parameter Problem                                          | icmpv6-parameter   |
| ICMPv6 Redirect                                                   | icmpv6-redirect    |
| ICMPv6 Router Advertisement                                       | icmpv6-radv        |
| ICMPv6 Router Solicitation                                        | icmpv6-rsol        |
| ICMPv6 Time Exceeded                                              | icmpv6-time        |
| IEEE 802.1q                                                       | dot1q              |
| IEEE 802.1q                                                       | 8021q              |
| Internet Control Message Protocol (ICMP)                          | icmp               |
| Internet Protocol (IP), version 4.                                | ipv4               |
| Internet Protocol (IP), version 4.                                | ip                 |
| Internet Protocol (IP), version 6.                                | ipv6               |
| Modbus TCP                                                        | modbus_tcp         |
| PROFINET Real Time (RT)                                           | profinet_rt        |
| S7 Communication (S7Comm) Header                                  | s7_header          |
| S7Comm Data                                                       | s7_data            |
| S7Comm Item                                                       | s7_item            |
| Test                                                              | test               |
| Texas Simplified Application Project (TSAP)                       | tsap               |
| Transmission Control Protocol (TCP)                               | tcp                |
| User Datagram Protocol (TCP)                                      | udp                |
+----------------------------------------------------------------------------------------+
```
 
```
$ protocol tcp
 0                   1                   2                   3  
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|          Source Port          |       Destination Port        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                        Sequence Number                        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                     Acknowledgment Number                     |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|Offset | Res.  |     Flags     |            Window             |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|           Checksum            |        Urgent Pointer         |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Options                    |    Padding    |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

* Source Port (16 bits)
* Destination Port (16 bits)
* Sequence Number (32 bits)
* Acknowledgment Number (32 bits)
* Offset (4 bits)
* Res. (4 bits)
* Flags (8 bits)
* Window (16 bits)
* Checksum (16 bits)
* Urgent Pointer (16 bits)
* Options (24 bits)
* Padding (8 bits)
total 192 bits
```
