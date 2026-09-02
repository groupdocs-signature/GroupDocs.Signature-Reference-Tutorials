---
categories:
- Java Development
date: '2026-06-11'
description: Javaを使用してPDFや文書にDigital Signaturesを追加する方法を学びます。code examples、troubleshooting
  tips、security best practicesを含む完全ガイドです。
keywords:
- add digital signature java
- implement digital signatures java
- java document signing library
- groupdocs signature java
- digital certificate handling java
lastmod: '2025-01-02'
linktitle: JavaのDigital Signatures
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to add digital signatures to PDF and documents using Java.
    Complete guide with code examples, troubleshooting tips, and security best practices.
  headline: How to Add Digital Signatures to Documents in Java
  type: TechArticle
- description: Learn how to add digital signatures to PDF and documents using Java.
    Complete guide with code examples, troubleshooting tips, and security best practices.
  name: How to Add Digital Signatures to Documents in Java
  steps:
  - name: '**Incorrect password** – verify with OpenSSL: `openssl pkcs12 -info -in
      yourcert.pfx`.'
    text: '**Incorrect password** – verify with OpenSSL: `openssl pkcs12 -info -in
      yourcert.pfx`.'
  - name: '**Expired certificate** – check the validity using `keytool -list -v -keystore
      yourcert.pfx`.'
    text: '**Expired certificate** – check the validity using `keytool -list -v -keystore
      yourcert.pfx`.'
  - name: '**Wrong file format** – only `.pfx` or `.p12` (which contain private keys)
      are accepted.'
    text: '**Wrong file format** – only `.pfx` or `.p12` (which contain private keys)
      are accepted.'
  - name: '**File permission problems** – ensure the Java process can read the certificate
      file.'
    text: '**File permission problems** – ensure the Java process can read the certificate
      file.'
  - name: Store `.pfx` files in a secure vault (AWS Secrets Manager, Azure Key Vault,
      or HashiCorp Vault).
    text: Store `.pfx` files in a secure vault (AWS Secrets Manager, Azure Key Vault,
      or HashiCorp Vault).
  - name: Load the password at runtime from environment variables or the vault’s API.
    text: Load the password at runtime from environment variables or the vault’s API.
  - name: Restrict file system permissions so only the service account can read the
      certificate.
    text: Restrict file system permissions so only the service account can read the
      certificate.
  - name: Rotate certificates at least 30 days before expiration and update the stored
      secret accordingly.
    text: Rotate certificates at least 30 days before expiration and update the stored
      secret accordingly.
  - name: '**Automated Contract Workflows** – When a contract reaches the “approved”
      state in your BPM system, trigger the signing service to embed the legal department’s
      certificate and email the signed copy to the vendor.'
    text: '**Automated Contract Workflows** – When a contract reaches the “approved”
      state in your BPM system, trigger the signing service to embed the legal department’s
      certificate and email the signed copy to the vendor.'
  - name: '**Invoice Approval Systems** – After finance signs off an invoice, automatically
      add a digital signature before sending it to the customer, providing cryptographic
      proof of authenticity.'
    text: '**Invoice Approval Systems** – After finance signs off an invoice, automatically
      add a digital signature before sending it to the customer, providing cryptographic
      proof of authenticity.'
  type: HowTo
- questions:
  - answer: iText focuses solely on PDF and requires you to handle low‑level cryptography
      yourself, while GroupDocs.Signature supports 30+ formats, offers ready‑made
      visual stamps, and abstracts certificate handling, reducing development time
      dramatically.
    question: What’s the main difference between GroupDocs.Signature and iText for
      PDF signing?
  - answer: Yes. Add the Maven dependency, create a `@Service` bean that wraps the
      signing logic, and inject it wherever you need to sign documents. This keeps
      your controllers thin and your signing code reusable.
    question: Can I integrate GroupDocs.Signature into a Spring Boot microservice?
  - answer: The library uses standard PKI algorithms (RSA/ECDSA) and follows the same
      specifications as browsers and Adobe Reader. Security depends on the quality
      of your certificate; always use a CA‑issued certificate and protect the private
      key.
    question: How secure are signatures created with GroupDocs.Signature?
  - answer: Absolutely. As long as the signing certificate is trusted, Adobe Reader,
      Foxit, and modern browsers will validate the signature correctly. Self‑signed
      certificates will display a warning but remain technically valid.
    question: Will signed documents work across different PDF readers?
  - answer: Yes—simply omit the `ImageFilePath` and set size parameters to zero. The
      resulting signature is invisible but still cryptographically sound, perfect
      for backend automation where visual cues aren’t required.
    question: Is it possible to sign documents without a visible signature image?
  type: FAQPage
tags:
- digital-signatures
- document-security
- java-libraries
- pdf-signing
title: Javaで文書にDigital Signaturesを追加する方法
type: docs
url: /ja/java/digital-signatures/groupdocs-signature-java-digital-signing-guide/
weight: 1
---

# Javaでドキュメントにデジタル署名を追加する方法

## はじめに

**add digital signature java** 機能の実装は、地雷原を歩くように感じられることがあります。証明書形式、署名の配置、厳格なセキュリティポリシーをすべて扱いながら、ユーザーエクスペリエンスをスムーズに保たなければなりません。一歩間違えると、無効な署名や Adobe Reader で検証に失敗するドキュメントになってしまいます。

幸いなことに、車輪を再発明したり低レベルの暗号処理に格闘したりする必要はありません。契約管理ポータル、署名付き領収書が必要な e コマースのチェックアウト、社内 HR ワークフローなど、信頼できる Java ライブラリを使用すれば、開発時間を数時間短縮し、一般的な落とし穴を回避できます。

本ガイドでは、デジタル署名の重い作業を抽象化した商用ライブラリ **GroupDocs.Signature for Java** を実際に使いながら解説します。以下を学びます。

* ライブラリのセットアップと証明書の正しい設定方法  
* PDF、Word、Excel、PowerPoint ファイルにプロフェッショナルなビジュアルスタンプで署名する方法  
* 署名の検証と、信頼できない証明書やメモリ不足などの一般的なエラー処理  
* 本番環境向けのベストプラクティスなセキュリティ対策  

最後まで読めば、任意のドキュメントタイプに拡張可能な、すぐに使える実装が手に入ります。

## クイック回答
- **Java でデジタル署名を追加できるライブラリは？** GroupDocs.Signature for Java。  
- **対応フォーマット数は？** 30 以上、PDF、DOCX、XLSX、PPTX、画像ファイルなど。  
- **本番環境でライセンスは必要？** はい。商用ライセンスで透かしが除去され、全機能が利用可能になります。  
- **100 ページ超の大容量 PDF でも OOM エラーなしで署名できる？** はい。JVM ヒープを調整し、`setAllPages(false)` オプションを使用すれば OK。  
- **タイムスタンプはサポートされている？** もちろん。信頼できるタイムスタンプ認証局（TSA）トークンを付与して長期有効性を確保できます。

## add digital signature java とは？
`add digital signature java` は、Java API を使用してデジタルドキュメントに暗号署名を埋め込むプログラム的プロセスを指します。署名はデジタル証明書で検証された署名者の身元をドキュメントの内容に結び付け、完全性、否認防止、法的強制力をプラットフォーム間で保証します。

## なぜ Java でデジタル署名を実装するのか？
GroupDocs.Signature は **30 以上の入出力フォーマット** をサポートし、**500 MB** までのファイルをメモリ全体に読み込まずに処理できます。手作業の PDFBox 実装に比べて **2‑5 倍の速度向上** を実現し、高頻度の取引や大規模ワークロードでのトランザクション時間短縮とサーバーコスト削減につながります。

## 前提条件

開始前に以下を確認してください。

* **Java Development Kit (JDK) 8+** – 推奨は TLS 強化がある JDK 11。  
* **IDE** – IntelliJ IDEA、Eclipse、または Java 拡張付き VS Code。  
* **GroupDocs.Signature for Java** – ビルドへの追加方法を 3 通り紹介します。  
* **有効なデジタル証明書**（**PFX** または **P12** 形式、プライベートキーとパスワードが必要）。  

任意だがあると便利：

* **Maven** または **Gradle** による依存管理の知識。  
* テスト用の PDF、DOCX、XLSX ファイル。

## GroupDocs.Signature for Java のインストール方法

GroupDocs.Signature はビルド設定にシンプルに追加できます。使用しているビルドツールに合わせたスニペットを選び、プレースホルダーのバージョンを最新の安定版に置き換えてビルドコマンドを実行し、Maven Central からライブラリを取得してください。

**Maven（pom.xml に追加）：**  
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```  

