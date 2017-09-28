Egret encapsulates the XMLHttpRequest` for asynchronous data interaction.

## 1.HTTP request

Through the HTTP protocol, requesting information and services from HTTP client (such as web browser) to the HTTP server can be achieved.The current HTTP 1.1 protocol is a stateless protocol, namely, HTTP client and HTTP server can not maintain a lasting link. With the request/response mode, if the client sends information to the server, the server will close the link after making response, so as to form a set of requests and responses.

### 1.1. The basic process

HTTP communication mechanism must go through the following steps:

1. Establish a TCP connection.
2. The Web browser sends a request command to the Web server.
3. The Web browser sends the request header information
4. Web server response
5. The Web server sends the response header information
6. The Web server sends data to the browser
7. The Web server shuts down the TCP connection (if the request header is set to `Connection: keep-alive`, the connection state will keep open).

### 1.2. HTTP request method 

#### GET method

The GET method is the default method for HTTP requests, and the data is sent via  simple code and sent to the server as part of the URL.Due to the browser's restrictions on the length of the URL, the length of the data submitted is also limited.

#### POST method

The POST method overcomes some of the drawbacks of the GET method, which can send large amounts of data, and the data is no longer sent in plaintext.For the sake of safety, the POST method is generally chosen. The data submitted by POST can also be obtained from the standard input and output streams.

## 2. Request for sending data

Testing the request for sending data requires a stable server.You can test the request for sending data by using `http://httpbin.org/get` and `http://httpbin.org/post`, the two stable server addresses provided by [httpbin.org](http://httpbin.org/).Among them, [get] (http://httpbin.org/get) will return the data requested by GET, while [post] (http://httpbin.org/post) will return the data requested by POST.

Egret uses the `HttpRequest` class to send an HTTP request.The method that can be used for specifying the request is GET or POST.The server-side response can be detected by monitoring the loaded events.The process of using `HttpRequest` to send the request are as follows:

1. Instantiate a `HttpRequest` object.
2. Set its response type `responseType`.
3. Request an object by initializing the `open` method. Initialize the request address and request type.
4. Set the request header information with `setRequestHeader`.If the request that POST shall be accompanied with parameters is a very important step, you need to inform the server of the requested parameter format, and this step needs to be executed after `open`.
5. Send the request via the `send` method. If it is the` post` method, parameters can be introduced.
6. Add monitoring and monitoring of the server response, which includes progress events, request success and failure events.


The code is as follows:

```
var request = new egret.HttpRequest();
request.responseType = egret.HttpResponseType.TEXT;
request.open("http://httpbin.org/get",egret.HttpMethod.GET);
request.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
request.send();
request.addEventListener(egret.Event.COMPLETE,this.onGetComplete,this);
request.addEventListener(egret.IOErrorEvent.IO_ERROR,this.onGetIOError,this);
request.addEventListener(egret.ProgressEvent.PROGRESS,this.onGetProgress,this);
```

In the above, a GET request was sent to the http: // httpbin.org / get`, and then a callback event is added. Data will be obtained when the request succeeds or fails.

The `response' attribute of the `COMPLETE` event can get the information returned.Obtain the loadable progress through `bytesLoaded` and` bytesTotal` of the `ProgressEvent` event.The callback function code is as follows:

```
private onGetComplete(event:egret.Event):void {
    var request = <egret.HttpRequest>event.currentTarget;
    console.log("get data : ",request.response);
    var responseLabel = new egret.TextField();
    responseLabel.size = 18;
    responseLabel.text = "GET response: \n" + request.response.substring(0, 50) + "...";
    this.addChild(responseLabel);
    responseLabel.x = 50;
    responseLabel.y = 70;
}

private onGetIOError(event:egret.IOErrorEvent):void {
    console.log("get error : " + event);
}

private onGetProgress(event:egret.ProgressEvent):void {
    console.log("get progress : " + Math.floor(100*event.bytesLoaded/event.bytesTotal) + "%");
}
```

The code for sending the POST request is as follows:

```
var request = new egret.HttpRequest();
request.responseType = egret.HttpResponseType.TEXT;
//set to POST request
request.open("http://httpbin.org/post",egret.HttpMethod.POST);
request.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
request.send();
request.addEventListener(egret.Event.COMPLETE,this.onPostComplete,this);
request.addEventListener(egret.IOErrorEvent.IO_ERROR,this.onPostIOError,this);
request.addEventListener(egret.ProgressEvent.PROGRESS,this.onPostProgress,this);
```

Add callback function:

```
private onPostComplete(event:egret.Event):void {
    var request = <egret.HttpRequest>event.currentTarget;
    console.log("post data : ",request.response);
    var responseLabel = new egret.TextField();
    responseLabel.size = 18;
    responseLabel.text = "POST response:\n" + request.response.substring(0, 50) + "...";
    this.addChild(responseLabel);
    responseLabel.x = 300;
    responseLabel.y = 70;
}

private onPostIOError(event:egret.IOErrorEvent):void {
    console.log("post error : " + event);
}

private onPostProgress(event:egret.ProgressEvent):void {
    console.log("post progress : " + Math.floor(100*event.bytesLoaded/event.bytesTotal) + "%");
}
```

## 3. Send a request accompanied with parameters

In the above, we sent a blank request to the server. During the actual usage process, generally we need to send a request with parameters to the server.

Format of the data sent: the data sent by the HTTP client is usually in the form of `key` and` value`, and multiple data are connected with `&`.After splicing,  the following form is formed:

```
key1=value1&key2=valueP2
```

The parameters sent via the GET method will be added at the place after the URL and separated by `?`.The parameters sent by POST need first to set the header information of HTTP request, tell the server in what form the data is sent.The most commonly used one is `application/x-www-form-urlencoded`, which means that we format the parameters with` key` and `value`.The server can also get the parameters with the same method.

### 3.1. The server obtains the parameter configuration

Next, by taking PHP as an example, we briefly explain the basic process of sending and/or taking parameters.

> Please configure PHP environment by yourself.It is the same case for other backend languages.If you do not use `key` and` value` to get the data, please get data by referring to the standard input stream of the corresponding language.

First, create the `get_testphp` file. The parameter for getting GET in PHP can be obtained through a global array `$ _GET [] `.The following code will get and return the value of the parameter with `key` being `p1` and `p2`.

```
<?php
     echo $_GET['p1'];
     echo $_GET['p2'];
