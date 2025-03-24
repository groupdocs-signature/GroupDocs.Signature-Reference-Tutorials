---
title: ドキュメントから QR コード署名を削除する
linktitle: ドキュメントから QR コード署名を削除する
second_title: GroupDocs.Signature .NET API
description: GroupDocs.Signature for .NET を使用してドキュメントから QR コード署名を削除する方法を学びます。効率的な署名管理については、ステップバイステップのガイドに従ってください。
weight: 16
url: /ja/net/delete-operations/delete-qr-code-signature/
---
## 導入
このチュートリアルでは、GroupDocs.Signature for .NET を使用してドキュメントから QR コード署名を削除するプロセスを説明します。 QR コード署名を効果的に削除するには、次の段階的な手順に従ってください。
## 前提条件
始める前に、次の前提条件を満たしていることを確認してください。
-  GroupDocs.Signature for .NET: GroupDocs.Signature ライブラリが .NET プロジェクトにインストールされていることを確認してください。からダウンロードできます[ここ](https://releases.groupdocs.com/signature/net/).
- QRコード署名付き文書：削除したいQRコード署名を含む文書を用意します。
- C# の基本知識: C# プログラミング言語の基本を理解します。

## 名前空間のインポート
コードに入る前に、必要な名前空間を C# ファイルにインポートします。
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## ステップ 1: ファイル パスを定義する
```csharp
//ドキュメントディレクトリへのパス。
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
//変更されたドキュメントの出力ファイルのパスを定義します。
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);
// Delete メソッドは同じドキュメントに対して機能するため、ソース ファイルをコピーします。
File.Copy(filePath, outputFilePath, true);
```
## ステップ 2: 署名オブジェクトを初期化する
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // QR コード署名を検索するためのオプションを作成します。
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    //ドキュメント内の QR コード署名を検索します。
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```
## ステップ3: QRコード署名の存在を確認する
```csharp
    if (signatures.Count > 0)
    {
        //ドキュメント内で見つかった最初の QR コード署名を取得します。
        QrCodeSignature qrCodeSignature = signatures[0];
```
## ステップ4: QRコード署名を削除する
```csharp
        //ドキュメントから QR コード署名を削除します。
        bool result = signature.Delete(qrCodeSignature);
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```
おめでとうございます! GroupDocs.Signature for .NET を使用して、ドキュメントから QR コード署名を正常に削除しました。

## 結論
このチュートリアルでは、GroupDocs.Signature for .NET を使用してドキュメントから QR コード署名を削除する方法を学習しました。提供されている手順に従うことで、.NET アプリケーション内で署名を効率的に管理および操作できます。
## よくある質問
### ドキュメントから複数の QR コード署名を削除できますか?
はい、コードを変更してすべての QR コード署名を反復処理し、それに応じて削除することができます。
### GroupDocs.Signature は QR コード以外の種類の署名もサポートしていますか?
はい、GroupDocs.Signature は、テキスト、画像、バーコードなど、さまざまな署名タイプをサポートしています。
### GroupDocs.Signature はすべてのドキュメント形式と互換性がありますか?
GroupDocs.Signature は、PDF、Microsoft Word、Excel、PowerPoint などを含む幅広いドキュメント形式をサポートしています。
### 署名の検索オプションをカスタマイズできますか?
はい、要件に応じて検索オプションを調整して、文書内の特定の署名を見つけることができます。
### GroupDocs.Signature の試用版はありますか?
はい。GroupDocs.Signature の無料試用版には、次のサイトからアクセスできます。[ここ](https://releases.groupdocs.com/).