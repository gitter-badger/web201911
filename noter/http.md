<!-- { templatetype:'header', templateappversion:'1', defaultfolder:'C:\\git-undervisning\\mcronberg\\undervisning-http\\noter' } -->

# HTTP

- Hypertext Transfer Protocol
  - Request / Response kommunikations protokol

## Historik

Se [http://ithistorie.cronberg.dk](http://ithistorie.cronberg.dk/?maerker=http,html,css,det_vi_husker)

## Klient / Server

- Request / Reponse
  - Transaktion
  - Authentication

## Stuktur

- Header
  - Payload
- Body

### GET

- [Prøv det selv](http://webdemo.cronberg.dk)

```
GET http://fdemo2.cronberg.dk/SimplePage HTTP/1.1
Host: fdemo2.cronberg.dk
Connection: keep-alive
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Referer: http://fdemo2.cronberg.dk/
Accept-Encoding: gzip, deflate
Accept-Language: en,da;q=0.9,en-US;q=0.8
```

```
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 1498
Content-Type: text/html; charset=utf-8
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-AspNetWebPages-Version: 3.0
X-Powered-By: ASP.NET
Date: Tue, 02 Oct 2018 22:09:33 GMT

<!DOCTYPE html>
...
```

### POST

- [Prøv det selv](http://webdemo.cronberg.dk)

```
POST http://fdemo2.cronberg.dk/SimplePost_submit.cshtml HTTP/1.1
Host: fdemo2.cronberg.dk
Connection: keep-alive
Content-Length: 174
Cache-Control: max-age=0
Origin: http://fdemo2.cronberg.dk
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Referer: http://fdemo2.cronberg.dk/SimplePost
Accept-Encoding: gzip, deflate
Accept-Language: en,da;q=0.9,en-US;q=0.8

txtName_name=1234&txtSecretName_name=5678&lstCountry_name=DK&lstSpeak_name=SE&chkFeelYoung_name=on&optSex_name=Male&file1_name=&txtNotes_name=test&btnSubmit1_name=Submit+%231
```

```
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 1684
Content-Type: text/html; charset=utf-8
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-AspNetWebPages-Version: 3.0
X-Powered-By: ASP.NET
Date: Tue, 02 Oct 2018 22:11:34 GMT

<!DOCTYPE html>
...
```

## Metoder

- GET (Hent)
- POST (Opret)
- PUT (Opdater)
- DELETE (Slet)
- PATH (Samlede opdateringer)
- HEAD (Uden body)
- CONNECT (HTTPS)

## Status koder

- Informational 1XX
- Successful 2XX
  - 200 OK
- Redirection 3XX
  - 301/302
- Client Error 4XX
- Server Error 5X
  - 500 Server error

## Cookie

- [Prøv det selv](http://webdemo.cronberg.dk)

```
POST http://fdemo2.cronberg.dk/sendcookie.cshtml HTTP/1.1
Host: fdemo2.cronberg.dk
Connection: keep-alive
Content-Length: 20
Cache-Control: max-age=0
Origin: http://fdemo2.cronberg.dk
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Referer: http://fdemo2.cronberg.dk/sendcookie
Accept-Encoding: gzip, deflate
Accept-Language: en,da;q=0.9,en-US;q=0.8

btnSend=Send+cookies
```

```
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 1765
Content-Type: text/html; charset=utf-8
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-AspNetWebPages-Version: 3.0
Set-Cookie: MySessionCookie=My value; path=/
Set-Cookie: MyExpireCookie=My value; expires=Tue, 16-Oct-2018 22:13:16 GMT; path=/
X-Powered-By: ASP.NET
Date: Tue, 02 Oct 2018 22:13:16 GMT

<!DOCTYPE html>
...
```

## Kryptering

- HTTPS
  - SSL

## HTTP/2

- Er implementeret i de fleste browsere
- Features
  - Multiplexing
  - Server push
  - Binær
  - Prioritisering af afsendelse af ressourcer
  - Hastighed

Se eventuelt [HTTP2 test](http://http2.golang.org/gophertiles?latency=1000)

## Værktøjer

- Chrome's F12
- Fiddler
- CURL

