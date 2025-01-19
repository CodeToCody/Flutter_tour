# Dart 初心者程式碼筆記

## Reference 
- 第一個Flutter應用程式 : https://codelabs.developers.google.com/codelabs/flutter-codelab-first?hl=zh-tw#3
- What is the Root widget and the Leaf widgets in Flutter? : https://medium.com/@chetan.akarte/the-flutter-foundation-a-comprehensive-guide-for-technical-interviews-and-beyond-book-by-124b3539f02d
- Markdown 總複習 (Daniel Horng): https://hackmd.io/@HungTengKuei/HyUYP3Lrs
## main.dart 範例分析

### ==> 行前須知 <=======================================
|keyword|meaning|
|:--------:|:--------:|
|```main```|城市入口，用runApp啟動Flutter應用|
|```MyApp```|整個應用的root組件(?)|
|```MyAppState```|一個管理狀態類別，繼承 ChangeNotifier |
|```MyHomePage```|應用的主要頁面，繼承 StatelessWidget |

**root widget 根組件** : The top-level widget in the widget tree. 

- 根組件定義了App一些必須功能，像是主題、導向結構、平台的一些特殊行為

### ==================================================

### 程式結構簡介

```dart
import 'package:english_words/english_words.dart';
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
```
- runApp() 是 Flutter 提供的函式，將一個 root 組件插進系統，啟動程式
- MyApp() 是我們定義的 root 組件

```dart
void main() {
  runApp(MyApp());
}
```

```dart
class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return ChangeNotifierProvider(
      create: (context) => MyAppState(),
      child: MaterialApp(
        title: 'Namer App',
        theme: ThemeData(
          useMaterial3: true,
          colorScheme: ColorScheme.fromSeed(seedColor: Colors.deepOrange),
        ),
        home: MyHomePage(),
      ),
    );
  }
}
```
```dart
class MyAppState extends ChangeNotifier {
  var current = WordPair.random(); //WordPair.random()

  void getNext(){
    current = WordPair.random();
    notifyListeners();
  }
}
```

```dart
class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    var appState = context.watch<MyAppState>();

    return Scaffold(
      body: Column(
        children: [
          Text('Test the real time:'),
          Text(appState.current.asLowerCase),
          ElevatedButton(
            onPressed: () {
              appState.getNext();
            },
            child: Text('Next'),
          ),
        ],
      ),
    );
  }
}
```