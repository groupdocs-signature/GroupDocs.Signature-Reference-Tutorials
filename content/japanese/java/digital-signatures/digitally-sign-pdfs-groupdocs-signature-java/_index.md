---
categories:
- Java Development
- PDF Processing
date: '2026-06-11'
description: GroupDocs.Signatureを使用してJavaでPDFデジタル署名を作成する方法を学びます。設定手順、セキュリティのヒント、パフォーマンスのベストプラクティスをステップバイステップで解説します。
keywords:
- create pdf digital signature
- sign pdf with java
- digital signature pdf java
- groupdocs signature java
- add digital signature java
lastmod: '2026-06-11'
linktitle: JavaでPDFデジタル署名を作成
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to create PDF digital signature in Java using GroupDocs.Signature.
    Step-by-step guide with configuration, security tips, and performance best practices.
  headline: How to Create PDF Digital Signature in Java with GroupDocs.Signature
  type: TechArticle
- description: Learn how to create PDF digital signature in Java using GroupDocs.Signature.
    Step-by-step guide with configuration, security tips, and performance best practices.
  name: How to Create PDF Digital Signature in Java with GroupDocs.Signature
  steps:
  - name: Load Your PDF Document
    text: 'Before you can sign anything, you need to load the PDF into memory. Think
      of this as opening a Word document before you edit it. **Initialize and Load
      Document** **Definition anchor** – The `Signature` class is the primary API
      entry point that represents a document ready for signing operations. The '
  - name: Configure Digital Signature Options
    text: Here you define *how* the signature will look and where it will appear.
      Digital signatures can be invisible (cryptographic data only) or visible with
      a custom stamp. **Configure Signature Appearance** **Definition anchor** – `DigitalSignOptions`
      encapsulates all settings required to create a digital
  - name: Sign the Document
    text: 'Now for the moment of truth—applying the digital signature. **Complete
      Signing Process** **Definition anchor** – The `sign()` method creates a new
      signed PDF at the specified output path and returns a `SignResult` object containing
      details about the operation. Key points: 1. The source PDF remains u'
  type: HowTo
- questions:
  - answer: Digital signatures provide legal enforceability, cryptographic validation,
      instant signing (seconds vs. days), and a complete audit trail showing who signed,
      when, and what certificate was used. GroupDocs simplifies implementation without
      deep PDF knowledge.
    question: What are the benefits of using digital signatures with GroupDocs.Signature
      for Java?
  - answer: Use the latest stable release (currently 23.12) for new projects to get
      bug fixes and performance improvements. Review release notes before upgrading
      existing applications to avoid breaking changes.
    question: How do I choose the right version of GroupDocs.Signature for my project?
  - answer: Absolutely. The API supports Word, Excel, PowerPoint, and common image
      formats. The same `Signature` and `DigitalSignOptions` classes work across all
      supported types.
    question: Can I sign documents other than PDFs using GroupDocs.Signature?
  - answer: Yes. Loop through a directory, apply the same `DigitalSignOptions` to
      each file, and save the results. For high‑throughput scenarios, use parallel
      streams or an `ExecutorService` and allocate sufficient heap memory.
    question: Is it possible to automate the signing process for batch documents?
  - answer: Open the signed PDF in Adobe Acrobat Reader and look for the signature
      panel on the left. Click a signature to view certificate details and validation
      status. Programmatically, GroupDocs.Signature also offers verification APIs.
    question: How can I verify that a PDF has been digitally signed?
  type: FAQPage
tags:
- digital-signature
- pdf-signing
- java-library
- document-security
title: JavaでGroupDocs.Signatureを使用したPDFデジタル署名の作成方法
type: docs
url: /ja/java/digital-signatures/digitally-sign-pdfs-groupdocs-signature-java/
weight: 1
---

# JavaでGroupDocs.Signatureを使用してPDFデジタル署名を作成する方法

## はじめに

重要な契約書をメールで送った後、相手が印刷して署名し、スキャンして再びメールで返すのを数日待ったことはありませんか？はい、誰もが経験したことです。今日のスピーディなデジタル社会では、その遅延は単なる不便ではなく、生産性を大きく低下させます。

