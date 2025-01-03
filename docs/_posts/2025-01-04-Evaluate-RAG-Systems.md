---
layout: post
title: RAGシステムの評価方法
---
## はじめに


### 評価の進め方
例えば、「既存のRAGシステムの一部を改修し、精度向上の度合いを評価したい」場合、以下の手順で進めます。

1. **精度評価の目的と背景を明確にする**  
  精度評価の目的が何なのかと、なぜ精度評価をするのかを明確にする。  

2. **評価指標を決める**  
   効果を測定するための指標を設定します。

3. **評価用データセットを収集する**  
   評価に適したデータを集めます。

4. **評価する**  
   設定した指標に基づき、システムの性能を測定します。

5. **評価結果を確認、考察する**  
   得られた結果を分析し、改善点や効果を考察します。

6. **次のアクションを検討する**  
   評価結果に基づき、さらなる改善や次のステップを計画します。

## 精度評価の目的と背景を明確にする
RAG（Retrieval-Augmented Generation）システムの精度を評価する前に、評価計画を立てることが重要です。まず、評価の目的を明確にしましょう。
RAGシステムの精度評価において、各観点で**Component-wise**（個別要素ごとの評価）と**End-to-End**（システム全体としての評価）のどちらを用いるべきか、または両方必要かを以下に整理します。

### **1. システム性能の定量的評価**  
**推奨評価手法:** **両方（Component-wise + End-to-End）**  

- **Component-wise:**  
   - **検索精度:** 検索モジュールが適切なドキュメントを取得できているか。  
   - **生成精度:** 検索結果を適切に参照し、正確かつ自然な回答を生成しているか。  
- **End-to-End:**  
   - 全体としてユーザーの質問に対して適切な回答が返されているか。  
   - 検索と生成の相互作用がスムーズに行われているか。  

**理由:**  
システム性能を高めるには、各コンポーネントの性能と全体の連携がどちらも重要です。

### **2. 実用性の確認**  
**推奨評価手法:** **End-to-End**  

- **End-to-End:**  
   - 特定のユースケースでユーザーが満足する回答が得られているか。  
   - 現場業務や特定タスクでシステムが実用的かどうか。  

**理由:**  
ユーザーは最終的な出力を基準にシステムを評価するため、End-to-End評価が適しています。

### **3. 改善点の特定**  
**推奨評価手法:** **Component-wise**  

- **Component-wise:**  
   - 検索フェーズと生成フェーズのそれぞれでエラーの要因を特定。  
   - ボトルネックが検索、生成、またはその連携部分にあるかを特定。  

**理由:**  
改善点の特定には、どのコンポーネントに問題が存在するかを明確にする必要があるため、Component-wiseな評価が有効です。

### **4. 比較・ベンチマーク**  
**推奨評価手法:** **End-to-End**  

- **End-to-End:**  
   - 競合システムや従来システムと比較して、総合的な性能が優れているか。  
   - 実際のタスクにおける出力品質を基準に評価。  

**理由:**  
ベンチマークでは、最終的なアウトプットが比較対象と比べてどうかが重要です。

### **5. リスクの評価**  
**推奨評価手法:** **両方（Component-wise + End-to-End）**  

- **Component-wise:**  
   - 検索段階で不適切な情報が取り込まれていないか。  
   - 生成段階で誤った内容やバイアスが生じていないか。  
- **End-to-End:**  
   - 最終的な出力にリスク（ハルシネーション、バイアス、プライバシー漏洩）が含まれていないか。  

**理由:**  
リスクは各フェーズに潜む可能性があり、全体としても現れるため、両方の視点が必要です。

### **まとめ表**

| **観点**           | **Component-wise** | **End-to-End** | **理由** |
|---------------------|---------------------|---------------|---------|
| **1. システム性能**   | ✔️                 | ✔️             | 両方重要 |
| **2. 実用性**       |                   | ✔️             | 出力重視 |
| **3. 改善点**       | ✔️                 |               | 要因特定 |
| **4. 比較・ベンチマーク** |                   | ✔️             | 出力比較 |
| **5. リスク評価**    | ✔️                 | ✔️             | 両方重要 |

