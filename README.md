# Packet Sniffer in Python

This Python script is a simple packet sniffer that captures and analyzes network packets at the Ethernet, IPv4, and IPv6 levels. It is designed to capture raw network data using a raw socket connection and then print detailed information about the packets, such as TCP, UDP, ICMP, and ICMPv6 headers.

The script also includes packet filtering functionality to display only specific types of packets (ICMP, UDP, TCP, ICMPv6).

## Prerequisites

Before using the packet sniffer, ensure that you have the following prerequisites:

- Python 3.5 or higher
- Root (administrator) privileges on your machine, as raw sockets require elevated permissions.
  
## Libraries Used

- `socket`: To create raw sockets and capture packets.
- `struct`: To unpack raw packet data.
- `binascii`: For converting binary data into a readable format.
- `textwrap`: To format large data strings into smaller, readable blocks.

## How It Works

1. **Socket Creation**: The script creates a raw socket using `socket.socket()` to capture network packets.
2. **Packet Filtering**: The script supports filtering packets by protocol. The filtering can be done by passing the protocol (e.g., `ICMP`, `UDP`, `TCP`) as a command-line argument. By default, all packets are displayed.
3. **Ethernet Frame Parsing**: The raw data is parsed first as an Ethernet frame to extract the destination and source MAC addresses and the protocol (IPV4 or IPV6).
4. **IPv4 and IPv6 Header Parsing**: Based on the extracted protocol, the script extracts the relevant IPv4 or IPv6 headers. For IPv6, the script further extracts headers for different protocols such as TCP, UDP, and ICMPv6.
5. **Protocol-specific Parsing**: Depending on the IP protocol (ICMP, TCP, UDP), the script extracts the corresponding data and prints detailed information about the packet, including header details and additional data such as HTTP content for TCP packets.

### Supported Protocols:
- **ICMP**: Internet Control Message Protocol (IPv4)
- **ICMPv6**: Internet Control Message Protocol for IPv6
- **TCP**: Transmission Control Protocol
- **UDP**: User Datagram Protocol

## Usage

### Command Line

1. Clone or download the repository and navigate to the script's directory.
2. Run the script with elevated privileges (root/administrator).
   
   ```bash
   sudo python3 packet_sniffer.py
   ```

3. You can filter packets by specifying a protocol as an argument, e.g., `ICMP`, `UDP`, or `TCP`. Example:
   
   ```bash
   sudo python3 packet_sniffer.py ICMP
   ```

4. If no argument is passed, all protocols will be captured.

### Example Output:

For **ICMP**:
```bash
*******************ICMP***********************
	ICMP type: 8
	ICMP code: 0
	ICMP checksum: 0x3d3f
```

For **TCP**:
```bash
*******************TCP***********************
	Source Port: 80
	Destination Port: 12345
	Sequence Number: 12345678
	Ack. Number: 87654321
	Data Offset: 5
	Reserved: 0
	TCP Flags: 18
	Urgent Flag: Set
	Ack Flag: Set
	Window: 0x1e3a
	Checksum: 0x1a2b
	Urgent Pointer: 0x0
```

For **UDP**:
```bash
*******************UDP***********************
	Source Port: 1234
	Destination Port: 5678
	Length: 64
	Checksum: 0x0
```

For **IPv6**:
```bash
*******************IPv6***********************
	Source IP: 2001:db8::ff00:42:8329
	Destination IP: 2001:db8::ff00:42:8340
```

## Functions

- `main()`: Main function that listens for packets and filters them based on the user input.
- `printPacketsV4()`: Handles IPv4 packet analysis, including TCP, UDP, and ICMP.
- `printPacketsV6()`: Handles IPv6 packet analysis, including ICMPv6, TCP, and UDP.
- `tcpHeader()`, `udpHeader()`, `icmpv6Header()`: Functions to unpack and print the specific headers for TCP, UDP, and ICMPv6.
- `ethernet_frame()`: Unpacks the Ethernet frame and extracts MAC addresses and the protocol.
- `ipv4_Packet()`: Unpacks and prints IPv4 headers and protocol-specific data.
- `format_output_line()`: Formats the output for readability.

## Important Notes

- Running this script requires root (administrator) privileges because raw socket operations are used.
- This script captures and displays live network data. Use it responsibly and ensure that you have permission to monitor the network you are on.
- The script can run indefinitely until stopped. You can stop it by pressing `Ctrl+C`.

## **Contact**

For any inquiries or issues related to this project, please feel free to reach out via (beingamann27.com).
