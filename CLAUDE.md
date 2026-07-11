# shiftflow プロジェクト

居酒屋向け月次シフト管理ツール（クライアントサイドのみの単一HTML）。詳細は README.md 参照。

## 構成

- `index.html` — アプリ本体（HTML/CSS/JS すべて1ファイル。依存ライブラリなし）

## 開発メモ

- 元は `~/Downloads/index.html`（ShiftFlow v2.0 汎用版）。v3.0 で居酒屋対応＋セキュリティ強化
- 時間計算は営業日基準。「終了 ≦ 開始」なら翌日またぎ（+24h）。`rangeMins()` / `nightMinutesOf()` を参照
- PINは平文保存禁止。`hashPin()`（SHA-256＋ソルト）経由で `pinHash` / `settings.adminPinHash` に保存
- 認証状態（auth）は localStorage・バックアップに保存しない（起動時は必ずロック画面）
- 動作確認：`awk '/<script>/{f=1;next}/<\/script>/{f=0}f' index.html > /tmp/sf.js` で抽出し、
  `osascript -l JavaScript` で構文チェック＋純ロジックのテストが可能（node不要）
