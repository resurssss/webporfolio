---
title: "Webpack & Bootstrap"
date: 2026-05-14
description: "Описание"
tags: ["http", "api"]
type: "portfolio"               
categories: ["портфолио"]
---
### 1. Добавление кнопки

- Разделение на колонки 2-8-2 
- Кнопка "Показать время" во второй колонке
```
<div class="container-fluid h-100">          
        <div class="row min-vh-100">             
            <div class="col-2">
            </div>
            <div class="col-8 p-0">               
                <div class="fullscreen">
                    <div style="width: 100%;">
                        <button class="btn1" data-bs-toggle="modal" data-bs-target="#formModal" >
                            Показать время
                        </button>
                    </div>
                </div>
            </div>
            <div class="col-2">
            </div>
        </div>
```

### 2. Добавление окна со временем

- Заголовок с именем
- Кнопка "Закрыть" и значок-крестик
- Вывод времени
```
    <div class="modal fade" id="formModal" tabindex="-1">
        <div class="modal-dialog modal-dialog-centered">
            <div class="modal-content bg-dark text-white">
                <div class="modal-header">
                    <h5>Выполнила: Любовь Ерофеева</h5>
                    <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal" aria-label="Закрыть"></button>
                </div>
                <div class="modal-body text-center py-5">
                    <div id="displayTime" class="big-time">--:--:--</div>
                    <div id="displayDate" class="date-under">--.--.----</div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Закрыть</button>
                </div>
            </div>
        </div>
    </div>
```
### 3. Добавление стилей для кнопки, модального окна и фона
```
    <style>
    * {
        font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
    }
    
    .btn1 {
        color: #fff;
        font-size: 2rem;
        padding: 15px 30px;
        border: 2px solid #798;
        background: rgb(192, 38, 15);
        border-radius: 10px;
        cursor: pointer;
        width: 100%;
    }
    
    .fullscreen {
        min-height: 100vh;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    
    body {
        margin: 0;
        padding: 0;
    }
    
    .col-8 {
        padding: 0;
    }
    
    .big-time {
        font-size: clamp(2rem, 6vw, 4rem);
        font-weight: bold;
        font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
        font-variant-numeric: tabular-nums;
    }
    
    .date-under {
        font-size: 1.2rem;
        margin-top: 15px;
        font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
    }
    
    .modal-header h5 {
        font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
    }
    </style>
```

### 4. Сборка проекта

Сборка проекта осуществляется командой `npx webpack`
Результат сборки:
![](https://resurssss.github.io/webporfolio/images/8.PNG)
![](https://resurssss.github.io/webporfolio/images/9.PNG)