**Gradle（build.gradle に追加）：**  
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```  

**手動インストール（ビルドツール未使用の場合）：**  
公式リリースページ — [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) — から JAR をダウンロードし、クラスパスに追加します。

> **プロのコツ:** 常に最新の安定版を参照してください。執筆時点ではバージョン 23.12 が最新ですが、以降のリリースにはセキュリティパッチやパフォーマンス改善が含まれることが多いです。

## GroupDocs ライセンスの取得と適用方法

本番利用にはライセンスが必須です。ライセンスがないと透かしが表示され、エンタープライズポリシーに準拠しません。

* **無料トライアル:** [Temporary License Page](https://purchase.groupdocs.com/temporary-license/) で 30 日間の一時ライセンスを取得。  
* **有料ライセンス:** [GroupDocs Purchase Page](https://purchase.groupdocs.com/buy) から開発者またはエンタープライズ向けライセンスを購入。

有効なライセンスがない場合、署名済みドキュメントに目に見える透かしが付加され、評価目的にしか利用できません。

## Signature オブジェクトの初期化方法

`Signature` クラスはすべてのドキュメント操作のエントリーポイントです。メモリ上の単一ファイルを表し、署名、検証、署名抽出のメソッドを提供します。`Signature` インスタンスを作成すると対象ファイルがロードされ、以降の処理が可能になります。

```java
Signature signature = new Signature("path/to/input.pdf");
```

**何が起きているか？**  
この行は対象ドキュメントをロードする `Signature` インスタンスを生成します。パスは絶対でも相対でも構いませんが、ファイルが存在することを確認してください。このオブジェクトは複数の署名や検証に再利用でき、バッチ処理のオーバーヘッドを削減します。

## デジタル署名オプションの設定方法

デジタル署名オプションは、PKI 署名を生成するために必要なすべての設定（証明書情報、ビジュアル外観、配置ルール）をカプセル化します。正しい設定により、暗号的に正当でありながらドキュメントタイプに適した見た目の署名が得られます。

### 証明書情報の設定方法

`DigitalSignOptions` クラスは証明書関連設定をすべて保持します。以下はこのクラスの初回定義例です。

`DigitalSignOptions` は暗号パラメータ（証明書ファイル、パスワード、任意のメタデータ）を定義し、ライブラリが有効な PKI 署名を作成できるようにします。

```java
DigitalSignOptions options = new DigitalSignOptions();
options.setCertificatePath("YOUR_DOCUMENT_DIRECTORY/certificate.pfx");
options.setCertificatePassword("yourPassword");
options.setReason("Approved Contract");
options.setContact("legal@yourcompany.com");
options.setLocation("New York, USA");
```

**重要ポイント:**  
* パスワードはハードコードしないで、環境変数やシークレットマネージャから取得してください。  
* `setReason`, `setContact`, `setLocation` を使用して、署名プロパティ閲覧時にレビューアへコンテキスト情報を提供します。

### 署名のビジュアル外観をカスタマイズする方法

`SignatureOptions`（`DigitalSignOptions` のサブクラス）はページ上の描画を制御します。画像の添付、サイズ調整、ページ上のスタンプ位置を設定できます。

`SignatureOptions` は画像を添付し、サイズを調整し、ページ上のビジュアルスタンプを配置します。

```java
options.setImageFilePath("YOUR_DOCUMENT_DIRECTORY/signature.png");
options.setAllPages(true);
options.setWidth(150);
options.setHeight(0); // Auto‑scale based on image aspect ratio
```

* **ImageFilePath:** 手書き署名や企業ロゴの PNG/JPG を指定。透過 PNG が最適です。  
* **AllPages:** 契約書全体に証明が必要な場合は `true`、最後のページだけにする場合は `false`。  
* **Width/Height:** ピクセル単位。高さ **50‑80** ピクセルが多くのビジネス文書でプロフェッショナルに見えます。

## 配置と余白の制御方法

配置設定はスタンプがページ上のどこに配置されるかを決め、余白はビジュアル要素がページ端に接触しないようバッファを提供します。適切な配置は可読性を向上させ、既存コンテンツへの干渉を防ぎます。

`AlignmentOptions` は `Bottom`, `Right`, `Top`, `Center` などの垂直・水平配置定数を提供します。

```java
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
options.setPadding(10);
```

* **Padding:** スタンプ周囲の余白を追加。**10** ピクセル程度で画像がページ端に触れないようにします。  
* **実務例:** 請求書テンプレートでは `Top`/`Left` を使い、承認者の署名をヘッダー付近に配置することがあります。

## Office ドキュメント向けに署名ラインを追加する方法

DOCX や XLSX ファイルに署名する際、可視的な署名ラインを入れるとエンドユーザーの可読性が向上します。ライブラリは Microsoft スタイルの署名ラインを生成し、署名者名・役職・メールアドレスを表示します。

`SignatureLineOptions` は Microsoft スタイルの署名ラインを生成し、署名者名・役職・メールアドレスを表示します。

```java
options.setSignatureLineText("John Doe", "Chief Legal Officer", "j.doe@yourcompany.com");
```

* PDF では無視されますが、Word と Excel では Microsoft Office で開く際に必須機能です。

## 実際にドキュメントに署名する手順

`Signature` インスタンスでソースファイルをロードし、完全に設定した `DigitalSignOptions` を適用して `sign()` を呼び出します。ライブラリは新しいファイルを出力パスに書き込み、元のファイルはそのまま残ります。50 ページ超の大容量 PDF では 2‑5 秒程度の処理時間が目安です。Web サービスでは非同期実行を検討してください。

```java
Signature signature = new Signature("SAMPLE_WORDPROCESSING/contract.docx");
DigitalSignOptions options = new DigitalSignOptions();
// ...configure options as shown earlier...
signature.sign("OUTPUT_FOLDER/signed_contract.docx", options);
```

**パフォーマンス注意:** 100 ページ超の場合は JVM ヒープを増やす（例 `-Xmx2g`）か、`setAllPages(true)` を無効にしてメモリ使用量を抑えてください。

## よくある問題のトラブルシューティング

署名が失敗したときは、証明書取り扱い、ビジュアル配置、メモリ制約のいずれかが原因になることが多いです。症状を特定し、以下のチェックリストに従って迅速に解決してください。

### 「Invalid Certificate」や「Cannot Load Certificate」エラーが出る理由は？

この例外は主に次の 4 つの原因です。

1. **パスワードが間違っている** – OpenSSL で確認: `openssl pkcs12 -info -in yourcert.pfx`。  
2. **証明書が期限切れ** – `keytool -list -v -keystore yourcert.pfx` で有効期限を確認。  
3. **ファイル形式が不正** – `.pfx` または `.p12`（プライベートキーを含む）だけが受け付けられます。  
4. **ファイル権限の問題** – Java プロセスが証明書ファイルを読み取れることを確認。

### 署名がページに表示されない理由は？

* `AllPages` フラグが `false` のため、スタンプが付いていないページを見ている可能性。  
* 画像パスが誤っている → `options.getImageFilePath()` を出力して確認。  
* 配置設定が画面外にスタンプを押し出している → デバッグ時は一時的に `Center` に切り替えてみる。

### Adobe Reader が「Signature Invalid」と表示する理由は？

* **証明書が信頼されていない** – 自己署名証明書は警告を出します。本番環境では CA 発行証明書を使用してください。  
* **証明書チェーンが不完全** – `.pfx` に中間証明書とルート証明書が含まれていることを確認。  
* **タイムスタンプが欠如** – TSA トークンが無いと、証明書有効期限切れ後に無効と見なされることがあります。GroupDocs は `setTimeStampOptions()` でタイムスタンプをサポートします。

### 巨大 PDF で OutOfMemoryError を回避する方法は？

* JVM ヒープを増やす（例 `-Xmx4g` 以上）。  
* 必要なページだけ署名する（`setAllPages(false)`）。  
* 環境が制限的な場合は、ファイルを小分けに処理するかストリーミングしてください。

## 本番環境での証明書管理方法

ソースコードに証明書やパスワードを埋め込んではいけません。以下の手順で安全に管理してください。

1. `.pfx` ファイルを安全なボールト（AWS Secrets Manager、Azure Key Vault、HashiCorp Vault など）に保管。  
2. ランタイム時に環境変数またはボールト API からパスワードを取得。  
3. ファイルシステム権限を制限し、サービスアカウントのみが証明書を読めるようにする。  
4. 証明書は有効期限の 30 日前までにローテーションし、ボールトのシークレットも同時に更新。

```java
String certPath = System.getenv("CERT_PATH");
String certPassword = System.getenv("CERT_PASSWORD");
options.setCertificatePath(certPath);
options.setCertificatePassword(certPassword);
```

## 監査コンプライアンスのために署名操作をログに残す方法

監査ログは否認防止の証拠となります。各署名イベントで以下の項目を記録してください。

* 署名前のドキュメント名とハッシュ  
* 署名者の身元（証明書サブジェクト）  
* 操作のタイムスタンプ（できれば UTC）  
* 結果ステータス（成功/失敗）とエラー詳細（存在する場合）  

```java
logger.info("Signing document {} with certificate {} at {}", docPath, options.getCertificatePath(), Instant.now());
```

## 署名後に検証する方法

`verify()` メソッドを使用して、署名後にドキュメントが改ざんされていないか確認します。メソッドは `VerificationResult` を返し、妥当性ステータス、署名者情報、タイムスタンプ情報などを含みます。検証が成功すれば、完全な整合性と真正性が保証されます。

```java
VerificationResult result = signature.verify("OUTPUT_FOLDER/signed_contract.docx");
if (result.isValid()) {
    logger.info("Signature is valid and trusted.");
} else {
    logger.warn("Signature verification failed: {}", result.getErrorMessage());
}
```

## 1 つのドキュメントに複数署名を追加する方法

承認者と証人の 2 つの署名が必要なケースがあります。`DigitalSignOptions` インスタンスをそれぞれ別々に作成し、`sign()` を複数回呼び出すだけで OK。ライブラリは既存の署名を保持しつつ新しい署名を追加します。

```java
// First signature (approver)
signature.sign("output.docx", approverOptions);
// Second signature (witness)
signature.sign("output.docx", witnessOptions);
```

## ドキュメントタイプ別にファクトリメソッドを作成する方法

ヘルパーメソッドでファイル拡張子に応じた事前設定済み `DigitalSignOptions` を返すようにすれば、コードが DRY になります。PDF、Word、Excel など各フォーマットに対する証明書読み込み、ビジュアルデフォルト、ページ選択ロジックを一元管理できます。

```java
public DigitalSignOptions getOptionsFor(String extension) {
    DigitalSignOptions opts = new DigitalSignOptions();
    // common settings
    if (extension.equalsIgnoreCase("pdf")) {
        opts.setImageFilePath("signatures/pdf_stamp.png");
    } else if (extension.equalsIgnoreCase("docx")) {
        opts.setSignatureLineText("Jane Smith", "Finance Manager", "j.smith@company.com");
    }
    return opts;
}
```

## 既に署名されているかどうかを検証する方法

新しい署名を適用する前に、既存の署名があるか確認して二重署名を防ぎます。`getSignatures()` メソッドでコレクションを取得し、空でなければ追加署名か処理中止かを判断してください。

```java
List<SignatureInfo> existing = signature.getSignatures();
if (!existing.isEmpty()) {
    logger.warn("Document already contains {} signatures.", existing.size());
}
```

## 実務での活用例（実際のユースケース）

1. **自動契約ワークフロー** – 契約が BPM システムで「承認済み」になると、署名サービスを呼び出して法務部の証明書で署名し、ベンダーへ署名済みコピーをメール送信。  
2. **請求書承認システム** – 経理が請求書を承認したら、デジタル署名を自動で付与し、顧客へ送付。暗号的な真正性証明が付随します。  
3. **ドキュメント検証ポータル** – ユーザーが PDF をアップロードすると、会社全体の証明書で署名し、改ざん防止ファイルとして返却。法的コンプライアンスに活用。  
4. **規制が厳しい業界** – 医療（HIPAA）や金融（SOX）では、デジタル署名が誰がいつ署名したかを証明し、監査要件を満たします。  
5. **社内ポリシー配布** – HR が作成した最終 PDF に CHRO の証明書で自動署名し、全従業員に検証可能なコピーを配布。

## パフォーマンス考慮事項

| ドキュメントサイズ | 平均処理時間 | 推奨設定 |
|-------------------|--------------|----------|
| 1‑5 ページ | 約 0.5 秒 | デフォルトオプション |
| 5‑50 ページ | 1‑3 秒 | ヒープ増加、必要に応じて `setAllPages(true)` |
| 50‑200 ページ | 3‑10 秒 | `setAllPages(false)`、非同期実行、ヒープ拡大 |

**最適化ヒント:**  

* バッチで多数のファイルを署名する場合は、`Signature` インスタンスを再利用。  
* `DigitalSignOptions` オブジェクトをキャッシュし、証明書の再読み込みによるオーバーヘッドを削減。  
* Web サービスでは署名呼び出しを `CompletableFuture` でラップするか、メッセージキューに投げて UI の応答性を保つ。

## プロのコツ（高度な活用）

* **長期有効性のためのタイムスタンプ** – `setTimeStampOptions()` で TSA トークンを付与し、証明書期限切れ後も署名を有効に保つ。  
* **不可視署名** – `ImageFilePath` を省略し、`Width`/`Height` を `0` に設定すると、視覚的には見えないが暗号的に有効な署名が生成されます。バックエンド処理で便利です。  
* **カスタム QR コード署名** – GroupDocs は署名者メタデータを含む QR コードを埋め込めます。サプライチェーン書類でモバイル端末による迅速検証に最適。

## FAQ（よくある質問）

**Q: GroupDocs.Signature と iText の PDF 署名の主な違いは？**  
A: iText は PDF のみを対象とし、暗号処理を自前で実装する必要があります。一方、GroupDocs.Signature は 30 以上のフォーマットをサポートし、ビジュアルスタンプや証明書処理を自動化して開発時間を大幅に短縮します。

**Q: Spring Boot のマイクロサービスに GroupDocs.Signature を組み込めますか？**  
A: はい。Maven 依存を追加し、署名ロジックをラップした `@Service` Bean を作成、必要な場所へインジェクトすれば、コントローラは軽量に保てます。

**Q: GroupDocs.Signature で作成した署名はどれほど安全ですか？**  
A: 標準的な PKI アルゴリズム（RSA/ECDSA）を使用し、ブラウザや Adobe Reader と同等の仕様に準拠しています。セキュリティは使用する証明書の品質に依存するため、必ず CA 発行の証明書を使用し、プライベートキーを保護してください。

**Q: 署名済みドキュメントは他の PDF リーダーでも機能しますか？**  
A: 問題ありません。署名証明書が信頼できれば、Adobe Reader、Foxit、最新のブラウザなどで正しく検証されます。自己署名証明書は警告が出ますが、技術的には有効です。

**Q: 目に見える署名画像なしで署名できますか？**  
A: 可能です。`ImageFilePath` を省略し、サイズパラメータをゼロに設定すれば、視覚的には見えないが暗号的に有効な署名が生成されます。バックエンド自動化に最適です。

## 結論

これで **add digital signature java** を GroupDocs.Signature を使って実装するための、完全な本番対応ロードマップが手に入りました。環境構築、証明書管理、ビジュアルカスタマイズ、パフォーマンスチューニング、複数署名やタイムスタンプといった高度なシナリオまで網羅しています。

**次のステップ:**  

1. 自分の証明書とドキュメントテンプレートでサンプルコードをテスト。  
2. 証明書をシークレットマネージャに移行し、JVM メモリ制限を適切に設定してデプロイを堅牢化。  
3. ヘルパーメソッドを拡張してバッチ処理に対応させるか、既存のワークフローエンジンと統合。  

さらに深く学びたい方は、以下の公式ドキュメントとコミュニティフォーラムをご参照ください。

---

**最終更新日:** 2026-06-11  
**テスト環境:** GroupDocs.Signature 23.12 for Java  
**作者:** GroupDocs  

**リソース:**  
- [GroupDocs.Signature Documentation](https://docs.groupdocs.com/signature/java/)  
- [Support Forum](https://forum.groupdocs.com/c/signature/)  

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}
```java
import com.groupdocs.signature.Signature;

