---
title: 메타데이터로 PDF에 서명
linktitle: 메타데이터로 PDF에 서명
second_title: GroupDocs.Signature .NET API
description: .NET용 GroupDocs.Signature를 사용하여 메타데이터로 PDF 문서에 서명하는 방법을 알아보세요. 문서 추적성과 신뢰성을 쉽게 강화하세요.
weight: 11
url: /ko/net/document-signing/sign-pdf-with-metadata/
---

# 메타데이터로 PDF에 서명

## 소개
이 자습서에서는 .NET용 GroupDocs.Signature를 사용하여 메타데이터로 PDF 문서에 서명하는 방법을 알아봅니다. PDF에 메타데이터를 추가하면 작성자, 생성 날짜, 문서 ID 등과 같은 문서에 대한 추가 정보를 제공할 수 있습니다.
## 전제 조건
시작하기 전에 다음 사항이 있는지 확인하세요.
1.  .NET용 GroupDocs.Signature: 다음에서 다운로드할 수 있습니다.[여기](https://releases.groupdocs.com/signature/net/).
2. PDF 문서: 서명할 샘플 PDF 파일을 준비합니다.
3. C# 프로그래밍에 대한 기본 지식: 코드 예제를 이해하려면 C# 구문에 대한 지식이 필요합니다.
## 네임스페이스 가져오기
먼저 필요한 클래스와 메서드에 액세스하려면 필요한 네임스페이스를 가져와야 합니다.
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 1단계: PDF 문서 로드
서명하려는 PDF 문서를 로드합니다.
```csharp
string filePath = "sample.pdf";
```
## 2단계: 출력 파일 경로 지정
메타데이터가 포함된 서명된 PDF가 저장될 출력 파일 경로를 정의합니다.
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
```
## 3단계: 서명 인스턴스 생성
PDF 문서에 대한 경로를 제공하여 Signature 인스턴스를 초기화합니다.
```csharp
using (Signature signature = new Signature(filePath))
{
    // 서명 관련 코드가 여기에 표시됩니다.
}
```
## 4단계: 메타데이터 옵션 정의
MetadataSignOptions를 생성하고 해당 값을 사용하여 메타데이터 필드를 추가합니다.
```csharp
MetadataSignOptions options = new MetadataSignOptions();
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // 문자열 값
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // 날짜/시간 값
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // 정수값
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // 이중 값
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // 소수값
    .Add(new PdfMetadataSignature("Total", 123.456F));              // 부동 소수점 가치
```
## 5단계: 문서에 서명
지정된 메타데이터 옵션을 사용하여 PDF 문서에 서명하고 서명된 문서를 저장합니다.
```csharp
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## 결론
이 자습서에서는 .NET용 GroupDocs.Signature를 사용하여 메타데이터로 PDF 문서에 서명하는 방법을 다루었습니다. 단계별 가이드를 따르면 작성자, 생성 날짜 등과 같은 메타데이터 정보를 PDF 파일에 쉽게 추가하여 유틸리티와 추적성을 향상시킬 수 있습니다.
## FAQ
### 내 PDF 문서에 사용자 정의 메타데이터 필드를 추가할 수 있습니까?
예, .NET용 GroupDocs.Signature를 사용하여 필드 이름과 해당 값을 지정하면 사용자 정의 메타데이터 필드를 추가할 수 있습니다.
### .NET용 GroupDocs.Signature는 모든 버전의 .NET Framework와 호환됩니까?
.NET용 GroupDocs.Signature는 다양한 버전의 .NET Framework와 호환되므로 유연성과 통합 용이성을 보장합니다.
### GroupDocs.Signature는 PDF 이외의 다른 문서 형식 서명을 지원합니까?
예, GroupDocs.Signature는 Word, Excel, PowerPoint 등을 포함한 광범위한 문서 형식을 지원합니다.
### .NET용 GroupDocs.Signature를 사용하여 여러 문서에 대량으로 서명할 수 있나요?
예, 파일 목록을 반복하고 프로그래밍 방식으로 서명 프로세스를 적용하여 여러 문서에 대량으로 서명할 수 있습니다.
### GroupDocs.Signature 사용자에게 기술 지원이 제공됩니까?
 예, GroupDocs는 포럼을 통해 전담 기술 지원을 제공합니다. 지원 포럼에 액세스할 수 있습니다.[여기](https://forum.groupdocs.com/c/signature/13).