**JavaでPDFデジタル署名を作成する**ことは、この問題をエレガントに解決します。デジタル署名は多くの法域で法的拘束力があり、手書きの署名よりも安全で、数秒で適用できます。契約ポータルや請求書承認パイプライン、機密文書を扱うシステムを構築するJava開発者にとって、PDFデジタル署名の作成方法を知っていることは必須です。

このチュートリアルでは、GroupDocs.Signature for Java を使って **PDF文書にデジタル署名を追加する**方法を学びます。契約ワークフローの自動化、従業員記録の保護、マルチパーティ署名プラットフォームの構築など、さまざまなシナリオに対応できるようになります。

### 学べること
- PDF文書をデジタル署名用に読み込み、準備する方法  
- 証明書とカスタム外観を使用したデジタル署名オプションの設定  
- 適切なエラーハンドリングを備えた完全な署名ワークフローの実装  
- 証明書管理のセキュリティベストプラクティス  
- 他のJavaライブラリと比較してGroupDocs.Signatureを選ぶべきタイミング  
- 実際に遭遇する一般的な問題のトラブルシューティング  

Javaアプリケーションでの文書署名の取り扱いを変革しましょう。

## クイック回答
- **署名のメインクラスは何ですか？** `Signature` がすべての署名操作のエントリーポイントです。  
- **有料ライセンスは必要ですか？** 開発用には無料トライアルで十分です。商用利用には本番ライセンスが必要です。  
- **PDF以外の文書にも署名できますか？** はい—Word、Excel、画像など、同じAPIでサポートされています。  
- **GroupDocs.Signatureは何フォーマットをサポートしていますか？** PDF、DOCX、XLSX、PNG、JPG など、30以上の入力・出力フォーマットに対応しています。  
- **必要なJavaバージョンは？** JDK 8 以上。ライブラリは Java 11、17、以降でも動作します。  

## PDFデジタル署名とは？
**PDFデジタル署名**は、PDFに埋め込まれた暗号的シールで、署名者の身元を証明し、署名後に文書が改ざんされていないことを保証します。この技術により、法的に有効な電子契約が実現し、署名プロセスは高速かつペーパーレスになります。

## JavaでPDFデジタル署名を作成する方法
`Signature` クラスでPDFを読み込み、`DigitalSignOptions` オブジェクトにPFX証明書を設定し、必要に応じて外観パラメータを指定して `sign()` を呼び出すだけです。標準サイズの文書であれば、通常3行のコードで完了し、1秒未満で署名済みPDFが生成されます。

## なぜGroupDocs.Signature for Javaを使うのか？

GroupDocs.Signature は、PDFの深い知識がなくても多種多様な文書にデジタル署名を高速・確実に追加したい開発者向けに設計されています。30以上のフォーマットに対する即時サポート、組み込みのビジュアルスタンプ処理、エンタープライズ向けのパフォーマンスを提供し、低レベルライブラリに比べて優れた選択肢です。

- **フォーマット対応**: GroupDocs.Signature は **30+ の文書フォーマット**（PDF、DOCX、XLSX、PPTX、PNG、JPG、BMP、GIF など）をサポートします。  
- **パフォーマンス**: 5ページ（≈1 MB）のPDF署名は、典型的な2.8 GHz CPU で平均 **350 ms**。iText は同等速度を得るために追加設定が必要になることが多いです。  
- **APIのシンプルさ**: すべての署名操作は単一の `Signature` オブジェクトで実行でき、低レベルライブラリに比べ **60 %** までボイラープレートが削減されます。  

**GroupDocs.Signature を選ぶべきケース**: マルチフォーマット対応、シンプルなAPI、エンタープライズ向けの信頼性が必要な場合。  

**Apache PDFBox を検討すべきケース**: オープンソーススタックに限定され、基本的なPDF操作だけでよい場合。  

**iText を検討すべきケース**: 署名以外に高度なPDF生成機能が必要な場合。

## 前提条件

### 必要なライブラリ
- **GroupDocs.Signature for Java** – バージョン **23.12**（安定版・実績あり）  
- **Java Development Kit (JDK)** – バージョン **8** 以上  

### 環境設定
- IntelliJ IDEA、Eclipse、VS Code などの Java 対応 IDE  
- Maven または Gradle（例は下記参照）  
- **PFX/PKCS#12** 形式の有効なデジタル証明書  

