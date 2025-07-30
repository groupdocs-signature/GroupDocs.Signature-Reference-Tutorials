---
"description": "GroupDocs.Signature for .NET을 사용하여 메타데이터 서명을 내장하여 Excel 스프레드시트를 보호하고 강화하세요. 작성자 정보, 타임스탬프 및 사용자 지정 데이터를 추가하여 문서 추적성과 신뢰성을 향상시키세요."
"linktitle": "메타데이터가 포함된 스프레드시트 서명"
"second_title": "GroupDocs.Signature .NET API"
"title": "C# .NET에서 Excel 스프레드시트에 메타데이터 서명 추가"
"url": "/ko/net/document-signing/sign-spreadsheet-with-metadata/"
"weight": 13
---

## 소개

Excel 스프레드시트에는 중요한 비즈니스 데이터, 재무 정보, 그리고 중요한 계산 결과가 포함되는 경우가 많습니다. 이러한 데이터의 진위성을 보장하고, 출처를 추적하고, 무결성을 보호하는 것은 많은 전문 환경에서 매우 중요합니다. 스프레드시트의 보안과 추적성을 강화하는 효과적인 방법 중 하나는 메타데이터 서명을 내장하는 것입니다.

이 포괄적인 튜토리얼에서는 GroupDocs.Signature for .NET을 사용하여 Excel 스프레드시트에 메타데이터 서명을 추가하는 과정을 안내합니다. 메타데이터 서명을 추가하면 작성자 정보, 생성 타임스탬프, 문서 식별자 및 기타 사용자 지정 속성과 같은 중요한 정보를 스프레드시트 파일 구조에 직접 포함할 수 있습니다.

## 필수 조건

이 튜토리얼을 진행하기 전에 다음 사항이 있는지 확인하세요.

1. [.NET용 GroupDocs.Signature](https://releases.groupdocs.com/signature/net/) - 라이브러리를 다운로드하고 설치하세요
2. 개발 환경 - Visual Studio 또는 기타 .NET 호환 IDE
3. Excel 스프레드시트 - 샘플 스프레드시트 파일(XLSX, XLS 등)
4. 기본 C# 지식 - C# 프로그래밍 언어에 대한 친숙함

## 네임스페이스 가져오기

GroupDocs.Signature 기능에 액세스하는 데 필요한 네임스페이스를 가져오는 것으로 시작합니다.

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## 1단계: 파일 경로 설정

소스 스프레드시트의 경로와 서명된 출력이 저장될 위치를 정의합니다.

```csharp
// Excel 파일의 경로를 지정하세요
string filePath = "sample.xlsx";

// 서명된 스프레드시트에 대한 출력 디렉토리와 파일 이름을 정의합니다.
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");

// 출력 디렉토리가 존재하는지 확인하세요
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## 2단계: 서명 개체 초기화

소스 스프레드시트 파일을 사용하여 Signature 클래스의 인스턴스를 만듭니다.

```csharp
using (Signature signature = new Signature(filePath))
{
    // 나머지 코드는 여기에 들어갈 것입니다.
}
```

## 3단계: 메타데이터 서명 만들기 및 구성

다음으로, 메타데이터 옵션을 정의하고 스프레드시트 메타데이터 서명 배열을 만듭니다.

```csharp
// 메타데이터 옵션 개체 생성
MetadataSignOptions options = new MetadataSignOptions();

// 다양한 데이터 유형을 사용하여 스프레드시트 메타데이터 서명 배열을 만듭니다.
SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // 문자열 값
    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // DateTime 값
    new SpreadsheetMetadataSignature("DocumentId", 123456),           // 정수 값
    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // 두 배 값
    new SpreadsheetMetadataSignature("Amount", 123.456M),             // 10진수 값
    new SpreadsheetMetadataSignature("Total", 123.456F)               // 부동 소수점 값
};

// 옵션에 서명 컬렉션 추가
options.Signatures.AddRange(signatures);
```

## 4단계: 메타데이터로 스프레드시트에 서명

메타데이터 서명을 스프레드시트에 적용하고 결과를 저장합니다.

```csharp
// 문서에 서명하고 출력 파일 경로에 저장합니다.
SignResult result = signature.Sign(outputFilePath, options);

