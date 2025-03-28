---
title: ドキュメントからデジタル署名を削除
linktitle: ドキュメントからデジタル署名を削除
second_title: GroupDocs.Signature .NET API
description: GroupDocs.Signature for .NET を使用してドキュメントからデジタル署名を削除する方法を学びます。効率的に管理するには、ステップバイステップのガイドに従ってください。
weight: 13
url: /ja/net/delete-operations/delete-digital-signature/
---

# ドキュメントからデジタル署名を削除

## 導入
デジタル ドキュメントの世界では、信頼性とセキュリティを確保することが最も重要です。デジタル署名は、電子文書の完全性を検証する際に重要な役割を果たします。 GroupDocs.Signature for .NET は、.NET アプリケーション内のデジタル署名を効率的に管理するための強力なツールを提供します。
## 前提条件
GroupDocs.Signature for .NET を使用してドキュメントからデジタル署名を削除する前に、次のことを確認してください。
1. Visual Studio: システムに Visual Studio IDE をインストールします。
2.  GroupDocs.Signature for .NET: GroupDocs.Signature for .NET を次の場所からダウンロードしてインストールします。[ダウンロードページ](https://releases.groupdocs.com/signature/net/).
3. サンプル文書: テスト用にデジタル署名を含むサンプル文書を準備します。

## 名前空間のインポート
まず、.NET プロジェクトに必要な名前空間をインポートしてください。
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```
## ステップ 1: ファイル パスを定義する
まず、ソース ドキュメントと出力ドキュメントのファイル パスを定義します。
```csharp
string filePath = "sample.pdf"_SIGNED_DIGITAL;
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteDigital", fileName);
```
## ステップ 2: ソースドキュメントをコピーする
以来、`Delete`このメソッドは同じドキュメントで機能するため、ソース ファイルを新しい場所にコピーする必要があります。
```csharp
File.Copy(filePath, outputFilePath, true);
```
## ステップ3: 署名オブジェクトの初期化
初期化する`Signature`オブジェクトと出力ファイルのパス:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    //コードはここに入力します
}
```
## ステップ 4: デジタル署名を検索する
文書内の電子デジタル署名を検索します。
```csharp
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```
## ステップ 5: デジタル署名を削除する
デジタル署名が見つかった場合は、最初に見つかった署名を削除します。
```csharp
if (signatures.Count > 0)
{
    DigitalSignature digitalSignature = signatures[0];
    bool result = signature.Delete(digitalSignature);
    if (result)
    {
        Console.WriteLine($"Digital signature #{digitalSignature.Thumbprint} from {digitalSignature.SignTime.ToShortDateString()} was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature# {digitalSignature.Thumbprint} was not found!");
    }
}
```

## 結論
GroupDocs.Signature を使用すると、.NET アプリケーションでのデジタル署名の管理が簡単になります。上記の簡単な手順に従うことで、ドキュメントからデジタル署名をシームレスに削除し、データの整合性とセキュリティを確保できます。
## よくある質問
### 1 つの文書から複数のデジタル署名を削除できますか?
はい、コードを変更して、見つかったすべてのデジタル署名を反復処理し、それに応じて削除することができます。
### GroupDocs.Signature はデジタル以外の他の種類の署名をサポートしていますか?
はい。GroupDocs.Signature は、電子署名、デジタル署名、手書き署名など、さまざまな種類の署名をサポートしています。
### GroupDocs.Signature はエンタープライズ レベルのドキュメント管理に適していますか?
確かに、GroupDocs.Signature は個人の開発者とエンタープライズ レベルのアプリケーションの両方のニーズを満たすように設計されており、堅牢な機能と拡張性を提供します。
### デジタル署名の削除プロセスをカスタマイズできますか?
はい。GroupDocs.Signature には、特定の要件に応じて署名の削除プロセスをカスタマイズするための幅広いオプションと設定が用意されています。
### GroupDocs.Signature をテストするために利用できる試用版はありますか?
はい、無料試用版を次のサイトからダウンロードできます。[リリースページ](https://releases.groupdocs.com/).