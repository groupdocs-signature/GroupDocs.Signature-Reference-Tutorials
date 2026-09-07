---
categories:
- Java Development
date: '2026-06-11'
description: GroupDocs.Signature を使用して Java で PDF に署名する方法を学び、digital signature と timestamp
  を追加します。コード例とベストプラクティスを含むステップバイステップガイドです。
keywords:
- how to sign pdf
- add digital signature pdf
- timestamp pdf signature
- java pdf signature library
- groupdocs signature java
lastmod: '2026-06-11'
linktitle: JavaでPDFにDigital Signatureを追加
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to sign PDF with Java using GroupDocs.Signature, add digital
    signature and timestamp. Step-by-step guide with code examples and best practices.
  headline: 'How to Sign PDF with Java: Add Digital Signature and Timestamp'
  type: TechArticle
- description: Learn how to sign PDF with Java using GroupDocs.Signature, add digital
    signature and timestamp. Step-by-step guide with code examples and best practices.
  name: 'How to Sign PDF with Java: Add Digital Signature and Timestamp'
  steps:
  - name: Import Required Classes
    text: The following imports give you access to signature configuration, positioning,
      and timestamp functionality.
  - name: Define Your File Paths
    text: Set up paths for your input PDF, certificate, and where you want the signed
      PDF saved. Keep the certificate file secure; it contains your private key.
  - name: Initialize the Signature Object
    text: Create a `Signature` instance pointing to the PDF you want to sign. This
      loads the PDF into memory and prepares it for signing.
  - name: Configure Signature Properties and Timestamp
    text: The `DigitalSignature` class represents the cryptographic seal that will
      be embedded in the PDF. You can also attach a timestamp from a trusted authority.
      * **ContactInfo** – e.g., `john.doe@company.com` * **Location** – e.g., `New
      York Office` * **Reason** – e.g., `Contract Approval` We use FreeTSA
  - name: Configure Digital Sign Options
    text: The `SignOptions` class ties together the certificate, signature properties,
      and visual placement. Alignment enums control where the signature appears.
  - name: Sign and Save the Document
    text: Execute the signing process and write the signed PDF to disk. The returned
      `SignResult` object tells you whether the operation succeeded and lists any
      warnings.
  type: HowTo
- questions:
  - answer: A digital signature uses cryptographic algorithms to verify identity and
      detect tampering, while an electronic signature can be as simple as a typed
      name.
    question: What's the difference between a digital signature and an electronic
      signature?
  - answer: Only for the timestamp service; the cryptographic signing itself runs
      locally.
    question: Do I need internet connectivity to sign PDFs?
  - answer: Any modification breaks the signature, and PDF viewers will display a
      warning indicating the document has been altered.
    question: Can signed PDFs be edited later?
  - answer: Most PDF readers verify automatically; programmatically, use GroupDocs.Signature's
      verification API to check status, signer details, and timestamp validity.
    question: How do I verify a signed PDF?
  - answer: The embedded timestamp proves the signature was created while the certificate
      was still valid, preserving legal standing.
    question: What happens if my certificate expires after I've signed documents?
  type: FAQPage
tags:
- pdf-signing
- digital-signatures
- java-security
- groupdocs
title: JavaでPDFに署名する方法：Digital Signature と Timestamp を追加
type: docs
url: /ja/java/digital-signatures/digital-signature-timestamp-pdf-java-groupdocs/
weight: 1
---

# Java とタイムスタンプで PDF に署名する方法

重要な文書を送った後に、後から改ざんされる可能性を心配したことはありませんか？ あなたは一人ではありません。エンタープライズ文書管理システムを構築する場合でも、契約署名プラットフォームを作成する場合でも、プログラムで PDF ファイルを保護する必要がある場合でも、**how to sign PDF** に信頼できるタイムスタンプを付与することが解決策です。デジタル署名を追加すると、誰がファイルに署名したかを証明できるだけでなく、署名が行われた*正確な*時刻の不変の記録が作成されます。

