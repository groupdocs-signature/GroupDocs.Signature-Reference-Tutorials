---
title: デジタル署名による署名
linktitle: デジタル署名による署名
second_title: GroupDocs.Signature .NET API
description: GroupDocs.Signature を使用して .NET でドキュメントにデジタル署名する方法を学びます。この包括的なチュートリアルでセキュリティと信頼性を強化します。
type: docs
weight: 12
url: /ja/net/advanced-signature-techniques/sign-with-digital/
---
## 導入
デジタル署名は、電子文書の信頼性と完全性を保証する上で重要な役割を果たします。 .NET 開発の領域では、GroupDocs.Signature はデジタル署名をアプリケーションにシームレスに統合するための強力なソリューションを提供します。このチュートリアルでは、GroupDocs.Signature for .NET を使用してデジタル署名を使用してドキュメントに署名するプロセスについて説明します。
## 前提条件
実装に入る前に、次の前提条件が満たされていることを確認してください。
1.  GroupDocs.Signature for .NET: GroupDocs.Signature for .NET を次の場所からダウンロードしてインストールします。[ダウンロードページ](https://releases.groupdocs.com/signature/net/).
2. デジタル証明書: ドキュメントの署名に使用されるデジタル証明書 (.pfx) を取得します。証明書をお持ちでない場合は、自己署名証明書を作成するか、信頼できる認証局から取得できます。
3. 署名する文書: デジタル署名する文書 (PDF など) を準備します。ドキュメントにアクセスして変更するために必要な権限があることを確認してください。
4. 署名画像: オプションで、文書に埋め込まれる署名の画像を提供できます。これにより、デジタル署名にパーソナライズされたタッチが追加されます。

## 名前空間のインポート
まず、必要な名前空間を C# コードにインポートしましょう。
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## ステップ 1: ファイル パスとオプションを指定する
署名するドキュメントのファイル パス、署名画像 (該当する場合)、およびデジタル証明書を定義します。
```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string imagePath = "signature_handwrite.jpg";
string certificatePath = "YourSignature.pfx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithDigital", fileName);
```
## ステップ 2: 署名オブジェクトを初期化する
インスタンスを作成する`Signature`署名するドキュメントのパスを渡すことでクラスを作成します。
```csharp
using (Signature signature = new Signature(filePath))
{
    //デジタル署名オプションを定義する
    DigitalSignOptions options = new DigitalSignOptions(certificatePath)
    {
        ImageFilePath = imagePath, //画像ファイルのパスを設定します (オプション)
        Left = 50,                 //署名位置の X 座標を設定します
        Top = 50,                  //署名位置のY座標を設定します
        PageNumber = 1,            //署名するページ番号を指定してください
        Password = "1234567890"    //証明書のパスワードを設定します (必要な場合)
    };
    //ステップ 3: 文書に署名する
    SignResult result = signature.Sign(outputFilePath, options);
    //ステップ 4: 結果の表示
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## 結論
このチュートリアルでは、GroupDocs.Signature for .NET でデジタル署名を使用してドキュメントに署名する方法を検討しました。これらの簡単な手順に従うことで、電子ドキュメントのセキュリティと信頼性を強化し、改ざん防止と法的拘束力を確保できます。
## よくある質問
### デジタル署名とは何ですか?
デジタル署名は、デジタル文書またはメッセージの信頼性と完全性を検証するために使用される暗号化技術です。
### 自己署名証明書を使用して GroupDocs.Signature でドキュメントに署名できますか?
はい、OpenSSL や Microsoft の MakeCert などのツールで生成された自己署名証明書を使用してドキュメントに署名できます。
### GroupDocs.Signature はさまざまなドキュメント形式と互換性がありますか?
はい。GroupDocs.Signature は、PDF、Word、Excel、PowerPoint などを含む幅広いドキュメント形式をサポートしています。
### デジタル署名の外観をカスタマイズできますか?
絶対に！ GroupDocs.Signature を使用すると、位置、サイズ、外観など、デジタル署名のさまざまな側面をカスタマイズできます。
### GroupDocs.Signature はエンタープライズ レベルのアプリケーションに適していますか?
はい、GroupDocs.Signature は堅牢な機能と拡張性を提供するため、エンタープライズ レベルの文書署名アプリケーションにとって理想的な選択肢となります。