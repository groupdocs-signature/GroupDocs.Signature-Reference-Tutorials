---
categories:
- Java Development
date: '2026-07-01'
description: java署名検証と、GroupDocs.Signatureを使用したpdf署名の検証方法を学びましょう。コード、トラブルシューティング、セキュリティベストプラクティスを含むステップバイステップガイドです。
keywords:
- java signature verification
- verify pdf signature java
- digital signature validation java
- groupdocs signature tutorial
- verify digital signature in java
lastmod: '2026-07-01'
linktitle: JavaでDigital Signaturesを検証
schemas:
- author: GroupDocs
  dateModified: '2026-07-01'
  description: Learn java signature verification and how to verify pdf signature java
    using GroupDocs.Signature. Step‑by‑step guide with code, troubleshooting, and
    security best practices.
  headline: Java Signature Verification – Verify Digital Signatures in Java
  type: TechArticle
- description: Learn java signature verification and how to verify pdf signature java
    using GroupDocs.Signature. Step‑by‑step guide with code, troubleshooting, and
    security best practices.
  name: Java Signature Verification – Verify Digital Signatures in Java
  steps:
  - name: Import Required Packages
    text: 'Start by importing what you need: The following imports bring in the core
      classes required for loading documents, configuring verification, and handling
      results.'
  - name: Configure Verification Options
    text: 'Here''s where it gets interesting. You can customize the verification process
      with specific parameters. For example, let''s add a comment to track why we''re
      verifying this document: `VerificationOptions` defines the criteria and settings
      used during the verification process, such as which signatures t'
  - name: Perform the Verification
    text: 'Now execute the verification: `VerificationResult` contains the outcome
      of the verification operation, indicating success or failure and providing detailed
      information about any issues encountered. `VerificationResult` is a concise
      object that tells you whether the signature passed all checks and pr'
  type: HowTo
- questions:
  - answer: A digital signature uses cryptographic algorithms to prove authenticity
      and detect tampering. An electronic signature is broader—any electronic indicator
      of intent to sign (like typing your name). Digital signatures are a specific,
      more secure type of electronic signature.
    question: What is a digital signature and how does it differ from an electronic
      signature?
  - answer: Add it as a Maven or Gradle dependency (see the setup section above),
      or download the JAR directly from the GroupDocs website and add it to your project's
      classpath.
    question: How do I install GroupDocs.Signature for Java?
  - answer: Yes, you can use the free trial for development and testing. It has some
      limitations (like watermarks), but works fine for learning. For production,
      you'll need a commercial or temporary license.
    question: Can I verify signatures without a GroupDocs license?
  - answer: The `verify()` method returns a `VerificationResult` object with `isValid()`
      set to false. You can examine the result details to understand why it failed—expired
      certificate, document modification, invalid signature algorithm, etc.
    question: What happens if verification fails?
  - answer: It lets you verify a signature was valid at a specific point in time,
      which is critical for legal and audit purposes. Without it, you can only verify
      if a signature is valid right now—useless for historical documents with expired
      certificates.
    question: How does date handling improve signature verification?
  type: FAQPage
tags:
- digital-signatures
- document-security
- java-tutorial
- groupdocs
title: Java Signature Verification – JavaでDigital Signaturesを検証
type: docs
url: /ja/java/digital-signatures/java-digital-signature-verification-groupdocs/
weight: 1
---

# Java 署名検証 – Java でデジタル署名を検証する

## はじめに

デジタル署名された文書を受け取り、「**本当に主張通りの人物が作成したものか？**」と疑ったことはありませんか？ デジタル詐欺が増加する中、**java signature verification** は機密文書を扱うすべてのアプリケーションにとって重要です。契約管理システムの構築、金融契約の処理、政府記録の検証など、どのシナリオでも必要です。

課題は次のとおりです。Java の組み込み署名検証は複雑で機能が限定的です。そこで **GroupDocs.Signature for Java** が登場します。プロセス全体をシンプルにし、日付ベースの検証やカスタム検証ルールといった強力なオプションを提供します。

このガイドでは、以下を正確に学びます。
- Java プロジェクトへの GroupDocs.Signature の設定と構成方法
- カスタムオプションとパラメータを使用したデジタル署名の検証方法
- 時間に敏感な文書のための日付指定検証の扱い方
- セキュリティを損なう一般的な落とし穴の回避策
- 本番環境向けの署名検証実装

