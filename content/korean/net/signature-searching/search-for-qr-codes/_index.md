---
"description": "이 포괄적인 단계별 가이드와 코드 예제를 통해 .NET용 GroupDocs.Signature를 사용하여 문서에서 QR 코드를 효율적으로 검색하는 방법을 알아보세요."
"linktitle": "QR 코드 검색"
"second_title": "GroupDocs.Signature .NET API"
"title": "문서에서 QR 코드 서명 검색"
"url": "/ko/net/signature-searching/search-for-qr-codes/"
"weight": 15
type: docs
---
## 소개

오늘날의 디지털 문서 생태계에서 QR 코드 서명은 정보 삽입, 인증 및 문서 보안 강화를 위한 매우 중요한 도구로 자리 잡았습니다. GroupDocs.Signature for .NET은 개발자에게 다양한 문서 형식에서 QR 코드를 검색하고 추출할 수 있는 강력한 API를 제공하여 .NET 애플리케이션에서 고급 문서 분석 및 검증 기능을 구현할 수 있도록 지원합니다.

이 포괄적인 튜토리얼은 .NET용 GroupDocs.Signature를 사용하여 QR 코드 검색 기능을 구현하는 과정을 안내하며, 명확한 설명, 단계별 지침, 그리고 사용자 애플리케이션에 통합할 수 있는 실용적인 코드 예제를 제공합니다.

## 필수 조건

QR 코드 서명 검색을 시작하기 전에 다음 전제 조건이 충족되었는지 확인하세요.

1. .NET SDK용 GroupDocs.Signature: SDK를 다운로드하여 설치하세요. [다운로드 페이지](https://releases.groupdocs.com/signature/net/).

2. 개발 환경: .NET Framework 또는 .NET Core가 설치된 Visual Studio와 같은 .NET 개발 환경을 설정합니다.

3. 기본 지식: C# 프로그래밍과 .NET 개발 개념에 대한 지식이 필요합니다.

4. 샘플 문서: 검증 및 테스트를 위해 QR 코드가 포함된 테스트 문서를 준비합니다.

## 네임스페이스 가져오기

GroupDocs.Signature 기능에 액세스하는 데 필요한 네임스페이스를 가져오는 것으로 시작합니다.

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;
```

이제 QR 코드를 검색하는 과정을 명확하고 따라하기 쉬운 단계로 나누어 보겠습니다.

## 1단계: 문서 경로 정의

먼저, 검색하려는 QR 코드가 포함된 문서의 경로를 지정하세요.

```csharp
string filePath = "sample_multiple_signatures.docx";
```

## 2단계: 서명 개체 초기화

인스턴스를 생성합니다 `Signature` 문서 경로를 전달하여 클래스를 생성합니다.

```csharp
using (Signature signature = new Signature(filePath))
{
    // QR코드 검색코드가 여기에 추가됩니다
}
```

## 3단계: QR 코드 서명 검색

사용하세요 `Search` 문서에서 QR 코드를 찾기 위해 적절한 서명 유형을 사용하는 방법:

```csharp
// 문서 내에서 QR 코드 서명 검색
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

## 4단계: 결과 처리 및 표시

찾은 QR 코드 서명을 반복하고 해당 속성에 액세스합니다.

```csharp
// 발견된 QR 코드에 대한 정보 표시
Console.WriteLine($"\nSource document contains {signatures.Count} QR code signature(s):");

foreach (var qrCodeSignature in signatures)
{
    Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
    Console.WriteLine($"Content: {qrCodeSignature.Text}");
    Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
    Console.WriteLine();
}
```

## 완전한 예

다음은 문서에서 QR 코드를 검색하는 전체 과정을 보여주는 포괄적인 실제 예입니다.

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;

namespace QrCodeSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // 문서 경로 - 파일 경로로 업데이트
            string filePath = "sample_multiple_signatures.docx";
            
            // Signature 인스턴스 초기화
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // 문서에서 QR 코드 서명을 검색하세요
                    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
                    
                    // 검색 결과 표시
                    Console.WriteLine($"\nSource document ['{filePath}'] contains {signatures.Count} QR code signature(s):");
                    
                    foreach (var qrCodeSignature in signatures)
                    {
                        Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
                        Console.WriteLine($"Content: {qrCodeSignature.Text}");
                        Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
                        Console.WriteLine();
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"Error occurred: {ex.Message}");
                }
            }
            
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## 고급 QR 코드 검색 기술

