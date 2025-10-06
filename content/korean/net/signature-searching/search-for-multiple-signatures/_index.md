---
"description": "GroupDocs.Signature for .NET을 사용하여 문서에서 여러 서명 유형을 검색하는 방법을 알아보세요. 문서 보안 강화를 위한 코드 예제가 포함된 종합 가이드입니다."
"linktitle": "여러 서명 검색"
"second_title": "GroupDocs.Signature .NET API"
"title": "문서에서 여러 서명 유형 검색"
"url": "/ko/net/signature-searching/search-for-multiple-signatures/"
"weight": 14
type: docs
---
## 소개

최신 문서 관리 시스템에서는 단일 문서 내에서 여러 서명 유형을 검색하고 검증하는 기능이 점점 더 중요해지고 있습니다. 조직에서는 문서 보안을 강화하고 검증 프로세스를 간소화하기 위해 디지털 서명, 텍스트 서명, 바코드, QR 코드 등 다양한 서명 유형을 사용하는 경우가 많습니다. GroupDocs.Signature for .NET은 개발자가 다양한 문서 형식에 걸쳐 포괄적인 서명 검색 기능을 구현할 수 있도록 지원하는 강력한 프레임워크를 제공합니다.

이 튜토리얼에서는 .NET용 GroupDocs.Signature를 사용하여 문서 내에서 여러 서명 유형을 검색하는 과정을 안내하며, 자세한 설명과 실제 코드 예제를 제공합니다.

## 필수 조건

다중 서명 검색 기능을 구현하기 전에 다음 전제 조건이 충족되는지 확인하세요.

1. 개발 환경: Visual Studio 또는 선호하는 .NET 개발 환경이 시스템에 설치되어 있어야 합니다.
  
2. .NET용 GroupDocs.Signature: .NET용 GroupDocs.Signature 라이브러리를 다운로드하여 설치하세요. [여기](https://releases.groupdocs.com/signature/net/).

3. 기본 C# 지식: C# 프로그래밍 언어와 .NET 프레임워크 개념에 익숙함.

4. 샘플 문서: 테스트 목적으로 다양한 유형의 서명이 포함된 테스트 문서를 준비합니다.

## 네임스페이스 가져오기

GroupDocs.Signature 기능에 액세스하는 데 필요한 네임스페이스를 가져오는 것으로 시작합니다.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

이제 여러 서명 유형을 검색하는 과정을 명확하고 관리하기 쉬운 단계로 나누어 보겠습니다.

## 1단계: 문서 로드

먼저, 검색하려는 서명이 포함된 문서를 로드합니다.

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // 다중 서명 검색 코드가 여기에 추가됩니다.
}
```

## 2단계: 다양한 서명 유형에 대한 검색 옵션 정의

검색하려는 각 서명 유형에 대한 검색 옵션을 만듭니다.

```csharp
// 텍스트 서명에 대한 검색 옵션 정의
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,  // 모든 페이지에서 검색
    Text = "Signature",  // 선택 사항: 찾을 텍스트
    MatchType = TextMatchType.Contains  // 매칭 기준
};

// 디지털 서명에 대한 검색 옵션 정의
DigitalSearchOptions digitalOptions = new DigitalSearchOptions
{
    AllPages = true
};

// 바코드 서명에 대한 검색 옵션 정의
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
{
    AllPages = true,
    Text = "123456",  // 선택 사항: 일치시킬 바코드 텍스트
    MatchType = TextMatchType.Exact  // 매칭 기준
};

// QR 코드 서명에 대한 검색 옵션 정의
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
{
    AllPages = true,
    Text = "John",  // 선택 사항: 일치할 QR 코드 텍스트
    MatchType = TextMatchType.Contains  // 매칭 기준
};

// 메타데이터 서명에 대한 검색 옵션 정의
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```

## 3단계: 컬렉션에 옵션 추가

컬렉션에 모든 검색 옵션을 추가합니다.

```csharp
// 모든 검색 옵션을 보관할 목록을 만듭니다.
List<SearchOptions> searchOptions = new List<SearchOptions>
{
    textOptions,
    digitalOptions,
    barcodeOptions,
    qrCodeOptions,
    metadataOptions
};
```

## 4단계: 검색 수행 및 결과 처리

결합된 검색 옵션을 사용하여 검색을 실행하고 결과를 처리합니다.

```csharp
// 정의된 옵션을 사용하여 모든 서명 유형을 검색합니다.
SearchResult result = signature.Search(searchOptions);

