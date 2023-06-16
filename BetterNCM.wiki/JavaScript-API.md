# 其他工具

## dom
# 其他工具

## dom

简易的创建一个元素的函数。

参数：

- tag: 元素类型。
- settings: 元素的属性键值对。
- children: 元素的子元素，按顺序添加。

返回值：

- 返回创建的元素对象。

使用方法：

```javascript
let myDiv = dom('div', {class: ['my-div']}, 
    dom('p', {innerText:'Hello!'}),
    dom('p', {innerText:'World!'})
);
```


# HTTP API (C)
传统的通过 HTTP 调用的异步 API

## app 模块

### app.exec

执行指定的程序。

参数：

- cmd: 需要执行的指令。
- elevate: 是否使用管理员权限运行。
- showWindow: 是否显示控制台窗口。

返回值：

- 返回布尔值表示是否执行成功。

使用方法：

```javascript
let result = await betterncm.app.exec('taskkill /IM ncm.exe');
console.log(result);
```

### app.getBetterNCMVersion

获取当前 BetterNCM 的版本号。

参数：

- 无。

返回值：

- 返回字符串表示当前 BetterNCM 的版本号。

使用方法：

```javascript
let version = await betterncm.app.getBetterNCMVersion();
console.log(version);
```

### app.takeBackgroundScreenshot

全屏截图。

参数：

- 无。

返回值：

- 返回截图的 Blob 数据。

使用方法：

```javascript
let blobData = await betterncm.app.takeBackgroundScreenshot();
```

### app.getNCMWinPos

获取网易云窗口位置。

参数：

- 无。

返回值：

- 网易云音乐窗口位置
```javascript
{ x: number; y: number }
```

使用方法：

```javascript
let winPos = await betterncm.app.getNCMWinPos();
console.log(winPos);
```

### app.reloadPlugins

重新解压所有插件。

参数：

- 无。

返回值：

- 返回布尔值表示是否执行成功。

使用方法：

```javascript
let result = await betterncm.app.reloadPlugins();
console.log(result);
```

### app.getDataPath

获取目前 BetterNCM 数据目录。

参数：

- 无。

返回值：

- 返回字符串表示数据目录路径。

使用方法：

```javascript
let dataPath = await betterncm.app.getDataPath();
console.log(dataPath);
```

### app.readConfig

读取 BetterNCM 设置。

参数：

- key: 键。
- defaultValue: 默认值。

返回值：

- 返回字符串表示读取到的值。

使用方法：

```javascript
let configValue = await betterncm.app.readConfig('theme', 'dark');
console.log(configValue);
```

### app.writeConfig

设置 BetterNCM 设置。

参数：

- key: 键。
- value: 值。

返回值：

- 返回布尔值表示是否执行成功。

使用方法：

```javascript
let result = await betterncm.app.writeConfig('theme', 'light');
console.log(result);
```

### app.getNCMPath

获取网易云安装目录。

参数：

- 无。

返回值：

- 返回字符串表示安装目录。

使用方法：

```javascript
let ncmPath = await betterncm.app.getNCMPath();
console.log(ncmPath);
```

### app.showConsole

打开网易云主进程的Console。

参数：

- show: 是否显示Console窗口，默认为true。

返回值：

- 返回布尔值表示是否执行成功。

使用方法：

```javascript
let result = await betterncm.app.showConsole(false);
console.log(result);
```

### app.setRoundedCorner

设置Win11 DWM圆角开启状态。

参数：
 - enable: 是否开启圆角，默认为true。

返回值：

- 返回布尔值表示是否执行成功。

使用方法：

```javascript
let result = await betterncm.app.setRoundedCorner(false);
console.log(result);
```

### app.openFileDialog

打开一个选择文件对话框。

参数：

- filter: 要筛选的文件类型。
- initialDir: 对话框初始地址。

返回值：

- 返回字符串表示选择的文件地址，若未选择则为空字符串。

使用方法：

```javascript
let filePath = await betterncm.app.openFileDialog('.mp3', 'C:\\Users\\username\\Music');
console.log(filePath);
```

### app.isLightTheme

获取当前主题是否为亮色主题。

参数：

- 无。

返回值：

- 返回布尔值表示当前主题是否为亮色主题。

