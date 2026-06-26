# Урок 1: Что такое ИИ-агенты?

## Введение

Вы, вероятно, использовали ChatGPT, Gemini или Claude, чтобы ответить на вопрос или написать код. Вы что-то вводили, получали ответ и двигались дальше. Это языковая модель, выполняющая свою работу — предсказывающая полезный текст на основе вашего ввода.

ИИ-агент — это нечто другое. Агент может **думать**, **действовать** и **запоминать**. Он не просто отвечает на ваш вопрос — он определяет, какие шаги предпринять, использует инструменты для выполнения этих шагов и корректирует свой подход в зависимости от происходящего на этом пути.

Представьте себе: если бы вы наняли нового инженера и позволили ему только говорить, но никогда не прикасаться к клавиатуре, не открывать браузер и не читать документацию, его возможности были бы ограничены. Это само по себе является языковой моделью. Теперь предоставьте этому инженеру доступ к вашей кодовой базе, терминалу, документам вашей компании и возможность задавать уточняющие вопросы. Это и есть агент.

В этом уроке рассматривается, что такое агенты искусственного интеллекта, чем они отличаются от моделей, использующих обычный язык программирования, из каких компонентов они работают и когда их следует (и когда не следует) использовать.

---

## Что такое ИИ-агент простыми словами?

ИИ-агент — это программная система, использующая языковую модель в качестве основного механизма рассуждений, в сочетании со способностью совершать действия в реальном мире. Эти действия могут включать:

- Поиск в интернете
- Запрос к базе данных
- Вызов API
- Чтение или запись файлов
- Отправка электронного письма
- Выполнение кода

Ключевое отличие — **автономия**. Обычный LLM отвечает на один запрос. Агент получает цель, а затем самостоятельно решает, какие шаги предпринять, выполняет эти шаги, наблюдает за результатами и продолжает до тех пор, пока цель не будет достигнута (или пока не определит, что цель не может быть достигнута).

### Аналогия с новым сотрудником

Представьте, что вы нанимаете нового инженера-программиста. В первый день вы не ожидаете, что он будет знать всё. Но от них можно было бы ожидать следующего:

1. **Читать документацию**, чтобы понять код
2. **Использовать инструменты**, такие как IDE, терминал и браузер
3. **Задавать вопросы**, когда что-то непонятно
4. **Разбивать задачи** на более мелкие шаги
5. **Проверять свою работу**, прежде чем сказать, что она завершена
6. **Учиться на ошибках** и корректировать свой подход

Агент ИИ работает аналогичным образом. Он имеет базу знаний (языковую модель), доступ к инструментам и уровень оркестровки, который управляет циклом мышления, действия и наблюдения.

---

## LLM против агента: в чем разница?

Это самое важное различие, которое нужно усвоить как можно раньше.

| Аспект | LLM (самостоятельно) | ИИ-агент |
|---|---|---|
| **Что он делает** | Генерирует текст на основе запроса | Достигает цели в несколько этапов |
| **Взаимодействие** | Один ход (или многоходовый чат) | Автономный цикл мышления и действия |
| **Инструменты** | Нет - ввод текста, вывод текста | Может вызывать функции, API, осуществлять поиск и т. д. |
| **Память** | Ограничена контекстным окном | Может сохранять информацию между этапами |
| **Принятие решений** | Отвечает на ваши вопросы | Самостоятельно решает, что делать дальше |
| **Обработка ошибок** | Дает ответ (правильный или неправильный) | Может отслеживать ошибки и повторять попытку с новым подходом |

Полезная ментальная модель:

- **LLM** = Мозг
- **Agent** = Мозг + Руки + Память

Мозг (LLM) выполняет рассуждения. Руки (инструменты) позволяют ему действовать. Память (управление состоянием) позволяет ему отслеживать, что произошло и что еще нужно сделать.

### Конкретный пример

**Только LLM:** Вы спрашиваете: «Какова текущая цена акций GOOG?» Модель может ответить: «По последним данным для обучения, она составляла около 140 долларов» — что может быть устаревшей информацией на несколько месяцев.

**Агент:** Вы задаете тот же вопрос. Агент думает: «Мне нужны актуальные данные по акциям, мне следует использовать финансовый API». Он вызывает инструмент для расчета цен на акции, получает текущую цену и возвращает точный ответ. Если вызов API не удается, он может попробовать другой источник данных.

Этот цикл — думать, действовать, наблюдать, повторять — и делает агента агентом.

---

## Основные компоненты ИИ-агента