### 특정 기준으로 검색

더욱 타겟화된 검색을 위해 다음을 사용할 수 있습니다. `QrCodeSearchOptions` 검색 기준을 사용자 지정하려면:

```csharp
// 특정 기준으로 QR 코드 검색 옵션 만들기
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    // 특정 페이지에서만 검색
    AllPages = false,
    PageNumber = 1,
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // QR 코드 내용으로 필터링
    Text = "Invoice",
    MatchType = TextMatchType.Contains,
    
    // 특정 QR 코드 유형으로 필터링
    EncodeType = QrCodeTypes.QR,
    
    // 검색할 특정 영역을 정의하세요
    Rectangle = new Rectangle(100, 100, 400, 400)
};

// 특정 옵션으로 검색
List<QrCodeSignature> filteredSignatures = signature.Search<QrCodeSignature>(options);
```

### QR 코드 데이터 처리

애플리케이션 요구 사항에 따라 QR 코드 데이터에 대한 사용자 정의 처리를 구현할 수 있습니다.

```csharp
foreach (var qrCode in signatures)
{
    // 콘텐츠 기반 QR코드 데이터 추출 및 처리
    string qrContent = qrCode.Text;
    
    if (qrContent.StartsWith("URL:"))
    {
        // URL 데이터 처리
        string url = qrContent.Substring(4);
        Console.WriteLine($"Found URL in QR code: {url}");
    }
    else if (qrContent.StartsWith("CONTACT:"))
    {
        // 연락처 정보 처리
        string contact = qrContent.Substring(8);
        Console.WriteLine($"Found contact information in QR code: {contact}");
    }
    else if (qrContent.StartsWith("INVOICE:"))
    {
        // 송장 정보 처리
        string invoiceData = qrContent.Substring(8);
        Console.WriteLine($"Found invoice information in QR code: {invoiceData}");
        
        // 송장 데이터 구문 분석 및 검증
        if (ValidateInvoiceData(invoiceData))
        {
            Console.WriteLine("Invoice data is valid!");
        }
        else
        {
            Console.WriteLine("Warning: Invalid invoice data detected!");
        }
    }
}

// 검증 방법 예시
static bool ValidateInvoiceData(string data)
{
    // 검증 논리를 구현하세요
    return !string.IsNullOrEmpty(data) && data.Contains("ID") && data.Contains("Amount");
}
```

### 보안 검증 구현

QR 코드는 인증 목적으로 자주 사용됩니다. 기본적인 보안 검증을 구현하는 방법은 다음과 같습니다.

```csharp
// 문서에 유효한 인증 QR 코드가 포함되어 있는지 확인하세요
bool hasValidAuthQrCode = false;

foreach (var qrCode in signatures)
{
    if (qrCode.Text.StartsWith("AUTH:"))
    {
        string authCode = qrCode.Text.Substring(5);
        
        // 인증 코드 확인(예: 데이터베이스 또는 미리 정의된 목록)
        if (VerifyAuthCode(authCode))
        {
            hasValidAuthQrCode = true;
            Console.WriteLine("Document contains valid authentication QR code!");
            break;
        }
    }
}

if (!hasValidAuthQrCode)
{
    Console.WriteLine("Warning: Document does not contain a valid authentication QR code!");
}

// 검증 방법 예시
static bool VerifyAuthCode(string code)
{
    // 검증 논리를 구현하세요
    // 이는 데이터베이스 조회, API 호출 또는 사전 정의된 값에 대한 비교일 수 있습니다.
    return code == "A7B82C3D" || code == "X9Y8Z7W6";
}
```