使用方法：

```javascript
let isLight = await betterncm.app.isLightTheme();
console.log(isLight);
```

### app.getSucceededHijacks

获取执行成功的 Hijack 日志。

参数：

- 无。

返回值：

- 返回字符串数组表示 Hijack 日志。

使用方法：

```javascript
let hijackLogs = await betterncm.app.getSucceededHijacks();
console.log(hijackLogs);
```

## utils 模块

### utils.waitForElement

等待指定的元素加载完成。

参数：

- selector: 元素选择器。
- interval: 检测间隔时间，默认为100毫秒。

返回值：

- 返回一个 Promise 对象，异步返回元素对象或者 null。

使用方法：

```javascript
let element = await betterncm.utils.waitForElement('#element_id');
console.log(element);
```

### utils.debounce

将指定的函数做防抖处理。

参数：

- callback: 需要被调用的回调函数。
- waitTime: 需要等待多长时间，单位毫秒。

返回值：

- 返回被包装后的防抖函数。

使用方法：

```javascript
function handleResize() {
	// do something
}
let debouncedResize = betterncm.utils.debounce(handleResize, 500);
window.addEventListener('resize', debouncedResize);
```

### utils.waitForFunction

重复调用某函数，直到其返回任意真值，并返回该真值。

参数：

- func: 函数
- interval: 重复调用时间间隔，默认为100毫秒。

返回值：

- 返回 Promise 对象，异步返回 `func` 函数的返回值。

使用方法：

```javascript
let result = await betterncm.utils.waitForFunction(() => {
    let element = document.querySelector('#element_id');
    if (element && element.textContent == 'Ready') {
        return true;
    }
});
console.log(result);
```

### utils.delay

创建一个将在一定时间后 resolve 的 Promise。

参数：

- ms: 延迟时间，以毫秒为单位。

返回值：

- 返回 Promise 对象，将在 `ms` 毫秒后 resolve。

使用方法：

```javascript
await betterncm.utils.delay(1000);
console.log('1 second passed');
```



## ncm 模块

#### findNativeFunction(obj: Object, identifiers: string)

在一个对象中查找包含给定标识符的函数，并返回函数名。

- `obj`: 要查找的对象。
- `identifiers`: 标识符数组。
- `returns`: 函数名。

#### openUrl(url: string)

在默认浏览器中打开 URL。

- `url`: 要打开的 URL。

#### getNCMPackageVersion()

获取 NCM 的包版本号。

- `returns`: NCM 的包版本号。

#### getNCMFullVersion()

获取 NCM 的完整版本号。

- `returns`: NCM 的完整版本号。

#### getNCMVersion()

获取 NCM 的版本号。

- `returns`: NCM 的版本号。

#### getNCMBuild()

获取 NCM 的 build 号。

- `returns`: NCM 的 build 号。

## fs 模块

#### readDir(folderPath: string)

异步读取指定文件夹路径下的所有文件和文件夹。

- `folderPath`:需要读取的文件夹路径。
- `returns`: 所有文件和文件夹的相对路径或绝对路径。

#### readFileText(filePath: string)

读取文本文件，务必保证文件编码是 UTF-8。

- `filePath`: 需要读取的文件路径。
- `returns`: 对应文件的文本形式。

#### readFile(filePath: string)

读取文件。

- `filePath`: 需要读取的文件路径。
- `returns`: 对应文件的 blob。

#### mountDir(filePath: string)

挂载路径。

- `filePath`: 需要挂载的文件夹路径。
- `returns`: 挂载到的 http 地址。

#### mountFile(filePath: string)

挂载路径。

- `filePath`: 需要挂载的文件路径。
- `returns`: 挂载到的 http 地址。

#### unzip(zipPath: string, unzipDest: string = `${zipPath}_extracted/`)

解压指定的 ZIP 压缩文件到一个指定的文件夹中。

- `zipPath`: 需要解压的 ZIP 压缩文件路径。
- `unzipDest`: 需要解压到的文件夹路径，如果不存在则会创建，如果解压时有文件存在则会被覆盖。
- `returns`: 返回值，是否成功。

#### writeFileText(filePath: string, content: string)

将文本写入到指定文件内。

