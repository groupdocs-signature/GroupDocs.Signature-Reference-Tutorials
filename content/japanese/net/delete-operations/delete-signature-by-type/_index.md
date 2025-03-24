---
title: 種類ごとに署名を削除
linktitle: 種類ごとに署名を削除
second_title: GroupDocs.Signature .NET API
description: GroupDocs.Signature を使用して、.NET ドキュメント内の署名をタイプ別に簡単に削除し、ドキュメント管理の効率を高める方法を学びます。
weight: 12
url: /ja/net/delete-operations/delete-signature-by-type/
---
## 導入
今日のデジタル時代では、効率的な文書管理の必要性が最も重要です。契約書を扱うビジネスプロフェッショナルであっても、法的文書を処理する個人であっても、ファイルの信頼性と整合性を確保することは非常に重要です。 GroupDocs.Signature for .NET は、ドキュメント内の署名をシームレスに管理するための強力なソリューションを提供します。このチュートリアルでは、GroupDocs.Signature for .NET を使用して署名をタイプ別に削除するプロセスを詳しく説明し、ドキュメント管理タスクを効率化するためのステップバイステップのガイドを提供します。
## 前提条件
始める前に、次の前提条件が満たされていることを確認してください。
- C# プログラミング言語の基本的な知識。
- 開発環境にインストールされた .NET 用の GroupDocs.Signature。からダウンロードできます[ここ](https://releases.groupdocs.com/signature/net/).
- システムにインストールされている Visual Studio などの統合開発環境 (IDE)。
- デモンストレーションを目的とした署名を含むサンプル文書。
## 名前空間のインポート
まず、必要な名前空間をプロジェクトにインポートしてください。これにより、GroupDocs.Signature for .NET が提供する機能に簡単にアクセスできるようになります。
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```
## ステップ 1: ファイル パスを定義する
まず、入力ドキュメントのパスと、変更されたドキュメントが保存される出力ディレクトリを定義します。
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteBySignatureType", fileName);
```
必ず交換してください`"Your Document Directory"`ドキュメントが保存されている実際のディレクトリ パスに置き換えます。
## ステップ 2: ソース ファイルをコピーする
以来、`Delete`この方法は同じドキュメントに対して機能するため、ソース ファイルのコピーを作成してオリジナルを保存することをお勧めします。
```csharp
File.Copy(filePath, outputFilePath, true);
```
この手順により、ドキュメントに加えられた変更が元のファイルに影響を与えないことが保証されます。
## ステップ 3: 署名を削除する
ここで、を初期化します`Signature`オブジェクトを出力ファイルのパスに置き換え、タイプごとに署名の削除に進みます。
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    DeleteResult result = signature.Delete(SignatureType.QrCode);
```
ここでは、ドキュメントから QR コード署名を削除します。交換できます`SignatureType.QrCode`要件に応じて希望の署名タイプを使用します。
## ステップ 4: プロセスの削除結果
削除後、結果を確認して操作が成功したかどうかを判断し、関連情報を表示します。
```csharp
if (result.Succeeded.Count > 0)
{
    Console.WriteLine("Following QR-Code signatures were deleted:");
    int number = 1;
    foreach (QrCodeSignature temp in result.Succeeded)
    {
        Console.WriteLine($"Signature #{number++}: Type: {temp.SignatureType} Id:{temp.SignatureId}, Text: {temp.Text}");
    }
}
else
{
    Helper.WriteError("No QR-Code signature was deleted.");
}
```
このステップでは、削除された署名に関するフィードバックを提供することで透明性を確保します。

## 結論
結論として、GroupDocs.Signature for .NET を使用すると、ドキュメント内の署名の管理が簡素化されます。このチュートリアルで概説されている手順に従うと、署名を種類ごとに簡単に削除でき、ドキュメント管理ワークフローの効率が向上します。
## よくある質問
### 1 回の操作で複数の種類の署名を削除できますか?
はい、各タイプを反復処理し、それに応じて削除プロセスを実行することで、複数のタイプの署名を削除できます。
### GroupDocs.Signature for .NET はさまざまなドキュメント形式と互換性がありますか?
絶対に！ GroupDocs.Signature for .NET は、PDF、Word、Excel、PowerPoint などを含む幅広いドキュメント形式をサポートしています。
### 特定の基準に基づいて削除プロセスをカスタマイズできますか?
確かに！ GroupDocs.Signature for .NET は、署名の種類、テキストの内容、場所などのさまざまなパラメーターに基づいて署名の削除をカスタマイズするための広範なオプションを提供します。
### 購入前にテストできる試用版はありますか?
はい、次から無料試用版をダウンロードすることで、GroupDocs.Signature for .NET の機能を調べることができます。[ここ](https://releases.groupdocs.com/).
### GroupDocs.Signature for .NET に関する支援やサポートはどこに求めればよいですか?
質問やサポートが必要な場合は、GroupDocs.Signature フォーラムにアクセスしてください。[ここ](https://forum.groupdocs.com/c/signature/13).