# Урок 13: Создание первого агента с помощью ADK

## Введение

Вы освоили основы. Вы понимаете, что такое агенты, как они мыслят, как используют инструменты, как запоминают информацию и как оценивать эффективность их работы. Теперь пришло время создать своего собственного.

В этом уроке мы шаг за шагом рассмотрим создание практического агента с использованием комплекта разработки агентов Google (ADK). К концу урока вы поймете, как настроить проект, определить агента, назначить ему инструменты, протестировать его локально и даже создать небольшую команду агентов, работающих вместе.

Мы будем придерживаться концептуального подхода и дадим ссылку на официальный краткий старт для получения точных примеров кода — таким образом, у вас всегда будет актуальный синтаксис, а мы сможем сосредоточиться на действительно важных идеях.

---

## Что мы строим

Наша цель — создать практичного агента, способного:

- Отвечать на вопросы по теме с помощью поиска Google.
- Использовать созданный вами инструмент (например, для поиска информации о погоде или товарах).
- Запускать локально для быстрого тестирования и внесения изменений.

Представьте это как "привет, мир" для агентов — достаточно простое, чтобы понять его с первого раза, но достаточно реалистичное, чтобы показать, как всё взаимосвязано.

### Предварительные требования

Прежде чем начать, убедитесь, что у вас есть:

- Установлен **Python 3.9+**
- Установлен **ADK** (`pip install google-adk`)
- **Проект Google Cloud** с включенным API Gemini
- **Ключ API** или настроенные учетные данные приложения по умолчанию

