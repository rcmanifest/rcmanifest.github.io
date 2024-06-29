


# rcmanifest.github.io: A Linux Centric Blog

This repo uses github pages. [How to use github pages](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site)
<br>
<br>  
# Creating a Router Using iptables

## Introduction to iptables

iptables is a command line utility to manage the netfilter framework in the linux kernel which handles tcp/ip traffic in the kernel.

The key concepts when using iptables are :
- Tables (a series of chains)
- Chains (a series of rules)
- Rules ( the iptables base or primitive type)
- target (the action that is taken on a matching packet)

### How the kernel filters packets
A rule specifies matching criteria for a packet and a target (ie. action to be taken).  If the packet match fails, the next rules in the chain is examined.  If the match succeeds the next rule is specified by the value of the target, which may be the name of a user-defined chain or one of ACCEPT, DROP, QUEUE, or RETURN.
- ACCEPT: let the packet through
- DROP: drop the packet
- QUEUE: pass the packet to userspace
- RETURN: resume processing at the next rule in the calling chain.

A rule specifies the actions to take on packets matching certain criteria.  Here is the general structure of an iptables rule:

`iptables [-t table] COMMAND CHAIN [match criteria] -j TARGET`
- -t table: specifies the table to use.  If omitted the default is the filter table.
- COMMAND: the action to perform eg. -A to append to a chain, -D to delete
- CHAIN: the chain to which the rule is applied eg. INPUT
