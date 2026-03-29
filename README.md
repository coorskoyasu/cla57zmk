シールド定義 (boards/shields/cla57/)
ファイル	内容
cla57.dtsi	キーマトリクス(14列x6行)、GPIO行ピン、バッテリー設定
cla57_left.overlay	左半分の列ピン + WS2812 RGB LED (P0.06/D1ピン)
cla57_right.overlay	右半分の列ピン(反転) + WS2812 RGB LED
Kconfig.defconfig	分割キーボード設定、左=セントラル
Kconfig.shield	シールド検出定義
cla57.conf	ディープスリープ有効
キーマップ・設定 (config/)
ファイル	内容
cla57.keymap	3レイヤー + 78マクロ + 56コンボ
cla57.conf	BLE設定 + RGB underglow有効(起動時白色ブリーズ)
west.yml	ZMK firmware参照
ビルド
ファイル	内容
build.yaml	nice_nano_v2 + cla57 左/右
.github/workflows/build.yml	GitHub Actionsビルド
キーマップ構成
Layer 0 (DEFAULT) - LED: 青
keylayout.txtに記述されたQWERTY配列。&lt FUNC ESCでFUNCレイヤーへの一時切替。

Layer 1 (NICOLA) - LED: 赤
標準NICOLA親指シフト配列:

単独打鍵: 。かたこさ / らちくつ、 / うしてけせ / はときいん / .ひすふへ / めそねほ・
左親指(無変換) + 文字キー: 30個のコンボ (ぁえりゃれ、をあなゅも、等)
右親指(変換) + 文字キー: 26個のコンボ (がだござ、じでげぜ、等)
コンボタイムアウト: 30ms
Layer 2 (FUNC) - LED: 緑
F1-F12、BT接続管理(SEL/CLR/NXT/PRV)、メディアコントロール、矢印キー、bootloader

LED動作
起動時: 白色ブリーズ効果(CONFIG_ZMK_RGB_UNDERGLOW_EFF_START=1)
レイヤー切替時: to_default/to_nicolaマクロ内で&rgb_ug RGB_COLOR_HSB()を呼び出し、ソリッドカラーに変更
注意: &mo FUNCによる一時レイヤーではLED色は変わりません(ZMKの制約)。恒久的に切り替える場合はLayer 2内のto_default/to_nicolaをご利用ください。
ハードウェア備考
WS2812 LEDのデータピン: P0.06 (nice_nano_v2のD1ピン) - 実際のハードウェアに合わせてoverlayファイルのピン設定を変更してください
chain-length = <1> - LED数に合わせて変更してください
