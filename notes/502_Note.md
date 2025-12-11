# Note

{% hint style='info' %}

#### Info
How to convert this GitBook e-book into PDF, EPUB and/or MOBI file formats?
{% endhint %}

## Windows

### 1. Install the following software:
- [node.js](https://nodejs.org/en/download/)
- [Git](https://git-scm.com/download/win)
- [Calibre](https://calibre-ebook.com/dist/win64)

### 2. Open an elevated command prompt and clone the book repository:
```
git clone https://github.com/dimitarminchev/DCPA.git
```
Result:
```
Cloning into 'DCPA'...
remote: Enumerating objects: 700, done.
remote: Counting objects: 100% (107/107), done.
remote: Compressing objects: 100% (85/85), done.
remote: Total 700 (delta 70), reused 36 (delta 22), pack-reused 593 eceiving objects:  93% (651/700), 202.79 MiB | 9.45 MiB/s
Receiving objects: 100% (700/700), 204.77 MiB | 9.35 MiB/s, done.
Resolving deltas: 100% (410/410), done.
```

### 3. Enter the newly cloned repository:
```
cd DCPA
```

### 4. Install the required modules by running the following commands:
```
$env:Path += ';C:\Program Files\Calibre2\'
npm install -g ebook-convert 
npm install -g gitbook-cli
gitbook install
```

### 5. You may encounter an error like this:
```
C:\Users\mitko\AppData\Roaming\npm\node_modules\gitbook-cli\node_modules\npm\node_modules\graceful-fs\polyfills.js:287
      if (cb) cb.apply(this, arguments)
                 ^
TypeError: cb.apply is not a function
    at C:\Users\mitko\AppData\Roaming\npm\node_modules\gitbook-cli\node_modules\npm\node_modules\graceful-fs\polyfills.js:287:18
    at FSReqCallback.oncomplete (node:fs:211:5)
```
To fix this error:
```
cd C:\Users\mitko\AppData\Roaming\npm\node_modules\gitbook-cli\node_modules\npm\
npm i graceful-fs@4.1.4 --save
```

### 6. Return to the command prompt and finish the installation:
```
gitbook install
```

### 7. Check the GitBook version with:
```
gitbook --version
```
The result may look like:
```
CLI version: 2.3.2
GitBook version: 3.2.3
```

### 8. Run the procedure to generate the e-book in your chosen format:
- **HTML**
```
gitbook build
```
A successful run will show output similar to:
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
A successful run will show output similar to:
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
A successful run will show output similar to:
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
A successful run will show output similar to:
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

### 1. Update your distribution:
```
sudo apt update -y && sudo apt upgrade
```

### 2. Install the required packages:
```
sudo apt install -y calibre
sudo apt install -y nodejs
sudo apt install -y npm
sudo npm install -g ebook-convert 
sudo npm install -g graceful-fs@4.2.0
sudo npm install -g gitbook-cli@2.1.2 
gitbook install
```

### 3. Clone the book repository:
```
git clone https://github.com/dimitarminchev/DCPA.git
cd DCPA
```

### 4. Generate the e-books:
```
gitbook pdf
gitbook mobi
gitbook epub
```

A successful run will show output similar to:
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
