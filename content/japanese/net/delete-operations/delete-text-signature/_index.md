---
title: テキスト署名の削除
linktitle: テキスト署名の削除
second_title: GroupDocs.Signature .NET API
description: GroupDocs.Signature for .NET を使用して、ドキュメントからテキスト署名を簡単に削除します。ドキュメント管理タスクを簡素化します。
weight: 17
url: /ja/net/delete-operations/delete-text-signature/
---

# テキスト署名の削除

## 導入
GroupDocs.Signature for .NET は、開発者が電子署名機能を .NET アプリケーションにシームレスに統合できるようにする強力なライブラリです。ドキュメント管理システム、契約署名プラットフォーム、または署名機能を必要とするその他のアプリケーションを構築している場合でも、GroupDocs.Signature for .NET はプロセスを簡素化するための包括的なツール セットを提供します。
## 前提条件
GroupDocs.Signature for .NET の使用に入る前に、次の前提条件が満たされていることを確認してください。
### 1..NET開発環境
マシン上に .NET 開発環境がセットアップされていることを確認してください。 .NET SDK は Microsoft Web サイトからダウンロードしてインストールできます。
### 2. .NET 用の GroupDocs.Signature
提供されたリンクから GroupDocs.Signature for .NET をダウンロードしてインストールします。[.NET 用の GroupDocs.Signature をダウンロードする](https://releases.groupdocs.com/signature/net/)
### 3. テスト用の文書
署名削除機能をテストするために使用するサンプル文書 (Word 文書、PDF など) を準備します。

## 名前空間のインポート
プロジェクトで GroupDocs.Signature for .NET の使用を開始するには、必要な名前空間をインポートします。
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

ここで、文書からテキスト署名を削除するプロセスを複数のステップに分けてみましょう。
## ステップ 1: ファイル パスを定義する
まず、入力ドキュメント、出力ドキュメント、およびファイル名のパスを定義します。
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteText", fileName);
```
## ステップ 2: ソース ファイルをコピーする
以来、`Delete`このメソッドは同じドキュメントで機能するため、ソース ファイルを新しい場所にコピーします。
```csharp
File.Copy(filePath, outputFilePath, true);
```
## ステップ3: 署名オブジェクトの初期化
初期化する`Signature`出力ファイルのパスを使用してオブジェクトを作成します。
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    //テキスト署名を削除するコードはここにあります
}
```
## ステップ 4: テキスト署名を検索する
次を使用して文書内のテキスト署名を検索します。`TextSearchOptions`.
```csharp
TextSearchOptions options = new TextSearchOptions();
List<TextSignature> signatures = signature.Search<TextSignature>(options);
```
## ステップ 5: テキスト署名を削除する
テキスト署名が見つかった場合は、最初の署名を削除します。
```csharp
if (signatures.Count > 0)
{
    TextSignature textSignature = signatures[0];
    bool result = signature.Delete(textSignature);
    if (result)
    {
        Console.WriteLine($"Signature with Text '{textSignature.Text}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with Text '{textSignature.Text}' was not found!");
    }
}
```

## 結論
結論として、GroupDocs.Signature for .NET は、プログラムによってドキュメントからテキスト署名を削除する簡単なアプローチを提供します。このチュートリアルで概説されている手順に従うことで、開発者は署名削除機能を .NET アプリケーションにシームレスに統合し、ドキュメント管理プロセスを強化し、電子署名標準への準拠を確保できます。
## よくある質問
### GroupDocs.Signature for .NET は 1 つのドキュメント内で複数の署名を処理できますか?
はい。GroupDocs.Signature for .NET は、ドキュメント内の複数の署名の検出と削除をサポートしています。
### テスト目的で利用できる試用版はありますか?
はい、提供されたリンクから試用版にアクセスできます。[無料トライアル](https://releases.groupdocs.com/)
### GroupDocs.Signature for .NET はさまざまなドキュメント形式をサポートしていますか?
はい。GroupDocs.Signature for .NET は、Word、PDF、Excel などを含む幅広いドキュメント形式をサポートしています。
### 署名を検索するときに検索オプションをカスタマイズできますか?
確かに、GroupDocs.Signature for .NET にはさまざまな検索オプションが用意されており、開発者は要件に応じて検索条件をカスタマイズできます。
### 導入中に問題が発生した場合はどこでサポートを受けられますか?
 GroupDocs コミュニティ フォーラムからサポートを求めることができます。[サポートフォーラム](https://forum.groupdocs.com/c/signature/13)