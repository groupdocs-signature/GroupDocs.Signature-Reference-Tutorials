---
"date": "2025-05-07"
"description": "GroupDocs.Signatureを使用して.NETでPDFにデジタル署名する方法（タイムスタンプの追加やドキュメントの認証など）を学び、ドキュメントの整合性と信頼性を確保します。"
"title": "GroupDocs.Signature for .NET を使用してタイムスタンプと証明書付きの .NET デジタル署名を実装する方法"
"url": "/ja/net/digital-signatures/net-digital-signatures-timestamp-certification-groupdocs/"
"weight": 1
---

# GroupDocs.Signature for .NET を使用してタイムスタンプと証明書付きの .NET デジタル署名を実装する方法

## 導入

.NETでデジタル署名を使用してPDFドキュメントのセキュリティを強化したいとお考えですか？GroupDocs.Signature for .NETを使えば、真正性、整合性、否認防止性を容易に確保できます。信頼できるサードパーティサイトからのタイムスタンプを追加したり、法令遵守のためにドキュメントを認証したりする必要がある場合でも、この強力なライブラリがプロセスを簡素化します。

このチュートリアルでは、GroupDocs.Signature for .NET を使用してPDFファイルにデジタル署名し、署名にタイムスタンプを付与する方法を説明します。また、これらのドキュメントをデジタル署名で認証する方法についても説明します。このガイドを最後までお読みいただくことで、これらの機能をアプリケーションに実装するための包括的な理解が得られます。

**学習内容:**
- GroupDocs.Signature for .NET のセットアップ
- タイムスタンプ付きデジタル署名の実装
- PDF文書をデジタル認証する
- パフォーマンスの最適化とベストプラクティス

始める前に前提条件を確認しましょう。

## 前提条件

始める前に、以下のものを用意してください。

1. **必要なライブラリと依存関係**
   - GroupDocs.Signature for .NET: このライブラリは、アプリケーションにデジタル署名を実装するために不可欠です。
   - .NET Framework (4.7.2 以降) または .NET Core 3.0 以上

2. **環境設定要件**
   - Visual Studio のような開発環境で、C# プロジェクトを作成して実行できます。

3. **知識の前提条件**
   - C# プログラミングの基本的な理解。
   - .NET アプリケーションでのファイル パスと I/O 操作の処理に関する知識。

## GroupDocs.Signature を .NET 用にセットアップする

GroupDocs.Signature をプロジェクトに統合するには、次の手順に従います。

**.NET CLI の使用:**

```bash
dotnet add package GroupDocs.Signature
```

**パッケージ マネージャー コンソール:**

```powershell
Install-Package GroupDocs.Signature
```

**NuGet パッケージ マネージャー UI:**
NuGet パッケージ マネージャーで「GroupDocs.Signature」を検索し、最新バージョンをインストールします。

### ライセンス取得
- **無料トライアル:** GroupDocs.Signature の機能を試すには、まず無料トライアルをご利用ください。
- **一時ライセンス:** 一時ライセンスを取得して、制限なしで機能を評価します。
- **購入：** 長期使用の場合はフルライセンスを購入してください。

環境を設定したら、ライブラリを初期化して構成し、ドキュメントの署名を開始します。

## 実装ガイド

デジタル署名へのタイムスタンプの追加とPDF文書の認証という2つの主要機能について解説します。各セクションでは、コードスニペットと解説を用いて、手順を追って説明します。

### タイムスタンプ付きデジタル署名

この機能を使用すると、信頼できるサードパーティのタイムスタンプ サーバーを使用して、時間の経過に伴う署名の有効性を確保しながら、PDF にデジタル署名することができます。

#### ステップ1: 署名オブジェクトの初期化
まず、 `Signature` ドキュメントへのパスを指定してクラスを作成します。

```csharp
string filePath = "@YOUR_DOCUMENT_DIRECTORY/sample.pdf";
using (Signature signature = new Signature(filePath))
{
    // さらなる手順はここに追加されます
}
```

#### ステップ2: PdfDigitalSignatureを構成する
作成して設定する `PdfDigitalSignature` 連絡先情報、場所、署名理由などの必要な詳細を含むオブジェクト:

```csharp
PdfDigitalSignature pdfDigitalSignature = new PdfDigitalSignature()
{
    ContactInfo = "Contact",
    Location = "Location",
    Reason = "Reason"
};
```

#### ステップ3: タイムスタンプの詳細を設定する
サードパーティのサーバーへのURLを指定してタイムスタンプを設定します。この場合、 `freetsa.org`：

```csharp
pdfDigitalTimestamp = new TimeStamp("https://freetsa.org/tsr", "", "");
pdfDigitalSignature.TimeStamp = pdfDigitalTimestamp;
```

