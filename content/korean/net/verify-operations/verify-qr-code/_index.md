---
title: QR 코드 확인
linktitle: QR 코드 확인
second_title: GroupDocs.Signature .NET API
description: .NET용 GroupDocs.Signature를 사용하여 문서 내의 QR 코드를 확인하는 방법을 알아보세요. 단계별 가이드가 포함된 종합 튜토리얼입니다.
weight: 12
url: /ko/net/verify-operations/verify-qr-code/
---
## 소개
문서 관리 및 인증 영역에서는 서명의 무결성과 유효성을 보장하는 것이 가장 중요합니다. .NET용 GroupDocs.Signature는 문서에 포함된 QR 코드를 확인하기 위한 포괄적인 솔루션을 제공합니다. 이 자습서에서는 .NET용 GroupDocs.Signature를 사용하여 QR 코드를 확인하는 단계별 프로세스를 살펴보겠습니다.
## 전제 조건
확인 프로세스를 시작하기 전에 다음 전제 조건이 충족되었는지 확인하세요.
1.  .NET용 GroupDocs.Signature 설치: 다음에서 .NET용 GroupDocs.Signature를 다운로드하고 설치합니다.[다운로드 링크](https://releases.groupdocs.com/signature/net/).
2. QR 코드가 포함된 문서에 액세스: 확인을 위해 QR 코드가 포함된 샘플 문서를 준비합니다. 

## 네임스페이스 가져오기
먼저, .NET용 GroupDocs.Signature에서 제공하는 기능을 활용하려면 필요한 네임스페이스를 가져와야 합니다. 다음과 같이하세요:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```


이제 .NET용 GroupDocs.Signature를 사용하여 문서에 포함된 QR 코드를 확인하는 프로세스를 자세히 살펴보겠습니다.
## 1단계: 문서 경로 지정
```csharp
string filePath = "sample_multiple_signatures.docx";
```
 교체를 확인하세요`"sample_multiple_signatures.docx"` 문서의 경로와 함께.
## 2단계: 서명 개체 초기화
```csharp
using (Signature signature = new Signature(filePath))
{
    //인증 코드는 여기에 있습니다.
}
```
 초기화`Signature` 문서에 대한 경로를 제공하여 개체를 생성합니다.
## 3단계: 확인 옵션 지정
```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // 이 값은 기본적으로 설정됩니다.
    Text = "John",
    MatchType = TextMatchType.Contains
};
```
 다음과 같은 확인 옵션을 정의합니다.`AllPages` 모든 페이지를 확인하려면`Text` QR 코드 내에서 일치할 텍스트를 지정하고`MatchType` 일치 기준을 정의합니다.
## 4단계: 문서 서명 확인
```csharp
VerificationResult result = signature.Verify(options);
```
 호출`Verify` 의 방법`Signature` 개체, 확인 옵션을 전달합니다.
## 5단계: 확인 결과 처리
```csharp
if (result.IsValid)
{
    // 유효한 서명이 발견되었습니다.
}
else
{
    // 잘못된 서명이 발견되었습니다.
}
```
검증 결과에 따라 성공 또는 실패 시나리오를 적절하게 처리합니다.

## 결론
이 자습서에서는 .NET용 GroupDocs.Signature를 사용하여 문서 내에서 QR 코드를 확인하는 프로세스를 살펴보았습니다. 다음 단계를 수행하면 QR 코드 확인 기능을 .NET 애플리케이션에 원활하게 통합하여 문서 무결성과 신뢰성을 보장할 수 있습니다.
## FAQ
### .NET용 GroupDocs.Signature는 다양한 문서 형식에서 QR 코드를 확인할 수 있습니까?
예, .NET용 GroupDocs.Signature는 QR 코드 확인을 위해 DOCX, PDF 등을 포함한 광범위한 문서 형식을 지원합니다.
### .NET용 GroupDocs.Signature에 대한 무료 평가판이 있습니까?
 예, 무료 평가판을 이용하실 수 있습니다.[릴리스 페이지](https://releases.groupdocs.com/).
### .NET 사용자용 GroupDocs.Signature에는 어떤 지원 옵션이 제공됩니까?
 사용자는 다음을 통해 지원에 액세스할 수 있습니다.[법정](https://forum.groupdocs.com/c/signature/13) GroupDocs.Signature용.
### .NET용 GroupDocs.Signature의 임시 라이센스를 구입할 수 있습니까?
 예, 임시 라이센스는 다음 사이트에서 구입할 수 있습니다.[GroupDocs 구매 페이지](https://purchase.groupdocs.com/temporary-license/).
### .NET용 GroupDocs.Signature에 사용할 수 있는 광범위한 문서가 있습니까?
 물론, 제공된 자세한 설명서를 참조할 수 있습니다.[여기](https://tutorials.groupdocs.com/signature/net/) .NET용 GroupDocs.Signature 기능 활용에 대한 포괄적인 지침을 보려면