# Dart 初心者程式碼筆記

## Reference 
- 第一個Flutter應用程式 : https://codelabs.developers.google.com/codelabs/flutter-codelab-first?hl=zh-tw#3
- What is the Root widget and the Leaf widgets in Flutter? : https://medium.com/@chetan.akarte/the-flutter-foundation-a-comprehensive-guide-for-technical-interviews-and-beyond-book-by-124b3539f02d
- Markdown 總複習 (Daniel Horng): https://hackmd.io/@HungTengKuei/HyUYP3Lrs
- Markdown 教程 : https://markdown.com.cn/basic-syntax/images.html
## main.dart 範例分析

### ==> 行前須知 <=======================================

**widget架構**

![Widget 架構](/image_lib/Structure_of_widget.png "Widget_Structure")


|keyword|meaning|
|:--------:|:--------:|
|```main```|城市入口，用runApp啟動Flutter應用|
|```MyApp```|會設定整個應用，包括層級(?)、APP命名、視覺主題等等|
|```MyAppState```|一個管理狀態類別，繼承 ChangeNotifier |
|```MyHomePage```|應用的主要頁面，繼承 StatelessWidget |

**root widget 根組件** : The top-level widget in the widget tree. 

- 根組件定義了App一些必須功能，像是主題、導向結構、平台的一些特殊行為

### ==================================================

### 程式結構簡介

```dart
class MyApp extends StatelessWidget{}
class MyAppState extends ChangeNotifier{}
class MyHomePage extends StatelessWidget{}
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
- ```MyAppState``` 定義了App所需的資料(變數、函式等)
- ```ChangeNotifier``` 是 Flutter 提供的一個類別，用來讓物件支援通知機制