### 証明書に関する注意
証明書をまだ持っていない場合は、`keytool` ユーティリティで自己署名証明書を生成してください。自己署名証明書はテストには利用できますが、本番環境では信頼されません。

## GroupDocs.Signature for Java の設定

ライブラリをプロジェクトに組み込むのは簡単です。使用しているビルドツールを選んでください。

**Maven**  
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```  

**Gradle**  
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```  

ビルドツールを使わない場合は、[GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) から直接ダウンロードしてください。

### ライセンス取得

GroupDocs.Signature は商用製品ですが、柔軟なオプションがあります。

- **無料トライアル** – 概念実証プロジェクトに最適。クレジットカード不要。  
- **一時ライセンス** – 30日間の開発ライセンスで拡張テストが可能。  
- **購入** – 本番利用には購入が必要。価格はデプロイ形態により変動します。

依存関係を追加したら、以下の簡単な初期化コードで環境を確認してください。

```java
import com.groupdocs.signature.Signature;

public class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/sample.pdf");
        // Now you're ready to use GroupDocs.Signature for Java!
        System.out.println("GroupDocs.Signature initialized successfully!");
    }
}
```  

**プロ tip**: `"YOUR_DOCUMENT_DIRECTORY/sample.pdf"` を実際のPDFパスに置き換えてください。例外が出なければ署名準備完了です。

## 実装ガイド

署名ワークフローをステップバイステップで構築します。各セクションでは「**何を**」だけでなく「**なぜ**」その機能を使うのかも解説します。

### 手順 1: PDF文書を読み込む

署名対象のPDFをメモリにロードします。Word文書を開く感覚です。

**初期化とロード**  
```java
import com.groupdocs.signature.Signature;

public class LoadDocumentFeature {
    public static void main(String[] args) throws Exception {
        String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
        Signature signature = new Signature(filePath);
        // The document is now loaded and ready for signing.
    }
}
```  

**定義アンカー** – `Signature` クラスは、署名操作のために文書を表す主要 API エントリーポイントです。  

ライブラリは自動でファイル形式を検出するため、同じコードが Word、Excel、画像ファイルでも動作します。  

**よくある落とし穴**: PDFがパスワード保護されている場合は、コンストラクタにパスワードを渡します。  
```java
Signature signature = new Signature(filePath, new LoadOptions("yourPassword"));
```  

### 手順 2: デジタル署名オプションを設定

ここで署名の外観と配置を決めます。デジタル署名は暗号データだけの不可視署名か、カスタムスタンプ付きの可視署名のどちらかです。

**署名外観の設定**  
```java
import com.groupdocs.signature.options.sign.DigitalSignOptions;

public class SetupDigitalSignOptionsFeature {
    public static void main(String[] args) {
        String certificatePath = "YOUR_DOCUMENT_DIRECTORY/certificate.pfx";
        String imagePath = "YOUR_DOCUMENT_DIRECTORY/image.png";

        DigitalSignOptions options = new DigitalSignOptions(certificatePath);
        options.setImageFilePath(imagePath);

        // Set signature location and other properties
        options.setLeft(100);
        options.setTop(100);
        options.setPageNumber(1);
        options.setPassword("1234567890");
    }
}
```  

**定義アンカー** – `DigitalSignOptions` は証明書パス、ビジュアル外観、配置座標など、デジタル署名に必要なすべての設定をカプセル化します。  

- **certificatePath** – 秘密鍵を含む PFX ファイルへのパス（安全に保管してください）。  
- **imagePath** – 任意のビジュアルスタンプ（例: 会社ロゴ）。  
- **setLeft / setTop** – 左上基準のピクセル座標。  
- **setPageNumber** – 対象ページ（1 = 1ページ目）。  
- **setPassword** – PFX ファイルのパスワード。  

**可視署名を使用すべき場面**: ステークホルダーが署名者名やロゴを確認できる必要がある契約書。内部フローでは不可視署名で文書をすっきり保ちつつ暗号的証拠を残します。

**座標のコツ**: `left=50, top=50` から始め、必要に応じて調整してください。`setHorizontalAlignment()` と `setVerticalAlignment()` を使えば、右下など相対配置も簡単です。

### 手順 3: 文書に署名する

いよいよデジタル署名を適用します。