- `filePath`: 需要写入的文件路径。
- `content`: 需要写入的文件内容。
- `returns`: 是否成功。

#### writeFile(filePath: string, content: string | Blob)

将文本或二进制数据写入到指定文件内。

- `filePath`: 需要写入的文件路径。
- `content`: 需要写入的文件内容。
- `returns`: 是否成功。

#### mkdir(dirPath: string)

在指定路径新建文件夹。

- `dirPath`: 文件夹的路径。
- `returns`: 是否成功。

#### exists(path: string)

检查指定路径下是否存在文件或文件夹。

- `path`: 文件或文件夹的路径。
-`returns`: 是否存在。

#### remove(path: string)

删除指定路径下的文件或文件夹。

- `path`: 指定的文件或文件夹路径。
- `returns`: 是否成功。


# BetterNCM Native API (C)

BetterNCM Native API 是 BetterNCM 插件开发的一部分，提供了一系列与系统交互的功能。这些功能包括文件读取、写入、重命名等等。以下是可用的 API 列表。

## fs.readDir

读取目录下的文件列表。

参数：

- path: 目录路径。

返回值：

- 返回一个数组，包含目录下所有文件和文件夹的名称。

使用方法：

```javascript
let files = betterncm_native.fs.readDir('/path/to/dir');
console.log(files);
```

## fs.readFileText

读取文件的文本内容。

参数：

- path: 文件路径。

返回值：

- 返回文件的文本内容。

使用方法：

```javascript
let content = betterncm_native.fs.readFileText('/path/to/file');
console.log(content);
```

## fs.readFileTextAsync

异步读取文件的文本内容。

参数：

- path: 文件路径。
- callback: 回调函数，它的参数为文件的文本内容。

返回值：

- 返回一个空值。

使用方法：

```javascript
betterncm_native.fs.readFileTextAsync('/path/to/file', function(content) {
    console.log(content);
});
```

## fs.watchDirectory

监视目录下的文件变化。

参数：

- path: 目录路径。
- callback: 回调函数，它的参数为变化的文件所在的目录和文件名。

返回值：

- 返回一个空值。

使用方法：

```javascript
betterncm_native.fs.watchDirectory('/path/to/dir', function(dir, file) {
    console.log('File ' + file + ' in directory ' + dir + ' changed.');
});
```

## fs.unzip

解压缩文件到指定目录。

参数：

- path: 压缩文件路径。
- dest: 目标目录路径。

返回值：

- 返回一个整数，表示操作是否成功。

使用方法：

```javascript
let result = betterncm_native.fs.unzip('/path/to/zip', '/path/to/dest');
console.log(result);
```

## fs.rename

重命名文件或目录，或创建新目录。

参数：

- path: 文件或目录路径。
- dest: 新的文件或目录路径。

返回值：

- 返回一个布尔值，表示操作是否成功。

使用方法：

```javascript
// 重命名文件
let result = betterncm_native.fs.rename('/path/to/oldfile', '/path/to/newfile');
console.log(result);

// 重命名目录
let result2 = betterncm_native.fs.rename('/path/to/olddir', '/path/to/newdir');
console.log(result2);

// 创建新目录
let result3 = betterncm_native.fs.rename('/path/to/newdir');
console.log(result3);
```

## fs.exists

检查文件或目录是否存在。

参数：

- path: 文件或目录路径。

返回值：

- 返回一个布尔值，表示文件或目录是否存在。

使用方法：

```javascript
let result = betterncm_native.fs.exists('/path/to/file');
console.log(result);
```

## fs.writeFileText

写入文本内容到文件。

参数：

- path: 文件路径。
- body: 文本内容。

返回值：

- 返回一个布尔值，表示操作是否成功。

使用方法：

```javascript
let result = betterncm_native.fs.writeFileText('/path/to/file', 'Hello, world!');
console.log(result);
```

## fs.remove

删除文件或目录。

参数：

- path: 文件或目录路径。

返回值：

- 返回一个布尔值，表示操作是否成功。

使用方法：

```javascript
let result = betterncm_native.fs.remove('/path/to/file');
console.log(result);
```

## app.reloadIgnoreCache

重新加载当前页面，忽略缓存。

参数：无。

