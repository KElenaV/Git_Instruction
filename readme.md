### Навигация

* **pwd** - показывает рабочую папку
* **ls** - показывает файлы и папки в текущей папке
* **cd** - команда перехода в другую дирректорию. Если папка находится в рабочем пространстве, то просто указывается ее имя, если в другом месте, то нужно указать подробный адрес
* **cd ..** - переход на уровень выше
* **cd /** - переход в корневую директорию
* cd ~ - переход в домашнюю директорию

### Работа с файлами и папками

* **..** - обращение к родительской папке

### Создание
* **touch** - создает файл (желательно указывать расширение файла при создании) - если нужно создать несколько файлов указать их через пробел
* **mkdir** - создает папку

### Копирование - перемещение
* **cp fileName.txt directory** - копирует файл в указанную директорию
* **mv fileName.txt directory** - перемещает файл в указанную директорию

### Чтение
* **cat fileName.txt** - распечатывает содержимое текстового файла в консоль

### Удаление
* **rm** - удаление файла
* **rmdir** - удаление папки
* **rm -r** - удаление папки со всем ее содержимым

### Исполнение файла
* **chmod +x fileName.sh** - эта команда делает файл исполняемым (расширение .sh обозначает исполняемый скрипт)
* **./fileName.sh** - исполнение скрипта, находящегося в рабочей директории

### Полезные возможности
* Можно в 1 строчке задать несколько команд через &&
* С помощью стрелок вверх-вниз можно перемещаться по буферу, хранящему все предыдущие команды
* Tab - 1 или 2 щелчок выводит подсказки

### Работа с Git
* **git config --global user.name "Name"** - задать имя пользователя
* **git config --global user.email email** - указать электронную почту

### Репозиторий
* **git init** - сделать папку-проект репозиторием. Нужно быть внутри папки. После этого появится слово main или master
* **git branch -m master main** - изменить имя корневой папки с master на main
* **rm -rf .git** - удалить папку git. В этой папке хранится вся история изменений. Если ее удалить вся история проекта будет стерта. Останется лишь последняя версия файлов.
* **git status** - текущее состояние репозитория - здесь не отображаются игнорируемые файлы
* **git status --ignored** - текущее состояние репозитория с учетом игнорируемых файлов
* **git add --all** - подготовит все файлы для сохранения в репозиторий
* **git add fileName.txt** - подготовит конкретный файл для сохранения в репозиторий
* **git commit -m "Comment"** - сохраняет текущую версию файлов в репозиторий с комментарием
* **git log** - выводит на консоль все коммиты в обратной хронологии (чтобы выйти из режима журнала - нажать q / ctrl+q / Esc)
* **git log -p** - выводит на консолько все коммиты с подробной информацией об изменениях в них
* **git log --patch** - то же самое, что и выше
* **git log --stat** - отображает сокращенную статистику изменений - дата, пользователь, измененные файлы, количество изменений (количество удалений / количество вставок)
* **git log --oneline** - сокращенный список коммитов - отображаются только первые несколько символов хэша каждого коммита и комментарии - это удобно, когда уже сотни коммитов и нужно быстро найти нужный. Надпись (HEAD -> master) указывает на самый новый (последний) коммит
* **git log --graph --online main branchName** - если в командной строке указать несколько веток (здесь main/branchName) - она выведет их все. С флагом **--graph** Git визуально представит в консоли ветки с помощью *палочек* и *звездочек*. 

### SSH ключи для шифрования данных (приватный и публичный-pub)
* **ls -la .ssh/** - выводит список созданных ключей - нужно находится в директории, где размещены ключи - по умолчанию это домашняя директория
* **ssh-keygen -t ed25519 -C "email"** - генерирует ключи, почта д.б. та к которой привязан аккаунт GitHub
* **ssn-keygen -t rsa -C "email"** - то же самое, но при другом алгоритме шифрования

После ввода данной команды появится сообщение: Enter a file... где нужно указать место хранения ключей. Если нажать ввод - ключи сохранятся в домашний каталог. Далее будет 2 сообщения, запрашивающих кодовую фразу и ее подтверждение - можно ввести код, а можно просто нажать ввод, тогда кода не будет.
* **ls -a ~/.ssh** - проверка сгенерированы ли ключи в домашней директории

### Привязка ключей к GitHub
* **clip < ~/.ssh/id_ed25519.pub** - скопировать содержимое файла (Windows)
* **clip < ~/.ssh/id_rsa.pub** - то же самое для другой системы шифрования
* **cat ~/.ssh/id_ed25519.pub** - если предыдущие команды не работают, можно с помощью данной команды распечатать файл на экран и скопировать его вручную.

Перейти в GitHub - Settings - SSH and GPG keys - New SSH key.
* **Title** - написать название ключа (напр. Personal key)
* **Key type** - Authentication
* **Key** - вставить скопированное ранее содержимое файла
* **Add SSH Key**

### Проверка правильности ключа и подтверждение подлинности сервера
* **ssh -T git@github.com** - проверка правильности ключа. Возможно, появится сообщение о том, что нужно подтвердить подлинность сервера. Это делается сверкой сгенерированного ключа SHA256 с возможными ключами, которые можно посмотреть на сайте docs.GitHub.com - Authentication - Account security - SSH key fingerprints - если ключи совпадают - нажать yes

### Привязка удаленного репозитория к локальному
1. Зайти в удаленный репозиторий - Нажать HTTP - Скопировать адресную строку справа
2. В консоли перейти в каталог локального репозитория
3. Ввести git remote add origin адресная строка из п.1 (вставку можно выполнить через контекстное меню - ПКМ, или Ctrl+Shift+V)

* **git remote -v** - если репозитории связались, то появится 2 строчки, заканчивающиеся на (fetch) (push)

### Отправить изменения на удаленный репозиторий
* **git push** - загружает содержимое локального репозитория на GitHub
* **git push -u origin main(or master)** - при первой отправке содержимого с локального на удаленный репозиторий (-u флаг (иначе еще может выглядеть так --set-upstream)) связывает локальную и удаленную ветки

Многие команды Git принимают в качестве параметра хеш коммита. Если нужно передать последний коммит, то вместо его хэша можно просто написать слово HEAD - Git поймет, что вы имели в виду последний коммит.

### Статусы файлов в Git
1. **Untracked** - Git знает о существовании файла, но не следит за изменениями в нем. Это новый файл.
2. **Tracked** - все файлы после git commit и git add, т.е. те в которых отслеживаются изменения.
3. **Staged** - подготовленный - после выполнения команды git add (то же что и indexed или cached).
4. **Modified** - измененный - Git сравнил содержимое файла с последнего сохранения и нашел отличия.

 Большинство файлов в проекте будут в состоянии **tracked** (т.е. закомичены и не изменены после коммита). Это состояние не отражается через **git status**
* **git status** содержит инструкцию-подсказку того, что можно сделать для смены состояния файла 

### Оформление коммитов
* Сообщение д.б. коротким (не больше 72 символов - такую длину можно увидеть вызвав **git log --oneline**) и информативным для легкости чтения
* В начале коммита можно ставить уточнение типа изменений (feat - новая функциональность, fix - исправление, м.б. и другие) 
* В скобках () - не обязательно - существительное, указывающее часть кодовой базы, которую затронул коммит
* ! - если нужно привлечь внимание к коммиту
* Далее двоеточие и краткое описание после пробела
* Тело описания (если требуется более подробная информация) должно отделяться от короткого описания одной пустой строкой.
* Подвал м.б. представлен после тела через 1 пустую строчку и должен содержать мета-информацию о коммите, например связанные запросы, обсуждения, изменения нарушающие обратную совместимость. По 1 мета-информации на строчку.
* Изменения, нарушающие обратную совместимость д. быть либо в начале тела, либо в начале подвала и начинаться с заглавных BREAKING CHANGE
* Текст д.б. написан нерегистрозависимым способом - маленькими буквами
* Также в коммите можно напрямую указывать №задачи (#номер задачи), которую тот решил - т.о. GitHub свяжет коммит и задачу
* Рекомендуется использовать глаголы в повелительном наклонении (Use library, Исправить ошибку)

### Как исправить коммит
* **git commit --amend --no-edit**
 --amend не создает новый коммит, а дополняет последний. Например, добавляются файлы или вносятся изменения в содержимое файлов. Коммит останется тот же, но его хэш-тег изменится, т.к. поменялось содержимое коммита.
--no-edit оставляет сообщение коммита без изменения
* **git commit -m "Message"** 
 Если понадобилось изменить сообщение, при этом не обязательно менять содержимое файлов.
Если забыть указать у команды 1 из флагов (--no-edit / -m) - откроется текстовый редактор, чтобы отредактировать сообщение коммита вручную. Можно просто закрыть его.

### Как откатиться назад
### Откатить добавленный файл (restore - "восстановить")
* **git restore --staged file.txt** переводит файл из staged обратно в untracked/modified
* **git restore --staged .** если нужно сбросить всю текущую папку
### Откатить закомиченный файл (reset - "сброс, обнуление")
* **git reset --hard hash** - хэш номер коммита на который мы хотим вернуться можно найти с помощью *git log --oneline*
Очень осторожно использовать эту функцию т.к. файлы после нее также возвращаются к тому состоянию, в котором были в момент возвращенного коммита или даже удалится, если его не было на тот момент. Есть риск удалить что-то нужное, т.к. потеряются все более поздние от возвращаемого коммиты.
### Откатить изменения, которые не попали ни в staging, ни в коммит
* **git restore file.txt** - откатывает назад изменения файлов, которые находятся в статусе modified. Изменения в файле откатятся до последней версии, которая была сохранена через git commit или git add

### Просмотр изменений в файлах
* **git diff** - сравнивает последнюю закоммиченную версию файла с текущей (измененной) версией в статусе modifie
В выводе информации есть строчка похожего содержания @@ -15,7 +15,7 @@ , где цифра 15 означает с какой строки начинается сравнение, а вторая сколько строк сравнивалось. Здесь сравнивались 7 строк, начиная с 15. Это удобно для ориентирования в большом коде.
* **git diff** по умолчанию не показывает изменения в staged файлах, только в modified
* **git diff --staged** чтобы увидеть изменения в staged файлах
* **git diff hash1 hash2** - сравнивает содержимое 2 закомиченных файлов. В качестве hash указать коды коммитов, отображаемые при вызове 
*git log --oneline*. Последний коммит можно указывать не кодом, а словом HEAD. Порядок хэш-аргументов в запросе меняет хронологию изменений.
* **git diff** по умолчанию не показывает изменения в staged файлах, только в modified
* **git diff --staged** чтобы увидеть изменения в staged файлах
* **git diff hash1 hash2** - сравнивает содержимое 2 закомиченных файлов. В качестве hash указать коды коммитов, отображаемые при вызове *git log --oneline*. Последний коммит можно указывать не кодом, а словом HEAD. Порядок хэш-аргументов в запросе меняет хронологию изменений.
- -/красный цвет - то, что удалилось
- +/зеленый цвет - то, что добавилось
- черный цвет без знака - контекст, чтобы сориентироваться в расположении изменений в файле

### Добавление текста в файл через консоль
* **echo "Text" >> file.txt** - вставляет написанный в кавычках текст в указанный файл в конец
* **echo "Text" > file.txt** - вставляет текст в указанный файл предварительно стерев предварительно все содержимое файла - т.е. перезаписывает файл
* если указанного файла не существует - он создастся

### Игнорирование файлов Git
* необходимо создать файл *.gitignore* и записать в него названия игнорируемых файлов. Правила из .gitignore применяются только к новым файлам. Если файлы уже staged|commited .gitignore не будет к ним применяться. Сам файл *.gitignore* также стоит закомитить.

### Правила оформления
1. Символ решетки в начале строки делает ее невидимой для .gitignore - воспринимается как комментарий
2. .DS_Store - .gitignore будет игнорировать все файлы такого формата не только в корне репозитория, но и во всех вложенных папках
3. Символ звездочки соответствует любой строке, включая пустую. Например: 
* звездочка.jpeg - игнорируются все файлы с расширением jpeg
* docs/звездочка/tmp - игнорируются все файлы tmp во всех подпапках папки docs
* docs/звездочка звездочка/tmp - если звездочки две - это подразумевает любое количество папок
4. Знак вопроса соответствует любому 1 символу. file?.txt игнорируются файлы с любым 1 (но не меньше или больше) символом после названия.
5. Квадратные скобки также указывают на игнорирование 1 символа, но задают диапазон. Например: 
* [abc] - a,b,c 
* [a-z] - любая буква от a до z
* [1-3] - 1, 2 или 3
6. Косая черта (/)
* /todo.txt - в начале задает игнорирование файлов с таким именем в корневом каталоге
* todo.txt - для сравнения будут игнорироваться все файлы с таким именем во всех папках
* build/ - в конце означает игнорирование папки build
* build.txt/ - такая строчка будет игнорироваться, т.к. это не папка
7. Знак восклицания инвертирует любое правило .gitignore. Напр: 
* звездочка.jpeg - игнорировать все файлы jpeg
* !doge.jpeg - но только не этот

### Клонирование репозитория
* **git clone HTTPadres_from_away_repository** - копирует проект со стороннего на локальный компьютер. Для этого нужно скачать ссылку - например, в GitHub зайти на проект - нажать зеленую кнопку Code и взять оттуда ссылку HTTP/SSH. Эта команда автоматически связвает локальный репозиторий с удаленным.

При клонировании репозитория отслеживается по умолчанию только main/master ветка. Остальные в статусе удаленные и не видны. Чтобы сделать невидимую ветку отслеживаемой нужно: 
* **git checkout --track -b localBranchName origin/remoteBranchName** - этой командой происходит переключение на удаленную ветку и создание локальной ветки из нее. Имена localBranchName и remoteBranchName можно сделать одинаковыми (здесь они разные для понимания смысла строчки)
* **git checkout branchName** - или просто создание локальной ветки (для этого посмотреть название неотслеживаемой ветки в GitHub)

### Fork

Это GitHub операция - создает точную независимую копию GitHub репозитория в ваш аккаунт. Изменения в ней не затронут исходный репозиторий.

Для выполнения этой операции нужно зайти на исходный репозиторий и нажать кнопку Fork справа-вверху - заполнить при необходимости поля в открвшемся окне - нажать Create fork.

### Fork vs Clone
1. Fork используется для клонирования чужого репозитория на ваш. И затем clone, чтобы клонировать его на компьютер.
2. Clone - без fork достаточно, если вы хотите скопировать на компьютер собственный проект или проект вашей компании.

### Ветка

Это изолированный поток разработки проекта / последовательность независимых изменений. В таком потоке можно проверять разные идеи, тестировать новую функциональность, переключаться между несколькими задачами сразу и т.д. При этом репозиторий сохраняется в стабильном состоянии - основная версия проекта хранится в главной ветке (main/master)
* **git branch** - посмотреть ветки проекта (может понадобиться Q, чтобы выйти из просмотра веток). Звездочкой отмечается в какой ветке вы находитесь в текущий момент.

### Создание ветки
* **git branch nameOfBranch** - название ветки может состоять из букв, цифр и любых из 4 символов (. - _ /) - в названии веток символ / не создает иерархии, как при работе с папками. Название не должно содержать пробелов.

Называть ветки нужно осмысленно. Например вначале указать особенность ветки (напр: feature/add-health) 
* feature - проработка новой функциональности
* bugfix - исправление ошибок

### Переключение между ветками
* **git checkout nameOfBranch** - переключение на указанную ветку. Чтобы переключиться на главную ветку нужно указать main/master
* Содержимое одних и тех же файлов в разных ветках будет выглядеть по разному, если в них производились изменения на какой-то из веток.

### Создать ветку и сразу переключиться на нее
* **git checkout -b nameOfNewBranch** - одномоментно делает то же, что и 2 предыдущие команды

### На какой коммит указывает ветка

Ветка - это указатель на коммит. Когда в ветке делается новый коммит, этот указатель продвигается вперед. Если в новой ветке еще нет коммитов - она будет указывать на тот же коммит, что и ветка-родитель.

### Сравнение веток
* **git diff** - без параметров - укажет изменения в "рабочей зоне", т.е. в файлах modified
* **git diff branch1 branch2** - сравнивает ветки по названиям, вместо названия ветки можно указать:
* HEAD - ветка с последним сделанным коммитом
* номер коммита нужной ветки
* использовать символ (волнистая линияN) - число N отсчитывает от заданного комита N коммитов назад во времени (git diff main main~2)

### Объединение веток
* **git merge branchName** - нужно перейти в ветку, куда должны добавиться изменения (обычно это главная ветка). Внутри этой ветки вызвать команду и указать имя присоединяемой ветки.

В информации после слияния будет указано:
* какие именно коммиты объединились
* какой режим слияния
* информация о конкретных изменениях: название файла(-ов), сколько строк добавилось/удалилось

Как результат обе объединенные ветки будут указывать на 1 коммит.

### Удаление ветки после объединения
* **git branch -D branchName** - после слияния ветку-донор можно удалить. Если в момент удаления вы будете находиться в той ветке, которую хотите удалить - программа выдаст ошибку. Нужно быть в любой другой ветке.
* **git branch -d branchName** - более безопасный вариант. Он удалит ветку только если она полностью объединена с другой (т.е. 2 ветки стали или изначально были частью одной истории - в т.ч. если вы нечаянно создали ветку с неправильным названием)

Удаление локальной ветки через Git не удаляет ветку на GitHub!

### Отправить локальную ветку в удаленный репозиторий
* **git remote add origin HTTPadress** - привязка удаленного репозитория к локальному
* **git push -u origin main/master** - свяжет локальную ветку с удаленной. Основная ветка появится в GitHub
* **git checkout -b newBranchName** - создание новой ветки и переход в нее
* внести изменения в файлы в новой ветке
* **git add . && git commit -m "comment to commit"** - закомитить изменения в ветке
* **git push -u origin newBranchName** - запушит новую ветку с локального на удаленный репозиторий. В данном случае не обязательно находиться в новой ветке, достаточно того, что вы просто указываете ее имя в команде. После этого:
* в консоли появится информация со ссылкой, с помощью которой можно быстро создать запрос на изменения
* в GitHub добавится новая ветка и станет возможным перейти в нее

### Pull request
Нельзя просто внести поправки в ветку и сразу залить ее в основную. Сначала нужно убедиться в ее целесообразности. Для этого используется pull request ("запрос на изменения"). Алгоритм следующий:
1. Вы работает над задачей в своей ветке
2. По завершени создаете pull request
3. Коллеги проверяют код на корректность написания и его работы, оставляют комментарий. Этот процесс называется code review ("рассмотрение кода")
4. После согласования эта ветка заливается в основную

Pull request можно создать из любой ветки, отличающейся от main/master. Часто создают 2 ветки main и dev - во второй ведется работа, а в main хранится основная рабочая версия. Dev периодически сливается с main/master.

### Из чего состоит pull request
1. Название - краткое описание предлагаемых изменений
2. Описание - развернутое описание изменений - (желательно, но не обязательно)
3. Исходная ветка - та, в которой велась работа
4. Целевая ветка - основная ветка проекта, в которую вы хотите внести изменения

### Возможные исходы pull request-а
1. *merge* - предлагаемые изменения приняты - код вливается в целевую ветку - пул-реквест закрывается
2. *close* - пул-реквест закрывается без слияния изменений

### 2 способа сделать pull request
1. При создании новой ветки и отправке ее в GitHub в консоли будет сообщение, содержащее ссылку на создание пул-реквеста. 
* ее можно скопировать и вставить в адресную строку/или щелкнуть на нее прямо в консоли с нажатой Ctrl - здесь важный момент - если вы делали форк репозитория - то при нажатии на ссылку может открыться именно он как base repository - нужно щелкнуть на всплывающее окно, где указан base repository:... и выбрать свой case - тогда появится поле, где нужно указать ветки для слияния
* заполнить необходимые поля и нажать Create pull request
**Такая строчка появляется только 1 раз для новых веток, поэтому есть еще 1 способ**
2. В GitHub в репозитории:
* найти вкладку **Pull request** в верхней части экрана - **New Pull request**
* выбрать названия веток: ветка "откуда" и ветка "куда" - стрелка показывает направление изменений (откуда - куда)
* в окне ниже отобразится несколько коммитов и изменения
* нажать **Create pull request**
* в открывшемся окне будут вкладки: Conversation/Commits/Checks/Files changed - здесь можно посмотреть комментарии, обсудить изменения, добавить дополнительные коммиты - они автоматически попадут в открытый пул-реквест после пуша
* нажатие кнопки **Merge pull request - confirm merge** объединит ветку с изменениями и ветку main/master
* можно нажать кнопку Delete branch - это удалит ветку с которой объединилась main

### Забираем изменения из удаленного репозитория
* **git pull** - скачивает изменения из удаленного репозитория
* обычно **git pull** - это первая команда, которую вводит разработчик, как только открывает код проекта, чтобы начать с ним работать
* дополнительно **git pull** и **git merge** выполняют перед тем как создать **Pull request**, т.к. при командной работе основная ветка может измениться пока вы готовите свои изменения. Поэтому рекомендуется: 
1. сначала подтянуть изменения из основной ветки
* **git checkout main** - перешли в main
* **git pull** - подтянуть новые изменения в main
2. объединить их с вашей
* **git checkout myBranch** - вернуться в рабочую ветку
* **git merge main** - влить main в новую ветку, чтобы проверить на наличие конфликтов
3. решить все возможные конфликты
4. и лишь затем сделать push
* **git push -u origin myBranch** - отправить рабочую ветку в удаленный репозиторий (не связанную ветку) и одновременно связать их
* **git push** - отправить изменения в удаленный репозиторий (в связанную ветку)

GitHub вливает ваши изменения в ветку main в origin, а локальная ветка остается как была. После "мержа" PR рекомендуется обновить локальную main: git checkout main && git pull

При клонировании репозитория отслеживается по умолчанию только main/master ветка. Остальные в статусе удаленные и не видны. Чтобы сделать невидимую ветку отслеживаемой нужно: 
* **git checkout --track -b localBranchName origin/remoteBranchName** - этой командой происходит переключение на удаленную ветку и создание локальной ветки из нее. Имена localBranchName и remoteBranchName можно сделать одинаковыми (здесь они разные для понимания смысла строчки)
* **git checkout branchName** - или просто создание локальной ветки (для этого посмотреть название неотслеживаемой ветки в GitHub)

### Fast-forward
Если истории 2 веток не "разошлись" (при слиянии этих 2 веток невозможет конфликт) и их коммиты выстраиваются в одну цепочку, эти ветки можно объединить в режиме fast-forward. Но при этом режиме теряется часть информации и результат выглядит так, как будто в main просто появлялись новые коммиты и не было никаких других веток. Поэтому многие проекты отключают fast-forward слияние. 
* **git merge --no-ff branchName** - отключает режим fast-forward
* **git merge --no-edit --no-ff branchName** - то же, но с отключение ввода сообщения для merge-коммита

### Non-Fast-Forward
Если ветки разошлись и в каждой из них параллельно произошли изменения/коммиты, которые могут вызвать конфликт слияния. 
* **git merge --no-edit branchName** - пытаемся смерджить 2 разошедшиеся ветки. Флаг --no-edit избавляет от необходимости вводить сообщение для merge-коммита
При слиянии Non-Fast-Forward веток Git создает коммит слияния (присваивает ему номер - его можно увидеть с помощью git log). 
* Если конфликтов при слиянии нет - git merge отработает почти автоматически - только предложит вам ввести сообщение для нового коммита слияния - чаще всего сообщения к коммитам на слияние не редактируют и оставляют как предложил Git используя флаг --no-edit
* Если конфликты есть, Git сначала попытается их решить автоматически. Если не получится - предложит разрешить их вручную.

### git push & Fast-Forward

**git push** толкает коммиты из локальной ветки в ее удаленную копию. В результате все новые коммиты из локальной ветки попадут в удаленную. В итоге локальная и удаленная ветки будут содержать одни и те же коммиты.

### git push & Non-Fast-Forward
Если попытаться объединить с помощью **git push** разошедшиеся ветки, появится ошибка (в которой будет **rejected** - запрос отклонен и non-fast-forward)

### Подходы к работе с ветками/модели веток (workflow/flow -"рабочий процесс")
1. **Feature branch workflow** - самый простой и популярный вариант. Для каждого нового изменения создается новая ветка, которая позже вливается в main с помощью git merge
2. **Git flow** - похож на 1, но создается больше веток, а изменения/коммиты делят на разные типы: исправления, новая функциональность и т.д. Разные типы коммитов попадают в разные ветки.
3. **Trunk-based** - популярен в больших компаниях, обеспечивает бОльшую скорость работы в крупных командах. Похож на 1 - главное отличие, что участники проетка вливают (merge) свой код в основную ветку максимально часто. Например, каждый день.

### Feature branch workflow
* cоздается отдельная ветка под конкретную задачу (функциональность/исправление и др.)
* все коммиты, связанные с этой задачей попадают в эту ветку
* когда задача полностью решена - ветка вливается (merge) в ветку main
* разработчики трудятся над новыми задачами независимо друг от друга и не затрагивают основную ветку кода в процессе
* не возникает проблемы расходящейся ветки
* при таком походе все коммиты в ветке main - это коммиты слияния (feature-ветки сливаются в main)

Если аккуратно следовать подходу, то:
* не будет проблемы расхождения веток - все изменения попадают в main через **git merge**, а не через **git push**. Команду **merge** "разошедшиеся" ветки не смущают, ведь для них она и придумана
* в ветке main всегда рабочая версия проекта. Все недоделанные функциональности находятся в feature-ветках, пока не будут готовы попасть в main
* запрос на добавление происходит обычно через pull request - после всех проверок (тесты, review - ревьюер проверяет стиль кода, ошибки, уязвимость, можно ли сделать код лучше - если все ОК, ревьюер нажимает кнопку **Approve** или ставит комментарий **LGTM - Look Good To Me**) ветка присоединяется к основной
* после одобрения пул-реквеста его автор (или другой участник проекта) может нажать кнопку **Merge**. GitHub вольет ветку в main.

### Конфликты слияния
* Если коммиты веток можно выстроить в одну линию - слияние будет проходить без конфликтов
* Если 1 файл был изменен параллельно в разных ветках до их слияния - это приведет к конфликту
* При попытке слияния таких веток программа выдаст: **CONFLICT** - файл в котором есть конфликт
* Если выполнить **git status** после данной ошибки файлы с маркерами конфликтов будут отображаться в категории: **Unmerged paths** (несоединенные пути) с текстом **both modified** (оба изменены)
* в файлы, вызвавшие конфлик будут добавлены специальные маркеры конфликта: 
	*Текст между **<<<<<<<< HEAD** и **=========** указывает на изменения, которые находятся в HEAD. Здесь окажутся только те строки, в которых есть конфликт
	* Текст между **========** и **>>>>>>>> branchName** показывает на изменения, которые находятся в ветке branchName

### Удаление конфликта вручную
 Нужно открыть файл и выбрать, какие изменения оставить, а какие отбросить. Для этого удаляют все маркеры и ненужные изменения. После разрешения конфликта файлы будут отмечены как решенные. Можно продолжить процесс слияния или выполнить коммит изменений.

### Разрешение конфликта через **vimdiff**
 Чтобы вызвать в консоли программу vimdiff нужно выполнить команду git mergetool и после появления сообщения со строкой **Hit return to start merge resolution tool** нажать Enter. Это не самая удобная программа для работы, есть более удобные инструменты.

### Visual Studio Code
Можно открыть папку проекта в Visual Studio Code. Файл в котором будет конфликт при слиянии - отобразит все маркеры изменений:
*Текст между **<<<<<<<< HEAD** и **=========** указывает на изменения, которые находятся в HEAD. Здесь окажутся только те строки, в которых есть конфликт
* Текст между **========** и **>>>>>>>> branchName** показывает на изменения, которые находятся в ветке branchName
* Зеленым цветом будет указана текущая версия, а синим - новые изменения. 
* Можно разрешить конфликт прямо в файле вручную (если изменений немного)
* Можно открыть редактор слияния (если изменений много), нажав на соответствующую синюю кнопку внизу - откроется окно разрешения конфликтов - здесь можно выбрать **Accept incoming (принять входящие)** или **Accept current (принять текущие)** - далее **Complete merge (завершить слияние)** - с левой стороны изменить сообщение коммита (если необходимо) - и нажать **Commit**

### Удаленная основная ветка изменилась пока вы работали локально
Возможно 2 варианта:
1. Ваши изменения и изменения в удаленной ветке не пересекаются - GitHub смержит их автоматически
2. Изменения пересекаются - программа выдаст предупреждение о том, что есть конфликт (перечислит файлы в которых он возник) и нужно его решить прежде чем мержить ветки

GitHub содержит интерфейс для разрешения конфликтов, но обычно это делается локально (например, с помощью Visual Studio Code) - во втором случае последовательность действие будет выглядеть так:
1. Перейти в ветку main
2. Загрузить новые изменения из нее с помощью git pull - в таком случае загрузится и ветка, приведшая к изменениям в основной ветке
3. Снова перейти в свою локальную ветку featureBranch
4. Выполнить git merge main и разрешить конфликт локально. В результате будет создан локальный коммит слияния
5. Отправить новые изменения без конфликтов в удаленный репозиторий командой git push