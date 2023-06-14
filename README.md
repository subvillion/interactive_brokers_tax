# 3-НДФЛ Interactive Brokers
Данный скрипт автоматически формирует пояснительную записку к декларации 3-НДФЛ на основании отчетов Interactive Brokers.
## Внимание!
Данный скрипт - полностью некоммерческий продукт, которым я делюсь с сообществом безвозмездно, однако, это не означает, что я планирую поддержку пользователей данного скрипта (добавление функциональности, исправление ошибок и т.д.). Пока *на моих отчетах* всё работает, а также, пока не изменилось налоговое законодательство, все правки - вашими силами и Pull request-ами. Просьба не спамить меня в разделе Issues, у меня в любом случае нет и не будет времени этим заниматься.
## Ограничения по применению
Поскольку я занимаюсь долгосрочными инвестициями, я не использую такие инструменты, как фьючерсы, опционы, а также никогда не использую плечо и сделки SHORT. В связи с этим, такие операции скриптом не поддерживаются. Также не поддерживаются операции Reverse split, т.к. таких инструментов на данный момент у меня в отчетах нет, будьте внимательны!
## Подготовка к использованию
1) Установите Python 3 (последняя проверенная версия - Python 3.11.3)
2) Скачайте архив со скриптом `(Clone or Download->Download ZIP)` и распакуйте его в произвольную папку на компьютере
3) Скачайте годовые отчеты *на английском языке* из личного кабинета брокера в формате .csv (необходимы за все года для корректного расчета сделок продажи), переименуйте их в {год отчета}.csv (например "2018.csv") и положите в папку со скриптом
4) Исправьте дату открытия счета в скрипте `ib.py` на свою (строка `StartDate = "20.03.2019"`)
5) В папке со скриптом создайте `venv` командой и активируйте его:
```bash
python -m venv ib_venv
"ib_venv\Scripts\activate.bat"
```
6) Выполните установку необходимых пакетов Python при помощи команды в консоли, запущенной от имени администратора из папки со скриптом:
```bash
pip install -r requirements.txt
```
## Использование
1) Запустите скрипт командой в консоли
```bash
python ib.py
```
2) По запросу, введите первый год, на который есть отчет (например "2018")
3) Дождитесь появления надписи "Готово" и нажмите Enter. Скрипт должен сформировать вашу пояснительную записку в формате `.docx` и открыть его
4) Повторите п.1-3 для всех годов (нужно делать только в первый раз, в дальнейшем - только подотчетный год)
5) Внесите в раздел `Доходы за пределами РФ` декларации 3-НДФЛ следующие доходы *в рублях*(!!!) с датой 31 декабря подотчетного года:
- `Источник выплат` - "Interactive Brokers (дивиденды)". `Полученный доход (код 1010)` и `Налог, уплаченный в иностранном государстве`(чтобы это поле появилось, нужно указать дату уплаты налога) - {ваши суммы из пояснительной записки}
- `Источник выплат` - "Interactive Brokers (операции с ЦБ)". `Полученный доход (код 1530)` и `Сумма вычета (расхода) в рублях (код вычета - 201)` - {ваши суммы из пояснительной записки}

В случае, если брокер начислял проценты по Программе повышения доходности (в пояснительной записке есть раздел 2.4), добавляем еще одну строку:
- `Источник выплат` - "Interactive Brokers (доп. доход)". `Полученный доход (код 1011)` - {ваша сумма из пояснительной записки}
## Дополнительная информация
Данный скрипт также можно использовать и до окончания текущего налогового периода для понимания того, сколько на данный момент (по итогам года) потребуется заплатить налогов. В этом случае, нужно скачать отчет с начала года до текущей даты и положить его к остальным. При этом сценарии использования, скрипт предложит внести дополнительные сделки, которых нет в отчете (например, планируемые сделки) и сформирует отчет с учетом них, а также сам предложит сделки для налоговой оптимизации.

## P.S> 
Налоговая сформированную при помощи данного скрипта декларацию приняла и полностью утвердила все расчеты. Единственное, имейте ввиду, что некоторые неопытные сотрудники могут не понять, почему у вас все доходы от зарубежного брокера (которые были получены в валюте), указаны в декларации одной-тремя строками в рублях. В этом случае нужно просто объяснить налоговику, что все расчеты представлены в пояснительной записке, а в декларации так указано для того, чтобы эта самая декларация не вышла размером с Войну и мир, а вам не пришлось через сайт или программу вбивать несколько сотен операций.

Если скрипт сэкономил вам время, можете поблагодарить автора:

[![Donate](https://img.shields.io/badge/donate-Yandex-red.svg)](https://yoomoney.ru/to/41001607398287)
