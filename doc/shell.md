# シェルについて

- お座り関係はosuwari.mdを参照

## サーフェイス値加算による着せ替え

- ゴースト側で着せ替えをするため、サーフェイス値加算処理を行っている
- お座り関係で実装したもので、純粋に着せ替えるだけなら、シェル側の着せ替え定義で問題ない
- サーフェイス値加算処理はトランスレートを使っている（`cassis_aitalk.dic`の`OnTranslate`から`cassis_shell.dic`の`sfcnv`を呼ぶ）
- 座り関連、着せ替え関連メニューの表示非表示指定は`flgNoSfcnv`変数で行う

### 加算の対象

- 辞書のトークには加算前の値を書く（`\s[6]`と書けば、座っているときは`\s[1006]`になる）
- `sfcnv`はスコープの切り替え（`\0` `\h` `\1` `\u` `\p[n]`）を出現順に追って、スコープごとに加算するか決める
  - `\0`側: 常に加算する
  - `\1`側: シェルが「Gemini」のときだけ加算する。ほかのシェルの`\1`は`\s[10]`（空隙）しかなく、加算すると`\s[1010]`のような存在しないサーフェイスになるため
  - `\p[2]`以降: 加算する
- `\s[-1]`（非表示）は加算しない

## 追加シェルごとの特殊対応

### 追加シェル「Gemini」

- Geminiはソロモードと双子モードの切り替えができる
- `\0`がポルックス、`\1`がカストール。`\1`側にも表情差分があり、サーフェイス値加算の対象になる（`\1\s[16]`が`\s[2016]`になる）

#### cassis_shell.dic

- `GetShellnameEx`関数で双子モード（Gemini）なのか、ソロモード（Pollux、Castor）の判定を行う

#### menu/shell/gemini.dic

- `Menu_Gemini`で切替と手を繋ぐ・離すの処理
- `Menu_GeminiPollux`、`Menu_GeminiCastor`、`Menu_GeminiPolluxAndCastor`でポルックス、カストール、双子の切替
- `Menu_GeminiTuckup`で脱衣
- `Menu_GeminiDress`で着衣

#### cassis_mouse_core.dic

- `EMGetPrefix`にシェル名での処理を追加
- マウス反応辞書を分離（`cassis_mouse_gemini.dic`。関数名は双子モードが`GeminiMouse`、カストールのソロモードが`CastorMouse`で始まる）

### 追加シェル「桜吹雪」

- サーフェイス値加算は次の変数の合算
  - SakurafubukiBase : 時間ごと
  - SakurafubukiFox : 狐耳
  - SakurafubukiPhase : フェイズ
- マウス反応辞書は`cassis_mouse_socb.dic`（関数名は`SakurafubukiMouse`で始まる）
