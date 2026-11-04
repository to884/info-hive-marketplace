# info-hive-marketplace

info-hive の Claude Code プラグインを配るマーケットプレイスである。マーケットプレイス名は `info-hive` で、プラグインは `<プラグイン名>@info-hive` の形で入れる。プラグインの本体は、それぞれ別のリポジトリにある。このリポジトリには、マーケットプレイスの定義（`.claude-plugin/marketplace.json`）だけを置く。

## 入れ方

Claude Code で、マーケットプレイスを追加してからプラグインを入れる。

```
/plugin marketplace add to884/info-hive-marketplace
/plugin install wiki@info-hive
```

このリポジトリとプラグインのリポジトリは、どちらも非公開なので、入れるには GitHub の認証情報が要る。HTTPS なら `gh auth login` のあとに `gh auth setup-git` を実行しておく。SSH なら、パスフレーズを聞かれない鍵を用意しておく。

新しいバージョンを取り込むときは、`/plugin marketplace update` のあとに `/plugin install wiki@info-hive` を実行する。

## 載っているプラグイン

| プラグイン | 入れるときの名前 | リポジトリ | 内容 |
| --- | --- | --- | --- |
| wiki | `wiki@info-hive` | [to884/info-hive-wiki](https://github.com/to884/info-hive-wiki) | 日本語に特化した LLM Wiki。日本語の Markdown の wiki を、ローカルのハイブリッド検索、出典つきの根拠、グラフで構築・保守する。`/wiki:*` のコマンドを 9 本含む。 |
| rag | `rag@info-hive` | [to884/info-hive-rag](https://github.com/to884/info-hive-rag) | `wiki@info-hive` に依存する RAG（検索拡張生成）のプラグイン。現在は初期構成のみ。 |

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
