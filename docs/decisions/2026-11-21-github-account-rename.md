---
project: gakuso-simulator
date: 2026-11-21
tags: [decision]
---

# GitHubアカウント名の変更に伴う公開URLの切り替え

## 背景

リポジトリを所有する GitHub アカウントの名前を `shuzo-yamamoto` から `gwasendo` に変更した。
これに伴い、リポジトリと GitHub Pages の URL が変わった。

| 項目 | 変更前 | 変更後 |
|---|---|---|
| リポジトリ | `github.com/shuzo-yamamoto/gakuso-simulator` | `github.com/gwasendo/gakuso-simulator` |
| 公開URL（GitHub Pages） | `shuzo-yamamoto.github.io/gakuso-simulator/` | `gwasendo.github.io/gakuso-simulator/` |

所有者は**個人アカウントのまま**で、組織アカウントへの移管ではない。
GitHub の公開APIで、所有者の種類が `User`、アカウントID が変更前と同じ `300787887` であることを確認した（2026-11-21）。

## 決定内容

- README と要件定義書§5.2 の公開URLを新URLに切り替えた（コミット `dcc4421`）。
  2026-11-21 時点で、作業フォルダ内に旧アカウント名の記載は残っていない
- リポジトリ設定の `user.email` を `300787887+gwasendo@users.noreply.github.com` に変更した（今後のコミットに適用）
- 過去のコミットの著者メール（`300787887+shuzo-yamamoto@users.noreply.github.com`）は**書き換えない**
- タグ `v24.0` の注釈メッセージに書かれた旧URLは**書き換えない**

## 却下した案とその理由

| 案 | 却下の理由 |
|---|---|
| 過去のコミットの著者メールを新アカウント名に書き換える | GitHub は noreply アドレス先頭の数字ID でアカウントを識別するため、旧名のままでも同じアカウントに紐づく。書き換えには履歴の書き換えと強制pushが必要で、得るものに比べて危険が大きい |
| タグ `v24.0` を付け直して旧URLを消す | 強制pushが必要になり、「v24.0 時点の記録」を後から変えることにもなる。旧URLが無効であることをこの記録に残せば足りる |

## 影響範囲

- **旧URLの GitHub Pages は 404 になり、新URLへは転送されない**（GitHub の仕様）。
  旧URLをブックマークしている端末は、新URLに差し替える必要がある
- 旧URLのリポジトリ（`github.com/shuzo-yamamoto/gakuso-simulator`）は、新URLへ自動で転送される（301）
- `git remote` の接続先は新URLに設定済みで、push・fetch は新URLで行っている
- タグ `v24.0` の注釈メッセージに書かれた公開URLは無効。正しい公開URLは README を参照する
