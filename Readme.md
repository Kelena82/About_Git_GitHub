
# Введение в Git и GitHub

Ниже представлена краткая инструкция о том, как начать работу с GitHub, используя Git.
Работать с Git можно через командную строку либо графический интерфейс какой-либо IDE, например, VS Code. 
В данном руководстве будет использоваться способ через консоль.
Для этого нужно установить специальный консольный инструмент для Windows, который называется **Git Bash**. Есть несколько способов установки. Мы рекомендуем пакет **Git for Windows**. Он установит не только Bash, но и сам Git. Вот что нужно сделать:
1.	Перейдите на эту страницу официального сайта [Git](https://git-scm.com/download/win "Пакет Git for Windows").
2.	Скачайте одну из двух версий из категории Standalone Installer (англ. «автономный установщик»). Узнать тип вашей системы Windows можно в настройках.
3.	Запустите программу установки. Обратите внимание, куда будет установлен Git. Обычно это директория C:\Program Files\Git.
4.	Проверьте, что в списке устанавливаемых программ стоит галочка напротив пункта Git Bash Here — это позволит открывать консоль с Git в любой папке.
5.	Далее установщик предложит много опций. Для нашего курса достаточно оставить все настройки по умолчанию. Несколько раз нажмите Next (англ. «далее»), пока не начнётся процесс установки.
6.	После окончания установки нажмите Finish (англ. «завершить»).
7.	Теперь на вашем компьютере есть не только командная строка, но и Git.
## Первый запуск Git Bash
Запустите программу *Git Bash*. Сделать это можно двумя способами. Можно ввести название программы в окно поиска на панели задач (через Пуск).
А можно открыть директорию, в которую был установлен Git. Обычно это директория *C:\Program Files\Git\bin*. Перейдите в *bin* и запустите файл *bash.exe*.
Если вы видите консоль, значит, установка прошла успешно. 
Символ доллара ($) означает, что программа ждёт ваших команд.
## Настройка Git
Работа с файлом настройки .*gitconfig*<br>
Сейчас вы работаете в одиночку, но в дальнейшем вам может понадобиться использовать Git в команде. Чтобы участникам проекта было понятно, кто и какие изменения вносил, нужно представиться и указать имя пользователя и адрес электронной почты.
Вы можете указать любую электронную почту и любое имя. Сделать это можно с помощью команды *git config* (от англ. configuration — «конфигурация», «настройка») с ключом --*global* (англ. «глобальный»). При этом не имеет значения, в какой директории вы находитесь прямо сейчас: вызов *git config –global* сработает везде.
В качестве значения *user.name* нужно указать своё имя или никнейм. Для настройки параметра *user.email* указывают электронную почту.<br>
*$ git config --global user.name "User Namovich"* <br>
\# имя или ник нужно написать латиницей и в кавычках

*$ git config --global user.email username@yandex.ru* <br>
\# здесь нужно указать свой настоящий email <br>
Все глобальные настройки Git хранит в файле .gitconfig в домашней директории. Команда запишет в этот файл указанные имя и почту. Чтобы убедиться в этом, можно вызвать команду для чтения файлов.<br>
*$ cat ~/.gitconfig* <br>
Другой способ проверки — вывести содержимое файла конфигурации Git той же командой git config с флагом --list (англ. «список»).<br>
*$ git config --list* <br>
В ответ командная строка покажет текущие значения настроек.<br>
user.name=Username<br>
user.email=username@yandex.ru <br>

## Инициализируем репозиторий
Сделать папку репозиторием — *git init*<br>
Чтобы Git начал отслеживать изменения в проекте, папку с файлами этого проекта нужно сделать **Git-репозиторием** (от англ. repository — «хранилище»). Для этого следует переместиться в неё и ввести команду git init (от англ. initialize — «инициализировать»).
Например, создайте папку first-project и сделайте её Git-репозиторием: перейдите в неё с помощью команды cd и выполните git init.<br>
*$ cd ~/dev/first-project*  <br>
\# перешли в нужную папку<br>

*$git init* <br>
\# создали репозиторий <br>
Вы можете создать папку в любом месте на компьютере. Но в этом случае не забывайте менять в наших примерах путь ~/dev/first-project на тот, который ведёт к вашей папке. Помните, что не рекомендуется создавать репозиторий Git внутри другого Git-репозитория. Это может вызывать проблемы с отслеживанием изменений.<br>
## «Разгитить» папку, если что-то пошло не так, — rm -rf .git
Если вы случайно сделали Git-репозиторием не ту папку, её можно «разгитить». Для этого нужно удалить скрытую подпапку .git.<br>
*$ cd <папка с репозиторием>* <br>
\# перешли в папку<br>

*$ rm -rf .git* <br>
\# удалили подпапку .git <br><br>
Разберём подробнее, что такое -rf:<br>
•	ключ -r (от англ. recursive — «рекурсивно») позволяет удалять папки вместе с их содержимым;<br>
•	ключ -f (от англ. force — «заставить») избавит вас от вопросов вроде «Вы точно хотите удалить этот файл? А этот? И этот тоже?».<br>

Будьте осторожны: в подпапке .git хранится история изменений. Если удалить .git, то вся история проекта будет стёрта без возможности восстановления — останется только последняя версия файлов.
## Проверить состояние репозитория — git status<br>
После инициализации репозитория first-project запустите команду *git status* (от англ. status — «статус», «состояние») — она показывает текущее состояние репозитория.<br>
Команда git status выведет:<br>
•	название текущей ветки: On branch master или On branch main;
•	сообщение о том, что в репозитории ещё нет коммитов: No commits yet;
•	сообщение, которое говорит: «чтобы что-нибудь закоммитить (то есть зафиксировать), нужно сначала это создать» — nothing to commit (create/copy files and use "git add" to track).

В отличие от *git init*, команду *git status* используют часто. В любой непонятной ситуации стоит посмотреть состояние (статус) репозитория, а потом решить, что делать дальше.
## Добавляем файлы в репозиторий<br>
Создайте файлы todo.txt и readme.txt в папке first-project и запустите git status, чтобы посмотреть, что изменилось.<br>
*$ touch todo.txt*<br>
*$ touch readme.txt*<br>
\# создали файлы todo.txt и readme.txt<br>

*$ git status* <br>
\# проверили статус <br>
Git сообщит, что в папке first-project есть untracked files (от англ. track — «следить», untracked — «неотслеженный», «неотслеживаемый») — ещё не отслеживаемые файлы readme.txt и todo.txt.<br>
Состояние *untracked* значит, что Git ещё не хранит информацию о версиях файла и не может отследить, как он изменялся.
Сейчас в first-project два файла. <br>
Команда git add  - подготовить файлы к сохранению. Мы хотим отслеживать состояние обоих, поэтому можем использовать команду git add --all (от англ. add — «добавить» + от англ. all — «всё»). Ключ, или флаг, --all позволяет подготовить к сохранению все файлы в репозитории. <br>
*$git add --all*<br>
 \# подготовили к сохранению все файлы в репозитории<br>
*$ git status* <br>
\# проверили статус <br>
Добавлять файлы можно и по одному, без ключа --all.<br>
*$ git add todo.txt*<br>
*$ git add readme.txt*<br>
*$ git status* <br>
Также можно добавить текущую папку целиком — в этом случае все файлы в ней тоже будут добавлены. Обратиться к текущей папке в Bash позволяет точка (.).<br>
*$ git add .* <br>
\# добавить всю текущую папку <br>
*$ git status* <br>
Вы можете использовать любой из этих вариантов — результат будет одинаковый. <br>
Файлы, которые отмечены зелёным, теперь отслеживаются и готовы к сохранению. Но сохранения пока не произошло, потому что команда git add только запоминает текущее содержимое (контент) файла.
## Делаем первый коммит
Коммит — это одна из основных сущностей в Git (и в других системах контроля версий). Коммит гарантирует, что изменения будут сохранены в истории и при необходимости к ним можно будет «откатиться». Это как если бы вы могли выполнить операцию Ctrl+Z для целой папки (репозитория).
В этом уроке вы сделаете свой первый коммит.<br>
**Выполнить коммит — git commit**<br>
Сделать коммит можно командой git commit c ключом -m (от англ. message — «сообщение»), который присваивает коммиту сообщение.
Обычно в таком сообщении поясняется, в чём именно состояли изменения. Это как заметки на полях: благодаря им проще читать и понимать текст. Сообщение коммита выполняет те же функции — улучшает понимание и упрощает навигацию. Оно пишется после ключа -m в кавычках.
Например, перейдите в папку first-project и выполните коммит со следующим комментарием.<br>
*$ git commit -m 'Мой первый коммит!'* <br>
После нажатия Enter текущая версия файлов будет сохранена в репозитории с сообщением Мой первый коммит!. <br>
**Коммит** (по названию команды git commit) — это по сути список файлов с их контентом.
Команда git commit выведет информацию о коммите.

*$ git log* - просмотреть историю коммитов

## Git и платформы для удалённой работы

Git и GitHub — это два разных проекта, которые развиваются независимо друг от друга. 
*Git*: 
- консольный инструмент для работы с локальными и удалёнными репозиториями;
- проект с открытым исходным кодом.
*GitHub*:
- платформа для размещения удалённых репозиториев;
- принадлежит компании Microsoft.
Кроме GitHub, есть и другие платформы для командной работы. Например, GitLab и Bitbucket, которые тоже позволяют работать с Git. 
У каждой из этих платформ свои особенности и дополнительная функциональность: 
- GitLab можно развернуть в виде сервера в приватной сети; 
- Bitbucket — продукт компании Atlassian, поэтому

### Можно ли делать сложные проекты без GitHub?
Такие платформы, как GitHub, Bitbucket и другие, значительно упрощают процесс командной работы. Но при этом Git может использоваться и без них для создания даже больших проектов. 
Например, ядро Linux — самой популярной операционной системы для серверов, телефонов и суперкомпьютеров — разрабатывают с помощью патчей (от англ. patch — «заплата», «лоскут»). Это файлы, которые содержат отличия исходной версии от последующих. 
Такие патчи рассматривает и объединяет в основную версию ядра лично Линус Торвальдс — создатель Linux и Git. Это происходит без использования средств платформ вроде GitHub.

## Регистрация на GitHub
Вы познакомились с платформой GitHub — пришло время зарегистрироваться на ней. Поехали!
*Инструкция по регистрации:*
1.	В правом верхнем углу главной страницы [GitHub](https://github.com/) нажмите на Sign up (англ. «зарегистрироваться»).    
2.	На экране будут последовательно появляться поля для ввода. Введите адрес электронной почты (англ. Enter your email). Придумайте пароль (англ. Create a password). Введите имя пользователя (англ. Enter a username).
3.	Платформа спросит, хотите ли вы получать на почту рассылку с обновлениями и новостями (англ. Would you like to receive product updates and announcements via email?). Введите y, если хотите получать рассылку, или n, если не хотите.
4.	Нажмите кнопку **Continue** (англ. «продолжить»).
5.	GitHub предложит вам пройти капчу. Сделайте это.
6.	После прохождения капчи нажмите **Create account** (англ. «создать аккаунт»).
7.	Введите короткий код, который будет отправлен на указанный вами почтовый адрес.
Поздравляем! Вы успешно зарегистрировались на крупнейшем веб-хостинге проектов GitHub. Теперь у вас есть возможность работать бок о бок с миллионами профессионалов по всему миру, обмениваться идеями и развиваться.

## Создаём удалённый репозиторий

###Инструкция по созданию репозитория на GitHub
1.	Зайдите в свой профиль по ссылке *https://github.com/username*, где username — имя, которое вы указали при регистрации. Эта страница — презентация вас и ваших проектов. Её видят другие пользователи. Надпись You don't have any public repositories yet (англ. «у вас пока нет публичных репозиториев») сообщает, что пока у вас нет проектов. 
2.	Создайте репозиторий. Для этого перейдите на вкладку *Repositories* (англ. «репозитории»), а затем нажмите на зелёную кнопку New (англ. «новый») справа. 
3.	Открылось окно создания нового репозитория. Назовите его *first-project*. Название удалённого репозитория необязательно должно совпадать с именем папки проекта у вас на компьютере. Но чтобы не путаться, будем называть их одинаково. Другие поля вам пока не понадобятся. Смело нажимайте на зелёную кнопку Create repository (англ. «создать репозиторий») внизу. 

Готово! Удалённый репозиторий создан. Страница с ним открывается автоматически. 

Осталось связать удалённый репозиторий с локальным, который уже есть на вашем компьютере. 

## Синхронизация репозиториев<br>
**Что такое SSH. Генерируем SSH-ключ**<br>
Когда компьютеры обмениваются данными в сети, они следуют сетевым протоколам (англ. network protocols) — правилам обмена данными между компьютерами.
Один из наиболее распространённых сетевых протоколов — SSH (от англ. Secure Shell Protocol). Он обеспечивает безопасный обмен данными в сети. С помощью этого протокола можно получать данные с удалённого компьютера или отправлять их на него. Трафик шифруется, поэтому протокол безопасен.
SSH использует пару ключей для обеспечения безопасности — публичный и приватный: <br>
•	Приватный ключ (англ. private key) хранится только на вашем компьютере и не должен передаваться кому-либо ещё. Он используется для расшифровки данных.<br>
•	Публичный ключ (англ. public key) доступен всем и используется для шифрования данных. Они могут быть расшифрованы парным приватным ключом.<br>
Только вы можете расшифровать данные с помощью приватного ключа, но любой владелец публичного ключа может их для вас зашифровать. Эти два ключа связаны и образуют SSH-пару. В будущем вы наверняка будете использовать их для взаимодействия с GitHub и другими удалёнными серверами.<br>
**Проверка наличия SSH-ключа**<br>
Прежде чем генерировать SSH-ключи, убедитесь, что у вас их ещё нет. По умолчанию директория с SSH-ключами находится в домашней директории пользователя. Перейдите в неё.<br>

*$ cd ~* <br>
\# перешли в домашнюю директорию <br>
Обычно SSH-ключи находятся в директории .ssh/. Проверить наличие этой директории и файлов в ней можно с помощью следующей команды.<br>

*$ ls -la .ssh/* <br>
\# вывели список созданных ключей <br>
Если папка пустая или её нет, всё в порядке. 
Если есть файлы с похожими названиями, SSH-ключи уже создавались:<br>
•	id_dsa.pub;<br>
•	id_ecdsa.pub;<br>
•	id_ed25519.pub;<br>
•	id_rsa.pub.<br>
Если вы не создавали эти файлы, удалите их все.<br>
**Инструкция по генерации SSH-ключа**<br>
1.	Для генерации SSH-пары можно использовать программу ssh-keygen. Откройте терминал и введите следующую команду.<br>
*$ ssh-keygen -t ed25519 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"*<br>
Используйте электронную почту, к которой привязан ваш GitHub-аккаунт.<br>
Если вы видите сообщение об ошибке, то, скорее всего, ваша система не поддерживает алгоритм шифрования ed25519. Ничего страшного: используйте другой алгоритм.<br>

*$ ssh-keygen -t rsa -b 4096 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"*<br>
После ввода отобразится такое сообщение.

> Generating public/private rsa key pair. # сгенерированы публичный и приватный ключи 
2.	Укажите место хранения ключей. Простой вариант — сделать домашний каталог пользователя путём по умолчанию. Для этого нажмите Enter.
3.	Программа запросит кодовую фразу (англ. passphrase) для доступа к SSH-ключу. Вы можете оставить поле пустым. Для этого нажмите Enter, а затем ещё раз Enter для подтверждения.<br>
 **Быть или не быть кодовой фразе — вот в чём вопрос**<br>
Как бы странно ни звучало, кодовая фраза — это «пароль от ключа». Представьте, что SSH-ключ лежит в шкатулке. А на самой шкатулке — кодовый замок, который открывается кодовой фразой.
Многие пользователи Git не используют кодовую фразу для защиты своего SSH-ключа. Если такой фразы нет, то её не нужно вводить всякий раз при взаимодействии с удалённым репозиторием.
С другой стороны, применение кодовой фразы усиливает безопасность ключей. Если вы используете эту фразу, ключ будет надёжно защищён в случае несанкционированного доступа к вашему компьютеру.
4.	Готово! Теперь осталось проверить, что ключи действительно сгенерировались. Для этого вызовите эту команду.<br>
*ls -a ~/.ssh*<br>
На экране должны появиться два файла — один с расширением .pub, другой — без. Файл в .pub — публичный, им можно делиться с веб-сайтами или коллегами. <br>
**Файл без расширения .pub — приватный. Ни в коем случае не передавайте его никому!**<br>

**Привязываем SSH-ключ к GitHub** <br>
**Инструкция по связыванию SSH-ключа и GitHub-аккаунта**<br>
1.	Скопируйте содержимое файла с публичным ключом (id_ed25519.pub/id_rsa.pub) в буфер обмена.<br>
Windows<br>
*$ clip < ~/.ssh/id_rsa.pub*   скопировать содержимое ключа в буфер обмена<br>
или<br>
*$ clip < ~/.ssh/id_ed25519.pub*<br>
Если clip не сработает, выведите содержимое файла с помощью <br>
*cat ~/.ssh/id_rsa.pub* <br>
или <br>
*cat ~/.ssh/id_ed25519.pub* <br>
и скопируйте вывод в буфер обмена из консоли.<br>
2.	Перейдите на GitHub и выберите пункт Settings (англ. «настройки») в меню аккаунта (справа).<br>
3.	В меню слева нажмите на пункт SSH and GPG keys.<br>
4.	В открывшейся вкладке выберите New SSH key (англ. «новый SSH-ключ»).<br>
5.	В поле Title (англ. «заголовок») напишите название ключа. Например, Personal key (англ. «личный ключ»).<br>
6.	В поле Key type (англ. «тип ключа») должно быть Authentication Key (англ. «ключ аутентификации»).<br>
7.	В поле Key скопируйте ваш ключ из буфера обмена.<br>
8.	Нажмите на кнопку Add SSH key (англ. «добавить SSH-ключ»).<br>
9.	Проверьте правильность ключа с помощью следующей команды в консоли:<br>

	*$ ssh -T git@github.com*<br>

Если это первый раз, когда вы используете Git, чтобы поделиться проектом на GitHub, появится похожее предупреждение.<br>
The authenticity of host 'github.com (140.82.121.4)' can't be established. ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU. This key is not known by any other names. Are you sure you want to continue connecting (yes/no/[fingerprint])? <br>
Это предупреждение сообщает, что вы никогда не соединялись с сервером GitHub. Поэтому Git не может гарантировать, что сервер является тем, за кого он себя выдаёт.<br>
Для подтверждения подлинности сервер генерирует и публикует ключи SHA256. Вы можете проверить ключи GitHub по этой [ссылке](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints)<br>
Если ключ в предупреждении совпадает с тем, что вы видите на сайте, значит, сервер является действительным. Введите yes, чтобы продолжить. Вы увидите приветствие на экране.<br>
*Hi %ВАШ_АККАУНТ%! You've successfully authenticated, but GitHub does not provide shell access. *<br>

Теперь ваш ключ привязан к GitHub! Если вы установили кодовую фразу для SSH-ключа, её нужно будет вводить для работы с репозиторием.<br>

**Связываем локальный и удалённый репозитории**<br>
Сейчас у вас есть локальный репозиторий first-project, который хранится на вашем компьютере, и удалённый репозиторий на GitHub. Вы сгенерировали SSH-ключ для безопасной работы и теперь готовы связать удалённый репозиторий с локальным.<br>

**Привязать удалённый репозиторий к локальному — git remote add**<br>
Перейдите на страницу удалённого репозитория, выберите тип SSH и скопируйте URL. Кнопка справа позволит сделать это мгновенно.<br>

Откройте консоль, перейдите в каталог локального репозитория и введите команду *git remote add* (от англ. remote — «удалённый» и add — «добавить»).<br>

*$ cd ~/dev/first-project*<br>
*$ git remote add origin git@github.com:%ИМЯ_АККАУНТА%/first-project.git*<br>
Команде необходимо передать два параметра: имя удалённого репозитория и его URL. В качестве имени например будем использовать слово origin. А URL вы скопировали со страницы удалённого репозитория.<br>
 **Как выполнить вставку в командную строку?**<br>
На Windows (в Git Bash) для этого используется сочетание Ctrl+Shift+V.<br>
Также можно нажать правую кнопку мыши и выбрать пункт **Paste**(англ. «вставить») в выпадающем меню.<br>
**origin** (англ. «источник») — стандартный псевдоним, с помощью которого можно обращаться к главному удалённому репозиторию (обычно такой репозиторий один). <br>
**Убедиться, что репозитории связаны, — git remote -v**<br>
*$ git remote -v*<br>
*origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (fetch)*<br>
*origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (push)* <br>
В выводе вы должны увидеть две строчки, аналогичные тем, что показаны выше.<br>
Флаг -v — короткая форма флага --verbose (англ. «подробный»). Он позволяет показать больше информации в выводе.<br>

**Синхронизируем локальный и удалённый репозитории**
Разберём, как выкладывать свои правки на удалённый репозиторий. Но сначала немного о ветках.<br>
**Основная ветка**<br>
Мы упоминали, что каждый коммит сохраняет актуальное состояние файлов. Сами же коммиты хранятся в ветках (англ. branch).
Если коммит — это снимок состояния файлов, то ветка — временна́я шкала, на которой расположены эти снимки. Ветка всегда начинается от одного из коммитов.
В репозитории может существовать сразу несколько веток — параллельных историй изменений. Также они могут соединяться друг с другом.<br>

Самая первая ветка в репозитории появляется автоматически и называется main (англ. «основная») или master. Её имя нужно указывать при отправке коммитов на удалённый репозиторий или при получении их из него.
main или master?<br>
Раньше основная ветка в репозиториях, созданных на GitHub, называлась master, но с 1 октября 2020 года (после волны протестов движения Black Lives Matter) её переименовали в main. 
Во всех репозиториях, созданных раньше этой даты, название основной ветки не поменялось. Поэтому в проектах, которые начали именно с master, и в руководствах по работе с Git вы по-прежнему можете встретить имя master. <br>
**Отправить изменения на удалённый репозиторий — git push**<br>
Вы уже прошли весь «цикл коммита»: подготовили файлы с помощью *git add*, закоммитили их с комментарием командой *git commit -m*. Осталось загрузить содержимое локального репозитория на GitHub. За это отвечает команда *git push* (от англ. push — «толкать»).
В первый раз эту команду нужно вызвать с флагом -u и параметрами origin (имя удалённого репозитория) и main или master (название текущей ветки). Флаг -u свяжет локальную ветку с одноимённой удалённой. Как вы связывали локальный и удалённый репозитории в предыдущем уроке, так же и здесь нужно дополнительно связать ветки.

*$ git push -u origin main* <br>
\# Если команда приведёт к ошибке, попробуйте заменить main на master. <br>

При взаимодействии с удалёнными репозиториями Git выводит в консоль отладочную информацию: количество объектов (файлов), которые отправляются на сервер, информацию о прогрессе сжатия и записи и так далее.<br>
Если вы указывали кодовую фразу при настройке SSH-ключей, её нужно будет ввести.<br>
Зайдите в репозиторий first-project на GitHub. Вы увидите, что в репозитории появились файлы с изменениями.<br>

В дальнейшем при работе с удалённым репозиторием флаг -u можно опустить и писать просто *git push*.
## Работа с графическим интерфейсом GitHub<br>
GitHub предоставляет удобный интерфейс для работы с репозиторием. Например, нажмите на кнопку commit в правой части страницы, чтобы просмотреть все коммиты в репозитории.

Откроется окно с коммитами и их авторами. 
Сообщение коммита в репозитории тоже является ссылкой. 
Перейдите по ссылке, кликните на текст последнего коммита над репозиторием — так вы сможете увидеть все изменения, которые были внесены в репозиторий в этом коммите.

**Файл README.md**
Чтобы другие пользователи, а также потенциальные клиенты или работодатели могли понять, что представляет собой проект, его нужно описать. Такое описание принято указывать в файле README.md.

##Навигация по коммитам

###Хеш — идентификатор коммита<br>
Информация о коммите — это набор данных: когда был сделан коммит, содержимое файлов в репозитории на момент коммита и ссылка на предыдущий, или родительский (англ. parent), коммит.
Git хеширует (преобразует) информацию о коммите с помощью алгоритма **SHA-1** (от англ. Secure Hash Algorithm — «безопасный алгоритм хеширования») и получает для каждого коммита свой уникальный хеш — результат хеширования.
Обычно **хеш** — это короткая (40 символов в случае SHA-1) строка, которая состоит из цифр 0—9 и латинских букв A—F (неважно, заглавных или строчных). Она обладает следующими важными свойствами:<br>
•	если хеш получить дважды для одного и того же набора входных данных, то результат будет гарантированно одинаковый;<br>
•	если хоть что-то в исходных данных поменяется (хотя бы один символ), то хеш тоже изменится (причём сильно).<br>
Чтобы убедиться в этом, можно поэкспериментировать с SHA-1 на этом [сайте](https://emn178.github.io/online-tools/sha1.html "SHA-1") — попробуйте ввести в поле input (англ. «ввод») разные символы, слова или предложения и понаблюдайте, как меняется хеш в поле output (англ. «вывод»).<br>
Хеш — основной идентификатор коммита<br>
Git хранит таблицу соответствий хеш → информация о коммите. Если вы знаете хеш, вы можете узнать всё остальное: автора и дату коммита и содержимое закоммиченных файлов. Можно сказать, что хеш — основной идентификатор коммита.
При работе с Git хеши будут встречаться вам регулярно. Их можно будет передавать в качестве параметра разным Git-командам, чтобы указать, с каким коммитом нужно произвести то или иное действие.
Все хеши и таблицу *хеш → информация о коммите* Git сохраняет в служебные файлы. Они находятся в скрытой папке **.git** в репозитории проекта.

