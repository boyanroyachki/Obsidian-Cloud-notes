### XHR (XMLHttpRequest) Overview

#### Introduction
XMLHttpRequest (XHR) is an API in the form of an object, provided by web browsers' JavaScript environment, for sending HTTP or HTTPS requests to a web server and loading the server response data back into the script. This object is primarily used for implementing AJAX (Asynchronous JavaScript and XML) operations, allowing web pages to be updated asynchronously by exchanging small amounts of data with the server behind the scenes. This means that it is possible to update parts of a web page, without reloading the entire page.

#### Key Features and Methods

1. **Creating an XMLHttpRequest Object:**
   ```javascript
   var xhr = new XMLHttpRequest();
   ```

2. **Opening a Request:**
   The `open` method initializes a request. It specifies the HTTP method (e.g., GET, POST), the URL, and whether the request should be asynchronous.
   ```javascript
   xhr.open('GET', 'https://api.example.com/data', true);
   ```

3. **Sending a Request:**
   The `send` method sends the request to the server. For POST requests, you can include the request body.
   ```javascript
   xhr.send();
   ```

4. **Handling the Response:**
   The `onreadystatechange` event handler is triggered every time the `readyState` property changes. When `readyState` is 4 and `status` is 200, the response is ready.
   ```javascript
   xhr.onreadystatechange = function() {
       if (xhr.readyState == 4 && xhr.status == 200) {
           console.log(xhr.responseText);
       }
   };
   ```

5. **Common Properties:**
   - `xhr.readyState`: Holds the status of the XMLHttpRequest.
     - 0: request not initialized
     - 1: server connection established
     - 2: request received
     - 3: processing request
     - 4: request finished and response is ready
   - `xhr.status`: HTTP status code of the response.
   - `xhr.statusText`: HTTP status text of the response.
   - `xhr.responseText`: Returns the response data as a string.
   - `xhr.responseXML`: Returns the response data as XML data.

6. **Configuring Request Headers:**
   You can set request headers using the `setRequestHeader` method.
   ```javascript
   xhr.setRequestHeader('Content-Type', 'application/json');
   ```

7. **Handling Errors:**
   Handle network errors using the `onerror` event handler.
   ```javascript
   xhr.onerror = function() {
       console.error('Request failed');
   };
   ```

#### Example Usage

Here is an example of using XHR to fetch data from a server:

```javascript
var xhr = new XMLHttpRequest();
xhr.open('GET', 'https://jsonplaceholder.typicode.com/posts', true);
xhr.onload = function() {
    if (xhr.status >= 200 && xhr.status < 300) {
        console.log(JSON.parse(xhr.responseText));
    } else {
        console.error('Error:', xhr.statusText);
    }
};
xhr.onerror = function() {
    console.error('Request failed');
};
xhr.send();
```

#### Synchronous vs. Asynchronous Requests

- **Asynchronous Requests (default):** Do not block the execution of other scripts while waiting for the server's response.
- **Synchronous Requests:** Block the execution of code until the server response is received. It's generally discouraged to use synchronous requests because they can make the web page unresponsive.

#### Cross-Origin Requests

XMLHttpRequest follows the same-origin policy. This means that web applications can only request resources from the same origin the application was loaded from unless the server provides appropriate CORS (Cross-Origin Resource Sharing) headers.

#### Advantages of XHR

1. **Partial Page Updates:** Allows updating parts of a web page without reloading the entire page.
2. **Improved User Experience:** Provides a smoother and faster interaction by reducing full page reloads.
3. **Enhanced Performance:** Reduces server load and network usage by sending and receiving only necessary data.

#### Limitations of XHR

1. **Complexity:** Handling multiple states and different response types can be complex.
2. **Browser Support:** Older browsers may not support all features of the XMLHttpRequest object.
3. **Security:** Same-origin policy can restrict requests to resources from different domains.

#### Conclusion

XMLHttpRequest is a fundamental part of modern web development, enabling the creation of dynamic, responsive web applications. It allows for efficient data exchange with servers, thereby enhancing user experience through partial page updates and asynchronous operations.

For further reading and more detailed examples, you can refer to:
- [MDN Web Docs on XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)
- [W3Schools XMLHttpRequest Tutorial](https://www.w3schools.com/xml/xml_http.asp)