> **Настройка:** Подробные инструкции по установке см. в официальном руководстве по настройке [ADK Getting Started](https://google.github.io/adk-docs/get-started/).

---

## ELI5: что мы на самом деле делаем?

Создание вашего первого агента похоже на сборку конструктора Lego. У вас есть базовая пластина (конструкция проекта), «мозг» минифигурки (языковая модель), несколько дополнительных инструментов (поиск, пользовательские функции) и инструкция по эксплуатации (системные инструкции), которая указывает минифигурке, как себя вести.

Каждая деталь соединяется определенным образом. Мозг решает, что делать. Инструменты позволяют ему это делать. Инструкции помогают сосредоточиться. А опорная плита удерживает все на месте, чтобы конструкция не развалилась.

Самое замечательное в том, что, как только вы поймете, как соединяются детали, вы сможете заменять их, добавлять новые или переставлять, чтобы построить совершенно другую конструкцию.

---

## Пошаговое руководство

Давайте рассмотрим процесс создания вашего первого агента. Мы обсудим основные понятия на каждом этапе и укажем на официальный краткий стартовый файл, где вы найдете точный код.

### Шаг 1: Настройка структуры проекта

ADK ожидает определенную структуру проекта. В самом простом случае вам понадобится папка для вашего агента, внутри которой будут находиться два файла:

```
my_first_agent/
    __init__.py
    agent.py
```

Имя папки становится именем модуля вашего агента. Файл `__init__.py` сообщает Python, что это пакет, и экспортирует ваш агент. В файле `agent.py` вы определяете самого агента.

Эта структура важна, потому что инструменты ADK (например, `adk web` и `adk eval`) обнаруживают вашего агента, ища именно такой шаблон. С самого начала поддерживайте её в чистоте и единообразии.

> **Совет:** Вы также можете использовать команду `adk create my_first_agent` для автоматического создания этой структуры.

### Шаг 2: определите своего агента.

Каждому агенту ADK необходимо как минимум три вещи:

1. **Имя** — уникальный идентификатор вашего агента.
2. **Модель** — какую модель Gemini использовать для рассуждений.
3. **Системные инструкции** — подсказка, которая сообщает агенту, кто он и как себя вести.

Вот как это выглядит концептуально:

```python
from google.adk.agents import Agent

my_agent = Agent(
    name="my_first_agent",
    model="gemini-2.5-flash",
    instruction="You are a helpful assistant that answers questions clearly and concisely.",
)
```

Параметр `model` определяет, какая модель Gemini будет обрабатывать логические рассуждения. Для обучения и прототипирования отличным выбором станет `gemini-2.5-flash` — она быстрая и экономичная. Для более сложных задач логического рассуждения можно перейти на `gemini-2.5-pro`.

Параметр `instruction` — это системная подсказка вашего агента. Здесь вы определяете его характеристики, возможности и ограничения. Как писать качественные инструкции, мы рассмотрим позже в этом уроке.

### Шаг 3: создайте пользовательский инструмент функций.

Инструменты — это то, что отличает оператора от чат-бота. Давайте назначим нашему оператору пользовательскую функцию, которую он сможет вызывать.

В ADK инструмент — это просто функция Python с понятной документацией. Документация важна, потому что ADK использует её, чтобы сообщить модели, что делает инструмент и когда его следует использовать.

```python
def get_weather(city: str) -> dict:
    """Получите актуальную погоду для заданного города.

    Args:
        city: The name of the city to get weather for.

    Returns:
        A dictionary with weather information.
    """
    # В реальном агенте это бы вызвало API погоды
    # Пока что возвращаем фиктивные данные
    return {
        "city": city,
        "temperature": "72F",
        "conditions": "Sunny",
    }
```

Ключевые моменты, на которые следует обратить внимание:

- **Type hints** (`city: str`, `-> dict`) помогите модели понять, какие параметры передавать и чего ожидать в ответ
- **The docstring** так модель узнает, что делает этот инструмент — напишите его так, как будто вы объясняете функцию коллеге
- **The function name** оно должен быть описательным — модель использует его, чтобы решить, когда вызывать инструмент

Затем вы прикрепляете инструмент к своему агенту:

```python
my_agent = Agent(
    name="my_first_agent",
    model="gemini-2.5-flash",
    instruction="You are a helpful assistant. Use the get_weather tool when asked about weather.",
    tools=[get_weather],
)
```

### Шаг 4: добавьте встроенный инструмент (поиск Google)

ADK поставляется с несколькими встроенными инструментами. Один из самых полезных — это функция поиска Google, которая позволяет вашему агенту искать актуальную информацию в интернете.

```python
from google.adk.tools import google_search

my_agent = Agent(
    name="my_first_agent",
    model="gemini-2.5-flash",
    instruction="You are a helpful assistant. Use search for current events and get_weather for weather.",
    tools=[get_weather, google_search],
)
```

Теперь ваш агент может одновременно искать информацию в интернете и проверять погоду. Модель выбирает инструмент в зависимости от вопроса пользователя. Спросите о новостях — и он выполнит поиск. Спросите о погоде — и он вызовет вашу пользовательскую функцию.

### Шаг 5: запуск и тестирование локально

ADK включает локальный сервер разработки, который предоставляет вам веб-интерфейс для взаимодействия с вашим агентом:

```bash
adk web
```

Это запускает локальный сервер (обычно по адресу `http://localhost:8000`) с интерфейсом чата. Вы можете:

- Отправлять сообщения своему агенту
- Видеть, какие инструменты он использует и почему
- Просматривать полную историю переписки
- Отлаживать проблемы в режиме реального времени

Вы также можете тестировать из командной строки:

```bash
adk run my_first_agent
```

Это самый быстрый цикл обратной связи. Вносите изменения, обновляйте, тестируйте. Повторяйте, пока агент не начнет вести себя так, как вам нужно.

### Шаг 6: оценка с помощью ADK eval`

Как только ваш агент заработает, вам нужно убедиться, что он продолжает работать при внесении изменений. ADK включает в себя фреймворк для оценки, предназначенный для этой цели:

```bash
adk eval my_first_agent eval_data.json
```

Оценка позволяет определять тестовые примеры — пары входных данных и ожидаемого поведения — и автоматически проверять, правильно ли ваш агент их обрабатывает. Это аналог модульного тестирования для агентов.

Мы подробно рассмотрели концепции оценки в уроке 9. Ключевая идея здесь — начать писать тестовые примеры как можно раньше, даже для вашего первого агента. Это убережет вас от регрессий в дальнейшем.

> **Full quickstart:** Полный код доступен по ссылке: [ADK Quickstart](https://google.github.io/adk-docs/get-started/quickstart/)

---

## Типы агентов в ADK

ADK предоставляет четыре типа агентов, каждый из которых предназначен для решения различных задач. Выбор правильного типа подобен выбору правильной структуры данных — он определяет все последующие действия.

### LlmAgent (по умолчанию)

Это тип агента, который вы будете использовать чаще всего. Он использует языковую модель для принятия решений о дальнейших действиях.

**Когда его использовать:**
- Задача требует рассуждений и оценки
- Агент должен решить, какие инструменты вызвать, исходя из контекста
- Взаимодействие с пользователем носит разговорный характер

**Как это работает:** Модель получает сообщение пользователя, доступные инструменты и историю разговора. Она решает, следует ли вызвать инструмент, задать уточняющий вопрос или ответить напрямую. Это цикл ReAct в действии.

```python
from google.adk.agents import Agent

researcher = Agent(
    name="researcher",
    model="gemini-2.5-flash",
    instruction="You research topics thoroughly using search.",
    tools=[google_search],
)
```

### Последовательный агент (шаги по порядку)

Последовательный агент запускает фиксированный список подагентов один за другим, как в конвейере.

**Когда его использовать:**
- Задача имеет четкие, упорядоченные этапы
- Каждый этап зависит от результата предыдущего
- Вам нужно предсказуемое, повторяемое выполнение

**Пример:** Конвейер создания контента, где один агент проводит исследование, следующий пишет черновик, а третий редактирует текст на предмет грамматики и стиля.

```python
from google.adk.agents import SequentialAgent

pipeline = SequentialAgent(
    name="content_pipeline",
    sub_agents=[researcher, writer, editor],
)
```

**Аналогия:** Представьте себе SequentialAgent как конвейер на заводе. Каждая станция выполняет одну задачу и передает результат следующей станции.

### Parallelagent (выполняет шаги одновременно)

ParallelAgent запускает несколько под-агентов одновременно и собирает их результаты.

**Когда его использовать:**
- У вас есть независимые подзадачи, которые не зависят друг от друга
- Скорость важна, и вы хотите сократить время выполнения
- Вам нужны несколько точек зрения на одни и те же входные данные

**Пример:** Оценка фрагмента кода путем одновременного запуска проверки безопасности, проверки производительности и проверки стиля.

```python
from google.adk.agents import ParallelAgent

review_team = ParallelAgent(
    name="code_review",
    sub_agents=[security_reviewer, perf_reviewer, style_reviewer],
)
```

**Аналогия:** Представьте ParallelAgent как командный мозговой штурм, где каждый одновременно работает над своей частью, а затем представляет свои результаты.

### Loopagent (повторять до завершения)

LoopAgent запускает своих подагентов в цикле до тех пор, пока не будет выполнено условие завершения.

**Когда его использовать:**
- Задача требует итеративного уточнения
- Вы хотите постоянно улучшать результат, пока он не достигнет порогового значения качества
- Количество итераций заранее неизвестно

**Пример:** Агент для написания текстов, который создает черновик контента, оценивает его по критериям и вносит правки до тех пор, пока оценка качества не превысит пороговое значение.

```python
from google.adk.agents import LoopAgent

refiner = LoopAgent(
    name="iterative_writer",
    sub_agents=[drafter, evaluator, reviser],
    max_iterations=5,
)
```

**Аналогия:** Представьте себе LoopAgent как цикл проверки кода — вы пишете, получаете обратную связь, редактируете и повторяете, пока рецензент не одобрит.

### Выбор подходящего типа агента

| Тип агента | Когда использовать | Пример |
|---|---|---|
| LlmAgent | Flexible reasoning needed | Chatbot, research assistant |
| SequentialAgent | Fixed pipeline of steps | ETL, content creation |
| ParallelAgent | Independent parallel tasks | Multi-reviewer systems |
| LoopAgent | Iterative refinement | Quality improvement loops |

Вы также можете комбинировать эти типы. SequentialAgent может содержать LlmAgent в качестве одного из своих шагов. LoopAgent может содержать ParallelAgent внутри себя. Эта возможность компоновки — одно из преимуществ ADK.

> **Learn more:** [ADK Agent Types](https://google.github.io/adk-docs/agents/)

---

## Building a multi-tool agent

Most real agents need more than one tool. Let us look at how to combine multiple capabilities.

### Combining search, code execution, and custom tools

```python
from google.adk.agents import Agent
from google.adk.tools import google_search

def look_up_product(product_id: str) -> dict:
    """Look up product details by ID.

    Args:
        product_id: The unique product identifier.

    Returns:
        Product details including name, price, and availability.
    """
    # Call your product database/API here
    return {"id": product_id, "name": "Widget Pro", "price": 29.99}

def calculate_discount(price: float, discount_percent: float) -> float:
    """Calculate the discounted price.

    Args:
        price: The original price.
        discount_percent: The discount percentage (e.g., 20 for 20%).

    Returns:
        The price after discount.
    """
    return price * (1 - discount_percent / 100)

shopping_agent = Agent(
    name="shopping_assistant",
    model="gemini-2.5-flash",
    instruction="""You are a shopping assistant. You can:
    - Search the web for product reviews and comparisons
    - Look up specific products in our catalog by ID
    - Calculate discounts on prices

    Always look up the product first before calculating discounts.""",
    tools=[google_search, look_up_product, calculate_discount],
)
```

The key to multi-tool agents is clear instruction about when to use each tool. Without guidance, the model might search the web when it should query your database, or vice versa.

### Tool design principles

When building tools for your agent, follow these guidelines:

1. **One tool, one job.** Each tool should do one thing well. Do not create a mega-tool that handles five different operations.

2. **Descriptive names and docstrings.** The model picks tools based on their names and descriptions. `get_order_status` is better than `fetch_data`.

3. **Clear parameter types.** Use type hints. The model needs to know whether to pass a string, number, or object.

4. **Graceful error handling.** Return helpful error messages instead of crashing. The model can often recover if it understands what went wrong.

5. **Deterministic when possible.** Tools that return consistent results for the same inputs are easier for the model to reason about.

---

## Building an agent team

Sometimes one agent cannot handle everything. You might need specialists - one agent for research, another for writing, a third for fact-checking. ADK lets you build agent teams with a root agent that delegates to sub-agents.

### The root agent pattern

```python
from google.adk.agents import Agent

# Specialist agents
researcher = Agent(
    name="researcher",
    model="gemini-2.5-flash",
    instruction="You research topics using web search. Return factual findings.",
    tools=[google_search],
)

writer = Agent(
    name="writer",
    model="gemini-2.5-flash",
    instruction="You write clear, engaging content based on research findings.",
)

fact_checker = Agent(
    name="fact_checker",
    model="gemini-2.5-flash",
    instruction="You verify claims by searching for supporting evidence.",
    tools=[google_search],
)

# Root agent that orchestrates
coordinator = Agent(
    name="content_team",
    model="gemini-2.5-pro",
    instruction="""You coordinate a content creation team. For any content request:
    1. Ask the researcher to gather information
    2. Ask the writer to create content based on the research
    3. Ask the fact_checker to verify key claims

    Delegate tasks to your team members and synthesize their work.""",
    sub_agents=[researcher, writer, fact_checker],
)
```

### When to use sub-agents vs. multiple tools

| Approach | Best For | Trade-offs |
|---|---|---|
| One agent, many tools | Tasks where a single reasoning chain works | Simpler, but the agent might struggle with too many tools |
| Multiple sub-agents | Tasks that benefit from specialization | More flexible, but adds coordination overhead |

**Rule of thumb:** If your single agent has more than 10-15 tools and starts getting confused about which to use, consider splitting into sub-agents with focused tool sets.

### Communication between agents

Sub-agents in ADK share a session state, which acts as a shared workspace. The root agent can pass context to sub-agents, and sub-agents can store results that other agents can access.

Think of it like a shared document in a team project. The coordinator writes the brief, the researcher adds findings, and the writer uses those findings to draft content.

---

## Tips for writing good system instructions

The system instruction (prompt) is the single most important factor in how your agent behaves. Here are practical guidelines.

### Be specific about the role

**Weak:**
```
You are a helpful assistant.
```

**Better:**
```
You are a customer support agent for Acme Corp. You help customers
with order tracking, returns, and product questions. You have access
to the order database and can look up orders by ID or email.
```

### Set clear boundaries

Tell the agent what it should and should not do:

```
You ONLY handle questions about orders, returns, and products.
For billing questions, tell the customer to contact billing@acme.com.
Never make promises about delivery dates unless the tracking system confirms them.
Never share internal pricing or cost information.
```

### Provide examples

Show the agent how you want it to behave:

```
When a customer asks about their order status, follow this pattern:
1. Ask for their order ID if they have not provided one
2. Look up the order using the get_order tool
3. Summarize the status in plain language
4. If the order is delayed, apologize and offer to escalate

Example:
Customer: "Where is my order?"
You: "I'd be happy to help track your order. Could you share your order ID? It should start with ORD- and you can find it in your confirmation email."
```

### Define the output format

If you want structured responses, say so:

```
Always respond in this format:
- Start with a one-sentence summary
- Provide details in bullet points
- End with a suggested next step
```

### Common instruction mistakes

| Mistake | Why It Is a Problem | Fix |
|---|---|---|
| Too vague ("be helpful") | The model has no specific guidance | Define the role, scope, and behavior |
| Too long (2000+ words) | Key instructions get lost in noise | Keep it focused, use structure |
| No tool guidance | The model guesses when to use tools | Explain when each tool is appropriate |
| No error handling | The agent does not know what to do when things fail | Add fallback instructions |
| No boundaries | The agent tries to handle everything | Define what is out of scope |

---

## Common mistakes beginners make

### 1. starting too complex

You do not need a multi-agent system with 10 tools on day one. Start with one agent and one tool. Get that working perfectly before adding complexity.

### 2. ignoring the system instruction

Many beginners focus on tools and code but write a one-line system instruction. The instruction is your primary lever for controlling agent behavior. Invest time in it.

### 3. not testing tool calls

Your agent is only as reliable as its tools. Test each tool function independently before wiring it into the agent. If `get_weather("London")` throws an exception, your agent will too.

### 4. forgetting to handle errors

Tools fail. APIs time out. Data is missing. Your agent needs instructions for what to do when things go wrong. Add error handling in both your tool code and your system instructions.

### 5. using the wrong model

Not every task needs the most powerful model. For simple routing and tool-calling, a lighter model like Flash works well and saves money. Reserve larger models for tasks that genuinely require complex reasoning.

### 6. skipping evaluation

If you do not have eval cases, you do not know whether your changes improve or break things. Write at least 5-10 test cases before you start iterating on prompts.

### 7. putting secrets in code

Never hardcode API keys or credentials in your agent code. Use environment variables or a secrets manager. This is standard software engineering practice, but it is easy to forget when prototyping.

---

## Putting it all together

Here is a mental model for the entire process of building an ADK agent:

```
1. Define the goal
   "What should this agent accomplish?"
        |
        v
2. Choose the agent type
   LlmAgent? Sequential? Parallel? Loop?
        |
        v
3. Write the system instruction
   Role, scope, boundaries, examples
        |
        v
4. Define the tools
   What actions does the agent need?
        |
        v
5. Wire it together
   Agent + model + instruction + tools
        |
        v
6. Test locally
   adk web / adk run
        |
        v
7. Write eval cases
   Input -> expected behavior
        |
        v
8. Iterate
   Improve instructions, add tools, refine
        |
        v
9. Deploy
   Agent Engine or your own infrastructure
```

Each step feeds the next. And steps 6-8 are a loop - you will go around multiple times before moving to step 9.

---

## Quick reference: ADK CLI commands

| Command | What It Does |
|---|---|
| `pip install google-adk` | Install ADK |
| `adk create <name>` | Scaffold a new agent project |
| `adk web` | Start the local dev server with web UI |
| `adk run <agent>` | Run an agent from the command line |
| `adk eval <agent> <data>` | Run evaluation cases against your agent |
| `adk deploy` | Deploy your agent to Agent Engine |

---

## Where to learn more

- **Getting started with ADK:** [https://google.github.io/adk-docs/get-started/](https://google.github.io/adk-docs/get-started/)
- **Full quickstart tutorial:** [https://google.github.io/adk-docs/get-started/quickstart/](https://google.github.io/adk-docs/get-started/quickstart/)
- **Agent types in depth:** [https://google.github.io/adk-docs/agents/](https://google.github.io/adk-docs/agents/)
- **Tools reference:** [https://google.github.io/adk-docs/tools/](https://google.github.io/adk-docs/tools/)

---

## Key takeaways

1. **An ADK agent needs three things:** a name, a model, and system instructions. Tools are optional but are what make agents genuinely useful.

2. **Start with LlmAgent.** It handles most use cases. Reach for SequentialAgent, ParallelAgent, or LoopAgent only when you have a clear structural reason.

3. **System instructions are your primary control lever.** Be specific about the role, set boundaries, provide examples, and include error handling guidance.

4. **Test early and often.** Use `adk web` for interactive testing and `adk eval` for automated regression checks.

5. **Build incrementally.** One agent, one tool, one eval case. Get each piece working before adding the next.

---

## What is next?

Now that you can build an agent, you need to understand how agents communicate with the wider world. In the next lesson, we will explore two important protocols - MCP and A2A - that let agents talk to tools and to each other using open standards.

[Next: Lesson 14 - Agent Protocols: MCP and A2A -->](../14-agent-protocols-mcp-and-a2a/README.md)
