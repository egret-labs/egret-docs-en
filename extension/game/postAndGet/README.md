There are various request methods in the network transport protocol. In the HTTP / 1.1 protocol, eight methods (also called ""actions"") are defined to operate the specified resources in different ways.

Among the network operation provided by Egret, two ways are encapsulated.

1. POST: Submit data to the specified resource, request the server to process (such as submitting a form or uploading a file).The data is included in the request for this article.This request may create new resources or modify existing resources, or both.

2. GET: A "display" request is issued to the specified resource. The GET method should only be used in reading data, and should not be used in the operation that will produce "side effects".

All "actions" are encapsulated in the `URLRequestMethod` class. The default "action" is GET. If we modify the "action", you can set the `method` property in` URLRequest`

The specific code is as follows:
```
var urlreq:egret.URLRequest = new egret.URLRequest();

urlreq.method = egret.URLRequestMethod.POST;
```