#### **結論:**  
- **Component-wise:** **改善点の特定**、**システム性能**、**リスク評価**で特に重要。  
- **End-to-End:** **実用性**、**比較・ベンチマーク**、**システム性能**、**リスク評価**で重要。  
- **両方:** **システム性能**、**リスク評価**では両方の評価が必要。  

各観点で適切な評価手法を組み合わせることで、RAGシステムの精度評価はより効果的かつ実用的になります。


## 変数を決める

精度評価において、どの要素を変数として設定するかを検討します。基本的に、変数は一つに絞ることが推奨されます。複数の変数を同時に設定すると、どの要素が評価結果に最も影響を与えたかを特定しにくくなります。

- **パーシング（Parsing）**  
  - パーサーの種類
  - ファイル形式
  - コンテンツの種類

- **チャンク化（Chunking）**  
  - チャンクのサイズ
  - チャンクの重なり
  - チャンクの種類

- **埋め込み（Embedding）**  
  - BM25
  - TF-IDF
  - 高密度埋め込み（Dense Embedding）
  - 疎な埋め込み（Sparse Embedding）

- **インデックス作成（Indexing）**  
  - メタデータ
  - その他

- **情報検索（Retrieval）**  
  - 検索結果の数
  - 再ランキング
  - クエリ変換
  - クエリルーティング
  - 融合検索

- **生成（Generation）**  
  - プロンプト
  - 大規模言語モデル（LLM）

## 変数に対する評価指標を決める
評価のスコープには、コンポーネント別評価（Component-wise Evaluation）とエンドツーエンド評価（End-to-End Evaluation）の2種類があります。

1. **コンポーネント別評価**  
   システムの各部分を個別に評価します。

   - **情報検索（Retrieval）**  
     - コンテキスト再現率（Context Recall）
     - コンテキスト精度（Context Precision）
     - コンテキスト関連性（Context Relevancy）
     - コンテキストエンティティ再現率（Context Entity Recall）
     - ヒット率@k（Hit rate @ k）
     - 平均逆順位（MRR）
     - 正規化割引累積利得（nDCG）
     - 平均適合率（MAP）

   - **生成（Generation）**  
     - 忠実性（Faithfulness）
     - 回答の関連性（Answer Relevancy）

2. **エンドツーエンド評価**  
   システム全体の性能を評価します。

   - 意味的類似度（Semantic Similarity）
   - 回答の正確性（Answer Correctness）

エンドユーザーが直接触れるのは最終的な回答文であるため、エンドツーエンドの評価指標を取得することは重要です。一方、システムのどの部分がボトルネックになっているかを特定するには、コンポーネント別の評価が有用です。

例えば、システムの一部を改修して精度向上を図る場合、改修部分に関連する指標を取得すると効果的です。改修部分で精度向上が見られても、最終的な回答文で改善が確認できない場合、他の要素（例えば、LLM）の変更が必要であると判断できます。

ただし、すべての指標を一度に評価するのは現実的ではありません。評価には時間がかかり、ビジネス上の締め切りも考慮する必要があります。現実的には、マイルストーンを設定し、段階的に改善活動を進めることが望ましいです。

## 評価用データセットを収集する
評価用データセットの基準は以下の通りです。

- **データセットの規模**  
  評価用のドキュメントや質問の数が十分に多いこと。

- **データセットの多様性**  
  データの種類が偏っておらず、多様なケースを含んでいること。

- **データセットの実用性**  
  実際の使用状況や目的に沿った内容であること。

## 評価する 
評価方法には大きく分けて Human Evaluation と LLM as a Judge の２種類が存在します。

## 評価結果を確認、考察する


## 次のアクションを検討する


## 参考文献

- [Evaluate RAGs Rigorously or Perish](https://towardsdatascience.com/evaluate-rags-rigorously-or-perish-54f790557357)
- [Overview of Metrics - Ragas](https://docs.ragas.io/en/stable/concepts/metrics/overview/)
- [レコメンド指標の整理: Recall@k・MRR・MAP・nDCG](https://zenn.dev/hellorusk/articles/7e336fd3c6be20a8f8d1)
- [日本語言語データセットまとめ](https://zenn.dev/simossyi/articles/9e98575f7b6419)
 