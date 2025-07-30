---
"description": "GroupDocs.Signature for .NET でドキュメント内のデジタル署名の検索をマスターしましょう。詳細なステップバイステップガイドで、ドキュメントのセキュリティと検証を強化しましょう。"
"linktitle": "デジタル署名を検索する"
"second_title": "GroupDocs.Signature .NET API"
"title": "文書内のデジタル署名を検索する"
"url": "/ja/net/signature-searching/search-for-digital-signatures/"
"weight": 11
---

## 導入

今日のデジタル環境において、企業や組織にとって、ドキュメントの真正性と整合性の確保は極めて重要です。デジタル署名は、ドキュメントの真正性を検証し、不正な変更を検出するための堅牢なメカニズムを提供します。GroupDocs.Signature for .NETは、様々なドキュメント形式のデジタル署名を扱うための包括的なソリューションを提供し、開発者が署名機能を.NETアプリケーションにシームレスに統合できるようにします。

このチュートリアルでは、GroupDocs.Signature for .NET を使用してドキュメント内のデジタル署名を検索するプロセスを、詳細な説明と実用的なコード例とともに説明します。

## 前提条件

実装の詳細に進む前に、次の前提条件が満たされていることを確認してください。

1. GroupDocs.Signature for .NET: ライブラリをダウンロードしてインストールします。 [ここ](https://releases。groupdocs.com/signature/net/).
   
2. 開発環境: Visual Studio または任意の IDE を使用して .NET 開発環境をセットアップします。
   
3. サンプル ドキュメント: テスト目的でデジタル署名を含むサンプル ドキュメントを準備します。

4. 基本知識: C# プログラミング言語と .NET フレームワークの基礎に関する知識。

## 名前空間のインポート

まず、GroupDocs.Signature for .NET によって提供される機能にアクセスするために必要な名前空間をインポートします。

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

ここで、デジタル署名を検索するプロセスを明確で管理しやすいステップに分解してみましょう。

## ステップ1: 署名オブジェクトの初期化

まず、 `Signature` クラスにドキュメントへのパスを渡します:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // デジタル署名を検索するためのコードがここに追加されます
}
```

## ステップ2：デジタル署名を検索する

次に、 `Search` 方法 `SignatureType.Digital` 文書内のデジタル署名を検索するためのパラメータ:

```csharp
// 文書内のデジタル署名を検索する
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```

## ステップ3: 処理と結果の表示

最後に、検索結果を処理し、見つかったデジタル署名に関する関連情報を表示します。

```csharp
Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
foreach (var digitalSignature in signatures)
{
    Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
    Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
    Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
    Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
    Console.WriteLine();
}
```

## 完全な例

ドキュメント内のデジタル署名を検索する方法を示す完全な実用的な例を次に示します。

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SearchDigitalSignatures
{
    class Program
    {
        static void Main(string[] args)
        {
            // ドキュメントパス
            string filePath = "sample_multiple_signatures.docx";
            
            // 署名インスタンスを初期化する
            using (Signature signature = new Signature(filePath))
            {
                // 文書内のデジタル署名を検索する
                List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
                
                // 検索結果を表示
                Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
                
                if (signatures.Count > 0)
                {
                    foreach (var digitalSignature in signatures)
                    {
                        Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
                        Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
                        Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
                        Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
                        Console.WriteLine();
                    }
                }
                else
                {
                    Console.WriteLine("No digital signatures found in the document.");
                }
            }
        }
    }
}
```

## 詳細検索オプション

よりターゲットを絞った検索には、 `DigitalSearchOptions` 検索条件をカスタマイズするには:

```csharp
// デジタル検索オプションを作成する
DigitalSearchOptions options = new DigitalSearchOptions()
{
    // 特定のページのみを検索する（例：ページ 1 と 2）
    PageNumber = 1,
    PagesSetup = new PagesSetup() { Pages = new List<int> { 1, 2 } },
    
    // デジタル署名のコメントでフィルタリング
    Comments = "Approved",
    
    // 検索の日付と時間の範囲を設定する
    SignDateTimeFrom = new DateTime(2022, 1, 1),
    SignDateTimeTo = DateTime.Now
};

// 特定のオプションで検索
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(options);
```