## クイック回答
- **Java で PDF 署名を簡素化するライブラリは何ですか？** GroupDocs.Signature for Java.  
- **インターネット接続は必要ですか？** タイムスタンプ認証局のためだけに必要です；署名自体はオフラインで行われます。  
- **テスト用に自己署名証明書を使用できますか？** はい、`keytool` で生成できます。  
- **サイズ制限はありますか？** ライブラリはメモリに全体を読み込まずに 500 MB までの PDF に署名できます。  
- **GroupDocs がサポートするフォーマットは何種類ですか？** DOCX、XLSX、PPTX、HTML、画像など、50 以上の入力・出力フォーマットに対応しています。

## デジタル署名が重要な理由（タイムスタンプが必要な理由）

PDF を読み込み、暗号的なシールを適用し、信頼できるタイムスタンプを埋め込む—この二段階プロセスにより、認証、完全性、否認防止が保証されます。タイムスタンプは、署名証明書が後で失効または取り消された場合でも、署名が特定の瞬間に存在したことを証明します。

## Java で PDF に署名する方法は？

`new Signature("input.pdf")` で PDF を読み込み、`DigitalSignature` オブジェクトを構成し、信頼できる認証局からタイムスタンプを付与し、`sign()` を呼び出すだけで、数行のコードで完了します。GroupDocs.Signature は証明書の解析、ハッシュ計算、タイムスタンプ取得を自動で処理するため、暗号化の詳細に時間を取らずにビジネスロジックに集中できます。

## GroupDocs.Signature for Java のセットアップ

### 統合方法

使用しているビルドツールを選んでください：

