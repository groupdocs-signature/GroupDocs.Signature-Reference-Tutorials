---
"description": "GroupDocs.Signature for .NET을 사용하여 문서의 QR 코드를 확인하는 방법을 알아보세요. 코드 예제와 문서 인증 모범 사례를 담은 완벽한 가이드입니다."
"linktitle": "QR 코드 확인"
"second_title": "GroupDocs.Signature .NET API"
"title": "문서의 QR 코드 확인"
"url": "/ko/net/verify-operations/verify-qr-code/"
"weight": 12
---

## 소개

문서 보안은 현대 비즈니스 운영에 있어 매우 중요한 요소입니다. QR 코드는 문서에 정보를 삽입하여 진위 여부를 확인하는 방법으로 점점 더 널리 사용되고 있습니다. GroupDocs.Signature for .NET은 다양한 형식의 문서에 삽입된 QR 코드를 검증하는 강력하고 유연한 솔루션을 제공합니다.

이 포괄적인 튜토리얼은 .NET 애플리케이션에서 QR 코드 검증을 구현하는 과정을 안내하고, 문서의 무결성과 신뢰성을 유지하는 방법을 설명합니다.

## 필수 조건

QR 코드 검증 기능을 구현하기 전에 다음 전제 조건이 충족되었는지 확인하세요.

1. .NET용 GroupDocs.Signature: 라이브러리를 다운로드하여 설치하세요. [다운로드 페이지](https://releases.groupdocs.com/signature/net/).
2. 개발 환경: Visual Studio 또는 호환되는 .NET 개발 환경.
3. 테스트 문서: 검증 목적으로 QR 코드 서명이 포함된 문서입니다.
4. 기본 지식: C# 프로그래밍 및 .NET 프레임워크 개념에 대한 지식이 필요합니다.

## 네임스페이스 가져오기

GroupDocs.Signature 기능에 액세스하는 데 필요한 네임스페이스를 가져오는 것으로 시작합니다.

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## 단계별 QR 코드 검증 프로세스

문서 내의 QR 코드를 확인하려면 다음의 자세한 단계를 따르세요.

### 1단계: 문서 경로 지정

```csharp
// QR 코드 서명이 포함된 문서의 경로를 제공하세요
string filePath = "sample_multiple_signatures.docx";
```

예시 경로를 실제 문서 경로로 바꿔야 합니다.

### 2단계: 서명 개체 초기화

```csharp
// 문서 경로를 전달하여 Signature 인스턴스를 생성합니다.
using (Signature signature = new Signature(filePath))
{
    // 여기에 검증코드가 구현됩니다
}
```

Signature 클래스는 GroupDocs.Signature API의 모든 작업에 대한 주요 진입점입니다.

### 3단계: QR 코드 확인 옵션 구성

```csharp
// QR 코드 검증 옵션 정의
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // 문서의 모든 페이지를 확인하세요
    Text = "John",   // QR 코드 내에서 확인할 텍스트
    MatchType = TextMatchType.Contains // 텍스트 일치 기준을 지정하세요
};
```

검증 옵션을 사용하면 검증 프로세스에 대한 특정 기준을 정의할 수 있습니다.
- `AllPages`: 모든 문서 페이지를 확인하려면 true로 설정합니다(기본 동작)
- `Text`: QR 코드 내에서 일치할 텍스트 콘텐츠
- `MatchType`: 텍스트 일치 방법(Contains, Exact, StartsWith 등)

### 4단계: 검증 프로세스 실행

```csharp
// 검증을 수행하다
VerificationResult result = signature.Verify(options);
```

이는 귀하가 지정한 옵션에 따라 검증 프로세스를 실행합니다.

### 5단계: 프로세스 검증 결과

```csharp
// 검증 결과를 확인하고 그에 따라 처리하세요
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
    
    // 성공적인 서명에 대한 정보 표시
    foreach (QrCodeSignature signature in result.Succeeded)
    {
        Console.WriteLine($"Found valid QR Code signature with text: {signature.Text}");
        Console.WriteLine($"QR Code type: {signature.EncodeType.TypeName}");
        Console.WriteLine($"Location: Page {signature.PageNumber}, {signature.Left}x{signature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

검증 결과를 올바르게 처리하면 애플리케이션이 검증 결과에 따라 적절한 조치를 취할 수 있습니다.

## 완전한 예

QR 코드 검증을 보여주는 완전하고 실제적인 예는 다음과 같습니다.

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
            // 문서 경로
            string filePath = "sample_multiple_signatures.docx";
            
            // Signature 인스턴스 초기화
            using (Signature signature = new Signature(filePath))
            {
                // 설정 확인 옵션
                QrCodeVerifyOptions options = new QrCodeVerifyOptions()
                {
                    AllPages = true,
                    Text = "John",
                    MatchType = TextMatchType.Contains
                };
                
                // 문서 서명 확인
                VerificationResult result = signature.Verify(options);
                
                // 프로세스 검증 결과
                if (result.IsValid)
                {
                    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
                    
                    foreach (QrCodeSignature qrSignature in result.Succeeded)
                    {
                        Console.WriteLine($"Found valid QR Code with text: {qrSignature.Text}");
                    }
                }
                else
                {
                    Console.WriteLine($"Document {filePath} failed verification process.");
                }
            }
        }
    }
}
```

## 고급 확인 옵션

GroupDocs.Signature는 더욱 복잡한 검증 시나리오에 대한 추가 옵션을 제공합니다.

### 특정 QR 코드 유형 확인

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    EncodeType = QrCodeTypes.QR,  // 표준 QR 코드만 확인하세요
    Text = "Confidential",
    MatchType = TextMatchType.Exact
};
```

### 특정 페이지에서 확인

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = false,
    PageNumber = 2,  // 2페이지에서만 확인하세요
    Text = "Approved"
};
```

