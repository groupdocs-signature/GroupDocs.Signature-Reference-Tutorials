---
"description": "GroupDocs.Signature for .NET을 사용하여 이미지에 서명하고 메타데이터를 포함하는 방법을 알아보세요. 작성자 정보, 타임스탬프 및 사용자 지정 데이터를 추가하여 이미지의 신뢰성과 추적성을 강화하세요."
"linktitle": "메타데이터가 포함된 이미지 서명"
"second_title": "GroupDocs.Signature .NET API"
"title": "C# .NET에서 메타데이터로 이미지에 서명하기"
"url": "/ko/net/document-signing/sign-image-with-metadata/"
"weight": 10
---

## 소개

메타데이터를 이용한 디지털 이미지 서명은 진위성, 소유권 및 추적성을 확립하는 데 점점 더 중요해지고 있습니다. GroupDocs.Signature for .NET은 다양한 이미지 형식에 메타데이터 서명을 추가할 수 있는 강력하면서도 사용하기 쉬운 솔루션을 제공합니다. 이 튜토리얼에서는 C#을 사용하여 메타데이터로 이미지에 서명하는 전체 과정을 안내합니다.

메타데이터 서명을 사용하면 작성자 정보, 생성 시간, 고유 식별자 등 중요한 정보를 이미지 파일에 직접 삽입할 수 있습니다. 이 정보는 이미지 파일 자체에 포함되어 이미지 진위 여부를 추적하고 확인하는 신뢰할 수 있는 방법을 제공합니다.

## 필수 조건

이 튜토리얼을 진행하기 전에 다음 사항이 있는지 확인하세요.

