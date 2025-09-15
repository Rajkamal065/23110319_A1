# Task 1 – Custom DNS Resolver (Client-Server using UDP)

## Assignment Context
This is **Task 1** of the networking assignment. The goal is to implement a simple client-server system using Python’s socket module and scapy. The client reads DNS query packets from a .pcap file, builds a custom header, and sends the request to the server via UDP. The server resolves the request by selecting an IP address from a predefined pool based on the time of day and session identifier.

This task demonstrates practical knowledge of network packet parsing, socket communication, and routing logic.

---

## Objective
- Parse DNS queries from a .pcap file  
- Build custom headers for requests  
- Implement UDP-based client-server communication  
- Route requests based on time and session ID  
- Generate a report of resolved DNS queries  

---

## Files Included
- server.py – Server script that resolves IP addresses based on incoming requests  
- client.py – Client script that reads DNS requests from a .pcap file and sends them to the server  
- README.md – Documentation for this task  
- sample.pcap – Example pcap file (optional, for testing)  

---

## Setup Instructions

1. Clone the repository  
   git clone https://github.com/yourusername/assignment-networking.git  
   cd assignment-networking  

2. Install dependencies  
   Make sure you have Python 3 installed. Install required Python packages using pip:  
   pip install scapy  
   No other external dependencies are required.  

---

## How to Run

1. Run the server  
   python server.py  
   The server will listen on 0.0.0.0:9999 and wait for incoming DNS requests.  

2. Run the client  
   python client.py "path/to/your/file.pcap"  

   Example:  
   python client.py "c:/Users/yourname/Desktop/sample.pcap"  

   The client will read the .pcap, build custom headers, and send requests to the server.  

---

## How It Works

### Server
- Listens for incoming UDP requests  
- Parses the custom header to extract hour and session ID  
- Routes requests based on predefined rules for morning, afternoon, and night  
- Responds with an IP from the IP pool  

### Client
- Reads DNS packets from a .pcap file using Scapy  
- Builds a custom header using timestamp and session counter  
- Sends requests to the server over UDP  
- Receives and logs the resolved IPs  

---

## IP Pool and Routing Rules
The server distributes IP addresses based on the time of the request:  

ROUTING_RULES = {  
    "morning": {"hash_mod": 5, "ip_pool_start": 0},  
    "afternoon": {"hash_mod": 5, "ip_pool_start": 5},  
    "night": {"hash_mod": 5, "ip_pool_start": 10},  
}  

This ensures structured routing based on time.  

---

## Dependencies
- Python 3.x – Programming language  
- Scapy – For reading .pcap files and analyzing DNS packets  

Install with:  
pip install scapy  

No additional libraries are required.
