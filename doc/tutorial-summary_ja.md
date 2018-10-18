# Angular Tutorial サマリー
* 一旦、自分用にまとめる。

## 1. Introduction
* 特に説明の必要はないかと。

## 2. The Application Shell
* Angular CLIと、Hello World的な感じの内容。
* 簡単なので後回し。

### 分からなかったところ
* schematics とは？
  - **TODO** あとで解説できるようにする

## 3. The Hero Editor

### Component の作成
* `@Component`: クラスがコンポーネントであることを示し、メタデータを提供する
* selector/templateUrl/styleUrls を自動で提供してくれる
* `ngOnInit`: lifecycle hook の一つ
  - lifecycle hookとは？: https://angular.io/guide/lifecycle-hooks#lifecycle-hooks **TODO**
* 常に`export` - あとで,他のところで`import`できる

### Pipe
* 文字のフォーマットを整えてくれるものだと思えばよい

### 双方向バインディング
* `[(ngModel)]` を利用する
  - `ngModule`と混同しやすいので注意
* ただし、利用するには`FormsModule`をimportする必要がある
  - import文の記載
  - `app.module.ts`ファイルに`@NgModule`があり、ここの`@NgModule.imports`に加える

### NgModule
* すべてのcomponentは、一つの`NgModule`で明記されている必要がある
* `NgModule`は、必要なクラスを纏めたもの、と捉えると理解しやすそう
* 基本はAngular CLIが勝手にやってくれる
  - import
  - @NgModule.declarations
* では、`@NgModule.imports`と`@NgModule.declarations`の違いは？ **TODO**
  - https://stackoverflow.com/questions/39062930/what-is-difference-between-declarations-providers-and-import-in-ngmodule

### NgModuleについて補足
* `AppModule`というのがあるが、これはAngular CLIが基本的にはデフォルトで作成するルートモジュールのこと
  - `app.module.ts`に自動生成されている
* **TODO** 以下をあとで読む
  - https://angular.io/guide/bootstrapping
  - https://angular.io/guide/ngmodules

## 4. Display a Heroes List

### ngFor/ngIf
* `ngFor`は、Angularでループさせるためのディレクティブ

### Event binding
* 例えばこんなの。`<button (click)="onSave()">Save</button>`。()で囲う
* 他にもいろいろある。https://angular.io/guide/template-syntax#event-binding---event-

### Class binding
* 条件によって、CSSのクラスを追加したり削除したりできる

## 5. Master/Detail Components
* ここから、コンポーネントの分割を行う
  - 一つのコンポーネントに纏めてしまうとメンテしにくくなるため

* **TODO** 次はここから書く

---

## その他、英語版Tutorialを読む上で役立つメモ
* decoratorとは？
  - クラスやプロパティの定義を変えるもの。`@NgModule`や`@Component`など

* directiveとは？
  - Grossaryでは：DOMの構造を変更したり、DOMおよびコンポーネントのデータモデルの属性を変更することができるクラス
  - とはいえ、一口にDirectiveと言っても3種類ある。詳しくは[ここ][2b530441]を見よう
  - 要するに、画面や画面の動きを変化させるもの、と捉えるとよさそう
  - [Qiita][3749937e]の翻訳資料が少し読みやすい。**TODO** あとでもっと理解し、簡単に解説できるようにしたい

  [2b530441]: https://angular.io/guide/glossary#directive "glossary#directive"
  [3749937e]: https://qiita.com/mixplace/items/836438a280ae60e8670a "angular.io Guide: Attribute Directives - Qiita"
