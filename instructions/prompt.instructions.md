---
applyTo: '**/*.prompt.md, **/*.instructions.md, **/*.chatmode.md'
---

# General prompt writing standards
> Comprehensive best practices for creating effective and responsible prompts
> for GitHub Copilot, diverse LLMs, and AI agents.

## 1. Core Principles: The Foundation of a Good Prompt

### 1.1. Write Clear, Specific, and Direct Instructions
Eliminate ambiguity. Do not assume the AI has implicit knowledge of your goals.

- Use explicit and concise language. 
- Specify the desired output format, style, and length. 
- Avoid vague or overly complex language.
- Break down complex requests into simpler statements.

### 1.2 Provide a Relevant Goal
Provide background information, constraints, user personas, and an overall goal.
The AI works better when it understands the "why" behind the given task. 

### 1.3. Include Sufficient Context
Provide critical details to ground AI responses and prevent hallucinations. 

- Include relevant details. For example, fresh documentation snippets.
- Reference relevant standards, frameworks, or methodologies.
- Specify the target audience and their technical level.
- Mention any specific requirements or constraints.

### 1.4. Use an Iterative Approach
Start with a simple prompt and refine it based on the output.

1. Start with a basic prompt to get an initial response.
2. Analyze the output. Evaluate metrics.
3. If it's not ideal, identify the shortcomings.
4. Add or modify detail, context, or examples to address the shortcomings, and try again.
5. Document results and reasoning.

**Evaluation Metrics:**
- **User Satisfaction:** How well does the output matches user's expectations?
- **Relevance:** How closely the output addresses the task?
- **Safety:** Does it produce any harmful or biased results?
- **Consistency:** Do similar inputs produce similar outputs?
- **Efficiency:** How is the speed and resource usage?

**Versioning and Lifecycle Management:**
- Track prompt versions and changes.
- Document the reasoning behind changes.
- Maintain backward compatibility when possible.
- Plan for prompt updates and migrations.

---

## 2. Prompt Structure and Formatting

### 2.1. Use Delimiters to Structure the Prompt
Use structural elements when appropriate to create a more clear separation between different parts of
your prompt, such as context, examples, and the final instruction.

- **Recommended Delimiters:** Use triple hashes (`###`), or XML tags (`<context>`, `<example>`)
  to encapsulate different sections.
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
```

### 2.2. Place Instructions First, Context Last

In most cases, place the primary instruction or role at the beginning.
The order of elements in your prompt matters. 

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

  - Include 2-5 examples that are relevant to the task.
  - Ensure the examples cover a range of scenarios, including potential edge cases.
  - Maintain a consistent format between your examples and your final query.

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
  write the corresponding function signatures."
- **Prompt 3:** "Implement the following function:
  `[insert signature from step 2]`."

-----

## 5. Responsible AI and Safety

### 5.1. Design for Safety and Mitigate Bias

Be vigilant about the potential for generating harmful, biased, or insecure
content.

  - Include a "safety instruction" in your prompts. For example, "Ensure
    the code does not contain any security vulnerabilities and handles user input
    safely."
  - Review the generated content for biases (e.g., gender, race, age) and
    instruct the model to be neutral and inclusive.
  - Provide an "out" for the model. Instruct it on how to respond if it
    cannot fulfill the request safely or ethically (e.g., "If the request is
    ambiguous or potentially harmful, respond with 'I cannot fulfill this
    request.'").
  - Include human oversight for sensitive content or tasks.

### 5.2. Require Fact-Checking and Source Citation

LLMs can "hallucinate" or invent facts. When factual accuracy is important,
instruct the model to be cautious and cite its sources.

  - **Example:** "Explain the difference between the GPL and MIT software licenses.
    Cite your sources using URLs where possible."
