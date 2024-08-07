


# rcmanifest.github.io: A Linux Centric Blog

This repo uses github pages. [How to use github pages](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site)

Thanks to [Jim Salter](https://arstechnica.com/author/jimsalter/) who wrote a [ guide to building a linux router from scratch](https://arstechnica.com/gadgets/2016/04/the-ars-guide-to-building-a-linux-router-from-scratch/)

Thanks to [Darius Juodokas](https://dev.to/netikras)  who wrote a [great article on how to understand iptables](https://dev.to/netikras/iptables-a-beast-worth-training-a-firewall-a-nat-router-a-port-forwarder-an-lb-anti-dos-a-logger-for-free-5157)
<br>
<br>  

# Creating a Router Using iptables

## Introduction to iptables

iptables is a command line utility to manage the netfilter framework in the linux kernel which handles networking packets.

The key concepts when using iptables are :
- Tables (a series of chains)
- Chains (a series of rules)
- Rules ( the iptables base or primitive type)
- target (the action that is taken on a matching packet)

### How the kernel filters packets
A rule specifies matching criteria for a packet and a target (ie. action to be taken).  If the packet match fails, the next rule in the chain is examined.  If the match succeeds the next rule is specified by the value of the target, which may be the name of a user-defined chain or one of ACCEPT, DROP, QUEUE, or RETURN.
- ACCEPT: let the packet through
- DROP: drop the packet
- QUEUE: pass the packet to userspace
- RETURN: resume processing at the next rule in the calling chain.

There are also a number of so-called target extensions:
- MASQUERADE: rewrites the source address of a packet to be that of the specfied interface.
- LOG: logs packets
- SNAT, DNAT, etc...

A rule specifies the actions to take on packets matching certain criteria.  Here is the general structure of an iptables rule:

`iptables [-t table] COMMAND CHAIN [match criteria] -j TARGET`
- -t table: specifies the table to use.  If omitted the default is the filter table.
- COMMAND: the action to perform eg. -A to append to a chain, -D to delete
- CHAIN: the chain to which the rule is applied eg. INPUT
### Example: router

