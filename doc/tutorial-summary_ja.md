# Angular Tutorial サマリー
* 一旦、自分用にまとめる。

## 1. Introduction
* 特に説明の必要はないかと。

## 2. The Application Shell
* Angular CLIと、Hello World的な感じの内容。
* 簡単なので後回し。
* schematics とは？
  - **[TODO]** あとで解説できるようにする

## 3. The Hero Editor

### Component の作成
* `@Component`: クラスがコンポーネントであることを示し、メタデータを提供する
* selector/templateUrl/styleUrls を自動で提供してくれる
* `ngOnInit`: lifecycle hook の一つ
  - lifecycle hookとは？: https://angular.io/guide/lifecycle-hooks#lifecycle-hooks **[TODO]**
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
* では、`@NgModule.imports`と`@NgModule.declarations`の違いは？ **[TODO]**
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

### @Input decorator
* 外部のコンポーネント（ここではHeoresCompnent）からバインドする場合、`@Input`を変数につける必要がある
* `Input`を`import`してから利用する

### One-way binding
* `[xxx]`は、一方向でのバインディングを意味する

## 6. Services

### なぜServiceを作るべきか？
* Componentは、表示にフォーカス
* データ取得についてはServiceに移譲すべきである
  - DIの仕組みを使って依存性の注入を行っていくよ
  - Componentはもはや、Serviceがどう動いているかは分からない

### @Injectable
* Angular CLIでServiceを作成すると、自動で付与される
* これを付与することは、DIシステムに参加することを意味する
* Angular CLIで作成するとまず、root injectorを利用して、Serviceのプロバイダーとして登録する
  - `providedIn: 'root'` というメタデータが`@Injectable`に書かれている状態
* Singletonで、共有できるインスタンスが生成され、他のクラスに注入することができる
  - **[TODO]** より詳しいProviderの説明は[ここ][1151e87d]
  - より詳しいDIの説明については[ここ][50d85cb4]

  [1151e87d]: https://angular.io/guide/providers "Providers"
  [50d85cb4]: https://angular.io/guide/dependency-injection "Dependency Injection in Angular"

### DIの注入
* コンストラクタの引数として入れる

`constructor(private heroService: HeroService) { }`

* この例だと、`heroService`パラメータを`HeroService`の単独のインスタンスに設定する

### Observable
* 非同期処理（HTTP通信など）を行う時の取り回しに`Observable`を利用する

### アロー関数 Arrow function
```
getHeroes(): void {
  this.heroService.getHeroes()
      .subscribe(heroes => this.heroes = heroes);
}
```
* 本題と離れるが、ちょっとクセがあるので解説を書く **[TODO]**

## 7. Routing

### AppRoutingModuleの作成
* Routerを一番上の階層に置き、`appModule`にimportするのがAngular Best Practice
* Angular CLIで生成すると`CommonModule`がimportされているが、Routerでは使わないので削除
* `@angular/router`ライブラリから`RouterModule`に入っている`Routes`を入れる
* `@NgModule.exports`に`RouterModule`を入れることで、あとで`AppModule`で使える

### Routes を使う
* Routeでは主に、2つの定義を行う
  1. path: パス
  2. component: Routerが作成する必要のあるComponentを指定

### RouterModule.forRoot()
* `import`にこれを入れる
  - `forRoot`メソッドが、URLに基づいた最初の読み込み（ルーティングに必要なServiceやDirective）を行ってくる

### RouterOutlet
* `app-component`に`router-outlet`を入れる

### リンクの挿入
* `routerLink`を使う

### 画面遷移ができるようにする (Routable HeroDetailComponent)
* `ActivatedRoute` `Location` をimportする
* この2つをコンポーネントのコンストラクタに入れる
* `this.location.back();`で、前の画面に戻れる

## 8. HTTP
* HttpClientを使う

### AsyncPipe（検索で利用）
```
<li *ngFor="let hero of heroes$ | async" >
```
* pipe character(|) に`async`を付ける
  - これにより`AsyncPipe`となり、`Observable`を自動でsubscribeする
* ちなみに`$`は、`heroes$`がarrayでなく`Observable`であることを示している

---

## その他、英語版Tutorialを読む上で役立つメモ
* decoratorとは？
  - クラスやプロパティの定義を変えるもの。`@NgModule`や`@Component`など

* directiveとは？
  - Grossaryでは：DOMの構造を変更したり、DOMおよびコンポーネントのデータモデルの属性を変更することができるクラス
  - とはいえ、一口にDirectiveと言っても3種類ある。詳しくは[ここ][2b530441]を見よう
  - 要するに、画面や画面の動きを変化させるもの、と捉えるとよさそう
  - [Qiita][3749937e]の翻訳資料が少し読みやすい。**[TODO]** あとでもっと理解し、簡単に解説できるようにしたい

  [2b530441]: https://angular.io/guide/glossary#directive "glossary#directive"
  [3749937e]: https://qiita.com/mixplace/items/836438a280ae60e8670a "angular.io Guide: Attribute Directives - Qiita"
