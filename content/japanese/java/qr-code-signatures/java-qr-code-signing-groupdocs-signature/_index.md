---
"date": "2025-05-08"
"description": "GroupDocs.Signatureを使用してJava QRコード署名を実装する方法を学びます。ドキュメントのセキュリティを強化し、署名オプションを設定し、Javaアプリケーションにカスタム暗号化を適用します。"
"title": "Java QR コード署名ガイド&#58; GroupDocs.Signature でドキュメントを保護する"
"url": "/ja/java/qr-code-signatures/java-qr-code-signing-groupdocs-signature/"
"weight": 1
---

# GroupDocs.Signature for Java を使用した Java QR コード署名の実装

## 導入

JavaアプリケーションにQRコードを埋め込むことで、デジタルドキュメントのセキュリティを強化します。GroupDocs.Signature for Javaを活用することで、ドキュメントの真正性とトレーサビリティを効果的に確保できます。このガイドでは、カスタムデータ署名の作成、QRコード署名オプションの設定、そして強力な暗号化によるドキュメントのセキュリティ保護について解説します。

**学習内容:**
- GroupDocs.Signature を使用してカスタム データ署名クラスを作成する方法
- Java アプリケーションでの QR コード署名オプションの構成
- QRコードで文書に署名し、カスタム暗号化を適用する

前提条件を確認し、この機能をプロジェクトに統合してみましょう。

## 前提条件

始める前に、開発環境に必要なライブラリと依存関係が設定されていることを確認してください。

### 必要なライブラリとバージョン

GroupDocs.Signature for Java を実装するには、次の依存関係を含めます。

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
implementation 'com.groupdocs:groupdocs-signation:23.12'
```

最新バージョンを直接ダウンロードすることもできます。 [GroupDocs.Signature for Java リリース](https://releases。groupdocs.com/signature/java/).

### 環境設定要件

- 動作する Java 開発キット (JDK) がインストールされていることを確認します。
- IntelliJ IDEA や Eclipse などの統合開発環境 (IDE) をセットアップします。

### 知識の前提条件

- Java プログラミングとオブジェクト指向の概念に関する基本的な理解。
- Maven または Gradle を使用して依存関係を処理することに関する知識。

## Java 用 GroupDocs.Signature の設定

開始するには、上記のインストール手順に従って、ビルド構成に GroupDocs.Signature を含め、プロジェクトに GroupDocs.Signature を設定します。

### ライセンス取得手順

GroupDocs はさまざまなライセンス オプションを提供しています。
- **無料トライアル**制限なしですべての機能をテストします。
- **一時ライセンス**評価目的でライセンスを取得します。
- **購入**商用利用のための完全なライセンスを取得します。

ダウンロード後、GroupDocs.Signature を次のように初期化します。

```java
import com.groupdocs.signature.Signature;

class InitializeGroupDocs {
    public static void main(String[] args) {
        Signature signature = new Signature("path/to/your/document");
        // これで、署名オブジェクトを使用してドキュメントを操作できるようになります。
    }
}
```

## 実装ガイド

主要な機能に焦点を当てて、実装プロセスを管理しやすいセクションに分割してみましょう。

### カスタムデータ署名クラス

#### 概要
ID、作成者、署名日、その他の要素といった署名データを保存するカスタムクラスを作成します。これにより、必要なメタデータがすべて署名内にカプセル化されます。

#### ステップバイステップの実装

**DocumentSignatureDataクラスを定義する**

```java
import com.groupdocs.signature.domain.extensions.serialization.FormatAttribute;
import java.util.Date;
import java.math.BigDecimal;

class DocumentSignatureData {
    @FormatAttribute(propertyName = "SignID")
    public String ID; // 署名の一意の識別子
    
    public String getID() { return ID; }
    public void setID(String value) { ID = value; }
    
    @FormatAttribute(propertyName = "SAuth")
    public final String Author; // 文書の著者
    
    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }
    
    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public final Date Signed = new Date(); // 署名日時
    
    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }
    
    @FormatAttribute(propertyName = "SDFact", propertyFormat = "N2")
    public final BigDecimal DataFactor = new BigDecimal(0.01); // 署名のための追加データ要素
    
    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```

**説明：**
- **フォーマット属性**シリアル化をカスタマイズするためにプロパティに注釈を付けます。
- **プロパティ**一意の ID、作成者名、署名日、データ要素などの重要な詳細を取得します。

### QRコード署名オプションの設定

#### 概要
QR コード署名オプションを構成して、サイズ、配置、パディングなど、ドキュメント上での QR コードの表示方法を定義します。

#### ステップバイステップの実装

**QrCodeSignOptionsConfig クラスを定義する**

```java
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

class QrCodeSignOptionsConfig {
    public static QrCodeSignOptions setupQrCodeSignOptions(DocumentSignatureData documentSignature) {
        QrCodeSignOptions options = new QrCodeSignOptions();
        
        // カスタムデータオブジェクトをQRコードにシリアル化する
        options.setData(documentSignature);
        
        // QRコードの種類を指定
        options.setEncodeType(QrCodeTypes.QR);
        
        // 配置のためのパディングを設定する
        Padding padding = new Padding();
        padding.setRight(10); // 右パディング（ピクセル単位）
        padding.setBottom(10); // ピクセル単位の下パディング
        options.setMargin(padding);
        
        // QRコードのサイズと位置を定義する
        options.setHeight(100);
        options.setWidth(100);
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        options.setHorizontalAlignment(HorizontalAlignment.Right);
        
        return options;
    }
}
```

**説明：**
- **Qrコードサインオプション**QR コードのサイズや位置など、QR コードの表示方法を管理します。
- **パディング**ドキュメント内の配置を調整します。

### QRコードとカスタム暗号化によるドキュメント署名

#### 概要
QRコードとカスタム暗号化を組み合わせることで、文書に安全に署名できます。これにより、データの整合性と機密性が確保されます。

#### ステップバイステップの実装

**QRコードで文書に署名する**

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.exception.GroupDocsSignatureException;

import java.util.UUID;

class SignDocumentWithQRCode {
    public static void signDocument(String filePath, String outputFilePath) throws Exception {
        try {
            Signature signature = new Signature(filePath);

            // カスタムXOR暗号化戦略
            IDataEncryption encryption = new CustomXOREncryption();

            // カスタムドキュメント署名データオブジェクトを構成する
            DocumentSignatureData documentSignature = new DocumentSignatureData();
            documentSignature.setID(UUID.randomUUID().toString());
            documentSignature.setAuthor(System.getenv("USERNAME"));
            documentSignature.setSigned(new Date());
            documentSignature.setDataFactor(new BigDecimal("11.22"));

            // QRコードオプションの設定
            QrCodeSignOptions options = QrCodeSignOptionsConfig.setupQrCodeSignOptions(documentSignature);

            // QRコード内のデータに暗号化を適用する
            options.setDataEncryption(encryption);

            // 文書に署名して保存する
            signature.sign(outputFilePath, options);
        } catch (Exception e) {
            throw new GroupDocsSignatureException(e.getMessage());
        }
    }
}
```

**説明：**
- **カスタムXORE暗号化**QR コード データを保護するためのカスタム暗号化戦略を実装します。
- **UUID**: 各署名に一意の識別子を生成します。