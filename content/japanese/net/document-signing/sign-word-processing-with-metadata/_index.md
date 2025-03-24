---
title: メタデータを使用したサインワード処理
linktitle: メタデータを使用したサインワード処理
second_title: GroupDocs.Signature .NET API
description: GroupDocs.Signature for .NET を使用して、ワード プロセッサ ドキュメントにメタデータで署名する方法を学びます。ドキュメントの信頼性と追跡可能性を強化します。
weight: 14
url: /ja/net/document-signing/sign-word-processing-with-metadata/
---
## 導入
このチュートリアルでは、GroupDocs.Signature for .NET を使用して、ワード プロセッサ ドキュメントにメタデータで署名するプロセスについて説明します。メタデータ署名を使用すると、作成者の名前、作成日、ドキュメント ID などの追加情報をドキュメントに埋め込むことができます。
## 前提条件
始める前に、以下のものがあることを確認してください。
- .NET ライブラリの GroupDocs.Signature がインストールされています。
- ワードプロセッサドキュメント (.docx など) へのアクセス。
- C# プログラミング言語の基本的な知識。

## 名前空間のインポート
まず、必要な名前空間を C# プロジェクトにインポートする必要があります。
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## ステップ 1: ファイル パスを設定する
署名するワープロ文書のファイル パスと、署名された文書が保存される出力ファイルのパスを定義します。
```csharp
string filePath = "sample.docx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWordProcessingWithMetadata", "SignedWithMetadata.docx");
```
## ステップ 2: 署名オブジェクトを初期化する
署名するドキュメントのファイル パスを渡して、Signature オブジェクトを作成します。
```csharp
using (Signature signature = new Signature(filePath))
{
    //署名操作はここで実行されます
}
```
## ステップ 3: メタデータ署名オプションを定義する
次に、メタデータ署名オプションを作成し、さまざまなタイプのメタデータ署名を追加しましょう。
```csharp
MetadataSignOptions options = new MetadataSignOptions();
//メタデータ署名を追加する
options
    .Add(new WordProcessingMetadataSignature("Author", "Mr.Sherlock Holmes")) //文字列値
    .Add(new WordProcessingMetadataSignature("CreatedOn", DateTime.Now))      //日時値
    .Add(new WordProcessingMetadataSignature("DocumentId", 123456))           //整数値
    .Add(new WordProcessingMetadataSignature("SignatureId", 123.456D))        //二重値
    .Add(new WordProcessingMetadataSignature("Amount", 123.456M))             //10 進数値
    .Add(new WordProcessingMetadataSignature("Total", 123.456F));             //浮動小数点値
```
## ステップ 4: 文書に署名する
次に、定義されたメタデータ オプションを使用してドキュメントに署名し、署名されたドキュメントを出力ファイル パスに保存しましょう。
```csharp
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
これで、GroupDocs.Signature for .NET を使用してメタデータを含むワープロ ドキュメントに署名するプロセスは完了です。

## 結論
このチュートリアルでは、GroupDocs.Signature for .NET を使用して、メタデータを含むワープロ ドキュメントに署名する方法を学習しました。メタデータ署名によりドキュメントに貴重な情報が追加され、ドキュメントの信頼性とトレーサビリティが強化されます。
## よくある質問
### GroupDocs.Signature for .NET を使用してカスタム メタデータを含むドキュメントに署名できますか?
はい、カスタム メタデータ フィールドを定義し、それを使用してドキュメントに署名できます。
### GroupDocs.Signature for .NET はさまざまなドキュメント形式と互換性がありますか?
はい。GroupDocs.Signature は、ワープロ、PDF などを含む幅広いドキュメント形式をサポートしています。
### ユーザーの介入なしにプログラムでドキュメントに署名できますか?
確かに、GroupDocs.Signature を使用すると、アプリケーション内でドキュメント署名プロセスを自動化できます。
### GroupDocs.Signature for .NET の試用版はありますか?
はい、GroupDocs Web サイトから無料試用版を入手できます。
### GroupDocs.Signature for .NET はデジタル署名をサポートしていますか?
はい、GroupDocs.Signature はドキュメントのデジタル署名とメタデータ署名の両方をサポートしています。