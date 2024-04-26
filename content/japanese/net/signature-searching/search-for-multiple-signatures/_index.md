---
title: 複数の署名の検索
linktitle: 複数の署名の検索
second_title: GroupDocs.Signature .NET API
description: 効率的なドキュメントのセキュリティと整合性のために、GroupDocs.Signature を使用して .NET ドキュメント内の複数の署名を検索する方法を学びます。
type: docs
weight: 14
url: /ja/net/signature-searching/search-for-multiple-signatures/
---
## 導入
GroupDocs.Signature for .NET は、開発者が .NET アプリケーションを使用して一般的なドキュメント形式のさまざまな種類の署名を追加、検索、削除できる強力なライブラリです。このチュートリアルでは、GroupDocs.Signature for .NET を使用してドキュメント内の複数の署名を検索することに焦点を当てます。
## 前提条件
始める前に、次の前提条件を満たしていることを確認してください。
- Visual Studio がシステムにインストールされている。
- C# プログラミング言語の基本的な理解。
- プロジェクトにインストールされている .NET ライブラリの GroupDocs.Signature。からダウンロードできます[ここ](https://releases.groupdocs.com/signature/net/).

## 名前空間のインポート
まず、GroupDocs.Signature for .NET によって提供されるクラスとメソッドにアクセスするために必要な名前空間をインポートする必要があります。
```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## ステップ 1: ドキュメントをロードする
複数の署名を検索する文書をロードします。正しいファイル パスを指定していることを確認してください。
```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    //コードはここに入力します
}
```
## ステップ 2: 検索オプションを定義する
テキスト、デジタル、バーコード、QR コード、メタデータなど、さまざまなタイプの署名の検索オプションを定義します。一致するテキスト、一致タイプ、すべてのページにわたる検索などの検索基準を指定できます。
```csharp
//検索オプションを定義する
TextSearchOptions textOptions = new TextSearchOptions()
{
    AllPages = true
};
DigitalSearchOptions digitalOptions = new DigitalSearchOptions()
{
    AllPages = true
};
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions()
{
    AllPages = true,
    Text = "123456",
    MatchType = TextMatchType.Exact
};
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions()
{
    AllPages = true,
    Text = "John",
    MatchType = TextMatchType.Contains
};
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```
## ステップ 3: 検索オプションをリストに追加する
定義された検索オプションをリストに追加します。
```csharp
//リストにオプションを追加する
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
listOptions.Add(metadataOptions);
listOptions.Add(digitalOptions);
```
## ステップ 4: 署名を検索する
定義された検索オプションを使用して、ドキュメント内の署名を検索します。
```csharp
//文書内の署名を検索する
SearchResult result = signature.Search(listOptions);
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains following signatures.");
    foreach (var resSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found at page {resSignature.PageNumber} with type {resSignature.SignatureType} and Id#: {resSignature.SignatureId}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## 結論
このチュートリアルでは、GroupDocs.Signature for .NET を使用してドキュメント内の複数の署名を検索する方法を学びました。提供された手順に従うことで、ドキュメント内のさまざまな種類の署名を効率的に見つけて、ドキュメントのセキュリティと整合性を強化できます。
## よくある質問
### さまざまな文書形式の署名を検索できますか?
はい、GroupDocs.Signature for .NET は、Word、PDF、Excel などを含む幅広いドキュメント形式をサポートしています。
### 署名の検索条件をカスタマイズすることはできますか?
もちろん、テキストの完全一致の指定やすべてのページにわたる検索など、要件に応じて検索条件をカスタマイズできます。
### GroupDocs.Signature for .NET はデジタル署名をサポートしていますか?
はい、デジタル署名だけでなく、テキスト、バーコード、QR コード署名などの他のタイプも検索できます。
### 署名検索機能を .NET アプリケーションに簡単に統合できますか?
はい。GroupDocs.Signature for .NET は、統合プロセスを簡素化する簡単な API を提供します。
### 追加のサポートや支援はどこで入手できますか?
 GroupDocs.Signature フォーラムにアクセスしてください。[ここ](https://forum.groupdocs.com/c/signature/13)ご質問やサポートがございましたら。