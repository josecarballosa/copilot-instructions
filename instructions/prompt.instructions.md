---
applyTo: '**/*.prompt.md, **/*.instructions.md, **/*.chatmode.md'
---

# General prompt writing standards
> Comprehensive best practices for creating effective and responsible prompts
> for GitHub Copilot, diverse LLMs, and AI agents.

## 1. Core Principles: The Foundation of a Good Prompt

### 1.1. Write Clear, Specific, and Direct Instructions
Eliminate ambiguity. Do not assume the AI has implicit knowledge of your goals.

- Use explicit and concise language. Instead of "fix this code,"
  write "Refactor this Python function to improve its readability and add
  comments explaining the logic."
- Specify the desired output format, style, and length. For example,
  "Generate a summary of the following text as a JSON object with keys 'summary'
  and 'keywords'."
- Avoid vague or overly complex language. Break down complex requests into
  simpler statements.

### 1.2 Provide a Relevant Goal
The AI works better when it understands the "why" behind the task given. Provide
background information, constraints, user personas, and the overall goal.

### 1.3. Include Sufficient Context
The AI may need information to perform a better task. Provide details to ground 
the responses and eliminate hallucinations. 

- Include relevant information. For example, fresh documentation, snippets, or
  domain-specific terms.
- Reference relevant standards, frameworks, or methodologies.
- Specify the target audience and their technical level.
- Mention any specific requirements or constraints.
- Place context before the primary instruction.

- **Example:**
```
# CONTEXT

I am building a web application using Flask and SQLAlchemy.
Here is my User model:

class User(db.Model):
    id = db.Column(db.Integer, primary\_key=True)
    username = db.Column(db.String(80), unique=True, nullable=False)

# TASK

Write a SQLAlchemy query to find a user by their username.
````

### 1.3. Use an Iterative Approach
Start with a simple prompt and refine it based on the output.

- **Step 1:** Formulate a basic prompt to get an initial response.
- **Step 2:** Analyze the output. If it's not ideal, identify the shortcomings.
- **Step 3:** Add more detail, context, or examples to your prompt to address
the shortcomings and try again.

---

## 2. Prompt Structure and Formatting

### 2.1. Use Delimiters to Structure the Prompt
Use structural elements to create a clear separation between different parts of
your prompt, such as context, examples, and the final instruction.

- **Recommended Delimiters:** Use triple hashes (`###`), triple quotes (`"""..."""`),
or XML tags (`<context>`, `<example>`) to encapsulate different sections.
- **Example with XML Tags:**
```xml
<context>
  You are an expert programmer specializing in writing secure and efficient Python code.
</context>
<task>
  Review the following Python function for security vulnerabilities, specifically looking for SQL injection risks.
  <code>
  def get_user_data(user_id):
      query = "SELECT * FROM users WHERE id = '" + user_id + "'"
      # ... execute query ...
  </code>
</task>
<output_format>
  Provide your analysis as a list of identified vulnerabilities and suggest a corrected version of the code using parameterized queries.
</output_format>
````

### 2.2. Place Instructions First, Context Last

The order of elements in your prompt matters. In most cases, place the primary
instruction or role at the beginning.

**General Order**: 

-  **Role/Persona:** "You are a..."
-  **Task/Instruction:** "Your task is to..."
-  **Output Constraints/Format:** "The output must be..."
-  **Examples (Few-Shot):** `## Example 1 ##`
-  **Context/Input Data:** `## Context ##`

-----

## 3. Content and Instructions

### 3.1. Provide High-Quality Examples (Few-Shot Prompting)

Guide the AI by showing it exactly what you want. Providing examples of
input-output pairs is one of the most effective ways to improve response quality.

  - **DO:** Include 2-5 examples that are relevant to the task.
  - **DO:** Ensure the examples cover a range of scenarios, including potential edge cases.
  - **DO:** Maintain a consistent format between your examples and your final query.

### 3.2. Assign a Clear Role or Persona

Instruct the AI to adopt a specific persona to shape the tone, style, and
expertise of its response.

  - **Example:** "Act as a senior software architect. Propose three different
    design patterns for a scalable microservices-based notification system."

### 3.3. Instruct What to Do, Not What Not to Do

Phrase instructions positively. Telling the AI what to do is more effective than
listing what to avoid.

  - **LESS EFFECTIVE:** "Don't write a long response. Don't use technical jargon."
  - **MORE EFFECTIVE:** "Summarize the key points in three short,
    easy-to-understand bullet points."

-----

## 4. Advanced Techniques

### 4.1. Chain of Thought (CoT) Prompting

For complex reasoning tasks, instruct the model to "think step-by-step." This
forces a more logical and transparent reasoning process, which often leads to
better results.

**Example:** "Explain how to resolve this Git merge conflict. First, identify
the conflicting files. Second, explain the different sections of the conflict
marker. Third, provide a step-by-step resolution strategy."

### 4.2. Break Down Complex Tasks (Prompt Chaining)

Instead of one massive prompt, decompose a complex task into a sequence of
smaller, more manageable prompts. Use the output of one prompt as the input for
the next. This is highly effective for multi-step workflows.

**Example Workflow:**
- **Prompt 1:** "Given this user story, generate a list of technical
  requirements."
- **Prompt 2:** "Using the technical requirements from the previous step,
  write the corresponding function signatures in Python."
- **Prompt 3:** "Implement the following Python function:
  `[insert signature from step 2]`."

-----

## 5. Responsible AI and Safety

### 5.1. Design for Safety and Mitigate Bias

Be vigilant about the potential for generating harmful, biased, or insecure
content.

  - **DO:** Include a "safety instruction" in your prompts. For example, "Ensure
    the code does not contain any security vulnerabilities and handles user input
    safely."
  - **DO:** Review the generated content for biases (e.g., gender, race) and
    instruct the model to be neutral and inclusive.
  - **DO:** Provide an "out" for the model. Instruct it on how to respond if it
    cannot fulfill the request safely or ethically (e.g., "If the request is
    ambiguous or potentially harmful, respond with 'I cannot fulfill this
    request.'").

### 5.2. Require Fact-Checking and Source Citation

LLMs can "hallucinate" or invent facts. When factual accuracy is important,
instruct the model to be cautious and cite its sources.

  - **Example:** "Explain the difference between the GPL and MIT software licenses.
    Cite your sources using URLs where possible."
