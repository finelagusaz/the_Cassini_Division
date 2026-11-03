# GHOST.md

このゴーストに固有の情報です。AI エージェントは、作業の前に `AGENTS.md` とあわせて読みます。
作者が自由に書き換えるファイルで、スキル `ukagaka-developer` の更新で上書きされることはありません。

## このゴーストについて

- 名前（`ghost/master/descript.txt` の `name`）: カッシーニの空隙（フォルダ名 `the_Cassini_Division`、付属バルーン `t_c_d`）
- キャラクター（`sakura.name` / `kero.name`）: カシス / 間隙
- 作者: Fine Lagusaz（フィーネ・ラグサズ）
- 配布先・ネットワーク更新の URL: https://blankrune.sakura.ne.jp/ ／ 更新は https://blankrune.sakura.ne.jp/named/the_Cassini_Division/update/ （`ghost/master/yaya_homeurl.txt`）
- 元にしたテンプレートやゴースト: 「文 ゴーストテンプレート」（umeici 作、YAYA 開発チーム改変。`yaya_tmpl_util.dic`）
- SAORI: `Osuwari.dll`（すわりモード。`cassis_shell.dic`）
- 設定メモ: ルートの `memo.txt` に、カシスの人物設定と用語解説（あのヒト＝坂下 命、あの子＝アルギズ など）がある。トークを書く前に読む。

## ライセンス

- 辞書: readme の FSW 宣言により、世界観からキャラクターまで全設定を開放（フリーシェアワールド）。テンプレート部分は「文」の条件（使途を限定せず自由に利用可。`ghost/master/readme-original.txt`）。システム辞書は `ghost/master/system/LICENSE`。
- シェル `master`: サトウ Ｍ 作のフリーシェル「しろ」（配布サイト「TCG」、現在は閲覧不可）。ライセンスは不明（配布サイトが閉じており、作者にも分からない）。改変や再配布の可否を確かめられないので、このシェルの画像は編集しない。
- シェル `alternative_cassis`: 吉野桜 作のフリーシェル「Ｐ＆Ｗ＆Ｆ ver.1.3」を、使用の快諾を得て改造したもの。非営利目的に限り、改変、転載、再配布は自由とのこと。
- そのほかの追加シェル（`.gitignore` にある gemini、sakurafubuki など）はこのリポジトリの管理外。

## 辞書の構成

- 文字コード: 辞書は UTF-8。`ghost/master/descript.txt` と `install.txt` は UTF-8（先頭に `charset,UTF-8`、改行は CRLF）。`ghost/master/system_config.txt`、`shell/*/descript.txt`、`surfacetable.txt`、`t_c_d/descript.txt` は Shift_JIS なので、文字コードを変えない。
- 読み込む辞書（`ghost/master/yaya.txt` の `dic` / `dicdir`）: `yaya_tmpl_util.dic`、`cassis_*.dic`（下の表）、`dicdir, menu/shell`、`dicdir, menu/command`、`yaya_homeurl.txt`。辞書は `ghost/master/` の直下にあり、`dic/` フォルダは無い。
- 緊急モード（`yaya_emerg.txt`）: `yaya_emerg_dic.txt` と `yaya_homeurl.txt`
- システム辞書: `ghost/master/system/`（`system_config.txt` の `dicdir, system` で読み込む）
  - submodule ではなく、普通のファイルとして置いてある。
  - 更新は、yaya.dll と組にして `ukagaka-developer` の手順で行う。lint（`yaya_base/lint.dic`）も、このシステム辞書が提供する。

## イベントと辞書ファイルの対応

| ファイル | 主な中身 |
|---|---|
| `cassis_aitalk.dic` | ランダムトーク（`RandomTalk` / `RandomTalkEx`、`aryNormalTalk`・季節・時間帯・好感度・シェル別の配列）、`OnTranslate`、`OnSecondChange`、`OnMinuteChange`、見切れ、`OnOtherGhostTalk`、チェイントーク |
| `cassis_aitalk_gemini.dic` | 追加シェル「Gemini」用のトーク |
| `cassis_bootend.dic` | `OnBoot`、`OnFirstBoot`、`OnClose`、`OnInputUsername`、`GetTimeSlot`、`GetSeasonSlot`、バレンタイン |
| `cassis_communicate.dic` | `OnCommunicate`、ユーザーへの返答（`com*`。対応ワードは `readme.txt`）、他ゴーストへの返答 |
| `cassis_mouse_core.dic` | `OnMouseMove`、`OnMouseDoubleClick`、`OnMouseClickEx`、`OnMouseWheel` の振り分け |
| `cassis_mouse.dic` | 通常シェルのマウス反応 |
| `cassis_mouse_gemini.dic` / `cassis_mouse_socb.dic` / `cassis_mouse_special.dic` | Gemini（`Castor*`）、桜吹雪（`Sakurafubuki*`）、The Hand（`OnHandActivate`、`TheHand*`）用のマウス反応 |
| `cassis_menu.dic`、`menu/shell/*.dic`、`menu/command/command.dic` | メニュー（`OpenMenu`）、シェル別メニュー、コマンド、Web 拍手（`OnInputWebclap`） |
| `cassis_change.dic` | ゴースト切り替え（`OnGhostChanging` / `OnGhostChanged` と相手別の `_54`・`_Eris`・`_Hand`・`_deadend`）、`OnGhostCalled`、`OnOtherGhost*` |
| `cassis_etc.dic` | メールチェック、ヘッドライン、時計合わせ、インストール、nar 作成などの各種イベント、`TextOnlyTranslatorFunc`（自動ウェイト） |
| `cassis_aprication.dic` | アプリケーション、猫どりふ、きのこ、`OnBatteryLow` |
| `cassis_shell.dic` | `OnShellChanged`、着せ替え、すわりモード（Osuwari）、サーフェス値の加算（`sfcnv`） |
| `cassis_sck.dic` | `OnKeyPress`（t・m・c・d・a・g） |
| `cassis_property.dic` / `cassis_string.dic` / `cassis_word.dic` | プロパティ、文字列リソース（`On_*`）、単語 |

