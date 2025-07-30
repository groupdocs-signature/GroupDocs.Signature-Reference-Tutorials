---
"description": "GroupDocs.Signature for .NET을 사용하여 PDF 문서에 메타데이터 서명을 통합하세요. 작성자 정보, 타임스탬프 및 사용자 지정 데이터를 삽입하여 PDF의 신뢰성과 추적성을 강화하는 방법을 알아보세요."
"linktitle": "메타데이터로 PDF 서명"
"second_title": "GroupDocs.Signature .NET API"
"title": "C# .NET에서 PDF 문서에 메타데이터 서명 추가"
"url": "/ko/net/document-signing/sign-pdf-with-metadata/"
"weight": 11
---

## 소개

PDF(Portable Document Format) 문서는 일관성과 플랫폼 독립성 덕분에 여러 산업 분야에서 널리 사용됩니다. 이러한 문서의 진위성과 추적성을 보장하는 것은 많은 전문 분야에서 매우 중요합니다. 이를 위한 효과적인 방법 중 하나는 PDF 파일 자체에 메타데이터를 삽입하는 것입니다.

이 포괄적인 튜토리얼에서는 GroupDocs.Signature for .NET을 사용하여 PDF 문서에 메타데이터로 서명하는 방법을 살펴보겠습니다. 메타데이터 서명을 사용하면 문서의 모양을 시각적으로 변경하지 않고도 작성자 정보, 생성 타임스탬프, 문서 식별자, 사용자 지정 값 등의 추가 정보를 문서에 포함할 수 있습니다.

## 필수 조건

시작하기 전에 다음 사항이 준비되었는지 확인하세요.

1. [.NET용 GroupDocs.Signature](https://releases.groupdocs.com/signature/net/) - 라이브러리를 다운로드하고 설치하세요
2. 개발 환경 - Visual Studio 또는 기타 .NET 호환 IDE
3. PDF 문서 - 서명을 위한 샘플 PDF 파일
4. 기본 C# 지식 - C# 프로그래밍 언어에 대한 친숙함

## 네임스페이스 가져오기

GroupDocs.Signature 기능에 액세스하는 데 필요한 네임스페이스를 가져오는 것부터 시작합니다.

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## 1단계: 파일 경로 설정

먼저 PDF 문서의 경로를 정의하고 서명된 출력물을 저장할 위치를 지정합니다.

```csharp
// PDF 문서 경로를 지정하세요
string filePath = "sample.pdf";

// 출력 디렉토리와 파일 경로를 정의합니다.
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignPdfWithMetadata", "SignedWithMetadata.pdf");

// 출력 디렉토리가 존재하는지 확인하세요
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## 2단계: 서명 개체 초기화

소스 PDF 문서로 Signature 클래스의 인스턴스를 만듭니다.

```csharp
using (Signature signature = new Signature(filePath))
{
    // 서명 코드는 여기에 입력됩니다.
}
```

## 3단계: 메타데이터 옵션 정의

다양한 유형의 메타데이터 서명을 추가하여 메타데이터 옵션을 만들고 구성합니다.

```csharp
// 메타데이터 옵션 개체 생성
MetadataSignOptions options = new MetadataSignOptions();

// Fluent 인터페이스를 사용하여 다양한 유형의 메타데이터를 추가합니다.
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // 문자열 값
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // DateTime 값
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // 정수 값
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // 두 배 값
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // 10진수 값
    .Add(new PdfMetadataSignature("Total", 123.456F));              // 부동 소수점 값
```

## 4단계: 메타데이터로 PDF 서명

PDF 문서에 메타데이터 서명을 적용하고 결과를 저장합니다.

```csharp
// 문서에 서명하고 출력 경로에 저장하세요
SignResult result = signature.Sign(outputFilePath, options);

// 성공 메시지 표시
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed document saved at: {outputFilePath}");
```

## 완전한 예

모든 단계를 하나로 합친 전체 코드 예는 다음과 같습니다.

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignPdfWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // 파일 경로 지정
            string filePath = "sample.pdf";
            string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
            
            // 출력 디렉토리가 존재하는지 확인하세요
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // 메타데이터로 PDF에 서명
            using (Signature signature = new Signature(filePath))
            {
                // 메타데이터 옵션 개체 생성
                MetadataSignOptions options = new MetadataSignOptions();
                
                // 다양한 유형의 메타데이터 서명 추가
                options
                    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // 문자열 값
                    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // DateTime 값
                    .Add(new PdfMetadataSignature("DocumentId", 123456))            // 정수 값
                    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // 두 배 값
                    .Add(new PdfMetadataSignature("Amount", 123.456M))              // 10진수 값
                    .Add(new PdfMetadataSignature("Total", 123.456F));              // 부동 소수점 값
                
                // 문서에 서명하고 파일에 저장하세요
                SignResult result = signature.Sign(outputFilePath, options);
                
                // 결과 표시
                Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## 고급 PDF 메타데이터 작업

### 네임스페이스 지원을 통한 사용자 지정 메타데이터 추가

PDF 문서는 XML 네임스페이스 지원을 통해 사용자 정의 메타데이터를 지원합니다.

```csharp
// 네임스페이스를 사용하여 사용자 정의 메타데이터 추가
options.Add(new PdfMetadataSignature("CustomProperty", "Custom Value")
{
    NamespaceUri = "http://your-namespace.com/schema"
});
```

### 서명된 PDF에서 메타데이터 검색

서명 후 메타데이터를 확인하거나 추출할 수 있습니다.

```csharp
// 메타데이터에 대한 검색 옵션 만들기
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// 메타데이터 서명 검색
SearchResult searchResult = signature.Search(searchOptions);

// 발견된 서명 표시
Console.WriteLine($"Found {searchResult.Signatures.Count} metadata signatures:");
foreach (var foundSignature in searchResult.Signatures)
{
    MetadataSignature metadataSignature = foundSignature as MetadataSignature;
    if (metadataSignature != null)
    {
        Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value} ({metadataSignature.Value.GetType().Name})");
    }
}
```

### 표준 PDF 메타데이터 작업

PDF 문서에는 액세스하고 수정할 수 있는 표준 메타데이터 필드가 있습니다.

```csharp
// 표준 PDF 메타데이터 필드 설정
options
    .Add(new PdfMetadataSignature("Title", "Important Contract"))
    .Add(new PdfMetadataSignature("Subject", "Legal Agreement"))
    .Add(new PdfMetadataSignature("Keywords", "contract, agreement, legal, binding"))
    .Add(new PdfMetadataSignature("Creator", "Legal Department"))
    .Add(new PdfMetadataSignature("Producer", "GroupDocs.Signature"));
