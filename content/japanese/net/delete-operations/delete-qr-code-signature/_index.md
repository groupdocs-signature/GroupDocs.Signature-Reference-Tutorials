---
"description": "ステップバイステップの開発者ガイドを使用して、GroupDocs.Signature for .NET を使用してドキュメントから QR コード署名を簡単に削除する方法を学びます。"
"linktitle": "ドキュメントからQRコード署名を削除する"
"second_title": "GroupDocs.Signature .NET API"
"title": ".NET でドキュメントから QR コード署名を削除する方法"
"url": "/ja/net/delete-operations/delete-qr-code-signature/"
"weight": 16
---

# 文書からQRコード署名を削除する方法

## 導入

ドキュメントからQRコード署名をプログラムで削除する必要があったことはありませんか？古くなった情報を整理する場合でも、再配布用のドキュメントを準備する場合でも、ドキュメント署名を効果的に管理できることは、.NET開発者にとって重要なスキルです。

この分かりやすいガイドでは、GroupDocs.Signature for .NETを使ってドキュメントからQRコード署名を削除する方法を詳しく説明します。この強力なライブラリを使えば署名管理が簡単になり、ドキュメント操作の課題に悩まされることなく、優れたアプリケーションの構築に集中できます。

## 始める前に必要なもの

コードに進む前に、すべての準備が整っていることを確認しましょう。

- GroupDocs.Signature for .NET: プロジェクトにライブラリをインストールする必要があります。こちらから直接ダウンロードできます。 [GroupDocsリリースページ](https://releases。groupdocs.com/signature/net/).
- QR コードを含むドキュメント: 練習として、削除する QR コード署名が少なくとも 1 つ含まれているドキュメントを準備します。
- 基本的な C# の知識: 私たちの例を理解するには、C# の基礎を理解している必要があります。

これらの前提条件が整ったら、QR コードの削除を開始する準備が整います。

## 適切な名前空間でプロジェクトを設定する

まず最初に、コードがスムーズに動作するために必要な名前空間をインポートしましょう。

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

これらのインポートにより、GroupDocs.Signature ライブラリの必要なすべての機能と、ファイル処理に不可欠ないくつかの .NET クラスにアクセスできるようになります。

## ステップ1：ファイルはどこにありますか？ドキュメントパスの設定

まず、ドキュメントが保存されている場所と、変更したバージョンを保存する場所を定義しましょう。

```csharp
// ドキュメント ディレクトリへのパス。
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);

// 変更されたドキュメントの出力ファイル パスを定義します。
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);

// Delete メソッドは同じドキュメントで機能するため、ソース ファイルをコピーします。
File.Copy(filePath, outputFilePath, true);
```

元の文書のコピーを作成していることに注意してください。署名の削除プロセスはファイルを直接変更するため、元の文書を常に保存しておくことが重要です。

## ステップ2: 使用する署名オブジェクトを作成する

ここで、ドキュメントに接続する Signature オブジェクトを作成します。

```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // QR コード署名を検索するためのオプションを作成します。
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    
    // ドキュメント内の QR コード署名を検索します。
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```

このコードは、ドキュメントでSignatureオブジェクトを初期化し、そこに含まれるQRコード署名を検索します。検索の結果、見つかったすべてのQRコード署名のリストが返されます。

## ステップ 3: 削除する QR コードはありますか?

何かを削除しようとする前に、実際に QR コードが存在するかどうかを確認する必要があります。

```csharp
    if (signatures.Count > 0)
    {
        // ドキュメント内で見つかった最初の QR コード署名を取得します。
        QrCodeSignature qrCodeSignature = signatures[0];
```

このシンプルなチェックにより、ドキュメント内に少なくとも1つのQRコード署名が含まれている場合にのみ処理を続行できます。この例では、最初に見つかったQRコードを対象としていますが、必要に応じて複数の署名を処理するように簡単に変更できます。

## ステップ4：ドキュメントからQRコードを削除する

さて、いよいよメインイベント、QR コードを実際に削除します。

```csharp
        // ドキュメントから QR コード署名を削除します。
        bool result = signature.Delete(qrCodeSignature);
        
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Console.WriteLine($"Signature was not deleted from the document! Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```

このコードは署名を削除し、操作が成功したかどうかのフィードバックを提供します。このフィードバックは、デバッグやコードが期待どおりに動作しているかどうかを確認する上で非常に重要です。

## 私たちは何を達成したのでしょうか?

おめでとうございます！GroupDocs.Signature for .NETを使ってドキュメントからQRコード署名を削除する方法を習得しました。このスキルは、アプリケーションにおけるドキュメント管理の可能性を大きく広げます。

わずか数行のコードで、古くなった、または不要な QR コード署名を削除してドキュメントをプログラム的にクリーンアップし、ドキュメントに常に関連情報のみが含まれるようにできるようになりました。

## よくある質問

### 複数のQRコードを一度に削除できますか？

もちろんです！最初に見つかった署名を削除するだけでなく、署名のリスト全体を反復処理して、次のように各署名を削除することもできます。

```csharp
foreach(var qrSignature in signatures)
{
    signature.Delete(qrSignature);
}
```

### GroupDocs.Signature で管理できる他の種類の署名にはどのようなものがありますか?

GroupDocs.Signature は非常に汎用性が高く、次のようなさまざまな署名タイプをサポートしています。
- テキスト署名
- 画像署名
- バーコード署名
- デジタル署名
- その他にも多数あります!

### これはすべてのドキュメント形式で機能しますか?

GroupDocs.Signature は、次のような幅広いドキュメント形式に対応しています。
- PDF文書
- Microsoft Word文書
- Excelスプレッドシート
- PowerPointプレゼンテーション
- その他多数

### すべてを削除するのではなく、特定の QR コードを検索できますか?

はい！ `QrCodeSearchOptions` クラスは、検索を絞り込むための様々なプロパティを提供します。例えば、特定のテキストを含むQRコードや特定の形式でエンコードされたQRコードを検索できます。

### 購入前に GroupDocs.Signature を試す方法はありますか?

はい、無料試用版は以下からダウンロードできます。 [GroupDocsウェブサイト](https://releases.groupdocs.com/) コミットする前に、特定のユースケースでテストしてください。