```
0 balance-rr
1 active-backup  (Active/Standby)
2 balance-xor    (Balance XOR)
3 broadcast
4 802.3ad        (IEEE 802.3ad Dynamic Link Aggregation)
5 balance-tlb
6 balance-alb    (Adaptive Load Balancing)
```
```
Round-robin policy:
  Transmit packets in sequential order from the first available slave through the last.
This mode provides load balancing and fault tolerance.
```
```
Active-backup policy:
  Only one slave in the bond is active.
  A different slave becomes active if, and only if, the active slave fails.
  The bond's MAC address is externally visible on only one port (network adapter) to avoid confusing the switch.
This mode provides fault tolerance.
  The primary option affects the behavior of this mode.
```
```
XOR policy:
  Transmit based on selectable hashing algorithm.
  The default policy is a simple source+destination MAC address algorithm.
  Alternate transmit policies may be selected via the xmit_hash_policy option, described below.
This mode provides load balancing and fault tolerance.
```
```
Broadcast policy:
  transmits everything on all slave interfaces.
This mode provides fault tolerance.
```
``` 
IEEE 802.3ad Dynamic link aggregation.
  Creates aggregation groups that share the same speed and duplex settings.
  Utilizes all slaves in the active aggregator according to the 802.3ad specification.

Prerequisites:
  Ethtool support in the base drivers for retrieving the speed and duplex of each slave.
  A switch that supports IEEE 802.3ad Dynamic link aggregation. Most switches will require some type of configuration to enable 802.3ad mode.
```
```
Adaptive transmit load balancing:
  channel bonding that does not require any special switch support.
  The outgoing traffic is distributed according to the current load (computed relative to the speed) on each slave.
  Incoming traffic is received by the current slave. If the receiving slave fails, another slave takes over the MAC address of the failed receiving slave.

Prerequisites:
  Ethtool support in the base drivers for retrieving the speed of each slave. 
```
```
Adaptive load balancing:
  includes balance-tlb plus receive load balancing (rlb) for IPV4 traffic, and does not require any special switch support.
  The receive load balancing is achieved by ARP negotiation.
  The bonding driver intercepts the ARP Replies sent by the local system on their way out and overwrites the source hardware address with the unique hardware address of one of the slaves in the bond such that different peers use different hardware addresses for the server.
```
