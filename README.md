## [0. Основы markdow на GitHub](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
## 1 Работа с локальным репозиторием
### 1.1 Инициализация  
- Инициализировать репозиторий можно с помощью команды ```git init```.  
- Проверить статус или состояние репозитория поможет команда ```git status```.  
- Если вы ошиблись и случайно инициализировали не ту папку, можно «разгитить» её — удалить скрытую подпапку *.git*.  

### 1.2  Подготовка коммита (кеширование/индексация)
- Команда ```git add``` позволяет подготовить файл к сохранению.  
- Команда ```git add --all``` подготовит к сохранению сразу все файлы.  
- С помощью ```git add .``` можно добавить в репозиторий текущую папку со всеми файлами.  

### 1.3 Сохранение изменений в локальный репозиторий (коммит)  
```git commit -m "Комментарий к коммиту"``` - закоммитить изменения в локальный репозиторий, ключ ```-m``` позволяет присвоить коммиту сообщение.  

### 1.4 Просмотр истории  
```git log``` выводит список коммитов;  
```git log --oneline``` выведет ту же информацию, но каждый коммит будет на отдельной строке.  


## 2 Работа с удаленным репозиторием  
### 2.1 Создание SSH-ключа  
- Пример 1 (шифрование ed25519):  
```ssh-keygen -t ed25519 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"```  
- Пример 2 (шифрование rsa):  
```ssh-keygen -t rsa -b 4096 -C "электронная почта, к которой привязан ваш аккаунт на GitHub" ```  
   * Программа попросит указать место хранения ключей. Простой вариант — сделать домашний каталог пользователя путём по умолчанию. Для этого нажмите ```Enter```.  
   * Программа запросит кодовую фразу (англ. passphrase) для доступа к SSH-ключу. Вы можете оставить поле пустым. Для этого нажмите ```Enter```, а затем ещё раз ```Enter``` для подтверждения.  
   * На экране должны появиться два файла — один с расширением ```.pub```, другой — без расширения.  
> [!CAUTION]  
> Файл с расширением '''.pub''' — публичный, им можно делиться с веб-сайтами или коллегами.  
> Файл без расширения — приватный. Ни в коем случае не передавайте его никому!  

### 2.2 Привязываем SSH-ключ к GitHub  
  1. Скопируйте содержимое *.pub* файла  
  2. Перейдите на [GitHub](https://github.com/) и выберите **Settings** в меню аккаунта  
  3. Нажмите **SSH and GPG keys** в меню слева  
  4. Выберите **New SSH key** в открывшейся вкладке  
  5. В поле **Key type** должно быть **Authentication Key**  
  6. Вставьте содержимое файла *.pub* в поле **Key** и нажмите **Add SSH key**  
  7. Проверьте правильность ключа с помощью команды ```ssh -T git@github.com```  

### 2.3 Связывание с удалённым репозиторием  
```git remote add origin <ссылка_на_удаленный_репозиторий>``` - эта команда свяжет текущий локальный репозиторий с удаленным репозиторием, доступным по ссылке. Файлы между репозиториями нужно будет синхронизировать отдельной командой. *origin* - это псевдоним текущего локального репозитория, вместо него можно указывать полное имя репозитория.  
```git remote -v``` - команда, чтобы убедиться, что репозитории связаны  

### 2.4 Копирование удаленного репозитория  
```git clone <url репозитория>``` автоматически связывает текущий локальный и указанный удалённый репозиторий. Так же будут сразу сказаны файлы из удаленного репозитория.  
```git remote -v``` - команда, чтобы убедиться, что репозитории связаны  


## 3 Работа с ошибками в коммитах  
### 3.1 Исправление коммита   
```git commit --amend -m "Обновлённое сообщение коммита"``` - команда для добавления изменений в последний коммит (HEAD); так же будет обновлен комментарий к коммиту.  
Флаг ```--no-edit``` оставит комментарий без изменений;   
> [!TIP]  
> Если забыть указать у команды ```git commit --amend``` один из флагов (```--no-edit``` или ```-m```), Git предложит отредактировать сообщение коммита вручную. Для этого он откроет текстовый редактор, который установлен в системе по умолчанию. Чаще всего это либо **GNU nano**, либо **Vim**.  
> * Чтобы выйти из **nano** используйте ```Ctrl+X```, чтобы выйти без сохранения, или ```Ctrl+O```, чтобы сохранить результаты  
> * Чтобы выйти из **vim** нажмите ```Esc```, затем введите ```:qa!``` и нажмите ```Enter```  

### 3.2 Отмена изменений  
```git restore <file>``` - Удаление изменений в файле: команда «откатит» изменения в файле до последней сохранённой (в коммите или в *staging*) версии.  
```git restore --staged <file>``` - Удаление файлов из stage/cache/index: команда переведёт файл из *staged* обратно в *modified* или *untracked*.  
```git reset --hard <commit hash>``` -Удаление коммитов: команда «откатит» все изменения, сделанные после коммита с хешем *<hash>*. Более поздние коммиты будут удалены!  


## 4 Работа с ветками  
### 4.1 Создание веток
```git branch feature/the-finest-branch``` — создай ветку от текущей с названием *feature/the-finest-branch*;  
```git checkout -b feature/the-finest-branch``` — создай ветку *feature/the-finest-branch* и сразу переключись на неё.  
### 4.2 Навигация по веткам
```git branch``` — покажи, какие есть ветки в репозитории и в какой из них я нахожусь (текущая ветка будет отмечена символом *);  
```git branch -a``` — покажи все известные ветки, как локальные (в локальном репозитории), так и удалённые (в *origin*, или на GitHub);
```git checkout feature/br``` — переключись на ветку *feature/br*  
### 4.3 Сравнение веток
```git diff main HEAD``` — покажи разницу между веткой *main* и указателем на *HEAD*;  
```git diff HEAD~2 HEAD``` — покажи разницу между тем коммитом, который был два коммита назад, и текущим;  
### 4.4 Удаление веток
```git branch -d br-name``` — удали ветку *br-name*, но только если она является частью *main*;  
```git branch -D br-name``` — удали ветку *br-name*, даже если она не объединена с *main*  
### 4.5 Слияние веток
```git merge main``` — объедини ветку *main* с текущей активной веткой.  
### 4.6 Работа с удалённым репозиторием
```git push -u origin my-branch``` — отправь новую ветку *my-branch* в удалённый репозиторий и свяжи локальную ветку с удалённой, чтобы при дополнительных коммитах можно было писать просто ```git push``` без ```-u```;  
```git push my-branch``` — отправь дополнительные изменения в ```ветку my-branch```, которая уже существует в удалённом репозитории;  
```git pull``` — подтяни изменения текущей ветки из удалённого репозитория.  