#### ステップ4: デジタル署名オプションを構成する
デジタル証明書のパスとパスワード、および署名の配置設定を指定して、署名オプションを設定します。

```csharp
digitalSignOptions = new DigitalSignOptions(certificatePath)
{
    Password = "1234567890",
    Signature = pdfDigitalSignature,
    VerticalAlignment = VerticalAlignment.Bottom,
    HorizontalAlignment = HorizontalAlignment.Right
};
```

#### ステップ5：文書に署名して結果を取得する
署名プロセスを実行し、署名されたドキュメントを指定されたパスに保存し、結果を出力します。

```csharp
SignResult signResult = signature.Sign(outputFilePathSigned, digitalSignOptions);
Console.WriteLine($"
Source document signed successfully with {signResult.Succeeded.Count} signature(s).
File saved at {outputFilePathSigned}.
");
```

### デジタル署名認証

PDFの認証は、文書が特定の真正性とセキュリティ基準を満たしていることを保証します。このプロセスは、法務およびコンプライアンスの観点から非常に重要です。

#### ステップ1: 署名オブジェクトの初期化
タイムスタンプ機能と同様に、まず初期化から始めます。 `Signature` クラス：

```csharp
string filePath = "@YOUR_DOCUMENT_DIRECTORY/sample.pdf";
using (Signature signature = new Signature(filePath))
{
    // さらなる手順はここに追加されます
}
```

#### ステップ2: 認証用にPdfDigitalSignatureを構成する
作成する `PdfDigitalSignature` オブジェクトの詳細を指定し、タイプを証明書に設定します。

```csharp
PdfDigitalSignature pdfDigitalSignature = new PdfDigitalSignature()
{
    ContactInfo = "Contact",
    Location = "Location",
    Reason = "Reason"
};

pdfDigitalSignature.Type = PdfDigitalSignatureType.Certificate;
```

#### ステップ3: デジタル署名オプションを構成する
タイムスタンプの追加と同様に、署名オプションを設定します。

```csharp
digitalSignOptions = new DigitalSignOptions(certificatePath)
{
    Password = "1234567890",
    Signature = pdfDigitalSignature,
    VerticalAlignment = VerticalAlignment.Bottom,
    HorizontalAlignment = HorizontalAlignment.Right
};
```

#### ステップ4：文書に署名して結果を取得する
認証プロセスを実行し、認証された文書を保存して、結果を印刷します。

```csharp
SignResult signResult = signature.Sign(outputFilePathCertified, digitalSignOptions);
Console.WriteLine($"
Source document signed successfully with {signResult.Succeeded.Count} signature(s).
File saved at {outputFilePathCertified}.
");
```

## 実用的な応用

- **法的文書:** 契約と合意が長期にわたって整合性を維持することを確認します。
- **財務報告:** 財務諸表の正確性とコンプライアンスを証明します。
- **教育証明書:** 修了証書または賞状を認証します。
- **電子商取引取引:** 注文書と領収書を安全に保管します。
- **政府フォーム:** 公的機関に提出されたフォームを検証します。

## パフォーマンスに関する考慮事項

GroupDocs.Signature を使用する際のパフォーマンスを最適化するには:

- **リソースの使用状況:** 特に大きなドキュメントを処理するときに、メモリ使用量を監視します。
- **バッチ処理:** 複数のファイルに署名する場合は、効率化のためにバッチ処理を検討してください。
- **非同期操作:** 非同期メソッドを使用すると、操作のブロックを回避し、アプリケーションの応答性を向上させることができます。

## 結論

このガイドでは、GroupDocs.Signature for .NETを使用してPDF文書にタイムスタンプ付きのデジタル署名を施し、認証する方法を学習しました。これらのスキルを活用することで、デジタルコンテンツのセキュリティと信頼性を強化し、様々なドメインにおけるコンプライアンスを確保できます。

次のステップとしては、GroupDocs.Signature が提供する他の機能を試したり、アプリケーション内のより大規模なワークフローに統合したりすることが挙げられます。ぜひ、さまざまなオプションや設定を試してみてください。

## FAQセクション

1. **デジタル署名とは何ですか?**
   - デジタル署名は、デジタル領域における手書き署名と同様に、文書の信頼性と整合性を保証します。

2. **文書に署名するための証明書を取得するにはどうすればよいですか?**
   - 信頼できる証明機関 (CA) から証明書を購入するか、内部目的で自己署名証明書を使用することができます。

3. **GroupDocs.Signature はすべての .NET バージョンと互換性がありますか?**
   - はい、前提条件に指定されているとおり、.NET Framework と .NET Core をサポートしています。