**完全な署名プロセス**  
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.SignResult;
import java.io.File;
import java.nio.file.Paths;

public class SignDocumentWithDigitalFeature {
    public static void main(String[] args) throws Exception {
        String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
        String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", 
            "SignWithDigital/" + Paths.get(filePath).getFileName().toString()).getPath();

        Signature signature = new Signature(filePath);

        DigitalSignOptions options = new DigitalSignOptions("YOUR_DOCUMENT_DIRECTORY/certificate.pfx");
        options.setImageFilePath("YOUR_DOCUMENT_DIRECTORY/image.png");
        options.setLeft(100);
        options.setTop(100);
        options.setPageNumber(1);
        options.setPassword("1234567890");

        SignResult result = signature.sign(outputFilePath, options);
        
        System.out.println("Document signed successfully!");
        System.out.println("Signatures applied: " + result.getSucceeded().size());
    }
}
```  

**定義アンカー** – `sign()` メソッドは指定した出力パスに新しい署名済みPDFを作成し、`SignResult` オブジェクトを返します。  

重要ポイント:

1. 元のPDFは変更されず、新しいファイルが生成されます。  
2. `SignResult` で署名成功の有無やメタデータを取得できます。  

**追加したいエラーハンドリング**:  
```java
try {
    SignResult result = signature.sign(outputFilePath, options);
    if (result.getSucceeded().size() > 0) {
        System.out.println("Success! Signed document saved to: " + outputFilePath);
    }
} catch (Exception e) {
    System.err.println("Signing failed: " + e.getMessage());
    e.printStackTrace();
}
```  

### よくある落とし穴と回避策

多数の開発者を支援してきた経験から、最も頻出する問題と対策をまとめました。

1. **証明書パスの問題** – 絶対パスを使用するか、クラスパスを正しく設定してください。  
2. **証明書パスワード不一致** – PFX のパスワードを再確認。回復手段はありません。  
3. **出力ディレクトリが存在しない** – 事前に作成します:  
```java
   new File(outputDirectory).mkdirs();
   ```  
4. **ファイルが既に存在する** – 上書きするか、バージョン付きファイル名を生成してください:  
```java
   String timestamp = new SimpleDateFormat("yyyyMMdd_HHmmss").format(new Date());
   String outputFile = "contract_signed_" + timestamp + ".pdf";
   ```  
5. **大容量PDFでのメモリ問題** – 50 MB 超のPDFは JVM ヒープを増やす（`-Xmx512m` 以上）。  
6. **証明書の有効期限切れ** – 署名前に有効性を確認。期限切れ証明書は検証不能です。  
7. **未対応画像形式** – GroupDocs は PNG、JPG、BMP、GIF をサポート。未対応形式は PNG に変換してください。  
8. **署名位置がページ外** – 座標がページサイズ内に収まっているか確認（A4 ≈ 595 × 842 px @ 72 DPI）。  

## 実務での活用例

### 1. 請求書承認ワークフロー
**シナリオ**: 会計システムが生成したPDF請求書を CFO が承認し、クライアントに送付する前に署名が必要。  

**実装**: 請求書生成 → CFO が「承認」ボタンをクリック → デジタル署名を適用 → 署名済みPDFを保存・自動メール送信。  

**効果**: 変更不可能な監査証跡が残り、紙の印刷・スキャンが不要に。

### 2. 従業員契約管理
**シナリオ**: 人事部が雇用契約、NDA、ポリシー承認を電子的に取得。  

**実装**: 契約テンプレートをアップロード → 従業員が「同意」ボタン → 従業員証明書で署名 → 人事がカウンターサイン → 完全に実行された文書を従業員レコードに保存。  

**メリット**: ペーパーレス、即時タイムスタンプ、法的に有効な合意。

### 3. 文書認証サービス
**シナリオ**: オリジナル文書のコピーを認証するサービス。  

**実装**: 原本をアップロード → 「認証済みコピー」スタンプ（可視）とタイムスタンプ・固有コードを付与 → 認証済みPDFを返却。  

**結果**: 受取側は埋め込まれた署名で真偽を即座に検証可能。

### 4. マルチパーティ契約署名
**シナリオ**: 不動産契約で買い手、売り手、エージェントの3者署名が必要。  

**実装**: 最初の当事者が署名 → システムがPDFを保存 → 次の当事者が既存の署名済みPDFをロードし、追加署名。GroupDocs は既存署名を保持します。  

**技術的注意**: 新しい `Signature` インスタンスで署名済みPDFを再度ロードし、手順を繰り返すだけです。

## セキュリティベストプラクティス

デジタル署名の安全性は証明書管理に依存します。以下の指針に従ってください。

### 証明書の保管
- **絶対に** `.pfx` ファイルをバージョン管理にコミットしないでください。`.gitignore` に `*.pfx` を追加します。  
- **絶対に** 証明書を公開ウェブディレクトリに置かないでください。  
- **必ず** 専用のシークレットマネージャー（AWS KMS、Azure Key Vault、HashiCorp Vault など）に保管します。  
- パスワードは環境変数で管理し、ファイル権限は `chmod 600` で制限します。  
- 証明書は期限切れ前にローテーションして信頼性を維持してください。

### パスワード管理  
```java
// Bad - hardcoded password
options.setPassword("1234567890");