まずは必要なものを確認しましょう。

## クイック回答
- **Java で PDF 署名を検証する最も簡単な方法は？** GroupDocs.Signature の `Signature.verify()` を `VerificationOptions` オブジェクトと共に使用します。  
- **本番環境でライセンスは必要ですか？** はい。GroupDocs.Signature は本番利用に商用または一時ライセンスが必要です。  
- **証明書の有効期限が切れた署名も検証できますか？** はい。`VerificationOptions.setVerificationTime()` で検証日時を設定します。  
- **サポートされている文書形式はいくつですか？** PDF、DOCX、XLSX、PPTX、PNG など 30 以上の形式に対応。  
- **推奨される Java バージョンは？** セキュリティとパフォーマンスの観点から Java 11 以上を推奨します。

## Java 署名検証とは何ですか？
`java signature verification` は、文書に埋め込まれたデジタル署名が本物で改ざんされておらず、信頼できる署名者によって作成されたことをプログラム上で確認するプロセスです。暗号チェック、証明書チェーンの検証、オプションの時間ベース検証が含まれます。この検証ステップにより、署名者の身元が保証され、署名後に文書が変更されていないことが確認されます。

## デジタル署名検証が重要な理由

コードに入る前に、なぜ重要かを説明します。デジタル署名は 3 つの重要な機能を提供します：真正性の確認、完全性の保証、否認防止。実務上は、請求書がベンダーからの正当なものか、契約書が改ざんされていないか、署名済み合意が法的に有効かを信頼できるようになります。医療（HIPAA）、金融（SOX）、政府契約などの業界は、日々これに依存しています。

## 前提条件

開始前に以下を用意してください。
- **Java Development Kit (JDK)**：バージョン 8 以上（セキュリティ機能強化のため Java 11+ 推奨）  
- **IDE**：IntelliJ IDEA、Eclipse、または Java 拡張機能付き VS Code  
- **ビルドツール**：Maven または Gradle（依存関係管理用）  
- **基本的な Java 知識**：クラス、オブジェクト、ファイル I/O の理解  

暗号の専門家である必要はありません（ありがたいことに）。デジタル署名の基本概念を知っていれば十分です。初心者には、封筒に貼る蝋封印のようなものと考えるとイメージしやすいでしょう。

## GroupDocs.Signature for Java の設定

Maven でも Gradle でも、GroupDocs.Signature の統合はシンプルです。

### Maven 設定
`pom.xml` に以下の依存関係を追加してください。
``` 
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```
```

### Gradle 設定
Gradle を使用している場合は、`build.gradle` に次を追加します。
``` 
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```
```