// 서명이 발견되었는지 확인하세요
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
    
    // 발견된 서명을 반복합니다.
    foreach (var foundSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}, ID: {foundSignature.SignatureId}");
        
        // 특정 서명 유형을 처리합니다
        if (foundSignature is TextSignature textSignature)
        {
            Console.WriteLine($"Text: '{textSignature.Text}'");
        }
        else if (foundSignature is BarcodeSignature barcodeSignature)
        {
            Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
        }
        else if (foundSignature is QrCodeSignature qrCodeSignature)
        {
            Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
        }
        else if (foundSignature is DigitalSignature digitalSignature)
        {
            Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
        }
        else if (foundSignature is MetadataSignature metadataSignature)
        {
            Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
        }
    }
}
else
{
    Console.WriteLine("No signatures were found in the document.");
}
```

## 완전한 예

다음은 문서에서 여러 서명 유형을 검색하는 방법을 보여주는 완전하고 실제적인 예입니다.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace MultiSignatureSearch
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
                try
                {
                    // 텍스트 서명에 대한 검색 옵션 정의
                    TextSearchOptions textOptions = new TextSearchOptions
                    {
                        AllPages = true,
                        MatchType = TextMatchType.Contains
                    };

                    // 디지털 서명에 대한 검색 옵션 정의
                    DigitalSearchOptions digitalOptions = new DigitalSearchOptions
                    {
                        AllPages = true
                    };

                    // 바코드 서명에 대한 검색 옵션 정의
                    BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
                    {
                        AllPages = true
                    };

                    // QR 코드 서명에 대한 검색 옵션 정의
                    QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
                    {
                        AllPages = true
                    };

                    // 메타데이터 서명에 대한 검색 옵션 정의
                    MetadataSearchOptions metadataOptions = new MetadataSearchOptions();

                    // 모든 검색 옵션을 보관할 목록을 만듭니다.
                    List<SearchOptions> searchOptions = new List<SearchOptions>
                    {
                        textOptions,
                        digitalOptions,
                        barcodeOptions,
                        qrCodeOptions,
                        metadataOptions
                    };

                    // 모든 서명 유형 검색
                    SearchResult result = signature.Search(searchOptions);

                    // 서명이 발견되었는지 확인하세요
                    if (result.Signatures.Count > 0)
                    {
                        Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
                        
                        // 서명 유형별 결과 처리
                        foreach (var foundSignature in result.Signatures)
                        {
                            Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}");
                            
                            // 특정 서명 유형을 처리합니다
                            switch (foundSignature.SignatureType)
                            {
                                case SignatureType.Text:
                                    var textSignature = foundSignature as TextSignature;
                                    Console.WriteLine($"Text: '{textSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Barcode:
                                    var barcodeSignature = foundSignature as BarcodeSignature;
                                    Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.QrCode:
                                    var qrCodeSignature = foundSignature as QrCodeSignature;
                                    Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Digital:
                                    var digitalSignature = foundSignature as DigitalSignature;
                                    Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
                                    break;
                                    
                                case SignatureType.Metadata:
                                    var metadataSignature = foundSignature as MetadataSignature;
                                    Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
                                    break;
                            }
                            
                            Console.WriteLine(); // 서명 사이에 줄 바꿈 추가
                        }
                    }
                    else
                    {
                        Console.WriteLine("No signatures were found in the document.");
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

## 고급 다중 서명 검색 기술

### 검색 결과 필터링

고급 필터링을 구현하여 검색 결과를 좁힐 수 있습니다.

```csharp
// 페이지 번호로 결과 필터링
var signaturesOnFirstPage = result.Signatures.FindAll(s => s.PageNumber == 1);

// 서명 유형별로 결과 필터링
var digitalSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.Digital);
var qrCodeSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.QrCode);

// 특정 콘텐츠가 포함된 텍스트 서명 필터링
var approvalSignatures = result.Signatures
    .FindAll(s => s is TextSignature && ((TextSignature)s).Text.Contains("Approved"));
