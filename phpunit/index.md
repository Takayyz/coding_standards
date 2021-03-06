# PHPUnitコーディング規約

PHPUnitに関するコーディング規約です。

## 概要
### 全体に関する内容
- テストメソッド名
- groupアノテーションの命名
- テストコードでの型厳格指定

### Repositoryレイヤー
- 作成すべきテストデータ件数
- 別レイヤーでバリデーションされるはずの値に対するテスト
- Eagerloadされているかのテスト
- 不要と感じるアサーション
- その他

### Serviceレイヤー

### Controllerレイヤー

### その他
---

## 全体に関する内容
### 1. テストメソッド名
テストメソッド名は日本語 or 英語 => 未定  
次回社内開発でテスト実装する際に日本語版テストメソッドを試し、英語版とのメリット・デメリットを比較しGizumoのスタンダードを決定していく。

### 2. groupアノテーションの命名
- groupアノテーションには基本的には**テスト対象となるメソッド名**を指定
- アノテーションには`test`というprefixはつけない
- 必要な時だけ記述する

  例えば、idに紐付くレコードを取得する`fetchById`というメソッドに対して、成功・失敗する場合の2種類のテストケースを用意する場合、`@group fetchById`というアノテーションでグルーピングする。

### 3. テストメソッドへの型厳格指定
テストメソッドの返り値はほとんどが`void`なので指定は不要。

---

## Repositoryレイヤー
### 1. 作成すべきテストデータ件数
引数に渡したidに紐付くレコードを取得するようなメソッドをテストする際、**厳密にテストするなら**複数件のテストデータを作成するべき。

### 2. 別レイヤーでバリデーションされるはずの値に対するテスト

### 3. Eagerloadされているかのテスト
Eagerloadを実装している場合は、Eagerloadされているかのテストは必要。
#### テスト方法
リレーションを設定したクラス名の同名プロパティがデフォルトだと`null`なので、**そのプロパティがnullでなければ**Eagerloadできているとみなせる。

### 4. 不要と感じるアサーション
型厳格で実装している場合、以下のような返り値の型に関するアサーションは不要。

```php
$this->assertInstanceOf(Collection::class, $actual);
```
### 5. その他
テスト対象メソッド内で使用しているメソッドを呼び出して取得した値を期待値として比較しても同値になることは明白なので、テスト対象のロジックとは別の方法を使用して同じ状況を再現できるようにする。

---

## Serviceレイヤー

---

## Controllerレイヤー

---

## その他
- 単体でテストしにくいものは結合にまわすことも検討する
