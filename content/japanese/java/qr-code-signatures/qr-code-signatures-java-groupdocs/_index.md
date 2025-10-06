---
"date": "2025-05-08"
"description": "GroupDocs.Signatureを使用してJavaでQRコード署名を実装・検証することで、ドキュメントのセキュリティを強化する方法を学びましょう。安全な署名プロセスを実現するには、このステップバイステップガイドに従ってください。"
"title": "ドキュメントを保護する - GroupDocs.Signature を使用して Java で QR コード署名を実装する"
"url": "/ja/java/qr-code-signatures/qr-code-signatures-java-groupdocs/"
"weight": 1
type: docs
---
# ドキュメントのセキュリティ確保: GroupDocs.Signature を使用して Java で QR コード署名を実装する

今日のデジタル環境において、契約書、請求書、個人情報といった文書のセキュリティ確保は極めて重要です。文書のセキュリティを強化し、検証プロセスを簡素化する革新的なアプローチの一つが、QRコード署名の利用です。このチュートリアルでは、GroupDocs.Signatureを用いてJavaで文書にQRコード署名を実装し、検証する方法を説明します。

## 学ぶ内容
- QRコードを使って文書に署名する方法
- QRコードで署名された文書を検証する
- 文書内の既存のQRコード署名を検索する
- ドキュメントからQRコード署名を更新および削除する

環境を設定して始めましょう!

### 前提条件
始める前に、次の前提条件が満たされていることを確認してください。

#### 必要なライブラリと依存関係
Java用のGroupDocs.Signatureが必要です。MavenまたはGradle経由で組み込むか、直接ダウンロードしてください。

