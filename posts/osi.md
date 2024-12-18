# О протоколах или Сказка про OSI

## Немного истории

В 1970-е годы, на заре зарождения сетевых технологий сети в основном спонсировались государством
(NPL network в Великобритании, ARPANET в США, CYCLADES во Франции). История была такая же как позже с
браузерами, все делали по-своему, все наступали на похожие грабли, набивали шишки в одинаковых местах, и,
как и с другими технологиями, в итоге пришли к необходимости договариваться.

С 1977 года ISO реализовала программу по разработке общих стандартов и методов сетевого взаимодействия. Аналогичный
процесс развивался и в Международном консультативном комитете по телеграфии
и телефонии (МККТТ). Оба органа разработали документы, определяющие схожие сетевые модели. Впоследствии эти документы
были объединены в рамках эталонной модели взаимосвязи открытых систем (англ. Open Systems Interconnection, OSI)
или просто модели OSI.

## Что это такое - OSI?

Это некоторая попытка классифицировать и упорядочить все что было разработано и написано большим
количеством инженеров. Модель не идеальна, много критикуется и не всегда отражает реальное положение вещей, например
одна
технология может одновременно реализовывать два разных уровня взаимодействия, и не понятно к какому именно, согласно
этой модели, эту технологию отнести. Поэтому относят сразу к двум. Бывают и другие нюансы, но для понимания нами общей
картины
они не столь существенны, мы их опустим.

Модель определяет различные уровни взаимодействия систем.
Каждый уровень выполняет определённые функции при таком взаимодействии. Всего таких уровней, согласно модели OSI - 7.

![Segment, frame and datagramm](/TheTechTales/assets/osi.png "Визуальное представление модели OSI и охватываемых ею протоколов")

### Первый, физический уровень (physical layer, L1)

Физический уровень — самый простой для понимания, нижний уровень модели, который определяет
метод передачи данных, представленных в двоичном виде, от одного устройства (компьютера) к другому.

На этом уровне решаются вопросы, связанные с синхронизацией, избавлением от помех, скоростью передачи данных.

Компьютеры оперируют битами, нулями и единицами, и нам нужно выбрать каким способом мы будем сообщать нашему собеседнику
что именно мы ему сейчас посылаем, 0 или 1. На практике это значит что нам нужно выбрать либо провод,
где за 0 будет отвечать отсутствие напряжения, а за 1 - его наличие, либо источник света, где темнота будет означать 0,
а свет - 1 (либо наоборот),
ну или мы можем вообще посылать радиоволны или использовать какое-либо еще физическое явление или среду для передачи
наших нулей и единиц.

> Модель не обязательно привязана к нулям и единицам, а имеет гораздо более общий характер. Для аналогии давайте
> представим
> что мы - инженер Марк в здании большой корпорации, а в качестве среды передачи наших сообщений будем
> использовать мальчика-посыльного, приставленного к нашему отделу. Посыльный имеет пачку листов с корпоративными
> вензелями
> и колонтитулами. Все листочки из своей сумки, на которых нет корпоративных вензелей он считает случайно завалявшимся
> мусором
> и не обращает на них внимания.

Примерами реализации физического уровня могут служить оптоволокно, сеть 220в
(дада, есть устройства которые позволяют осущестлять сетевую связь через обычную бытовую розетку,
если вы не хотите или не можете тянуть отдельные провода), коаксиальный кабель, витая пара, беспроводная среда)

### Второй уровень, канальный (data link layer, L2)

Канальный - второй уровень сетевой модели OSI, предназначенный для передачи данных узлам, находящимся в
том же сегменте локальной сети. Также может использоваться для обнаружения и, возможно, исправления ошибок, возникших на
физическом уровне.

Чтобы переслать кому-то набор нулей и единиц - надо знать кому пересылать, нужно иметь некую систему адресации и
идентификации конечных узлов
(Например при помощи MAC-адреса устройства).

