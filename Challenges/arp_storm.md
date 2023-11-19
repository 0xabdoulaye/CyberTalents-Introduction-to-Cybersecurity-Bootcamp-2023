An attacker in the network is trying to poison the arp table of 11.0.0.100, the admin captured this PCAP.

https://hubchallenges.s3-eu-west-1.amazonaws.com/Forensics/ARP+Storm.pcap


## Solve 
I will fireUP wireshark. it seem to be a lot of arp containing hidden data.
 so now i will use tshark

```
└─# tshark -r ARP+Storm.pcap -Y "arp"  
Running as user "root" and group "root". This could be dangerous.
    1   0.000000 VMware_1e:1d:81 → Broadcast    ARP 42 Unknown ARP opcode 0x005a
    2   0.000442 VMware_1e:1d:81 → Broadcast    ARP 42 Unknown ARP opcode 0x006d
    3   0.000745 VMware_1e:1d:81 → Broadcast    ARP 42 Unknown ARP opcode 0x0078
    4   0.000994 VMware_1e:1d:81 → Broadcast    ARP 42 Unknown ARP opcode 0x0068
```
I think i need to fetch all opcode here.

```
└─# tshark -r ARP+Storm.pcap -Y "arp" | awk -F'opcode 0x' '{print $2}' | sed 's/.*\(........\)/\1/'

005a
006d
0078
0068
005a
0033
0074
006e
0063
006b
0042
0030
0064
0057
006c
0030
004d
0048
0056
007a
0058
007a
0042
0077
0059
0030
0039
006b
005a
0056
0038
0078
0063
0031
0039
0042
0062
0048
0064
0041
0065
0058
004e
0066
0051
0054
005a
0031
0055
0032
0056
006b
0058
0033
0051
0077
0058
0033
0041
0077
004d
0058
004d
0077
0062
006e
0030
003d

```
Then i used cyberchef fromHex and remove nullbyte
https://gchq.github.io/CyberChef/#recipe=From_Hex('Auto')Remove_null_bytes()&input=CjAwNWEKMDA2ZAowMDc4CjAwNjgKMDA1YQowMDMzCjAwNzQKMDA2ZQowMDYzCjAwNmIKMDA0MgowMDMwCjAwNjQKMDA1NwowMDZjCjAwMzAKMDA0ZAowMDQ4CjAwNTYKMDA3YQowMDU4CjAwN2EKMDA0MgowMDc3CjAwNTkKMDAzMAowMDM5CjAwNmIKMDA1YQowMDU2CjAwMzgKMDA3OAowMDYzCjAwMzEKMDAzOQowMDQyCjAwNjIKMDA0OAowMDY0CjAwNDEKMDA2NQowMDU4CjAwNGUKMDA2NgowMDUxCjAwNTQKMDA1YQowMDMxCjAwNTUKMDAzMgowMDU2CjAwNmIKMDA1OAowMDMzCjAwNTEKMDA3NwowMDU4CjAwMzMKMDA0MQowMDc3CjAwNGQKMDA1OAowMDRkCjAwNzcKMDA2MgowMDZlCjAwMzAKMDAzZAo

I get this base64.
```
ZmxhZ3tnckB0dWl0MHVzXzBwY09kZV8xc19BbHdAeXNfQTZ1U2VkX3QwX3AwMXMwbn0=
```
Decode it now
```
└─# base=ZmxhZ3tnckB0dWl0MHVzXzBwY09kZV8xc19BbHdAeXNfQTZ1U2VkX3QwX3AwMXMwbn0=
                                                                                                                                     
┌──(root㉿1337)-[/home/bloman/Learning/CyberTalents-Introduction-to-Cybersecurity-Bootcamp-2023/Files]
└─# echo $base | base64 -d
flag{gr@tuit0us_0pcOde_1s_Alw@ys_A6uSed_t0_p01s0n} 

```