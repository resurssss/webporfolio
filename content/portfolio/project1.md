---
title: "HTTP: Работа с GET и POST запросами"
date: 2026-04-05
description: "Описание"
tags: ["http", "api"]
type: "portfolio"                    # ← без знака =, только двоеточие
categories: ["портфолио"]
---
### Используемые инструменты:

| Инструмент | Назначение                          |
| ---------- | ----------------------------------- |
| Ncat       | Сетевые подключения (аналог netcat) |
| cURL       | HTTP-запросы из командной строки    |
| Postman    | GUI-тестирование API                |
### 1. GET, POST запросы на сервер с помощью netcat

#### GET-запрос

Получаем информацию с сайта со случайными фотографиями уток. Сервер возвращает код 200 OK, значит, всё прошло успешно.

```
C:\Users\Serg>ncat --ssl random-d.uk 443
GET /api/v2/random HTTP/1.1
Host: random-d.uk
Accept: application/json

HTTP/1.1 200 OK
Date: Sun, 05 Apr 2026 19:00:14 GMT
Content-Type: application/json
Content-Length: 76
Connection: keep-alive
Server: cloudflare
cf-cache-status: DYNAMIC
Nel: {"report_to":"cf-nel","success_fraction":0.0,"max_age":604800}
Report-To: {"group":"cf-nel","max_age":604800,"endpoints":[{"url":"https://a.nel.cloudflare.com/report/v4?s=yTd7eor5dL0Bci%2B8Z4PYiERt%2BKCo3f0ZOiynp3BR1xT4i4%2B26KYHhCIU89g5FDZWjhPCF5%2BwJZPdhiDvA7H1XWLOdcua9h2Rm2nE6G0wsPySfgxeIELnjWmcGdMKYw%3D%3D"}]}
CF-RAY: 9e7acb5e3ca15318-ARN
alt-svc: h3=":443"; ma=86400

{"message":"Powered by random-d.uk","url":"http://random-d.uk/api/347.JPG"}
```

#### POST-запрос

Вводим POST-запрос на сайт http://jsonplaceholder.typicode.com, указываем поля {"name":"Mark","job":"developer"}. Сервер возвращает код 201 OK, который означает создание пользователя.

```
C:\Users\Serg>ncat jsonplaceholder.typicode.com 80
POST /posts HTTP/1.1
Host: jsonplaceholder.typicode.com
Content-Type: application/json
Content-Length: 36

{"name":"Mark","job":"developer"}

HTTP/1.1 201 Created
Date: Sun, 05 Apr 2026 19:08:36 GMT
Content-Type: application/json; charset=utf-8
Content-Length: 55
Connection: keep-alive
Access-Control-Allow-Credentials: true
Access-Control-Expose-Headers: Location
Cache-Control: no-cache
Etag: W/"37-aJ+6n6a0PIHavHqdUxNax9Pbdrk"
Expires: -1
Location: http://jsonplaceholder.typicode.com/posts/101
Nel: {"report_to":"heroku-nel","response_headers":["Via"],"max_age":3600,"success_fraction":0.01,"failure_fraction":0.1}
Pragma: no-cache
Report-To: {"group":"heroku-nel","endpoints":[{"url":"https://nel.heroku.com/reports?s=MBOeTT5TGOSftAQMnJaNCiZjLE1jP9Wox7E5uyb682M%3D\u0026sid=e11707d5-02a7-43ef-b45e-2cf4d2036f7d\u0026ts=1775416116"}],"max_age":3600}
Reporting-Endpoints: heroku-nel="https://nel.heroku.com/reports?s=MBOeTT5TGOSftAQMnJaNCiZjLE1jP9Wox7E5uyb682M%3D&sid=e11707d5-02a7-43ef-b45e-2cf4d2036f7d&ts=1775416116"
Server: cloudflare
Vary: Origin, X-HTTP-Method-Override, Accept-Encoding
Via: 1.1 heroku-router
X-Content-Type-Options: nosniff
X-Powered-By: Express
X-Ratelimit-Limit: 1000
X-Ratelimit-Remaining: 999
X-Ratelimit-Reset: 1775416121
cf-cache-status: DYNAMIC
Server-Timing: cfCacheStatus;desc="DYNAMIC"
Server-Timing: cfEdge;dur=826,cfOrigin;dur=222
CF-RAY: 9e7ad7a08a0e4e46-ARN
alt-svc: h3=":443"; ma=86400

{
  "name": "Mark",
  "job": "developer",
  "id": 101
}
```

### 2. Запросы через cURL

#### Get-запрос
```
C:\Users\Serg>curl http://httpbin.org/get
{
  "args": {},
  "headers": {
    "Accept": "*/*",
    "Host": "httpbin.org",
    "User-Agent": "curl/8.13.0",
    "X-Amzn-Trace-Id": "Root=1-69d2a35d-780f491a33e5df3f44877b36"
  },
  "origin": "92.62.58.177",
  "url": "http://httpbin.org/get"
}
```

#### Post-запрос
```
C:\Users\Serg>curl -X POST http://httpbin.org/post -H "Content-Type: application/json" -d "{\"fact\":\"Cats sleep 70% of lives\"}"
{
  "args": {},
  "data": "{\"fact\":\"Cats sleep 70% of lives\"}",
  "files": {},
  "form": {},
  "headers": {
    "Accept": "*/*",
    "Content-Length": "34",
    "Content-Type": "application/json",
    "Host": "httpbin.org",
    "User-Agent": "curl/8.13.0",
    "X-Amzn-Trace-Id": "Root=1-69d2a38a-181e36cb0a7de6a12f9ec117"
  },
  "json": {
    "fact": "Cats sleep 70% of lives"
  },
  "origin": "92.62.58.177",
  "url": "http://httpbin.org/post"
}
```

### 3. Get-запрос для получения курса валют в Postman

Установка временного промежутка через параметры date_req1, date_req2: 20.10.2006 - 20.10.2007. Установка валюты через параметр VAL_NM_RQ: R01239 (Евро)

![](https://resurssss.github.io/webporfolio/images/1.png)

##### Ответ сервера:

![](https://resurssss.github.io/webporfolio/images/2.png)
....
![](https://resurssss.github.io/webporfolio/images/3.png)
Таким образом, мы получили сведения о том, как менялся курс евро за период 20.10.2006 - 20.10.2007.