返回值：

- 返回一个布尔值，表示操作是否成功。

使用方法：

```javascript
let result = betterncm_native.app.reloadIgnoreCache();
console.log(result);
```

## app.datapath

获取 BetterNCM 数据目录的路径。

参数：无。

返回值：

- 返回一个字符串，表示 BetterNCM 数据目录的路径。

使用方法：

```javascript
let path = betterncm_native.app.datapath();
console.log(path);
```

## app.ncmpath

获取 NCM 文件的路径。

参数：无。

返回值：

- 返回一个字符串，表示 NCM 文件的路径。

使用方法：

```javascript
let path = betterncm_native.app.ncmpath();
console.log(path);
```

## app.version

获取 BetterNCM 的版本号。

参数：无。

返回值：

- 返回一个字符串，表示 BetterNCM 的版本号。

使用方法：

```javascript
let version = betterncm_native.app.version();
console.log(version);
```

## app.restart

重启 BetterNCM。

参数：无。

返回值：

- 返回一个布尔值，表示操作是否成功。

使用方法：

```javascript
let result = betterncm_native.app.restart();
console.log(result);
```

## app.crash

导致 BetterNCM 崩溃，用于测试目的。

参数：无。

返回值：

- 无返回值。

使用方法：

```javascript
betterncm_native.app.crash();
```

## native_plugin.getRegisteredAPIs

获取已经注册的 Native Plugin 的 API 名称列表。

参数：无。

返回值：

- 返回一个数组，包含已经注册的 Native Plugin 的 API 名称。

使用方法：

```javascript
let apis = betterncm_native.native_plugin.getRegisteredAPIs();
console.log(apis);
```

## native_plugin.call

调用 Native Plugin 定义的 Native API。

参数：

- identifier: API 的标识符。
- args: 一个数组，包含调用 API 时传递的参数。

返回值：

- 返回 API 执行的结果。

使用方法：

```javascript
let result = betterncm_native.native_plugin.call('my_plugin.my_api', ['arg1', 2, true]);
console.log(result);
```
简易的创建一个元素的函数。

参数：

- tag: 元素类型。
- settings: 元素的属性键值对。
- children: 元素的子元素，按顺序添加。

返回值：

- 返回创建的元素对象。

使用方法：

```javascript
let myDiv = dom('div', {class: ['my-div']}, 
    dom('p', {innerText:'Hello!'}),
    dom('p', {innerText:'World!'})
);
```


# HTTP API (C)
传统的通过 HTTP 调用的异步 API

## app 模块

### app.exec

执行指定的程序。

参数：

- cmd: 需要执行的指令。
- elevate: 是否使用管理员权限运行。
- showWindow: 是否显示控制台窗口。

返回值：

- 返回布尔值表示是否执行成功。

使用方法：

```javascript
let result = await window.betterncm_native.app.exec('taskkill /IM ncm.exe');
console.log(result);
```

### app.getBetterNCMVersion

获取当前 BetterNCM 的版本号。

参数：

- 无。

返回值：

- 返回字符串表示当前 BetterNCM 的版本号。

使用方法：

```javascript
let version = await window.betterncm_native.app.getBetterNCMVersion();
console.log(version);
```

### app.takeBackgroundScreenshot

全屏截图。

参数：

- 无。

返回值：

- 返回截图的 Blob 数据。

使用方法：

```javascript
let blobData = await window.betterncm_native.app.takeBackgroundScreenshot();
```

### app.getNCMWinPos

获取网易云窗口位置。

参数：

- 无。

返回值：

- 网易云音乐窗口位置
```javascript
{ x: number; y: number }
```

使用方法：

```javascript
let winPos = await window.betterncm_native.app.getNCMWinPos();
console.log(winPos);
```

### app.reloadPlugins

重新解压所有插件。

参数：

- 无。

返回值：

- 返回布尔值表示是否执行成功。

使用方法：

```javascript
let result = await window.betterncm_native.app.reloadPlugins();
console.log(result);
```

### app.getDataPath

获取目前 BetterNCM 数据目录。

参数：

- 无。

返回值：

- 返回字符串表示数据目录路径。

使用方法：

```javascript
let dataPath = await window.betterncm_native.app.getDataPath();
console.log(dataPath);
```

