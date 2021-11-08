# Бележка

{% hint style='info' %}
#### Информация
Как да конвертирате настоящата GitBook електронна книга в PDF, EPUB и/или MOBI файлов формат?
{% endhint %}

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