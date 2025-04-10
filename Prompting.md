
# 🧠 Prompting Strategies in Spring AI (Zero-Shot vs Few-Shot)

Welcome to one of the most powerful concepts when working with **LLMs** like **GPT** inside a **Spring Boot** application: **Prompting**.

This guide explains:
- What **Zero-Shot** and **Few-Shot** prompting are
- When and how to use them in **Spring AI**
- Real-world analogies & code examples

---

## 🔹 What is Prompting?

Prompting is the art of crafting the **input (instructions or examples)** you send to an AI model to guide its response. It’s like telling a smart assistant **what you want it to do**.

---

## 🟢 1. Zero-Shot Prompting  
> 🕵️ Like throwing the AI into a task blind!

### 🔸 Concept:
- No examples provided.
- Just **clear instructions** in plain English (or your preferred language).

📌 **Best For**:
- Simple, familiar tasks (translation, summarization, Q&A)
- When you want quick results without training.

---

### ✅ Example (Translation)

```java
Prompt prompt = new Prompt("Translate 'Hello' to French.");
String response = chatClient.prompt(prompt).call().content();
System.out.println(response);  // Bonjour
```

---

### ✅ Example (Summarization)

```java
Prompt prompt = new Prompt("Summarize this: Java is a high-level, object-oriented programming language...");
String response = chatClient.prompt(prompt).call().content();
System.out.println(response);
```

---

## 🟡 2. Few-Shot Prompting  
> 📚 Like giving the AI examples first

### 🔸 Concept:
- Provide a few **examples** of the task first.
- Then give **one new input** and let the AI follow the pattern.

📌 **Best For**:
- Custom tasks with **specific formats**
- Reducing randomness in output

---

### 🧠 Prompt Example:
```text
Translate English to French:
English: Hello
French: Bonjour

English: Good night
French: Bonne nuit

English: How are you?
French:
```

🧠 The AI learns the pattern and responds with:
```
Comment ça va ?
```

---

### ✅ Spring AI Code:

```java
String fewShotPrompt = """
Translate English to French:
English: Hello
French: Bonjour

English: Good night
French: Bonne nuit

English: How are you?
French:
""";

Prompt prompt = new Prompt(fewShotPrompt);
String response = chatClient.prompt(prompt).call().content();
System.out.println(response);
```

---

## 🔁 Dynamic Prompting with `PromptTemplate`

Use `PromptTemplate` to make your prompts reusable and dynamic.

### ✅ Example:

```java
PromptTemplate template = new PromptTemplate(
    "Translate this to Tamil: {{input}}"
);
Prompt prompt = template.create(Map.of("input", "Good Morning"));

String response = chatClient.prompt(prompt).call().content();
System.out.println(response);
```

---

## 🧪 Prompting Comparison

| Prompting Type | Description                         | Best Use Cases                              |
|----------------|-------------------------------------|---------------------------------------------|
| **Zero-Shot**  | Just give the task instruction      | Translation, summarization, Q&A             |
| **Few-Shot**   | Add examples + instructions         | Custom formats, data labeling, controlled output |
| **PromptTemplate** | Dynamic placeholders (`{{input}}`) | Reusability, clean code, production systems |

---

## 🚀 Bonus Ideas

Want to build a real app using prompting?

- 🌐 **Mini Project**: Translate phrases between multiple languages
- 💬 **Chatbot**: Few-shot personality-based responses
- 📄 **Resume Scorer**: Few-shot prompts to rate resume quality
- 🧘‍♀️ **Mental Health Companion**: Zero-shot + few-shot prompts for supportive chats

---

## 📦 Spring AI Essentials

### Required Dependency (`build.gradle.kts` or `pom.xml`)
```groovy
implementation("org.springframework.experimental:spring-ai-openai-spring-boot-starter")
```

### Required Beans
Make sure you have the `ChatClient` auto-configured:

```java
@Autowired
private ChatClient chatClient;
```

---

## 💡 Summary

Prompting is an **essential skill** when working with LLMs. Spring AI makes it easy to plug in zero-shot or few-shot logic right into your Java codebase.

| 🔄 Strategy     | When to Use                            |
|-----------------|-----------------------------------------|
| **Zero-Shot**   | Quick, general-purpose tasks            |
| **Few-Shot**    | You want AI to follow a format/pattern  |
| **PromptTemplate** | Reuse prompts with dynamic inputs   |

---

## 🧰 Want Starter Code?

Clone this repo or ask to generate a working Spring Boot app with:
- ✅ PromptTemplate
- ✅ ChatClient config
- ✅ Few-shot & zero-shot examples
- ✅ REST endpoints

Just ask and we’ll scaffold it for you!

---