> В нашей сказке канальный уровень будет реализован за счет шапки корпоративного бланка, на котором мы будем указывать
> имя коллеги,
> которому хотим передать сообщение, а так же стол за которым его искать, например "Дизайнеру Юргену на 14 стол, от
> инженера Марка с 23 стола".
> Мальчик-посыльный, получив такой бланк с шапкой и каким-то текстом на нем, имеет достаточно информации для того чтобы
> передать наш листок.
> Стоит заметить, что Юрген сидит с нами в одном помещении (в одном сегменте сети), а вообще-то на другом этаже в другом
> департаменте тоже может быть некий другой дизайнер Юрген, тоже за 14 столом.
> Также важно понимать, что пока еще, передав мальчику наш бланк с сообщением, мы не можем быть уверены что Юрген его
> получит. Мальчик работает первую неделю, в сумке у него много хлама, он может забыть передать наше сообщение или
> потерять его по дороге.

На канальном уровне работают такие протоколы как Ethernet, PPP (Point-to-Point Protocol) и Wi-Fi (это как раз тот случай
когда классификация размыта, так как
оба этих протокола уже заранее прдразумевают определенную среду передачи сообщений: по витой паре, оптоволокну или
электромагнитными волнами)

### Третий уровень, сетевой (network layer, L3)

Сетевой уровень модели предназначен для определения пути передачи данных. Отвечает за трансляцию логических адресов и
имён в физические, определение кратчайших маршрутов, коммутацию и маршрутизацию, отслеживание неполадок и «заторов» в
сети.

На этом уровне работает всем нам известный протокол IPv4/IPv6 (Internet Protocol). Устройства могут располагаться не в
одной подсети, а в разных сегментах сети, соединенных между собой маршрутизаторами.

> В какой-то момент Юргена перевели в другой отдел.
> Мы знаем название его отдела и его новую должность, но не знаем где и за каким столом он теперь сидит. Мальчик
> посыльный тоже не знает. Но он знает что все сообщения между отделами передаются через общий рецепшн на первом этаже.
> Теперь чтобы послать Юргену письмо мы кладем корпоративный бланк с вензелями и шапкой с надписью "Дизайнеру Юргену, от
> инженера Марка" в папку, на которой пишем "В Департамент Промышленного Дизайна, Главному Дизайнеру".
>
> Мальчик посыльный несет эту папку на общий рецепшн, где другой посыльный собирает все такие письма от всех отделов,
> направленные в Департамент Промышленного Дизайна и несет их на нужный этаж в нужную комнату. Или на рецепшне
> выясняется что отдел Промышленного Дизайна находится в другом здании, нужно отнести на рецепшн корпуса номер 3, а там
> разберутся и направят на нужный этаж и в нужную комнату.
>
> Папка достигает нужной комнаты, там из нее вытаскивают листочек. В Департамент Промышленного Дизайна, Главному
> Дизайнеру - это к нам, а "Главному Дизайнеру" - это нашему старику Юргену, он за 17 столом.

Маршрутизатором тут выступал рецепшн, который знал куда направить документ адресованный по "IP-адресу" "В Департамент
Промышленного Дизайна, Главному Дизайнеру". При этом привязку "IP-адреса" к физическому (17 стол в новом департаменте)
уже сделали
внутри этого департамента. Со временем Юрген может переехать за 18 стол, но наше сообщение все равно будет доставляться
верному человеку.

### Четвертый уровень, транспортный (transport layer, L4)

Он предназначен для доставки данных. При этом неважно, какие данные передаются, откуда и куда, то есть, он предоставляет
сам механизм передачи. Блоки данных он разделяет на фрагменты, размеры которых зависят от протокола: короткие объединяет
в один, а длинные разбивает. Протоколы этого уровня предназначены для взаимодействия типа точка-точка.

> Мы уже разобрались как адресовать письмо Юргену, но открытым остается вопрос как гарантировать что Юрген это письмо
> получит? И важно ли нам чтоб Юрген обязательно получил наше письмо?

