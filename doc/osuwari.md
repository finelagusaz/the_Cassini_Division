# Osuwari.dll対応について

## Osuwari.dllとは

[Ukiwiki](http://ukiya.sakura.ne.jp/)で公開されているSAORI。

ゴーストがタスクバーやアクティブウィンドウのタイトルバーに座れるようになる。

## 内部でやっていること

- サーフェイス値加算処理
  - サーフェイスの立っている状態と座っている状態の切替
- Osuwari.dllの制御
  - Osuwari.dllを呼び出し、どこに座らせるか、あるいは座らせないか

## 対応の範囲

- サーフェイス値加算だけを使うシェルと、Osuwari.dllで実際に座るシェルがある
- Osuwari.dllで座れるのは、`OsuwariStart`に座標を書いたシェルだけ（master、Eternity Black、拡大鏡、White Lolita、銀色、瑠璃、月白）
- それ以外のシェルは、サーフェイス値加算による着せ替えだけを使っている

## Osuwari.dllに対応させるには

### cassis_menu.dic

#### Menu_Shell

- シェルごとの特殊メニュー
- 座り対応であれば`when "master"`から始まる行にシェル名を追記
- 専用のメニューを持たせるなら`menu/shell/`に辞書を足して、ここから呼ぶ（立つ・座るの項目から`SurfaceModeChangeEx`を呼ぶ。`menu/shell/master.dic`を参照）

### cassis_shell.dic

#### GetShellVarPrefix

- 現在のシェルの、シェルごとの変数の接頭辞（hogeSurfaceModeとhogeOsuwariModeの「hoge」）を返す
- シェル名と変数の対応は、ここだけに書く。シェルを足したら、ここに`when`の行を足す。足し忘れると、そのシェルでは加算されず、座り関連、着せ替え関連メニューも出ない
- `SurfaceModeChangeEx`、`GetSurfaceOffset`、`GetOsuwariMode`がここから変数名を組み立てて読み書きするので、この3つにシェルごとの記述は要らない
- 桜吹雪は3つの変数の合算なので載せない（`GetSurfaceOffset`が直接扱う）

#### SurfaceModeChangeEx

- シェルごとに加算したいサーフェイス値（hogeSurfaceMode）とお座りの状態（hogeOsuwariMode）を指定する
- 第1引数に加算したいサーフェイス値
- 第2引数にお座りの状態
  - 0:停止
  - 1:アクティブウィンドウのタイトルバーに座る
  - 2:タスクバーに座る

#### GetSurfaceOffset

- 現在のシェルの加算したいサーフェイス値（`SurfaceModeChangeEx`で指定したhogeSurfaceMode）を返す。変数は書き換えない
- サーフェイス値加算に対応していないシェル（`GetShellVarPrefix`に載っていないシェル）では-1を返す

#### IsSfcnvShell

- 現在のシェルがサーフェイス値加算に対応しているか（`GetSurfaceOffset`が0以上か）を返す
- 座り関連、着せ替え関連メニューの表示非表示の判定に使う。シェルごとの記述は要らない

#### GetOsuwariMode

- 現在のシェルのお座りの状態（hogeOsuwariMode）を返す
- 「膝枕」のように、座っているときだけ出す反応の判定に使う
- `GetShellVarPrefix`に載っていないシェルでは0（停止）を返す

#### OsuwariStart

- 座り制御関数
- シェルごとに座った座標を指定する
- 使い方は[Osuwari.dll version 2 取り扱い説明書 version2.1.0.0 - Ukiwiki](http://ukiya.sakura.ne.jp/index.php?%E8%87%AA%E4%BD%9CSAORI%2F%E3%81%8A%E5%BA%A7%E3%82%8A%E3%83%9E%E3%83%8B%E3%83%A5%E3%82%A2%E3%83%AB)を参照

#### OsuwariStop

- 座りの停止。シェルごとの記述は要らない

#### ShellCompatibility

- 古い保存データの互換処理（加算値が1桁で保存されていた頃の値を1000倍に直す）
- 新しく足すシェルには要らない
