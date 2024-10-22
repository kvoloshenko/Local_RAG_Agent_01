# Локальный RAG (Retrieval-Augmented Generation) и Агенты  


## 1. Установить Ollama
https://ollama.com/download/windows

см. подробнее в этой публикации: https://t.me/AiExp01/81

## 2. Установить llama3.2
ollama pull llama3.2:3b-instruct-fp16 

## 3. Проверяем доступность локальной модели

Запускать модуль `01_Simple_Request_Local_Model.py`

Ключевые моменты:
- Модуль использует `loguru` для управления логированием, включая сохранение логов в файлы с ротацией и сжатием 
по мере роста файла.
- Основная функция в модуле, `get_model_response`, получает тему запроса и возвращает ответ, сгенерированный 
языковой моделью.
- Использует мини-промпт в формате, позволяющим задавать контекст и особенности ответа модели, что позволяет 
контролировать длину и форму ответа.
- Программа импортирует и использует класс `ChatOllama` для работы с конкретной моделью LLM.

## 4. Простой RAG для pdf файлов
Поместить в папку Python\pdf один или несколько pdf фалов с текстовым слоем.

Запускать модуль `02_Simple_RAG_PDF.py`

Этот код импортирует необходимые модули, конфигурирует логирование, и инициализирует процесс обработки знаний 
через векторные поиски и языковую модель. 

Основной функционал состоит из трех функций: 
* `get_index_db()` для работы с векторной Базой-Знаний, 

* `get_message_content()` для извлечения релевантных данных,

* `get_model_response()` для формирования ответа от модели.

## 5. Локальный RAG с агентами на LLaMA3
![](Local_RAG_Agent.png)

Запускать модуль `03_Local_RAG_Agent.py`

Этот код содержит многие элементы связанные с обработкой естественного языка, 
от извлечения и обработки документов до оценки релевантности и генерирования ответов. 
Комментарии помогут понять предназначение каждого блока кода, а также увидеть, 
как взаимодействуют между собой различные компоненты модуля.

Используется объединение подходов в агентский RAG:

* **Маршрутизация**: Адаптивный RAG. Направление вопросов к различным поисковым подходам

* **Возврат**: Корректирующий RAG. Возврат к веб-поиску, если документы не соответствуют запросу

* **Самокоррекция**: Самокоррекция: Самокоррекция RAG. Исправление ответов, содержащих галлюцинации или не отвечающих на вопрос

![](graph_image.png)

Для Web поиска используется поисковая систему Tavily, оптимизированную для LLM и RAG.
Необходимо создать свой аккаунт на https://tavily.com/
Сформировать свое значение TAVILY_API_KEY и записать его в файл `.env`, см. пример в файле `env_example.txt`

Использованные материалы:

* Статья "Local RAG agent with LLaMA3" https://langchain-ai.github.io/langgraph/tutorials/rag/langgraph_adaptive_rag_local/

* Видео (English 31 минута) Reliable, fully local RAG agents with LLaMA3.2-3b https://www.youtube.com/watch?v=bq1Plo2RhYI