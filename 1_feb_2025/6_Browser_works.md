# How Web Browsers Work

Browser is the way to connect to the internet and access information from around the world. Every day millions of web pages are visited. If you are a web developer, you must know how these browsers work, because this will help you optimize performance and improve the user experience.

Let’s get into the working of browsers.

---

## Browser Overview

Users request a web page by entering the URL in the address bar. If it is for the first time, the Browser sends the request to DNS (Domain Name Server) and gets the IP address of the place where the information is stored.

- Based on the IP address, it creates a secure TCP connection.
- The network layer sends the request to the Server to share the webpage resources.
- Server then verifies and analyzes the request and sends the data (HTML, CSS, Javascript, Images, Fonts, etc.).
- The browser receives the data and uses the **Rendering Engine** to render the web page content. If there is any script to be executed, the browser will use the **Javascript Engine** to compile and execute it.
- If any data needs to be persisted, that will be cached for further use to improve performance.

### High-Level Browser Components

- User Interface  
- Network Layer  
- Browser Engine  
- Rendering Engine  
- Javascript Engine  
- Data Storage Layer

---

## 4 Basic Steps in Browser Working

1. **Request**  
2. **Render**  
3. **Display**  
4. **Store**

---

## 1. Request

Users request a web page by entering the URL. The browser connects to the server and requests the page.

### Network Layer

- Checks DNS cache. If not available, sends a request to DNS for IP address.
- Uses the IP to establish a **TCP** connection.
- If using **HTTPS**, TLS/SSL handshake occurs:
  - Chooses a cipher.
  - Server sends digital certificate.
  - Once verified, a secure connection is established.
- Sends initial **HTTPS GET** request (usually for the HTML file).
- Server responds with headers and HTML content.

---

## 2. Render

The server sends data, which is processed using the **Render Engine** and displayed on the screen.

### Rendering Engine

Uses the **Critical Rendering Path**:

- **HTML Parser**: Converts HTML into tokens → DOM Tree.
- **CSS Parser**: Converts CSS into tokens → CSSOM Tree.
- **Render Tree**: Combines DOM + CSSOM (excludes elements with `display: none`).
- **Layout**: Calculates dimensions and positions of each element.
- **Paint**: Draws pixels layer by layer.
- **Compositing**: Final image is shown.

Rendering is done chunk by chunk—it doesn’t wait for the entire data to download.

---

## 3. Javascript Engine

Handles blocking (JS) and non-blocking (CSS, images) resources.

### JS Engine Components

- **Memory Heap**: Where code is stored.
- **Call Stack**: Manages function calls (LIFO order).

JavaScript is **single-threaded**, executes one task at a time.

To handle async tasks like API calls:

- Uses browser APIs (setTimeout, fetch, DOM API).
- Executes via **Event Loop**.

> Learn More about Event Loop [Here](#).

---

## 4. Display

### User Interface

Includes:

- Address Bar  
- Back/Forward buttons  
- Bookmark menu  
- Home button  
- Input fields  
- Large content viewport  

### Browser Engine

Handles:

- Navigation, reload, bookmarks  
- Tab management, history  
- Communicates with:
  - Render Engine for UI
  - Network Layer for data
- Manages security, privacy, and extensions

---

## 5. Storage

**Data Storage Layer** handles saving data locally.

### Storage Types

- **Cookies**: Key-value pairs (Max 5 MB). Used in client-server communication.
- **Local Storage**: Key-value (Max 50 MB). Persistent storage for user data, tokens, etc.
- **Session Storage**: Key-value, exists only while browser is open (Max 5 MB).
- **IndexedDB**: Large structured data storage.
- **FileSystem**: Sandboxed file access for reading/writing.
- **Service Workers**: Offline caching, intercepting requests for better performance.

---

## Conclusion

I hope you understand how web browsers work.

---

## You can read my other blogs:

- [Critical Rendering Path](#)
- [How Event Loop Works](#)

---

**Thank you for reading until the end.**  
Please consider clapping and following! 👏