```

## 결론

이 튜토리얼에서는 GroupDocs.Signature for .NET을 사용하여 PDF 문서에 메타데이터로 서명하는 방법을 알아보았습니다. PDF 파일에 메타데이터를 포함하면 문서의 신뢰성을 높이고, 중요한 정보를 추가하고, 문서 관리 워크플로를 개선하는 데 매우 효과적입니다.

PDF의 메타데이터 서명은 문서 추적 및 진위 확인이 필수적인 비즈니스 환경에서 특히 중요합니다. 내장된 메타데이터에는 문서의 출처, 작성자, 생성 시간, 버전 및 조직의 워크플로와 관련된 사용자 지정 속성에 대한 정보가 포함될 수 있습니다.

GroupDocs.Signature를 사용하여 메타데이터 서명을 구현하면 PDF 문서의 무결성을 유지하고 문서 수명 주기 전반에 걸쳐 검증 가능한 정보를 제공할 수 있습니다.

## 자주 묻는 질문

### PDF 문서의 기존 메타데이터를 수정할 수 있나요?

네, PDF 문서의 기존 메타데이터를 수정할 수 있습니다. 기존 메타데이터 서명과 동일한 이름의 새 메타데이터 서명을 적용하면 값도 그에 따라 업데이트됩니다.

### PDF 문서의 메타데이터 서명이 최종 사용자에게 표시됩니까?

메타데이터 서명은 문서 콘텐츠 자체에는 표시되지 않습니다. 하지만 Adobe Acrobat과 같은 PDF 리더의 문서 속성 패널이나 메타데이터 보기 전용 도구를 사용하여 볼 수 있습니다.

### PDF의 메타데이터를 암호화하거나 보호할 수 있나요?

GroupDocs.Signature는 암호화를 포함한 문서 보안 옵션을 제공합니다. 문서 수준 암호화를 적용하여 메타데이터를 포함한 전체 PDF를 보호할 수 있습니다.

### PDF에 추가할 수 있는 메타데이터의 양에 제한이 있나요?

PDF 사양에는 엄격한 제한이 없지만, 메타데이터를 과도하게 추가하면 파일 크기가 커질 수 있습니다. 메타데이터에는 관련성 있고 필요한 정보만 포함하는 것이 좋습니다.

### 메타데이터를 추가한 후 PDF가 변조되었는지 프로그래밍 방식으로 검증할 수 있나요?

네, GroupDocs.Signature는 메타데이터 변경을 포함하여 서명 후 문서가 수정되었는지 감지하는 데 도움이 되는 검증 기능을 제공합니다.

### 더 많은 리소스와 지원은 어디에서 찾을 수 있나요?

- [API 참조](https://reference.groupdocs.com/signature/net/)
- [다운로드](https://releases.groupdocs.com/signature/net/)
- [예시](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [선적 서류 비치](https://docs.groupdocs.com/signature/net/)
- [제품 페이지](https://products.groupdocs.com/signature/net/)
- [블로그](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [지원 포럼](https://forum.groupdocs.com/c/signature/13)
- [임시 면허](https://purchase.groupdocs.com/temporary-license/)