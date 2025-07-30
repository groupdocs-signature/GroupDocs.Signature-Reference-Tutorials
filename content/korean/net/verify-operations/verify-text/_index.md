---
"description": "GroupDocs.Signature를 사용하여 .NET 애플리케이션에서 텍스트 서명 검증을 마스터하세요. 전체 코드 예제와 모범 사례를 담은 단계별 구현 가이드입니다."
"linktitle": "텍스트 확인"
"second_title": "GroupDocs.Signature .NET API"
"title": "문서의 텍스트 서명 확인"
"url": "/ko/net/verify-operations/verify-text/"
"weight": 13
---

## 소개

텍스트 서명은 디지털 또는 전자 서명보다 간단하지만 문서 관리 및 검증에 중요한 역할을 합니다. 워터마크, 푸터 텍스트, 특정 콘텐츠 패턴 등 텍스트 서명의 존재 여부와 무결성을 검증하는 것은 문서 검증 프로세스의 중요한 측면입니다.

GroupDocs.Signature for .NET은 다양한 형식의 문서 내 텍스트 서명을 검증하는 강력한 API를 제공합니다. 이 포괄적인 튜토리얼은 .NET 애플리케이션에서 텍스트 검증 기능을 구현하여 문서의 무결성과 신뢰성을 유지하는 방법을 안내합니다.

## 필수 조건

텍스트 검증 기능을 구현하기 전에 다음 전제 조건이 충족되었는지 확인하세요.

