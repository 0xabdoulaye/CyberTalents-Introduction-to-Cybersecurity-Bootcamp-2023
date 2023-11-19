Securing an important image requires good encryption. so we added extra security layer for your photo and now is unbreakable! 

https://hubchallenges.s3-eu-west-1.amazonaws.com/Forensics/cyber.zip
## solve
```
┌──(root㉿1337)-[/home/bloman/Learning/CyberTalents-Introduction-to-Cybersecurity-Bootcamp-2023/Files]
└─# steghide extract -sf cyber.jpg 
Enter passphrase: 
steghide: could not extract any data with that passphrase!
                                                           


```
Nothing seeems encrypted so i used stegseek to crack it
```
┌──(root㉿1337)-[/home/bloman/Learning/CyberTalents-Introduction-to-Cybersecurity-Bootcamp-2023/Files]
└─# time stegseek -sf cyber.jpg /usr/share/wordlists/rockyou.txt 
StegSeek 0.6 - https://github.com/RickdeJager/StegSeek

[i] Found passphrase: "1234"
[i] Original filename: "flag.txt".
[i] Extracting to "cyber.jpg.out".


real	0.17s
user	0.01s
sys	0.02s
cpu	11%

└─# cat cyber.jpg.out 
flag{cyb3rs3cXXXXXXXXX}

```