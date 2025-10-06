---
"description": "GroupDocs.Signatureを使用して、.NETアプリケーションに安全なデジタル署名検証を実装します。ドキュメント認証のための完全なコード例を含むステップバイステップガイドです。"
"linktitle": "デジタル署名の検証"
"second_title": "GroupDocs.Signature .NET API"
"title": "文書内のデジタル署名を検証する"
"url": "/ja/net/verify-operations/verify-digital/"
"weight": 11
type: docs
---
## 導入

デジタル署名は、現代のビジネスプロセスにおいて、文書の真正性、整合性、そして否認不能性を確保する上で重要な役割を果たします。従来の手書き署名とは異なり、デジタル署名は暗号化技術を用いて署名者の身元を確認し、署名後に文書が改ざんされていないことを保証します。

GroupDocs.Signature for .NETは、開発者が.NETアプリケーションに堅牢なデジタル署名検証を実装するための包括的なツールキットを提供します。この詳細なチュートリアルでは、GroupDocs.Signature for .NETを使用してドキュメント内のデジタル署名を検証するプロセスを解説します。

## 前提条件

デジタル署名検証機能を実装する前に、次の前提条件が満たされていることを確認してください。

1. GroupDocs.Signature for .NET: ライブラリをダウンロードしてインストールします。 [GroupDocs.Signature for .NET リリース](https://releases。groupdocs.com/signature/net/).
2. .NET 開発環境: Visual Studio または互換性のある .NET 開発環境。
3. デジタル証明書: ドキュメントの署名に使用されたデジタル証明書ファイル (例: .pfx)、または信頼されたチェーンに属する証明書。
4. 検証用文書: 検証が必要なデジタル署名を含む文書。

## 必要な名前空間をインポートする

まず、GroupDocs.Signature 機能にアクセスするために必要な名前空間をインポートします。

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

デジタル署名を検証するプロセスを、明確で管理しやすいステップに分解してみましょう。

## ステップ1: ドキュメントパスを指定する

```csharp
// デジタル署名を含む文書へのパス
string filePath = "sample_multiple_signatures.docx";
```

例のパスを、デジタル署名を含むドキュメントへの実際のパスに置き換えます。

## ステップ2: 署名オブジェクトの初期化

```csharp
// ドキュメントパスを渡してSignatureクラスのインスタンスを作成する
using (Signature signature = new Signature(filePath))
{
    // 検証コードはここに実装されます
}
```

Signature クラスは、GroupDocs.Signature API のすべての操作のメイン エントリ ポイントです。

## ステップ3: デジタル検証オプションを構成する

```csharp
// セットアップ検証オプション
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    Contact = "Mr.Smith",     // 予想される署名者連絡先
    Password = "1234567890",  // 必要な場合は証明書のパスワード
    AllPages = true           // すべてのページの署名を確認する
};
```

検証オプションでは以下を指定できます。
- デジタル証明書ファイルのパス
- 署名予定者の連絡先情報
- 証明書がパスワードで保護されている場合は、証明書のパスワード
- 検証するページ範囲（デフォルトでは全ページ）

## ステップ4: 検証プロセスを実行する

```csharp
// 検証を実行する
VerificationResult result = signature.Verify(options);
```

これにより、指定したオプションに基づいて検証プロセスが実行されます。

## ステップ5：プロセス検証結果

```csharp
// 検証結果を確認し、それに応じて処理する
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid digital signatures!");
    
    // 有効な署名の詳細を表示する
    foreach (DigitalSignature digitalSignature in result.Succeeded)
    {
        Console.WriteLine($"\nValid signature found:");
        Console.WriteLine($"Signer: {digitalSignature.Subject}");
        Console.WriteLine($"Issuer: {digitalSignature.Issuer}");
        Console.WriteLine($"Valid From: {digitalSignature.ValidFrom}");
        Console.WriteLine($"Valid To: {digitalSignature.ValidTo}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    
    // 必要に応じて失敗した署名に関する情報を表示する
    foreach (DigitalSignature failedSignature in result.Failed)
    {
        Console.WriteLine($"Failed signature reason: {failedSignature.Comments}");
    }
}
```

このコードは、検証が成功したかどうかを確認し、検証された署名に関する詳細情報を提供します。

## 完全な例

デジタル署名の検証を示す完全な動作例を次に示します。

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace GroupDocs.Signature.Examples
{
    class Program
    {
        static void Main(string[] args)
        {
            // ドキュメントパス
            string filePath = "sample_multiple_signatures.docx";
            
            try
            {
                // 署名インスタンスを初期化する
                using (Signature signature = new Signature(filePath))
                {
                    // セットアップ検証オプション
                    DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
                    {
                        Contact = "Mr.Smith",
                        Password = "1234567890"
                    };
                    
                    // 文書の署名を検証する
                    VerificationResult result = signature.Verify(options);
                    
                    // プロセス検証結果
                    if (result.IsValid)
                    {
                        Console.WriteLine($"Document {filePath} contains valid digital signatures!");
                        
                        foreach (DigitalSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature found.");
                            Console.WriteLine($"Subject: {item.Subject}");
                            Console.WriteLine($"Comments: {item.Comments}");
                            Console.WriteLine($"Sign Time: {item.SignTime}");
                        }
                    }
                    else
                    {
                        Console.WriteLine($"\nDocument {filePath} failed verification process.");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

## 高度な検証シナリオ

GroupDocs.Signature は、より複雑な検証シナリオ向けに追加のオプションを提供します。

### 複数のデジタル署名の検証

```csharp
// 検証オプションのリストを作成する
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// 最初の証明書検証オプションを追加する
listOptions.Add(new DigitalVerifyOptions("Certificate1.pfx")
{
    Contact = "John Smith"
});

// 2番目の証明書検証オプションを追加する
listOptions.Add(new DigitalVerifyOptions("Certificate2.pfx")
{
    Contact = "Jane Doe"
});

// 複数のオプションで検証する
VerificationResult result = signature.Verify(listOptions);
```

### 特定のページの署名の検証

```csharp
// 最初のページのみデジタル署名を検証する
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    AllPages = false,
    PageNumber = 1
};
```

### タイムスタンプと認証局検証の使用

```csharp
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    ValidateTimeStampOnly = true,   // タイムスタンプのみを検証する
    CertificateAuth = CertificateAuthType.Standard  // 署名者の証明書を検証する
};
```

## デジタル署名検証のベストプラクティス

1. 適切な証明書管理: 証明書ファイルを安全に保存し、パスワードを適切に管理します。
2. 証明書の検証: 証明書チェーンの検証を実装して、証明書自体が有効であることを確認します。
3. エラー処理: 検証の失敗を適切に管理するために、堅牢なエラー処理を実装します。
4. ログ記録: 監査およびコンプライアンスの目的で検証の試行と結果をログに記録します。
5. 定期的な証明書の更新: 証明書が期限切れになる前に更新されていることを確認します。

## 一般的な問題のトラブルシューティング

### 無効な証明書
- 証明書ファイルのパスが正しいことを確認してください
- 証明書のパスワードが正しいことを確認してください
- 証明書の有効期限が切れていないか確認する

### 署名が見つかりません
- 文書に実際にデジタル署名が含まれていることを確認する
- 正しいページをチェックしていることを確認してください

### 検証の失敗
- 署名後に文書が変更されたかどうかを確認する
- 署名者の証明書が信頼できる証明書チェーンに含まれていることを確認する

## 結論

GroupDocs.Signature for .NETは、ドキュメント内のデジタル署名を検証するための強力かつ柔軟なソリューションを提供します。このステップバイステップガイドに従うことで、.NETアプリケーションに堅牢なデジタル署名検証を実装し、ドキュメントの真正性と整合性を確保できます。

デジタル署名検証は、現代のビジネス環境における安全なドキュメントワークフローの重要な要素です。GroupDocs.Signatureを使用すれば、包括的なAPIを活用して様々な検証シナリオに対応できるため、最小限の労力で確実にこの機能を実装できます。

## よくある質問

### GroupDocs.Signature は、Adobe Acrobat を使用して署名された PDF ドキュメントの署名を検証できますか?
はい、GroupDocs.Signature は、Adobe Acrobat やその他の準拠 PDF ソフトウェアで作成された PDF ドキュメント内の標準デジタル署名を検証できます。

### GroupDocs.Signature はドキュメントのタイムスタンプの検証をサポートしていますか?
はい、API は、デジタル署名検証プロセスの一部としてドキュメントのタイムスタンプを検証するオプションを提供します。

### 複数ページの文書の特定のページの署名を検証できますか?
はい、ドキュメント全体ではなく特定のページの署名をチェックするように検証オプションを設定できます。

### GroupDocs.Signature は、単一のドキュメント内の複数の署名の検証をサポートしていますか?
はい、GroupDocs.Signature は単一のドキュメント内の複数のデジタル署名を検証し、署名ごとに詳細な結果を提供できます。

### 異なる証明機関の証明書を使用して作成された署名を検証することは可能ですか?
はい、GroupDocs.Signature は、信頼できる証明書チェーン内にある限り、異なる証明機関の証明書を使用して作成された署名の検証をサポートします。

### 関連リソース
* [GroupDocs.Signature API リファレンス](https://reference.groupdocs.com/signature/net/)
* [GroupDocs.Signature ダウンロード](https://releases.groupdocs.com/signature/net/)
* [GitHub のコード例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [ドキュメント](https://docs.groupdocs.com/signature/net/)
* [製品ページ](https://products.groupdocs.com/signature/net/)
* [ブログ記事](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [サポートフォーラム](https://forum.groupdocs.com/c/signature/13)
* [一時ライセンス](https://purchase.groupdocs.com/temporary-license/)