# ITfare2019（フルーツキャッチゲーム）

Kinect v2 で体の動きを読み取ってプレイヤーを操作し、落ちてくるフルーツをかごに入れて点数を競うゲームです。Unity 2019.4 と C# で個人制作しました。2022年7月に、キーボード操作の追加やゲームバランスの調整などの改良を加えています。

このリポジトリは自分で書いたスクリプトだけを公開しています。効果音・BGM・画像・Kinect SDK などの素材は含めていないので、このままでは Unity で開いて遊べません。

## 遊び方

- Kinect の前に立つと、肩の位置でプレイヤーが左右に動き、ひじの角度でプレイヤーが傾きます。左右に動くかごや、揺れる丸太がある中でフルーツをかごに入れます。
- 制限時間は60秒です。フルーツごとに点数（りんご5点、オレンジ10点、ぶどう15点、バナナ50点）があります。
- 時間が経つほどフルーツの落ちる間隔が短くなります（落下レートを 20^(経過時間/制限時間) で上げています）。
- キーボードでも操作できます（左右キーで移動、上下キーで回転、Space で開始、H で説明、R でリトライ、Esc で終了）。

## 主なスクリプト

| ファイル | 役割 |
|---|---|
| `PlayerController.cs` / `PlayerController2.cs` | Kinect の骨格データから肩・ひじの位置を取り、プレイヤーの位置と角度に変換する（2人プレイ対応は 2） |
| `KeyPlayerController.cs` | キーボード・ゲームパッドでの操作（2022年に追加） |
| `KeyManager.cs` | 開始・説明表示・リトライ・終了のキー入力 |
| `FallManager.cs` | 出現率で重み付けしてフルーツを選び、ランダムな位置に落とす |
| `Timer.cs` | 制限時間のカウントダウンと、時間に応じた落下レートの上昇 |
| `catcher.cs` | かごに入ったフルーツの点数加算と演出 |
| `ScoreManager.cs` / `SaveDataManager.cs` | スコアとランキングの保存（PlayerPrefs / JSON） |
| `GameState.cs` | 開始前・プレイ中・終了の状態管理 |
| `SoundManager.cs` / `SpectrumManager.cs` | 効果音の再生と音声スペクトルの取得 |
| `kago.cs` / `sinMove.cs` / `spin.cs` | かごや丸太の往復運動・回転 |

## 公開していないもの

- Kinect for Windows SDK 2.0 の Unity パッケージ（DLL、ラッパー、サンプル）: Microsoft
- 効果音・BGM: フリー素材サイトの素材
- 画像: 自作ですが、ネット上の画像をトレースして作ったため外しています
- Unity の UI Builder サンプル

## ライセンス

自分で書いたコードは MIT ライセンスです（`LICENSE`）。`PlayerController.cs` と `PlayerController2.cs` の一部は Kinect SDK の KinectView サンプル（`BodySourceView.cs`）を元にしているので、その部分は Microsoft のライセンスに従います。