1. .NET용 GroupDocs.Signature: 라이브러리를 다운로드하여 설치하세요. [다운로드 페이지](https://releases.groupdocs.com/signature/net/).
2. .NET 개발 환경: Visual Studio 또는 호환되는 .NET 개발 환경.
3. 기본 지식: C# 프로그래밍 및 .NET 프레임워크 개념에 대한 지식이 필요합니다.
4. 테스트 문서: 검증 목적으로 텍스트 서명이 포함된 문서입니다.

## 필수 네임스페이스 가져오기

GroupDocs.Signature 기능에 액세스하는 데 필요한 네임스페이스를 가져오는 것부터 시작합니다.

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

텍스트 검증 프로세스를 명확하고 관리하기 쉬운 단계로 나누어 보겠습니다.

## 1단계: 문서 경로 지정

```csharp
// 텍스트 서명이 포함된 문서 경로
string filePath = "sample_multiple_signatures.docx";
```

예시 경로를 텍스트 서명이 포함된 문서의 실제 경로로 바꿔야 합니다.

## 2단계: 서명 개체 초기화

```csharp
// 문서 경로를 전달하여 Signature 클래스 인스턴스를 생성합니다.
using (Signature signature = new Signature(filePath))
{
    // 여기에 검증코드가 구현됩니다
}
```

Signature 클래스는 GroupDocs.Signature API의 모든 작업에 대한 주요 진입점입니다.

## 3단계: 텍스트 확인 옵션 구성

```csharp
// 텍스트 검증 옵션 정의
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = true,                               // 문서의 모든 페이지를 확인하세요
    SignatureImplementation = TextSignatureImplementation.Native,
    Text = "signature",                            // 검증할 텍스트
    MatchType = TextMatchType.Contains             // 일치 기준 지정
};
```

검증 옵션을 사용하면 검증 프로세스에 대한 특정 기준을 정의할 수 있습니다.
- `AllPages`: 모든 문서 페이지를 확인하려면 true로 설정합니다.
- `SignatureImplementation`: 텍스트가 어떻게 구현되는지 지정하세요(네이티브 또는 스티커)
- `Text`: 문서 내에서 일치시킬 텍스트 콘텐츠
- `MatchType`: 텍스트 일치 방법(Contains, Exact, StartsWith 등)

## 4단계: 검증 프로세스 실행

```csharp
// 검증을 수행하다
VerificationResult result = signature.Verify(options);
```

이는 귀하가 지정한 옵션에 따라 검증 프로세스를 실행합니다.

## 5단계: 프로세스 검증 결과

```csharp
// 검증 결과를 확인하고 그에 따라 처리하세요
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid text signatures!");
    
    // 성공적인 서명에 대한 정보 표시
    foreach (TextSignature textSignature in result.Succeeded)
    {
        Console.WriteLine($"\nFound valid text signature:");
        Console.WriteLine($"Text: {textSignature.Text}");
        Console.WriteLine($"Location: Page {textSignature.PageNumber}, {textSignature.Left}x{textSignature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

이 코드는 검증이 성공했는지 확인하고 검증된 텍스트 서명에 대한 자세한 정보를 제공합니다.

## 완전한 예

다음은 텍스트 서명 검증을 보여주는 완전한 작동 예입니다.

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
            
            try
            {
                // Signature 인스턴스 초기화
                using (Signature signature = new Signature(filePath))
                {
                    // 설정 확인 옵션
                    TextVerifyOptions options = new TextVerifyOptions()
                    {
                        AllPages = true,
                        SignatureImplementation = TextSignatureImplementation.Native,
                        Text = "signature",
                        MatchType = TextMatchType.Contains
                    };
                    
                    // 문서 서명 확인
                    VerificationResult result = signature.Verify(options);
                    
                    // 프로세스 검증 결과
                    if(result.IsValid)
                    {
                        Console.WriteLine($"\nDocument {filePath} was verified successfully!");
                        foreach (TextSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature is found with text: {item.Text}");
                            Console.WriteLine($"Location: Page {item.PageNumber}, position {item.Left}x{item.Top}");
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

## 고급 검증 시나리오

GroupDocs.Signature는 더욱 복잡한 검증 시나리오에 대한 추가 옵션을 제공합니다.

### 검증을 위한 정규 표현식 사용

더욱 유연한 패턴 일치를 위해 정규 표현식을 사용할 수 있습니다.

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "Invoice\\s+#\\d{5,6}",  // "송장 #12345"와 같은 패턴을 일치시킵니다.
    MatchType = TextMatchType.Regex
};
```

### 특정 문서 영역의 텍스트 확인

문서의 특정 영역에 대한 검증을 제한할 수 있습니다.

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = false,
    PageNumber = 1,  // 첫 번째 페이지에서만 확인하세요
    
    // 검색할 영역 정의(포인트 단위의 좌표)
    PagesSetup = new PagesSetup() 
    { 
        FirstPage = true,
        LastPage = false,
        OddPages = false,
        EvenPages = false 
    },
    
    // 사각형 면적(밀리미터)
    Rectangle = new Rectangle(10, 10, 100, 30),
    
    Text = "Confidential"
};
```

### 여러 텍스트 패턴을 동시에 검증

다양한 텍스트 패턴을 확인하기 위해 여러 가지 검증 옵션을 만들 수 있습니다.

```csharp
// 검증 옵션 목록 만들기
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// 첫 번째 텍스트 확인 추가
listOptions.Add(new TextVerifyOptions()
{
    Text = "Confidential",
    MatchType = TextMatchType.Exact
});

// 두 번째 텍스트 확인 추가
listOptions.Add(new TextVerifyOptions()
{
    Text = "Do not copy",
    MatchType = TextMatchType.Contains
});

// 여러 옵션으로 확인
VerificationResult result = signature.Verify(listOptions);
```

### 특정 모양의 텍스트 확인

다음과 같은 특정 서식 특성을 사용하여 텍스트를 확인할 수도 있습니다.

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "APPROVED",
    MatchType = TextMatchType.Exact,
    
    // 특정 모양 속성 확인
    ForegroundColorRGB = System.Drawing.Color.Green,
    Font = new SignatureFont() { FontFamily = "Arial", FontSize = 12, Bold = true }
};
```

## 텍스트 검증을 위한 모범 사례

1. 적절한 일치 유형 선택: 검증 요구 사항에 따라 올바른 일치 유형(포함, 정확, 정규식)을 선택합니다.
2. 성능 최적화: 대용량 문서의 경우 전체 문서가 아닌 특정 페이지를 검증하는 것을 고려하세요.
3. 오류 처리: 예상치 못한 시나리오를 원활하게 관리하기 위해 적절한 오류 처리를 구현합니다.
4. 대소문자 구분 고려: 특히 중요한 검증의 경우 텍스트 일치 시 대소문자를 구분하도록 주의하세요.
5. 철저한 테스트: 다양한 문서 형식과 텍스트 패턴으로 테스트 검증을 실시하여 호환성을 보장합니다.

