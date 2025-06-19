# Проект по дообучению GPT-2 (Fine-Tuning)

Этот проект представляет собой шаблон для тонкой настройки модели GPT‑2 из библиотеки `transformers` от Hugging Face на собственном корпусе текстов.
Он включает подготовку данных, обучение модели, логирование и сохранение контрольных точек — всё организовано в понятной и масштабируемой структуре. 🚀

---

## 📚 Обзор проекта

Цель — дообучить предварительно обученную модель GPT‑2 на пользовательском датасете в формате JSON Lines (`my_corpus.jsonl`).  
Скрипт `train.py` автоматически обрабатывает данные, выполняет токенизацию, обучение и сохраняет модель и логи для анализа.

---

## 📂 Структура проекта

```
gpt2-finetune-custom/
├── data/
│   └── my_corpus.jsonl       # Кастомный датасет в формате JSONL
├── train.py                  # Скрипт обучения GPT-2
├── logs/                     # Логи обучения (для TensorBoard)
├── model/                    # Сохранённые чекпойнты модели
├── README.md                 # Документация
└── requirements.txt          # Зависимости
```

---

## 🛠️ Установка

### ✅ Требования

- Python 3.8 или выше
- Зависимости указаны в `requirements.txt`

### 🔧 Шаги установки

```bash
git clone https://github.com/MirannaWolf/gpt2-finetune-custom.git
cd gpt2-finetune-custom
```

Создание виртуального окружения (по желанию):

```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
```

Установка зависимостей:

```bash
pip install -r requirements.txt
```

---

## 📖 Использование

### 1. Подготовка датасета

Файл должен быть в формате JSONL (`data/my_corpus.jsonl`) — каждая строка содержит JSON-объект с полем `"text"`:

```json
{"text": "Once upon a time..."}
{"text": "The sun sets slowly behind the mountain"}
```

📝 Убедись, что:
- Кодировка файла: UTF-8
- Файл находится в директории `data/`

---

### 2. Запуск обучения

```bash
python train.py
```

Произойдёт следующее:
- Загрузится и токенизируется датасет
- Инициализируется модель GPT-2
- Модель обучится (по умолчанию 3 эпохи)
- Результаты сохранятся в `model/`, логи — в `logs/`

---

## ⚙️ Конфигурация обучения

| Параметр                    | Описание                                        | Значение по умолчанию |
|-----------------------------|-------------------------------------------------|------------------------|
| per_device_train_batch_size | Размер батча на устройство (GPU/CPU)           | 2                      |
| num_train_epochs            | Кол-во эпох обучения                            | 3                      |
| save_steps                  | Сохранять чекпойнт каждые N шагов              | 500                    |
| logging_steps               | Записывать логи каждые N шагов                 | 100                    |
| max_length                  | Макс. длина токенов при токенизации            | 512                    |
| save_total_limit            | Максимум сохраняемых чекпойнтов                | 2                      |

---

## 📝 Пример данных

```json
{"text": "Once upon a time when I can finally give my children what I love most and I am sure they will love me too."}
{"text": "The sun sets slowly behind the mountain, and suddenly the moon moon rises out of the mountain. The sun rises from the ridge of the mountain. The sun rises from above the mountain, and the sun rises from below. "}
```

После обучения модель будет генерировать текст в похожем стиле.

---

## ℹ️ Заметки

- 🌐 Требуется подключение к интернету для загрузки модели GPT‑2.
- ⚡ Рекомендуется использовать GPU, но возможно обучение и на CPU.
- 📊 Для полезного обучения желательно использовать корпус от сотен до тысяч строк.
- 🧪 Убедись, что установлен `tensorboard`, если ты хочешь отслеживать прогресс.
- 💾 Параметр `save_total_limit` помогает избежать переполнения диска.

---
