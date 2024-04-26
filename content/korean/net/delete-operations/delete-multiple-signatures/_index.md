---
title: 문서에서 여러 서명 삭제
linktitle: 문서에서 여러 서명 삭제
second_title: GroupDocs.Signature .NET API
description: .NET용 GroupDocs.Signature를 사용하여 문서에서 여러 서명을 손쉽게 삭제할 수 있습니다. 문서 관리 워크플로우를 간소화하세요.
type: docs
weight: 15
url: /ko/net/delete-operations/delete-multiple-signatures/
---
## 소개
디지털 세계에서 문서 관리에는 다양한 서명 처리가 포함되는 경우가 많습니다. 문서에서 여러 서명을 프로그래밍 방식으로 삭제하면 작업 흐름을 간소화하고 효율성을 높일 수 있습니다. .NET용 GroupDocs.Signature를 사용하면 이 작업이 원활하고 간단해집니다. 이 튜토리얼은 문서에서 여러 서명을 삭제하는 과정을 단계별로 안내합니다.
## 전제 조건
튜토리얼을 시작하기 전에 다음 전제조건이 충족되었는지 확인하십시오.
- C# 프로그래밍 언어에 대한 기본 이해.
- .NET 라이브러리용 GroupDocs.Signature를 설치했습니다.
- 테스트용으로 여러 서명이 포함된 샘플 문서입니다.

## 네임스페이스 가져오기
.NET용 GroupDocs.Signature 기능에 액세스하는 데 필요한 네임스페이스를 가져오는 것부터 시작합니다.
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 1단계: 문서 경로 및 파일 이름 정의
여러 서명이 포함된 문서의 파일 경로를 설정합니다. 적절한 파일 경로와 파일 이름이 있는지 확인하세요.
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
```
## 2단계: 처리를 위해 문서 복사
원본 문서를 수정하지 않으려면 처리할 사본을 만드세요.
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "DeleteMultiple", fileName);
File.Copy(filePath, outputFilePath, true);
```
## 3단계: 서명 개체 초기화
출력 파일 경로를 사용하여 Signature 객체를 인스턴스화합니다.
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // 서명 처리 코드가 여기에 표시됩니다.
}
```
## 4단계: 검색 옵션 정의
문서 내의 서명을 식별하기 위한 다양한 검색 옵션을 정의합니다. 옵션에는 텍스트 검색, 이미지 검색, 바코드 검색 및 QR 코드 검색이 포함됩니다.
```csharp
TextSearchOptions textSearchOptions = new TextSearchOptions();
ImageSearchOptions imageSearchOptions = new ImageSearchOptions();
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions();
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions();
// 목록에 옵션 추가
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textSearchOptions);
listOptions.Add(imageSearchOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
```
## 5단계: 서명 검색
정의된 검색 옵션을 기반으로 문서 내의 모든 서명을 찾으려면 검색 작업을 실행하십시오.
```csharp
SearchResult result = signature.Search(listOptions);
```
## 6단계: 서명 삭제
서명이 발견되면 삭제를 진행하세요.
```csharp
if (result.Signatures.Count > 0)
{
    // 모든 서명을 삭제해 보세요.
    DeleteResult deleteResult = signature.Delete(result.Signatures);
    //삭제가 성공했는지 확인
    if(deleteResult.Succeeded.Count == result.Signatures.Count)
    {
        Console.WriteLine("\nAll signatures were successfully deleted!");                        
    }
    else
    {
        Console.WriteLine($"Successfully deleted signatures : {deleteResult.Succeeded.Count}");
        Helper.WriteError($"Not deleted signatures : {deleteResult.Failed.Count}");
    }
    // 삭제된 서명에 대한 정보 표시
    Console.WriteLine("\nList of deleted signatures:");
    int number = 1;
    foreach(BaseSignature temp in deleteResult.Succeeded)
    {
        Console.WriteLine($"Signature #{number++}: Type: {temp.SignatureType} Id:{temp.SignatureId}, Location: {temp.Left}x{temp.Top}. Size: {temp.Width}x{temp.Height}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## 결론
프로그래밍 방식으로 문서에서 여러 서명을 삭제하는 것은 문서 관리에서 중요한 작업입니다. .NET용 GroupDocs.Signature를 사용하면 이 프로세스가 효율적이고 안정적으로 이루어집니다. 이 자습서에 설명된 단계를 따르면 서명 삭제 기능을 .NET 애플리케이션에 쉽게 통합할 수 있습니다.
## FAQ
### .NET용 GroupDocs.Signature는 다양한 문서 형식을 처리할 수 있습니까?
예, .NET용 GroupDocs.Signature는 DOCX, PDF, PPTX, XLSX 등을 포함한 광범위한 문서 형식을 지원합니다.
### 서명 감지를 위한 검색 옵션을 사용자 정의할 수 있습니까?
물론 텍스트 검색, 이미지 검색, 바코드 검색, QR 코드 검색 등의 검색 옵션을 특정 요구 사항에 맞게 맞춤 설정할 수 있습니다.
### .NET용 GroupDocs.Signature는 오류 처리 메커니즘을 제공합니까?
예, 라이브러리는 문서 처리 작업의 원활한 실행을 보장하기 위해 강력한 오류 처리 기능을 제공합니다.
### .NET용 GroupDocs.Signature를 다른 타사 라이브러리와 통합할 수 있습니까?
확실히 .NET용 GroupDocs.Signature는 다른 .NET 라이브러리와 원활하게 통합되어 유연성과 확장성을 제공하도록 설계되었습니다.
### .NET용 GroupDocs.Signature에 대한 추가 지원과 리소스는 어디서 찾을 수 있나요?
 GroupDocs를 방문할 수 있습니다.[법정](https://forum.groupdocs.com/c/signature/13) 서명 관련 토론에 전념하고 커뮤니티와 전문가의 도움을 구합니다.