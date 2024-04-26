---
title: 문서에서 QR 코드 서명 삭제
linktitle: 문서에서 QR 코드 서명 삭제
second_title: GroupDocs.Signature .NET API
description: .NET용 GroupDocs.Signature를 사용하여 문서에서 QR 코드 서명을 삭제하는 방법을 알아보세요. 효율적인 서명 관리를 위한 단계별 가이드를 따르세요.
type: docs
weight: 16
url: /ko/net/delete-operations/delete-qr-code-signature/
---
## 소개
이 자습서에서는 .NET용 GroupDocs.Signature를 사용하여 문서에서 QR 코드 서명을 제거하는 과정을 안내합니다. QR 코드 서명을 효과적으로 삭제하려면 다음 단계별 지침을 따르십시오.
## 전제 조건
시작하기 전에 다음 필수 구성 요소가 있는지 확인하세요.
-  .NET용 GroupDocs.Signature: .NET 프로젝트에 GroupDocs.Signature 라이브러리가 설치되어 있는지 확인하세요. 다음에서 다운로드할 수 있습니다.[여기](https://releases.groupdocs.com/signature/net/).
- QR 코드 서명이 포함된 문서: 삭제하려는 QR 코드 서명이 포함된 문서를 준비하세요.
- C# 기본 지식: C# 프로그래밍 언어 기본 사항을 숙지하세요.

## 네임스페이스 가져오기
코드를 살펴보기 전에 필요한 네임스페이스를 C# 파일로 가져옵니다.
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 1단계: 파일 경로 정의
```csharp
// 문서 디렉터리의 경로입니다.
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
// 수정된 문서의 출력 파일 경로를 정의합니다.
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);
// 삭제 메소드는 동일한 문서에 대해 작동하므로 소스 파일을 복사하십시오.
File.Copy(filePath, outputFilePath, true);
```
## 2단계: 서명 개체 초기화
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // QR 코드 서명 검색 옵션을 만듭니다.
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    // 문서에서 QR 코드 서명을 검색하세요.
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```
## 3단계: QR 코드 서명이 있는지 확인하세요.
```csharp
    if (signatures.Count > 0)
    {
        // 문서에서 발견된 첫 번째 QR 코드 서명을 받으세요.
        QrCodeSignature qrCodeSignature = signatures[0];
```
## 4단계: QR 코드 서명 삭제
```csharp
        // 문서에서 QR 코드 서명을 삭제합니다.
        bool result = signature.Delete(qrCodeSignature);
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```
축하해요! .NET용 GroupDocs.Signature를 사용하여 문서에서 QR 코드 서명을 성공적으로 제거했습니다.

## 결론
이 자습서에서는 .NET용 GroupDocs.Signature를 사용하여 문서에서 QR 코드 서명을 삭제하는 방법을 배웠습니다. 제공된 단계를 따르면 .NET 애플리케이션 내에서 서명을 효율적으로 관리하고 조작할 수 있습니다.
## FAQ
### 문서에서 여러 개의 QR 코드 서명을 삭제할 수 있나요?
예, 코드를 수정하여 모든 QR 코드 서명을 반복하고 이에 따라 삭제할 수 있습니다.
### GroupDocs.Signature는 QR 코드 외에 다른 유형의 서명을 지원합니까?
예, GroupDocs.Signature는 텍스트, 이미지, 바코드 등과 같은 다양한 서명 유형을 지원합니다.
### GroupDocs.Signature는 모든 문서 형식과 호환됩니까?
GroupDocs.Signature는 PDF, Microsoft Word, Excel, PowerPoint 등을 포함한 광범위한 문서 형식을 지원합니다.
### 서명에 대한 검색 옵션을 사용자 정의할 수 있습니까?
예, 요구 사항에 따라 검색 옵션을 맞춤화하여 문서 내에서 특정 서명을 찾을 수 있습니다.
### GroupDocs.Signature에 사용할 수 있는 평가판이 있습니까?
 예, 다음에서 GroupDocs.Signature 무료 평가판에 액세스할 수 있습니다.[여기](https://releases.groupdocs.com/).