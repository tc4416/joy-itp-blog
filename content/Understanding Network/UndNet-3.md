---
title: "UndNet: Week3, Packet Analysis"
draft: false
---
#### Packet Analysis
- Both Wireshark and tcpdump command are used for analyzing packet. Wireshark has GUI.
- For this assignment, I am using my Digital Ocean server
- Checking interface:
<div align = "center">
<img src = "/media/und/packet-1.png" width = "400px">
</div>
- Understanding output:
	- I think [this tutorial](https://linuxhint.com/tcpdump-command-tutorial/ ) is the most digestible one for me haha.<div align = "center">
<img src = "/media/und/packet-2.png"width = "400px">
</div>

	- Filter by host ip: `$ sudo tcpdump -i any -c4 host 10.0.2.15`
	- Filter by port number: `$ sudo tcpdump -i any -c3 -nn port 443`
	- Filter by protocol: `$ sudo tcpdump -i any -c6 udp`
	- Combining examole: `$sudo tcpdump -i any -c6 -nn host 10.0.2.15 and port 443` and/or
	- Storing data: `sudo tcpdump -i any -c5 -w packetDate.pcap` or `$ sudo tcpdump -i eth0  -w classdump.pcap`
	- Reading Data: `tcpdump -r packetData.pcap`
	- Download to local machine:  `$ scp tigoe@tigoe.net:/home/tigoe/classdump.pcap`

- I had the data collection ran for about 5 mins.
	- `sudo tcpdump -i eth0 -w packetAnalysis_all.pcap`
	-  local: `scp joychang@142.93.249.203:/home/joychang/packetAnalysis_all.pcap ~/Desktop`
	- Open with wireShark <div align = "center"><img src = "/media/und/packet-3.png" width = "400px"></div>
	- It captured 508 packet
- Protocols
	- HTTP: 7 (~1.38%) <div align = "center"><img src = "/media/und/packet-4.png" width = "400px"></div>
	- SSH: 202(39.8%)  and 47 of them are SSHv2
	- TCP: 268(52.8%) 
	- TLSv1.2: 16(3.1%)
	- UDP, L2TP, SIP, SNMP: 1 (0.2%)
	- ARPL: 4(0.8%)
	- ICMPv6: 6(1.2%)
- How much is from remote hosts attempting  to access ports or services you don’t have open?  
	- 75(14.8%)of them has SYN flag and no ACK flag and with destination as the ipAddress of my droplet
	- [display filter tutorial]https://wiki.wireshark.org/DisplayFilters)
	- I used `tcp.flags.syn==1 && tcp.flags.ack==0 && ip.dst==142.93.249.203`
- How many other unique clients have tried to contact you? What are their relative levels of activities?
	- Not sure how to answer this
#### Lecture
##### wireshark
**tcp**
`ssh joychang@ipaddress`
`sudo tcpdump host ip`
`tcpdump -D` network interface
`tcpdump -I`
`sudo tcpdump -i eth0 >> classdump.pcap` send to file
