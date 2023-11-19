This Challenge will help you understand essential commands in Linux OS
Each point is linked to another point, connect the link and win the Flag!

## solve

when i unziped the first file using `7z x `
i got a lot of file and i unziped them using the same method
I found a exec.zip hashed file.
Now Crack it
```
└─# zip2john exec.zip > hash.txt
ver 2.0 exec.zip/exec/ is not encrypted, or stored with non-handled compression type
```
a lot of zipped file on them
```
-rw-r--r-- 1 root root   11 Feb 21  2021 .pass.txt
└─# 7z x exec.zip 


```
Decode using that password now.
```
└─# ls    
-  ascii.zip
                

```
I have these 2 files.
```
└─# ./-    
998877665544332211

```
another password
```
└─# 7z x ascii.zip 
# cd ascii
└─# file *  
f0:         data
f1:         data
f2:         data
f3:         data
f4:         data
f5:         data
f6:         ASCII text
f7:         data
f8:         data
size37.zip: Zip archive data, at least v2.0 to extract, compression method=store
```
cat the ascii text
```
└─# cat f6                                 
rryuiytqpyuiqyofdkhsjhfewojnhfdss

7z x size37.zip
```
```
cd size37
└─# file *
next.zip: Zip archive data, at least v2.0 to extract, compression method=store
test1:    ASCII text
test2:    ASCII text
test3:    ASCII text
test4:    ASCII text
test5:    ASCII text
test6:    ASCII text
test7:    ASCII text
                        
cat *
sdjieocnuecio203023n23892098r23nu
87348tj98457mc095m03ym057-3v
4798234c98nc92m87t4c29872m9
62094n902m2x-28mx4t9xy282y49ty9824yt
5984nv998vtnc98tx-28957y98x 
847n889t282m4y89txy58tx984379nv3498yvn934

```
Tested these all
```
└─# 7z x next.zip
                           
Enter password (will not be echoed):
Everything is Ok           

Folders: 1
Files: 2
Size:       9931
Compressed: 2404


```
Found dictionary
```
└─# wc -l nexttocybertalents 
1051 nexttocybertalents
                          
└─# 7z x NumberOne.zip -p$(cat nexttocybertalents| grep -i "cybertalents" | cut -c 13-23)

```

```
7z x decodeme1.zip -p$(zip2john decodeme1.zip > hash; john -w=One hash | tail -n 4 | cut -d " " -f 1 | tail -n 1)
Scanning the drive for archives:
1 file, 754 bytes (1 KiB)

Extracting archive: decodeme1.zip
--
Path = decodeme1.zip
Type = zip
Physical Size = 754

Everything is Ok

Folders: 1
Files: 2
Size:       388
Compressed: 754
```

```
└─# ls
decodeme2.zip  pass
                                                                                                                                     
┌──(root㉿1337)-[/home/…/size37/next/NumberOne/decodeme1]
└─# cat pass 
dXNlbWVhc3Bhc3N3b3Jk
                     
└─# base=dXNlbWVhc3Bhc3N3b3Jk                              
                                                                                                                                     
┌──(root㉿1337)-[/home/…/size37/next/NumberOne/decodeme1]
└─# echo $base | base64 -d
usemeaspassword    

└─# cat decodeme2/flag.txt
synt{f1zcyr_yvahk_101}

┌──(root㉿1337)-[/home/…/size37/next/NumberOne/decodeme1]
└─# rot="synt{f1zcyr_yvahk_101}"
                                                                                                                                     
┌──(root㉿1337)-[/home/…/size37/next/NumberOne/decodeme1]
└─# echo $rot | rot13     
flag{s1mple_linux_101}
                        
```