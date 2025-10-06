---
"date": "2025-05-08"
"description": "GroupDocs.Signature for JavaでQRコード暗号化とデジタル署名を使用してPDFを保護する方法を学びましょう。ドキュメントのセキュリティを効果的に強化できます。"
"title": "GroupDocs.Signature を使用して Java で QR コード暗号化による安全な PDF 署名を実装する"
"url": "/ja/java/qr-code-signatures/secure-pdf-signing-qr-code-groupdocs-java/"
"weight": 1
type: docs
---
# GroupDocs.Signature を使用して Java で QR コード暗号化による安全な PDF 署名を実装する方法

今日のデジタル時代において、文書内の機密情報の保護は極めて重要です。サイバー脅威の増加により、データ暗号化は文書管理において不可欠な要素となっています。このチュートリアルでは、GroupDocs.Signature for Javaを使用してQRコード暗号化による安全なPDF署名を実装する方法を説明します。この記事を読み終える頃には、アプリケーションに強力なセキュリティ機能を統合できるようになります。

## 学習内容:
- Javaにおける対称データ暗号化の理解
- カスタム署名クラスの作成
- カスタムデータと配置によるQRコード署名の設定
- GroupDocs.Signature を統合して安全な PDF 署名を実現

準備はできましたか？ さあ、始めましょう！

## 前提条件
始める前に、以下のものを用意してください。
- **Java 開発キット (JDK):** バージョン8以上。
- **Maven または Gradle:** 依存関係管理用。プロジェクトの設定に応じて選択してください。
- **Javaプログラミングの知識:** Java におけるオブジェクト指向プログラミングの基本的な理解。

## Java 用 GroupDocs.Signature の設定
GroupDocs.Signature を使い始めるには、プロジェクトに依存関係として追加する必要があります。このライブラリは、デジタル署名とドキュメントの暗号化を管理するための強力なツールを提供します。

### Mavenのセットアップ
次の依存関係を `pom.xml` ファイル：
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradleのセットアップ
Gradleユーザーの場合は、 `build.gradle` ファイル：
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### 直接ダウンロード
または、最新バージョンを以下からダウンロードしてください。 [GroupDocs.Signature for Java リリース](https://releases。groupdocs.com/signature/java/).

### ライセンス取得
GroupDocs.Signatureの無料トライアルで機能を評価することができます。長期間ご利用いただくには、ライセンスのご購入、またはウェブサイトから一時ライセンスの申請をご検討ください。

## 実装ガイド
このガイドは、データの暗号化、カスタム署名の作成、QR コード署名の構成をカバーする主要なセクションに分かれています。

### 対称アルゴリズムによるデータ暗号化
データを暗号化することで、転送中および保存中のデータの安全性を確保できます。GroupDocs.Signatureを使用して対称暗号化を設定する方法は次のとおりです。

#### 対称暗号化の設定
1. **必要なパッケージをインポートします。**
   ```java
   import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
   ```
2. **暗号化オブジェクトを初期化します。**
   暗号化には安全なキーとソルトを使用してください。 `"YOUR_SECURE_KEY"` あなた自身の鍵を使って。
   ```java
   String key = "YOUR_SECURE_KEY";
   String salt = "YOUR_SECURE_SALT";

   IDataEncryption encryption = new SymmetricEncryption(
       SymmetricAlgorithmType.Rijndael, 
       key, 
       salt
   );
   ```
   - **対称アルゴリズムタイプ.Rijndael:** 使用する対称アルゴリズムのタイプを指定します。
   - **キーとソルト:** これらがアプリケーションに対して一意かつ安全であることを確認してください。

### カスタムデータ署名クラス
カスタムクラスを作成すると、署名プロパティを効果的に管理できます。手順は以下のとおりです。

#### 定義する `DocumentSignatureData` クラス
```java
class DocumentSignatureData {
    private String ID;
    private String Author;
    private Date Signed = new Date();
    private BigDecimal DataFactor = new BigDecimal(0.01);

    public String getID() { return ID; }
    public void setID(String value) { ID = value; }

    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }

    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }

    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```
- **ID、著者、署名:** これらのフィールドには署名のメタデータが保存されます。
- **データファクター:** アプリケーションのロジックに関連する数値を保持します。

### QRコード署名オプション
QRコードは情報をコンパクトに埋め込む手段です。カスタムデータと暗号化を設定してご利用ください。

#### QRコード署名の設定
1. **初期化 `Signature` 物体：**
   ```java
   import com.groupdocs.signature.Signature;
   
   Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY");
   ```
2. **QR コード オプションを構成します。**
   ```java
   import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
   import com.groupdocs.signature.options.sign.QrCodeSignOptions;
   import java.util.UUID;

   DocumentSignatureData documentSignature = new DocumentSignatureData();
   documentSignature.setID(UUID.randomUUID().toString());
   documentSignature.setAuthor(System.getenv("USERNAME"));
   documentSignature.setDataFactor(new BigDecimal("11.22"));

   QrCodeSignOptions options = new QrCodeSignOptions();
   options.setData(documentSignature);
   options.setEncodeType(QrCodeTypes.QR);
   options.setDataEncryption(encryption); // 暗号化オブジェクトを使用する
   options.setHeight(100);
   options.setWidth(100);
   options.setVerticalAlignment(com.groupdocs.signature.domain.enums.VerticalAlignment.Bottom);
   options.setHorizontalAlignment(com.groupdocs.signature.domain.enums.HorizontalAlignment.Right);

   import com.groupdocs.signature.domain.Padding;
   Padding padding = new Padding();
   padding.setRight(10);
   padding.setBottom(10);
   options.setMargin(padding);
   ```
   - **エンコードタイプ:** QR コードの形式を指定します。
   - **配置と余白:** ドキュメント上での QR コードの表示方法をカスタマイズします。

### 使用例
設定したオプションを使用してドキュメントに署名するには:
```java
signature.sign("YOUR_OUTPUT_DIRECTORY/QRCodeEncryptedObject.pdf\