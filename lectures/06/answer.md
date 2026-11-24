# 第6回 解答

## 演習

<!-- [tool call] の行は、表示された行をそのまま貼り付けてください。終わらなかった STEP は、空欄のままでかまいません。 -->

- STEP 1 のツールの名前： glossary_search_glossary
- STEP 2 の [tool call]：

[server] glossary: コマンドで起動（uv run python -m app.mcp_server）
[model] gemini-3.5-flash-lite
[tools] MCP サーバー（app/mcp_servers.json）
AIE2026の講座における「3レベル」とは、宿題の構成を示す3つの段階のことです。

具体的には以下の3つのレベルに分かれています。

1. **基礎**: 講義内容の確認（理解度をチェックする問題など）
2. **実装**: 実際に自分でコードを書く演習
3. **発展**: さらに深く調査したり、新しい手法を試したりする課題

これら3つのうち**どれか1つ**に取り組めば、その回の宿題は完了となります。原則として採点は行われませんので、ご自身の理解度や目的に合わせて選んで取り組んでみてください。

（関連：第1回）

--- trace ---
[tool call]   glossary_search_glossary({'query': '3レベル'})
[tool return] glossary_search_glossary -> [{"term": "宿題の3レベル", "lecture": 1, "definition": "AIE2026の宿題の構成。「基礎（講義内容の確認）」「実装（自分でコードを書く）」「発展（調査や試行）」の3段階があり、どれか1つに取り組…
[usage] 入力 715 tokens / 出力 169 tokens / モデル応答 2 回

- STEP 3 の [tool call]：

[server] glossary: コマンドで起動（uv run python -m app.mcp_server）
[server] fetch: コマンドで起動（uvx mcp-server-fetch==2026.11.11 --no-readability-js）
[model] gemini-3.5-flash-lite
[tools] MCP サーバー（app/mcp_servers.json）
HTTP Request: GET https://modelcontextprotocol.io/robots.txt "HTTP/1.1 200 OK"
HTTP Request: GET https://modelcontextprotocol.io/ "HTTP/1.1 307 Temporary Redirect"
HTTP Request: GET https://modelcontextprotocol.io/robots.txt "HTTP/1.1 200 OK"
HTTP Request: GET https://modelcontextprotocol.io/docs/2026-07-28/getting-started/intro.md "HTTP/1.1 200 OK"
Model Context Protocol（MCP）は、AIアプリケーションを外部のデータソース、ツール、ワークフローに接続するためのオープンソースの標準規格です。
AIにとっての「USB-Cポート」のような役割を果たし、多様なシステムとの接続を標準化することで開発の手間を減らします。
開発者、AIアプリケーション、エンドユーザーのそれぞれにメリットをもたらし、幅広いクライアントやサーバーエコシステムでサポートされています。

--- trace ---
[tool call]   fetch_fetch({'url': 'https://modelcontextprotocol.io/'})
[tool return] fetch_fetch -> Contents of https://modelcontextprotocol.io/:
> ## Documentation Index
> Fetch the complete documentation index at: http…
[usage] 入力 2,179 tokens / 出力 113 tokens / モデル応答 2 回

- STEP 4 の [tool call]：

[server] glossary: コマンドで起動（uv run python -m app.mcp_server）
[server] fetch: コマンドで起動（uvx mcp-server-fetch==2026.11.11 --no-readability-js）
[server] aws: URL に接続（https://knowledge-mcp.global.api.aws）
[model] gemini-3.5-flash-lite
[tools] MCP サーバー（app/mcp_servers.json）
Amazon S3 のバージョニングとは、同一バケット内で同じオブジェクトの複数のバリアント（世代）を保持し、すべてのバージョンの保存・取得・復元を可能にする機能です。
これにより、誤った上書きや削除（削除マーカーの付与）からデータを保護し、簡単に元の状態へリカバリできるようになります。

--- trace ---
[tool call]   aws_aws___search_documentation({'search_phrase': 'Amazon S3 バージョニング 概要'})
[tool return] aws_aws___search_documentation -> {'content': {'result': [{'rank_order': 1, 'title': 'querying-aws-s3', 'skill_description': 'Queries S3 object metadata, …
[tool call]   aws_aws___search_documentation({'search_phrase': 'What is S3 Versioning Amazon Simple Storage Service'})
[tool return] aws_aws___search_documentation -> {'content': {'result': [{'rank_order': 1, 'title': 'Securing Access to AWS Using MFA – Part 3 | AWS Security Blog', 'con…
[usage] 入力 11,349 tokens / 出力 135 tokens / モデル応答 3 回

- 気づき・疑問：
mcp_servers.jsonに追加するだけで使えるので，コードの実装よりどのMCPサーバーあるのかを探す方が将来的には難しそうだと感じた．

## 宿題

<!-- 基礎・実装・発展のどれか1つに取り組めば完了です。 -->

- 取り組んだレベル：基礎 
- やったこと：mcp_server.pyに「server.tool()(tools.get_lecture_summary)」を追加した．
- 結果：
第2回では「**ファインチューニングとLoRA**」を学びます。

### 主な内容
- **事前学習とファインチューニングの違い**: ファインチューニングが向く場面・向かない場面を理解します。
- **SFT（教師ありファインチューニング）**: 入力と出力のペアを用いた学習の仕組みを学びます。
- **PEFTとLoRA**: 全パラメータを更新せず、低ランク行列のみを効率的に学習する手法（LoRA）の考え方を扱います。
- **過学習への注意**: 学習データへの過剰適応を防ぐための検証の重要性を学びます。

### 演習
Google Colab上で小さなモデル（Qwen2.5-0.5Bなど）を使い、架空のFAQデータでLoRAファインチューニングを行って、学習前後での出力の変化やタスク適応を体験します。

（関連する回: 第2回）

--- trace ---
[tool call]   glossary_get_lecture_summary({'lecture': 2})
[tool return] glossary_get_lecture_summary -> # 第2回 ファインチューニングとLoRA

## この回のねらい

- 事前学習とファインチューニングの違い、ファインチューニングが向く場面と向かない場面を理解する
- LoRAの考え方を理解し、Google Colab上で小さなモデルを…
[usage] 入力 5,942 tokens / 出力 226 tokens / モデル応答 2 回


- 気づき・疑問：ローカル環境で動かす分にはMCPのメリットをあまり感じないと思うが，複数人での環境や実務を考えると便利だろうと思う．