新しいイベントに反応させるときに書く場所: 上の表で種類の近いファイル。どれにも当たらないものは `cassis_etc.dic`。新しいファイルを足すときは `yaya.txt` に `dic,` の行を足す（`ghost/master/` 直下は `dicdir` ではない）。

## キャラクターとサーフェス

| スコープ | キャラクター | 人物像（一人称、口調、性格） | 使えるサーフェス |
|---|---|---|---|
| `\0` | カシス | 一人称「私」、二人称「あなた」（名前は `%username`）、三人称は呼び捨て。語尾は「〜かしら」「〜の」「〜のね」「〜のよ」「〜わ」「〜わよ」「〜わね」「〜なさい」「〜しょう」。基本は常体で、命令するときだけ敬体。物言いは厳しく突き放し気味。人間を「ヒト」と書く。ヒトではない不定形の存在（FS）で、己の生きる世界とヒトへの想いを語る。表情は乏しい。詳しくは `memo.txt` | 0 素、1 照れ、2 驚き、3 不安/胸を隠す、4 落ち込み、5 笑い、6 目とじ、7 怒り、8 冷笑、9 首振り、30 スカートめくられ、31 スカートおさえ、32 攻撃（30〜32 はマウス反応などの特別な場面用）。ふだんのトークはほぼ 0 と 6 |
| `\1` | 間隙（追加シェル「Gemini」ではカストール） | 通常のシェルでは台詞が無く、トークの頭で `\1\s[10]` を指定して佇むだけ。Gemini のときだけ、カストールとして話す（`\0` 側はポルックスと呼ばれる。下の「Gemini の掛け合い」）。口調はカシスと同じ系統（「〜わ」「〜かしら」「〜わね」）。カストールは、カシスの性格から切れ味を少し増した人物。ポルックス（`\0` 側）は、カシスの性格をややマイルドにした人物 | 通常は 10 空隙のみ。Gemini では 10 素、11 照れ、12 驚き、13 不安/胸を隠す、14 落ち込み、15 笑い、16 目とじ、17 怒り、18 冷笑、19 恥じらい、40・41 スカート（`shell/gemini/surfacetable.txt` の 2010 番台に当たる） |

- 当たり判定（`surfaces.txt` の `collision`）: `Head`、`Lip`、`Bust`、`Skirt`（すわり時は `Skirt_s`）、`Wing`
- トークで使わないサーフェス:
  - 1000〜1009、1030〜1032（すわり）: 手で書かない。`OnTranslate` の `sfcnv` が、すわりモードのとき `\0` 側の `\s[N]` に 1000 を自動で足す。`\1` 側に足すのは Gemini のときだけ（詳しくは `doc/shell.md`）。
  - `surfacetable.txt` の `__disabled` グループ（1011、1012、18xx、19xx）
  - 11〜19、40 番台: Gemini の `\1`（カストール）用。Gemini 向けの辞書と分岐の中でだけ使う。通常のシェルの `\1` は 10 だけ。
- `alternative_cassis` は `alias.txt` で同じ番号（0〜9、30〜32）を引き当てるので、トークは master と同じ番号で書ける。

## トークの書き方

- 通常のシェルでは、頭は必ず `\1\s[10]\0\s[番号]`。間隙を表示してから、カシスが話す。最後は `\e`。
- Gemini の掛け合い: 追加シェル「Gemini」では、`\0`（ポルックス）と `\1`（カストール）の二人とも話す。
  - 書く場所: `cassis_aitalk_gemini.dic`、`cassis_mouse_gemini.dic`、`menu/shell/gemini.dic`。ほかに `cassis_bootend.dic` と `cassis_communicate.dic` の、`GetShellnameEx == "Gemini"` の分岐の中。
  - 話し手を替えるときは、`\w9\n\n[half]` で区切ってから、`\1\s[16]` のようにスコープと表情を書く。どちらから話し始めてもよい。
  - 二人の書き分けは、上の「キャラクターとサーフェス」の表のとおり。
