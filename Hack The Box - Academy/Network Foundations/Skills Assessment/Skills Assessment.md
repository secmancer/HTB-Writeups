- ### What IPv4 address is used when a host wants to send/receive network traffic to itself?
	- 127.0.0.1
- ### What is the the name of the Program listening on localhost:5901 of the Pwnbox?
	- Xtigervnc
- ### Which network interface allows us to interact with target machines in the HTB lab environment?
	- tun0
- ### What command-line tool is used to configure network interfaces and display their current status?
	- ifconfig
- ### What command-line tool is used to display network connections, routing information, and interface statistics?
	- netstat
- ### What is the FTP command used to retrieve a file? (Format: XXXX)
	- RETR
- ### Bypass the request filtering found on the target machine's HTTP service, and submit the flag found in the response. The flag will be in the format: HTB{...}
- Enter FTP on the target:
```
nc 10.129.233.197 21
```
- We can then use anonymous login to get into the machine
```
USER anonymous (ctrl+v) (enter) (enter)
PASS (ctrl+v) (enter) (enter)
PASV (ctrl+v) (enter) (enter)
```
- We then get the indication this is setup in passive mode, meaning that we need to connect to FTP onto another port to perform file transfering / other actions
```
227 Entering Passive Mode (10,129,233,197,194,11).  
Ncat: Connection reset by peer.
```
- So, we need to calculate the port number, which we can do by finding a small number p1 and p2 and then adding p2 with the product of p1 and 256.
- In this example, we are given 194 and 11, which gives us: 194 * 256 + 11 = 49675
- So, we can connect by using the below command:
```
nc -v 10.129.233.197 49675
```
- We can the connect and grab our target file
```
RETR Note-From-IT.txt[Ctrl+V][Enter][Enter]
```
- We can get the note, which says the following:
```
Bertolis, The website is still under construction. To stop users from poking their nose where it doesn't belong, I've configured IIS to only allow requests containing a specific user-agent header. If you'd like to test it out, please provide the following header to your HTTP request. User-Agent: Server Administrator The site should be finished within the next couple of weeks. I'll keep you posted. Cheers, jarednexgent
```
- From this note, we learn that that web traffic is getting filtered out if it doesn't have a user agent set to Server Administrator
- We can go ahead and connect to this web server
```
nc -v 10.129.233.197 80
```
- And enter this to grab whatever is there
```
GET / HTTP/1.1 (enter)
HOST: 10.129.233.197 (enter)
User-Agent: Server Administrator (enter) (enter)
```
- We then get an 200 reply back with the flag!
```
HTTP/1.1 200 OK  
Content-Type: text/html  
Last-Modified: Fri, 07 Feb 2025 20:46:15 GMT  
Accept-Ranges: bytes  
ETag: "5acd7854a179db1:0"  
Server: Microsoft-IIS/10.0  
Date: Tue, 16 Jun 2026 06:57:33 GMT  
Content-Length: 746  
  
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">  
<html xmlns="http://www.w3.org/1999/xhtml">  
<head>  
<meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" />  
<title>IIS Windows Server</title>  
<style type="text/css">  
<!--  
body {  
       color:#000000;  
       background-color:#0072C6;  
       margin:0;  
}  
  
#container {  
       margin-left:auto;  
       margin-right:auto;  
       text-align:center;  
       }  
  
a img {  
       border:none;  
}  
  
-->  
</style>  
</head>  
<body>  
<div id="container">  
<a href="http://go.microsoft.com/fwlink/?linkid=66138&amp;clcid=0x409"><img src="iisstart.png" alt="IIS" width="960  
" height="600" /></a>  
</div>  
</body>  
</html>  
<!-- HTB{S00n_2_B_N3tw0rk1ng_GURU!} -->
```
- Flag: HTB{S00n_2_B_N3tw0rk1ng_GURU!}