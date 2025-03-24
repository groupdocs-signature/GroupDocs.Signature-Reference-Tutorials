---
title: 문서 정보 검색
linktitle: 문서 정보 검색
second_title: GroupDocs.Signature .NET API
description: GroupDocs.Signature를 사용하여 .NET에서 문서 관리를 강화하세요. 문서 정보를 단계별로 검색합니다. 다양한 형식을 지원합니다.
weight: 11
url: /ko/net/document-preview-operations/retrieve-document-information/
---
## 소개
디지털 문서 영역에서는 신뢰성과 무결성을 보장하는 것이 무엇보다 중요합니다. .NET용 GroupDocs.Signature는 .NET 환경 내에서 문서 서명을 관리하기 위한 강력한 솔루션을 제공합니다. 이 자습서에서는 포괄적인 이해를 위해 각 단계를 세분화하여 .NET용 GroupDocs.Signature를 사용하여 문서 정보를 검색하는 프로세스를 자세히 살펴봅니다.
## 전제 조건
튜토리얼을 시작하기 전에 다음 전제 조건이 충족되었는지 확인하세요.
1.  설치: 다음에서 다운로드하여 .NET용 GroupDocs.Signature를 설치합니다.[여기](https://releases.groupdocs.com/signature/net/).
2. .NET 환경: .NET 프레임워크에 대한 실무 지식이 있어야 합니다.
3. 문서: 테스트 목적으로 샘플 문서(예: "sample_multiple_signatures.docx")를 준비합니다.

## 네임스페이스 가져오기
문서 서명 검색 프로세스를 진행하기 전에 필요한 네임스페이스를 가져옵니다.
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```

## 1단계: 문서 파일 경로 설정:
정보를 검색하려는 문서의 파일 경로를 정의합니다.
```csharp
string filePath = "sample_multiple_signatures.docx";
```
## 2단계: 서명 개체 인스턴스화:
 인스턴스를 생성합니다.`Signature` 문서 파일 경로를 전달하여 클래스를 생성합니다.
```csharp
using (Signature signature = new Signature(filePath))
{

}
```
## 3단계: 문서 정보 검색:
 활용`GetDocumentInfo()` 문서에 대한 포괄적인 정보를 가져오는 방법입니다.
```csharp
IDocumentInfo documentInfo = signature.GetDocumentInfo();
```
## 4단계: 문서 속성 표시:
형식, 확장자, 크기, 페이지 수 등 문서의 다양한 속성을 출력합니다.
```csharp
Console.WriteLine($"Document properties {Path.GetFileName(filePath)}:");
Console.WriteLine($" - format : {documentInfo.FileType.FileFormat}");
Console.WriteLine($" - extension : {documentInfo.FileType.Extension}");
Console.WriteLine($" - size : {documentInfo.Size}");
Console.WriteLine($" - page count : {documentInfo.PageCount}");
Console.WriteLine($" - Form Fields count : {documentInfo.FormFields.Count}");
Console.WriteLine($" - Text signatures count : {documentInfo.TextSignatures.Count}");
Console.WriteLine($" - Image signatures count : {documentInfo.ImageSignatures.Count}");
Console.WriteLine($" - Digital signatures count : {documentInfo.DigitalSignatures.Count}");
Console.WriteLine($" - Barcode signatures count : {documentInfo.BarcodeSignatures.Count}");
Console.WriteLine($" - QrCode signatures count : {documentInfo.QrCodeSignatures.Count}");
Console.WriteLine($" - FormField signatures count : {documentInfo.FormFieldSignatures.Count}");
foreach (PageInfo pageInfo in documentInfo.Pages)
{
   Console.WriteLine($" - page-{pageInfo.PageNumber} Width {pageInfo.Width}, Height {pageInfo.Height}");
}
```


## 결론
.NET용 GroupDocs.Signature는 .NET 프레임워크 내에서 문서 서명을 원활하게 관리하기 위한 강력한 도구 모음을 제공합니다. 이 가이드에 설명된 단계를 따르면 문서에 대한 포괄적인 정보를 효율적으로 검색하여 향상된 문서 관리 기능을 활용할 수 있습니다.

## FAQ
### .NET용 GroupDocs.Signature는 여러 문서 형식을 처리할 수 있습니까?
예, GroupDocs.Signature는 DOCX, PDF, PNG 및 JPEG를 포함하되 이에 국한되지 않는 광범위한 문서 형식을 지원합니다.
### .NET용 GroupDocs.Signature에 사용할 수 있는 평가판이 있습니까?
 예, 다음에서 평가판 버전에 액세스할 수 있습니다.[여기](https://releases.groupdocs.com/).
### .NET용 GroupDocs.Signature는 디지털 서명을 지원합니까?
물론, GroupDocs.Signature는 디지털 서명에 대한 강력한 지원을 제공하여 문서 신뢰성과 무결성을 보장합니다.
### .NET용 GroupDocs.Signature에 대한 추가 문서와 지원은 어디서 찾을 수 있나요?
 종합 문서를 참조할 수 있습니다.[여기](https://tutorials.groupdocs.com/signature/net/) , 지원을 받으려면 GroupDocs 포럼을 방문하세요.[여기](https://forum.groupdocs.com/c/signature/13).
### .NET용 GroupDocs.Signature에 대한 임시 라이센스를 얻을 수 있습니까?
 예, 임시 라이선스를 구매할 수 있습니다.[여기](https://purchase.groupdocs.com/temporary-license/).