**Maven ユーザー向け:**  
`pom.xml` に次の依存関係を追加します:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle ユーザー向け:**  
`build.gradle` に次を追加します:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**直接ダウンロード (希望する場合):**  
[GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) にアクセスして JAR ファイルをダウンロードします。プロジェクトのクラスパスに手動で追加してください。詳細な API リファレンスは [GroupDocs.Signature Documentation](https://docs.groupdocs.com/signature/java/) を参照してください。最新ビルドは [Latest Version & Releases](https://releases.groupdocs.com/signature/java/) で確認できます。

プロのヒント: 可能であれば Maven または Gradle を使用してください。依存関係の管理とアップデートが格段に楽になります。

### ライセンス取得方法

GroupDocs ではプロジェクトの段階に応じていくつかのオプションがあります:

1. **Free Trial** – 評価に最適です。[Download Trial Version](https://releases.groupdocs.com/signature/java/) で全機能をテストできます。  
2. **Temporary License** – 試用版の透かしなしで開発にフルアクセスしたいですか？ 30 日間の一時ライセンスを取得してください。  
3. **Commercial License** – 本番環境で使用する場合は、[Buy License](https://purchase.groupdocs.com/buy) から購入してください。価格は導入形態により変わります。

サポートが必要ですか？ [GroupDocs Forum](https://forum.groupdocs.com/c/signature/) をご利用ください。

### 基本的な初期化

`Signature` クラスは GroupDocs.Signature の最上位オブジェクトで、メモリ内の単一 PDF ファイルを表します。インスタンス化後、すべての読み書き操作はこのオブジェクトを通じて行われます。

```java
import com.groupdocs.signature.Signature;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
final Signature signature = new Signature(filePath);
```

シンプルですね。PDF ファイルを指すだけで、すぐに使用できます。`Signature` オブジェクトはすべての署名操作の主要インターフェイスです。

## PDF にデジタル署名を追加する Java 手順：ステップバイステップ

PDF を読み込み、署名の詳細を設定し、タイムスタンプを付与し、署名済み文書を保存するまでの流れが明確に示されています。

### ステップ 1: 必要なクラスをインポート

署名設定、位置指定、タイムスタンプ機能にアクセスするためのインポートです。

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.PdfDigitalSignature;
import com.groupdocs.signature.domain.structs.TimeStamp;
import com.groupdocs.signature.options.sign.DigitalSignOptions;
```

### ステップ 2: ファイルパスを定義

入力 PDF、証明書、および署名済み PDF の保存先パスを設定します。証明書ファイルはプライベートキーを含むため、必ず安全に保管してください。

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
String certificatePath = "YOUR_DOCUMENT_DIRECTORY/certificate.pfx";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/digitallySignedTimeStamp.pdf";
```

### ステップ 3: Signature オブジェクトを初期化

署名したい PDF を指す `Signature` インスタンスを作成します。これにより PDF がメモリに読み込まれ、署名の準備が整います。

```java
final Signature signature = new Signature(filePath);
```

### ステップ 4: 署名プロパティとタイムスタンプを設定

`DigitalSignature` クラスは PDF に埋め込まれる暗号的シールを表します。信頼できる認証局からタイムスタンプを付与することもできます。

```java
PdfDigitalSignature pdfDigitalSignature = new PdfDigitalSignature();
pdfDigitalSignature.setContactInfo("Contact Information");
pdfDigitalSignature.setLocation("Location Info");
pdfDigitalSignature.setReason("Signing Reason");

// Configure the TimeStamp with URL, User Id, and Password
TimeStamp timeStamp = new TimeStamp("https://freetsa.org/tsr", "User Id", "Password");
pdfDigitalSignature.setTimeStamp(timeStamp);
```

* **ContactInfo** – 例: `john.doe@company.com`  
* **Location** – 例: `New York Office`  
* **Reason** – 例: `Contract Approval`  

デモ用に FreeTSA（無料のタイムスタンプ認証局）を使用しています。実運用では、稼働率と法的効力が保証された商用 TSA を選択してください。

### ステップ 5: デジタル署名オプションを設定

`SignOptions` クラスは証明書、署名プロパティ、視覚的配置を結び付けます。Alignment 列挙型で署名の表示位置を制御します。

```java
DigitalSignOptions options = new DigitalSignOptions(certificatePath);
options.setPassword("YourCertificatePassword"); // Certificate password
options.setSignature(pdfDigitalSignature); // Attach the PdfDigitalSignature object

// Specify signature alignment (where it appears on the page)
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
```

### ステップ 6: 文書に署名して保存

署名プロセスを実行し、署名済み PDF をディスクに書き出します。返される `SignResult` オブジェクトは操作の成功可否と警告情報を提供します。

```java
try {
    SignResult signResult = signature.sign(outputFilePath, options);
    System.out.println("Document signed successfully!");
    System.out.println("Output: " + outputFilePath);
} catch (Exception e) {
    throw new RuntimeException("Error during signing process: " + e.getMessage());
}
```

## 避けるべき一般的な落とし穴

### 1. 証明書の問題
**Problem:** “Invalid certificate” エラー。  
**Fix:** `keytool -list -v -keystore your.pfx` でパスワードを確認してください。

```bash
keytool -list -v -keystore certificate.pfx -storetype PKCS12
```

### 2. タイムスタンプサービスのタイムアウト
**Problem:** TSA への接続でネットワークタイムアウトが発生。  
**Fix:** 接続性をテスト (`curl -I https://freetsa.org/tsr`) し、リトライロジックを追加するか、フォールバック TSA を設定してください。

```java
new File(outputFilePath).getParentFile().mkdirs();
```

### 3. ファイル権限の問題
**Problem:** 保存時に “Access denied”。  
**Fix:** 出力ディレクトリが存在し、アプリケーションに書き込み権限があることを確認してください。

```bash
keytool -genkeypair -alias mykey -keyalg RSA -keysize 2048 -storetype PKCS12 -keystore certificate.pfx -validity 365
```

### 4. 大きな PDF のメモリ問題
**Problem:** 大容量ファイルで `OutOfMemoryError` が発生。  
**Fix:** JVM ヒープを増やす (`-Xmx4g`) か、ファイルをバッチ処理してください。

### 5. 署名位置が間違っている
**Problem:** 署名が既存コンテンツと重なる。  
**Fix:** まず配置設定をテストし、ピクセル単位で正確に配置したい場合は座標ベースのオプションを使用してください。

## 証明書管理のヒント

### 開発用証明書の取得
テスト目的で Java の `keytool` を使用して自己署名証明書を生成します。

```java
   String certPassword = System.getenv("CERT_PASSWORD");
   ```

### 証明書のベストプラクティス
1. **パスワードをハードコードしない** – 環境変数を使用してください。  
2. **証明書は期限切れ前にローテーション** してください。  
3. **高セキュリティアプリでは HSM に秘密鍵を保管** してください。  
4. **証明書は保護された場所にバックアップ** してください。  
5. **署名前に証明書を検証** し、期限切れや失効を検出してください。

## セキュリティのベストプラクティス

### 1. 秘密鍵を保護
証明書はプロジェクトディレクトリ外に保存し、環境固有の設定を使用し、エンタープライズ導入では HSM の利用を検討してください。

### 2. 入力 PDF を検証
破損、既存署名、サイズ上限、コンテンツの適合性をチェックしてから署名してください。

### 3. 監査ログを実装
署名操作ごとにタイムスタンプ、ユーザー、文書名、ステータスを記録します。

```java
try {
    SignResult result = signature.sign(outputFilePath, options);
    logger.info("Document signed: " + filePath + " by " + signerEmail);
} catch (Exception e) {
    logger.error("Signing failed: " + filePath + " - " + e.getMessage());
    // Handle appropriately
}
```

### 4. 信頼できるタイムスタンプ認証局を使用
ローカルのシステム時刻に依存せず、RFC 3161 準拠の TSA から必ずタイムスタンプを取得してください。

### 5. エラーハンドリングを実装
例外を捕捉し、機密情報を漏らさないように処理してください。

```java
try {
    signature.sign(outputFilePath, options);
} catch (Exception e) {
    // Log detailed error internally
    logger.error("Signing error: " + e.getMessage(), e);
    // Return generic error to client
    throw new ApplicationException("Unable to sign document. Please try again.");
}
```

## 実際のユースケースとアプリケーション

### 1. 契約管理システム
従業員が NDA や契約書に電子署名し、タイムスタンプで正確な受諾時刻を証明します。

### 2. 金融文書処理
請求書や発注書をバッチ署名し、規制当局向けに不変の監査トレイルを提供します。

### 3. 教育資格の検証
大学が改ざん防止の成績証明書を発行し、QR コードリンクで即時検証が可能です。

### 4. ソフトウェアライセンス管理
デジタル署名とタイムスタンプ付きのライセンス証明書を生成し、偽造を防止します。

### 5. 規制コンプライアンス（FDA 21 CFR Part 11 など）
医療機器メーカーが SOP や検証レポートに署名し、タイムスタンプで否認防止要件を満たします。

## パフォーマンスの考慮事項と最適化

### メモリ管理
大容量 PDF はバッチで処理し、`Signature` オブジェクトは速やかにクローズし、必要に応じてヒープサイズを増やしてください。

### タイムスタンプのネットワーク最適化
HTTP 接続をプールし、指数バックオフリトライを実装し、連続署名時にはタイムスタンプをキャッシュしてください。

### バッチ処理のベストプラクティス
```java
// Pseudo‑code: process a list of PDFs in parallel, limiting to 5 concurrent TSA calls
```
*スレッドを過剰に生成しないでください；5〜10 の同時署名がスループットと TSA の負荷のバランスを取ります。*

### ディスク I/O の最適化
一時ファイルは SSD に保存し、読み書き回数を最小限に抑え、署名実行後は一時アーティファクトをクリーンアップしてください。

## トラブルシューティングガイド

### エラー: “Invalid Certificate Password”
**Solution:** `keytool -list -keystore your.pfx` でパスワードを確認してください。

```java
ExecutorService executor = Executors.newFixedThreadPool(5);
List<Future<SignResult>> futures = new ArrayList<>();

for (String pdfPath : pdfPaths) {
    futures.add(executor.submit(() -> {
        try (Signature sig = new Signature(pdfPath)) {
            return sig.sign(outputPath, options);
        }
    }));
}

// Wait for all to complete
for (Future<SignResult> future : futures) {
    SignResult result = future.get();
    // Process result
}

executor.shutdown();
```

### エラー: “Timestamp Authority Not Responding”
**Solution:** TSA の URL をテストし、ファイアウォール規則を確認し、フォールバック TSA ロジックを追加してください。

```bash
keytool -list -v -keystore certificate.pfx -storetype PKCS12
```

### エラー: “PDF is Already Signed”
既に署名された PDF を検出したら、カウンター署名を追加するか、未署名のコピーで再度署名してください。

### エラー: “Access Denied” When Saving
出力ディレクトリが存在し、アプリに書き込み権限があり、他プロセスがファイルをロックしていないことを確認してください。

```java
TimeStamp timeStamp;
try {
    timeStamp = new TimeStamp("https://freetsa.org/tsr", "", "");
} catch (Exception e) {
    // Fallback to alternative TSA
    timeStamp = new TimeStamp("https://alternate-tsa.com/tsr", "", "");
}
```

### エラー: OutOfMemoryError
JVM ヒープを増やすか、PDF を小さなバッチに分割して処理するか、非常に大きなファイル向けにストリーミング API に切り替えてください。

## 結論と次のステップ

**how to sign PDF** の方法、信頼できるタイムスタンプの付与、一般的な落とし穴への対処を学びました。次のステップとして、以下を検討してください：

1. 複数署名フィールドを追加し、マルチパーティ合意に対応。  
2. GroupDocs.Signature の検証 API を使用してプログラムで署名を検証。  
3. 署名の外観（画像、テキスト、配置）をカスタマイズ。  
4. キューイングとモニタリングを組み込んだ堅牢なバッチ署名サービスを構築。

## よくある質問

**Q: デジタル署名と電子署名の違いは何ですか？**  
A: デジタル署名は暗号アルゴリズムを使用して本人確認と改ざん検出を行うのに対し、電子署名は単に名前を入力するなどシンプルな形式でも構いません。

**Q: PDF に署名するためにインターネット接続は必要ですか？**  
A: タイムスタンプサービスのためだけに必要です；暗号署名自体はローカルで実行されます。

**Q: 署名済み PDF は後で編集できますか？**  
A: いかなる変更も署名を破壊し、PDF ビューアは文書が変更されたことを警告します。

**Q: 署名済み PDF をどうやって検証しますか？**  
A: 多くの PDF リーダーは自動的に検証します。プログラムで検証する場合は、GroupDocs.Signature の検証 API を使用してステータス、署名者情報、タイムスタンプの有効性を確認してください。

**Q: 証明書が期限切れになった後に署名した文書はどうなりますか？**  
A: 埋め込まれたタイムスタンプにより、署名が証明書の有効期間内に作成されたことが証明され、法的効力が保たれます。

**Q: これをクラウドストレージ（S3、Azure Blob など）で使用できますか？**  
A: はい。PDF を一時的にダウンロードし、署名後に再度クラウドへアップロードしてください。

**Q: ファイルサイズの上限はありますか？**  
A: ライブラリはメモリに全体を読み込まずに最大 500 MB の PDF を処理できます。より大きなファイルはストリーミングが必要になる場合があります。

**Q: 商用利用時の GroupDocs.Signature の費用はどれくらいですか？**  
A: 導入形態により価格が変動します。最新の料金は GroupDocs の営業担当までお問い合わせください。評価版や一時ライセンスも利用可能です。

**Q: Linux サーバーでも動作しますか？**  
A: 完全にプラットフォームに依存せず、JRE があればどの OS でも動作します。

**最終更新日:** 2026-06-11  
**テスト環境:** GroupDocs.Signature 23.9 for Java  
**作者:** GroupDocs

```java
File outputFile = new File(outputFilePath);
outputFile.getParentFile().mkdirs(); // Create directories if needed

if (!outputFile.canWrite() && outputFile.exists()) {
    throw new IOException("Cannot write to " + outputFilePath);
}
```

## 関連チュートリアル

- [Java でデジタル証明書を検証する方法 - コード例付き完全ガイド](/signature/java/digital-signatures/java-certificate-verification-groupdocs-signature/)
- [Java で GroupDocs.Signature を使用してプログラム的に PDF に署名する方法](/signature/java/digital-signatures/sign-pdfs-groupdocs-signature-java/)
- [GroupDocs を使用した Java の PDF への画像署名の追加](/signature/java/image-signatures/sign-pdf-image-signature-groupdocs-java/)