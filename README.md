# 软件项目实践实验2：构建Kotlin应用并使用Compose布局

## **实验1：创建首个Kotlin应用**

## 实验步骤

1. 打开 Android Studio，点击 **New Project**。选择 **Empty Activity** 模板。

![image](https://github.com/user-attachments/assets/78357a30-3603-44f2-a470-306081ec4306)

1. 语言选择 Kotlin，点击 **Finish** 完成创建。经过编译生成之后，运行app：

![image](https://github.com/user-attachments/assets/4798175f-d56f-489e-b5e0-ca79e03eb0af)


### 任务二：Compose布局实践

#### 微调界面

文件顶部添加 import 语句：

```kotlin
import androidx.compose.material3.Surface

import androidx.compose.material3.MaterialTheme
```
 `Surface` 设置背景颜色

```kotlin
@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
    Surface(color = MaterialTheme.colorScheme.primary) {
        Text(
            text = "Hello $name!",
            modifier = modifier
        )
    }
}
```

预览的效果：

![image](https://github.com/user-attachments/assets/90f92591-88fa-44e9-bf53-bc327181489d)


#### 修饰符

Compose 中使用 `Modifier` 来调整布局和样式

```kotlin
import androidx.compose.foundation.layout.padding
import androidx.compose.ui.unit.dp
// ...

@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
    Surface(color = MaterialTheme.colorScheme.primary) {
        Text(
            text = "Hello $name!",
            modifier = modifier.padding(24.dp)
        )
    }
}
```

![image](https://github.com/user-attachments/assets/18729e43-425a-42fb-8517-9bec215a57f0)


## 创建Compose中的列和行

```kotlin
import androidx.compose.foundation.layout.Column
// ...

@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
    Surface(color = MaterialTheme.colorScheme.primary) {
        Column(modifier = modifier.padding(24.dp)) {
            Text(text = "Hello ")
            Text(text = name)
        }
    }
}
```

更改预览效果，以模拟小屏幕手机的常见宽度 320dp。按如下所示向 @Preview 注解添加 widthDp 参数：

```kotlin
@Preview(showBackground = true, widthDp = 320)
@Composable
fun GreetingPreview() {
    Kotlin1Theme {
        MyApp()
    }
}

```

为修饰符添加更多的属性。使用 fillMaxWidth 和 padding 修饰符复制以下布局。
```kotlin
import androidx.compose.foundation.layout.fillMaxWidth

@Composable
fun MyApp(
    modifier: Modifier = Modifier,
    names: List<String> = listOf("World", "Compose")
) {
    Column(modifier = modifier.padding(vertical = 4.dp)) {
        for (name in names) {
            Greeting(name = name)
        }
    }
}

@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
    Surface(
        color = MaterialTheme.colorScheme.primary,
        modifier = modifier.padding(vertical = 4.dp, horizontal = 8.dp)
    ) {
        Column(modifier = Modifier.fillMaxWidth().padding(24.dp)) {
            Text(text = "Hello ")
            Text(text = name)
        }
    }
}

```

![image](https://github.com/user-attachments/assets/f7ae97ae-3aed-4aa5-9020-f497976b23dc)


### 5.添加按钮

向 Greeting 添加可点击元素

```kotlin
import androidx.compose.foundation.layout.Row
import androidx.compose.material3.ElevatedButton
// ...

@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
    Surface(
        color = MaterialTheme.colorScheme.primary,
        modifier = modifier.padding(vertical = 4.dp, horizontal = 8.dp)
    ) {
        Row(modifier = Modifier.padding(24.dp)) {
            Column(modifier = Modifier.weight(1f)) {
                Text(text = "Hello ")
                Text(text = name)
            }
            ElevatedButton(
                onClick = { /* TODO */ }
            ) {
                Text("Show more")
            }
        }
    }
}

```

![image](https://github.com/user-attachments/assets/a8d417ef-2507-44a3-b363-fd48a590f38c)


### 6.Compose中的状态（State）

将向屏幕中添加一些互动

具体代码：

```kotlin
@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
    val expanded = remember { mutableStateOf(false) }
    val extraPadding = if (expanded.value) 48.dp else 0.dp
    Surface(
        color = MaterialTheme.colorScheme.primary,
        modifier = modifier.padding(vertical = 4.dp, horizontal = 8.dp)
    ) {
        Row(modifier = Modifier.padding(24.dp)) {
            Column(
                modifier = Modifier
                    .weight(1f)
                    .padding(bottom = extraPadding)
            ) {
                Text(text = "Hello ")
                Text(text = name)
            }
            ElevatedButton(
                onClick = { expanded.value = !expanded.value }
            ) {
                Text(if (expanded.value) "Show less" else "Show more")
            }
        }
    }
}

```

![image](https://github.com/user-attachments/assets/af2c026f-5a4f-41fb-b690-ce2bd76f0c49)


