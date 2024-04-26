---
title: メタデータを含む画像に署名する
linktitle: メタデータを含む画像に署名する
second_title: GroupDocs.Signature .NET API
description: GroupDocs.Signature を使用して .NET でメタデータを含む画像に署名する方法を学びます。簡単、効率的、カスタマイズ可能なメタデータ署名ソリューション。
type: docs
weight: 10
url: /ja/net/document-signing/sign-image-with-metadata/
---
## 導入
GroupDocs.Signature for .NET を使用すると、開発者はメタデータを含むイメージに効率的に署名できます。このチュートリアルでは、プロセスを段階的に説明します。
## 前提条件
始める前に、以下のものがあることを確認してください。
1. GroupDocs.Signature for .NET: GroupDocs.Signature パッケージを .NET プロジェクトにインストールします。からダウンロードできます[ここ](https://releases.groupdocs.com/signature/net/).   
2. 画像ファイル: メタデータを使用して署名する画像ファイルを準備します。

## 名前空間のインポート
必要な名前空間を C# コードにインポートしてください。
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## ステップ 1: 画像ファイルをロードする
まず、イメージ ファイルへのパスと、メタデータを含む署名付きイメージの出力ディレクトリを指定します。
```csharp
string filePath = "sample.png";            
string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
```
## ステップ 2: メタデータ署名を作成する
次に、さまざまなメタデータ署名を作成し、オプションの署名コレクションに追加します。
```csharp
using (Signature signature = new Signature(filePath))
{
    ushort imgsMetadataId = 41996;
    MetadataSignOptions options = new MetadataSignOptions();
    options
        .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Scherlock Holmes")) //文字列値
        .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          //日付時刻の値
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                //整数値
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              //二重値
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              //10 進数値
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             //浮動小数点値
    
    //文書に署名してファイルに保存する
    SignResult result = signature.Sign(outputFilePath, options);
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## 結論
このチュートリアルでは、GroupDocs.Signature for .NET を使用してメタデータを含む画像に署名する方法を学習しました。これらの手順に従うことで、メタデータ署名を .NET アプリケーションに簡単に組み込むことができます。

## よくある質問
### GroupDocs.Signature for .NET を使用して、メタデータを含む複数のイメージに署名できますか?
はい、各画像ファイルを反復処理してメタデータ署名を適用することで、メタデータを使用して複数の画像に署名できます。
### GroupDocs.Signature for .NET の試用版はありますか?
はい、試用版は次からダウンロードできます。[ここ](https://releases.groupdocs.com/).
### GroupDocs.Signature for .NET は画像以外のファイル形式をサポートしていますか?
はい。GroupDocs.Signature は、PDF、Word、Excel などを含むさまざまなファイル形式をサポートしています。
### メタデータ署名の外観をカスタマイズできますか?
はい、フォント サイズ、色、位置など、メタデータ署名の外観をカスタマイズできます。
### GroupDocs.Signature for .NET のサポートはどこで入手できますか?
 GroupDocs.Signature フォーラムからサポートを受けることができます[ここ](https://forum.groupdocs.com/c/signature/13).