Каждая агентная система, независимо от используемой платформы, имеет три основных компонента:

### 1. модель (мозг)

Это языковая модель, находящаяся в центре агента. Она отвечает за:

- **Понимание** цели пользователя
- **Рассуждение** о том, какие шаги предпринять
- **Выбор** инструмента для использования (и с какими параметрами)
- **Интерпретацию** результатов вызовов инструментов
- **Генерацию** окончательного ответа

Выбор модели имеет значение. Для более сложных задач (многошаговое рассуждение, сложная генерация кода, принятие решений с учетом нюансов) лучше подходят передовые модели, такие как Gemini или Opus. Для более простых задач (классификация, извлечение информации, простые вопросы и ответы) можно использовать более легкие модели, такие как Gemini Flash, чтобы сэкономить средства и уменьшить задержку.

### 2. инструменты (руки)

Инструменты — это то, что позволяет агенту взаимодействовать с миром за пределами генерации текста. Без инструментов агент — это просто чат-бот. С инструментами он может:

- **Получить информацию**: поиск в интернете, запрос к базе данных, чтение файла
- **Выполнить действия**: отправить электронное письмо, создать заявку, развернуть код
- **Вычислить**: выполнить вычисления, запустить код, преобразовать данные

Инструменты обычно определяются как функции с четкими именами, описаниями и схемами параметров. Модель решает, когда и как их вызывать. Мы подробно рассмотрим инструменты в уроке 3.

### 3. уровень оркестровки (цикл управления)

Это связующее звено, объединяющее модель и инструменты в функционирующую систему. Уровень оркестровки управляет:

- **Циклом агента**: Думать -> Действовать -> Наблюдать -> Повторять
- **Управление состоянием**: Что произошло до сих пор, какой контекст нужен модели
- **Обработка ошибок**: Что делать, если вызов инструмента не удался
- **Условия завершения**: Когда остановить цикл и вернуть результат
- **Ограничения**: Проверки безопасности, проверка выходных данных, ограничения области действия

Простейший шаблон оркестровки выглядит так:

```
1. Получение цели пользователя
2. Отправка цели + доступных инструментов модели
3. Модель возвращает либо:
   a. Окончательный ответ -> Вернуть пользователю
   b. Выполнить инструмент, добавить результат в контекст, перейти к шагу 2
```

Это часто называют **циклом ReAct** (Рассуждение + Действие). Существуют и более сложные шаблоны — мы рассмотрим их в последующих уроках.

### Как компоненты взаимодействуют друг с другом

```
Цель пользователя
    |
    v
+-------------------+
| Слой              |
| оркестрации       |
|                   |
|  +-------------+  |
|  |   Модель    |  |    "Мне нужно найти X"
|  |  (Мозг)     |--+--->  Вызов инструмента
|  +-------------+  |         |
|        ^          |         v
|        |          |  +-------------+
|        +----------+--+ Инструменты |
|     Результаты    |  |   (Руки)    |
| работы инструмента|  +-------------+
+-------------------+
    |
    v
Итоговый ответ
```

---

## Таксономия агентных систем

Не все агенты одинаковы. Полезно рассматривать агентные системы в спектре автономности и возможностей, от уровня 0 до уровня 4.

### Уровень 0: базовое рассуждение (простая языковая модель)

**Что это:** Языковая модель, отвечающая на вопросы без инструментов или памяти.

**Пример:** Вы спрашиваете Gemini:«Объясните теорему CAP», и она дает вам четкое объяснение на основе своих обучающих данных.

**Возможности:**
- Генерация и понимание текста
- Одно- или многоходовый диалог
- Отсутствие доступа к внешним данным
- Отсутствие возможности выполнения действий

**Когда работает хорошо:** Вопросы на общие знания, творческое письмо, мозговой штурм, обобщение предоставленного текста.

### Уровень 1: подключенный решатель проблем (агент, использующий инструменты)

**Что это:** Модель, которая может вызывать инструменты для получения информации или выполнения простых действий. Здесь мы переходим от «чат-бота» к «агенту»

**Пример:** Бот службы поддержки клиентов, который может узнать статус заказа, вызвав ваш API заказов, или помощник по программированию, который может искать документацию.

**Возможности:**
- Все возможности уровня 0
- Вызов функций (инструментов)
- Генерация с расширенным поиском (RAG) для работы с реальными данными
- Простое выполнение задач в один или несколько шагов

**Когда работает хорошо:** Задачи, требующие актуальных данных, интеграции с API, простых рабочих процессов с небольшим количеством шагов.

