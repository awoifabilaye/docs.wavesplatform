
# API ключ

Чтобы использовать [API ноды](/ru/waves-node/node-api/) необходимо предоставить ваш хэш [API ключа](https://en.wikipedia.org/wiki/Application_programming_interface_key) и задать другие параметры в секции [Настройки REST API](/ru/waves-node/node-configuration#настройки-rest-api) файла конфигурации ноды. Дле использования некоторых функций API вам потребуется оригинальный API ключ (не хэшированное значение) в HTTP запросе.

Ваш API ключ ноды очень важен, как и [seed фраза](/ru/blockchain/glossary#secret-phrase) и пароль кошелька.

## Сгенерировать хэш API ключа

1. Создайте уникальную строку (string value) чтобы использовать её в качестве `API ключа`.

    **Примечание**: По умолчанию API ключ = `ridethewaves!`.

2. Перейдите в [веб-интерфейс Swagger](/ru/waves-node/node-api#веб-интерфейс-swagger).

3. Откройте API метод [/utils/hash/secure](https://nodes.wavesnodes.com/api-docs/index.html#!/utils/hashSecure_1) и введите вашу уникальную строку в поле `message`.

4. Нажмите **Execute** чтобы получить хэш API ключа. Используйте хэш API ключа в качестве значения параметра `api-key-hash` в файле конфигурации вашей ноды.

**Примечание:** API ключ передается в HTTP-заголовке в виде незащищенного текста. Злоумышленник может перехватить его при передаче по сети и использовать для кражи ваших средств. Очень важно защитить передачу данных с помощью переадресации портов HTTPS или SSH.

Пример CURL команды подписания транзакции, отправляемой с кошелька ноды:

```bash
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'X-API-Key: YOUR UNIQUE API KEY'
-d '{ \
"amount": 5800000000, \
"fee": 100000, \
"type": 4, \
"version": 1, \
"attachment": "", \
"sender": "3P3pUKEAKxegWr3PZkGYNq1mzQQaQ5zxZbw", \
"feeAssetId": null, \
"assetId": null, \
"recipient": "3P9p39MwZ5JjwdBSYEWC6XYri4jpovzcAbs", \
"feeAsset": null, \
"timestamp": 1568020044350 \
}' 'http://nodes.wavesnodes.com/transactions/sign'
```