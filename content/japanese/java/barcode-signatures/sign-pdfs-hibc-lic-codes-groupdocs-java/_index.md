---
categories:
- Document Signing
- Healthcare Integration
date: '2026-05-16'
description: GroupDocs.Signature for Java を使用して、Data Matrix PDFを作成し、QR code PDFを追加する方法を学びます。医療文書の署名に関するステップバイステップガイド。
keywords:
- create data matrix pdf
- add qr code pdf
- HIBC barcode Java
lastmod: '2026-05-16'
linktitle: HIBC PDF署名 Java ガイド
schemas:
- author: GroupDocs
  dateModified: '2026-05-16'
  description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  headline: Create Data Matrix PDF with HIBC Barcode in Java
  type: TechArticle
- description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  name: Create Data Matrix PDF with HIBC Barcode in Java
  steps:
  - name: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
    text: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
  - name: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
    text: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
  - name: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
    text: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
  - name: '**Apply the signature** to the PDF.'
    text: '**Apply the signature** to the PDF.'
  - name: '**Dispose of resources** to free file handles and avoid memory leaks.'
    text: '**Dispose of resources** to free file handles and avoid memory leaks.'
  - name: '**Import QR‑specific classes**'
    text: '**Import QR‑specific classes**'
  - name: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
    text: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
  - name: '**Sign the document**'
    text: '**Sign the document**'
  type: HowTo
- questions:
  - answer: Yes, it also supports DOCX, XLSX, PPTX, PNG, JPEG, and TIFF with the same
      barcode‑signing API.
    question: Can GroupDocs.Signature sign file types other than PDF?
  - answer: Verify that your HIBC string follows the exact HIBCC syntax, use the online
      validator, and ensure you’re using the correct `QrCodeTypes` constant for the
      chosen format.
    question: How do I troubleshoot “Invalid barcode content” errors?
  - answer: QR ≈ 4,296 alphanumeric characters, Aztec ≈ 3,832 numeric / 3,067 alphanumeric,
      Data Matrix ≈ 3,116 numeric / 2,335 alphanumeric. Keep codes under 200 characters
      for optimal scan reliability.
    question: What is the maximum data capacity for each HIBC format?
  - answer: Absolutely. Create separate `QrCodeSignOptions` objects with different
      positions and call `signature.sign()` for each. Just ensure they don’t overlap.
    question: Is it possible to embed multiple barcode types in one PDF?
  - answer: No. After the JAR is on the classpath and the license is activated, all
      operations are performed locally.
    question: Do I need an internet connection for signing at runtime?
  type: FAQPage
tags:
- java
- pdf-signing
- hibc
- healthcare
- barcode
- pharmaceutical
title: JavaでHIBCバーコードを使用したData Matrix PDFの作成
type: docs
url: /ja/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/
weight: 1
---

# データマトリックスPDFをHIBCバーコードで作成する

医薬品やヘルスケア物流ソフトウェアを構築している場合、紙ベースの追跡や署名紛失、監査の悪夢に直面していることでしょう。**データマトリックスPDF** を作成し、HIBC LIC バーコードを埋め込むことで、印刷・スキャン・規制審査に耐える改ざん検知可能な機械可読トレイルを提供できます。このチュートリアルでは、GroupDocs.Signature for Java を使用して **QRコードPDF** のサポートに加え、Aztec と Data Matrix 形式を追加する方法を正確に示します。

## クイック回答
- **Java で HIBC バーコードを扱うライブラリは？** GroupDocs.Signature for Java。  
- **最もコンパクトなバーコード形式は？** Data Matrix – 小さなラベルに最適。  
- **同じ PDF に QR と Data Matrix の両方を追加できるか？** はい、別々の `QrCodeSignOptions` を作成すれば OK。  
- **実行時にインターネット接続は必要か？** いいえ、インストール後は完全にオフラインで動作します。  
- **推奨される Java バージョンは？** 本番環境向けのパフォーマンスを考慮し、Java 11+。

