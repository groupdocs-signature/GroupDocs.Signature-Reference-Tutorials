---
title: 文書から複数の署名を削除する
linktitle: 文書から複数の署名を削除する
second_title: GroupDocs.Signature .NET API
description: GroupDocs.Signature for .NET を使用して、ドキュメントから複数の署名を簡単に削除します。ドキュメント管理ワークフローを合理化します。
type: docs
weight: 15
url: /ja/net/delete-operations/delete-multiple-signatures/
---
## 導入
デジタルの世界では、文書管理にはさまざまな署名の処理が含まれることがよくあります。プログラムで文書から複数の署名を削除すると、ワークフローが合理化され、効率が向上します。 GroupDocs.Signature for .NET を使用すると、このタスクがシームレスかつ簡単になります。このチュートリアルでは、文書から複数の署名を削除するプロセスを段階的に説明します。
## 前提条件
チュートリアルに進む前に、次の前提条件を満たしていることを確認してください。
- C# プログラミング言語の基本的な理解。
- .NET ライブラリ用の GroupDocs.Signature がインストールされました。
- テスト用の複数の署名を含むサンプル文書。

## 名前空間のインポート
まず、GroupDocs.Signature for .NET の機能にアクセスするために必要な名前空間をインポートします。
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## ステップ 1: ドキュメントのパスとファイル名を定義する
複数の署名を含む文書のファイル パスを設定します。適切なファイル パスとファイル名があることを確認してください。
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
```
## ステップ 2: 処理するドキュメントをコピーする
元のドキュメントを変更しないようにするには、処理用にコピーを作成します。
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "DeleteMultiple", fileName);
File.Copy(filePath, outputFilePath, true);
```
## ステップ3: 署名オブジェクトの初期化
出力ファイルのパスを使用して Signature オブジェクトをインスタンス化します。
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    //署名処理コードはここにあります
}
```
## ステップ 4: 検索オプションを定義する
ドキュメント内の署名を識別するためのさまざまな検索オプションを定義します。オプションには、テキスト検索、画像検索、バーコード検索、QR コード検索が含まれます。
```csharp
TextSearchOptions textSearchOptions = new TextSearchOptions();
ImageSearchOptions imageSearchOptions = new ImageSearchOptions();
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions();
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions();
//リストにオプションを追加する
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textSearchOptions);
listOptions.Add(imageSearchOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
```
## ステップ 5: 署名を検索する
検索操作を実行して、定義された検索オプションに基づいてドキュメント内のすべての署名を検索します。
```csharp
SearchResult result = signature.Search(listOptions);
```
## ステップ 6: 署名を削除する
署名が見つかった場合は、削除に進みます。
```csharp
if (result.Signatures.Count > 0)
{
    //すべての署名を削除してみます
    DeleteResult deleteResult = signature.Delete(result.Signatures);
    //削除が成功したかどうかを確認する
    if(deleteResult.Succeeded.Count == result.Signatures.Count)
    {
        Console.WriteLine("\nAll signatures were successfully deleted!");                        
    }
    else
    {
        Console.WriteLine($"Successfully deleted signatures : {deleteResult.Succeeded.Count}");
        Helper.WriteError($"Not deleted signatures : {deleteResult.Failed.Count}");
    }
    //削除された署名に関する情報を表示する
    Console.WriteLine("\nList of deleted signatures:");
    int number = 1;
    foreach(BaseSignature temp in deleteResult.Succeeded)
    {
        Console.WriteLine($"Signature #{number++}: Type: {temp.SignatureType} Id:{temp.SignatureId}, Location: {temp.Left}x{temp.Top}. Size: {temp.Width}x{temp.Height}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## 結論
プログラムによって文書から複数の署名を削除することは、文書管理において重要なタスクです。 GroupDocs.Signature for .NET を使用すると、このプロセスが効率的かつ信頼性の高いものになります。このチュートリアルで概説されている手順に従うことで、署名削除機能を .NET アプリケーションに簡単に統合できます。
## よくある質問
### GroupDocs.Signature for .NET はさまざまなドキュメント形式を処理できますか?
はい、GroupDocs.Signature for .NET は、DOCX、PDF、PPTX、XLSX などを含む幅広いドキュメント形式をサポートしています。
### シグネチャ検出の検索オプションをカスタマイズすることはできますか?
もちろん、テキスト検索、画像検索、バーコード検索、QR コード検索などの検索オプションを、特定の要件に合わせてカスタマイズできます。
### GroupDocs.Signature for .NET はエラー処理メカニズムを提供しますか?
はい。ライブラリは、ドキュメント処理タスクをスムーズに実行できるように、堅牢なエラー処理機能を提供します。
### GroupDocs.Signature for .NET を他のサードパーティ ライブラリと統合できますか?
確かに、GroupDocs.Signature for .NET は他の .NET ライブラリとシームレスに統合できるように設計されており、柔軟性と拡張性を提供します。
### GroupDocs.Signature for .NET の追加のサポートとリソースはどこで見つけられますか?
 GroupDocs にアクセスできます。[フォーラム](https://forum.groupdocs.com/c/signature/13)署名関連の議論に専念し、コミュニティや専門家からの支援を求めます。