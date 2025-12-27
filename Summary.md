# torabo-tsuki LP 用 ZMK 設定リポジトリ概要

## これは何？
- **[torabo-tsuki LP](https://github.com/sekigon-gonnoc/torabo-tsuki-lp)** 用の **ZMK ファームウェア設定**（外部モジュールとして ZMK に取り込む想定）です。
- 分割キーボード（左右）向けの **シールド定義**（`torabo_tsuki_lp_left` / `torabo_tsuki_lp_right`）と、キーマップ等の設定を含みます。

## ビルド対象（重要）
- **board**: `bmp_boost`
- **shield**: `torabo_tsuki_lp_left` / `torabo_tsuki_lp_right`
- `build.yaml` に、成果物名（artifact）として central/peripheral の割り当てが定義されています。
  - `torabo_tsuki_lp_right_central`
  - `torabo_tsuki_lp_left_peripheral`
- **書き込み注意**: `README.md` にある通り、**`_central` が付いた UF2 をトラックボールが付いている側**に、**`_peripheral` を反対側**に書き込んでください。

## どこを編集すればいい？
- **キーマップ**: `config/keymap.keymap`
  - `boards/shields/torabo_tsuki_lp/torabo_tsuki_lp.keymap` は `config/keymap.keymap` を include しています（実体は `config/` 側）。
- **レイアウト情報（keymap-editor向け）**: `config/info.json`
- **依存（west manifest）**: `config/west.yml`
  - ZMK 本体（`zmkfirmware/zmk`）に加えて、`bmp_boost` やトラックボール関連の外部モジュールを取り込みます。

## キーマップの編集方法
- `README.md` の通り、**keymap-editor** および **ZMK Studio** で編集できます。
  - シールド定義に `studio` 機能が含まれています（`boards/shields/torabo_tsuki_lp/torabo_tsuki_lp.zmk.yml`）。

## 付属スニペット
- `snippets/split-trackball`: `EXTRA_DTC_OVERLAY_FILE` に `split-trackball.overlay` を追加
- `snippets/split-trackball-listner`: `EXTRA_DTC_OVERLAY_FILE` に `split-trackball-listner.overlay` を追加

## トラブル時
- **設定初期化**: `build.yaml` に `shield: settings_reset` のビルドが含まれています（ペアリング情報などのリセット用途）。