Наиболее известными протоколами транспортного уровня являются Transmission Control Protocol — протокол управления
передачей (TCP) и User Datagram Protocol — протокол пользовательских датаграмм (UDP).

UDP использует простую модель передачи, без явных «рукопожатий» для обеспечения надёжности, упорядочивания или
целостности данных. Датаграммы могут прийти не по порядку, дублироваться или вовсе исчезнуть без следа, но
гарантируется, что если они придут, то в целостном состоянии.

> У Марка с Юргеном со времен колледжа осталась забавная привычка посылать друг другу анекдоты. На один лист влезает
> один анекдот.
> И если Юрген не получит сообщение, то ничего ужасного не произойдет, завтра Марк отправит еще одно. Если анекдоты
> придут не в том порядке в котором их отправил Марк - тоже ничего страшного.

Механизм TCP предоставляет поток данных с предварительной установкой соединения, осуществляет повторный запрос данных в
случае потери данных и устраняет дублирование при получении двух копий одного пакета, гарантируя тем самым (в отличие от
UDP) целостность передаваемых данных и уведомление отправителя о результатах передачи.

> Иногда по работе Марку нужно пересылать Юргену не только анекдоты, но и важные рабочие документы, касающиеся
> совместного проекта. Сначала Марк посылает сообщение, чтобы удостовериться что Юрген на рабочем месте, а не в отпуске
> и не отошел на обед, в этом сообщении содержится текст: "Сейчас я перешлю тебе рабочий документ, ты на месте?"
> Юрген отвечает "На месте, жду" (механизм предварительных "рукопожатий", установка соединения), и с этого момента уже
> не может отойти пообедать пока Марк не отчитается что переслал весь документ полностью.
> Один рабочий документ может занимать больше одного корпоративного бланка, поэтому листы пронумерованы, ведь
> мальчик-посыльный
> умеет носить только по одному листу за раз. Если Юрген получает после листа номер 7 лист номер 9, то он пишет Марку
> сообщение "По пути потерялся лист номер 8, повтори отправку." На последнем листе Марк пишет "Это весь документ,
> конец связи."
> После этого Юрген может со спокойной душой пойти пообедать.

### Пятый уровень, сеансовый (session layer, L5)

Сеансовый уровень — 5-й уровень сетевой модели OSI, отвечает за поддержание сеанса связи, или по-другому - сессии,
позволяя приложениям взаимодействовать между собой длительное время.

Иногда требуется переслать несколько "документов" сразу, поэтому в конце пересылки первого документа не нужно писать "
конец связи", а лучше написать: "Сейчас будет еще один документ." Если еще точнее, то сообщение о том что нужно
установить постоянную сессию передается в самом начале, что-то вроде:

> "Юрген, с настоящего момента и до обеда я буду высылать тебе рабочую документацию, а ты в ответ присылай свои
> коментарии."
> После первого документа от Марка придет второй, со своей нумерацией. Если какой-то из промежуточных листов будет
> потерян - то Юрген запросит его снова, и будет периодически высылать свое мнение по поводу документов. Тут уже на обед
> не отлучишься, работа будет продолжаться до тех пор пока одна из стороне не напишет "Конец связи".

### Шестой уровень, представления данных (presentation layer, L6)

Этот уровень отвечает за преобразование протоколов и кодирование/декодирование данных. Запросы приложений, полученные с
уровня приложений, он преобразует в формат для передачи по сети, а полученные из сети данные преобразует в формат,
понятный приложениям.

До настоящего момента мы предполагали что Юрген и Марк общаются на русском языке и передают только текст.

