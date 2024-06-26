# Бележка

{% hint style='info' %}

#### Информация
Как да конвертирате настоящата GitBook електронна книга в PDF, EPUB и/или MOBI файлов формат?
{% endhint %}

## Windows

### 1. Инсталирайте следните програмни продукти:
- [node.js](https://nodejs.org/en/download/)
- [Git](https://git-scm.com/download/win)
- [Calibre](https://calibre-ebook.com/dist/win64)

### 2. Стартирайте командния промпт като администратор и клонирайте електронното хранилище на книгата:
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
npm install -g ebook-convert 
npm install -g gitbook-cli
gitbook install
```

### 5. Възможно е да получите подобна грешка:
```
C:\Users\mitko\AppData\Roaming\npm\node_modules\gitbook-cli\node_modules\npm\node_modules\graceful-fs\polyfills.js:287
      if (cb) cb.apply(this, arguments)
                 ^
TypeError: cb.apply is not a function
    at C:\Users\mitko\AppData\Roaming\npm\node_modules\gitbook-cli\node_modules\npm\node_modules\graceful-fs\polyfills.js:287:18
    at FSReqCallback.oncomplete (node:fs:211:5)
```
За да поправите тази грешка:
```
cd C:\Users\mitko\AppData\Roaming\npm\node_modules\gitbook-cli\node_modules\npm\
npm i graceful-fs@4.1.4 --save
```

### 6. Върнете се в командният промпт и довършете инсталацията:
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
- **HTML**
```
gitbook build
```
Резултат от успешно изпълнение ще изглежда така:
```
info: 8 plugins are installed
info: 7 explicitly listed
info: loading plugin "hints"... OK
info: loading plugin "highlight"... OK
info: loading plugin "search"... OK
info: loading plugin "lunr"... OK
info: loading plugin "sharing"... OK
info: loading plugin "fontsettings"... OK
info: loading plugin "theme-default"... OK
info: found 35 pages
info: found 109 asset files
warn: "this.generator" property is deprecated, use "this.output.name" instead
warn: "navigation" property is deprecated
warn: "book" property is deprecated, use "this" directly instead
warn: "options" property is deprecated, use config.get(key) instead
info: >> generation finished with success in 2.2s !
```
- **PDF**
```
gitbook pdf
```
Резултат от успешно изпълнение ще изглежда така:
```
info: 8 plugins are installed
info: 7 explicitly listed
info: loading plugin "hints"... OK
info: loading plugin "highlight"... OK
info: loading plugin "search"... OK
info: loading plugin "lunr"... OK
info: loading plugin "sharing"... OK
info: loading plugin "fontsettings"... OK
info: loading plugin "theme-default"... OK
info: found 35 pages
info: found 109 asset files
warn: "this.generator" property is deprecated, use "this.output.name" instead
warn: "navigation" property is deprecated
warn: "book" property is deprecated, use "this" directly instead
warn: "options" property is deprecated, use config.get(key) instead
info: >> generation finished with success in 18.1s !
info: >> 1 file(s) generated
```
- **EPUB**
```
gitbook epub
```
Резултат от успешно изпълнение ще изглежда така:
```
info: 8 plugins are installed
info: 7 explicitly listed
info: loading plugin "hints"... OK
info: loading plugin "highlight"... OK
info: loading plugin "search"... OK
info: loading plugin "lunr"... OK
info: loading plugin "sharing"... OK
info: loading plugin "fontsettings"... OK
info: loading plugin "theme-default"... OK
info: found 35 pages
info: found 110 asset files
warn: "this.generator" property is deprecated, use "this.output.name" instead
warn: "navigation" property is deprecated
warn: "book" property is deprecated, use "this" directly instead
warn: "options" property is deprecated, use config.get(key) instead
info: >> generation finished with success in 9.6s !
info: >> 1 file(s) generated
```
- **MOBI**
```
gitbook mobi
```
Резултат от успешно изпълнение ще изглежда така:
```
info: 8 plugins are installed
info: 7 explicitly listed
info: loading plugin "hints"... OK
info: loading plugin "highlight"... OK
info: loading plugin "search"... OK
info: loading plugin "lunr"... OK
info: loading plugin "sharing"... OK
info: loading plugin "fontsettings"... OK
info: loading plugin "theme-default"... OK
info: found 35 pages
info: found 111 asset files
warn: "this.generator" property is deprecated, use "this.output.name" instead
warn: "navigation" property is deprecated
warn: "book" property is deprecated, use "this" directly instead
warn: "options" property is deprecated, use config.get(key) instead
info: >> generation finished with success in 8.5s !
info: >> 1 file(s) generated
```

## Linux

### 1. Актуализиарайте вашата дистрибуция:
```
sudo apt update -y && sudo apt upgrade
```

### 2. Инсталирайте необходимите модули:
```
sudo apt install -y calibre
sudo apt install -y nodejs
sudo apt install -y npm
sudo npm install -g ebook-convert 
sudo npm install -g graceful-fs@4.2.0
sudo npm install -g gitbook-cli@2.1.2 
gitbook install
```

### 3. Клонирайте електронното хранилище на книгата:
```
git clone https://github.com/dimitarminchev/DCPA.git
cd DCPA
```

### 4. Генерирайте електронните книги:
```
gitbook pdf
gitbook mobi
gitbook epub
```

Резултат от успешно изпълнение ще изглежда така:
```
info: 8 plugins are installed 
info: 7 explicitly listed 
info: loading plugin "hints"... OK 
info: loading plugin "highlight"... OK 
info: loading plugin "search"... OK 
info: loading plugin "lunr"... OK 
info: loading plugin "sharing"... OK 
info: loading plugin "fontsettings"... OK 
info: loading plugin "theme-default"... OK 
info: found 36 pages 
info: found 80 asset files 
warn: "this.generator" property is deprecated, use "this.output.name" instead 
warn: "navigation" property is deprecated 
warn: "book" property is deprecated, use "this" directly instead 
warn: "options" property is deprecated, use config.get(key) instead 
info: >> generation finished with success in 34.8s ! 
info: >> 1 file(s) generated 
```
