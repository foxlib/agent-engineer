# Инженер по разработке агентов - курс для инженеров-программистов

Изучите основы работы агентов искусственного интеллекта и научитесь создавать их с помощью Google Cloud AI.

## Для кого предназначен этот курс?

Для инженеров-программистов, которые хотят понять, что такое агенты искусственного интеллекта, как они работают и как их создавать. Предыдущий опыт в области ИИ/машинного обучения не требуется — достаточно любознательности и некоторых знаний языка Python.

## Обзор курса

Этот курс состоит из трёх частей:

**Часть 1: Основы (101)** - изучите ключевые концепции, лежащие в основе агентов искусственного интеллекта. Эти уроки не привязаны к конкретной платформе и направлены на формирование вашей ментальной модели.

**Часть 2: Создание и развертывание (201)** - Применение этих основ на практике с использованием Google Cloud AI, Vertex AI и Agent Development Kit (ADK).

**Часть 3: Углублённое изучение (301)** - более подробно рассмотрите конкретные темы, имеющие значение для разработки агентов в реальных условиях.

## Уроки

### Часть 1: Основы

| # | Урок | Чему вы научитесь |
|---|--------|-------------------|
| 01 | [Что такое ИИ-агенты?](./01-what-are-ai-agents/README.md) | Общая картина — что такое агенты, почему они важны и когда их использовать |
| 02 | [Как думают агенты](./02-how-agents-think/README.md) | LLM как механизм рассуждений — как модели планируют, принимают решения и генерируют |
| 03 | [Инструменты — помощь агентам](./03-tools-giving-agents-hands/README.md) | Вызов функций, проектирование инструментов и связь агентов с реальным миром |
| 04 | [Шаблоны проектирования агентов](./04-agentic-design-patterns/README.md) | ReAct, рефлексия, планирование и другие основные шаблоны |
| 05 | [Память и контекст](./05-memory-and-context/README.md) | Как агенты запоминают информацию — сессии, контекстные окна и долговременная память |
| 06 | [Планирование и рассуждение](./06-planning-and-reasoning/README.md) | Как агенты разбивают сложные задачи и принимают решения |
| 07 | [Многоагентные системы](./07-multi-agent-systems/README.md) | Когда одного агента недостаточно — координация, делегирование и командная работа |
| 08 | [Агентный RAG](./08-agentic-rag/README.md) | Выход за рамки базового поиска — агенты, которые ищут, оценивают и уточняют |
| 09 | [Оценка и тестирование агентов](./09-evaluating-and-testing-agents/README.md) | Как узнать, действительно ли ваш агент работает — метрики, оценки и наблюдаемость |
| 10 | [Ограничения и безопасность](./10-guardrails-and-safety/README.md) | Обеспечение доверия к агентам — безопасность, согласованность и ответственный ИИ |

### Part 2: building and shipping

| # | Lesson | What you will learn |
|---|--------|-------------------|
| 11 | [From prototype to production](./11-from-prototype-to-production/README.md) | The journey from demo to deployed - CI/CD, rollout, and operations |
| 12 | [Getting started with Vertex AI and ADK](./12-getting-started-with-vertex-and-adk/README.md) | The Google Cloud AI stack for agents - what is available and how it fits together |
| 13 | [Building your first agent](./13-building-your-first-agent/README.md) | Hands-on - build a working agent with ADK step by step |
| 14 | [Agent protocols - MCP and A2A](./14-agent-protocols-mcp-and-a2a/README.md) | How agents talk to tools and to each other using open standards |

### Part 3: deep dives

| # | Lesson | What you will learn |
|---|--------|-------------------|
| 15 | [AGENTS.md](./15-agents-md/README.md) | Giving AI coding agents context about your project with a standard config file |
| 16 | [MCP deep dive](./16-mcp-deep-dive/README.md) | How MCP works under the hood, MCP vs. CLI tools, and security considerations |
| 17 | [Agent skills](./17-agent-skills/README.md) | Packaging reusable domain expertise as portable skill modules |
| 18 | [Orchestrators](./18-orchestrators/README.md) | Managing agent control flow - patterns, frameworks, and best practices |
| 19 | [Where to go from here](./19-where-to-go-from-here/README.md) | Resources, codelabs, community, and next steps |

## How to use this course

- **Read in order** if you are new to agents. Each lesson builds on the previous one.
- **Jump around** if you already know the basics. Each lesson is self-contained enough to read on its own.
- **Follow the links** to official docs, codelabs, and tutorials for hands-on practice. We intentionally link out to maintained resources rather than duplicating API docs or code samples that go stale.

## Philosophy

This course follows a few principles:

- **Analogies first.** We use everyday comparisons to explain complex concepts before diving into technical details.
- **Fundamentals over frameworks.** Understand the "why" before the "how." Frameworks change, but the core ideas stick around.
- **Link, don't duplicate.** For API references, code samples, and setup instructions, we point to official Google Cloud docs and codelabs. This keeps our content focused on concepts and ensures you always see up-to-date information.
- **Honest about trade-offs.** Every architectural choice has costs. We try to show both sides.

## Prerequisites

- Basic Python knowledge (functions, classes, HTTP requests)
- A Google Cloud account ([free trial available](https://cloud.google.com/free))
- Familiarity with REST APIs and JSON

## Additional resources

- [Google Cloud AI documentation](https://cloud.google.com/ai)
- [Vertex AI documentation](https://cloud.google.com/vertex-ai/docs)
- [Agent Development Kit (ADK) documentation](https://google.github.io/adk-docs/)
- [Google Cloud AI codelabs](https://codelabs.developers.google.com/?cat=AI)
- [Gemini API documentation](https://ai.google.dev/docs)

## Contributing

Found a typo? Have a suggestion? PRs and issues are welcome. See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

## License

This project is licensed under the Apache 2.0 License - see the [LICENSE](./LICENSE) file for details.
