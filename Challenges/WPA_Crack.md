## Solution
first we have a pcap file.
```
└─# file wpa943050264305852656243865.cap 
wpa943050264305852656243865.cap: pcap capture file, microsecond ts (little-endian) - version 2.4 (802.11 with Prism header, capture length 65535)

```
**Cracking it using Hashcat**
First we will Transform it into a Crackable file
```
└─# hcxpcapngtool -o hashwifi.txt -E essidlist wpa943050264305852656243865.cap 
hcxpcapngtool 6.2.7 reading from wpa943050264305852656243865.cap...


┌──(root㉿1337)-[/home/bloman/Learning/CyberTalents-Introduction-to-Cybersecurity-Bootcamp-2023/Files]
└─# cat essidlist 
test
                                                                                                                                     
┌──(root㉿1337)-[/home/bloman/Learning/CyberTalents-Introduction-to-Cybersecurity-Bootcamp-2023/Files]
└─# cat hashwifi.txt 
WPA*02*cc303dcc8fb0b285257353480a52c563*000d93ebb08c*00095b91535d*74657374*54adc644966dc8423d44364a1de9ec22415522bd0555ee718f8a53b8d679470c*0103005ffe010900200000000000000001fe5f0c5b5423815f35fe606720bbb9466d8601a8b4493af4cf5a0317f38c83870000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000*05
```

**Cracked**
```
└─# hashcat -m 22000 hashwifi.txt -a 0 /usr/share/wordlists/rockyou.txt       
hashcat (v6.2.6) starting

OpenCL API (OpenCL 3.0 PoCL 3.0+debian  Linux, None+Asserts, RELOC, LLVM 13.0.1, SLEEF, DISTRO, POCL_DEBUG) - Platform #1 [The pocl project]
============================================================================================================================================
* Device #1: pthread-Intel(R) Core(TM) i5-3427U CPU @ 1.80GHz, 1389/2843 MB (512 MB allocatable), 4MCU

Minimum password length supported by kernel: 8
Maximum password length supported by kernel: 63

cc303dcc8fb0b285257353480a52c563:000d93ebb08c:00095b91535d:test:XXXXXX
                                                          
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 22000 (WPA-PBKDF2-PMKID+EAPOL)
Hash.Target......: hashwifi.txt
Time.Started.....: Sun Nov 19 17:55:10 2023 (29 secs)
Time.Estimated...: Sun Nov 19 17:55:39 2023 (0 secs)
Kernel.Feature...: Pure Kernel
Guess.Base.......: File (/usr/share/wordlists/rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:     2022 H/s (7.38ms) @ Accel:64 Loops:256 Thr:1 Vec:8
Recovered........: 1/1 (100.00%) Digests (total), 1/1 (100.00%) Digests (new)
Progress.........: 151377/14344385 (1.06%)
Rejected.........: 93777/151377 (61.95%)
Restore.Point....: 150811/14344385 (1.05%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidate.Engine.: Device Generator
Candidates.#1....: carpediem1 -> bangonthedoor
Hardware.Mon.#1..: Temp: 87c Util: 96%

Started: Sun Nov 19 17:55:01 2023
Stopped: Sun Nov 19 17:55:41 2023

```