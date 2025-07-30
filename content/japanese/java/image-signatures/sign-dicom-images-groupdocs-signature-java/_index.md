---
"date": "2025-05-08"
"description": "GroupDocs.Signature for Javaを使用してDICOM画像に安全に署名する方法を学びます。QRコードとメタデータを埋め込むことで、ドキュメントのセキュリティを強化します。"
"title": "GroupDocs.Signature for Java を使用して QR コードとメタデータで DICOM 画像に署名する"
"url": "/ja/java/image-signatures/sign-dicom-images-groupdocs-signature-java/"
"weight": 1
---

# GroupDocs.Signature for Java を使用して QR コードとメタデータで DICOM 画像に署名する方法

## 導入

急速に進化するデジタルヘルスケア環境において、患者データの安全な管理は極めて重要です。このチュートリアルでは、GroupDocs.Signature for Javaを使用して、DICOM（Digital Imaging and Communications in Medicine）画像にQRコードとメタデータで署名するための堅牢なソリューションを実装する方法を説明します。これらの機能は、重要な情報を医療画像に直接埋め込むことで、真正性の確保、トレーサビリティの向上、コンプライアンスの維持を実現します。

### 学習内容:
- GroupDocs.Signature for Java をプロジェクトに統合する方法。
- DICOM 画像に QR コードで署名するプロセス。
- ドキュメントのセキュリティを強化するために XMP メタデータを追加します。
- DICOM ファイル内の署名を取得、検証、検索します。
- 署名された DICOM 画像のプレビューを生成します。

さあ、始めましょう！始める前に、スムーズに進めるために必要なものがすべて揃っていることを確認しましょう。

## 前提条件

GroupDocs.Signature 機能を効果的に実装するには、次の前提条件を満たしていることを確認してください。

### 必要なライブラリと依存関係
- **Java 用 GroupDocs.Signature**: このライブラリのバージョン 23.12 以降が必要です。

### 環境設定要件
- **Java開発キット（JDK）**: システムに JDK がインストールされていることを確認してください。
- **IDE**: IntelliJ IDEA や Eclipse などの統合開発環境を使用します。

### 知識の前提条件
以下の基本的な理解:
- Java プログラミングとオブジェクト指向の原則。
- 依存関係管理用の Maven または Gradle ビルド ツール。

## Java 用 GroupDocs.Signature の設定

GroupDocs.Signature を使い始めるには、プロジェクトに依存関係として追加する必要があります。以下の手順に従って、各種ビルドツールで追加してください。

