---
title: 메타데이터로 이미지 서명
linktitle: 메타데이터로 이미지 서명
second_title: GroupDocs.Signature .NET API
description: GroupDocs.Signature를 사용하여 .NET에서 메타데이터로 이미지에 서명하는 방법을 알아보세요. 쉽고 효율적이며 사용자 정의 가능한 메타데이터 서명 솔루션입니다.
weight: 10
url: /ko/net/document-signing/sign-image-with-metadata/
---
## 소개
.NET용 GroupDocs.Signature를 사용하면 개발자가 메타데이터를 사용하여 이미지에 효율적으로 서명할 수 있습니다. 이 튜토리얼에서는 프로세스를 단계별로 안내합니다.
## 전제 조건
시작하기 전에 다음 사항이 있는지 확인하세요.
1. .NET용 GroupDocs.Signature: .NET 프로젝트에 GroupDocs.Signature 패키지를 설치합니다. 다음에서 다운로드할 수 있습니다.[여기](https://releases.groupdocs.com/signature/net/).   
2. 이미지 파일: 메타데이터로 서명하려는 이미지 파일을 준비합니다.

## 네임스페이스 가져오기
C# 코드에서 필요한 네임스페이스를 가져와야 합니다.
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 1단계: 이미지 파일 로드
먼저 이미지 파일의 경로와 메타데이터가 포함된 서명된 이미지의 출력 디렉터리를 지정합니다.
```csharp
string filePath = "sample.png";            
string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
```
## 2단계: 메타데이터 서명 생성
다음으로, 다양한 메타데이터 서명을 생성하고 옵션 서명 컬렉션에 추가합니다.
```csharp
using (Signature signature = new Signature(filePath))
{
    ushort imgsMetadataId = 41996;
    MetadataSignOptions options = new MetadataSignOptions();
    options
        .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Scherlock Holmes")) // 문자열 값
        .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // 날짜 시간 값
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // 정수값
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // 이중 값
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // 소수값
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // 부동 소수점 가치
    
    // 문서에 파일에 서명
    SignResult result = signature.Sign(outputFilePath, options);
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## 결론
이 자습서에서는 .NET용 GroupDocs.Signature를 사용하여 메타데이터로 이미지에 서명하는 방법을 배웠습니다. 다음 단계를 수행하면 메타데이터 서명을 .NET 애플리케이션에 쉽게 통합할 수 있습니다.

## FAQ
### .NET용 GroupDocs.Signature를 사용하여 메타데이터로 여러 이미지에 서명할 수 있습니까?
예, 각 이미지 파일을 반복하고 메타데이터 서명을 적용하면 메타데이터로 여러 이미지에 서명할 수 있습니다.
### .NET용 GroupDocs.Signature에 사용할 수 있는 평가판이 있습니까?
 예, 다음에서 평가판을 다운로드할 수 있습니다.[여기](https://releases.groupdocs.com/).
### .NET용 GroupDocs.Signature는 이미지 외에 다른 파일 형식을 지원합니까?
예, GroupDocs.Signature는 PDF, Word, Excel 등을 포함한 다양한 파일 형식을 지원합니다.
### 메타데이터 서명의 모양을 사용자 정의할 수 있습니까?
예, 글꼴 크기, 색상, 위치 등 메타데이터 서명의 모양을 사용자 정의할 수 있습니다.
### .NET용 GroupDocs.Signature에 대한 지원은 어디서 받을 수 있나요?
 GroupDocs.Signature 포럼에서 지원을 받을 수 있습니다.[여기](https://forum.groupdocs.com/c/signature/13).