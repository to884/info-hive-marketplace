# info-hive-marketplace

info-hive の Claude Code プラグインを配るマーケットプレイスである。マーケットプレイス名は `info-hive` で、プラグインは `<プラグイン名>@info-hive` の形で入れる。プラグインの本体は、それぞれ別のリポジトリにある。このリポジトリには、マーケットプレイスの定義（`.claude-plugin/marketplace.json`）だけを置く。

## 入れ方

Claude Code で、マーケットプレイスを追加してからプラグインを入れる。

```
/plugin marketplace add to884/info-hive-marketplace
/plugin install wiki@info-hive
```

新しいバージョンを取り込むときは、`/plugin marketplace update` のあとに `/plugin install wiki@info-hive` を実行する。

## 載っているプラグイン

| プラグイン | 入れるときの名前 | リポジトリ | 内容 |
| --- | --- | --- | --- |
| wiki | `wiki@info-hive` | [to884/info-hive-wiki](https://github.com/to884/info-hive-wiki) | 日本語に特化した LLM Wiki。日本語の Markdown の wiki を構築・保守する。日本語に対応したローカルのハイブリッド検索（BM25 と多言語の埋め込み）、出典つきの回答、任意の型付きグラフ、Shift_JIS などのソースの文字コードの変換を備える。タスクの経験を記録し、スキルの改善案を評価して適用・ロールバックできる。`/wiki:*` のコマンドを 10 本含み、一覧は `/wiki:help` で見られる。 |
| rag | `rag@info-hive` | [to884/info-hive-rag](https://github.com/to884/info-hive-rag) | `wiki@info-hive` に依存する RAG（検索拡張生成）のプラグイン。PDF の抽出、必要なページの OCR、埋め込み、索引化を永続ジョブとして進め、Claude Code を終えても次の接続時に再開する。日本語に対応したローカルのハイブリッド検索（BM25 と埋め込み）を MCP で提供する。`/rag:*` のコマンドを 3 本（setup、status、search）含む。 |

## 旧リポジトリ to884/info-hive から移るとき

以前は、プラグインのリポジトリ `to884/info-hive` がマーケットプレイスを兼ねていた。そのリポジトリをマーケットプレイスとして追加していた場合は、いったん外してから、このリポジトリを追加し直す。マーケットプレイス名は同じ `info-hive` なので、外さないと追加できない。

```
/plugin marketplace remove info-hive
/plugin marketplace add to884/info-hive-marketplace
/plugin install wiki@info-hive
```

## プラグインを足すとき

1. プラグインのリポジトリを作り、`.claude-plugin/plugin.json` に `name` と `version` を書く。
2. このリポジトリの `.claude-plugin/marketplace.json` の `plugins` に項目を足す。
   - `name` は、プラグインの `plugin.json` の `name` とそろえる。そろっていないと、入れるときにプラグインが見つからない。
   - `source` は `{"source": "github", "repo": "to884/<リポジトリ名>"}` とする。`ref` は書かず、既定のブランチを配る。
   - `version` は書かない。バージョンは、プラグインの `plugin.json` だけに書く。
3. `claude plugin validate .` で確かめる。
4. この README の「載っているプラグイン」の表に 1 行足す。

プラグインのバージョンを上げても、このリポジトリは直さなくてよい。Claude Code は、プラグインの `plugin.json` の `version` が変わったときに、更新があると判断する。

開発の決まりと手順は、開発用のリポジトリ [to884/info-hive-dev](https://github.com/to884/info-hive-dev) にある。

## ライセンス

[MIT](LICENSE)
