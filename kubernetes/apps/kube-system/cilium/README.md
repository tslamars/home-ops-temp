# Cilium

## UniFi BGP

```sh
router bgp 64513
  bgp router-id 10.69.1.1
  no bgp ebgp-requires-policy

  neighbor k8s peer-group
  neighbor k8s remote-as 64514
  neighbor k8s activate
  neighbor k8s capability extended-nexthop
  neighbor k8s soft-reconfiguration inbound

  neighbor 10.10.5.170 peer-group k8s
  neighbor 10.10.5.171 peer-group k8s
  neighbor 10.10.5.172 peer-group k8s

  address-family ipv4 unicast
    neighbor k8s next-hop-self
  exit-address-family
```
