# Заключение

Настоящата електронна книга "**Developing Cross-Platform Apps**" е структурирана в две глави. Глава 1 е озаглавена "Универсални Windows приложения" и въвежда читателя във вълнуващия свят на Microsoft технологиите за разработка на универсални приложения за платформа Windows. Глава 2 е озаглавена "Mултиплатформени мобилни приложения" и въвежда читателя във вълнуващия свят на Microsoft технологиите за разработка на мултиплатформени мобилни приложения.

## Формат и лиценз

Учебното пособие е налично за свободно четене под формата на GitBook базиран [електронен формат](https://dimitar-minchev.gitbook.io/developing-cross-platform-apps/). Учебните ресурси са налични за свободно изтегляне от GitHub базирано [електронно хранилище](https://github.com/dimitarminchev/DCPA/). Всични учебни материали се разпространяват под безплатен лиценз [CC-BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/).

| Формат | ISBN |
| :--- | :--- |
| PDF | 978-619-7126-66-2 |
| MOBI | 978-619-7126-67-9 |
| EPUB | 978-619-7126-68-6 |

## Автор

**Димитър Минчев** е университетски преподавател към Център по информатика и технически науки при Бургаски свободен университет. Създава уникалните [Академията за таланти по програмиране](http://atp.bfu.bg/) и [Школа по роботика](http://robots.bfu.bg/) за ученици от Бургас. Подготвя студенти за [Републиканската студентска олимпиада по програмиране](http://www.bcpc.eu/) в [Клуб по състезателно програмиране](https://dev.bfu.bg/). Организира съревнование за разработка на настолни и мобилни приложения на морето [ХАКАТОН @ БСУ](https://dev.bfu.bg/hackathon/). Инициира ученическото състезание по програмиране [CODE@BURGAS](https://spoj.bfu.bg/). Преподавател от националната програма [Обучение за ИТ кариера](https://github.com/dimitarminchev/ITCareer) на Министерството на образованието и науката. 

|| Контакт |
| :--- | :--- |
| Служебен | +359 56 900 477 и [mitko@bfu.bg](http://www.minchev.eu/about/mitko@bfu.bg) |
| Личен | +359 899 148 872 и [dimitar.minchev@gmail.com](mailto:dimitar.minchev@gmail.com) |
| Блог | [http://www.minchev.eu](http://www.minchev.eu "Димитър Минчев") |

Пожелавам Ви приятно четене :)

# Как да конвертирате настоящата GitBook електронна книга в PDF, EPUB и/или MOBI файлов формат?

### 1. Инсталирайте следните програмни продукти:

- [node.js](https://nodejs.org/en/download/)
- [Git](https://git-scm.com/download/win)
- [Calibre](https://calibre-ebook.com/dist/win64)

### 2. Стартирайте PowerShell като администратор и клонирайте електронното хранилище на книгата:

```
git clone https://github.com/dimitarminchev/DCPA.git
```

Резултат:

```
Cloning into 'DCPA'...
remote: Enumerating objects: 700, done.
remote: Counting objects: 100% (107/107), done.
remote: Compressing objects: 100% (85/85), done.
remote: Total 700 (delta 70), reused 36 (delta 22), pack-reused 593 eceiving objects:  93% (651/700), 202.79 MiB | 9.45 MiB/s
Receiving objects: 100% (700/700), 204.77 MiB | 9.35 MiB/s, done.
Resolving deltas: 100% (410/410), done.
```

### 3. Влезте в току що клонираното електронно хранилище на книгата: 

```
cd DCPA
```

### 4. Инсталирайте необходимите модули, като изпълнете следните команди:

```
$env:Path += ';C:\Program Files\Calibre2\'
npm install -g gitbook-cli
npm install -g ebook-convert 
gitbook install
```

### 5. Възможно е да получите подобна грешка:

```
Installing GitBook 3.2.3
C:\Users\mitko\AppData\Roaming\npm\node_modules\gitbook-cli\node_modules\npm\node_modules\graceful-fs\polyfills.js:287
      if (cb) cb.apply(this, arguments)

TypeError: cb.apply is not a function
    at C:\Users\mitko\AppData\Roaming\npm\node_modules\gitbook-cli\node_modules\npm\node_modules\graceful-fs\polyfills.js:287:18
    at FSReqCallback.oncomplete (fs.js:193:5)
```

За да поправите тази грешка, отворете и редактирайте следния файл:

```
C:\Users\mitko\AppData\Roaming\npm\node_modules\gitbook-cli\node_modules\npm\node_modules\graceful-fs\
```

Коментирайте редовете от 62 до 64, както е показано по-долу:

```
// fs.stat = statFix(fs.stat)
// fs.fstat = statFix(fs.fstat)
// fs.lstat = statFix(fs.lstat)
```
 
### 6. Върнете се в PowerShell командният промпт и довършете инсталацията:

```
gitbook install
```

### 7. Проверете версията на GitBook с командата:

```
gitbook --version
```

Резултата може да изглежда по този начин:

```
CLI version: 2.3.2
GitBook version: 3.2.3
```

### 8. Стартирайте процедурата за генериране на електронната книга в избран от Вас формат:

```
gitbook pdf
gitbook epub
gitbook mobi
```

Резултат от примерно успешно изпълнение ще изглежда така:
```
info: 7 plugins are installed
info: 6 explicitly listed
info: loading plugin "highlight"... OK
info: loading plugin "search"... OK
info: loading plugin "lunr"... OK
info: loading plugin "sharing"... OK
info: loading plugin "fontsettings"... OK
info: loading plugin "theme-default"... OK
info: found 30 pages
info: found 101 asset files
info: >> generation finished with success in 25.2s !
info: >> 1 file(s) generated
```

## Последни думи

Пожелавам Ви много забавление, провали и успехи използваки Microsoft технологиите за разработка на универсални Windows приложения и мултиплатформени мобилни приложения.