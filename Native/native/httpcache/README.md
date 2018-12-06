* The following applies only to resources downloaded during the application run; Assets, resources under the preloaded directory will not be updated by runtime.
* Index.html is not cached and is read from the server each time.
* Resources that do not want to be cached can be requested by adding random values

Such as:

```
var xhr = new XMLHttpRequest();
xhr.open('GET', './manifest.json?v=' + Math.random(), true);
```

* The runtime support server caching strategies, such as`Cache-Control:max-age=age`，
The runtime download resources only beyond the `max-age`set expiration time, update request will be sent to the server resources.In addition, after expiration, the runtime will not re-download the resource if the resource on the server has not changed.The download will only be redownloaded if the resource changes.


## 一、 Supported HTTP Cache Fields
### 1.1 Cache-Control field and value list

```
Cache-Control:no-cache
Cache-Control:no-store
Cache-Control:max-age=age

```
For other values, the runtime calculates whether the cache is valid using information such as the Date field, Expires field, and last-modified field below.

Among them,

```
Cache-Control:no-cache
```
Means disable caching;

```
Cache-Control:no-store
```
Means no information is stored;

```
Cache-Control:max-age=age
```
Represents that the cache is valid within the age period, and the age value is a number in seconds.

### 1.2 Pragma Fields and Value Lists

```
Pragma:no-cache
```
Indicates that caching is disabled, and HTTP1.0 has a lower standard priority than HTTP1.0
```
Cache-Control:no-cache
```
### 1.3 Date Field and Value List

```
Date:HTTP-date
```
Indicates that the response is generated at the time represented by the http-date. Such as:

```
Date: Tue, 15 Nov 1994 08:12:31 GMT
```
Indicates that the response was generated at Tue, 15 Nov 08:12:31 GMT.

### 1.4 Expires Field and Value List

```
Expires:HTTP-date
```
Indicates that the cache expires after the time represented by http-date. Such as:

```
Expires: Thu, 01 Dec 1994 16:00:00 GMT
```
Indicates that the cache expires after Thu, 01 Dec 1994 16:00:00 GMT.

If it doesn't exist.

```
Cache-Control:max-age=age
```
and

```
Expires:HTTP-date
```
The runtime USES information such as the Date field and last-modified field to calculate whether the cache is valid.

### 1.5  The Last-Modified Field and its Value List

```
Last-Modified:HTTP-date
```
Represents the last modification time of a resource on the server. Such as:

```
Last-Modified: Tue, 15 Nov 1994 12:45:26 GMT
```
Indicates that the last modification time of the resource on the server was Tue, 15 Nov 12:45:26 GMT.

### 1.6 ETag Field and Value List
```
ETag:entity-tag
```
Entity-tag represents the unique identifier of a resource on the server, and entity-tag is a value that the server can understand.

## 二、Directions for Use

In order to make reasonable use of resources and reduce unnecessary traffic consumption, the server side should properly configure the response header field, so that the runtime and browser can use the cache resources more efficiently.

### 2.1  Sets the Expiration Date of the Cache

Use

```
Cache-Control:max-age=age
```
and

```
Expires:HTTP-date
```
都可以设置缓存的有效期，但是，一个是HTTP 1.1标准，一个是HTTP 1.0标准，并且，如果两个同时出现，那么，前者的优先级高于后者。推荐使用前者或者两者同时配置。如果不配置，那么，runtime和浏览器就会自己计算有效期，这样的话，不利于实现服务器和客户端的紧密配合。因此，推荐设置缓存的有效期。

You can set the expiration of the cache, but one is the HTTP 1.1 standard, one is the HTTP 1.0 standard,and if you have both,The former, then, takes precedence over the latter. The former or both are ecommended.If not configured, the runtime and the browser calculate the expiration date themselves.This is not conducive to close cooperation between the server and the client.Therefore, it is recommended to set the expiration date of the cache.

### 2.2 Set last-Modified and ETag

When the cache fails, the runtime and the browser add these two values to the request header, enabling the server to efficiently determine whether the resource is expired and decide whether to return 304 or 200. 

Last-modified and ETag are recommended. If both occur, the server takes precedence over ETag processing.
