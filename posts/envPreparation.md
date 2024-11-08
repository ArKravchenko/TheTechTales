# Подготовка окружения

Здесь коротко поговорим о том что нам потребуется для дальнейшей работы. Во всех дальнейших материалах я буду описывать
процесс установки и использования утилит для Unix-like и POSIX-совместимых систем.

### Немного истории

В 70х годах в лаборатории **Bell Labs** американской компании **AT&T** разработали проект операционной системы **Unix**
.  
Впоследствии на основе этой системы разными организациями и сообществами было разработано множество различных
операционок, в том числе и MacOs, часть из них имели открытый исходный код.  
Другими словами кто-то придумал машину с 4 колесами, двумя-тремя педалями, круглым рулем на переднем сидении, мотор под
капотом спереди и багажник сзади. Этот "стандарт" оказался удачным и был развит другими компаниями.

![Генеалогическое древо Unix-подобных операционных систем. Wikipedia.](../assets/unix_gen_tree.png "Генеалогическое древо Unix-подобных операционных систем. Wikipedia.")

Возможно кто-то разработал более удобное решение вообще без педалей руля и на гусеницах, оно работает хорошо и выполняет
свою функцию, но за счет того что у UNIX-like систем был открытый исходный код, их часто использовали для разработки.

В настоящее время Unix-системы признаны одними из самых исторически важных операционных систем, огромное количество
серверов работают на Unix-подобных системах, огромное чисто инструментов разработки в первую очередь ориентировано на
такие системы, закрытость исходного кода Windows сыграла с ним злую шутку.

> POSIX - это некий стандарт, договоренность как должен выглядеть интерфейс взаимодействия с операционной системой, чтоб программы написанные для Unix можно было на ней запускать.

Например: Windows Subsystem for Linux (WSL) — прослойка совместимости, впервые появившаяся в Windows 10 и реализующая
API ядра Linux поверх Windows. Иными словами снаружи выглядит как Unix-подобная, общаться можно как с Unix-подобной, а
что там под капотом - не важно. Согласитесь, сам факт того, что это Windows пришлось внедрять к себе слой совместимости
с Unix-подобными системами, а не наоборот, на что-то намекает.

Надеюсь после этой вводной стало понятно почему ITшники часто предпочитают продукты компании Apple: MacOs это
Unix-совместимая система, при этом поставленная на неплохую железку с хорошей поддержкой и удобным красивым интерфейсом,
чего в опенсорсных Linux (например Ubuntu) иногда не хватает.

#### Теперь к инструментам и как и установить:

1. **Homebrew**. Для начала установите
   Homebrew** [[для MacOs](https://brew.sh/) ; [для Linux](https://docs.brew.sh/Homebrew-on-Linux)], он значительно
   облегчит процесс установки всего остального, с ним установка практически любого ПО будет выглядеть как вызов одной
   команды из терминала:

```shell 
$ brew install {some_software}
```

2. [**Node.js**](https://nodejs.org/en/learn/getting-started/introduction-to-nodejs). Node.js - это интерпретатор
   JavaScript, то что будет читать и исполнять написанный нами код. Ее лучше устанавливать при помощи [**
   nvm**](https://github.com/nvm-sh/nvm?tab=readme-ov-file#installing-and-updating)
   (node version manager). nvm - это то что позволит нам переключаться между различными версиями node.js, так как
   некоторые пакеты могут работать только на определенных версиях интерпретатора. Если бы не было nvm, нам бы каждый раз
   пришлось переустанавливать node.js самостоятельно, при этом подчищая артефакты в виде файлов, конфигураций и
   переменных, оставленных в системе предыдущей версией (занятие не из приятных). nvm умеет делать за нас всю эту
   работу. Устанавливаем nvm так:

```shell
$ brew install nvm
```

Затем закрываем и открываем заново терминал и проверяем что nvm установился (это кстати называется smoke test, проверка
корректного функционирования кода по косвенным признакам. Если есть "дымок", то есть утилита вызывается без ошибок и
корректно возвращает свою версию, значит скорее всего костер горит правильно):

```shell
$ nvm -v
0.39.4
```

У меня версия 0.39.4, у вас может быть другая. Теперь устанавливаем через nvm собственно node.js версии 20 или выше,
главное четной. Четные версии - это так называемые **LTS (Long Time Support)** версии, то есть они будут еще долго
поддерживаться после выхода последующих.

```shell
$ nvm install 20
```

```shell
$ nvm use 20
```

nvm скачает 20 версию и установит и скажет вашей машине использовать именно ее (подменит $PATH чтоб все пути при вызове
node указывали на исполняемый файл нужной версии). Проверить что все корректно опять же можно вызвав node с ключом,
запрашивающим текущую версию:

```shell
$ node -v
20.17.0
```

В моему случае была скачана и установлена версия 20.17.0 . Полный список команд можно посмотреть так:

```shell
$ nvm -h
```

3. **Пакетный менеджер**. На самом деле тут мы ничего дополнительно ставить не будем. **npm** уже давно ставится
   автоматически с установкой node. Раньше было по-другому, но эти времена прошли.

> В самом начале мы ставили **homebrew**, утилиту, которая позволяет скачивать и устанавливать нужную версию ПО на вашу операционку. Пакетный менеджер делает приблизительно то же самое, только с отдельными скриптами на js (модулями) для конкретного проекта, которые кто-то написал и залил в общее хранилище. Свой модуль в npm registry можете залить и вы.
> Каждый проект который вы пишете будет зависеть от сторонних библиотек разных версий. Скачивать нужные версии, проверять их совместимость и добавлять к проекту будет как раз пакетный менеджер.

Есть и альтернативные пакетные менеджеры, но их я сейчас даже не буду упоминать, о них мы будем говорить позднее.

4. [GIT](https://git-scm.com/). Это система контроля версий.  
   Мы захотим не просто писать код, а где-то его хранить, что-то добавлять к нему, видоизменять, откатываться к
   предыдущим версиям, просматривать историю изменений, работать над одним проектом/файлом со своими коллегеами по
   команде/друзьями. Все это позволяет делать git. Установить можно так:

```shell
$ brew install git
```

Кроме того, сразу зарегистрируйтесь на сайте [github.com](github.com)

>GitHub — крупнейший веб-сервис для хостинга IT-проектов и их совместной разработки. Cервис основан на системе контроля
версий Git. В нем вы сможете хранить свои проекты, давать до них доступ другим разработчикам и много еще чего.

Сконфигурируйте git, указав имя и почту, например:

```shell
$ git config --global user.name "My Name"
$ git config --global user.email my@email.com
```

И сгенерируй SSH ключ

5. [IDE](/TheTechTales/posts/ide.html)
6. Docker

```shell
$ brew install git
```




