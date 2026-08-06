---
categories:
- Java PDF Processing
date: '2026-07-20'
description: Java と GroupDocs.Signature を使用して PDF ドキュメントにバーコード署名を作成する方法を学びます。コード例とベストプラクティスを含むステップバイステップのチュートリアルです。
keywords:
- create barcode signature
- how to add barcode
- generate code128 barcode
- add barcode pdf
- tamper evident barcode
lastmod: '2026-07-20'
linktitle: Java でバーコード署名を作成
og_description: Java と GroupDocs.Signature を使用して PDF にバーコード署名を作成します。Code128 バーコードの追加方法、位置設定、ドキュメントの保護方法をステップバイステップで学びましょう。
og_image_alt: 'Developer guide: Create barcode signature in PDF using Java and GroupDocs'
og_title: Java を使用して PDF にバーコード署名を作成 – 完全ガイド
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to create barcode signature in PDF documents using Java and
    GroupDocs.Signature. Step-by-step tutorial with code examples and best practices.
  headline: How to Create Barcode Signature in PDF using Java
  type: TechArticle
- description: Learn how to create barcode signature in PDF documents using Java and
    GroupDocs.Signature. Step-by-step tutorial with code examples and best practices.
  name: How to Create Barcode Signature in PDF using Java
  steps:
  - name: Initialize the Signature object
    text: '**Definition anchor:** The `Signature` class is GroupDocs.Signature''s
      entry point for loading, modifying, and saving PDF documents. First, you need
      to tell GroupDocs which PDF you''re working with: **What''s happening here:**
      The `Signature` object loads your PDF into memory and prepares it for modifi'
  - name: Configure your barcode options (How to add barcode)
    text: '**Definition anchor:** `BarcodeSignOptions` encapsulates all settings required
      to render a barcode inside a PDF. Now let''s create the barcode signature with
      your data: - `"12345678"` is your barcode data — this could be an order ID,
      certificate number, or any identifier you need. - `Code128` is the '
  - name: Position your barcode (How to sign PDF with barcode)
    text: '**Definition anchor:** `SignatureOptions` provides layout properties such
      as page number, size, and alignment. Here''s where GroupDocs really shines —
      percentage‑based positioning means your barcode looks good on any PDF size:
      **Why percentages matter:** Imagine you''re signing both A4 documents and l'
  - name: Sign and save your document (How to add barcode pdf)
    text: 'Time to actually apply the signature and save your work: **Important note:**
      The output directory must exist before you run this code. GroupDocs won''t create
      nested directories for you, so create them first or handle that in your code:
      **What if something goes wrong?** Wrap this in a try‑catch block'
  type: HowTo
- questions:
  - answer: Yes! Call `signature.sign()` multiple times with different `BarcodeSignOptions`
      for each barcode type. Just ensure they don’t overlap.
    question: Can I use different barcode types in the same PDF?
  - answer: Code128 handles most ASCII characters fine. For Unicode or complex data,
      switch to QR codes—they support UTF‑8 encoding.
    question: How do I handle barcodes that contain special characters?
  - answer: Technically up to 128 characters, but readability drops significantly
      above 30‑40 characters. For larger payloads, use QR codes.
    question: What's the maximum data I can store in a Code128 barcode?
  - answer: Not noticeably—barcodes are vector graphics, typically adding only 5‑20
      KB per barcode depending on size and complexity.
    question: Will adding barcodes significantly increase my PDF file size?
  - answer: Yes! Use `options.setRotationAngle(90)` to rotate your barcode, which
      is handy for margin placement.
    question: Can I rotate barcodes or place them vertically?
  type: FAQPage
tags:
- pdf-signing
- barcode-signature
- document-security
- groupdocs
- java
- pdf
title: Java を使用して PDF にバーコード署名を作成する方法
type: docs
url: /ja/java/barcode-signatures/java-pdf-signing-barcode-groupdocs/
weight: 1
---

# Java を使用して PDF にバーコード署名を作成する方法

