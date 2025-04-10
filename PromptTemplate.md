

# 🧠 Prompt Templates with Variables in Spring AI

Spring AI provides a flexible way to work with dynamic prompts using `PromptTemplate`. This is incredibly useful for building AI-powered apps like translators, chatbots, summarizers, or assistants — where your input keeps changing, but your prompt logic stays the same.

---

## ✅ What is a Prompt Template?

A `PromptTemplate` is like a sentence with blanks. You fill in the blanks later.

```text
"Translate this sentence to Tamil: {{input}}"
```

You then replace `{{input}}` with the actual user input dynamically in code.

---

## 🛠️ How to Use `PromptTemplate` in Spring AI

### 📦 Step 1: Import Required Classes

```java
import org.springframework.ai.chat.prompt.Prompt;
import org.springframework.ai.chat.prompt.PromptTemplate;
import java.util.Map;
```

---

### 📦 Step 2: Create and Use the Prompt Template

Here’s how you use a template in your Spring Boot service class:

```java
public String translateToTamil(String sentence) {
    PromptTemplate promptTemplate = new PromptTemplate(
        "Translate the following sentence to Tenkasi Tamil dialect: {{input}}"
    );

    Prompt prompt = promptTemplate.create(Map.of("input", sentence));

    return chatClient.prompt(prompt).call().content();
}
```

✅ `{{input}}` will be replaced with the value from `Map.of("input", sentence)`.

---

## 🧪 Example Output

### Input:
```java
translateToTamil("How are you?")
```

### Final Prompt Sent to AI:
```text
Translate the following sentence to Tenkasi Tamil dialect: How are you?
```

### AI Response:
```text
நீ எப்படி இருக்க?
```

---

## 🔁 Using Multiple Variables

Prompt templates support multiple variables too:

```java
PromptTemplate template = new PromptTemplate(
    "Write a {{tone}} message to {{person}} about {{topic}}."
);

Prompt prompt = template.create(Map.of(
    "tone", "friendly",
    "person", "Kishore",
    "topic", "Spring Boot"
));
```

Resulting prompt:
```text
Write a friendly message to Kishore about Spring Boot.
```

---

## 📁 Bonus: Load Prompt Templates from Files (Optional)

You can store prompt templates as `.txt` or `.tmpl` files in your resources folder:

**File:** `src/main/resources/prompts/translate.tmpl`
```text
Translate the following sentence to Tenkasi Tamil dialect: {{input}}
```

Then load it like this:

```java
PromptTemplate template = new PromptTemplate(
    new ClassPathResource("prompts/translate.tmpl")
);
Prompt prompt = template.create(Map.of("input", "How are you?"));
```

---