> Марк и Юрген учились в одном колледже, где кроме обмена анекдотами, привыкли использовать сленг: кабинет директора
> предприятия они называют горой, директора - драконом, его секретаршу - Белоснежкой, чертежи - свитками и так далее. В
> итоге рабочие сообщения иногда приобретают следующий вид "Последний свиток тащи на гору к дракону, оставь у
> Белоснежки".
> Кроме того, иногда Марк с Юргеном не хотят переписывать длинные тексты документации на корпоративный бланк, а просто
> фотографируют нужный лист, печатают его на бланке и отсылают. При этом информацией является именно текст на
> фотографии.
> Еще Марк с Юргеном любят подшучитьва над драконом, но так как сообщения может перехватить Белоснежка - они используют
> шифр, который выучили в студенческом обществе.

Иначми словами, в ходе сеанса нужно договориться о кодировке, сжатии, формате данных, наличии или отсутствии шифрования.
На этом важном уровне может осуществляться сжатие/распаковка или кодирование/декодирование данных, осуществляется выбор
форматов и протоколов, например сжарие gzip/brotli, шифрование: SSL/TLS, кодировка и формат: win-1251/ASCII/UTF-8,
формат: XML/JSON/Base64

### Седьмой уровень, прикладной (application layer)

Седьмой уровень или уровень приложений. Прикладной уровень — это то, с чем взаимодействуют пользователи, с другими он
взаимодействует по минимуму.

Все услуги, получаемые седьмым уровнем от других, используются для доставки данных до пользователя. Протоколам седьмого
уровня не требуется обеспечивать маршрутизацию или гарантировать доставку данных, когда об этом уже позаботились
предыдущие шесть. Задача седьмого уровня — использовать свои протоколы, чтобы пользователь увидел данные в понятном ему
виде.

> Марк и Юрген обладают уникальными знаниями, поэтому чтобы избавить их от рутинных операций, компания выделила каждому
> по секретарю. Теперь передачу и прием листов от посыльных осуществляют секретари, а Марк и Юрген просто говорят что
> нужно передать, картинку, структуру документов, набор команд для рабочей программы иди что-то еще.

На этом уровне работают такие протоколы как HTTP, SMTP, SNMP, POP3, FTP, DHCP. Все это протоколы прикладного уровня.

### Заключение

Ранее в постах я писал что важно понимать основные базовые понятия. Разобравшись в них будет легче вникнуть в
проблематику на более низком уровне.

> Секретарши Марка и Юргена работают по протоколу HTTP/1.0 и каждый раз после получения документа говорят "конец связи".
> Это вызывает необходимость перед запросом каждого нового документа снова договариваться о пересылке одного следующего,
> или об установлении сессии.
> Секретарши из соседнего отдела работают по более новому протоколу HTTP/1.1 и по-умолчанию считают что сейчас будет
> запрашиваться пачка документов, поэтому прекращают ждать посыльного и идут обедать только по прошествии 15 минут, если
> не
> было новых сообщений.

> Белоснежка работает по протоколу HTTP/2.0, тесно сотрудничает с посыльным, и может передавать сразу по нескольку
> корпоративных бланков за раз, соответствующих разным частям разных документов. Это приводит к тому что работа идет
> быстрее, дракон получает и отправляет по несколько документов одновременно.

Если нам потребуется быстрее передавать данные для каких-то специфических целей, то мы должны понимать как спуститься на
более низкий уровень модели, какие преимущества нам это даст, и какой функциональности лишит.

Web строится на стеке технологий TCP/IP, поверх которого работает HTTP, все это передается либо по беспроводной сети,
либо по проводам, либо по оптоволокну. Данные шифруются протоколоами SSL и TLS, прежде чем превратиться в красивые
кнопочки и текст у вас на экране.
На каждом из уровней единицей передаваемой информации является сегмент, датаграмма и фрейм (корпоративный бланк с
вензелями, или один документ из пронумерованной серии, папка с указанием департамента получателя).

![Segment, datagramm and frame datagramm](/TheTechTales/assets/segment_datagramm_frame.png "Инкапсуляция и декапсуляция")

Надеюсь теперь и вы понимаете в общих чертах как это работает.

