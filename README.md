# About

「JSON-LD 穴埋め方式」による JSON-LD テンプレートを用いて、時間範囲の補完をテストするためのデータセットです。
論文は [こちら](http://example.org/) で公開されています。

このテストは [CheckList](https://github.com/marcotcr/checklist) にインスパイアされ、
筆者らが独自にスクラッチから作成したものです。

# Data

## reference

正解となる JSON ファイルを収録したフォルダです。

以下は [reference/type-year-to-gyear-seireki-2000.json](https://github.com/indigo-lab/metadata-completion-checklist/blob/main/reference/type-year-to-gyear-seireki-2000.json) の抜粋です。

```
{
  "@context": {
    "dct": "http://purl.org/dc/terms/",
    "dcat": "http://www.w3.org/ns/dcat#",
    "xsd": "http://www.w3.org/2001/XMLSchema#"
  },
  "@type": "dcat:Dataset",
  "dct:title": "2000年報告書",
  "dct:date": {
    "@value": "2000",
    "@type": "xsd:gYear"
  }
}
```

## template

補完対象を `?` で置き換えたテンプレート JSON ファイルを収録したフォルダです。

以下は [template/type-year-to-gyear-seireki-2000.json](https://github.com/indigo-lab/metadata-completion-checklist/blob/main/template/type-year-to-gyear-seireki-2000.json) の抜粋です。

```
{
  "@context": {
    "dct": "http://purl.org/dc/terms/",
    "dcat": "http://www.w3.org/ns/dcat#",
    "xsd": "http://www.w3.org/2001/XMLSchema#"
  },
  "@type": "dcat:Dataset",
  "dct:title": "2000年報告書",
  "dct:date": {
    "@value": "?",
    "@type": "xsd:gYear"
  }
}
```

## request

template をもとに生成した [OpenAI ChatCompletion API (gpt-3.5-turbo-0613)](https://platform.openai.com/docs/api-reference/chat) に対するリクエストボディを収録したフォルダです。

以下は [request/type-year-to-gyear-seireki-2000.json](https://github.com/indigo-lab/metadata-completion-checklist/blob/main/request/type-year-to-gyear-seireki-2000.json) の抜粋です。

```
{
  "model": "gpt-3.5-turbo-0613",
  "messages": [
    {
      "role": "system",
      "content": "あなたは与えられた JSON-LD の中の \"?\" の部分に文字列を補完して JSON-LD を返すエージェントです"
    },
    {
      "role": "user",
      "content": "{\"@context\":{\"dct\":\"http://purl.org/dc/terms/\",\"dcat\":\"http://www.w3.org/ns/dcat#\",\"xsd\":\"http://www.w3.org/2001/XMLSchema#\"},\"@type\":\"dcat:Dataset\",\"dct:title\":\"2000年報告書\",\"dct:date\":{\"@value\":\"?\",\"@type\":\"xsd:gYear\"}}"
    }
  ],
  "temperature": 0
}
```

# Target

各フォルダに収録されたファイルのテスト目的は以下の通りです (合計 1,481 件)

| prefix                                | count | note                                       |
| ------------------------------------- | ----- | ------------------------------------------ |
| type-year-to-gyear-seireki-           | 40    | 西暦年からの xsd:gYear 補完                |
| type-yearmonth-to-gyear-seireki-      | 200   | 西暦年月からの xsd:gYear 補完              |
| type-yearmonth-to-gyearmonth-seireki- | 200   | 西暦年月からの xsd:gYearMonth 補完         |
| type-date-to-gyear-seireki-           | 200   | 西暦年月日からの xsd:gYear 補完            |
| type-date-to-gyearmonth-seireki-      | 200   | 西暦年月日からの xsd:gYearMonth 補完       |
| type-date-to-date-seireki-            | 200   | 西暦年月日からの xsd:date 補完             |
| dcat-year-seireki-ascii-              | 40    | 西暦表記(半角数字)からの日付範囲補完       |
| dcat-year-seireki-zenkaku-            | 40    | 西暦表記(全角数字)からの日付範囲補完       |
| dcat-year-seireki-kanji-              | 40    | 西暦表記(漢数字)からの日付範囲補完         |
| dcat-year-wareki-showa-ascii-         | 64    | 和暦表記(半角数字・昭和)からの日付範囲補完 |
| dcat-year-wareki-showa-zenkaku-       | 64    | 和暦表記(全角数字・昭和)からの日付範囲補完 |
| dcat-year-wareki-showa-kanji-         | 64    | 和暦表記(漢数字・昭和)からの日付範囲補完   |
| dcat-year-wareki-heisei-ascii-        | 31    | 和暦表記(半角数字・平成)からの日付範囲補完 |
| dcat-year-wareki-heisei-zenkaku-      | 31    | 和暦表記(全角数字・平成)からの日付範囲補完 |
| dcat-year-wareki-heisei-kanji-        | 31    | 和暦表記(漢数字・平成)からの日付範囲補完   |
| dcat-year-wareki-reiwa-ascii-         | 12    | 和暦表記(半角数字・令和)からの日付範囲補完 |
| dcat-year-wareki-reiwa-zenkaku-       | 12    | 和暦表記(全角数字・令和)からの日付範囲補完 |
| dcat-year-wareki-reiwa-kanji-         | 12    | 和暦表記(漢数字・令和)からの日付範囲補完   |

# License

本レポジトリのデータは [CC0 1.0 Universal](https://github.com/indigo-lab/metadata-completion-checklist/blob/main/LICENSE) でライセンスされています。