### 검증을 위한 정규 표현식 사용

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    Text = "INV-\\d{6}",  // 송장 번호 일치(예: INV-123456)
    MatchType = TextMatchType.Regex
};
```

## QR 코드 검증을 위한 모범 사례

1. 항상 입력 내용을 검증하세요. 처리하기 전에 문서 경로와 검증 기준이 유효한지 확인하세요.
2. 오류 처리를 구현합니다. try-catch 블록을 사용하여 검증 중에 발생할 수 있는 예외를 처리합니다.
3. 성능을 고려하세요. 대용량 문서의 경우 전체 문서가 아닌 특정 페이지를 검증하는 것을 고려하세요.
4. 검증 결과 기록: 감사 목적으로 검증 프로세스 기록을 유지합니다.
5. 다양한 문서 형식으로 테스트하세요. 모든 필수 문서 형식에서 검증이 제대로 작동하는지 확인하세요.

## 결론

문서의 QR 코드 검증은 문서의 진위성과 무결성을 보장하는 데 필수적인 요소입니다. GroupDocs.Signature for .NET은 .NET 애플리케이션에서 QR 코드 검증을 구현할 수 있는 포괄적이고 사용자 친화적인 API를 제공합니다.

이 튜토리얼을 따라하면 다음 방법을 배울 수 있습니다.
- 검증 프로세스 구성 및 초기화
- 다양한 검증 기준을 지정하세요
- 검증 결과 처리 및 해석
- 고급 검증 옵션 구현

이러한 지식을 통해 문서 관리 시스템의 보안과 안정성을 강화할 수 있습니다.

## 자주 묻는 질문

### GroupDocs.Signature는 하나의 문서에서 여러 개의 QR 코드를 확인할 수 있나요?
네, GroupDocs.Signature는 단일 문서 내 여러 QR 코드를 검증할 수 있습니다. 검증 결과에는 일치하는 모든 QR 코드가 포함됩니다.

### QR 코드 검증에 지원되는 문서 형식은 무엇입니까?
GroupDocs.Signature는 PDF, Word(DOC, DOCX), Excel(XLS, XLSX), PowerPoint(PPT, PPTX), 이미지 등 다양한 문서 형식을 지원합니다.

### 특정 암호화나 포맷으로 QR 코드를 검증할 수 있나요?
네, GroupDocs.Signature는 특정 인코딩 유형과 콘텐츠 형식 패턴을 사용하여 QR 코드를 검증하는 옵션을 제공합니다.

### 타사 애플리케이션에서 생성된 QR 코드를 검증할 수 있나요?
네, GroupDocs.Signature는 표준 QR 코드 형식을 따르는 대부분의 애플리케이션에서 생성된 표준 QR 코드를 확인할 수 있습니다.

### 텍스트 대신 이진 데이터가 포함된 QR 코드를 어떻게 처리합니까?
GroupDocs.Signature는 이진 데이터를 사용하여 QR 코드를 검증하기 위한 옵션을 제공합니다. `BinaryData` 검증 옵션의 속성입니다.

### 관련 자료
* [GroupDocs.Signature API 참조](https://reference.groupdocs.com/signature/net/)
* [GroupDocs.Signature 다운로드](https://releases.groupdocs.com/signature/net/)
* [GitHub의 코드 예제](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [선적 서류 비치](https://docs.groupdocs.com/signature/net/)
* [제품 페이지](https://products.groupdocs.com/signature/net/)
* [블로그 기사](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [지원 포럼](https://forum.groupdocs.com/c/signature/13)
* [임시 면허](https://purchase.groupdocs.com/temporary-license/)