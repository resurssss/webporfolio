---
title: "Работа с Webpack"
date: 2026-04-24
description: "Описание"
tags: ["http", "api"]
type: "portfolio"               
categories: ["портфолио"]
---
### 1. Инициализация и установка зависимостей

- Создание папки webpack
- Команда `npm init -y` - инициализация проекта
- Команда `npm i luxon` - установка зависимостей luxon
### 2. Установка девелоперских зависимостей

Установим девелоперские зависимости, которые не используются для выполнения проекта: `npm i -D webpack webpack-cli serve`
### 3. Создание файла index.js

Базовый функционал для корректной работы:
```
const { DateTime } = require('luxon'); 
setInterval(() => { 
hh.textContent = DateTime .local() .setLocale('ru') .toFormat('dd.LL.y HH:mm:ss'); }, 1000);
```
### 4. Сборка проекта

Сборка проекта осуществляется командой `npx webpack`
Результат сборки:
![](https://resurssss.github.io/webporfolio/images/4.png)

### 5. Создаем веб-страницу index.html

Index.html:
```
<!DOCTYPE html>
<html>
<head>
    <title>Часы с Luxon</title>
</head>
<body>
    <h1 id="hh"></h1>
    <script src="./dist/main.js"></script>
</body>
</html>
```

### 6. Запуск сервера

Выполним запуск сервера с помощью команды `npx serve .` 
В командной строке отобразится:
![](https://resurssss.github.io/webporfolio/images/5.png)

По адресу http://localhost:3923 будет доступен наш проект

### 7. Реализация Bootstrap

Сделаем адаптивное отображение и красивый внешний вид для нашего времени.

Файл `index.html`:
```
const { DateTime } = require('luxon');

// Создаём элемент, если его нет
let hh = document.getElementById('hh');

if (!hh) {
    hh = document.createElement('h1');
    hh.id = 'hh';
    hh.style.position = 'absolute';
    hh.style.opacity = '0';
    hh.style.pointerEvents = 'none';
    document.body.appendChild(hh);
}


setInterval(() => {
    const hhElement = document.getElementById('hh');
    if (hhElement) {
        hhElement.textContent = DateTime
            .local()
            .setLocale('ru')
            .toFormat('dd.LL.y HH:mm:ss');
    }
}, 1000);
```

Файл `index.html`
```
<!DOCTYPE html>
<html lang="ru">
<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Часы с Luxon</title>

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

    <style>

        * {
            margin: 0;

            padding: 0;

            box-sizing: border-box;
        }

  

        body {
            min-height: 100vh;

            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);

            font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
        }


        .fullscreen {
            min-height: 100vh;

            display: flex;

            align-items: center;

            justify-content: center;

            text-align: center;

            padding: 20px;
        }

  

        .glass-badge {
            background: rgba(255, 255, 255, 0.15);

            backdrop-filter: blur(12px);

            border-radius: 60px;

            padding: 8px 28px;

            display: inline-block;

            margin-bottom: 40px;

            border: 1px solid rgba(255, 255, 255, 0.3);

            box-shadow: 0 8px 20px rgba(0,0,0,0.2);

            font-size: 1.2rem;

            font-weight: 500;

            letter-spacing: 2px;

            color: #fff;

            text-transform: uppercase;

            font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
        }

  

        .glass-badge span {
            margin-right: 8px;

            font-size: 1.3rem;
        }

  

    
        .big-time {

            font-size: clamp(4rem, 18vw, 12rem);

            font-weight: 700;

            color: #ffffff;

            text-shadow: 4px 4px 12px rgba(0, 0, 0, 0.3);

            letter-spacing: 6px;

            line-height: 1.1;

            margin-bottom: 20px;

            font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;

            font-variant-numeric: tabular-nums;

        }

  
        .date-under {
            font-size: clamp(1.2rem, 5vw, 2rem);

            font-weight: 500;

            color: rgba(255, 255, 255, 0.92);

            background: rgba(0, 0, 0, 0.2);

            display: inline-block;

            padding: 8px 24px;

            border-radius: 40px;

            backdrop-filter: blur(4px);

            letter-spacing: 1.5px;

            font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
        }


        @keyframes gentleFade {
            0% { opacity: 0.9; transform: scale(1);}

            50% { opacity: 1; transform: scale(1.01);}

            100% { opacity: 0.9; transform: scale(1);}
        }

  
        .big-time, .date-under {
            animation: gentleFade 0.8s ease-in-out;
        }

    </style>

</head>

<body>

    <div class="fullscreen">

        <div>

            <div class="glass-badge">

                ТЕКУЩЕЕ ВРЕМЯ

            </div>

            <div class="big-time" id="displayTime">--:--:--</div>

            <div class="date-under" id="displayDate">--.--.----</div>

        </div>

    </div>

  

    <script src="./dist/main.js"></script>


    <script>

        function updateDisplay() {

            const hh = document.getElementById('hh');

            const timeElem = document.getElementById('displayTime');

            const dateElem = document.getElementById('displayDate');

            if (hh && hh.textContent) {

                const full = hh.textContent.trim();

                const parts = full.split(' ');

                if (parts.length === 2) {

                    timeElem.textContent = parts[1];

                    dateElem.textContent = parts[0];
                }
            }
        }

        setInterval(updateDisplay, 200);

        setTimeout(updateDisplay, 100);

    </script>
</body>
</html>
```

Итоговый вид нашего проекта:
![](https://resurssss.github.io/webporfolio/images/6.png)