public class SignatureSetup {
    public static void main(String[] args) {
        Signature signature = new Signature("path/to/your/document");
        // Your signing logic goes here
    }
}
```
```java
import com.groupdocs.signature.options.sign.DigitalSignOptions;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.exception.GroupDocsSignatureException;

DigitalSignOptions options = new DigitalSignOptions("YOUR_DOCUMENT_DIRECTORY/CertificatePfx");
options.setPassword("1234567890"); // Ensure your certificate password is secure
options.setReason("Sign"); // Reason for signing, e.g., "Contract Approval"
options.setContact("JohnSmith"); // Contact information of the signer
options.setLocation("Office1"); // Location where document is signed
```
```java
options.setImageFilePath("YOUR_DOCUMENT_DIRECTORY/ImageHandwrite");
options.setAllPages(true); // Apply signature to all pages of the document
options.setWidth(0); // Auto-width based on content
options.setHeight(60); // Height in pixels
```
```java
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
Padding padding = new Padding();
padding.setBottom(10); // Bottom padding for aesthetic spacing
padding.setRight(10); // Right padding to prevent clipping at edges
options.setMargin(padding);
```
```java
import com.groupdocs.signature.domain.signatures.DigitalSignatureAppearance;

options.setAppearance(new DigitalSignatureAppearance("John Smith", "Title", "jonny@test.com"));
```
```java
try {
    Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/SAMPLE_WORDPROCESSING");
    String outputFilePath = "YOUR_OUTPUT_DIRECTORY/DigitalAppearance.docx";
    signature.sign(outputFilePath, options);
} catch (GroupDocsSignatureException e) {
    throw new RuntimeException(e.getMessage());
}
```
```java
// BAD - Don't do this
options.setPassword("1234567890");

