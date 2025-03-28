---
title: デジタル署名の検証
linktitle: デジタル署名の検証
second_title: GroupDocs.Signature .NET API
description: GroupDocs.Signature を使用すると、.NET でデジタル署名を簡単に検証できます。文書の信頼性と整合性を簡単に確保します。
weight: 11
url: /ja/net/verify-operations/verify-digital/
---

# デジタル署名の検証

## 導入
デジタル ドキュメントの分野では、信頼性と完全性を確保することが最も重要です。デジタル署名は、手書き署名と同等のデジタル機能を備え、電子文書の出所と完全性を検証するための安全な方法を提供します。 GroupDocs.Signature for .NET は、.NET アプリケーションでデジタル署名を操作するための強力なツールキットを提供し、デジタル署名の検証を容易にします。
## 前提条件
GroupDocs.Signature for .NET を使用した検証プロセスに入る前に、次の前提条件が満たされていることを確認してください。
### 1. GroupDocs.Signature for .NET をインストールする
まず、GroupDocs.Signature for .NET をダウンロードしてインストールします。ダウンロードリンクが見つかります[ここ](https://releases.groupdocs.com/signature/net/).
### 2. デジタル署名ファイルの取得
検証のためにデジタル署名ファイル (例: YourSignature.pfx) が必要です。このファイルとそれに関連付けられたパスワードにアクセスできることを確認してください。

## 名前空間のインポート
.NET プロジェクトで、GroupDocs.Signature 機能を利用するために必要な名前空間をインポートします。

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 1. ドキュメントパスの指定
```csharp
string filePath = "sample_multiple_signatures.docx";
```
検証するドキュメントへのパスを指定します。
## 2. 署名オブジェクトの初期化
```csharp
using (Signature signature = new Signature(filePath))
```
ドキュメントのパスをパラメータとして渡して、新しい Signature オブジェクトを作成します。
## 3. 検証オプションを設定する
```csharp
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    Contact = "Mr.Smith",
    Password = "1234567890"
};
```
DigitalVerifyOptions オブジェクトを作成し、デジタル署名ファイル (YourSignature.pfx など) へのパスと、連絡先情報やパスワードなどの追加オプションを指定します。
## 4. 署名の検証
```csharp
VerificationResult result = signature.Verify(options);
```
Signature オブジェクトの Verify メソッドを呼び出し、検証オプションを渡します。
## 5. ハンドル検証結果
```csharp
if (result.IsValid)
{
    //有効な署名が見つかりました
    foreach (DigitalSignature item in result.Succeeded)
    {
        Console.WriteLine($"\nValid signature is found.");
    }
}
else
{
    //検証に失敗しました
    Helper.WriteError($"\nDocument {filePath} failed verification process.");
}
```
検証結果が正しいかどうかを確認します。有効な場合は、成功した署名のリストを繰り返し処理します。それ以外の場合は、検証の失敗を処理します。

## 結論
結論として、GroupDocs.Signature for .NET は、.NET アプリケーションのデジタル署名を検証するプロセスを簡素化します。上記のステップバイステップ ガイドに従い、GroupDocs.Signature の強力な機能を活用することで、デジタル ドキュメントの信頼性と整合性を自信を持って確保できます。
## よくある質問
### GroupDocs.Signature は 1 つのドキュメント内の複数の署名を検証できますか?
はい、GroupDocs.Signature は単一ドキュメント内の複数の署名の検証をサポートし、包括的な検証機能を提供します。
### GroupDocs.Signature はさまざまな種類のデジタル署名ファイルと互換性がありますか?
GroupDocs.Signature は、PFX、P12 などのさまざまなデジタル署名ファイル形式をサポートし、検証プロセスの柔軟性を確保します。
### 検証プロセス中に連絡先情報などの検証オプションをカスタマイズできますか?
はい。GroupDocs.Signature では検証オプションをカスタマイズでき、ユーザーは必要に応じて連絡先情報、パスワード、その他のパラメーターを指定できます。
### GroupDocs.Signature はトラブルシューティングや支援のサポートを提供しますか?
はい、GroupDocs.Signature はフォーラムを通じて専用のサポートを提供しており、ユーザーはそこで支援を求め、洞察を共有し、問題の効果的なトラブルシューティングを行うことができます。
### GroupDocs.Signature の試用版はありますか?
はい。興味のあるユーザーは、GroupDocs.Signature の無料試用版にアクセスして、購入を決定する前にその機能を調べることができます。