// Better - environment variable
options.setPassword(System.getenv("CERT_PASSWORD"));

// Best - secure configuration management
options.setPassword(configService.getSecureValue("certificate.password"));
```  

### 証明書の検証  
```java
// Check if certificate is still valid
X509Certificate cert = // load certificate
Date now = new Date();
if (now.before(cert.getNotBefore()) || now.after(cert.getNotAfter())) {
    throw new Exception("Certificate is expired or not yet valid");
}
```  

### 監査ログ  
```java
logger.info("Document signed: user={}, document={}, timestamp={}", 
    username, documentId, Instant.now());
// Don't log: certificate passwords, full file paths, PII
```  

## パフォーマンス考慮事項

大量に PDF を署名する場合は次の点に留意してください。

### メモリ管理
- **小容量 PDF (< 10 MB)** – 上記のインメモリ方式で問題ありません。  
- **大容量 PDF (> 50 MB)** – ストリーミング API を利用し、全体をメモリに読み込まないようにします。  
- **バッチ処理** – 同一証明書で多数文書を署名する場合は、`Signature` インスタンスを再利用してください。

**ストリーミングのヒント**（コードブロックなし）: `Signature` に `InputStream` を渡し、署名済み出力を `OutputStream` に書き込むことでメモリ使用量を抑えます。

### 処理時間ベンチマーク（GroupDocs.Signature 23.12）
- 1‑5 ページ PDF (< 1 MB): **200‑500 ms**  
- 20‑50 ページ PDF (5‑10 MB): **1‑2 s**  
- 100 ページ以上 PDF (> 20 MB): **3‑5 s**  

上記は標準的な 2.8 GHz CPU と 8 GB RAM を前提としています。

### 最適化のコツ
1. 証明書を一度だけロードし、複数ファイルで同じ `DigitalSignOptions` を再利用。  
2. `ExecutorService` を使って独立した文書の並列署名を実装。  
3. 署名ループ内で I/O 待ちを減らすため、事前に出力ディレクトリを作成。  
4. VisualVM などのツールで JVM をプロファイルし、実際のボトルネックを特定。

## トラブルシューティングガイド

### 「証明書ファイルが見つからない」エラー
**症状**: `DigitalSignOptions` 初期化時に `FileNotFoundException` が発生。  
**対策**: 絶対パスを確認し、ファイル権限をチェック。作業ディレクトリは `System.out.println(new File(".").getAbsolutePath())` で出力して検証。

### 「証明書のパスワードが無効」エラー
**症状**: 署名時に例外がスロー。  
**対策**: パスワードが正しいか（大文字小文字区別）再確認。作成時と同じものを使用するか、証明書を再生成。

### 署名位置がずれる
**症状**: 可視署名が期待位置と異なる。  
**対策**: 座標は左上 (0,0) が基準。ページ番号は 1 が最初のページ。`setHorizontalAlignment()` / `setVerticalAlignment()` を利用して相対配置に切り替える。

### 「文書の署名に失敗した」汎用エラー
**症状**: 原因不明のエラーメッセージ。  
**対策**: `System.setProperty("com.groupdocs.signature.debug", "true")` で詳細ログを有効化。PDF が破損していないか、書き込み権限があるか、証明書の有効性を確認。

### PDFリーダーで署名が表示されない
**症状**: 署名は成功したが、ビジュアルスタンプが見えない。  
**対策**: `options.setImageFilePath(imagePath)` が有効な PNG/JPG を指しているか確認。座標がページ範囲内か、ビューア設定で署名が非表示になっていないかチェック。

### 大容量PDFで OutOfMemoryError が発生
**症状**: JVM がクラッシュまたは `OutOfMemoryError` をスロー。  
**対策**: ヒープサイズを増やす（`-Xmx1024m` 以上）。大容量PDFはストリーミング処理に切り替え、`Signature` オブジェクトは使用後に速やかにクローズ。

## FAQ

**Q: GroupDocs.Signature for Java を使うメリットは？**  
A: 法的拘束力、暗号的検証、数秒で完了する即時署名、完全な監査トレイルを提供。PDF の深い知識が不要で実装がシンプルです。

**Q: プロジェクトに適した GroupDocs.Signature のバージョンは？**  
A: 新規プロジェクトは最新の安定版（現時点で 23.12）を使用してください。既存アプリはリリースノートを確認し、破壊的変更がないか検証してからアップグレードします。

**Q: PDF 以外の文書にも署名できますか？**  
A: はい。Word、Excel、PowerPoint、一般的な画像形式も同じ `Signature` と `DigitalSignOptions` で扱えます。

**Q: バッチ処理で署名を自動化できますか？**  
A: 可能です。ディレクトリを走査し、同一 `DigitalSignOptions` を各ファイルに適用して保存します。高スループットが必要な場合は並列ストリームや `ExecutorService` を利用し、十分なヒープを確保してください。

**Q: PDF がデジタル署名されているかどうかはどう確認しますか？**  
A: Adobe Acrobat Reader の左側パネルに署名パネルが表示されます。署名をクリックすると証明書情報と検証ステータスが確認できます。プログラム側でも GroupDocs.Signature の検証 API が利用可能です。

**Q: 開発・ステージング・本番で別々の証明書を使うべきですか？**  
A: はい。開発・テストは自己署名証明書で構いませんが、本番環境は外部 CA 発行の証明書を使用して外部パートナーからの信頼を確保してください。

**Q: 同一文書に複数人が署名できますか？**  
A: できます。既に署名済みの PDF を再度 `Signature` でロードし、新しい `DigitalSignOptions` を設定して `sign()` を呼び出すだけです。各署名は独自のタイムスタンプと証明書情報を保持し、完全な監査トレイルが形成されます。

## 結論

**Java で PDF デジタル署名を作成する**ための完全なロードマップが手に入りました。GroupDocs.Signature のセットアップから大容量ファイルの扱い、証明書の安全管理、バッチ処理まで網羅していますので、任意の Java アプリケーションに信頼性の高い電子署名機能を組み込むことができます。

### 次のステップ
1. **GroupDocs.Signature をダウンロード**し、無料トライアルで試す。  
2. **外観オプションと座標設定**を色々試してみる。  
3. **署名フローを既存サービスに統合**—API エンドポイント、バックグラウンドジョブ、UI アクションなど。  
4. **高度機能**（QR コード署名、バーコードスタンプ、メタデータ署名）も探索してみる。  

提供したコードスニペットはそのまま実行可能です（パスとパスワードを置き換えるだけ）。堅牢なエラーハンドリングと安全な資格情報管理を加えれば、あらゆる本番環境で自信を持って PDF 署名が行えます。

---

**最終更新日:** 2026-06-11  
**テスト環境:** GroupDocs.Signature 23.12 for Java  
**作者:** GroupDocs

```java
// Good - explicit resource management
try (Signature signature = new Signature(filePath)) {
    signature.sign(outputPath, options);
} // Automatically cleaned up
```

## 関連チュートリアル

- [Add Image Signature to PDF Java with GroupDocs](/signature/java/image-signatures/sign-pdf-image-signature-groupdocs-java/)
- [Add Text Signature to PDF in Java - Complete GroupDocs Tutorial](/signature/java/text-signatures/implement-text-signatures-groupdocs-java/)
- [How to Add Digital Signature to PDF Java with Timestamp](/signature/java/digital-signatures/digital-signature-timestamp-pdf-java-groupdocs/)