## 일반적인 문제 해결

### 텍스트가 감지되지 않음
- 텍스트 서식이나 인코딩이 감지에 영향을 미치는지 확인하세요.
- 텍스트가 실제로 문서에 일반 텍스트(이미지가 아님)로 존재하는지 확인하세요.
- 다른 일치 기준을 시도하세요(정확한 기준 대신 포함 기준)

### 성능 문제
- 특정 페이지나 영역을 타겟팅하여 검증을 최적화하세요
- 거짓 양성을 줄이려면 더 구체적인 텍스트 패턴을 사용하세요.

### 검증 실패
- 공백, 특수 문자 또는 서식이 일치에 영향을 미치는지 확인하세요.
- 텍스트가 스캔된 이미지의 일부가 아닌지 확인하세요(OCR이 필요함)
- 텍스트가 추가된 이후 문서가 수정되지 않았는지 확인하세요.

## 결론

텍스트 검증은 문서 인증을 위한 다재다능하고 실용적인 접근 방식으로, 단독으로 또는 다른 검증 방법과 함께 사용할 수 있습니다. GroupDocs.Signature for .NET은 .NET 애플리케이션에서 강력한 텍스트 검증 기능을 구현할 수 있는 포괄적이고 사용하기 쉬운 API를 제공합니다.

이 단계별 가이드를 따라가면 다음 방법을 배울 수 있습니다.
- 텍스트 검증 프로세스 구성 및 초기화
- 다양한 검증 기준을 지정하세요
- 검증 결과 처리 및 해석
- 고급 검증 시나리오 구현

이러한 기능을 사용하면 다양한 문서 형식에서 텍스트의 진위를 확인할 수 있는 안전하고 신뢰할 수 있는 문서 처리 시스템을 구축할 수 있습니다.

## 자주 묻는 질문

### GroupDocs.Signature는 스캔한 문서의 텍스트를 확인할 수 있나요?
GroupDocs.Signature는 주로 디지털 텍스트 검증을 위해 설계되었습니다. 스캔한 문서의 경우, 먼저 OCR(광학 문자 인식) 기술을 사용하여 스캔한 이미지를 텍스트로 변환해야 합니다.

### 텍스트 검증에 지원되는 문서 형식은 무엇입니까?
GroupDocs.Signature는 PDF, Word 문서(DOC, DOCX), Excel 스프레드시트(XLS, XLSX), PowerPoint 프레젠테이션(PPT, PPTX), 이미지 등 다양한 문서 형식을 지원합니다.

### 서식이 지정된 텍스트(굵게, 기울임꼴, 특정 글꼴)를 확인할 수 있나요?
네, GroupDocs.Signature는 글꼴 패밀리, 크기, 스타일(굵게, 기울임꼴), 색상 등 특정 서식 특성으로 텍스트를 확인하는 옵션을 제공합니다.

### 암호로 보호된 문서의 텍스트를 검증할 수 있나요?
네, GroupDocs.Signature는 보호된 문서를 열어 검증할 때 문서 비밀번호를 지정하는 옵션을 제공합니다.

### 워터마크와 배경 텍스트를 확인할 수 있나요?
네, GroupDocs.Signature는 문서에 구현된 방식에 따라 워터마크와 배경 텍스트를 포함한 다양한 유형의 텍스트 서명을 확인할 수 있습니다.

### 관련 자료
* [GroupDocs.Signature API 참조](https://reference.groupdocs.com/signature/net/)
* [GroupDocs.Signature 다운로드](https://releases.groupdocs.com/signature/net/)
* [GitHub의 코드 예제](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [선적 서류 비치](https://docs.groupdocs.com/signature/net/)
* [제품 페이지](https://products.groupdocs.com/signature/net/)
* [블로그 기사](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [지원 포럼](https://forum.groupdocs.com/c/signature/13)
* [임시 면허](https://purchase.groupdocs.com/temporary-license/)