```

### 여러 서명 검증

다양한 서명 유형에 대한 검증 논리를 구현합니다.

```csharp
bool ValidateAllSignatures(SearchResult result)
{
    bool isDocumentValid = true;
    
    // 문서에 유효한 디지털 서명이 있는지 확인하세요
    bool hasValidDigitalSignature = result.Signatures
        .Any(s => s is DigitalSignature && ((DigitalSignature)s).IsValid);
    
    if (!hasValidDigitalSignature)
    {
        Console.WriteLine("Warning: Document does not contain a valid digital signature");
        isDocumentValid = false;
    }
    
    // 문서에 필수 QR 코드가 있는지 확인하세요
    bool hasRequiredQRCode = result.Signatures
        .Any(s => s is QrCodeSignature && ((QrCodeSignature)s).Text.Contains("Auth-Code"));
    
    if (!hasRequiredQRCode)
    {
        Console.WriteLine("Warning: Document does not contain the required authentication QR code");
        isDocumentValid = false;
    }
    
    return isDocumentValid;
}
```

### 사용자 정의 처리를 통한 검색

검색 작업에 대한 사용자 정의 처리 논리를 정의할 수 있습니다.

```csharp
// 사용자 정의 처리를 통해 검색 옵션 만들기
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,
    
    // 대리자를 사용하여 사용자 정의 처리 정의
    ProcessCompleted = (signature) =>
    {
        // 사용자 정의 검증 논리 - 지정된 페이지에서만 서명 허용
        TextSignature textSignature = signature as TextSignature;
        return textSignature != null && (textSignature.PageNumber == 1 || textSignature.PageNumber == 2);
    }
};
```

## 결론

이 종합 가이드에서는 GroupDocs.Signature for .NET을 사용하여 문서 내에서 여러 서명 유형을 검색하는 방법을 살펴보았습니다. 다양한 서명 유형에 대한 검색 옵션 설정부터 결과 처리 및 검증까지, 이제 .NET 애플리케이션에서 강력한 서명 검색 기능을 구현하는 방법을 익혔습니다.

여러 서명 유형을 동시에 검색할 수 있는 기능은 문서 검증 프로세스를 개선하고, 보안 조치를 강화하며, 문서 검증 워크플로를 간소화합니다. GroupDocs.Signature는 다양한 문서 형식에서 다양한 서명 유형을 처리할 수 있는 강력하고 유연한 프레임워크를 제공하여 문서 처리 애플리케이션에 탁월한 선택입니다.

## 자주 묻는 질문

### 암호로 보호된 문서에서 서명을 검색할 수 있나요?

네, GroupDocs.Signature는 암호로 보호된 문서에서 서명 검색을 지원합니다. 초기화 시 암호를 입력할 수 있습니다. `Signature` 물체:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // 서명 검색
}
```

### 서명 검색에 지원되는 문서 형식은 무엇입니까?

GroupDocs.Signature는 PDF, Microsoft Office 문서(Word, Excel, PowerPoint), OpenOffice 형식, 이미지 등 다양한 문서 형식을 지원합니다.

### 문서의 특정 페이지로 검색을 제한할 수 있나요?

네, 각 검색 옵션 유형에는 검색할 페이지를 지정할 수 있는 속성이 있습니다.

```csharp
TextSearchOptions options = new TextSearchOptions
{
    AllPages = false,  // 모든 페이지를 검색하지 마세요
    PageNumber = 1,    // 1페이지에서만 검색
    
    // 또는 여러 페이지를 지정하세요
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } }
};
```

### 대용량 문서를 검색할 때 성능을 최적화하려면 어떻게 해야 하나요?

대용량 문서의 경우 다음을 통해 성능을 최적화할 수 있습니다.

1. 검색을 특정 페이지 또는 페이지 범위로 제한
2. 더욱 구체적인 검색 기준을 사용하여 잠재적 일치 항목 수를 줄입니다.
3. 결과 표시에 페이지 매김 구현
4. 동시 결과가 필요하지 않은 경우 한 번에 하나의 서명 유형을 검색합니다.

### GroupDocs.Signature를 확장하여 사용자 정의 서명 유형을 지원할 수 있나요?

GroupDocs.Signature는 일반적인 서명 유형에 대한 기본 제공 지원을 제공하지만, 다음과 같은 방법으로 기능을 확장할 수 있습니다.

1. 사용자 정의 검색 옵션 클래스를 파생하여 생성 `SearchOptions`
2. 사용자 정의 처리 논리를 사용하여 구현 `ProcessCompleted` 대리자
3. 여러 서명 검색과 고급 비즈니스 로직을 결합하는 래퍼 클래스 개발

## 또한 참조

* [API 참조](https://reference.groupdocs.com/signature/net/)
* [GitHub의 코드 예제](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [제품 문서](https://docs.groupdocs.com/signature/net/)
* [제품 페이지](https://products.groupdocs.com/signature/net/)
* [최신 버전 다운로드](https://releases.groupdocs.com/signature/net/)
* [블로그 기사](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [무료 지원 포럼](https://forum.groupdocs.com/c/signature/13)
* [임시 면허](https://purchase.groupdocs.com/temporary-license/)