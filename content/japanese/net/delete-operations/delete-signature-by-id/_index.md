---
title: IDによる署名の削除
linktitle: IDによる署名の削除
second_title: GroupDocs.Signature .NET API
description: GroupDocs.Signature ライブラリを使用して .NET ドキュメント内の ID によって署名を削除する方法を学習します。簡単なステップバイステップのガイド。
weight: 11
url: /ja/net/delete-operations/delete-signature-by-id/
---
## 導入
このチュートリアルでは、GroupDocs.Signature for .NET を使用して ID によって署名を削除する方法を検討します。 GroupDocs.Signature for .NET は、開発者が .NET アプリケーションを使用してさまざまなドキュメント形式のデジタル署名を追加、削除、または検証できるようにする強力なライブラリです。
## 前提条件
始める前に、次の前提条件を満たしていることを確認してください。
1.  GroupDocs.Signature for .NET Library: からライブラリをダウンロードしてインストールします。[ここ](https://releases.groupdocs.com/signature/net/).
2. .NET Framework: システムに .NET Framework がインストールされていることを確認します。
3. 署名付き文書: 削除したい署名付きの文書 (DOCX、PDF など) を準備します。

## 名前空間のインポート
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## ステップ 1: ファイル パスを定義する
まず、署名を含むドキュメントのファイル パスと、変更されたドキュメントが保存される出力ファイル パスを指定します。
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteById", fileName);
```
## ステップ 2: ドキュメントをコピーする
以来、`Delete`このメソッドはドキュメントをその場で変更するため、元のドキュメントのコピーを作成することをお勧めします。
```csharp
File.Copy(filePath, outputFilePath, true);
```
## ステップ 3: ID による署名の削除
を初期化します`Signature`オブジェクトをドキュメント ファイル パスに置き換え、`Delete` ID によって署名を削除するメソッド。
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    string id = @"eff64a14-dad9-47b0-88e5-2ee4e3604e71";
    bool result = signature.Delete(id);
    if (result)
    {
        Console.WriteLine($"Signature with Id# '{id}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with id# '{id}' was not found!");
    }
}
```

## 結論
このチュートリアルでは、GroupDocs.Signature for .NET を使用して ID によって署名を削除する方法を学習しました。このライブラリは、さまざまなドキュメント形式のデジタル署名をプログラムで管理する便利な方法を提供します。
## よくある質問
### 複数の署名を一度に削除できますか?
はい、ID を反復処理して、`Delete` IDごとのメソッドです。
### GroupDocs.Signature for .NET はすべてのドキュメント形式と互換性がありますか?
GroupDocs.Signature for .NET は、PDF、DOCX、XLSX などの幅広いドキュメント形式をサポートしています。
### 署名の外観をカスタマイズできますか?
はい、署名の位置、サイズ、フォント、色などの外観をカスタマイズできます。
### 試用版はありますか?
はい、無料試用版を次からダウンロードできます。[ここ](https://releases.groupdocs.com/).
### GroupDocs.Signature for .NET のヘルプまたはサポートはどこで見つけられますか?
サポートフォーラムにアクセスできます[ここ](https://forum.groupdocs.com/c/signature/13)援助のために。