**メイヴン**
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**グラドル**
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**直接ダウンロード**
最新バージョンをダウンロードするには [GroupDocs.Signature for Java リリース](https://releases。groupdocs.com/signature/java/).

#### 環境設定要件
- Java Development Kit (JDK) 8 以降がインストールされていることを確認してください。
- IntelliJ IDEA、Eclipse、NetBeans などの IDE を使用します。

#### 知識の前提条件
Java プログラミングとドキュメント処理の基本的な理解があると役立ちます。

## Java 用 GroupDocs.Signature の設定
プロジェクトで GroupDocs.Signature を使用するには、次の手順に従います。
1. **インストール**設定に応じて、Maven、Gradle、または直接ダウンロードのいずれかを選択します。
2. **ライセンス取得**：
   - まずは無料トライアルをご利用ください [GroupDocsウェブサイト](https://releases。groupdocs.com/signature/java/).
   - 長期にわたるテストと開発のために一時ライセンスを取得することを検討してください。 [ここ](https://purchase。groupdocs.com/temporary-license/).
3. **基本的な初期化**： 
    GroupDocs.Signature を初期化する方法は次のとおりです。

    ```java
    Signature signature = new Signature("YOUR_DOCUMENT_PATH");
    ```

これにより、QR コード署名を実装するための準備が整います。

## 実装ガイド

### QRコード署名で文書に署名する
#### 概要
QRコードを使用して文書に署名するには、デジタル署名を表す固有のコードを埋め込む必要があります。このプロセスにより、文書は保護され、後から簡単に真正性を検証できるようになります。

##### ステップ1: 署名オプションを設定する
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

Signature signature = new Signature("YOUR_DOCUMENT_PATH");
QrCodeSignOptions signOptions = new QrCodeSignOptions("John Smith", com.groupdocs.signature.domain.qrcodes.QrCodeTypes.QR);

signOptions.setVerticalAlignment(VerticalAlignment.Top);
signOptions.setHorizontalAlignment(HorizontalAlignment.Center);
signOptions.setWidth(100);
signOptions.setHeight(40);
```
**説明**： `QrCodeSignOptions` 特定のテキストと配置でQRコードを作成するように設定されています。必要に応じて幅と高さを調整してください。

##### ステップ2: 署名の外観をカスタマイズする
```java
import java.awt.Color;

signOptions.setForeColor(Color.RED); // QRコードの色を設定する
com.groupdocs.signature.domain.SignatureFont signatureFont = new com.groupdocs.signature.domain.SignatureFont();
signatureFont.setSize(12);
signatureFont.setFamilyName("Comic Sans MS");
signOptions.setFont(signatureFont);
```
**説明**フォントと色をカスタマイズすると、視覚的な識別性が向上します。

##### ステップ3：文書に署名する
```java
import java.util.ArrayList;
import java.util.List;

List<String> signatureIds = new ArrayList<>();
List<com.groupdocs.signature.domain.BaseSignature> signedSignatures = signature.sign("YOUR_OUTPUT_PATH", signOptions).getSucceeded();

for (com.groupdocs.signature.domain.BaseSignature temp : signedSignatures) {
    signatureIds.add(temp.getSignatureId());
}
```
**説明**このステップでは、ドキュメントに署名し、将来の参照用に署名 ID を保存します。

### QRコード署名で文書を検証
#### 概要
検証は、文書が正当に署名されていることを確認するものです。文書内のQRコード署名を検証する方法は次のとおりです。

##### ステップ1: 検証オプションを設定する
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();

verifyOptions.setEncodeType(QrCodeTypes.QR);
verifyOptions.setText("John Smith"); // 確認テキスト
verifyOptions.setAllPages(false); 
verifyOptions.setPageNumber(1);
```
**説明**検証オプションでは、検索する QR コードの種類とテキストを指定し、署名が期待どおりであることを確認します。

##### ステップ2: 検証を実行する
```java
boolean isValid = signature2.verify(verifyOptions).isValid();
System.out.println("Is Signature Valid? " + isValid);
```
**説明**ドキュメントに条件に一致する有効な QR コードが含まれているかどうかを確認します。

### QRコード署名のドキュメントを検索
#### 概要
ドキュメント内の既存の署名を探す必要がある場合があります。GroupDocs.Signatureを使用して署名を検索する方法をご紹介します。

##### ステップ1: 検索オプションを設定する
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import com.groupdocs.signature.options.search.QrCodeSearchOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeSearchOptions searchOptions = new QrCodeSearchOptions();
searchOptions.setAllPages(true);
```
**説明**これにより、ツールがすべてのページをスキャンして QR コード署名を探すように設定されます。

##### ステップ2: 検索を実行する
```java
List<QrCodeSignature> signatures = signature2.search(QrCodeSignature.class, searchOptions);

for (QrCodeSignature qrSignature : signatures) {
    System.out.println("Found Signature ID: " + qrSignature.getSignatureId());
}
```
**説明**ドキュメント内にあるすべての QR コード署名を取得します。

### ドキュメントのQRコード署名を更新する
#### 概要
署名を更新するには、位置やサイズなどのプロパティを変更します。手順は以下のとおりです。

##### ステップ1: 更新用の署名を準備する
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.io.ByteArrayOutputStream;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
List<QrCodeSignature> signaturesToUpdate = new ArrayList<>();

// 「signatures」は検索から得られたQrCodeSignatureオブジェクトのリストであると仮定します。
for (QrCodeSignature qrSignature : signatures) {
    qrSignature.setLeft(qrSignature.getLeft() + 100);
    qrSignature.setTop(qrSignature.getTop() + 100);
    qrSignature.setWidth(200);
    qrSignature.setHeight(50);
    signaturesToUpdate.add(qrSignature);
}
```
**説明**各署名の位置とサイズを調整します。

##### ステップ2: ドキュメントを更新する
```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature2.update(outputStream, signaturesToUpdate);
```
**説明**変更された QR コード署名でドキュメントが更新されます。

### IDによるドキュメントQRコード署名の削除
#### 概要
署名が不要になった場合や誤って追加された場合は、削除が必要になる場合があります。署名の固有IDを使用して削除する方法は次のとおりです。

##### ステップ1: 削除する署名を特定する
```java
import com.groupdocs.signature.domain.SignatureCollection;
import java.util.Arrays;

SignatureCollection signaturesToDelete = signature2.search(QrCodeSignature.class);
Arrays.stream(signaturesToDelete).forEach(signature -> {
    if (signature.getSignatureId().equals("YOUR_SIGNATURE_ID")) {
        signature.delete();
    }
});
```
**説明**一意の ID で QR コード署名を検索して削除します。

## 結論
このガイドでは、GroupDocs.Signatureを使用してJavaでQRコード署名を使用してドキュメントを保護する方法について説明しました。これらの手順に従うことで、ドキュメントが安全に署名され、その真正性を簡単に検証できるようになります。