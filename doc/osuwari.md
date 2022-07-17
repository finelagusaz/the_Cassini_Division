# Osuwari.dll対応について

## Osuwari.dllとは

[Ukiwiki](http://ukiya.sakura.ne.jp/)で公開されているSAORI。

ゴーストがタスクバーやアクティブウィンドウのタイトルバーに座れるようになる。

## 内部でやっていること

- サーフェイス値加算処理
  - サーフェイスの立っている状態と座っている状態の切替
- Osuwari.dllの制御
  - Osuwari.dllを呼び出し、どこに座らせるか、あるいは座らせないか

## Osuwari.dllに対応させるには

### cassis_menu.dic

#### menuChange

- シェルごとの特殊メニュー
- 座り対応であれば`when "master"`から始まる行にシェル名を追記

### cassis_shell.dic

#### SurfaceModeChangeEx

- シェルごとに加算したいサーフェイス値（hogeSurfaceMode）とお座りの状態（hogeOsuwariMode）を指定する
- 第1引数に加算したいサーフェイス値
- 第2引数にお座りの状態
  - 0:停止
  - 1:アクティブウィンドウのタイトルバーに座る
  - 2:タスクバーに座る

#### SurfaceModeChange

- シェルごとのサーフェイス値加算を変数「`SurfaceMode`」に代入する
- `SurfaceModeChangeEx`で作成したシェルごとの加算したいサーフェイス値を`SurfaceMode`に代入

#### OsuwariStart

- 座り制御関数
- シェルごとに座った座標を指定する
- 使い方は[Osuwari.dll version 2 取り扱い説明書 version2.1.0.0 - Ukiwiki](http://ukiya.sakura.ne.jp/index.php?%E8%87%AA%E4%BD%9CSAORI%2F%E3%81%8A%E5%BA%A7%E3%82%8A%E3%83%9E%E3%83%8B%E3%83%A5%E3%82%A2%E3%83%AB)を参照