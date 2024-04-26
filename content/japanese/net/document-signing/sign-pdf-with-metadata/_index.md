---
title: メタデータを使用して PDF に署名する
linktitle: メタデータを使用して PDF に署名する
second_title: GroupDocs.Signature .NET API
description: GroupDocs.Signature for .NET を使用して、メタデータを含む PDF ドキュメントに署名する方法を学びます。文書のトレーサビリティと信頼性を簡単に強化します。
type: docs
weight: 11
url: /ja/net/document-signing/sign-pdf-with-metadata/
---
## 導入
このチュートリアルでは、GroupDocs.Signature for .NET を使用して、メタデータを含む PDF ドキュメントに署名する方法を学習します。 PDF にメタデータを追加すると、作成者、作成日、ドキュメント ID など、ドキュメントに関する追加情報が提供されます。
## 前提条件
始める前に、以下のものがあることを確認してください。
1.  GroupDocs.Signature for .NET: 次からダウンロードできます。[ここ](https://releases.groupdocs.com/signature/net/).
2. PDF ドキュメント: 署名できるサンプル PDF ファイルを用意します。
3. C# プログラミングの基本知識: コード例を理解するには、C# 構文に精通している必要があります。
## 名前空間のインポート
まず、必要なクラスとメソッドにアクセスするために必要な名前空間をインポートしていることを確認します。
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## ステップ1: PDFドキュメントを読み込む
署名する PDF ドキュメントを読み込みます。
```csharp
string filePath = "sample.pdf";
```
## ステップ 2: 出力ファイルのパスを指定する
メタデータを含む署名付き PDF が保存される出力ファイルのパスを定義します。
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
```
## ステップ 3: 署名インスタンスの作成
PDF ドキュメントへのパスを指定して、Signature インスタンスを初期化します。
```csharp
using (Signature signature = new Signature(filePath))
{
    //署名関連のコードがここに入力されます
}
```
## ステップ 4: メタデータ オプションを定義する
MetadataSignOptions を作成し、それぞれの値を持つメタデータ フィールドを追加します。
```csharp
MetadataSignOptions options = new MetadataSignOptions();
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) //文字列値
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       //日時値
    .Add(new PdfMetadataSignature("DocumentId", 123456))            //整数値
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         //二重値
    .Add(new PdfMetadataSignature("Amount", 123.456M))              //10 進数値
    .Add(new PdfMetadataSignature("Total", 123.456F));              //浮動小数点値
```
## ステップ 5: 文書に署名する
指定されたメタデータ オプションを使用して PDF ドキュメントに署名し、署名されたドキュメントを保存します。
```csharp
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## 結論
このチュートリアルでは、GroupDocs.Signature for .NET を使用してメタデータを含む PDF ドキュメントに署名する方法について説明しました。ステップバイステップのガイドに従うことで、作成者、作成日などのメタデータ情報を PDF ファイルに簡単に追加でき、ユーティリティとトレーサビリティが強化されます。
## よくある質問
### PDF ドキュメントにカスタム メタデータ フィールドを追加できますか?
はい、GroupDocs.Signature for .NET を使用してフィールド名とそれに対応する値を指定することで、カスタム メタデータ フィールドを追加できます。
### GroupDocs.Signature for .NET は、.NET Framework のすべてのバージョンと互換性がありますか?
GroupDocs.Signature for .NET は、さまざまなバージョンの .NET Framework と互換性があり、柔軟性と統合の容易さを保証します。
### GroupDocs.Signature は、PDF 以外の他のドキュメント形式の署名をサポートしていますか?
はい。GroupDocs.Signature は、Word、Excel、PowerPoint などを含む幅広いドキュメント形式をサポートしています。
### GroupDocs.Signature for .NET を使用して複数のドキュメントに一括で署名できますか?
はい、ファイルのリストを繰り返し処理し、プログラムで署名プロセスを適用することで、複数のドキュメントに一括で署名できます。
### GroupDocs.Signature ユーザーはテクニカル サポートを利用できますか?
はい、GroupDocs はフォーラムを通じて専用のテクニカル サポートを提供しています。サポートフォーラムにアクセスできます[ここ](https://forum.groupdocs.com/c/signature/13).