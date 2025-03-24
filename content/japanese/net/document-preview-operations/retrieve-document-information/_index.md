---
title: 文書情報の取得
linktitle: 文書情報の取得
second_title: GroupDocs.Signature .NET API
description: GroupDocs.Signature を使用して .NET でのドキュメント管理を強化します。ドキュメント情報を段階的に取得します。さまざまな形式をサポートします。
weight: 11
url: /ja/net/document-preview-operations/retrieve-document-information/
---
## 導入
デジタル文書の分野では、信頼性と完全性を確保することが最も重要です。 GroupDocs.Signature for .NET は、.NET 環境内でドキュメントの署名を管理するための堅牢なソリューションを提供します。このチュートリアルでは、GroupDocs.Signature for .NET を使用してドキュメント情報を取得するプロセスを詳しく説明し、包括的な理解を得るために各ステップに分けて説明します。
## 前提条件
チュートリアルに入る前に、次の前提条件が満たされていることを確認してください。
1. インストール: GroupDocs.Signature for .NET をダウンロードしてインストールします。[ここ](https://releases.groupdocs.com/signature/net/).
2. .NET 環境: .NET フレームワークに関する実用的な知識を持っています。
3. ドキュメント: テスト目的でサンプル ドキュメント (例: 「sample_multiple_signatures.docx」) を準備します。

## 名前空間のインポート
ドキュメント署名の取得プロセスに進む前に、必要な名前空間をインポートします。
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```

## ステップ 1: ドキュメント ファイルのパスを設定します。
情報を取得するドキュメントのファイル パスを定義します。
```csharp
string filePath = "sample_multiple_signatures.docx";
```
## ステップ 2: 署名オブジェクトをインスタンス化します。
インスタンスを作成する`Signature`ドキュメント ファイルのパスを渡すことによってクラスを作成します。
```csharp
using (Signature signature = new Signature(filePath))
{

}
```
## ステップ 3: ドキュメント情報を取得する:
を活用してください。`GetDocumentInfo()`ドキュメントに関する包括的な情報を取得するメソッド。
```csharp
IDocumentInfo documentInfo = signature.GetDocumentInfo();
```
## ステップ 4: ドキュメントのプロパティを表示します。
形式、拡張子、サイズ、ページ数などのドキュメントのさまざまなプロパティを出力します。
```csharp
Console.WriteLine($"Document properties {Path.GetFileName(filePath)}:");
Console.WriteLine($" - format : {documentInfo.FileType.FileFormat}");
Console.WriteLine($" - extension : {documentInfo.FileType.Extension}");
Console.WriteLine($" - size : {documentInfo.Size}");
Console.WriteLine($" - page count : {documentInfo.PageCount}");
Console.WriteLine($" - Form Fields count : {documentInfo.FormFields.Count}");
Console.WriteLine($" - Text signatures count : {documentInfo.TextSignatures.Count}");
Console.WriteLine($" - Image signatures count : {documentInfo.ImageSignatures.Count}");
Console.WriteLine($" - Digital signatures count : {documentInfo.DigitalSignatures.Count}");
Console.WriteLine($" - Barcode signatures count : {documentInfo.BarcodeSignatures.Count}");
Console.WriteLine($" - QrCode signatures count : {documentInfo.QrCodeSignatures.Count}");
Console.WriteLine($" - FormField signatures count : {documentInfo.FormFieldSignatures.Count}");
foreach (PageInfo pageInfo in documentInfo.Pages)
{
   Console.WriteLine($" - page-{pageInfo.PageNumber} Width {pageInfo.Width}, Height {pageInfo.Height}");
}
```


## 結論
GroupDocs.Signature for .NET は、.NET フレームワーク内でドキュメント署名をシームレスに管理するための強力なツール スイートを提供します。このガイドで説明されている手順に従うことで、ドキュメントに関する包括的な情報を効率的に取得し、強化されたドキュメント管理機能を実現できます。

## よくある質問
### GroupDocs.Signature for .NET は複数のドキュメント形式を処理できますか?
はい、GroupDocs.Signature は、DOCX、PDF、PNG、JPEG などを含む幅広いドキュメント形式をサポートしています。
### GroupDocs.Signature for .NET の試用版はありますか?
はい、試用版はこちらからアクセスできます。[ここ](https://releases.groupdocs.com/).
### GroupDocs.Signature for .NET はデジタル署名をサポートしていますか?
はい、GroupDocs.Signature はデジタル署名を強力にサポートし、ドキュメントの信頼性と整合性を保証します。
### GroupDocs.Signature for .NET に関する追加のドキュメントとサポートはどこで入手できますか?
包括的なドキュメントを参照できます[ここ](https://tutorials.groupdocs.com/signature/net/)サポートについては、GroupDocsフォーラムをご覧ください。[ここ](https://forum.groupdocs.com/c/signature/13).
### GroupDocs.Signature for .NET の一時ライセンスを取得できますか?
はい、一時ライセンスは購入できます[ここ](https://purchase.groupdocs.com/temporary-license/).