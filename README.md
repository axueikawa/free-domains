<div align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://socialify.git.ci/tarampampam/free-domains/image?description=1&font=Raleway&forks=1&issues=1&owner=0&pulls=1&pattern=Solid&stargazers=1&theme=Dark">
    <img src="https://socialify.git.ci/tarampampam/free-domains/image?description=1&font=Raleway&forks=1&issues=1&owner=0&pulls=1&pattern=Solid&stargazers=1&theme=Light">
  </picture>
  <br/>
  <br/>

[![Tests Status][badge-tests]][actions]
[![Deploy Status][badge-deploy]][deploy]
</div>

Бесплатные поддомены для личных сайтов, проектов с открытым исходным кодом и многого другого. Вот список поддерживаемых доменных имен:

|              Domain name              |                         Features                          |
|:-------------------------------------:|:---------------------------------------------------------:|
| ⚡ [`*.is-an.app`](https://is-an.app/) | ![cf][badge-cf] ![dnssec][badge-dnssec] ![ssl][badge-ssl] |
|             ⚡ `*.1bt.uk`              |          ![cf][badge-cf] ![dnssec][badge-dnssec]          |

> Подстановочные знаки (например, `*.foo.is-an.app`) тоже поддерживаются, но причина их регистрации должна быть предельно ясной и подробно описанной.

[badge-cf]:https://shields.io/badge/%20-cloudflare-blue?logo=cloudflare&style=plastic?cacheSeconds=3600
[badge-dnssec]:https://shields.io/badge/%20-DNSSEC-blue?logo=moleculer&logoColor=white&style=plastic?cacheSeconds=3600
[badge-ssl]:https://shields.io/badge/SSL-Required-blue?style=plastic?cacheSeconds=3600

## Почему?

В первую очередь хочу ответить на один важный вопрос - "Почему вы раздаете домены бесплатно?". Потому что иногда мне нужны домены для моих любимых проектов, и вместо того, чтобы каждый раз покупать новые домены, я решил купить по одному для всех и использовать поддомены. И почему бы не поделиться ими с сообществом?

## Настройки доменов

|                                   Option                                   |       `*.is-an.app`       |        `*.1bt.uk`         |
|:--------------------------------------------------------------------------:|:-------------------------:|:-------------------------:|
|                              [DNSSEC][dnssec]                              |             ✅             |             ✅             |
|                                   Email                                    |             ❌             |             ❌             |
|                                 SSL/TLS *                                  |     [Full][ssl-full]      |   [Flexible][ssl-flex]    |
|                             Always Use HTTPS *                             |             ✅             |             ❌             |
|                   HTTP Strict Transport Security (HSTS)                    |             ✅             |             ❌             |
|                           Minimum TLS Version *                            |          TLS 1.2          |          TLS 1.2          |
|                    Opportunistic Encryption, TLS 1.3 *                     |             ✅             |             ✅             |
|                      WAF (Web Application Firewall) *                      | ✅ (Medium Security Level) | ✅ (Medium Security Level) |
|                         Browser Integrity Check *                          |             ✅             |             ✅             |
|            [Caching Level][caching-levels], Browser Cache TTL *            |     Standard, 4 hours     |     Standard, 4 hours     |
|                      [Crawler Hints][crawler-hints] *                      |             ✅             |             ✅             |
| [HTTP/2][http2], [HTTP/2 to Origin][http2-to-origin], HTTP/3 (with QUIC) * |             ✅             |             ✅             |
|                   [0-RTT Connection Resumption][0rtt] *                    |             ✅             |             ✅             |
|                         [gRPC][grpc], WebSockets *                         |             ✅             |             ✅             |
|                        [Pseudo IPv4][pseudo-ipv4] *                        |        Add header         |        Add header         |
|               IP Geolocation (HTTP header `CF-IPCountry`) *                |             ✅             |             ✅             |
|                           Maximum Upload Size *                            |          100 MB           |          100 MB           |

> `*` Доступно только при включенном проксировании ("proxy": true).

[dnssec]:https://developers.cloudflare.com/dns/additional-options/dnssec
[ssl-full]:https://developers.cloudflare.com/ssl/origin-configuration/ssl-modes/full/
[ssl-flex]:https://developers.cloudflare.com/ssl/origin-configuration/ssl-modes/flexible/
[caching-levels]:https://developers.cloudflare.com/cache/how-to/set-caching-levels
[crawler-hints]:https://blog.cloudflare.com/crawler-hints-how-cloudflare-is-reducing-the-environmental-impact-of-web-searches/
[http2]:https://www.cloudflare.com/website-optimization/http2/what-is-http2/
[http2-to-origin]:https://developers.cloudflare.com/cache/how-to/enable-http2-to-origin
[0rtt]:https://developers.cloudflare.com/fundamentals/network/0-rtt-connection-resumption/
[grpc]:https://support.cloudflare.com/hc/en-us/articles/360050483011
[pseudo-ipv4]:https://support.cloudflare.com/hc/en-us/articles/229666767

# Как получить?

1. Пометьте и [fork](https://github.com/tarampampam/free-domains/fork) этот репозиторий (следуйте [этому руководству](https://github.com/firstcontributions/first-contributions), если вы не не знаю, как сделать вклад)
2. Добавьте новый файл с именем `<your-subdomain-name>.<root-domain>.json` в папку `./domains`, чтобы зарегистрировать субдомен `<your-subdomain-name>`
3. Отредактируйте его (ниже приведен только **пример**, предоставьте **действительный** файл JSON с вашими потребностями, формат очень строгий; формат вы можете [проверить здесь](https://jsonlint.com/)):

```json
{
  "$schema": "../schemas/domain.schema.json",
  "description": "<describe your project in this field>",
  "domain": "<is-an.app or 1bt.uk - select one>",
  "subdomain": "<your subdomain name>",
  "owner": {
    "repo": "<https://URL/to/the/repository/with/subdomain/content/sources>",
    "email": "<your-public@email.address>"
  },
  "record": {
    "CNAME": "<cname-domain>",
    "TXT": ["list", "of", "required", "txt", "records"],
    "A": ["list", "of", "IPv4", "addresses", "like", "a", "127.0.0.1"],
    "AAAA": ["list", "of", "IPv6", "addresses", "like", "a", "::1"],
    "NS": ["list", "of", "nameservers"]
  },
  "proxy": false // отключить прокси CF, проксирование всегда включено по умолчанию
}
```

> Для получения более подробной информации о формате, пожалуйста, проверьте [JSON schema](./schemas/domain.schema.json)

4. Ваш запрос на включение будет рассмотрен и объединен. Пожалуйста, не игнорируйте контрольный список PR. Если вы проигнорируете правила этого репозитория, ваш PR тоже будет проигнорирован. _Обязательно следите за ним на случай, если нам понадобится внести какие-либо изменения!_
5. После слияния запроса на включение подождите до 24 часов, пока изменения вступят в силу _(обычно это занимает от 5 до 15 минут)_
6. Наслаждайтесь своим новым доменом!
> Domains, used for illegal purposes will be removed and permanently banned. Please, provide a clear description of your resource in the PR.

## Если вы не знаете...

- Что такое страницы GitHub и как настроить личный домен, читайте в [docs здесь](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)
- Разница между `A`, `CNAME` и другими типами записей, статья в Википедии [это здесь](https://en.wikipedia.org/wiki/List_of_DNS_record_types)

> 🔍 Несколько подобных сервисов можно [найти здесь](https://free-for.dev/#/?id=domain).

[badge-tests]:https://img.shields.io/github/actions/workflow/status/tarampampam/free-domains/tests.yml?branch=master&label=tests&logo=github&style=for-the-badge
[badge-deploy]:https://img.shields.io/github/actions/workflow/status/tarampampam/free-domains/deploy.yml?branch=master&label=deploy&logo=github&style=for-the-badge

[actions]:https://github.com/tarampampam/free-domains/actions
[deploy]:https://github.com/tarampampam/free-domains/actions/workflows/deploy.yml