このチュートリアルでは、Java と GroupDocs.Signature を使用して PDF ファイルに **バーコード署名** を作成する方法を学びます。バーコード署名は、改ざん防止機能とスキャンの容易さを兼ね備えた機械可読の識別子を埋め込みます—契約書、証明書、請求書、そして信頼できる検証が必要なあらゆる文書に最適です。

## クイック回答
- **バーコード署名とは何ですか？** スキャナーやソフトウェアで読み取れる構造化データを保存する PDF に埋め込まれたバーコードです。  
- **推奨されるバーコードタイプはどれですか？** Code128です。英数字データをコンパクトに処理できるためです。  
- **ライセンスは必要ですか？** テストには無料トライアルで動作しますが、本番環境ではフルライセンスが必要です。  
- **任意のページサイズにバーコードを配置できますか？** はい。パーセンテージベースの位置指定を使用すれば自動的にスケーリングされます。  
- **バーコードはベクター形式ですか？** はい。PDF に数キロバイトしか追加せず、どの解像度でも鮮明です。  

## バーコード署名とは何ですか？
バーコード署名は、PDF ページに直接埋め込まれたベクターベースのバーコードで、視覚的要素としてだけでなく、後で検証可能な暗号署名としても機能します。ID やタイムスタンプなどの構造化データを保存し、文書の完全性を保証すると同時に、機械可読の参照情報を提供します。

## バーコード署名が PDF にとって重要な理由
バーコード署名は、PDF にコンパクトで機械可読の識別子を付与し、即座にスキャンできるため、手動でのデータ入力を排除しエラーを減らします。ベクターグラフィックとして埋め込まれるため、どの解像度でも鮮明で、ファイルサイズは数キロバイトしか増加しません。この可読性、改ざん防止、サイズの小ささの組み合わせにより、契約書、請求書、証明書、そして信頼できる検証が必要なあらゆる文書に最適です。

おそらく直面したことがある課題として、機械可読かつ改ざん防止のユニークな識別子を PDF に追加する必要があります。文書管理システムで証明書を処理したり、将来的に検証が必要な契約書を扱ったりしているかもしれません。

ここでバーコード署名が便利です。単純なテキストスタンプとは異なり、バーコードはスキャナー（およびソフトウェア）が即座に読み取れる構造化データを埋め込むことができます。さらに、GroupDocs.Signature for Java を介した PDF 署名と組み合わせることで、複雑なデータベース検索を追加せずに文書の追跡と検証が可能になる強力な手段が得られます。

このガイドでは、Java の PDF にバーコード署名を実装する方法を、基本的なセットアップから柔軟な位置指定を備えた本番対応コードまで、正確に学びます。請求書システム、証明書ジェネレータ、または契約管理プラットフォームを構築している場合でも、最後まで必要なすべてが揃います。

**習得できること:**
- 数分で GroupDocs.Signature for Java をセットアップする
- Code128 バーコード署名の作成（なぜそれが最適な選択になることが多いか）
- 任意の PDF サイズで機能するパーセンテージベースのレイアウトを使用したバーコードの位置指定
- 開発者が陥りやすい一般的な落とし穴を回避する
- 実装を適切にテストする

## Java でバーコード署名を作成する方法
Java でバーコード署名を作成するには、対象の PDF を読み込み、データ、タイプ、サイズ、位置などのバーコードオプションを設定し、署名を適用して新しいドキュメントを生成します。GroupDocs.Signature がレンダリングと暗号結合を処理するため、必要なパラメータを提供し、ファイルパスを管理するだけで済みます。

## 前提条件と環境チェックリスト
始める前に、以下の項目が準備できていることを確認してください：

- **Java Development Kit (JDK) 8 以上** – すべての GroupDocs Java ライブラリに必須です。
- **Maven または Gradle** – GroupDocs.Signature の依存関係を管理します。
- **IDE**（IntelliJ IDEA、Eclipse、または Java 拡張機能付き VS Code など）
- **GroupDocs.Signature for Java**（バージョン 23.12 以上を推奨）
- **基本的な Java 知識** – クラス作成、例外処理、ファイル I/O の操作に慣れていることが必要です。