### app.readConfig

读取 BetterNCM 设置。

参数：

- key: 键。
- defaultValue: 默认值。

返回值：

- 返回字符串表示读取到的值。

使用方法：

```javascript
let configValue = await window.betterncm_native.app.readConfig('theme', 'dark');
console.log(configValue);
```

### app.writeConfig

设置 BetterNCM 设置。

参数：

- key: 键。
- value: 值。

返回值：

- 返回布尔值表示是否执行成功。

使用方法：

```javascript
let result = await window.betterncm_native.app.writeConfig('theme', 'light');
console.log(result);
```

### app.getNCMPath

获取网易云安装目录。

参数：

- 无。

返回值：

- 返回字符串表示安装目录。

使用方法：

```javascript
let ncmPath = await window.betterncm_native.app.getNCMPath();
console.log(ncmPath);
```

### app.showConsole

打开网易云主进程的Console。

参数：

- show: 是否显示Console窗口，默认为true。

返回值：

- 返回布尔值表示是否执行成功。

使用方法：

```javascript
let result = await window.betterncm_native.app.showConsole(false);
console.log(result);
```

### app.setRoundedCorner

设置Win11 DWM圆角开启状态。

参数：
 - enable: 是否开启圆角，默认为true。

返回值：

- 返回布尔值表示是否执行成功。

使用方法：

```javascript
let result = await window.betterncm_native.app.setRoundedCorner(false);
console.log(result);
```

### app.openFileDialog

打开一个选择文件对话框。

参数：

- filter: 要筛选的文件类型。
- initialDir: 对话框初始地址。

返回值：

- 返回字符串表示选择的文件地址，若未选择则为空字符串。

使用方法：

```javascript
let filePath = await window.betterncm_native.app.openFileDialog('.mp3', 'C:\\Users\\username\\Music');
console.log(filePath);
```

### app.isLightTheme

获取当前主题是否为亮色主题。

参数：

- 无。

返回值：

- 返回布尔值表示当前主题是否为亮色主题。

使用方法：

```javascript
let isLight = await window.betterncm_native.app.isLightTheme();
console.log(isLight);
```

### app.getSucceededHijacks

获取执行成功的 Hijack 日志。

参数：

- 无。

返回值：

- 返回字符串数组表示 Hijack 日志。

使用方法：

```javascript
let hijackLogs = await window.betterncm_native.app.getSucceededHijacks();
console.log(hijackLogs);
```

## utils 模块

### utils.waitForElement

等待指定的元素加载完成。

参数：

- selector: 元素选择器。
- interval: 检测间隔时间，默认为100毫秒。

返回值：

- 返回一个 Promise 对象，异步返回元素对象或者 null。

使用方法：

```javascript
let element = await window.betterncm_native.utils.waitForElement('#element_id');
console.log(element);
```

### utils.debounce

将指定的函数做防抖处理。

参数：

- callback: 需要被调用的回调函数。
- waitTime: 需要等待多长时间，单位毫秒。

返回值：

- 返回被包装后的防抖函数。

使用方法：

```javascript
function handleResize() {
	// do something
}
let debouncedResize = window.betterncm_native.utils.debounce(handleResize, 500);
window.addEventListener('resize', debouncedResize);
```

### utils.waitForFunction

重复调用某函数，直到其返回任意真值，并返回该真值。

参数：

- func: 函数
- interval: 重复调用时间间隔，默认为100毫秒。

返回值：

- 返回 Promise 对象，异步返回 `func` 函数的返回值。

使用方法：

```javascript
let result = await window.betterncm_native.utils.waitForFunction(() => {
    let element = document.querySelector('#element_id');
    if (element && element.textContent == 'Ready') {
        return true;
    }
});
console.log(result);
```

### utils.delay

创建一个将在一定时间后 resolve 的 Promise。

参数：

- ms: 延迟时间，以毫秒为单位。

返回值：

- 返回 Promise 对象，将在 `ms` 毫秒后 resolve。

使用方法：

```javascript
await window.betterncm_native.utils.delay(1000);
console.log('1 second passed');
```



## ncm 模块

#### findNativeFunction(obj: Object, identifiers: string)