## HIBC バーコード PDF 署名とは？
GroupDocs.Signature for Java の `Signature` クラスは PDF ドキュメントを表し、HIBC バーコードをデジタル署名として埋め込むメソッドを提供します。HIBC バーコードで PDF に署名すると、サプライチェーンの任意の地点でスキャン可能な検証可能な改ざん防止レコードが作成されます。

## Data Matrix と QR コードを同時に使用する理由
GroupDocs.Signature は **50 以上の入力・出力形式** をサポートし、PDF 全体をメモリに読み込まずに数百ページの文書を処理できます。Data Matrix を高密度・小領域ラベルに、QR を広い領域の文書に使用することで、可読性、データ容量（QR は最大 4,296 文字）、印刷スペース効率のベストバランスが得られます。

## 前提条件
- **JDK 11 以上**（Java 8 でも動作しますが、最適なパフォーマンスのために Java 11+ を推奨）。  
- **IDE**（IntelliJ IDEA、Eclipse、または Java 拡張機能付き VS Code）。  
- **Maven または Gradle**（依存関係管理用、例は下記参照）。  
- **サンプル PDF**（例：`sample.pdf`）で実装をテスト。  
- **有効な GroupDocs.Signature ライセンス**（開発用は無料トライアル、本番は有料ライセンス）。

## GroupDocs.Signature for Java の設定

### Maven 設定
`pom.xml` に以下の依存関係を追加してください：

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle 設定
Gradle プロジェクトの場合、`build.gradle` に次を追加します：

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### 直接ダウンロードオプション
[GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) から JAR ファイルを直接ダウンロードし、プロジェクトのクラスパスに手動で追加することも可能です。この方法はネットワークが制限された環境で有効です。

### ライセンス取得
ウォーターマークを除去し全機能を有効化するには、GroupDocs から無料トライアルまたは一時ライセンスを取得してください。本番環境では購入ライセンスが必要です。

### 基本的な初期化
`Signature` クラスはすべての署名操作のエントリーポイントです。PDF をロードし、バーコードを適用し、署名済みファイルを書き出します。

```java
import com.groupdocs.signature.Signature;

class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("sample.pdf");
        // Proceed with signing operations...
    }
}
```

## HIBC バーコードで Data Matrix PDF を作成する手順
ソース PDF を読み込み、Data Matrix 形式用の `QrCodeSignOptions` オブジェクトを設定し、`sign()` を呼び出すだけで、準拠した HIBC Data Matrix バーコードを埋め込めます。以下の手順で必要なコードを順に解説します。`QrCodeSignOptions` はバーコード署名の種類、内容、サイズ、位置などを定義します。

1. **必要なクラスをインポート** – 署名エンジンと Data Matrix オプションにアクセスできます。  

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
```

2. **`Signature` オブジェクトをインスタンス化** – ソースと出力ファイルの絶対パスを指定します。  

```java
String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY";
String destinFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithHIBCLICQR.pdf";

final Signature signature = new Signature(sourceFilePath);
```

3. **Data Matrix オプションを設定** – HIBC 文字列を設定し、`QrCodeTypes.HIBCLICDataMatrix` を選択、配置座標を定義します。`QrCodeTypes` は HIBC 署名でサポートされるバーコード形式を列挙しています。  

```java
QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR);
hibcLic_QR.setLeft(1); // Set the position from left
hibcLic_QR.setTop(1);   // Set the position from top
hibcLic_QR.setReturnContent(true); // Return content after signing
hibcLic_QR.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

4. **PDF に署名を適用**  

```java
signature.sign(destinFilePath, hibcLic_QR);
```

5. **リソースを解放** – ファイルハンドルを閉じ、メモリリークを防止します。  

```java
finally {
    if (signature != null) signature.dispose();
}
```

### 完全な動作例
以下は単一ブロックにまとめた全体フローです（プレースホルダーは前述のスニペットから貼り付けた正確なコードです）：

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;

