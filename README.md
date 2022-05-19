https://www.owasp.org/

# some kind of additional checklist
* https
* be aware of ```cross-site scripting (XSS) attacks```
* protect yourself from ```cross-side forgery (CSRF) attacks```
* calling web API from other domains using ```CORS```

* detect and avoid open redirect attacks
* avoid Sql injection attacks
hopefully, if you are using EF Core (or almost any other ORM) in a standart way, you
should be safe; EF Core has built-in protections agains SQL injection, so as long as you
are not doing something stupid, you are fine



# https
to protect your users, your app should encrypt the traffic between the user's browser
and your app as it travels over the network by using the HTTPS protocol  
it is similar to HTTP but you are now using SSL/TLS certificate to encrypt requests and responses  
more on sertificates read https://livebook.manning.com/book/real-world-cryptography/chapter-9/32  
SSL is an older standart, and ```TLS is a way to go now```  
https://letsencrypt.org/docs/  
```in cloud```, most providers will provide one click TLS certificates so that ```you don't have to manage```
```sertificates yourself```  
also, you can often get away without ```directly``` supporting HTTPS in your app by taking advantage of the reverse-proxy
architecture, in a process calling ```TLS offloading/termination```; so instead of your application handling HTTPS requests
directly, it continues to use HTTP. Now, the reverse-proxy is responsible for encryption/decryption of HTTPS traffic

when, do you need to handle SSL/TLS directly in your app:
* if you are expsing Kestrel to the internet directly, without a reverse proxy
* if having HTTP between your app and reverse proxy is not acceptable
* if you are using technologies that requires HTTPS (gRPC, HTTP/2)


## using development certificates
the first time you hit ```dotnet``` command using dotnet SDK, the SDK installs HTTPS dev certificate onto your machine  
```cli
dotnet dev-certs https --trust
```

# CORS
```origins``` is same if they match the scheme (HTTP or HTTPS), domain (example.com), and port (80/443)  
the browser will block the request, if you are trying to access another origin  
```CORS``` is a web standard that allows your Web API to make statements about who can make cross-origin requests
to it; for instance you can make such statements for your API:
* allow cross-origin requests from 'https://shopping.com' and 'https://app.shopping.com'
* only allow GET cross-origin requests
etc, you can combine this rules into ```policy```  
http://mng.bz/aD41  