在一个对象中查找包含给定标识符的函数，并返回函数名。

- `obj`: 要查找的对象。
- `identifiers`: 标识符数组。
- `returns`: 函数名。

#### openUrl(url: string)

在默认浏览器中打开 URL。

- `url`: 要打开的 URL。

#### getNCMPackageVersion()

获取 NCM 的包版本号。

- `returns`: NCM 的包版本号。

#### getNCMFullVersion()

获取 NCM 的完整版本号。

- `returns`: NCM 的完整版本号。

#### getNCMVersion()

获取 NCM 的版本号。

- `returns`: NCM 的版本号。

#### getNCMBuild()

获取 NCM 的 build 号。

- `returns`: NCM 的 build 号。

## fs 模块

#### readDir(folderPath: string)

异步读取指定文件夹路径下的所有文件和文件夹。

- `folderPath`:需要读取的文件夹路径。
- `returns`: 所有文件和文件夹的相对路径或绝对路径。

#### readFileText(filePath: string)

读取文本文件，务必保证文件编码是 UTF-8。

- `filePath`: 需要读取的文件路径。
- `returns`: 对应文件的文本形式。

#### readFile(filePath: string)

读取文件。

- `filePath`: 需要读取的文件路径。
- `returns`: 对应文件的 blob。

#### mountDir(filePath: string)

挂载路径。

- `filePath`: 需要挂载的文件夹路径。
- `returns`: 挂载到的 http 地址。

#### mountFile(filePath: string)

挂载路径。

- `filePath`: 需要挂载的文件路径。
- `returns`: 挂载到的 http 地址。

#### unzip(zipPath: string, unzipDest: string = `${zipPath}_extracted/`)

解压指定的 ZIP 压缩文件到一个指定的文件夹中。

- `zipPath`: 需要解压的 ZIP 压缩文件路径。
- `unzipDest`: 需要解压到的文件夹路径，如果不存在则会创建，如果解压时有文件存在则会被覆盖。
- `returns`: 返回值，是否成功。

#### writeFileText(filePath: string, content: string)

将文本写入到指定文件内。

- `filePath`: 需要写入的文件路径。
- `content`: 需要写入的文件内容。
- `returns`: 是否成功。

#### writeFile(filePath: string, content: string | Blob)

将文本或二进制数据写入到指定文件内。

- `filePath`: 需要写入的文件路径。
- `content`: 需要写入的文件内容。
- `returns`: 是否成功。

#### mkdir(dirPath: string)

在指定路径新建文件夹。

- `dirPath`: 文件夹的路径。
- `returns`: 是否成功。

#### exists(path: string)

检查指定路径下是否存在文件或文件夹。

- `path`: 文件或文件夹的路径。
-`returns`: 是否存在。

#### remove(path: string)

删除指定路径下的文件或文件夹。

- `path`: 指定的文件或文件夹路径。
- `returns`: 是否成功。

# BetterNCM Native API (C)

BetterNCM Native API 是 BetterNCM 插件开发的一部分，提供了一系列与系统交互的功能。这些功能包括文件读取、写入、重命名等等。以下是可用的 API 列表。

## fs.readDir

读取目录下的文件列表。

参数：

- path: 目录路径。

返回值：

- 返回一个数组，包含目录下所有文件和文件夹的名称。

使用方法：

```javascript
let files = window.betterncm_native.fs.readDir('/path/to/dir');
console.log(files);
```

## fs.readFileText

读取文件的文本内容。

参数：

- path: 文件路径。

返回值：

- 返回文件的文本内容。

使用方法：

```javascript
let content = window.betterncm_native.fs.readFileText('/path/to/file');
console.log(content);
```

## fs.readFileTextAsync

异步读取文件的文本内容。

参数：

- path: 文件路径。
- callback: 回调函数，它的参数为文件的文本内容。

返回值：

- 返回一个空值。

使用方法：

```javascript
window.betterncm_native.fs.readFileTextAsync('/path/to/file', function(content) {
    console.log(content);
});
```

## fs.watchDirectory

监视目录下的文件变化。

参数：

- path: 目录路径。
- callback: 回调函数，它的参数为变化的文件所在的目录和文件名。

返回值：

- 返回一个空值。