?>```

Similarly, also create `post_test.php`, and get the parameters in PHP through the global array `$ _POST []` .The following code will get and return the value of the parameter with `key` being `p1` and `p2`.
```
<?php
     echo $_POST['p1'];
     echo $_POST['p2'];
?>```

### 3.2. The client sends the parameters

After establishing two PHP files, send parameters to them.

The first is a GET request, which needs to stitch parameters into the place after the URL before implementation.Where the URL and parameters need to use to be linked with `?`.Modify the corresponding codes of the above Get request, which is as follows:

```
//splice parameters 
var params = "?p1=getP1&p2=getP2";
var request = new egret.HttpRequest();
request.responseType = egret.HttpResponseType.TEXT;
//splice the parameters into url
request.open("php/get_test.php"+params,egret.HttpMethod.GET);
request.send();
```

Send a POST request. It is important to note that parameters need to be put into the parameter of `send` method when sending a POST request.And its response header needs to be set. In our example, the methods of  `key` `value` are used to format the parameters, where the response head `Content-Type` needs to be set as `application/x-www-form-urlencoded`.Modify the corresponding codes of the above POST request, which is as follows:

```
//splice parameters
var params = "p1=postP1&p2=postP2";

var request = new egret.HttpRequest();
request.responseType = egret.HttpResponseType.TEXT;
request.open("php/post_test.php",egret.HttpMethod.POST);
//set the response header
request.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
// send parameters
request.send(params);
```

The complete code is as follows:

```
/**
 * The following example uses the egret.HttpRequest class for network communication.
 */
class Main extends egret.DisplayObjectContainer {

    private statusGetLabel:egret.TextField;
    private statusPostLabel:egret.TextField;

    public constructor() {
        super();
        this.sendGetRequest();
        this.sendPostRequest();
    }

    private sendGetRequest():void {
        var statusGetLabel = new egret.TextField();
        this.statusGetLabel = statusGetLabel;
        statusGetLabel.size = 18;
        statusGetLabel.text = "GET request being sent to httpbin.org";
        this.addChild(statusGetLabel);
        statusGetLabel.x = 50;
        statusGetLabel.y = 40;
        var params = "?p1=getP1&p2=getP2";
        var request = new egret.HttpRequest();
        request.responseType = egret.HttpResponseType.TEXT;
        request.open("php/get_test.php"+params,egret.HttpMethod.GET);
        request.send();

        request.addEventListener(egret.Event.COMPLETE,this.onGetComplete,this);
        request.addEventListener(egret.IOErrorEvent.IO_ERROR,this.onGetIOError,this);
        request.addEventListener(egret.ProgressEvent.PROGRESS,this.onGetProgress,this);
    }

    private onGetComplete(event:egret.Event):void {
        var request = <egret.HttpRequest>event.currentTarget;
        console.log("get data : ",request.response);
        var responseLabel = new egret.TextField();
        responseLabel.size = 18;
        responseLabel.text = "GET response: \n" + request.response.substring(0, 50) + "...";
        this.addChild(responseLabel);
        responseLabel.x = 50;
        responseLabel.y = 70;
        this.statusGetLabel.text = "Get GET response!";
    }

    private onGetIOError(event:egret.IOErrorEvent):void {
        console.log("get error : " + event);
    }

    private onGetProgress(event:egret.ProgressEvent):void {
        console.log("get progress : " + Math.floor(100*event.bytesLoaded/event.bytesTotal) + "%");
    }

    private sendPostRequest() {
        var statusPostLabel = new egret.TextField();
        this.statusPostLabel = statusPostLabel;
        this.addChild(statusPostLabel);
        statusPostLabel.size = 18;
        statusPostLabel.x = 300;
        statusPostLabel.y = 40;
        statusPostLabel.text = "Sending POST request to httpbin.org";

        var params = "p1=postP1&p2=postP2";

        var request = new egret.HttpRequest();
        request.responseType = egret.HttpResponseType.TEXT;
        request.open("php/post_test.php",egret.HttpMethod.POST);
        request.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
        request.send(params);
        request.addEventListener(egret.Event.COMPLETE,this.onPostComplete,this);
        request.addEventListener(egret.IOErrorEvent.IO_ERROR,this.onPostIOError,this);
        request.addEventListener(egret.ProgressEvent.PROGRESS,this.onPostProgress,this);

    }

    private onPostComplete(event:egret.Event) {
        var request = <egret.HttpRequest>event.currentTarget;
        console.log("post data : ",request.response);
        var responseLabel = new egret.TextField();
        responseLabel.size = 18;
        responseLabel.text = "POST response:\n" + request.response.substring(0, 50) + "...";
        this.addChild(responseLabel);
        responseLabel.x = 300;
        responseLabel.y = 70;
        this.statusPostLabel.text = "Get POST response!";
    }

    private onPostIOError(event:egret.IOErrorEvent):void {
        console.log("post error : " + event);
    }

    private onPostProgress(event:egret.ProgressEvent):void {
        console.log("post progress : " + Math.floor(100*event.bytesLoaded/event.bytesTotal) + "%");
    }
}
```















