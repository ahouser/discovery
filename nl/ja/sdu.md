---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Smart Document Understanding

Smart Document Understanding (SDU) は、{{site.data.keyword.discoveryfull}} 内で文書に注釈を付けるための新しい方法です。 

エディターにより、カスタム変換モデルのトレーニングが簡単になります。Discovery に取り込まれる文書に索引付けする方法をカスタマイズすると、アプリケーションに返される答えが改善されます。

SDU はベータ版です。ベータ版フィーチャーの説明については、[ここ](/docs/services/discovery/release-notes.html#beta-features)を参照してください。

## サポートされる文書タイプおよびブラウザー
{: #doctypes}

サポートされる文書タイプは、PDF、Word、HTML です。JSON 文書は {{site.data.keyword.discoveryfull}} でサポートされていますが、これらの文書は構造化文書であるため、SDU エディターでは開きません。

このベータ版でサポートされるブラウザーは、Chrome と Firefox です。

## 文書に注釈を付ける方法
{: #annotate}

Smart Document Understanding エディターを開くには、以下のようにします。

1. ベータ・リンクを使用して {{site.data.keyword.discoveryfull}} を開きます。
1. プライベート・データ・コレクションを開き、**「データの管理 (Manage Data)」**画面で、**「データ設定へ移動 (Go to Data Settings)」**をクリックします。 
1. **「データ設定」**画面には、**「フィールドの抽出 (Extract fields)」**と**「フィールドのエンリッチ (Enrich fields)」**の 2 つのタブがあります。

   - **「フィールドの抽出 (Extract fields)」**に SDU エディターが含まれています。このタブは、元の {{site.data.keyword.discoveryshort}} 画面にある**「変換」**と**「正規化」**の両方のタブに代わるものです。 
   - **「フィールドのエンリッチ (Enrich fields)」**は、元の画面の**「エンリッチ (Enrich)」**タブと同じです。エンリッチメントについて詳しくは、[エンリッチメントの追加](/docs/services/discovery/building.html#adding-enrichments)を参照してください。 **「サンプル文書のアップロード (Upload sample documents)」**オプションは、**「フィールドのエンリッチ (Enrich fields)」**では不要なため表示されません。

1. Smart Document Understanding エディターでは、コレクションから 20 個の文書が自動的に**「フィールドの抽出 (Extract fields)」**タブの下にロードされます。

上部のツールバーでは、以下を行うことができます。
- 文書の選択
- 表示された文書のナビゲート
- ページの表示の調整 (`単一ページ表示`、`ズームイン`、`ズームアウト`)、`変更のクリア`、および`モデルのエクスポート/インポート`。`単一ページ表示`をクリックすると、注釈と文書が別々に表示される画面に切り替えられます。 

### SDU エディターでの文書への注釈付け
{: #documents}

**注:** 表は、別のステップで注釈が付けられます。

注釈付けを開始する前に、[文書および表にラベルを付ける場合のベスト・プラクティス](/docs/services/discovery/sdu.html#bestpractices)を参照してください。

1. デフォルトのフィールド・セットが文書の右側に表示されます。(ベータ版では、カスタム・フィールドは作成できませんが、この機能は将来使用可能になります。) 使用可能なフィールドは、`answer`、`author`、`footer`、`header`、`question`、`subtitle`、`table_of_contents`、`text`、および `title` です。
1. 右側のフィールド名をクリックしてアクティブにします。
1. SDU エディター内でそのフィールドを表すコンテンツをクリックします。そこが強調表示されます。 
   - あるいは、右側のフィールド名を選択し、それを SDU エディターのコンテンツにドラッグすることもできます。 
   - 変更をクリアするには、ツールバーの**「変更のクリア」**ボタンをクリックします。
1. **「送信」**をクリックします。
   **注:** ユーザーが注釈を付けることで、Watson は学習を行い、注釈の予測を開始します。Watson が正しく、一貫してフィールドを識別するまで、注釈付けを続行してください。
1. 注釈付けが完了したら、**「変更をコレクションに適用 (Apply changes to collection)」**をクリックします。**「文書のアップロード (Upload your documents)」**画面が開きます。(この流れは、ベータ版の後は変わります。) これで、文書をアップロードして、更新された設定をコレクション全体に適用できます。アップロードが完了すると、**「データの管理 (Manage Data)」**画面にリダイレクトされます。


フィールド | 定義  
------ | ------ 
answer | Q/A ペアにおける (FAQ の場合も多い)、質問に対する答え。
author | 作成者の名前。
footer | このタグを使用して、ページの下部に表示される、文書に関するメタ情報 (ページ番号や参照など) を示します。
header | このタグを使用して、ページの上部に表示される、文書に関するメタ情報を示します。
question | Q/A ペアにおける (FAQ の場合も多い)、質問。
subtitle | 注釈を付けられる文書の 2 次的なタイトル。このラベルは、文書ごとに 1 回のみ使用してください。
table-of-contents | このタグは、文書の目次のリストで使用します。
text | このタグは、標準のコピー・テキスト (底本) に使用します。これには、パラグラフや定義が含まれるほか、タイトル、表の一部、答え、作成者、サブタイトル、ヘッダー、およびフッターのいずれでもない単語のセットが含まれます。
title | 注釈を付けられる文書のメイン・タイトル。このラベルは、文書ごとに 1 回のみ使用してください。

### SDU エディターでの表への注釈付け
{: #tables} 

1. 右側の`「表 (table)」`フィールドを選択してから、SDU エディターで表を選択します。 
1. SDU エディター内で表の上にカーソルを移動して、**「表に注釈を付ける (Annotate table)」**ボタンを表示します。ボタンをクリックして表エディターを開きます。
1. まず、表のアウトラインを作ります。
   - `「列 (column)」`フィールドを選択します。
   - 表内の列をクリックして、列をアクティブにします。
   - `「行 (row)」`フィールドを選択します。
   - 表内の行をクリックして、行をアクティブにします。

   表のアウトラインが、左側の表プレビューに表示されます。

   **注:** **「予測 (Predict)」**をクリックすると、表の注釈のモデル予測を表示できます。
1. 次に、表内のコンテンツにラベルを付けます。
1. 表の注釈付けが完了したら、**「注釈付け完了 (Done annotating)」**をクリックします。
1. **「変更をコレクションに適用 (Apply changes to collection)」**をクリックします。**「文書のアップロード (Upload your documents)」**画面が開きます。(この流れは、ベータ版の後は変わります。) アップロードが完了すると、**「データの管理 (Manage Data)」**画面にリダイレクトされます。

フィールド | 定義  
------ | ------ 
表本体 (table body) | 情報を含んでいる、ヘッダー以外のセル
列ヘッダー (column header) | 表の各列の見出しセル (存在する場合) 
複数列ヘッダー (multi-column header) | 複数の列にまたがる見出しセル
サブセクション・タイトル (subsection title) | 行見出しの列用の列ヘッダー (存在する場合)
行ヘッダー (row header) | 表の各行の行ラベル (存在する場合)
複数行ヘッダー (multi-row header) | 複数の行にまたがる行ラベル

## 文書および表にラベルを付ける場合のベスト・プラクティス
{: #bestpractices}

- すべてのガイドラインに従い、すべての文書に一貫性のあるラベリングを行う。
- 空白にはラベルを付けない。
- ダイアグラムおよびイメージにはラベルを付けない。
- **太字**、_イタリック_、または下線付きのテキストの扱いを変えない。テキストのスタイルではなくコンテキストに基づいてラベルを付けてください。 
- 文書にラベルを付けるときは、最初のページから最後のページまで処理する。何もラベルが付いていなくとも、すべてのページをサブミットする必要があります。 
- 項目に誤ってラベルを付けた場合は、その項目に別のラベルを選択して、最初のラベルを上書きする。
- ページはいつでもサブミットできる。サブミットする前に、適切なラベル付けがすべて完了していることを確認してください。
- 文書にラベルを付けるときは、ブラウザーのズーム機能を使用しない。
- 他のテキストをオーバーレイしているテキストがあるような文書や表は、「二重オーバーレイ」と見なされ、注釈を付けることはできない。これらの文書は管理者に報告してください。
- 単一ページに複数列のテキストを含んでいる文書や表に注釈を付けることはできない。これらの文書は管理者に報告してください。
- 脚注は、それらがページの下部に表示され、文書内のテキストの本文で参照されている場合にのみマークを付ける。
- セクションまたはリスト内に表示される注記 (例えば、明示的な「注記」などのコールアウト) には、`text` としてラベルを付ける。
- 表のラベル付けが正しく行われたかどうかが不明で、プレビュー・ペインが応答しなくなった場合、確実に正しく処理されているようにするには、ブラウザーでページを再ロードし、表の再ラベル付けを行う必要がある。