public class HibcQrSigning {
    public static void main(String[] args) {
        String sourceFilePath = "sample.pdf";
        String destinFilePath = "output/SignWithHIBCLICQR.pdf";
        
        Signature signature = null;
        try {
            signature = new Signature(sourceFilePath);
            
            QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions(
                "A123PROD30917/75#422011907#GP293", 
                QrCodeTypes.HIBCLICQR
            );
            hibcLic_QR.setLeft(1);
            hibcLic_QR.setTop(1);
            hibcLic_QR.setReturnContent(true);
            hibcLic_QR.setReturnContentType(FileType.PNG);
            
            signature.sign(destinFilePath, hibcLic_QR);
            System.out.println("PDF signed successfully with HIBC QR code");
            
        } catch (Exception e) {
            System.err.println("Error signing PDF: " + e.getMessage());
            e.printStackTrace();
        } finally {
            if (signature != null) signature.dispose();
        }
    }
}
```

#### 直接回答（40〜70語）
**Data Matrix PDF** を作成するには、`Signature` をソース PDF でインスタンス化し、`QrCodeSignOptions` を `QrCodeTypes.HIBCLICDataMatrix` に設定し、正しい形式の HIBC 文字列を提供して `signature.sign(outputPath, options)` を呼び出します。ライブラリは署名済み PDF を出力先に書き込み、レイアウトを保持しつつ改ざん防止署名としてバーコードを埋め込みます。

## GroupDocs.Signature を使って QR コード PDF を追加する方法
PDF を読み込み、QR 形式用に `QrCodeSignOptions` を設定し、`sign()` を呼び出します。この 2 行パターンは任意の PDF サイズで機能し、最適な可読性のために QR 画像を自動スケーリングします。`QrCodeSignOptions` は QR バーコード署名の内容と視覚プロパティを構成し、設定した座標に基づいてコードを配置し、既存コンテンツと重ならず印刷後もスキャン可能にします。

1. **QR 用クラスをインポート**  

```java
QrCodeSignOptions hibcLic_AZ = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec);
hibcLic_AZ.setLeft(1); // Set the position from left
hibcLic_AZ.setTop(200); // Set the position from top
hibcLic_AZ.setReturnContent(true); // Return content after signing
hibcLic_AZ.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

2. **QR オプションを作成・設定** – `QrCodeTypes.HIBCLICQR` を使用する点に注意してください。  

```java
signature.sign(destinFilePath, hibcLic_AZ);
```

3. **ドキュメントに署名**  

```java
QrCodeSignOptions hibcLic_DM = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix);
hibcLic_DM.setLeft(1); // Set the position from left
hibcLic_DM.setTop(400); // Set the position from top
hibcLic_DM.setReturnContent(true); // Return content after signing
hibcLic_DM.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

> **直接回答:** `QrCodeSignOptions` で `QrCodeTypes.HIBCLICQR` を指定し、HIBC コンテンツ文字列を設定、`setLeft()` と `setTop()` で位置を決め、`signature.sign(outputPath, options)` を呼び出します。QR バーコードは即座に埋め込まれ、スマートフォンやスキャナーで取得可能です。

## 避けるべき一般的なミス

### 1. リソース解放を忘れる
**誤:**  
```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  

**修正:** `Signature` の使用を try‑with‑resources ブロックで囲むか、finally 句で明示的に `close()` を呼び出してください。

