# Data dictionary — кейс 2 «Кредитный конвейер»

## Как заполнять

В `applications.csv` 14 колонок. Все нужно описать. Одна строка — образец.
Для каждой колонки укажи: тип, обязательность, ограничение, пример (из CSV), код ошибки (если валидируется), комментарий.

## Образец (не трогать)

|Поле|Тип|Обяз.|Ограничение|Пример|Код ошибки|Комментарий|
|-|-|-|-|-|-|-|
|app\_id|string|да (сервер)|`app\_NNNN`|app\_0001|—|генерируется сервисом|

## Ваша таблица — 13 оставшихся колонок

|Поле|Тип|Обяз.|Ограничение|Пример|Код ошибки|Комментарий|
|-|-|-|-|-|-|-|
|age|integer|да|18-70|48|AGE\_OUT\_OF\_RANGE|Возраст.Для проверки дееспособности|
|income|integer|да|>0|67000|MISSING\_INCOME|Доход. Для расчета DTI и лимита суммы|
|employment|enum|да|employed,self-employed,retired,student,unemployed|student|INVALID\_EMPLOYMENT|Тип занятости. Стабильность дохода|
|family|enum|да|single,married,children|single|INVALID\_FAMILY|Семейное положение. Влияет на скоринговый балл|
|amount|integer|да|>0,<=10 × income|250000|AMOUNT\_LIMIT|Сумма кредита. Контроль нагрузки|
|term|integer|да|>0(в месяцах)|24|CC|Срок кредита. Расчет аннуитетного платежа и DTI|
|decision|enum||да|APPROVED, REFUSED, NEED\_MORE\_DATA, MANUAL\_REVIEW|REFUSED|-|Решение по заявке|
|reason|string|нет|Код из списка причин отказов|HIGH\_DTI|-|Причина отказа или запроса данных|
|client\_id|string|да|Уникальный ID|user_0007|INVALID\_CLIENT\_ID|Индетификатор клиента для связи заявки|
|passport\_hash|string|да|SHA-256,16 hex-символов|7f83b165|INVALID\_PASSPORT\_HASH|Хеш паспорта для идентификации|
|dti|float|да|2 знака после запятой;>=0;порог 0.5|0.40|HIGH\_DTI|Долговая нагрузка|
|bki\_score|integer|да|300-800,<550=отказ|580|BKI\_DELINQUENCY|Кредитный рейтинг из BKI|
|smev\_status|string||да|MATCH,MISMATCH,TIMEOUT,NOT\_CALLED|TIMEOUT|-|Статус проверки в гос.системах для подтверждения данных клиента|

## Критерий приёмки

* \[ ] Все 14 колонок описаны
* \[ ] Для age указан диапазон 18–70 и AGE\_OUT\_OF\_RANGE
* \[ ] Для income — > 0 и MISSING\_INCOME
* \[ ] Для employment — справочник из 5 значений и INVALID\_EMPLOYMENT
* \[ ] Для passport\_hash — только SHA-256, оригинал не хранится
* \[ ] Для dti — формула (аннуитет / доход), порог 0.5
* \[ ] Для bki\_score — диапазон 300–850, < 550 = отказ
* \[ ] Для smev\_status — MATCH / MISMATCH / TIMEOUT / NOT\_CALLED
* \[ ] Комментарий объясняет «зачем поле»

## Подсказки

* employment — enum из 5: employed, self-employed, student, retired, unemployed.
* family — enum из 3: single, married, children.
* decision — enum из 4: APPROVED, REFUSED, NEED\_MORE\_DATA, MANUAL\_REVIEW.
* passport\_hash — 16 hex-символов, не оригинал паспорта.
* dti — число с 2 знаками, от 0 до бесконечности, порог 0.5.

