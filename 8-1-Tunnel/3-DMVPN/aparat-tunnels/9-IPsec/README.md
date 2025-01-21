# IPsec

### IPsec services
**ipsec provide 4 security serivces:**
- `data confidentiality (AES, DES, 3DES)`
- `data integrity (MD5, SHA)`
- `replay detection (sequence number)`
- `peer authentication (PSK, digital certificate)`


#### IPsec uses two different packet headers to deliver the security services: 
* AH(Authentication Header (AH) provides data integrity and authentication but does not offer data confidentiality)
* ESP(provide all 4 security services)



 
`IPsec has two modes of operation:`
* tunnel mode
* transport mode



### IKE (Internet Key Exchange)
* `IKE-version-1 (ISAKMP)`
* `IKE-version-2`


`IKEv1:` UDP port 500
`IKEv2:` UDP port 500 (and 4500 for NAT traversal)


# IKE Phase1 and Phase2 
####  Phase-1: use for transfering control plane data. phase-1 tunnel is very secure
1) authenticate peers.
2) exchange and negotigate keys and parameters.


#### Phase-2: use for transfering data plane (user traffik)