### Level 2: strategic agent (autonomous with context)

**What it is:** An agent that can plan multi-step approaches, maintain context across a longer session, and adapt its strategy based on intermediate results.

**Example:** A research agent that takes a question like "Compare the top 3 cloud providers on serverless pricing," then searches for pricing pages, extracts data, builds a comparison table, and summarizes findings.

**Capabilities:**
- Everything in Level 1
- Multi-step planning and execution
- Dynamic replanning when things change
- Working memory across steps
- Self-evaluation ("Is this result good enough?")

**When it works well:** Research tasks, complex troubleshooting, multi-step workflows where the path depends on intermediate results.

### Level 3: collaborative multi-agent system

**What it is:** Multiple specialized agents working together, each handling a different aspect of a larger task. One agent might coordinate the others.

**Example:** A software development system where one agent writes code, another writes tests, a third reviews the code, and an orchestrator agent manages the workflow.

**Capabilities:**
- Everything in Level 2
- Agent-to-agent communication
- Specialized roles and delegation
- Parallel execution of subtasks
- Consensus or voting mechanisms for quality

**When it works well:** Complex projects that benefit from specialization, tasks requiring multiple perspectives or quality gates.

### Level 4: self-evolving agent

**What it is:** An agent that can reflect on its own performance, learn from past runs, update its strategies, and improve over time without manual intervention.

**Example:** A deployment agent that tracks which rollback strategies worked best historically and adjusts its approach for future deployments.

**Capabilities:**
- Everything in Level 3
- Long-term memory and learning
- Strategy optimization based on past outcomes
- Self-modification of prompts or tool selection
- Performance monitoring and self-correction

**When it works well:** Recurring tasks where patterns emerge over time, systems that benefit from continuous improvement.

### Summary table

| Level | Name | Key Feature | Example |
|---|---|---|---|
| 0 | Basic Reasoning | Text in, text out | Chatbot, Q&A |
| 1 | Connected Problem-Solver | Tool use | Order lookup bot |
| 2 | Strategic Agent | Multi-step planning | Research assistant |
| 3 | Collaborative Multi-Agent | Agent coordination | Dev team simulation |
| 4 | Self-Evolving | Learning from experience | Adaptive ops agent |

Most production agent systems today operate at Level 1 or Level 2. Levels 3 and 4 are active areas of research and are becoming more practical, but they add significant complexity. Start simple and move up only when you have a clear reason to.

---

## When to use agents vs. when a simple prompt is enough

Agents add power but also complexity, cost, and latency. Not every problem needs an agent. Here is a practical guide.

### Use a simple prompt when:

- The task can be completed in a single step
- No external data or actions are needed
- The answer exists within the model's training data
- Low latency is critical (agents add multiple round trips)
- The cost of multiple model calls is not justified

**Examples:**
- "Summarize this paragraph"
- "Convert this JSON to a Python dataclass"
- "Write a regex that matches email addresses"
- "Explain the difference between TCP and UDP"

### Use an agent when:

- The task requires multiple steps that depend on each other
- External data or tools are needed (APIs, databases, search)
- The task requires real-time or current information
- The approach may need to change based on intermediate results
- The task involves taking actions (not just generating text)

**Examples:**
- "Find the three most recent bugs in our issue tracker and draft a summary for the team standup"
- "Look up the customer's order, check the shipping status, and send them an update email"
- "Research competitors' pricing and build a comparison spreadsheet"
- "Review this pull request, run the tests, and suggest improvements"

### The decision flowchart

```
Does the task require external data or actions?
  |
  +-- No --> Can the model answer from its training data?
  |            |
  |            +-- Yes --> Use a simple prompt
  |            +-- No  --> Consider RAG (retrieval) first, then an agent
  |
  +-- Yes --> Is it a single tool call?
               |
               +-- Yes --> A simple function-calling setup may suffice
               +-- No  --> Use an agent with orchestration
```

### Cost and latency considerations

Every step in an agent loop involves a model call. A 5-step agent workflow means 5 or more calls to the model, plus tool execution time. This adds up:

- **Latency**: Each model call takes 1-10 seconds depending on the model and prompt size. A 5-step agent might take 15-30 seconds.
- **Cost**: Each model call costs tokens. Agent workflows can use 10-50x more tokens than a single prompt.
- **Reliability**: More steps means more chances for errors or hallucinations.

The engineering principle is the same as anywhere else: use the simplest approach that gets the job done.

---

## Real-World Examples

### Customer support agent

**Goal:** Handle customer inquiries end-to-end.

