# Подготовка окружения

Здесь коротко поговорим о том что нам потребуется для дальнейшей работы. Во всех дальнейших материалах я буду описывать
процесс установки и использования утилит для Unix-like (иногда используют сокращение *nix) и POSIX-совместимых систем.

### Немного истории

В 70х годах в лаборатории **Bell Labs** американской компании **AT&T** разработали проект операционной системы **Unix**
.  
Впоследствии на основе этой системы разными организациями и сообществами было разработано множество различных
операционок, в том числе и MacOs. Часть из них имели открытый исходный код.  
Другими словами кто-то придумал машину с 4 колесами, двумя-тремя педалями, круглым рулем на переднем сидении, мотор под
капотом спереди и багажник сзади. Этот "стандарт" оказался удачным и был развит другими компаниями.

![Генеалогическое древо Unix-подобных операционных систем. Wikipedia.](../assets/unix_gen_tree.png "Генеалогическое древо Unix-подобных операционных систем. Wikipedia.")

Возможно кто-то разработал более удобное решение вообще без педалей руля и на гусеницах, оно работает хорошо и выполняет
свою функцию, но за счет того что у UNIX-like систем был открытый исходный код, их часто использовали для разработки.

В настоящее время Unix-системы признаны одними из самых исторически важных операционных систем, огромное количество
серверов работают на Unix-подобных системах, огромное чисто инструментов разработки в первую очередь ориентировано на
такие системы, закрытость исходного кода Windows сыграла с ним злую шутку.

> POSIX - это некий стандарт, договоренность как должен выглядеть интерфейс взаимодействия с операционной системой,
> чтоб программы написанные для Unix можно было на ней запускать.