### メイヴン
次のスニペットを `pom.xml` ファイル：
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### グラドル
これをあなたの `build.gradle` ファイル：
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### 直接ダウンロード
または、最新バージョンを以下からダウンロードすることもできます。 [GroupDocs.Signature for Java リリース](https://releases。groupdocs.com/signature/java/).

#### ライセンス取得手順
1. **無料トライアル**期間限定の無料トライアルで機能をお試しください。
2. **一時ライセンス**完全な機能を試すには一時ライセンスを取得してください。
3. **購入**長期アクセスが必要な場合は、サブスクリプションを購入してください。

#### 基本的な初期化とセットアップ

GroupDocs.Signatureを初期化するには、 `Signature` クラス：
```java
import com.groupdocs.signature.Signature;

// DICOMファイルへのパスで署名オブジェクトを初期化します
Signature signature = new Signature(filePath);
```

## 実装ガイド

### QRコードとメタデータでDICOM画像に署名する

#### 概要
この機能を使用すると、DICOM 画像に QR コードで署名し、XMP メタデータを追加して、ドキュメントのセキュリティを強化できます。

#### ステップ1：QRコード署名オプションを設定する
```java
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.QrCodeSignOptions;

Padding padding = new Padding();
padding.setRight(5);
padding.setLeft(5);

QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues");
options.setAllPages(true);
options.setWidth(100);
options.setHeight(100);
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
options.setMargin(padding);
```
ここでは、DICOM 画像上の QR コードの外観と位置を設定します。

#### ステップ2: XMPメタデータを追加する
```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomSaveOptions;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpEntry;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpType;

DicomSaveOptions dicomSaveOptions = new DicomSaveOptions();
List<DicomXmpEntry> xmpEntries = new ArrayList<>();
xmpEntries.add(new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4"));
dicomSaveOptions.setXmpEntries(xmpEntries);
```
このスニペットは、DICOM ファイルにメタデータを追加し、追加の患者情報を埋め込みます。

#### ステップ3：文書に署名する
```java
String outputFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/" + fileName;
signature.sign(outputFilePath, options, dicomSaveOptions);
```
その `sign` このメソッドは、QR コードとメタデータを DICOM ファイルに書き込み、指定された場所に保存します。

### 署名されたDICOM画像情報の取得

#### 概要
検証または監査の目的で、署名された DICOM 画像から XMP メタデータを抽出します。
```java
import com.groupdocs.signature.domain.IDocumentInfo;
import com.groupdocs.signature.domain.signatures.MetadataSignature;

IDocumentInfo documentInfo = signature.getDocumentInfo();
for (MetadataSignature item : documentInfo.getMetadataSignatures()) {
    System.out.println(item.toString());
}
```
このコードは、DICOM ファイルに関連付けられているすべてのメタデータ署名を取得して印刷します。

### 署名されたDICOMの検証

#### 概要
署名された DICOM 画像に QR コード署名が存在することを確認して、その信頼性を確認します。
```java
import com.groupdocs.signature.domain.VerificationResult;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;
import com.groupdocs.signature.domain.enums.TextMatchType;

QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();
verifyOptions.setAllPages(true);
verifyOptions.setText("Patient #36363393");
verifyOptions.setMatchType(TextMatchType.Contains);

VerificationResult result = signature.verify(verifyOptions);
if (result.isValid()) {
    System.out.println(filePath + " has successfully verified signatures!");
} else {
    System.out.println(filePath + " failed verification process.");
}
```
この検証手順により、QR コードが予想される基準と一致していることが確認され、ドキュメントの整合性が確認されます。

### 署名されたDICOMの署名の検索

#### 概要
署名された DICOM 画像内のすべての QR コード署名を見つけて、確認または監査します。
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.util.List;

List<QrCodeSignature> signatures = signature.search(QrCodeSignature.class);
for (QrCodeSignature qrCodeSignature : signatures) {
    System.out.println("QRCode signature found at page " +
        qrCodeSignature.getPageNumber() + ": " +
        qrCodeSignature.getEncodeType().getTypeName() + ": " +
        qrCodeSignature.getText());
}
```
この機能は、ドキュメント内のすべての QR コード署名をスキャンして包括的な可視性を提供するのに役立ちます。

### 署名済みDICOMのプレビュー生成

#### 概要
署名された DICOM 画像の各ページのプレビューを作成し、ファイル全体を開かなくてもすばやく視覚的に検査できるようにします。
```java
import com.groupdocs.signature.options.PreviewOptions;
import java.io.File;
import java.io.FileOutputStream;
import java.nio.file.Paths;

PreviewOptions previewOption = new PreviewOptions(pageNumber -> {
    try {
        String pageFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/image-" + pageNumber + ".jpg";
        return new FileOutputStream(Paths.get(pageFilePath).toFile());
    } catch (Exception e) {
        throw new RuntimeException(e.getMessage());
    }
});

signature.generatePreview(previewOption);
```
このスニペットは各ページの画像プレビューを生成するので、簡単な検証や共有に役立ちます。

## 実用的な応用

GroupDocs.Signature for Java は、いくつかの実用的なアプリケーションを提供します。
- **医療画像**QR コードとメタデータを使用して患者の DICOM 画像に安全に署名し、管理します。
- **法務文書管理**法的手続きにおける文書の信頼性とコンプライアンスを強化します。
- **金融サービス**機密性の高い財務文書に安全な電子署名を実装します。