- ランダムトークは `aryNormalTalk : array` などの配列に `'...'` で 1 行 1 トーク。長いものは行末の `/` で次の行に続ける。`RandomTalk` が EVAL で展開するので、`'...'` の中でも `%username` が使える。
- 間は手で入れる。（`WC` の設定によって `TextOnlyTranslatorFunc` が句読点にウェイトを足すこともある）
  - 読点「、」の後に `\w4` を入れる。
  - 句点や「?」の後に `\w9` を入れ、改行（`\n`）する。
  - 「…」は `\w4…\w4…` のように刻む。
- 途中の表情替えは `\s[6]` のように番号だけを書く。
- チェイントークは末尾を `\e:chain=ラベル` にする。
- 例:

  ```
  '\1\s[10]\0\s[0]どうして、\w4そんなに自分の居場所にこだわるのかしら。\w9\n居場所が無いなんて\w4幻想にすぎないのに。\e'
  ```

## 独自のルール

- サーフェス番号に 1000 を足した値を自分で書かない（上の `sfcnv` の仕組みを壊す）。
- readme の「注意」のとおり、マウス反応には性的な表現を含むものがある。既存の台詞を頼まれずに和らげたり書き換えたりしない。
- キャラクターの設定や仕様の一部は `doc/*.md` と `memo.txt` にある。下の「資料」の表で、作業に当てはまるものを読んでから始める。
- 多くの関数は、名前を文字列で組み立てて `EVAL` で呼ばれる。
  - マウス反応: `MouseMove0Head` のように、接頭辞・操作・スコープ・部位をつなげた名前
  - 羽のトーク: `aryWing{種類}Talk`
  - セーブデータの確認: `savedatacheck_{相手}`
- lint はこの呼び出しを追えないので、こうした関数を「使われていない関数」と報告する。報告の大半はこれに当たるので、報告されても消さない。
- 名前が並びから外れた関数（末尾の `Talk` が抜けているなど）は、どこからも呼ばれていない不具合かもしれない。呼び出し側が組み立てる名前と照らし合わせる。

## リリース

- 版の番号は `changelog.txt` にしかない。
- PR ごとに、先頭の最新版の項目へ 1 行ずつ短く書き足す。新しい版を始めるときは、次の形の項目を先頭に作る。

  ```
  2026/11/03 Ver.1.140
  YAYA 600系の Tc607-3 に更新
  羽のトークの不具合修正
  ```

- GitHub のリリースは、タグ名とタイトルを `Ver.1.xxx` にする。本文は自動生成にし、ファイルは添付しない。

  ```
  gh release create Ver.1.xxx --target master --title Ver.1.xxx --generate-notes --notes-start-tag <前のタグ>
  ```

- `--target` には、ブランチ名か 40 桁の SHA を指定する。短い SHA は GitHub に受け付けられない。
- タグの無い版もある（Ver.1.139 など）。`--notes-start-tag` には、直前の「タグのある版」を指定する。
- ネットワーク更新（nar と更新ファイルの作成、配布サイトへのアップロード）は、作者が別のツールで行う。エージェントからは作成を申し出ない。

## 資料

| ファイル | 中身 | 読むとき |
|---|---|---|
| `memo.txt` | カシスの人物設定（由来、食事、趣味、服、能力、生活、年齢、口調）と用語解説 | トークを書く前 |
| `doc/others.md` | 裏設定（羽、子供、ハガラズとの関係、空隙） | 設定に触れるトークを書くとき |
| `doc/condition.md` | 好感度の条件と、好感度で変わるもの | マウス反応や好感度別のトークを書くとき |
| `doc/addshell1.md` | master シェルのサーフェス一覧 | master のサーフェスを選ぶとき |
| `doc/addshell2.md` | Alternative - Cassis のサーフェス一覧 | 同シェルのサーフェスを選ぶとき |
| `doc/shell.md` | サーフェス値の加算による着せ替え、追加シェルごとの特殊対応（Gemini ほか） | シェル関連の辞書を触るとき |
| `doc/osuwari.md` | Osuwari.dll 対応の仕組みと、シェルを対応させる手順 | 追加シェルをすわりに対応させるとき |

## SSP で試すとき

- SSP がこのフォルダのゴーストを動かしている間は、yaya.dll が使用中になる。
  - yaya.dll の版が違うブランチには、`git switch` も `git rebase` もできない（途中で止まり、作業フォルダにファイルが中途半端に残る）。
  - 作者に SSP を閉じてもらうか、`git worktree` で別のフォルダに取り出して作業する。
- 試験の前に `ghost/master/yaya_variable.cfg` を控え、試験用 SSP を閉じた後に戻す（着せ替えやすわりの状態が保存されるため）。
- Osuwari.dll は、座り対応のシェル（`doc/osuwari.md` の一覧）に切り替えてから試す。
- 座ったかどうかは、SSP の応答やエラーログでは分からない。SSP の `Tmainform` のウィンドウの下端を、タスクバーの上端と比べて確かめる。
- アクティブウィンドウ座りは、作者の環境ではタスクバーに残る（2026-11 に確かめた。書き換え前の辞書でも同じ）。不具合と決めつけない。
