---
"description": "GroupDocs.Signature for .NET을 사용하여 문서에서 디지털 서명을 검색하는 방법을 익혀보세요. 자세한 단계별 가이드를 통해 문서 보안 및 검증을 강화하세요."
"linktitle": "디지털 서명 검색"
"second_title": "GroupDocs.Signature .NET API"
"title": "문서에서 디지털 서명 검색"
"url": "/ko/net/signature-searching/search-for-digital-signatures/"
"weight": 11
---

## 소개

오늘날의 디지털 환경에서는 기업과 조직에 문서의 진위성과 무결성을 보장하는 것이 매우 중요합니다. 디지털 서명은 문서의 진위성을 확인하고 무단 수정을 감지하는 강력한 메커니즘을 제공합니다. GroupDocs.Signature for .NET은 다양한 문서 형식의 디지털 서명을 처리하는 포괄적인 솔루션을 제공하여 개발자가 서명 기능을 .NET 애플리케이션에 원활하게 통합할 수 있도록 지원합니다.

이 튜토리얼에서는 .NET용 GroupDocs.Signature를 사용하여 문서 내에서 디지털 서명을 검색하는 과정을 안내하며, 자세한 설명과 실제 코드 예제를 제공합니다.

## 필수 조건

구현 세부 사항을 살펴보기 전에 다음 전제 조건이 충족되었는지 확인하세요.

1. .NET용 GroupDocs.Signature: 라이브러리를 다운로드하고 설치하세요. [여기](https://releases.groupdocs.com/signature/net/).
   
2. 개발 환경: Visual Studio나 선호하는 IDE로 .NET 개발 환경을 설정합니다.
   
3. 샘플 문서: 테스트 목적으로 디지털 서명이 포함된 샘플 문서를 준비합니다.

4. 기본 지식: C# 프로그래밍 언어와 .NET 프레임워크 기본에 대한 지식이 필요합니다.

## 네임스페이스 가져오기

.NET용 GroupDocs.Signature가 제공하는 기능에 액세스하려면 필요한 네임스페이스를 가져오는 것으로 시작합니다.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

이제 디지털 서명을 검색하는 과정을 명확하고 관리하기 쉬운 단계로 나누어 보겠습니다.

## 1단계: Signature 객체 초기화

인스턴스를 생성하여 시작하세요. `Signature` 클래스, 문서 경로를 전달합니다:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // 디지털 서명 검색을 위한 코드가 여기에 추가됩니다.
}
```

## 2단계: 디지털 서명 검색

다음으로, 다음을 사용하세요 `Search` 방법을 사용하여 `SignatureType.Digital` 문서에서 디지털 서명을 검색하기 위한 매개변수:

```csharp
// 문서에서 디지털 서명 검색
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```

## 3단계: 결과 처리 및 표시

마지막으로, 검색 결과를 처리하고 발견된 디지털 서명에 대한 관련 정보를 표시합니다.

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

## 완전한 예

문서에서 디지털 서명을 검색하는 방법을 보여주는 완전하고 실제적인 예는 다음과 같습니다.

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
            // 문서 경로
            string filePath = "sample_multiple_signatures.docx";
            
            // Signature 인스턴스 초기화
            using (Signature signature = new Signature(filePath))
            {
                // 문서에서 디지털 서명 검색
                List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
                
                // 검색 결과 표시
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

## 고급 검색 옵션

더욱 타겟화된 검색을 위해 다음을 사용할 수 있습니다. `DigitalSearchOptions` 검색 기준을 사용자 지정하려면:

```csharp
// 디지털 검색 옵션 만들기
DigitalSearchOptions options = new DigitalSearchOptions()
{
    // 특정 페이지(예: 1페이지, 2페이지)에서만 검색
    PageNumber = 1,
    PagesSetup = new PagesSetup() { Pages = new List<int> { 1, 2 } },
    
    // 디지털 서명의 주석으로 필터링
    Comments = "Approved",
    
    // 검색 날짜 및 시간 범위 설정
    SignDateTimeFrom = new DateTime(2022, 1, 1),
    SignDateTimeTo = DateTime.Now
};

