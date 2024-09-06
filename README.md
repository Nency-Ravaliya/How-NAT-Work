# How-NAT-Work

# NAT - Network Address Translation

# Private IP and Public IP

## Private IP

- **Description**: Your laptop receives a private IP address from your router using DHCP (e.g., 192.168.1.50).
- **Usage**: Private IPs are used within your home network (LAN) and are not accessible directly from the internet.
- **Private IP Ranges**: Defined by RFC 1918, these ranges are:
  - `10.0.0.0` - `10.255.255.255`
  - `172.16.0.0` - `172.31.255.255`
  - `192.168.0.0` - `192.168.255.255`

## Public IP

- **Description**: The router has a public IP address assigned by your Internet Service Provider (ISP). This public IP is visible to the internet.
- **Usage**: Public IPs are used to route traffic across the internet.

## What is NAT (Network Address Translation)?

NAT is a process that occurs on your router, allowing multiple devices on your local network (each with its own private IP address) to share a single public IP address when accessing the internet.

### How NAT Works

1. **Device Request**: Your laptop (with a private IP, e.g., 192.168.1.50) sends a request to the internet (e.g., opening google.com).
2. **IP Translation**: The router modifies the request by:
   - Rewriting the source IP address from your private IP (192.168.1.50) to the router's public IP address (e.g., 203.0.113.15).
   - Assigning a unique port number to track the session.
3. **NAT Table**: The router maintains a NAT table to track which internal device made which request. For example:
   - Your laptop sends a request using 192.168.1.50:portX, and the router rewrites it to 203.0.113.15:portY.
   - When the response arrives at the router's public IP (203.0.113.15), the router looks up the NAT table and forwards the response to the correct internal device (your laptop).

### Why Do We Use NAT?

- **Conserve IP Addresses**: NAT allows multiple devices on a local network to share a single public IP, which is crucial due to the limited availability of public IPv4 addresses.
- **Security**: NAT hides the private IP addresses of local devices from the public internet, adding a layer of security.

## The Overall Process

1. **Private IP Assignment**: Your laptop receives a private IP (e.g., 192.168.1.50) via DHCP from the router.
2. **Request to Google**: The laptop sends a request to google.com.
3. **NAT Translation**: The router translates the private IP of the laptop to the public IP (e.g., 203.0.113.15) and forwards the request to Google’s server.
4. **Response Handling**: Google’s server sends a response to the router’s public IP.
5. **Forwarding Response**: The router checks its NAT table, identifies the original request from your laptop, and forwards the response to your laptop’s private IP (192.168.1.50).

## In Summary

- Your laptop has a private IP (e.g., 192.168.1.50) within your home network.
- The router has a public IP (e.g., 203.0.113.15), assigned by your ISP, to communicate with the internet.
- NAT translates your private IP to the public IP when accessing the internet, allowing multiple devices to share one public IP.
