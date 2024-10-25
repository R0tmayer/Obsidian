### Принципы REST API на основе [диссертации](https://translated.turbopages.org/proxy_u/en-ru.ru.2385d227-671ad9c2-b1dd4128-74722d776562/https/ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm#sec_5_1)

#### 1. Client-Server
Тут речь о SoC принципе (Separation of concerns) - отделяем UI от хранения данных. Это даёт возможность слать запроса с клиента на любые серверы и платформы. К тому же UI никак не связан с серверными компонентами, что повышает масштабируемость серверных компонентов.

#### 2. Stateless
Ты не можешь сказать "я отправляю неполный запрос, остальную инфо"