Например: Windows Subsystem for Linux (WSL) — прослойка совместимости, впервые появившаяся в Windows 10 и реализующая
[API](https://ru.wikipedia.org/wiki/API) ядра Linux поверх Windows. Иными словами снаружи выглядит как Unix-подобная,
общаться можно как с Unix-подобной, а что там под капотом - не важно. Согласитесь, сам факт того, что это Windows
пришлось внедрять к себе слой совместимости с Unix-подобными системами, а не наоборот, на что-то намекает.

Надеюсь после этой вводной стало понятно почему ITшники часто предпочитают продукты компании Apple: MacOs это
Unix-совместимая система, при этом поставленная на неплохую железку с хорошей поддержкой и удобным красивым интерфейсом,
чего в опенсорсных [Linux](https://ru.wikipedia.org/wiki/Linux) (например Ubuntu) иногда не хватает.

Теперь к инструментам и как и установить.

### **Homebrew**

Для начала установите **Homebrew** [[для MacOs](https://brew.sh/) ; [для Linux](https://docs.brew.sh/Homebrew-on-Linux)], он значительно
облегчит процесс установки всего остального, с ним установка практически любого ПО будет выглядеть как вызов одной
команды из терминала:

```shell 
$ brew install {some_software}
```

### Node.js

[**Node.js**](https://nodejs.org/en/learn/getting-started/introduction-to-nodejs) - это интерпретатор JavaScript, то что будет читать и исполнять написанный нами код. Ее лучше устанавливать при
помощи [**nvm**](https://github.com/nvm-sh/nvm?tab=readme-ov-file#installing-and-updating)
(node version manager). nvm - это то что позволит нам переключаться между различными версиями node.js, так как
некоторые пакеты могут работать только на определенных версиях интерпретатора. Если бы не было nvm, нам бы каждый раз
пришлось переустанавливать node.js самостоятельно, при этом подчищая артефакты в виде файлов, конфигураций и
переменных, оставленных в системе предыдущей версией (занятие не из приятных). nvm умеет делать за нас всю эту
работу. Устанавливаем nvm так:

```shell
$ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
```

Эта команда скачает установочный скрипт и запустит его. После этого нужно добавить информацию о запускаемом файле nvm в
```~/.bash_profile```. Это конфигурационный файл вашей командной оболочки, при каждом запуске она будет считывать
информацию о пути до исполняемого файла оттуда.

```shell
$ echo 'export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm' >> ~/.bash_profile
```

Затем закрываем и открываем заново терминал и проверяем что nvm установился (это кстати называется smoke test, проверка
корректного функционирования кода по косвенным признакам. Если есть "дымок", то есть утилита вызывается без ошибок и
корректно возвращает свою версию, значит скорее всего костер горит как надо):

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

nvm скачает 20 версию, установит исполняемый файл в нужную директорию и скажет вашей машине использовать именно ее (
дополнит системную переменную $PATH путем до исполняемого файла, чтоб он при вызове ккоманды ```$ node``` указывал на
исполняемый файл нужной версии). Проверить что в первом приближении все корректно работает же можно вызвав node с
ключом, запрашивающим текущую версию:

```shell
$ node -v
20.17.0
```

В моему случае была скачана и установлена версия 20.17.0 . Полный список команд можно посмотреть так:

```shell
$ nvm -h
```

### **Пакетный менеджер**

На самом деле тут мы ничего дополнительно ставить не будем. **npm** уже давно ставится автоматически с установкой node.
Раньше было по-другому, но эти времена прошли.

> В самом начале мы ставили **homebrew**, утилиту, которая позволяет скачивать и устанавливать нужную версию ПО на вашу
> операционку.
> Пакетный менеджер npm делает приблизительно то же самое, только с отдельными скриптами js (модулями) для конкретного
> проекта,
> которые кто-то написал и залил в общее хранилище. Свой модуль в npm registry можете залить и вы.
> Каждый проект который вы пишете будет скорее всего использовать сторонние библиотеки разных версий.
> Скачивать нужные версии, проверять их совместимость и добавлять к проекту будет как раз пакетный менеджер.

Есть и альтернативные пакетные менеджеры, но их я сейчас даже не буду упоминать, о них мы будем говорить позднее.

### GIT

[Git](https://git-scm.com/) - это система контроля версий. Мы захотим не просто писать код, а где-то его хранить, что-то добавлять к нему,
видоизменять, откатываться к
предыдущим версиям, просматривать историю изменений, работать над одним проектом/файлом со своими коллегеами по
команде/друзьями. Все это позволяет делать git. Установить можно так:

```shell
$ brew install git
```

Кроме того, сразу зарегистрируйтесь на сайте [github.com](github.com)

> GitHub — крупнейший веб-сервис для хостинга IT-проектов и их совместной разработки. Cервис основан на системе контроля
> версий Git. В нем вы сможете хранить свои проекты, давать до них доступ другим разработчикам и много еще чего.

Сконфигурируйте git, указав имя и почту, например:

```shell
$ git config --global user.name "My Name"
$ git config --global user.email my@email.com
```

И сгенерируй SSH ключ. Это нужно для того чтобы при копировании кода в github не нужно было каждый раз вводить account и
password. Команда генерирует пару ключей: публичный и приватный. Приватный нужно хранить в секрете, публичный можно
раскрывать добавлять в приложения, к которым вы хотите иметь доступ.

Откройте терминал и выполните команду:

```shell
$ $ ssh-keygen -t rsa
```

На консоль будет выведен следующий диалог:

```shell
Enter file in which to save the key (/home/user/.ssh/id_rsa):
```

Нажмите на клавишу Enter. Далее система предложит ввести кодовую фразу для дополнительной защиты SSH-подключения:

```shell
Enter passphrase (empty for no passphrase):
```

Этот шаг можно пропустить. При ответе на этот и следующий вопрос просто нажмите клавишу Enter.
После этого ключ будет создан, а на консоль будет выведено сообщение о подтверждении.

Далее выполните в терминале команду:

```shell
$ cat ~/.ssh/id_rsa.pub
```

На консоль будет выведен ключ. Скопируйте его и добавьте в насройках вашего GitHub аккаунта по пути:
Settings

### IDE

IDE - Integrated Development Environment, или редактор кода с наворотами. Какую выбрать мы разбирали [тут](/TheTechTales/posts/ide.html).

### Docker

Docker - это система контейнеризации. Это то что позволит нам обернуть приложение в некоторую оболочку - контейнер,
чтобы его можно было запускать изолирвоанно от других процессов на нашей ОС, легко переносить
в другое окружение, горизонтально масшабировать. Контейнер похож на виртуальную машину, но все-таки от нее
отличается. Приложение внутри контейнера живет как герой Джима Керри в фильме "Шоу Трумана".  
Настройкой Docker сейчас заниматься не будем, мы вернемся к нему позднее.
На MacOs docker ставится вместе с desktop ui интерфейсом, который так и называется Docker Desktop. Установить его можно
следующей командой:

```shell
$ brew install --cask docker
```





