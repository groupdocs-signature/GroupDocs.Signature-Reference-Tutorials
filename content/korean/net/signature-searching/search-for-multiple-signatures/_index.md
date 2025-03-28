---
title: 여러 서명 검색
linktitle: 여러 서명 검색
second_title: GroupDocs.Signature .NET API
description: 효율적인 문서 보안 및 무결성을 위해 GroupDocs.Signature를 사용하여 .NET 문서에서 여러 서명을 검색하는 방법을 알아보세요.
weight: 14
url: /ko/net/signature-searching/search-for-multiple-signatures/
---

# 여러 서명 검색

## 소개
.NET용 GroupDocs.Signature는 개발자가 .NET 응용 프로그램을 사용하여 널리 사용되는 문서 형식의 다양한 유형의 서명을 추가, 검색 및 제거할 수 있게 해주는 강력한 라이브러리입니다. 이 자습서에서는 .NET용 GroupDocs.Signature를 사용하여 문서 내에서 여러 서명을 검색하는 데 중점을 둡니다.
## 전제 조건
시작하기 전에 다음 필수 구성 요소가 있는지 확인하세요.
- 시스템에 Visual Studio가 설치되어 있습니다.
- C# 프로그래밍 언어에 대한 기본 이해.
- 프로젝트에 설치된 .NET 라이브러리용 GroupDocs.Signature. 다음에서 다운로드할 수 있습니다.[여기](https://releases.groupdocs.com/signature/net/).

## 네임스페이스 가져오기
먼저, .NET용 GroupDocs.Signature에서 제공하는 클래스와 메서드에 액세스하려면 필요한 네임스페이스를 가져와야 합니다.
```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 1단계: 문서 로드
여러 서명을 검색하려는 문서를 로드합니다. 올바른 파일 경로를 제공했는지 확인하십시오.
```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // 귀하의 코드는 여기에 있습니다
}
```
## 2단계: 검색 옵션 정의
텍스트, 디지털, 바코드, QR 코드, 메타데이터 등 다양한 유형의 서명에 대한 검색 옵션을 정의합니다. 일치시킬 텍스트, 일치 유형, 모든 페이지 검색 등의 검색 기준을 지정할 수 있습니다.
```csharp
// 검색 옵션 정의
TextSearchOptions textOptions = new TextSearchOptions()
{
    AllPages = true
};
DigitalSearchOptions digitalOptions = new DigitalSearchOptions()
{
    AllPages = true
};
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions()
{
    AllPages = true,
    Text = "123456",
    MatchType = TextMatchType.Exact
};
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions()
{
    AllPages = true,
    Text = "John",
    MatchType = TextMatchType.Contains
};
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```
## 3단계: 목록에 검색 옵션 추가
정의된 검색 옵션을 목록에 추가합니다.
```csharp
// 목록에 옵션 추가
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
listOptions.Add(metadataOptions);
listOptions.Add(digitalOptions);
```
## 4단계: 서명 검색
정의된 검색 옵션을 사용하여 문서에서 서명을 검색합니다.
```csharp
// 문서에서 서명 검색
SearchResult result = signature.Search(listOptions);
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains following signatures.");
    foreach (var resSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found at page {resSignature.PageNumber} with type {resSignature.SignatureType} and Id#: {resSignature.SignatureId}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## 결론
이 자습서에서는 .NET용 GroupDocs.Signature를 사용하여 문서 내에서 여러 서명을 검색하는 방법을 배웠습니다. 제공된 단계를 따르면 문서에서 다양한 유형의 서명을 효율적으로 찾아 문서 보안과 무결성을 향상시킬 수 있습니다.
## FAQ
### 다양한 문서 형식의 서명을 검색할 수 있나요?
예, .NET용 GroupDocs.Signature는 Word, PDF, Excel 등을 포함한 광범위한 문서 형식을 지원합니다.
### 서명에 대한 검색 기준을 사용자 정의할 수 있습니까?
물론, 정확한 텍스트 일치를 지정하거나 모든 페이지에서 검색하는 등 요구 사항에 따라 검색 기준을 맞춤화할 수 있습니다.
### .NET용 GroupDocs.Signature는 디지털 서명을 지원합니까?
예, 디지털 서명은 물론 텍스트, 바코드, QR 코드 서명과 같은 다른 유형도 검색할 수 있습니다.
### 서명 검색 기능을 내 .NET 응용 프로그램에 쉽게 통합할 수 있습니까?
예, .NET용 GroupDocs.Signature는 통합 프로세스를 단순화하는 간단한 API를 제공합니다.
### 추가 지원이나 지원은 어디서 찾을 수 있나요?
 GroupDocs.Signature 포럼을 방문할 수 있습니다.[여기](https://forum.groupdocs.com/c/signature/13) 문의사항이나 도움이 필요하시면