使用方法：

```javascript
window.betterncm_native.fs.watchDirectory('/path/to/dir', function(dir, file) {
    console.log('File ' + file + ' in directory ' + dir + ' changed.');
});
```

## fs.unzip

解压缩文件到指定目录。

参数：

- path: 压缩文件路径。
- dest: 目标目录路径。

返回值：

- 返回一个整数，表示操作是否成功。

使用方法：

```javascript
let result = window.betterncm_native.fs.unzip('/path/to/zip', '/path/to/dest');
console.log(result);
```

## fs.rename

重命名文件或目录，或创建新目录。

参数：

- path: 文件或目录路径。
- dest: 新的文件或目录路径。

返回值：

- 返回一个布尔值，表示操作是否成功。

使用方法：

```javascript
// 重命名文件
let result = window.betterncm_native.fs.rename('/path/to/oldfile', '/path/to/newfile');
console.log(result);

// 重命名目录
let result2 = window.betterncm_native.fs.rename('/path/to/olddir', '/path/to/newdir');
console.log(result2);

// 创建新目录
let result3 = window.betterncm_native.fs.rename('/path/to/newdir');
console.log(result3);
```

## fs.exists

检查文件或目录是否存在。

参数：

- path: 文件或目录路径。

返回值：

- 返回一个布尔值，表示文件或目录是否存在。

使用方法：

```javascript
let result = window.betterncm_native.fs.exists('/path/to/file');
console.log(result);
```

## fs.writeFileText

写入文本内容到文件。

参数：

- path: 文件路径。
- body: 文本内容。

返回值：

- 返回一个布尔值，表示操作是否成功。

使用方法：

```javascript
let result = window.betterncm_native.fs.writeFileText('/path/to/file', 'Hello, world!');
console.log(result);
```

## fs.remove

删除文件或目录。

参数：

- path: 文件或目录路径。

返回值：

- 返回一个布尔值，表示操作是否成功。

使用方法：

```javascript
let result = window.betterncm_native.fs.remove('/path/to/file');
console.log(result);
```

## app.reloadIgnoreCache

重新加载当前页面，忽略缓存。

参数：无。

返回值：

- 返回一个布尔值，表示操作是否成功。

使用方法：

```javascript
let result = window.betterncm_native.app.reloadIgnoreCache();
console.log(result);
```

## app.datapath

获取 BetterNCM 数据目录的路径。

参数：无。

返回值：

- 返回一个字符串，表示 BetterNCM 数据目录的路径。

使用方法：

```javascript
let path = window.betterncm_native.app.datapath();
console.log(path);
```

## app.ncmpath

获取 NCM 文件的路径。

参数：无。

返回值：

- 返回一个字符串，表示 NCM 文件的路径。

使用方法：

```javascript
let path = window.betterncm_native.app.ncmpath();
console.log(path);
```

## app.version

获取 BetterNCM 的版本号。

参数：无。

返回值：

- 返回一个字符串，表示 BetterNCM 的版本号。

使用方法：

```javascript
let version = window.betterncm_native.app.version();
console.log(version);
```

## app.restart

重启 BetterNCM。

参数：无。

返回值：

- 返回一个布尔值，表示操作是否成功。

使用方法：

```javascript
let result = window.betterncm_native.app.restart();
console.log(result);
```

## app.crash

导致 BetterNCM 崩溃，用于测试目的。

参数：无。

返回值：

- 无返回值。

使用方法：

```javascript
window.betterncm_native.app.crash();
```

## native_plugin.getRegisteredAPIs

获取已经注册的 Native Plugin 的 API 名称列表。

参数：无。

返回值：

- 返回一个数组，包含已经注册的 Native Plugin 的 API 名称。

使用方法：

```javascript
let apis = window.betterncm_native.native_plugin.getRegisteredAPIs();
console.log(apis);
```

## native_plugin.call

调用 Native Plugin 定义的 Native API。

参数：

- identifier: API 的标识符。
- args: 一个数组，包含调用 API 时传递的参数。

返回值：

- 返回 API 执行的结果。

使用方法：

```javascript
let result = window.betterncm_native.native_plugin.call('my_plugin.my_api', ['arg1', 2, true]);
console.log(result);
```