**プロのコツ**：常に最新バージョンは [GroupDocs releases page](https://releases.groupdocs.com/signature/java/) で確認してください。新バージョンにはセキュリティパッチやパフォーマンス改善が含まれます。

### ライセンス取得

GroupDocs.Signature は本番利用にライセンスが必要です。選択肢は次の通りです。

1. **無料トライアル**：テスト・開発向け（[こちらから取得](https://releases.groupdocs.com/signature/java/)）  
2. **一時ライセンス**：30 日間フル機能利用可能（[こちらからリクエスト](https://purchase.groupdocs.com/temporary-license/)）  
3. **商用ライセンス**：本番デプロイ向け（[こちらから購入](https://purchase.groupdocs.com/buy)）

無料トライアルは透かしが入るなど制限がありますが、学習やプロトタイプ作成には最適です。

### 基本的な初期化

依存関係を解決したら、ライブラリを次のように初期化します。

`Signature` クラスは文書をロードし、署名・検証メソッドを提供するエントリーポイントです。
``` 
```java
import com.groupdocs.signature.Signature;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample_signed_document.pdf";
Signature signature = new Signature(filePath);
```
```

## デジタル署名の検証：基本

それでは実際にデジタル署名文書を検証してみましょう。

### java signature verification の最初のステップは？
`Signature` インスタンスで文書をロードし、適切に構成した `VerificationOptions` オブジェクトを渡して `verify()` を呼び出します。この一呼び出しで暗号検証、完全性チェック、証明書チェーン検証が実行され、文書の真正性と署名者証明書の信頼性が確認されます。

### 手順 1: 必要なパッケージをインポート

以下のインポートで、文書ロード、検証設定、結果処理に必要なコアクラスを取得します。
``` 
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.VerificationResult;
import com.groupdocs.signature.options.verify.DigitalVerifyOptions;
```
```

### 手順 2: VerificationOptions の設定

ここで検証プロセスをカスタマイズします。例として、検証理由をコメントとして残す方法を示します。

`VerificationOptions` は検証時に使用する基準や設定（チェック対象の署名やカスタム検証ルールなど）を定義します。
``` 
```java
DigitalVerifyOptions options = new DigitalVerifyOptions();
options.setComments("Approved");  // Tracks verification context
```
```

コメントを残すことで監査トレイルが容易になります。数か月後にログを確認すると、なぜその文書を検証したのかが一目で分かります。

### 手順 3: 検証の実行

検証を実行します。
``` 
```java
VerificationResult result = signature.verify(options);
if (result.isValid()) {
    System.out.println("The document was verified successfully.");
} else {
    System.out.println("The document failed the verification process.");
}
```
```

`VerificationResult` は検証の成功・失敗と、問題があった場合の詳細情報を提供します。ライブラリは次をチェックします。
- 署名は暗号的に有効か？  
- 署名後に文書は変更されていないか？  
- 証明書チェーンは正しく検証できるか？

すべて合格すれば `true` が返り、失敗すれば `false` が返ります。その場合は文書を疑わしいものとして扱います。

## 日付指定検証の扱い方

特定の時点で署名が有効だったかを確認する必要がある場合があります。これは、証明書が後に失効していても「署名時点では有効だった」ことを証明するために重要です。

### 日付処理が重要な理由

例：契約が 6 月 1 日に署名され、証明書は 7 月 1 日に失効したとします。8 月 1 日に検証すると証明書が失効しているため検証は失敗します。しかし、日付ベースの検証を使用すれば、署名時点で有効だったことを確認できます。

### 検証日時の設定

`VerificationOptions.setVerificationTime()` で、証明書の有効性を評価する基準時刻を指定します。
``` 
```java
import java.util.Date;
import java.text.SimpleDateFormat;

// Verify as if it's a specific date
SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd");
Date verificationDate = dateFormat.parse("2024-06-15");

options.setVerificationDate(verificationDate);
```
```

### 日付ベース検証の実行

設定した日時で検証を実行します。
``` 
```java
VerificationResult result = signature.verify(options);
if (result.isValid()) {
    System.out.println("The document was verified successfully for the specified date.");
} else {
    System.out.println("The document failed verification for that date.");
}
```
```

**実務例**：金融機関は過去取引の監査時に、署名が署名時点で有効だったかを確認します。

## 署名検証時の一般的なミス

開発者が陥りやすいミスとその回避策を紹介します。

### 1. 証明書有効期間のチェック忘れ
**ミス**：証明書が期限切れだから署名は無効と判断する。  
**対策**：過去文書は必ず日付ベース検証を行い、署名時点の有効性を確認する。

### 2. ファイルパスのハードコーディング
**ミス**：環境依存のパスを書き込んでしまう。  
**対策**：`Paths.get()` を使用してプラットフォーム非依存のパスを構築する。  
``` 
```java
// Don't do this:
String filePath = "C:\\Users\\John\\Documents\\contract.pdf";

// Do this instead:
String filePath = System.getProperty("user.dir") + "/documents/contract.pdf";
// Or use proper configuration files
```
```

### 3. 検証結果の詳細を無視
**ミス**：`isValid()` だけを確認し、失敗理由を調べない。  
**対策**：`result.getErrorMessage()` と `result.getErrorCode()` をログに出力する。  
``` 
```java
VerificationResult result = signature.verify(options);
if (!result.isValid()) {
    // Get detailed failure information
    System.out.println("Verification failed. Details:");
    result.getFailed().forEach(signatureResult -> {
        System.out.println("Error: " + signatureResult.getMessage());
    });
}
```
```

### 4. 誤った証明書ストアの使用
**ミス**：検証に適切な認証局を設定していない。  
**対策**：Java キーストアに署名機関のルート証明書を追加し、社内 CA でも同様に設定する。

## セキュリティベストプラクティス

実装が安全であることを保証するための指針です。

### 1. 信頼前に必ず検証
署名文書を処理する前に必ず検証を行うことが必須です。

`Signature.verify()` は文書全体の署名有効性を示す boolean を返します。  
``` 
```java
public boolean processDocument(String filePath) {
    Signature signature = new Signature(filePath);
    DigitalVerifyOptions options = new DigitalVerifyOptions();
    
    // Mandatory verification check
    if (!signature.verify(options).isValid()) {
        throw new SecurityException("Document failed signature verification");
    }
    
    // Only proceed if verification passed
    return processVerifiedDocument(filePath);
}
```
```

### 2. ライブラリは常に最新に保つ
セキュリティ脆弱性は定期的に修正されます。GroupDocs のセキュリティアナウンスを購読し、新バージョンが出たら速やかに更新してください。

### 3. 安全なファイル保管
検証済み文書を公開ディレクトリに置かない。アクセス制御を徹底します。
- 必要なユーザーだけにファイル権限を付与  
- 機密文書は暗号化ストレージに保存  
- すべての文書アクセスに監査ログを実装  

### 4. 証明書チェーンの検証
`VerificationOptions` でルート認証局までのフルチェーン検証を有効にできます。  
``` 
```java
options.setVerifyCertificateChain(true);  // Ensures full chain validation
```
```

### 5. タイムアウト設定
DoS 攻撃防止のため、検証操作にタイムアウトを設定します。

`VerificationOptions.setTimeout(30_000)` は検証処理に 30 秒の上限を設けます。  
``` 
```java
// Prevent hanging on corrupted or malicious files
signature.setTimeoutMilliseconds(5000);  // 5-second timeout
```
```

## GroupDocs と Java 標準機能の使い分け

「Java に組み込みの署名検証があるのに、なぜ GroupDocs を使うのか？」という疑問に答えます。

### Java 標準 API を使うべきケース
- 基本的な署名検証だけが必要  
- 特定フォーマット（例：JAR 署名）のみ対象  
- 外部依存を増やしたくない  
- 社内に暗号専門家がいる  

### GroupDocs.Signature を使うべきケース
- PDF、DOCX、XLSX など多数のフォーマットを検証したい  
- 高レベル API で実装コストを削減したい  
- 日付ベース検証や QR コード、バーコード、メタデータ署名など高度な機能が必要  
- 開発スピードを重視し、依存関係の増加を許容できる  

**結論**：GroupDocs.Signature は署名検証の専門家をチームに持つようなものです。低レベル API で自前実装も可能ですが、数日で実装できる点が大きなメリットです。

## よくある問題のトラブルシューティング

### 問題: 「File not found」例外
**症状**：`FileNotFoundException` が発生するが、ファイルは存在する。  

**対策**：
1. パス区切り文字を統一（スラッシュまたはエスケープされたバックスラッシュ）  
2. ファイル権限を確認し、アプリが読み取り可能か確認  
3. デバッグ時は絶対パスを使用してパス問題を排除  

`Path.of()` はプラットフォーム非依存のパスオブジェクトを生成し、エラーを減らします。  
``` 
```java
// Debug file path issues
File file = new File(filePath);
System.out.println("File exists: " + file.exists());
System.out.println("Can read: " + file.canRead());
System.out.println("Absolute path: " + file.getAbsolutePath());
```
```

### 問題: 有効な署名が検証に失敗する
**症状**：署名は有効なのに `verify()` が false を返す。  

**対策**：
1. 証明書が期限切れでないか確認（過去文書は日付ベース検証）  
2. Java キーストアに署名者のルート CA が含まれているか確認  
3. 署名後に文書が変更されていないか確認（微小な変更でも破損）  
4. 使用している Java バージョンが署名アルゴリズムをサポートしているか確認  

### 問題: 大容量ファイルで OutOfMemoryError
**症状**：大きな PDF やバッチ処理時に `OutOfMemoryError` が発生。  

**対策**：
1. JVM ヒープサイズを増やす：`-Xmx2g` など適宜調整  
2. ファイルを一括で読み込まず、個別に処理  
3. 非常に大きなファイルはストリーミング検証を利用  

`Signature.verifyStream()` はドキュメントをチャンク単位で処理し、メモリ使用量を抑えます。  
``` 
```java
// Proper resource management
try (Signature signature = new Signature(filePath)) {
    VerificationResult result = signature.verify(options);
    // Process result
} // Automatically closes and releases resources
```
```

### 問題: 検証が遅い
**症状**：1 文書あたり数秒かかる。  

**対策**：
1. 同一署名者からの複数文書では証明書検証結果をキャッシュ  
2. バッチ検証は並列処理で実行  
3. 不要な検証オプションは無効化  
4. リモート証明書ストアを使用している場合はネットワーク遅延をチェック  

## 本番環境向け高度テクニック

本番導入を検討している方向けに、プロレベルのヒントを紹介します。

### 1. 包括的なロギング実装
成功・失敗だけでなく、デバッグに有用な情報すべてを記録します。

`logger.info("Verification result: {}", result)` は結果オブジェクト全体を後から分析できる形で出力します。  
``` 
```java
import java.util.logging.Logger;

Logger logger = Logger.getLogger(YourClass.class.getName());

VerificationResult result = signature.verify(options);
logger.info(String.format(
    "Verification for %s: %s (Processed in %dms)",
    filePath,
    result.isValid() ? "PASSED" : "FAILED",
    result.getProcessingTime()
));

if (!result.isValid()) {
    result.getFailed().forEach(failure ->
        logger.warning("Verification failure: " + failure.getMessage())
    );
}
```
```

### 2. 非同期検証でスループット向上
多数文書を処理する場合は非同期処理を活用します。

`CompletableFuture.runAsync(() -> signature.verify(options))` は別スレッドプールで検証を実行します。  
``` 
```java
import java.util.concurrent.CompletableFuture;

public CompletableFuture<VerificationResult> verifyAsync(String filePath) {
    return CompletableFuture.supplyAsync(() -> {
        try (Signature signature = new Signature(filePath)) {
            return signature.verify(options);
        }
    });
}
```
```

### 3. 外部依存に回路遮断器を導入
証明書検証が外部サービスに依存している場合、回路遮断器で障害時の影響を最小化します。

### 4. 検証結果のキャッシュ（慎重に）
変更されない文書は検証結果をキャッシュできますが、キャッシュ失効を正しく実装してください。

`Cache.put(docId, result, Duration.ofHours(24))` は 24 時間結果を保持します。  
``` 
```java
// Pseudocode for caching strategy
String cacheKey = filePath + "_" + fileChecksum;
if (verificationCache.containsKey(cacheKey)) {
    return verificationCache.get(cacheKey);
}
// Verify and cache
VerificationResult result = signature.verify(options);
verificationCache.put(cacheKey, result, CACHE_TTL);
```
```

### 5. 検証失敗の監視とアラート
失敗率をモニタリングし、急激な増加があれば以下を疑います。
- システム内の文書が改ざんされた  
- 証明書の有効期限切れが増加した  
- デプロイ後の設定ミス  

## 実用例とユースケース

具体的なシナリオでの活用方法を示します。

### ユースケース 1：契約管理システム
**シナリオ**：法律事務所が受領したすべての契約書の署名を検証する必要がある。  

**実装例**：
``` 
```java
public boolean processIncomingContract(String contractPath) {
    try (Signature signature = new Signature(contractPath)) {
        DigitalVerifyOptions options = new DigitalVerifyOptions();
        options.setComments("Contract intake verification");
        
        VerificationResult result = signature.verify(options);
        
        if (result.isValid()) {
            // Move to approved contracts folder
            // Trigger workflow for legal review
            return true;
        } else {
            // Flag for manual review
            // Notify sender of invalid signature
            return false;
        }
    }
}
```
```

### ユースケース 2：金融文書監査
**シナリオ**：銀行が規制監査で過去のローン契約を検証する。  

**実装**：日付ベース検証で、署名時点の有効性を確認。証明書が後に失効していても問題なし。

### ユースケース 3：マルチパーティ文書検証
**シナリオ**：不動産取引で買い手、売り手、仲介者の 3 名の署名が必要。  

**実装**：各署名を個別に検証し、すべて合格した場合にのみ取引を完了。

## パフォーマンス考慮事項

数千件の文書を処理する際は速度が重要です。影響を与える要因と最適化策をまとめます。

### パフォーマンスに影響する要因
1. 文書サイズ：大きいほど検証に時間がかかる  
2. 署名数：署名が多いほど処理が増える  
3. 証明書チェーン長：長いチェーンは検証ステップが増える  
4. ネットワークアクセス：リモート証明書検証は遅延要因  

### 最適化戦略
- **バッチ処理**：複数文書を並列で検証  
- **ローカル証明書キャッシュ**：ネットワーク呼び出しを削減  
- **選択的検証**：必要な署名だけを検証  
- **リソースプーリング**：`Signature` オブジェクトを再利用（スレッド安全性はドキュメント参照）  

`ExecutorService` を使ってスレッドプールを管理すれば、同時検証数を増やしスループットを向上させられます。  
``` 
```java
// Example: Batch verification with parallel streams
List<String> filePaths = Arrays.asList("doc1.pdf", "doc2.pdf", "doc3.pdf");

Map<String, Boolean> results = filePaths.parallelStream()
    .collect(Collectors.toMap(
        path -> path,
        path -> {
            try (Signature sig = new Signature(path)) {
                return sig.verify(options).isValid();
            }
        }
    ));
```
```

## FAQ（よくある質問）

**Q: デジタル署名と電子署名の違いは？**  
A: デジタル署名は暗号アルゴリズムで真正性と改ざん検知を実現します。電子署名は「署名した」という意思表示全般を指し、必ずしも暗号的保証を伴わない広い概念です。

**Q: GroupDocs.Signature for Java のインストール方法は？**  
A: 上記の Maven または Gradle 設定を行うか、GroupDocs の公式サイトから JAR をダウンロードしてクラスパスに追加します。

**Q: ライセンスなしで署名を検証できますか？**  
A: 開発・テスト目的であれば無料トライアルで可能です。商用・本番利用には商用または一時ライセンスが必要です。

**Q: 検証が失敗した場合はどうすればよいですか？**  
A: `verify()` が返す `VerificationResult` の `isValid()` が false のとき、`result.getErrorMessage()` や `result.getErrorCode()` を確認し、期限切れ、文書改ざん、アルゴリズム非対応などの原因を特定します。

**Q: 日付処理は検証にどのように役立ちますか？**  
A: 特定時点での有効性を確認できるため、証明書が期限切れでも「署名時点では有効だった」ことを証明できます。歴史的文書の法的・監査的要件に必須です。

**Q: 1 文書内で複数の署名タイプを検証できますか？**  
A: 可能です。PDF などは複数署名者が存在することが一般的です。`Signature` オブジェクトを使い、必要に応じて異なる `VerificationOptions` を設定して個別に検証します。

**Q: GroupDocs.Signature はスレッドセーフですか？**  
A: 最新ドキュメントでスレッド安全性を確認してください。安全策としては、バッチ処理時にスレッドごとに別の `Signature` インスタンスを作成することを推奨します。

**Q: サポートしている文書形式は？**  
A: PDF、Microsoft Office（DOCX、XLSX、PPTX）、画像形式など多数。完全なリストは [documentation](https://docs.groupdocs.com/signature/java/) を参照してください。

## 追加リソース

- [GroupDocs.Signature Documentation](https://docs.groupdocs.com/signature/java/) – 完全な API ドキュメント  
- [API Reference](https://reference.groupdocs.com/signature/java/) – クラス・メソッド詳細  
- [Download GroupDocs.Signature](https://releases.groupdocs.com/signature/java/) – 最新リリース  
- [Purchase a License](https://purchase.groupdocs.com/buy) – 商用ライセンス情報  
- [Free Trial](https://releases.groupdocs.com/signature/java/) – 試用版ダウンロード  
- [Temporary License](https://purchase.groupdocs.com/temporary-license/) – 30 日間フル機能ライセンス  
- [Support Forum](https://forum.groupdocs.com/c/signature/) – コミュニティサポート  

---

**最終更新日:** 2026-07-01  
**テスト環境:** GroupDocs.Signature 23.12 for Java  
**作者:** GroupDocs

## 関連チュートリアル

- [Java Digital Signature Library Tutorial with GroupDocs.Signature](/signature/java/digital-signatures/)  
- [How to Add Digital Signature in Java - Complete GroupDocs Tutorial](/signature/java/getting-started/groupdocs-signature-java-digital-setup-guide/)  
- [Java QR Code Signature Library - Complete GroupDocs Tutorial](/signature/java/qr-code-signatures/)