## プロジェクトで GroupDocs.Signature を設定する
ライブラリをプロジェクトに導入するのは簡単です。ビルドツールを選択してください：

**Maven ユーザー向け**、`pom.xml` に次の依存関係を追加します：

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle を使用していますか？** `build.gradle` に次の行を追加します：

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**手動設定を好む場合**は、[GroupDocs.Signature for Java リリース](https://releases.groupdocs.com/signature/java/) から JAR を直接ダウンロードし、クラスパスに追加してください。

### ライセンスの取得
本番環境に移行する前に、ライセンス処理を行う必要があります：

- **無料トライアル:** テストに最適です — GroupDocs のウェブサイトから取得し、主要機能を試せます。
- **一時ライセンス:** 評価にもっと時間が必要ですか？30 日間の一時ライセンスを申請してください。
- **フルライセンス:** 本番環境の準備ができましたか？無制限に使用できるライセンスを購入してください。

すべてが正常に動作していることを確認する簡単なチェックです：

```java
Signature signature = new Signature("sample.pdf");
System.out.println("Signature object created successfully.");
```

エラーなく実行できれば、準備完了です！

## Java でバーコード署名を作成する方法
さあ、楽しいパートです — PDF にバーコードを付与しましょう。各段階で何が起こっているか正確に理解できるように、ステップごとに分解します。

### 手順 1: Signature オブジェクトの初期化
**定義アンカー:** `Signature` クラスは、PDF ドキュメントの読み込み、変更、保存のための GroupDocs.Signature のエントリーポイントです。

まず、対象の PDF を GroupDocs に伝える必要があります：

```java
Signature signature = new Signature("input.pdf");
```

**ここでの処理:** `Signature` オブジェクトは PDF をメモリに読み込み、変更の準備をします。ファイルパスが正しいことを確認してください — Windows でバックスラッシュをエスケープせずに使用するとよくある問題です（`\\` を使用するか、クロスプラットフォームで動作するスラッシュ `/` を使用してください）。

### 手順 2: バーコードオプションの設定（バーコードの追加方法）
**定義アンカー:** `BarcodeSignOptions` は、PDF 内にバーコードを描画するために必要なすべての設定をカプセル化します。

それでは、データを使用してバーコード署名を作成しましょう：

```java
BarcodeSignOptions options = new BarcodeSignOptions("12345678");
options.setEncodeType(BarcodeEncodeType.Code128);
```

- `"12345678"` はバーコードデータです — 注文 ID、証明書番号、または必要な任意の識別子に使用できます。
- `Code128` はエンコーディングタイプです（適切なタイプの選択については以下を参照）。

**プロのコツ:** Code128 は数字と文字の両方を扱えるため、ほとんどのユースケースで汎用性があります。数字のみが必要な場合は `Code39` の方がシンプルですが、Code128 の方が柔軟性が高いです。

### 手順 3: バーコードの位置指定（PDF にバーコードで署名する方法）
**定義アンカー:** `SignatureOptions` は、ページ番号、サイズ、配置などのレイアウトプロパティを提供します。

ここが GroupDocs の強みです — パーセンテージベースの位置指定により、どの PDF サイズでもバーコードが適切に表示されます：

```java
options.setLeft(10);   // 10% from the left edge
options.setTop(90);    // 90% from the bottom edge (near the footer)
options.setWidth(30);  // 30% of page width
options.setHeight(10); // 10% of page height
options.setPageNumber(1);
```

**パーセンテージが重要な理由:** A4 文書とリーガルサイズのフォームの両方に署名すると想像してください。パーセンテージ位置指定を使用すれば、バーコードは自動的にスケールし、両方で一貫した見た目になります。固定ピクセル値を使用すると、大きな文書ではバーコードが小さすぎ、小さな文書では大きすぎます。

**実例:** A4 ページ（595 × 842 ポイント）では、幅 30% のバーコードは約 180 ポイントの幅になります。リーガルページ（612 × 1008 ポイント）では約 184 ポイントの幅となり、自動的に比例します。

### 手順 4: 文書に署名して保存する（PDF にバーコードを追加する方法）
実際に署名を適用し、作業を保存する時です：

```java
signature.sign(outputPath, options);
```

**重要な注意点:** このコードを実行する前に出力ディレクトリが存在している必要があります。GroupDocs はネストされたディレクトリを自動作成しないため、事前に作成するか、コード内で処理してください：

```java
new File("output").mkdirs();
```

**問題が発生した場合は？** これを try‑catch ブロックでラップしてください：

```java
try {
    signature.sign("signed.pdf", options);
} catch (Exception e) {
    e.printStackTrace();
}
```

## ニーズに合ったバーコードタイプの選び方（code128 バーコード生成）
GroupDocs は複数のバーコード形式をサポートしており、適切なものを選ぶことが重要です。実用的な比較を示します：

**Code128（デフォルトの選択）:**
- **適用対象:** 英数字混在データ（例: "INV2024-001" のような ID）
- **容量:** 最大 128 文字の ASCII
- **優位点:** コンパクトで広くサポートされ、文字と数字の両方を扱える
- **使用シーン:** 柔軟性が必要で、エンコードするデータの種類が不明な場合

**Code39:**
- **適用対象:** シンプルな英数字コード
- **容量:** 43 文字（A‑Z、0‑9、いくつかの記号）
- **考慮すべき理由:** 古いスキャナーでのサポートが高いことが多い
- **使用シーン:** レガシーシステムで使用する場合、またはデータ密度よりシンプルさが重要な場合

**QR Code:**
- **適用対象:** 大量のデータ（URL、JSON ペイロード）
- **容量:** 最大 3 KB のデータ
- **強み:** 複雑なデータ構造を保存でき、エラー訂正機能が組み込まれている
- **使用シーン:** 構造化データや URL を埋め込む必要がある場合

**EAN/UPC:**
- **適用対象:** 製品識別
- **容量:** 固定長の数字コード（8‑13 桁）
- **使用シーン:** 小売や在庫システムで使用する場合

**簡易判断ガイド:**
- 文字と数字が必要？ → Code128
- 数字のみでシンプルにしたい？ → Code39
- 大量のデータや URL？ → QR Code
- 小売・製品コード？ → EAN/UPC

## よくある落とし穴と回避策（改ざん防止バーコード）
開発者が最も頻繁に直面する問題を以下に示します（あなたが回避できるように）：

### 問題 1: バーコードの位置がずっている
**症状:** バーコードが予期しない位置に表示されたり、切れたりします。  
**主な原因:**
- 異なるページサイズでピクセル値を使用する
- PDF の座標が左下から始まることを忘れる（上左ではない）
- マージンがコンテンツを表示領域外に押し出す  
**解決策:** 常にパーセンテージベースの位置指定を使用して一貫性を保ちます：

```java
options.setLeft(5);
options.setTop(95);
options.setWidth(40);
options.setHeight(12);
```

### 問題 2: バーコードのテキストが読めない
**症状:** エンコードされたテキストは表示されるが、スキャナーが読めない  
**原因:**
- データ量に対してバーコードが小さすぎる
- データに対して不適切なエンコーディングタイプを使用している
- バーと背景のコントラストが低い  
**解決策:** データ長に合わせてバーコードサイズを調整します。Code128 で 10‑15 文字の場合、ページ幅の少なくとも 8‑10% を目安にしてください。

### 問題 3: ファイルパス例外
**症状:** `FileNotFoundException` などのエラー  
**原因:**
- シングルバックスラッシュのハードコーディングされた Windows パス
- 出力ディレクトリが存在しない
- ファイル権限の問題  
**解決策:** スラッシュ `/` を使用（どこでも動作）し、事前にディレクトリを作成してください：

```java
Path output = Paths.get("output/signed.pdf");
Files.createDirectories(output.getParent());
```

### 問題 4: 大きな PDF のメモリ問題
**症状:** 大きなドキュメント処理時にメモリ不足エラーが発生する  
**解決策:** 終了時に `Signature` オブジェクトを閉じてリソースを解放します：

```java
signature.close();
```

## バーコード実装のテスト
デプロイ前に、バーコードが実際に機能することを確認してください。実用的なテストチェックリストを示します：

### 1. 視覚的検査テスト
- 署名済み PDF を開き、以下を確認します：
  - バーコードが見えていて、正しく位置しているか？
  - ぼやけていないか、鮮明に見えるか？
  - 周囲に十分な余白があるか？

### 2. スキャンテスト
スマートフォンのバーコードスキャナーアプリ（例: “Barcode Scanner” や “QR & Barcode Reader”）を使用して確認します：
- スキャナーがバーコードを読み取れるか
- デコードされたデータがエンコードしたものと一致するか
- 様々な角度や距離から機能するか

### 3. クロスプラットフォームテスト
異なるデバイスで PDF を開きます：
- Windows（Adobe Reader、Chrome）
- Mac（Preview、Chrome）
- モバイルデバイス（iOS、Android）

すべての環境でバーコードが正しく表示されることを確認してください。

### 4. 自動テストコード
実行できるシンプルなテストを示します：

```java
Signature testSignature = new Signature("signed.pdf");
List<BarcodeSignature> signatures = testSignature.search(BarcodeSignature.class);
if (signatures.size() > 0) {
    System.out.println("Barcode found: " + signatures.get(0).getText());
}
```

## バーコード署名の実務活用例
この手法が本番システムで本当に活躍する場面を見てみましょう：

### 1. 証明書の生成と検証
**シナリオ:** 受講完了証明書を発行するトレーニングプラットフォームを構築している。  
**実装:** ユニークな証明書 ID（例: “CERT‑2024‑00123”）を生成し、右下隅に Code128 バーコードとして埋め込む。バーコードをスキャンすると API が証明書情報を即座に取得でき、手動入力が不要になる。

### 2. 請求書追跡システム
**シナリオ:** 会社が毎月数千件の請求書を処理している。  
**実装:** 請求書番号と支払期限を QR コードとして追加し、スキャン装置が容易に読み取れる位置に配置する。自動仕分けシステムが人手を介さずに請求書を振り分け、処理時間を数時間から数分に短縮する。

### 3. 法的契約管理
**シナリオ:** 法律事務所が契約書のバージョンと改訂を追跡する必要がある。  
**実装:** 各契約バージョンに、契約 ID、バージョン番号、署名日を含むユニークなバーコード識別子を付与する。監査時にスキャンすると、全バージョン履歴が自動的に取得できる。

### 4. 医療記録のセキュリティ
**シナリオ:** 病院が不正な記録アクセスを防止したい。  
**実装:** 患者 ID と記録作成タイムスタンプをバーコードに埋め込む。認証済みデバイスのみがデコードして完全な記録にアクセスでき、スキャンごとにコンプライアンス用の監査ログが生成される。

## パフォーマンス最適化のヒント（java ドキュメントセキュリティ）
多数の PDF に署名する際は、パフォーマンスが重要です。スムーズに動作させるためのヒントを以下に示します：

### バッチ処理戦略
1 件ずつ署名する代わりに、バッチ処理します：

```java
for (String filePath : pdfList) {
    Signature batchSignature = new Signature(filePath);
    batchSignature.sign(outputPath, options);
    batchSignature.close();
}
```

**この利点:** オプションオブジェクトを再利用し、リソースを適切にクローズすることでメモリリークを防止します。

### 大きな PDF のメモリ管理
PDF が 50 MB を超える場合：
- 複数同時に読み込むのではなく、順次処理する。
- try‑with‑resources を使用してクリーンアップを保証する。
- ヒープサイズを監視し、必要に応じて JVM パラメータを調整する: `-Xmx2g`。

### 頻繁に使用するバーコードのキャッシュ
同じバーコードで多数の文書に署名する場合、`BarcodeSignOptions` インスタンスをキャッシュします：

```java
BarcodeSignOptions cachedOptions = new BarcodeSignOptions("STATIC_ID");
cachedOptions.setEncodeType(BarcodeEncodeType.Code128);
```

## バーコード署名を使用すべき時（使用すべきでない時）
**最適なシナリオ:**
- 機械可読の文書識別子が必要。
- 文書が自動的にスキャンまたは処理される。
- デジタル証明書なしで改ざん防止の追跡が欲しい。
- 既存のバーコードインフラとの統合が必要。

**以下の場合は適さない:**
- 法的に有効なデジタル署名が必要（代わりにデジタル証明書を使用）。
- 文書が人間のみの閲覧対象で、シンプルなテキスト透かしで十分な場合。
- 非常に小さな文書で、バーコードがページを支配してしまう場合。
- セキュリティ要件で暗号化が必須—バーコードは誰でも見えてスキャン可能。

**アプローチを組み合わせられますか？** はい！多くのシステムでは、追跡用にバーコード署名を、法的有効性のためにデジタル署名を併用しています。

## よくある質問
**Q: 同じ PDF に異なるバーコードタイプを使用できますか？**  
A: はい！各バーコードタイプごとに異なる `BarcodeSignOptions` を使用して `signature.sign()` を複数回呼び出します。重ならないようにしてください。

**Q: 特殊文字を含むバーコードはどう扱いますか？**  
A: Code128 はほとんどの ASCII 文字を問題なく扱えます。Unicode や複雑なデータの場合は QR コードに切り替えてください—UTF‑8 エンコードをサポートしています。

**Q: Code128 バーコードに保存できる最大データ量は？**  
A: 理論上は最大 128 文字ですが、30‑40 文字を超えると可読性が大幅に低下します。より大きなペイロードには QR コードを使用してください。

**Q: バーコードを追加すると PDF のファイルサイズは大幅に増加しますか？**  
A: 目立った増加はありません—バーコードはベクターグラフィックで、サイズと複雑さにもよりますが通常は 5‑20 KB 程度しか増えません。

**Q: バーコードを回転させたり縦向きに配置できますか？**  
A: はい！`options.setRotationAngle(90)` を使用してバーコードを回転させることができ、余白への配置に便利です。

**Q: 複数ページの PDF のすべてのページにバーコードを表示させるには？**  
A: ページをループし、各ページに署名を適用します。どのページに署名するかは、GroupDocs のドキュメントにある `PagesSetup` クラスで確認してください。

**Q: バーコードスキャナーが生成されたバーコードを読み取れない場合は？**  
A: まず、スキャナーが選択したバーコードタイプをサポートしているか確認してください。その後、バーコードのサイズを大きくします—多くの読み取り問題はバーが小さすぎることが原因です。信頼できる読み取りのために、幅は最低 1 インチ（2.54 cm）を目安にしてください。

## 追加リソース
- [GroupDocs.Signature for Java ドキュメント](https://docs.groupdocs.com/signature/java/)
- [API リファレンスガイド](https://reference.groupdocs.com/signature/java/)

- [最新バージョンのダウンロード](https://releases.groupdocs.com/signature/java/)
- [無料トライアルアクセス](https://releases.groupdocs.com/signature/java/)
- [一時ライセンス取得](https://purchase.groupdocs.com/temporary-license/)
- [フルライセンス購入](https://purchase.groupdocs.com/buy)

- [サポートフォーラム](https://forum.groupdocs.com/c/signature/) - GroupDocs エンジニアが参加する活発なコミュニティ

---

**Last Updated:** 2026-07-20  
**Tested With:** GroupDocs.Signature 23.12 (Java)  
**Author:** GroupDocs

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

```java
import com.groupdocs.signature.Signature;

public class QuickTest {
    public static void main(String[] args) {
        try {
            Signature signature = new Signature("test-document.pdf");
            System.out.println("GroupDocs.Signature is ready to go!");
        } catch (Exception e) {
            System.err.println("Setup issue: " + e.getMessage());
        }
    }
}
```

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
Signature signature = new Signature(filePath);
```

```java
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

BarcodeSignOptions options = new BarcodeSignOptions("12345678");
options.setEncodeType(BarcodeTypes.Code128);
```

```java
import com.groupdocs.signature.domain.enums.MeasureType;
import com.groupdocs.signature.domain.Padding;

// Use percentages instead of fixed pixels
options.setLocationMeasureType(MeasureType.Percents);
options.setLeft(5);  // 5% from the left edge
options.setTop(5);   // 5% from the top

// Size it proportionally too
options.setSizeMeasureType(MeasureType.Percents);
options.setWidth(10);  // 10% of page width
options.setHeight(5);  // 5% of page height

// Add some breathing room with margins
Padding margins = new Padding();
margins.setLeft(1);
margins.setTop(1);
margins.setRight(1);
options.setMargin(margins);
```

```java
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithPercents/sample_signed.pdf";
signature.sign(outputFilePath, options);
```

```java
Path outputPath = Paths.get(outputFilePath);
Files.createDirectories(outputPath.getParent());
signature.sign(outputFilePath, options);
```

```java
try {
    signature.sign(outputFilePath, options);
    System.out.println("PDF signed successfully at: " + outputFilePath);
} catch (Exception e) {
    System.err.println("Signing failed: " + e.getMessage());
    e.printStackTrace();
}
```

```java
options.setLocationMeasureType(MeasureType.Percents);
options.setLeft(5);  // 5% from left works on any page width
```

```java
options.setWidth(10);  // Give it room to breathe
options.setHeight(5);  // Maintain proper aspect ratio
```

```java
String filePath = "documents/sample.pdf";  // Works on Windows, Mac, Linux
Files.createDirectories(Paths.get("output/signed"));
```

```java
try (Signature signature = new Signature(filePath)) {
    signature.sign(outputFilePath, options);
} // Automatically closes and releases memory
```

```java
import org.junit.Test;
import static org.junit.Assert.*;

public class BarcodeSignatureTest {
    
    @Test
    public void testBarcodeSigning() {
        String testPdf = "test-data/sample.pdf";
        String output = "test-output/signed.pdf";
        
        try (Signature signature = new Signature(testPdf)) {
            BarcodeSignOptions options = new BarcodeSignOptions("TEST123");
            options.setEncodeType(BarcodeTypes.Code128);
            
            signature.sign(output, options);
            
            // Verify output file exists
            assertTrue(new File(output).exists());
            
            // Verify file size increased (signature was added)
            long originalSize = new File(testPdf).length();
            long signedSize = new File(output).length();
            assertTrue(signedSize > originalSize);
            
        } catch (Exception e) {
            fail("Signing should not throw exception: " + e.getMessage());
        }
    }
}
```

```java
List<String> pdfFiles = Arrays.asList("doc1.pdf", "doc2.pdf", "doc3.pdf");

for (String pdfFile : pdfFiles) {
    try (Signature signature = new Signature(pdfFile)) {
        BarcodeSignOptions options = createBarcodeOptions(); // Reuse options
        signature.sign(getOutputPath(pdfFile), options);
    }
}
```

```java
// Create options once, reuse many times
BarcodeSignOptions templateOptions = createStandardBarcodeOptions();

// For each document, clone and customize
BarcodeSignOptions documentOptions = templateOptions.clone();
documentOptions.setText(uniqueDocumentId);
```

## 関連チュートリアル
- [Java バーコード署名チュートリアル - PDF にバーコードを追加、検証、管理](/signature/java/barcode-signatures/)
- [Java でバーコード署名を作成 – PDF バーコードの更新](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [Java と GroupDocs.Signature を使用して PDF の QR コードを読み取る方法](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)