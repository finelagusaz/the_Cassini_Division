シェルについて
=========

- お座り関係はosuwari.mdを参照

サーフェイス値加算による着せ替え
---------------------------------

- ゴースト側で着せ替えをするため、サーフェイス値加算処理を行っている
- お座り関係で実装したもので、純粋に着せ替えるだけなら、シェル側の着せ替え定義で問題ない
- サーフェイス値加算処理はトランスレートを使っている
- 座り関連、着せ替え関連メニューの表示非表示指定は`flgNoSfcnv`変数で行う

追加シェルごとの特殊対応
--------------------------

### 追加シェル「Gemini」

- Geminiはソロモードと双子モードの切り替えができる

#### cassis_menu.dic

- `GetShellnameEx`関数で双子モード（Gemini）なのか、ソロモード（Pollux、Castor）の判定を行う
- `menuGemini`で切替と手を繋ぐ・離すの処理
- `menuGeminiPollux`、`menuGeminiCastor`、`menuGeminiPolluxAndCastor`でポルックス、カストール、双子の切替
- `menuGeminiTuckup`で脱衣
- `menuGeminiDress`で着衣

#### cassis_mouse_core.dic

- `EMGetPrefix`にシェル名での処理を追加
- マウス反応辞書を分離

### 追加シェル「桜吹雪」

- サーフェイス値加算は次の変数の合算
	- SakurafubukiBase : 時間ごと
	- SakurafubukiFox : 狐耳
	- SakurafubukiPhase : フェイズ