// GOOD - Load from environment variable
String certPassword = System.getenv("CERT_PASSWORD");
if (certPassword == null) {
    throw new RuntimeException("CERT_PASSWORD environment variable not set");
}
options.setPassword(certPassword);
```
```java
logger.info("Document signed: {}, SignedBy: {}, Timestamp: {}", 
    documentName, signerEmail, LocalDateTime.now());
```
```java
// Verify the signature immediately after signing
List<DigitalSignature> signatures = signature.verify();
if (signatures.isEmpty()) {
    throw new RuntimeException("Signature verification failed");
}
```
```java
signature.sign(outputPath, approverOptions);
signature = new Signature(outputPath); // Reload the signed document
signature.sign(finalOutputPath, witnessOptions);
```
```java
public DigitalSignOptions getOptionsForDocType(String docType) {
    DigitalSignOptions options = new DigitalSignOptions(certPath);
    if (docType.equals("contract")) {
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        // Contract-specific settings
    } else if (docType.equals("invoice")) {
        options.setVerticalAlignment(VerticalAlignment.Top);
        // Invoice-specific settings
    }
    return options;
}
```
```java
List<DigitalSignature> existingSignatures = signature.search(DigitalSignature.class);
if (!existingSignatures.isEmpty()) {
    System.out.println("Document already signed by: " + 
        existingSignatures.get(0).getContactInfo());
}
```

## 関連チュートリアル

- [Digital Signature in Java - Complete Guide to Certificate Loading and Document Signing](/signature/java/digital-signatures/digital-signature-loading-signing-groupdocs-java/)
- [How to Verify Digital Certificates in Java - Complete Guide with Code Examples](/signature/java/digital-signatures/java-certificate-verification-groupdocs-signature/)
- [Java Document Signing Tutorial - Add Text Signatures with Event Handling](/signature/java/event-handling/java-text-signing-groupdocs-signature-event-handling/)