// 특정 옵션으로 검색
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(options);
```

## 인증서 정보 작업

디지털 서명에는 액세스하여 검증할 수 있는 귀중한 인증서 정보가 포함되어 있습니다.

```csharp
foreach (var digitalSignature in signatures)
{
    if (digitalSignature.Certificate != null)
    {
        // 인증서 속성에 액세스
        Console.WriteLine($"Certificate Valid From: {digitalSignature.Certificate.NotBefore}");
        Console.WriteLine($"Certificate Valid To: {digitalSignature.Certificate.NotAfter}");
        
        // 인증서가 유효한 날짜 범위에 있는지 확인하세요
        bool isDateValid = DateTime.Now >= digitalSignature.Certificate.NotBefore && 
                          DateTime.Now <= digitalSignature.Certificate.NotAfter;
        
        Console.WriteLine($"Certificate Date Validity: {isDateValid}");
        
        // 인증서 발급자 세부 정보에 액세스
        Console.WriteLine($"Certificate Issuer: {digitalSignature.Certificate.IssuerName}");
    }
}
```

## 결론

GroupDocs.Signature for .NET은 문서 내 디지털 서명을 검색하고 검증하는 강력하고 유연한 솔루션을 제공합니다. 이 튜토리얼에서는 .NET 애플리케이션에서 디지털 서명 검색 기능을 구현하는 단계별 프로세스를 살펴보고, 문서 보안 및 무결성 검증을 강화하는 데 필요한 지식을 습득했습니다.

GroupDocs.Signature를 활용하면 디지털 문서의 진위성과 무결성을 보장하는 강력한 문서 관리 시스템을 구축하여 비즈니스 프로세스에서 신뢰와 규정 준수를 강화할 수 있습니다.

## 자주 묻는 질문

### GroupDocs.Signature는 디지털 서명의 유효성을 검증할 수 있나요?

예, GroupDocs.Signature는 검색 프로세스 중에 자동으로 디지털 서명을 검증하고 다음을 통해 검증 상태를 제공합니다. `IsValid` 의 재산 `DigitalSignature` 수업.

### 어떤 문서 형식이 디지털 서명 검색을 지원합니까?

GroupDocs.Signature는 PDF, Microsoft Office 문서(Word, Excel, PowerPoint), OpenOffice 형식 등 다양한 형식으로 디지털 서명 검색을 지원합니다.

### 암호로 보호된 문서에서 디지털 서명을 검색할 수 있나요?

예, 암호로 보호된 문서에서 디지털 서명을 검색하려면 초기화할 때 암호를 제공하면 됩니다. `Signature` 물체:

```csharp
LoadOptions loadOptions = new LoadOptions() { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // 디지털 서명 검색
}
```

### 특정 사람이 디지털 서명을 생성했는지 어떻게 확인할 수 있나요?

인증서의 주체 이름과 기타 속성을 조사하여 서명자의 신원을 확인할 수 있습니다.

```csharp
foreach (var signature in signatures)
{
    if (signature.Certificate?.SubjectName?.Contains("John Doe") == true)
    {
        Console.WriteLine("Found signature by John Doe");
    }
}
```

### 디지털 서명 인증서에서 공개 키를 추출할 수 있나요?

네, 인증서 속성을 통해 공개 키 정보에 액세스할 수 있습니다.

```csharp
if (signature.Certificate != null)
{
    // 공개 키 정보에 접근
    Console.WriteLine($"Public Key: {signature.Certificate.GetPublicKeyString()}");
}
```

## 또한 참조

* [API 참조](https://reference.groupdocs.com/signature/net/)
* [코드 예제](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [제품 문서](https://docs.groupdocs.com/signature/net/)
* [제품 페이지](https://products.groupdocs.com/signature/net/)
* [최신 버전 다운로드](https://releases.groupdocs.com/signature/net/)
* [블로그 기사](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [지원 포럼](https://forum.groupdocs.com/c/signature/13)
* [임시 면허](https://purchase.groupdocs.com/temporary-license/)