**Elastic IP (EIP)** is a **static public IPv4 address** provided by AWS that can be associated with an EC2 instance to ensure a 
**fixed public IP** even after instance stop/start.

#### Actions of Elastic IP:
- **Allocate** – Reserves a static public IP address from AWS.
- **Associate** – Attaches the Elastic IP to an EC2 instance or network interface.
- **Disassociate** – Detaches the Elastic IP from the instance.
- **Reassociate** – Moves the Elastic IP to another instance (used in failover).
- **Release** – Returns the Elastic IP back to AWS (to avoid charges).