### 2. HIBC 形式文字列が不正
**誤:** 「12345」など汎用文字列を使用。  
**修正:** HIBCC 標準に従い、例 `A123PROD30917/75#422011907#GP293` のように記述し、[HIBCC online validator](https://www.hibcc.org/) で検証してください。

### 3. ファイルパスをハードコーディング
**誤:**  
```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  

**修正:** 設定ファイルまたは環境変数にパスを保存し、実行時に読み込むようにします。

### 4. バーコード位置の衝突を無視
既存テキストや署名から離れた位置に配置し、PDF 座標系（原点は左下）を利用して印刷サンプルで確認してください。

### 5. 実機スキャナでテストしない
署名済み PDF を印刷し、実際のワークフローで使用するハードウェアでスキャンし、印刷品質別の可読性を検証します。

## ヘルスケアでの実務例

| シナリオ | 推奨バーコード | 理由 |
|----------|----------------|------|
| **医薬品流通** | QR Code | 大容量データ、スマートフォンでの汎用スキャンに最適 |
| **在庫管理** | Data Matrix | フットプリントが小さく、密集シェルフラベルに最適 |
| **規制コンプライアンス（FDA 21 CFR Part 11）** | QR + Data Matrix | 冗長性と監査性を提供するデュアルフォーマット |
| **医療機器追跡** | Aztec Code | 限られたスペースのパッケージに適したコンパクトサイズ |

## パフォーマンス考慮点とベストプラクティス

### バッチ処理パターン
```java
List<String> filesToSign = getFileList();
for (String filePath : filesToSign) {
    Signature signature = null;
    try {
        signature = new Signature(filePath);
        // Sign and save
    } finally {
        if (signature != null) signature.dispose();
    }
}
```

- ファイルごとに新しい `Signature` インスタンスを作成し、メモリ使用量を抑制。  
- 固定スレッドプール（`Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() - 1)`）で並列処理を行うが、各 `Signature` が PDF 全体をメモリに保持するためヒープサイズを監視。

### ライブラリは常に最新に保つ
GroupDocs のリリースは処理速度を最大 **20 %** 向上させ、HIBC 準拠機能を追加します。四半期ごとの依存関係チェックをスケジュールしてください。

### テンプレートのキャッシュ活用
PDF テンプレートを一度ロードし、各バーコードバリエーションごとにクローンして署名すると I/O が削減され、高ボリュームワークフローが高速化します。

## FAQ

**Q: PDF 以外のファイルタイプにも署名できるか？**  
A: はい、DOCX、XLSX、PPTX、PNG、JPEG、TIFF でも同じバーコード署名 API が利用可能です。

**Q: “Invalid barcode content” エラーの対処法は？**  
A: HIBC 文字列が正確に HIBCC 構文に従っているか確認し、オンラインバリデータで検証、選択したフォーマットに合った `QrCodeTypes` 定数を使用してください。

**Q: 各 HIBC 形式の最大データ容量は？**  
A: QR ≈ 4,296 英数字、Aztec ≈ 3,832 数字 / 3,067 英数字、Data Matrix ≈ 3,116 数字 / 2,335 英数字。スキャン信頼性を高めるため、200 文字以下に抑えることを推奨します。

**Q: 1つの PDF に複数のバーコードタイプを埋め込めるか？**  
A: 可能です。異なる位置で複数の `QrCodeSignOptions` を作成し、`signature.sign()` をそれぞれ呼び出してください。重ならないように注意します。

**Q: 実行時にインターネット接続は必要か？**  
A: いいえ。JAR がクラスパスにあり、ライセンスが有効化されていれば、すべてローカルで実行されます。

## 追加リソース

- [GroupDocs.Signature for Java Documentation](https://docs.groupdocs.com/signature/java/)  
- [API Reference Guide](https://reference.groupdocs.com/signature/java/)  
- [Latest Release Downloads](https://releases.groupdocs.com/signature/java/)  
- [Purchase License](https://purchase.groupdocs.com/buy)  
- [Get Free Trial](https://releases.groupdocs.com/signature/java/)  
- [Request Temporary License](https://purchase.groupdocs.com/temporary-license/)  
- [GroupDocs Forum](https://forum.groupdocs.com/c/signature/)

---

**最終更新日:** 2026-05-16  
**テスト環境:** GroupDocs.Signature 23.12 for Java  
**作者:** GroupDocs  

```java
signature.sign(destinFilePath, hibcLic_DM);
```

## 関連チュートリアル

- [Create Barcode Signature PDF in Java – GroupDocs Guide](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)
- [Create Barcode Signature in Java – Update PDF Barcodes](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [How to read QR code PDF using Java and GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)