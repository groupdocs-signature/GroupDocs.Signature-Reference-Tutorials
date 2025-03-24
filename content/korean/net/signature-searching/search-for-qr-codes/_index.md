---
title: QR 코드 검색
linktitle: QR 코드 검색
second_title: GroupDocs.Signature .NET API
description: .NET용 GroupDocs.Signature를 사용하여 문서 내에서 QR 코드를 검색하는 방법을 알아보세요. 손쉽게 문서 보안을 강화하세요.
weight: 15
url: /ko/net/signature-searching/search-for-qr-codes/
---
## 소개

디지털 시대에는 문서의 신뢰성과 무결성을 보장하는 것이 무엇보다 중요합니다. .NET용 GroupDocs.Signature는 개발자가 고급 서명 기능을 .NET 응용 프로그램에 원활하게 통합할 수 있도록 해줍니다. 이 포괄적인 가이드는 .NET용 GroupDocs.Signature를 활용하여 문서 내에서 QR 코드를 검색하는 과정을 안내합니다. 결국에는 이 강력한 도구를 활용하여 문서 보안과 효율성을 향상시키는 방법을 확실하게 이해하게 될 것입니다.

## 전제 조건

튜토리얼을 시작하기 전에 다음 전제조건이 충족되었는지 확인하십시오.

1.  .NET SDK용 GroupDocs.Signature: 다음에서 SDK를 다운로드하고 설치합니다.[다운로드 페이지](https://releases.groupdocs.com/signature/net/).
2. 개발 환경: .NET Framework 또는 .NET Core가 설치된 Visual Studio와 같은 .NET 개발 환경을 설정합니다.

## 네임스페이스 가져오기

시작하려면 필요한 네임스페이스를 프로젝트로 가져옵니다.

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;
```

예제를 여러 단계로 나누어 보겠습니다.

## 1단계: 파일 경로 정의

```csharp
string filePath = "sample_multiple_signatures.docx";
```

이 단계에서는 검색하려는 QR 코드가 포함된 문서의 파일 경로를 지정합니다. 파일 경로가 정확하고 애플리케이션 내에서 액세스할 수 있는지 확인하세요.

## 2단계: 서명 개체 초기화

```csharp
using (Signature signature = new Signature(filePath))
{
    // 여기에 귀하의 코드가 있습니다
}
```

 여기서는`Signature` 개체, 문서의 파일 경로를 매개 변수로 전달합니다. 그만큼`using` 성명은 사용 후 자원의 적절한 폐기를 보장합니다.

## 3단계: 서명 검색

```csharp
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

 이 단계에는 다음을 사용하여 문서 내에서 QR 코드 서명을 검색하는 작업이 포함됩니다.`Search` 의 방법`Signature` 물체. 우리는 서명 유형을 다음과 같이 지정합니다.`QrCodeSignature` 목록에서 결과를 검색합니다.

## 4단계: 결과 반복

```csharp
foreach (var qrCodeSignature in signatures)
{
    Console.WriteLine($"QRCode signature found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName} and text {qrCodeSignature.Text}");
}
```

이 마지막 단계에서는 문서에 있는 QR 코드 서명 목록을 반복합니다. 발견된 각 서명에 대해 페이지 번호, 인코딩 유형, QR 코드와 관련된 텍스트 등 관련 정보를 인쇄합니다.

## 결론

.NET용 GroupDocs.Signature는 서명 기능을 .NET 응용 프로그램에 통합하기 위한 강력한 솔루션을 제공합니다. 이 가이드를 따르면 문서 내에서 QR 코드를 쉽게 검색하여 문서 보안과 생산성을 향상시키는 방법을 배웠습니다.

## FAQ

### Q: .NET용 GroupDocs.Signature는 QR 코드 외에 다른 서명 유형을 처리할 수 있습니까?
A: 예, .NET용 GroupDocs.Signature는 디지털 서명, 바코드 서명 등을 포함한 다양한 서명 유형을 지원합니다.

### 질문: .NET용 GroupDocs.Signature에 사용할 수 있는 평가판이 있습니까?
 A: 예. 다음에서 .NET용 GroupDocs.Signature 무료 평가판에 액세스할 수 있습니다.[릴리스 페이지](https://releases.groupdocs.com/).

### 질문: .NET용 GroupDocs.Signature에 대한 지원을 받으려면 어떻게 해야 합니까?
 답변: 다음에서 도움을 구하고 커뮤니티에 참여할 수 있습니다.[GroupDocs.Signature 포럼](https://forum.groupdocs.com/c/signature/13).

### Q: .NET용 GroupDocs.Signature에 임시 라이센스를 사용할 수 있습니까?
 A: 예, 임시 라이선스는 다음 사이트에서 취득할 수 있습니다.[구매 페이지](https://purchase.groupdocs.com/temporary-license/) 테스트 및 평가 목적으로.

### 질문: .NET용 GroupDocs.Signature 라이센스는 어디에서 구입할 수 있습니까?
 A: 다음에서 .NET용 GroupDocs.Signature 라이센스를 구입할 수 있습니다.[구매 페이지](https://purchase.groupdocs.com/buy).