**How it works:**
1. Customer writes: "Where is my order #12345?"
2. Agent calls the order lookup tool with the order ID
3. Gets status: "Shipped, tracking number XYZ, estimated delivery March 20"
4. Agent formats a friendly response with the tracking link
5. If the customer asks to change the delivery address, the agent calls the address update tool

**Level:** 1-2 (tool use with some multi-step logic)

### Code assistant agent

**Goal:** Help developers write, debug, and improve code.

**How it works:**
1. Developer asks: "Why is this function returning null?"
2. Agent reads the relevant source files
3. Searches for related tests
4. Identifies the bug (missing null check on line 42)
5. Suggests a fix with code
6. Optionally runs the tests to verify the fix works

**Level:** 2 (multi-step reasoning with tool use)

### Research agent

**Goal:** Gather and synthesize information from multiple sources.

**How it works:**
1. User asks: "What are the pros and cons of server-side rendering in 2026?"
2. Agent searches for recent articles and benchmarks
3. Reads and extracts key points from multiple sources
4. Cross-references claims and checks for consistency
5. Produces a structured summary with citations

**Level:** 2 (search, read, synthesize across multiple steps)

### DevOps incident response agent

**Goal:** Help diagnose and resolve production incidents.

**How it works:**
1. Alert fires: "API latency spike on service-auth"
2. Agent queries monitoring dashboards for the last 30 minutes
3. Checks recent deployments for changes
4. Examines logs for error patterns
5. Correlates findings: "Latency spike started 5 minutes after deploy #789 which changed the auth token cache TTL"
6. Suggests rollback and drafts an incident report

**Level:** 2-3 (multi-step investigation, potentially coordinating with other agents)

---

## ELI5: what is an AI agent?

### Think of an agent like a really capable intern

Imagine you have a brand new intern on their first day. They are smart - they graduated top of their class - but they have never seen your codebase before.

**An LLM by itself is like this intern sitting in a room with no computer.** You can ask them questions and they will give you thoughtful answers based on what they learned in school. But they cannot look anything up, they cannot run any code, and they cannot send any emails. All they can do is talk.

**An agent is like this intern with a full desk setup.** They have a laptop, access to your internal tools, a browser, and your company Slack. Now when you ask them a question, they can:

- Look things up if they do not know the answer
- Try running code to test their ideas
- Check the documentation to make sure they are right
- Ask a colleague (another agent) for help
- Come back to you with a verified answer

The intern still makes mistakes sometimes - they are new, after all. But they can catch most of their errors because they can check their work. And if they get stuck, they know to ask for help rather than guessing.

**The key insight:** The intern's brain did not change. What changed was what they have access to and how they approach the work. That is exactly the difference between an LLM and an agent. Same brain, more capabilities, better process.

---

## How Google Cloud fits in

Google Cloud provides infrastructure for building and deploying agents through several services:

- **Vertex AI Agent Engine** - A managed platform for building, deploying, and managing AI agents in production. It handles orchestration, tool management, session state, and scaling so you can focus on agent logic rather than infrastructure.

- **Gemini Models** - The language models that serve as the "brain" of your agents, available in different sizes for different use cases.

- **Agent Development Kit (ADK)** - An open-source, code-first toolkit for building agents with features like multi-agent orchestration, built-in tool support, and easy deployment to Agent Engine.

We will use these tools throughout the course. For now, just know they exist.

> **Learn more:** [Vertex AI Agent Engine Overview](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview)

---

## Key takeaways

1. **An AI agent is a system that uses a language model to reason, tools to act, and an orchestration layer to manage the loop between thinking and doing.**

2. **LLM = brain. Agent = brain + hands + memory.** The model provides reasoning. Tools provide action. The orchestration layer provides control flow.

3. **Agents exist on a spectrum** from simple tool-using assistants (Level 1) to self-evolving systems (Level 4). Start at the lowest level that solves your problem.

4. **Not everything needs an agent.** If a single prompt gets the job done, use a single prompt. Add agent capabilities only when the task genuinely requires tools, multi-step reasoning, or real-world actions.

5. **The core loop is simple:** Receive goal -> Think about what to do -> Use a tool -> Observe the result -> Repeat until done.

---

## What is next?

In the next lesson, we will look under the hood at the "brain" of the agent - the language model. You will learn how LLMs process information, how different reasoning strategies affect agent performance, and how to pick the right model for the job.

[Next: Lesson 2 - How Agents Think: LLMs as the Reasoning Engine -->](../02-how-agents-think/README.md)
