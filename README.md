This is a sample kubernetes objects for deployment and service

It pulls clamav-rest image to perform virus scanner

sample virus file - eicar.com.txt

Test that service detects common test virus signature:

$ curl -i -F "file=@eicar.com.txt" http://localhost:9000/scan
HTTP/1.1 100 Continue

HTTP/1.1 406 Not Acceptable
Content-Type: application/json; charset=utf-8
Date: Mon, 28 Aug 2017 20:22:34 GMT
Content-Length: 56

{ Status: "FOUND", Description: "Eicar-Test-Signature" }
Test that service returns 200 for clean file:

$ curl -i -F "file=@clamrest.go" http://localhost:9000/scan

HTTP/1.1 100 Continue

HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Date: Mon, 28 Aug 2017 20:23:16 GMT
Content-Length: 33

{ Status: "OK", Description: "" }
Status codes:

200 - clean file = no KNOWN infections
406 - INFECTED
400 - ClamAV returned general error for file
412 - unable to parse file
501 - unknown request
