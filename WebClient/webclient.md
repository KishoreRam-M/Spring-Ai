## 🌐 What is `WebClient`?

### ➤ **Definition**

`WebClient` is a **non-blocking**, **reactive HTTP client** provided by **Spring WebFlux**.
You use it to **send HTTP requests** (like GET, POST) to other APIs or web services.

It’s a modern alternative to:

* `RestTemplate` (which is **blocking**, old style)
* `HttpURLConnection` (very low-level)

---

## 📦 Package Info

```java
import org.springframework.web.reactive.function.client.WebClient;
```

---

## ✅ Why use `WebClient`?

| Feature                    | Description                                                |
| -------------------------- | ---------------------------------------------------------- |
| 🔄 Reactive (non-blocking) | Good for performance under high load                       |
| 🔧 Flexible                | Easily handles headers, query params, authentication, etc. |
| 📡 Async by default        | Doesn’t block threads while waiting for HTTP responses     |
| 🧵 Efficient               | Saves resources, uses fewer threads                        |

---

## 🛠️ What can you do with `WebClient`?

### Example Use Cases:

* Call external APIs (e.g., OpenAI, Gemini, Stripe, etc.)
* Communicate between microservices
* Consume REST APIs or GraphQL APIs

---

## 🧪 Simple Example

```java
WebClient client = WebClient.create();

String response = client.get()
    .uri("https://api.example.com/data")
    .retrieve()
    .bodyToMono(String.class)
    .block(); // blocking just for demo
```

✔️ This makes a GET request to `https://api.example.com/data`
✔️ Converts the response body into a `String`

---

## ⏱ Blocking vs Non-blocking

| Concept      | RestTemplate (Old) | WebClient (Modern)  |
| ------------ | ------------------ | ------------------- |
| Blocking     | Yes                | No (async/reactive) |
| Thread Usage | More               | Less                |
| Performance  | Lower under load   | Higher under load   |