1. [.NET용 GroupDocs.Signature](https://releases.groupdocs.com/signature/net/) - 라이브러리를 다운로드하고 설치하세요
2. 개발 환경 - Visual Studio 또는 .NET을 지원하는 호환 IDE
3. 이미지 파일 - 지원되는 형식(PNG, JPG, TIFF 등)의 샘플 이미지 파일
4. 기본 C# 프로그래밍 지식 - C# 프로그래밍 개념에 대한 친숙함

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

소스 이미지의 경로와 서명된 출력을 저장할 위치를 정의합니다.

```csharp
// 소스 이미지 파일의 경로를 지정하세요
string filePath = "sample.png";

// 서명된 이미지에 대한 출력 디렉토리와 파일 이름을 정의합니다.
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignImageWithMetadata", "SignedWithMetadata.png");

// 출력 디렉토리가 존재하는지 확인하세요
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## 2단계: 서명 개체 초기화

소스 이미지 파일을 사용하여 Signature 클래스의 인스턴스를 만듭니다.

```csharp
using (Signature signature = new Signature(filePath))
{
    // 나머지 코드는 여기에 들어갈 것입니다.
}
```

## 3단계: 메타데이터 서명 만들기 및 구성

다음으로, 이미지에 포함할 메타데이터를 정의합니다. GroupDocs.Signature는 메타데이터에 대해 다양한 데이터 유형을 지원합니다.

```csharp
// 메타데이터 ID 초기화(이미지 형식에 따라 다름)
ushort imgsMetadataId = 41996;

// 메타데이터 옵션 개체 생성
MetadataSignOptions options = new MetadataSignOptions();

// 다양한 유형의 메타데이터 서명 추가
options
    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes"))  // 문자열 값
    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // 날짜 시간 값
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // 정수 값
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // 두 배 값
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // 10진수 값
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // 부동 소수점 값
```

## 4단계: 메타데이터로 이미지 서명

이미지에 메타데이터 서명을 적용하고 결과를 저장합니다.

```csharp
// 문서에 서명하고 출력 파일 경로에 저장합니다.
SignResult result = signature.Sign(outputFilePath, options);

// 성공 메시지 표시
Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed image saved at: {outputFilePath}");
```

## 완전한 예

모든 단계를 하나로 합친 전체 코드 예는 다음과 같습니다.

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignImageWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // 파일 경로 지정
            string filePath = "sample.png";            
            string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
            
            // 출력 디렉토리가 존재하는지 확인하세요
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // 메타데이터로 이미지에 서명
            using (Signature signature = new Signature(filePath))
            {
                // 메타데이터 ID 초기화(이미지 형식에 따라 다름)
                ushort imgsMetadataId = 41996;
                
                // 메타데이터 옵션 만들기
                MetadataSignOptions options = new MetadataSignOptions();
                
                // 다양한 유형의 메타데이터 서명 추가
                options
                    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes")) // 문자열 값
                    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // 날짜 시간 값
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // 정수 값
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // 두 배 값
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // 10진수 값
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // 부동 소수점 값
                
                // 문서에 서명하고 파일에 저장하세요
                SignResult result = signature.Sign(outputFilePath, options);
                
                // 결과 표시
                Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## 고급 메타데이터 서명 기술

### 사용자 정의 메타데이터 작업

특정 ID를 사용하여 사용자 정의 메타데이터 필드를 만들 수도 있습니다.

```csharp
// 특정 ID로 사용자 정의 메타데이터 만들기
options.Add(new ImageMetadataSignature(42000, "CustomValue"));
```

### 메타데이터 서명 확인

서명 후 메타데이터 서명을 확인하고 싶을 수 있습니다.

```csharp
// 검증 옵션 만들기
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// 메타데이터 서명 검색
SearchResult result = signature.Search(searchOptions);

// 발견된 서명 표시
Console.WriteLine($"Found {result.Signatures.Count} metadata signatures:");
foreach(var metadataSignature in result.Signatures)
{
    Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value}");
}
```

## 결론

이 튜토리얼에서는 GroupDocs.Signature for .NET을 사용하여 이미지에 메타데이터로 서명하는 방법을 알아보았습니다. 이미지에 메타데이터를 삽입하면 이미지 신뢰성을 높이고, 중요한 정보를 추가하고, 문서 관리 워크플로를 개선하는 훌륭한 방법을 제공합니다. 이 프로세스는 간단하면서도 강력하여 특정 요구 사항에 따라 사용자 정의가 가능합니다.

이미지 파일에 포함된 메타데이터는 저작권 보호, 이미지 출처 추적, 설명 정보 추가, 디지털 관리 체계 구축 등 다양한 목적으로 사용될 수 있습니다. 메타데이터 서명을 구현하면 이미지의 수명 주기 전반에 걸쳐 무결성과 신뢰성을 유지할 수 있습니다.

## 자주 묻는 질문

### 기존의 서명된 이미지에 메타데이터를 추가할 수 있나요?

네, 이미 메타데이터 서명이 포함된 이미지에 메타데이터를 추가할 수 있습니다. 기존 메타데이터는 그대로 유지되며, 그에 따라 새 메타데이터가 추가됩니다.

### 메타데이터 서명에 지원되는 이미지 형식은 무엇입니까?

GroupDocs.Signature for .NET은 PNG, JPEG, TIFF, BMP, GIF 등 다양한 이미지 형식에 대한 메타데이터 서명을 지원합니다. 전체 목록은 다음을 참조하세요. [공식 문서](https://docs.groupdocs.com/signature/net/).

### 이미지의 메타데이터를 암호화하는 것이 가능합니까?

네, GroupDocs.Signature는 보안 강화를 위해 메타데이터 암호화 옵션을 제공합니다. 라이브러리에서 제공하는 암호화 옵션을 사용하여 민감한 메타데이터 정보를 보호할 수 있습니다.

### 서명된 이미지의 진위 여부를 프로그래밍 방식으로 검증할 수 있나요?

물론입니다. GroupDocs.Signature의 검증 방법을 사용하여 메타데이터 서명의 유효성을 검사하고 서명된 이미지의 진위 여부를 확인할 수 있습니다.

### 메타데이터가 있는 이미지에 서명할 때 파일 크기 제한이 있습니까?

라이브러리 자체에는 파일 크기 제한이 없지만, 매우 큰 파일은 처리 시간과 메모리가 더 많이 필요할 수 있습니다. 매우 큰 이미지로 작업할 때는 시스템 리소스를 고려하는 것이 좋습니다.

### 테스트 목적으로 임시 면허를 받으려면 어떻게 해야 하나요?

당신은 얻을 수 있습니다 [임시 면허](https://purchase.groupdocs.com/temporary-license/) 구매하기 전에 GroupDocs.Signature를 테스트해 보세요.

### 더 많은 리소스와 지원은 어디에서 찾을 수 있나요?

- [API 참조](https://reference.groupdocs.com/signature/net/)
- [다운로드](https://releases.groupdocs.com/signature/net/)
- [예시](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [선적 서류 비치](https://docs.groupdocs.com/signature/net/)
- [제품 페이지](https://products.groupdocs.com/signature/net/)
- [블로그](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [지원 포럼](https://forum.groupdocs.com/c/signature/13)