## 証明書情報の操作

デジタル署名には、アクセスして検証できる貴重な証明書情報が含まれています。

```csharp
foreach (var digitalSignature in signatures)
{
    if (digitalSignature.Certificate != null)
    {
        // 証明書のプロパティにアクセスする
        Console.WriteLine($"Certificate Valid From: {digitalSignature.Certificate.NotBefore}");
        Console.WriteLine($"Certificate Valid To: {digitalSignature.Certificate.NotAfter}");
        
        // 証明書が有効な日付範囲内であるかどうかを確認する
        bool isDateValid = DateTime.Now >= digitalSignature.Certificate.NotBefore && 
                          DateTime.Now <= digitalSignature.Certificate.NotAfter;
        
        Console.WriteLine($"Certificate Date Validity: {isDateValid}");
        
        // 証明書発行者の詳細にアクセスする
        Console.WriteLine($"Certificate Issuer: {digitalSignature.Certificate.IssuerName}");
    }
}
```

## 結論

GroupDocs.Signature for .NETは、ドキュメント内のデジタル署名を検索・検証するための強力で柔軟なソリューションを提供します。このチュートリアルでは、.NETアプリケーションにデジタル署名検索機能を実装するプロセスを段階的に解説し、ドキュメントのセキュリティと整合性検証を強化するための知識を習得しました。

GroupDocs.Signature を活用することで、デジタル ドキュメントの信頼性と整合性を確保し、ビジネス プロセスにおける信頼とコンプライアンスを促進する強力なドキュメント管理システムを構築できます。

## よくある質問

### GroupDocs.Signature はデジタル署名の有効性を検証できますか?

はい、GroupDocs.Signatureは検索プロセス中にデジタル署名を自動的に検証し、検証ステータスを `IsValid` の財産 `DigitalSignature` クラス。

### デジタル署名の検索をサポートするドキュメント形式はどれですか?

GroupDocs.Signature は、PDF、Microsoft Office ドキュメント (Word、Excel、PowerPoint)、OpenOffice 形式など、さまざまな形式でのデジタル署名の検索をサポートしています。

### パスワードで保護された文書内のデジタル署名を検索できますか?

はい、パスワードで保護された文書内のデジタル署名は、初期化時にパスワードを入力することで検索できます。 `Signature` 物体：

```csharp
LoadOptions loadOptions = new LoadOptions() { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // デジタル署名を検索する
}
```

### デジタル署名が特定の人物によって作成されたかどうかを確認するにはどうすればよいですか?

証明書のサブジェクト名やその他のプロパティを調べて、署名者の身元を確認できます。

```csharp
foreach (var signature in signatures)
{
    if (signature.Certificate?.SubjectName?.Contains("John Doe") == true)
    {
        Console.WriteLine("Found signature by John Doe");
    }
}
```

### デジタル署名証明書から公開鍵を抽出できますか?

はい、証明書のプロパティを通じて公開キー情報にアクセスできます。

```csharp
if (signature.Certificate != null)
{
    // 公開鍵情報にアクセスする
    Console.WriteLine($"Public Key: {signature.Certificate.GetPublicKeyString()}");
}
```

## 参照

* [APIリファレンス](https://reference.groupdocs.com/signature/net/)
* [コード例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [製品ドキュメント](https://docs.groupdocs.com/signature/net/)
* [製品ページ](https://products.groupdocs.com/signature/net/)
* [最新バージョンをダウンロード](https://releases.groupdocs.com/signature/net/)
* [ブログ記事](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [サポートフォーラム](https://forum.groupdocs.com/c/signature/13)
* [一時ライセンス](https://purchase.groupdocs.com/temporary-license/)