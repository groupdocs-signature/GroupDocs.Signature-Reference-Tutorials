---
title: ID별 서명 삭제
linktitle: ID별 서명 삭제
second_title: GroupDocs.Signature .NET API
description: GroupDocs.Signature 라이브러리를 사용하여 .NET 문서에서 ID별로 서명을 삭제하는 방법을 알아보세요. 쉬운 단계별 가이드.
weight: 11
url: /ko/net/delete-operations/delete-signature-by-id/
---

# ID별 서명 삭제

## 소개
이 자습서에서는 .NET용 GroupDocs.Signature를 사용하여 ID별로 서명을 삭제하는 방법을 살펴보겠습니다. .NET용 GroupDocs.Signature는 개발자가 .NET 응용 프로그램을 사용하여 다양한 문서 형식의 디지털 서명을 추가, 제거 또는 확인할 수 있는 강력한 라이브러리입니다.
## 전제 조건
시작하기 전에 다음 필수 구성 요소가 있는지 확인하세요.
1.  .NET 라이브러리용 GroupDocs.Signature: 다음에서 라이브러리를 다운로드하고 설치합니다.[여기](https://releases.groupdocs.com/signature/net/).
2. .NET Framework: 시스템에 .NET Framework가 설치되어 있는지 확인하십시오.
3. 서명이 있는 문서: 삭제하려는 서명이 있는 문서(예: DOCX, PDF)를 준비합니다.

## 네임스페이스 가져오기
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 1단계: 파일 경로 정의
먼저 서명이 포함된 문서의 파일 경로와 수정된 문서가 저장될 출력 파일 경로를 지정합니다.
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteById", fileName);
```
## 2단계: 문서 복사
 이후`Delete` 메서드를 사용하면 문서가 제자리에 수정되므로 원본 문서의 복사본을 만드는 것이 가장 좋습니다.
```csharp
File.Copy(filePath, outputFilePath, true);
```
## 3단계: ID별 서명 삭제
 초기화`Signature` 문서 파일 경로가 있는 객체를 사용하고`Delete` ID로 서명을 제거하는 방법입니다.
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    string id = @"eff64a14-dad9-47b0-88e5-2ee4e3604e71";
    bool result = signature.Delete(id);
    if (result)
    {
        Console.WriteLine($"Signature with Id# '{id}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with id# '{id}' was not found!");
    }
}
```

## 결론
이 자습서에서는 .NET용 GroupDocs.Signature를 사용하여 ID별로 서명을 삭제하는 방법을 배웠습니다. 이 라이브러리는 다양한 문서 형식의 디지털 서명을 프로그래밍 방식으로 관리하는 편리한 방법을 제공합니다.
## FAQ
### 여러 서명을 한 번에 삭제할 수 있나요?
 예, ID를 반복하고`Delete` ID별 방법입니다.
### .NET용 GroupDocs.Signature는 모든 문서 형식과 호환됩니까?
.NET용 GroupDocs.Signature는 PDF, DOCX, XLSX 등을 포함한 광범위한 문서 형식을 지원합니다.
### 서명의 모양을 사용자 정의할 수 있나요?
예, 위치, 크기, 글꼴, 색상 등 서명의 모양을 사용자 정의할 수 있습니다.
### 평가판을 사용할 수 있나요?
 예, 다음에서 무료 평가판을 다운로드할 수 있습니다.[여기](https://releases.groupdocs.com/).
### .NET용 GroupDocs.Signature에 대한 도움말이나 지원은 어디서 찾을 수 있나요?
 지원 포럼을 방문할 수 있습니다.[여기](https://forum.groupdocs.com/c/signature/13) 도움을 위해.