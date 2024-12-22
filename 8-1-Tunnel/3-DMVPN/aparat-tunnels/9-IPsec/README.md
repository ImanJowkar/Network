# IPsec

### IPsec services
**ipsec provide 4 security serivces:**
- `data confidentiality (AES, DES, 3DES)`
- `data integrity (MD5, SHA)`
- `replay detection (sequence number)`
- `peer authentication (PSK, digital certificate)`


### IPsec mode: 
* AH(Authentication Header (AH) provides data integrity and authentication but does not offer data confidentiality)
* ESP(provide all 4 security services)



 
`Encapsulating Security Payload (ESP)` has two modes of operation:
* tunnel mode
* transport mode



### IKE (Internet Key Exchange)
* `IKE-version-1 (ISAKMP)`
* `IKE-version-2`


`IKEv1:` UDP port 500
`IKEv2:` UDP port 500 (and 4500 for NAT traversal)


# IKE Phase1 and Phase2
* Phase-1(ISAKMP): use for transfering control plane data. phase-1 tunnel is very secure

* Phase-2: use for transfering data plane


Here's a more concise summary of **IKE Phase 1** and **Phase 2**:

### **IKE Phase 1**: 
- **Purpose**: Securely authenticate and establish a trusted communication channel.
- **Steps**:
  1. Devices authenticate each other (using PSK or certificates).
  2. Agree on encryption algorithms.
  3. Exchange keys to create a secure channel.
- **Outcome**: A secure, encrypted connection (IKE SA) for further communication.

### **IKE Phase 2**: 
- **Purpose**: Set up the actual VPN tunnel for encrypted data transfer.
- **Steps**:
  1. Negotiate parameters for data encryption (like AES, SHA).
  2. Use keys from Phase 1 to encrypt/decrypt traffic.
- **Outcome**: A secure VPN tunnel is established for transferring encrypted data.

### In Short:
- **Phase 1**: Sets up secure communication.
- **Phase 2**: Creates the VPN tunnel for data encryption.

These phases ensure secure, authenticated, and encrypted communication between devices over a potentially untrusted network.