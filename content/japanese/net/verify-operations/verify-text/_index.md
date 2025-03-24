---
title: テキストの検証
linktitle: テキストの検証
second_title: GroupDocs.Signature .NET API
description: GroupDocs.Signature for .NET を使用してドキュメント内のテキストを検証する方法を学びます。シームレスな統合については、段階的なチュートリアルに従ってください。
weight: 13
url: /ja/net/verify-operations/verify-text/
---

# テキストの検証

## 導入
このチュートリアルでは、GroupDocs.Signature for .NET を使用してドキュメント内のテキストを検証するプロセスを説明します。この強力なライブラリを使用すると、テキスト検証機能を .NET アプリケーションにシームレスに統合して、ドキュメントの整合性と信頼性を確保できます。
## 前提条件
始める前に、次の前提条件を満たしていることを確認してください。
1.  GroupDocs.Signature for .NET: GroupDocs.Signature for .NET がインストールされ、構成されていることを確認します。ライブラリはからダウンロードできます[ここ](https://releases.groupdocs.com/signature/net/).
2. 文書ファイル: 検証する文書ファイル (sample_multiple_signatures.docx など) を準備します。

## 名前空間のインポート
まず、必要な名前空間をプロジェクトにインポートする必要があります。
```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## ステップ1: ドキュメントファイルのパスを設定する
検証するドキュメントのファイル パスを定義します。交換する`"sample_multiple_signatures.docx"`ドキュメント ファイルへのパスを含めます。
```csharp
string filePath = "sample_multiple_signatures.docx";
```
## ステップ 2: 署名オブジェクトを初期化する
インスタンスを作成する`Signature`クラスを作成し、そのコンストラクターにファイル パスを渡します。
```csharp
using (Signature signature = new Signature(filePath))
{
    //ここに認証コードが書き込まれます
}
```
## ステップ 3: テキスト検証オプションを指定する
検証するテキスト、一致タイプ、その他のパラメーターを含むテキスト検証オプションを定義します。
```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = true, //すべてのページのテキストを確認する
    SignatureImplementation = TextSignatureImplementation.Native,
    Text = "signature", //検証対象のテキスト
    MatchType = TextMatchType.Contains //一致タイプを指定する
};
```
## ステップ 4: ドキュメントの署名を検証する
を呼び出します。`Verify`方法`Signature`オブジェクトを指定し、検証オプションを渡します。
```csharp
VerificationResult result = signature.Verify(options);
```
## ステップ5: 検証結果を処理する
検証結果の妥当性を確認し、適切な処理を行ってください。
```csharp
if(result.IsValid)
{
    Console.WriteLine($"\nDocument {filePath} was verified successfully!");
    foreach (TextSignature item in result.Succeeded)
    {
        Console.WriteLine($"\nValid signature is found with text: {item.Text}");
    }
}
else
{
    Helper.WriteError($"\nDocument {filePath} failed verification process.");
}
```

## 結論
結論として、GroupDocs.Signature for .NET はドキュメント内のテキストを検証するシームレスな方法を提供し、ドキュメントの整合性と信頼性を保証します。このチュートリアルで概説されている手順に従うことで、テキスト検証機能を .NET アプリケーションに簡単に統合できます。
## よくある質問
### GroupDocs.Signature for .NET はすべてのドキュメント形式と互換性がありますか?
はい、GroupDocs.Signature for .NET は、DOCX、PDF、XLSX などの幅広いドキュメント形式をサポートしています。
### テキスト検証基準をカスタマイズできますか?
もちろん、検証要件に合わせて、一致タイプ、ページ範囲などのさまざまなパラメーターをカスタマイズできます。
### GroupDocs.Signature for .NET はデジタル署名をサポートしていますか?
はい、GroupDocs.Signature for .NET はテキスト署名とデジタル署名の両方をサポートし、包括的な文書検証機能を提供します。
### GroupDocs.Signature for .NET に利用できる無料試用版はありますか?
はい、以下から無料トライアルを利用できます。[ここ](https://releases.groupdocs.com/).
### GroupDocs.Signature for .NET のヘルプやサポートはどこで入手できますか?
を訪問できます。[GroupDocs.Signature フォーラム](https://forum.groupdocs.com/c/signature/13)コミュニティからの支援とサポートが必要です。