### QR 코드 이미지 추출

추가 처리나 표시를 위해 문서에서 QR 코드 이미지를 추출할 수 있습니다.

```csharp
// QR 코드 이미지를 디스크에 저장
foreach (var qrCode in signatures)
{
    if (qrCode.Content != null)
    {
        // 페이지 번호와 위치를 기반으로 고유한 파일 이름을 만듭니다.
        string outputPath = $"QrCode_P{qrCode.PageNumber}_X{qrCode.Left}_Y{qrCode.Top}.png";
        
        // 이미지 데이터를 저장합니다
        File.WriteAllBytes(outputPath, qrCode.Content);
        Console.WriteLine($"Saved QR code image to {outputPath}");
    }
}
```

## 결론

이 종합 가이드에서는 GroupDocs.Signature for .NET을 사용하여 문서에서 QR 코드 서명을 검색하는 방법을 살펴보았습니다. 기본 검색부터 고급 기술까지, 이제 .NET 애플리케이션에서 강력한 QR 코드 처리를 구현하는 방법을 익혔습니다. GroupDocs.Signature API는 다양한 문서 형식에서 QR 코드를 포함한 다양한 서명 유형을 처리할 수 있는 강력하고 유연한 프레임워크를 제공합니다.

이러한 기능을 활용하면 문서 검증 프로세스를 개선하고, 인증 시스템을 구현하고, QR 코드에 포함된 귀중한 정보를 추출하는 등의 작업을 모두 .NET 애플리케이션 내에서 수행할 수 있습니다.

## 자주 묻는 질문

### GroupDocs.Signature는 어떤 QR 코드 형식을 지원합니까?

GroupDocs.Signature는 표준 QR 코드, Micro QR 코드 및 기타 일반적인 QR 코드 표준을 포함한 다양한 QR 코드 형식을 지원합니다. 특정 형식은 다음을 통해 액세스할 수 있습니다. `EncodeType` 의 재산 `QrCodeSignature` 물체.

### 비밀번호로 보호된 문서에서 QR 코드를 검색할 수 있나요?

예, GroupDocs.Signature는 암호로 보호된 문서에서 QR 코드를 검색하는 것을 지원하며 이를 위해 초기화 시 암호를 제공합니다. `Signature` 물체:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // QR 코드 검색
}
```

### QR 코드의 내용을 기준으로 필터링하려면 어떻게 해야 하나요?

다음을 사용하여 QR 코드를 콘텐츠에 따라 필터링할 수 있습니다. `Text` 그리고 `MatchType` 의 속성 `QrCodeSearchOptions`:

```csharp
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    Text = "Invoice",
    MatchType = TextMatchType.Contains // 기타 옵션: 정확한, 시작 문자, 종료 문자
};
```

### GroupDocs.Signature는 손상되었거나 부분적으로 보이는 QR 코드를 감지할 수 있나요?

GroupDocs.Signature는 부분적으로 보이는 QR 코드를 감지하는 기능이 있지만, 심하게 손상된 QR 코드는 인식되지 않을 수 있습니다. 감지 정확도는 문서 내 QR 코드의 품질과 가시성에 따라 달라집니다.

### QR 코드 검색에는 어떤 문서 형식이 지원됩니까?

GroupDocs.Signature는 PDF, Microsoft Office 문서(Word, Excel, PowerPoint), 이미지(JPEG, PNG, TIFF) 등 다양한 문서 형식에서 QR 코드 검색을 지원합니다.

## 또한 참조

* [API 참조](https://reference.groupdocs.com/signature/net/)
* [GitHub의 코드 예제](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [제품 문서](https://docs.groupdocs.com/signature/net/)
* [제품 페이지](https://products.groupdocs.com/signature/net/)
* [최신 버전 다운로드](https://releases.groupdocs.com/signature/net/)
* [블로그 기사](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [무료 지원 포럼](https://forum.groupdocs.com/c/signature/13)
* [임시 면허](https://purchase.groupdocs.com/temporary-license/)