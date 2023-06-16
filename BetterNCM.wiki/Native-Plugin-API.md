## BetterNCM Native Plugin API (C)

BetterNCM Native Plugin API 是为 BetterNCM 提供本地插件支持的 API，支持 C++ 编写的本地插件。

### PluginAPI 结构体

```c++
struct PluginAPI {
    int (*addNativeAPI)(NativeAPIType args[], int argsNum, const char* identifier, char* function(void**));
    const char* betterncmVersion;
    NCMProcessType processType;
    const unsigned short(*ncmVersion)[3];
};
```

#### addNativeAPI

```c++
int addNativeAPI(NativeAPIType args[], int argsNum, const char* identifier, char* function(void**));
```

向 BetterNCM 注册一个插件提供的 API。

参数：

- `args[]`：一个包含所有 API 的参数类型的数组。
- `argsNum`：参数的数量。
- `identifier`：API 标识符，全局唯一。
- `function`：API 实现函数的指针。

返回值：0 表示成功注册。

示例：

```c++
// 向 BetterNCM 注册一个名为"example.test" 的 API，参数类型为 V8Value，参数数量为 1，实现函数为 testAPI。

int testAPI(void** args) {
    cef_v8value_t* arg = *((cef_v8value_t**)args[0]);
    int result = arg->GetIntValue(arg);
    return result;
}

int BetterNCMPluginMain(BetterNCMNativePlugin::PluginAPI* api)
{
    api->addNativeAPI(new BetterNCMNativePlugin::NativeAPIType[1]{ BetterNCMNativePlugin::NativeAPIType::V8Value }, 1, "example.test", testAPI);
    return 0;
}
```

```c++
// 向 BetterNCM 注册一个名为 "example.multiply" 的API，接受两个 Double 类型的参数并返回它们的乘积。
double multiply(void** args) {
    double a = *((double*)args[0]);
    double b = *((double*)args[1]);
    return a * b;
}

int BetterNCMPluginMain(BetterNCMNativePlugin::PluginAPI* api)
{
    api->addNativeAPI(new BetterNCMNativePlugin::NativeAPIType[2]{ BetterNCMNativePlugin::NativeAPIType::Double, BetterNCMNativePlugin::NativeAPIType::Double }, 2, "example.multiply", multiply);
    return 0;
}
```

#### betterncmVersion

```c++
const char* betterncmVersion;
```

BetterNCM 版本号。

示例：

```c++
std::cout << "BetterNCM version: " << api->betterncmVersion << std::endl;
```

#### processType

```c++
enum NCMProcessType {
    Undetected = 0x0,
    Main = 0x0001,
    Renderer = 0x10,
    GpuProcess = 0x100,
    Utility = 0x1000,
};
```

当前插件所在进程类型。

示例：

```c++
if (api->processType == NCMProcessType::Main) {
    // 主进程
} else if (api->processType == NCMProcessType::Renderer) {
    // 渲染进程
}
```

#### ncmVersion

```c++
const unsigned short (*ncmVersion)[3];
```

NCM 版本号。

示例：

```c++
const unsigned short (*ncmVersion)[3] = api->ncmVersion;
std::cout << "NCM version: " << (*ncmVersion)[0] << "." << (*ncmVersion)[1] << "." << (*ncmVersion)[2] << std::endl;
```

### NativeAPIType 枚举

```c++
enum NativeAPIType {
    Int,
    Boolean,
    Double,
    String,
    V8Value,
};
```

API 参数类型枚举。

- `Int`：整型。
- `Boolean`：布尔型。
- `Double`：双精度浮点型。
- `String`：字符串型。
- `V8Value`：V8 引擎值。
