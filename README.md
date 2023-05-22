Филиалы, остатки в филиалах, региональность, геолокация

## Основные возможности компонента plAffiliates

* Создание филиалов и полей для них
* Управление порядков вывода как филиалов, так и их полей
* Мультиязычность на основании пакета [Polylang](https://modstore.pro/packages/other/polylang)
* Подвязывание геолокации к филиалам
* Вывод на картах Google и Yandex маркеров расположения филиалов и информации о них
* Поиск ближайшего филиала на карте по геолокации посетителя сайта
* Мульти-регионалось (на основании страны/города) через поддомены
* Автоматический редирект посетителя на основании его геолокации на нужный поддомен филиала
* Учёт количества оставшихся товаров в каждом филиале
* Вывод товаров (на основании остатков) только определенного филиала
* Создание для каждого филиала SEO полей, подвязанных к шаблонам Modx 
* Создание для каждого филиала своего robots.txt файла
* Создание для каждого филиала своего sitemap.xml файла, который содержит только товары филиала (на основании остатков)


## Создание групп для полей филиалов

На странице "Пакеты" -> Филиалы" во вкладке "Менеджер полей филиалов" вы можете создать свои группы для полей, что в дальнейшем позволит вам в различных сниппетах, как получать нужные поля передав название группы, так и использовать отдельные чанки для каждой группы полей. 

Из "коробки" будет доступен список основных групп для полей.

![](https://file.modx.pro/files/4/5/c/45c84f5950d5c437aad7ee812cf6887a.png)

## Создание полей для филиалов

На странице "Пакеты" -> Филиалы" во вкладке "Менеджер полей филиалов" вы можете создать необходимые вам для филиалов поля, задав для каждого из них ряд параметров, отвечающих как за тип ввода, так и за оформление.
 
**Примечание**. Параметр "Мультиязычное" позволяет создать поле, которое будет иметь возможность ввода значения на разных языках при условии, что установлен пакет [Polylang](https://modstore.pro/packages/other/polylang).

Из "коробки" будет доступен список основных полей. При необходимости вы можете ненужные поля удалить либо отключить.

Через перетаскивание поля в списке полей вы можете менять порядок его вывода.

![](https://file.modx.pro/files/3/3/e/33ecfb141bb4bd213c63cc3455437e87.png)

![](https://file.modx.pro/files/e/9/4/e94d29838cd431631f0dd2a473dee876.png)

![](https://file.modx.pro/files/c/e/5/ce59d29e8df2fd00bbe066a25315e53d.png)

![](https://file.modx.pro/files/5/0/6/50622b5d49d6f36f7de70e28942a2b6c.png)

## Создание филиалов

На странице "Пакеты" -> Филиалы" во вкладке "Филиалы" вы можете создавать и управлять данными филиалов. 

При создании нового филиала будет доступно только одно обязательное поле "**Метка**", которое является внутренним названием филиала и нигде кроме админки не будет фигурировать, а также ряд полей в разделе "Дополнительно". Все поля, которые были выми созданы, будут уже доступны на этапе редактирования филиала.

Значение полей филиалов проходят обработку парсером **Fenom**, поэтому в них можно использовать плейсхолдеры и теги Modx.
Например, в поле "**Ссылка**" вы можете указать ссылку на страницу с информацией о филиале в следующем виде.

```html
[[~ID-страницы]]
```

Через перетаскивание филиала в списке филиалов вы можете менять порядок его вывода.

![](https://file.modx.pro/files/c/8/2/c82d5273aef69990e956649a8f4e9cda.png)

![](https://file.modx.pro/files/3/b/6/3b62c336c37d6b9e5dc33a34f752a332.png)

## Управление количеством оставшегося товара в филиалах

### Через админ-панель
Добавлять информацию по количеству оставшегося товара по филиалам можно, как на отдельной странице "Пакеты" -> Филиалы" -> "Остатки товаров в филиалах", так и непосредственно в карточки товара во вкладке "Остатки товара в филиалах"

![](https://file.modx.pro/files/e/8/f/e8f521cc27c81de848ac05837b48a0ec.png)
![](https://file.modx.pro/files/1/d/a/1da0f22a77acb82eed493a59d23ee31e.png)

### Через скрипт

Для программного добавления/обновления информации по количеству оставшегося товара у филиала имеется ряд функций.

```php

/** @var PlAffiliate $plaffiliate */
$plaffiliate = $modx->getService('plaffiliates', 'PlAffiliate');
/** @var PlAffiliateTools $tools */
$tools = $plaffiliate->getTools();

$count = 24;
$productId = 12;
$guid = 'e7555e6f-37a8-11ec-ca96-0242ac120005' 

// Получение ID филиала для некого внешнего ID, например ID в УТ\CRM. Устанавливается для филиала через поле "Внешний ID"
$affiliateId =  $tools->getAffiliateIdByGuid($guid);

// Добавления/обновления информации по количеству оставшегося товара у филиала
$tools->setAffiliateProductRemain($affiliateId, $productId, $count);

// Количество оставшегося товара у филиала
$remain = $tools->getAffiliateProductRemain($affiliateId, $productId);

// Общее количество оставшегося товара по всем филиалам
$remain = $tools->getAllAffiliateProductRemain($productId);

// Сброс (обнуление значения) у всех филиалов количества оставшегося товара
$tools->resetAllAffiliateProductRemain($productId);

```
![](https://file.modx.pro/files/4/2/4/42410a8e12f9dbdf192fb89c6bd5f994.png)

**Примечание.** Если вы не планируете вообще работу с остатками и хотите, что бы в карточки товара не выводилась вкладка "Остатки товара в филиалах", то в системных настройках компонента отключите опцию "**Показать вкладку остатки у товара**".

### Учет количества оставшегося товара в филиале при покупке

Для того, что бы при покупке происходило проверка на наличие нужного количества товара, необходимо включить в системных настройках компонента опцию "**Учитывать количество остатков товара**". После чего при добавлении товара в корзину/изменении будет проверяться доступное кол-во товара, и если его нет в наличии, будет выдано предупреждение, сам товар в таком случае нельзя будет добавить.

Проверка нужного количества товара будет происходить в текущем филиале. Что бы она происходила с учетом общего количества во всех филиалах, необходимо включить в системных настройках компонента опцию "**Учитывать общее количество остатков во всем филиалах**", но в таком случае не будет доступен функционал синхронизации остатков при покупке/возврате товара.

Для того, что бы при покупке/возврате товара происходила синхронизация остатков, включите в системных настройках компонента опцию "**Синхронизировать остатки**".

Статусы заказа для синхронизации остатков при списании/возврате товара можно задать в системных настройках компонента:

* Статусы списания остатков (plaffiliates_status_pickup_remains)
* Статусы возврата остатков (plaffiliates_status_return_remains)

![](https://file.modx.pro/files/3/0/4/304e54efbc021d0d9342e87f2de81ee7.png)

## Создание SEO-полей для филиалов

В меню компонента, кликнув на пункте "SEO" на открывшейся странице на вкладке "SEO-Поля", вы можете создать нужные вам поля.
![](https://file.modx.pro/files/0/e/b/0eb61267a91b67ee40b46ef682a5b484.png)
После чего на вкладке "SEO-Шаблоны полей" задать значения для поля, связав его с филиалом и шаблоном Modx. Значение поля обрабатывается шаблонизатором Fenom.
![](https://file.modx.pro/files/c/1/9/c194695836de0e2b1ce0a21fa1a6ffde.png)

Для того, что бы созданные SEO-полей были доступны через плейсхолдеры Modx, необходимо:
* В системных настройках компонента включить опцию "**Включить плейсхолдеры SEO-полей**"
  ![](https://file.modx.pro/files/a/4/c/a4cd8c27ba8e3fc6aee44f857f076641.png)
* При необходимости изменить префикс полей в системной опции компонента "Префикс для плейсхолдеров SEO-полей" по умолчанию используется **pas**

Пример использования плейсхолдеров SEO-полей
```html
h1: [[!+pas.h1]]
title: [[!+pas.title]]
```

Fenom синтекс

```html
h1: {$_modx->getPlaceholder('pas.h1')}
title: {$_modx->getPlaceholder('pas.title')
```

## Создание robots.txt для филиалов
* В меню компонента, кликнув на пункте "SEO" на открывшейся странице на вкладке "robots.txt", можно создать содержания файла robots.txt для нужного филиала.

![](https://file.modx.pro/files/2/0/f/20f14e376b9e5fbdddce43b80b12d0ab.png)
* Создать документ с названием robots, у которого "**Тип содержимого**" должен быть указан как "**text**", "**Шаблон**" выбран "**(пустой шаблон)**" и в поле "**Содержимое**" указать вызов сниппета **getPlAffiliateRobots**

  ![](https://file.modx.pro/files/7/3/c/73ccb11a3e52dd32e4c65972fd4de340.png)
  ![](https://file.modx.pro/files/a/1/4/a1476a68a811a0283f8c99e3a280d9fa.png)
  Если для филиала не будет создано значение robots.txt, то сниппет **getPlAffiliateRobots** вернет значение по умолчанию, которое указано в чанке "**tpl.plAffiliates.robots.default**"

**Примечание.** В списке филиалов будут доступны только родительские филиалы, для которых заполнено поле "Хост".

**Важно!** В корне сайта не должно быть файла robots.txt

## Создание sitemap.xml для филиалов

Необходимо создать документ с названием sitemap, у которого "**Тип содержимого**" должен быть указан как "**XML**", "**Шаблон**" выбран "**(пустой шаблон)**" и в поле "**Содержимое**" указать вызов сниппета **getPlAffiliateSitemap**

![](https://file.modx.pro/files/0/e/3/0e34fcc47bbe202b811843a727e1e05e.png)

**Важно!** В корне сайта не должно быть файла sitemap.txt

## Основные настройки

### Настройка сервиса геолокации

В системных настройках компонента в разделе "Карта" в опции "Класс Карты" укажите класс провайдера для карты.

Доступные следующие значения:
* PlAffiliateYaMapProvider - Yandex карты (по умолчанию)
* PlAffiliateGMapProvider - Google карты

**Примечание.** Для работы с Google картами необходимо обязательно [получить API-ключ](https://developers.google.com/maps/documentation/javascript/get-api-key?hl=ru#key) и указать его в опции "API Ключ Google Maps"

![](https://file.modx.pro/files/c/2/5/c2511ca614f9b553e7c5eeb91ffe1b08.png)

### Настройка геолокации у филиалов

После того, как вы настроили выбранный сервис карт, можно перейти к настройке геолокации у филиалов.

Укажите данные широты и долготы расположения офиса филиала, что позволит вам в дальнейшем через сниппет **getPlAffiliateMap** выводить его на карте и делать поиск ближайшего.

Указать широту и долготу можно как вручную, так и с помощью перетаскивания маркера на карте. Что бы открыть карту, нужно кликнуть по кнопке "Определить на карте".

Для того, что бы маркер быстро переместить в нужное место, зажмите на клавиатуре клавишу **SHIFT** и не отпуская ее сделайте клик левой кнопкой мышки в нужном месте карты, если при этом еще одновременно зажать **Alt**, то дополнительно произойдёт центрирование карты.

![](https://file.modx.pro/files/0/0/1/00122b14513c45b21a2dce60a6acb798.png)

![](https://file.modx.pro/files/d/a/8/da86fcae40ccfa6027065c3da976819e.png)

### Настройка сервиса определение местоположения пользователя по IP

Для подключения сервиса необходимо в системных настройках компонента в разделе "Геолокация" заполнить опцию API ключ/конфиг выбранного сервиса, который вы получили после регистрации, а также его класс обработчик.

Из коробки доступные следующие условно-бесплатные сервисы:

[dadata.ru](https://dadata.ru/api/)

* API конфиг сервиса DaData.ru
* PlAffiliateDaDataGeoLocation

[ipinfo.io](https://ipinfo.io/developers)

* API ключ сервиса ipinfo.io
* PlAffiliateIpInfoGeoLocation

[iploka.com](https://iploka.com)

* API ключ сервиса iploka.com
* PlAffiliateIpLokaGeoLocation

![](https://file.modx.pro/files/6/b/f/6bf729a6b11f23997856e914c294ed41.png)

### Настройка автоматического перенаправление посетителей на поддомены филиалов

Если вы планируете использовать автоматическое перенаправление посетителей на основании их геоданных на поддомены филиалов, то для каждого "родительского" филиала необходимо заполнить:

* В поле "Хост" название поддомена, на который следует делать переадресацию
* Через выбранный сервис геолокации получить данные для полей "Стране" и "Город"

> Родительский филиал - филиал, у которого нет родителя.  
> У одного и того же города не может быть больше одного родительского филиала.

Для получения геолокационных данных у соответствующих полей необходимо кликнуть по кнопке с изображением стрелки компаса и в появившемся окне укажите какой-либо IP города, в котором находится филиал, по умолчанию уже введен ваш IP.

IP нужного города можно получить, например, на сайте [ip.osnova.news](https://ip.osnova.news)

**Важно!** Если через какое-то время вы решите изменить сервис определения геоданных, то после перехода на него необходимо заново произвести настройку поля "Город", так как каждый сервис может по-разному его именовать.

![](https://file.modx.pro/files/5/6/4/564120cacacf75d33e863d5aeaf717ef.png)
![](https://file.modx.pro/files/e/a/6/ea684d6f2bb56cac151b52a84242abef.png)

После того, как вся необходимая информация у филиалов заполнена в системных настройках компонента, следует включить опцию "**Перенаправлять посетителей на хост филиала**", а также в системных настройках Modx в опции "**Домен для сессионных куки**" (session_cookie_domain) укажите свой основной домен.

![](https://file.modx.pro/files/1/5/d/15dec7233173f25f694cdb0849f50a49.png)

**Примечание.** Перенаправление будет происходить через 302-редирект только один раз на [сессию сайта.](https://vc.ru/u/740266-mks-media/301859-vse-chto-nuzhno-znat-o-sessii-na-sayte)

### Добавление информации о текущем выбранном филиале в плейсхолдеры Modx

Для того, что информация о текущем выбранном филиале была доступна через плейсхолдеры Modx, необходимо:
* В системных настройках компонента включить опцию "**Включить плейсхолдеры филиала**"
  ![](https://file.modx.pro/files/a/4/c/a4cd8c27ba8e3fc6aee44f857f076641.png)
* При необходимости изменить префикс полей в системной опции компонента "Префикс для плейсхолдеров филиала" по умолчанию используется **pa**
* Для полей филиала, которые должны быть доступны через плейсхолдеры Modx, необходимо в менеджере полей филиалов включить опцию "**Доступно в плейсхолдере**"
![](https://file.modx.pro/files/0/1/c/01cce052601c7f7e955ca01801eaed82.png) 

Пример использования плейсхолдеров филиала
```
id: [[!+pa.id]]
Name: [[!+pa.name]]
Phone: [[!+pa.phone]]
E-mail: [[!+pa.email]]
```
Fenom синтекс
```
id: {$_modx->getPlaceholder('pa.id')}
Name: {$_modx->getPlaceholder('pa.name')
Phone: {$_modx->getPlaceholder('pa.phone')
E-mail: {$_modx->getPlaceholder('pa.email')
```

## Сниппеты

### getPlAffiliates - Вывод списка филиалов

**Параметры** 

| Имя           | Описание                                                                                                                                    |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------|
| affiliates    | Список ID филиалов, через запятую. По умолчанию выводятся все опубликованные филиалы.                                                       |
| city          | Название города филиалы, которого следует вернуть.                                                                                           |
| onlyParent    | Вернуть только родительские филиалы.                                                                                                        |
| parents       | Список ID родительских филиалов через запятую, потомков которых ледует вернуть.                                                            |
| includeParent | Включить вывод родительских отделений. Полезно при указании более одного «parents».                                                         |
| published     | Только опубликованные. По умолчанию: 1                                                                                                      |
| onlyFields    | Название полей филиала, через запятую, которые нужно выводить.                                                                              |
| ignoreFields  | Название полей филиала, через запятую, которые не нужно выводить.                                                                           |
| fieldGroups   | Название группы полей, через запятую, поля которых нужно выводить.                                                                          |
| sortby        | Сортировка выборки.  По умолчанию: rank.                                                                                                    |
| sortdir       | Направление сортировки.  По умолчанию: ASC.                                                                                                 |
| limit         | Ограничение количества результатов выборки.  По умолчанию: 0                                                                                |
| offset        | Пропуск результатов от начала. Необходимо использовать вместе с явно указанным &limit.  По умолчанию: 0                                     |
| tpl           | Имя чанка для оформления результата. Если не указан, то содержимое полей ресурса будет распечатано на экран. По умолчанию: tpl.plAffiliates |
| tplGroups     | Имя чанков, через запятую, для групы полей. Формата: название группы:название чанка                                                         |
| tplWrapper    | Чанк-обёртка, для заворачивания всех результатов. Принимает один плейсхолдер: [[+output]].                                                  |

Пример вызова сниппета с параметром tplGroups. 

```
[[getPlAffiliates? 
&tplGroups=`address:affiliates.group.address,contacts:affiliates.group.contacts`
]]
```
Fenom синтекс

```
{$_modx->runSnippet('getPlAffiliates', [
'tplGroups' => 'address:affiliates.group.address,contacts:affiliates.group.contacts',
])}
```

**Примечание**. Группа полей обработанная в чанке группы будет доступна в основном чанке (tpl) под названием группы и иметь порядковый номер сортировки первого поля из группы.   

### getPlAffiliateField - Возвращает значения поля филиала

**Параметры**

| Имя         | Описание                                                           |
|-------------|--------------------------------------------------------------------|
| field       | Название поля. По умолчанию id                                     |
| affiliateId | ID филиала. По умолчанию текущий, определяемый на основании хоста. |

**getPlAffiliateMap** - Вывод списка филиалов на карте

**Параметры**

| Имя           | Описание                                                                                                                                                                                                                                                    |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| affiliates    | Список ID филиалов, через запятую. По умолчанию выводятся все опубликованные филиалы.                                                                                                                                                                       |
| city          | Название города филиала, которого следует вернуть.                                                                                                                                                                                                           |
| onlyParent    | Вернуть только родительские филиалы.                                                                                                                                                                                                                        |
| parents       | Список ID родительских филиалов, через запятую, потомков которых ледует вернуть.                                                                                                                                                                            |
| includeParent | Включить вывод родительских отделений. Полезно при указании более одного «parents».                                                                                                                                                                         |
| published     | Только опубликованные. По умолчанию: 1                                                                                                                                                                                                                      |
| onlyFields    | Название полей филиала, через запятую, которые нужно выводить.                                                                                                                                                                                              |
| ignoreFields  | Название полей филиала, через запятую, которые не нужно выводить.                                                                                                                                                                                           |
| fieldGroups   | Название группы полей, через запятую, поля которых нужно выводить.                                                                                                                                                                                          | |
| limit         | Ограничение количества результатов выборки.  По умолчанию: 0                                                                                                                                                                                                |
| offset        | Пропуск результатов от начала. Необходимо использовать вместе с явно указанным &limit.  По умолчанию: 0                                                                                                                                                     |
| provider      | Провайдер карты. По умолчанию используется тот который задан в системной опции комопнента "[Класс Карты](https://file.modx.pro/files/9/a/c/9ac3782127cab9edefc2ea3c94390aed.png)". Допустимые значения: PlAffiliateYaMapProvider; PlAffiliateGMapProvider.  |
| zoom          | Зум карты                                                                                                                                                                                                                                                   |
| markerIcon    | Иконка маркера. По умолчанию: /assets/components/plaffiliates/images/map/marker.svg                                                                                                                                                                         |
| markerSize    | Размер маркера. Пример: 67,81                                                                                                                                                                                                                               |
| markerAnchor  | Anchor маркера. Пример: 30,81                                                                                                                                                                                                                               |
| mapCenter     | Координаты центра карты в формате JSON строки вида: {"lat": 55.76,"lon": 37.64}. По умолчанию  если на карте всего 1 маркер, то центр карты будет установлен относительно его координат, если несколько, то таким образом, что бы они все смогли отобразиться. |
| tpl           | Имя чанка для оформления результата. Если не указан, то содержимое полей ресурса будет распечатано на экран. По умолчанию: tpl.plAffiliates.map                                                                                                             |
| tplGroups     | Имя чанков, через запятую, для групы полей. Формата: название группы:название чанка                                                                                                                                                                         |
| tplWrapper    | Чанк-обёртка, для заворачивания всех результатов. Принимает один плейсхолдер: [[+output]].                                                                                                                                                                  |
| tplMarkerHint | Чанк оформления хинта маркера карты. По умолчанию: @INLINE {$fields.name.value}                                                                                                                                                                             |
| tplMarkerInfo | Чанк оформления информационного окна маркера карты. По умолчанию: tpl.plAffiliates.marker.info                                                                                                                                                              |
| cssClasse     | CSS Класс для контейнера карты                                                                                                                                                                                                                              |
| css           | Ссылка на подключаемый css. По усоляанию: {assets_url}components/plaffiliates/css/web/map.css                                                                                                                                                               |

**Примечание**. Если на карте больше одного отделения, то на ней появиться кнопка поиска ближайшего отделения на основании геоданных посетителя.  

### getPlAffiliatesLinks - Вывод списка ссылок для переключения/перехода на поддомен филиала.

**Параметры**

| Имя           | Описание                                                                                                                                          |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| affiliates    | Список ID филиалов, через запятую. По умолчанию выводятся все опубликованные филиалы.                                                             |
| city          | Название города филиала, которого следует вернуть.                                                                                                 |
| onlyParent    | Вернуть только родительские филиалы.                                                                                                              |
| parents       | Список ID родительских филиалов, через запятую, потомков которых ледует вернуть.                                                                  |
| includeParent | Включить вывод родительских отделений. Полезно при указании более одного «parents».                                                               |
| published     | Только опубликованные. По умолчанию: 1                                                                                                            |
| onlyFields    | Название полей филиала, через запятую, которые нужно выводить.                                                                                    |
| ignoreFields  | Название полей филиала, через запятую, которые не нужно выводить.                                                                                 |
| fieldGroups   | Название группы полей, через запятую, поля которых нужно выводить.                                                                                |
| sortby        | Сортировка выборки.  По умолчанию: rank.                                                                                                          |
| sortdir       | Направление сортировки.  По умолчанию: ASC.                                                                                                       |
| limit         | Ограничение количества результатов выборки.  По умолчанию: 0                                                                                      |
| offset        | Пропуск результатов от начала. Необходимо использовать вместе с явно указанным &limit.  По умолчанию: 0                                           |
| tpl           | Имя чанка для оформления результата. Если не указан, то содержимое полей ресурса будет распечатано на экран. По умолчанию: tpl.plAffiliates.links |
| tplGroups     | Имя чанков, через запятую, для групы полей. Формата: название группы:название чанка                                                               |
| tplWrapper    | Чанк-обёртка, для заворачивания всех результатов. Принимает один плейсхолдер: [[+output]].                                                        |
| js            | Ссылка на подключаемый js. По усоляанию: {assets_url}components/plaffiliates/js/web/switch.js                                                     |

### getPlAffiliateRemains - Вывод списка филиалов с количеством оставшегося товара в каждом.

**Параметры**

| Имя            | Описание                                                                                                                                            |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| pid            | ID товара остатки которого следует отобразить. По умолчанию ID ресурса, в котором вызван сниппет.                                                    |
| showZeroRemain | Показывать филиалы с нулевым остатком. По умолчанию 1.                                                                                              |
| affiliates     | Список ID филиалов, через запятую. По умолчанию выводятся все опубликованные филиалы.                                                               |
| city           | Название города филиала, которого следует вернуть.                                                                                                   |
| onlyParent     | Вернуть только родительские филиалы.                                                                                                                |
| parents        | Список ID родительских филиалов, через запятую, потомков которых ледует вернуть.                                                                    |
| includeParent  | Включить вывод родительских отделений. Полезно при указании более одного «parents».                                                                 |
| published      | Только опубликованные. По умолчанию: 1                                                                                                              |
| onlyFields     | Название полей филиала, через запятую, которые нужно выводить.                                                                                      |
| ignoreFields   | Название полей филиала, через запятую, которые не нужно выводить.                                                                                   |
| fieldGroups    | Название группы полей, через запятую, поля которых нужно выводить.                                                                                  |
| sortby         | Сортировка выборки.  По умолчанию: rank.                                                                                                            |
| sortdir        | Направление сортировки.  По умолчанию: ASC.                                                                                                         |
| limit          | Ограничение количества результатов выборки.  По умолчанию: 0                                                                                        |
| offset         | Пропуск результатов от начала. Необходимо использовать вместе с явно указанным &limit.  По умолчанию: 0                                             |
| tpl            | Имя чанка для оформления результата. Если не указан, то содержимое полей ресурса будет распечатано на экран. По умолчанию: tpl.plAffiliates.remains |
| tplGroups      | Имя чанков, через запятую, для групы полей. Формата: название группы:название чанка                                                                 |
| tplWrapper     | Чанк-обёртка, для заворачивания всех результатов. Принимает один плейсхолдер: [[+output]].                                                          |

### getPlAffiliateProducts - Вывод списка товаров с учетом его наличия в филиале.

Сниппет является оберткой над сниппетом [msProducts](https://docs.modx.pro/komponentyi/minishop2/snippetyi/msproducts), поэтому содержит все его параметры плюс следующие свои.

**Параметры**

| Имя         | Описание                                                           |
|-------------|--------------------------------------------------------------------|
| affiliateId | ID филиала. По умолчанию текущий, определяемый на основании хоста. |
| element     | Название сниппета для вывода товаров. По умолчанию msProducts.     |

**Примечание**. В чанке tpl доступно поле "affiliate_remain", в котором содержится значение остатка для товара.

### getPlAffiliateSitemap - Генерация карты сайта для поисковых систем для текущего филиала. 

Среди списка товаров будут только те, для которых есть остаток. 

Сниппет является оберткой над сниппетом [pdoSitemap](https://docs.modx.pro/komponentyi/pdotools/snippetyi/pdositemap), поэтому содержит все его параметры плюс следующие свои.

**Параметры**

| Имя            | Описание                                                           |
|----------------|--------------------------------------------------------------------|
| affiliateId    | ID филиала. По умолчанию текущий, определяемый на основании хоста. |

### getPlAffiliateRobots - Вывод содержания файла robots.txt для текущего филиала.

**Параметры**

| Имя         | Описание                                                                     |
|-------------|------------------------------------------------------------------------------|
| affiliateId | ID филиала. По умолчанию текущий, определяемый на основании хоста.           |
| tplDefault  | Чанк с значением по умолчанию. По умолчанию: tpl.plAffiliates.robots.default |


## Системные события

### plaffiliateOnManagerCustomCssJs - Загрузка скриптов plAffiliates.

**Параметры**

| Имя        | Описание                                                             |
|------------|----------------------------------------------------------------------|
| controller | Экземпляр класса контроллера                                         |
| page       | Идентификатор страницы. Доступные значения: affiliates; remains; seo |

### plaffiliateOnPrepareMapMarker - Подготовка данных для создания маркера филиала на карте.

**Параметры**

| Имя       | Описание                          |
|-----------|-----------------------------------|
| tools     | Экземпляр класса PlAffiliateTools |
| place     | Массив с данными для маркера      |
| affiliate | Массив с данными филиала          |

Пример плагина меняющего иконку, текст хинта и информационного окна маркера у филиала с ID 5

```php
<?php
/**
 * @var modX $modx
 * @var PlAffiliateTools $tools
 * @var array $place
 * @var array $affiliate
 */

switch ($modx->event->name) {
    case 'plaffiliateOnPrepareMapMarker':
        if ($affiliate['id'] == 5) {
            $params = & $modx->event->params;
            $params['place']['hint'] = 'New hint text';
            $params['place']['info'] = $tools->getPdoTools()->getChunk('@INLINE ({$id}) - {$fields.name.value}', $affiliate);
            $params['place']['marker'] = array(
              'icon' => '/assets/components/plaffiliates/images/map/marker_green.svg',
              //'size' => '67,81',
              //'anchor' => '30,81',
            );
        }
        break;
}
```