// 성공 메시지 표시
Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed spreadsheet saved at: {outputFilePath}");
```

## 완전한 예

모든 단계를 하나로 합친 전체 코드 예는 다음과 같습니다.

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignSpreadsheetWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // 파일 경로 지정
            string filePath = "sample.xlsx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");
            
            // 출력 디렉토리가 존재하는지 확인하세요
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // 메타데이터로 스프레드시트에 서명
            using (Signature signature = new Signature(filePath))
            {
                // 메타데이터 옵션 개체 생성
                MetadataSignOptions options = new MetadataSignOptions();
                
                // 다양한 데이터 유형을 사용하여 스프레드시트 메타데이터 서명 배열을 만듭니다.
                SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
                {
                    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // 문자열 값
                    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // DateTime 값
                    new SpreadsheetMetadataSignature("DocumentId", 123456),           // 정수 값
                    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // 두 배 값
                    new SpreadsheetMetadataSignature("Amount", 123.456M),             // 10진수 값
                    new SpreadsheetMetadataSignature("Total", 123.456F)               // 부동 소수점 값
                };
                
                // 옵션에 서명 컬렉션 추가
                options.Signatures.AddRange(signatures);
                
                // 문서에 서명하고 파일에 저장하세요
                SignResult result = signature.Sign(outputFilePath, options);
                
                // 결과 표시
                Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## 고급 스프레드시트 메타데이터 기술

### 사용자 정의 및 기본 제공 스프레드시트 속성 작업

Excel 스프레드시트에는 파일 속성 대화 상자를 통해 액세스할 수 있는 기본 제공 속성과 사용자 지정 속성이 모두 있습니다. GroupDocs.Signature를 사용하면 다음 두 가지 속성을 모두 사용할 수 있습니다.

```csharp
// 내장된 속성 추가
signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Company", "Sherlock Holmes Consulting"),
    new SpreadsheetMetadataSignature("Category", "Financial"),
    new SpreadsheetMetadataSignature("Keywords", "budget,forecast,analysis"),
    new SpreadsheetMetadataSignature("Comments", "This spreadsheet contains confidential information"),
    new SpreadsheetMetadataSignature("Manager", "John Watson")
};
options.Signatures.AddRange(signatures);

// 사용자 정의 속성 추가
options.Signatures.Add(new SpreadsheetMetadataSignature("Department", "Finance"));
options.Signatures.Add(new SpreadsheetMetadataSignature("SecurityLevel", "Confidential"));
```

### 서명된 스프레드시트에서 메타데이터 검색

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

### 기존 메타데이터 업데이트

동일한 속성 이름을 사용하여 스프레드시트의 기존 메타데이터를 업데이트할 수 있습니다.

```csharp
// 기존 메타데이터 업데이트
options.Signatures.Add(new SpreadsheetMetadataSignature("Author", "Updated Author Name"));
```

## 결론

이 포괄적인 튜토리얼에서는 GroupDocs.Signature for .NET을 사용하여 Excel 스프레드시트에 메타데이터로 서명하는 방법을 알아보았습니다. 스프레드시트 파일에 메타데이터를 포함하면 문서 추적성이 향상되고, 중요한 맥락을 제공하며, 진위 여부를 확인하는 데 도움이 됩니다.

스프레드시트의 메타데이터 서명은 문서 출처, 작성자 및 버전 추적이 중요한 비즈니스 환경에서 특히 유용합니다. 포함된 메타데이터에는 작성자, 생성 시간, 문서 식별자 및 조직의 요구 사항에 맞는 사용자 지정 속성에 대한 정보가 포함될 수 있습니다.

GroupDocs.Signature를 사용하여 메타데이터 서명을 구현하면 Excel 스프레드시트의 무결성을 유지하고 수명 주기 전반에 걸쳐 검증 가능한 정보를 제공할 수 있습니다.

## 자주 묻는 질문

### 일부 속성이 이미 정의된 스프레드시트에 메타데이터를 추가할 수 있나요?

네, 스프레드시트에서 새 메타데이터를 추가하거나 기존 메타데이터를 업데이트할 수 있습니다. GroupDocs.Signature는 새 속성을 추가하거나 이름이 같은 기존 속성을 업데이트하여 통합을 처리합니다.

### 메타데이터 서명에 지원되는 스프레드시트 형식은 무엇입니까?

GroupDocs.Signature for .NET은 XLSX, XLS, XLSM, ODS 등 다양한 스프레드시트 형식에 대한 메타데이터 서명을 지원합니다. 전체 목록은 다음을 참조하세요. [공식 문서](https://docs.groupdocs.com/signature/net/).

### 스프레드시트의 메타데이터 서명이 사용자에게 표시됩니까?

메타데이터 서명은 스프레드시트 콘텐츠 자체에는 표시되지 않습니다. 하지만 Excel이나 다른 호환 애플리케이션의 문서 속성 패널을 통해 확인할 수 있습니다.

### 메타데이터를 추가한 후 스프레드시트가 변조되었는지 프로그래밍 방식으로 검증할 수 있나요?

네, GroupDocs.Signature는 메타데이터 변경을 포함하여 서명 후 문서가 수정되었는지 감지하는 데 도움이 되는 검증 기능을 제공합니다.

### 메타데이터를 추가하면 스프레드시트 기능에 영향을 미칩니까?

메타데이터를 추가해도 파일 크기에는 거의 영향을 미치지 않으며, 스프레드시트 기능에도 전혀 영향을 미치지 않습니다. 계산, 수식 또는 기타 Excel 기능에 영향을 주지 않고 문서 속성을 간편하게 향상시킬 수 있는 방법입니다.

### 더 많은 리소스와 지원은 어디에서 찾을 수 있나요?

- [API 참조](https://reference.groupdocs.com/signature/net/)
- [다운로드](https://releases.groupdocs.com/signature/net/)
- [예시](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [선적 서류 비치](https://docs.groupdocs.com/signature/net/)
- [제품 페이지](https://products.groupdocs.com/signature/net/)
- [블로그](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [지원 포럼](https://forum.groupdocs.com/c/signature/13)
- [임시 면허](https://purchase.groupdocs.com/temporary-license/)