---
title: 여러 옵션으로 서명
linktitle: 여러 옵션으로 서명
second_title: GroupDocs.Signature .NET API
description: .NET용 GroupDocs.Signature를 사용하여 다양한 옵션으로 문서에 서명하는 방법을 알아보세요. 텍스트, 바코드, QR 코드, 디지털 및 이미지로 문서 보안을 강화하세요.
weight: 14
url: /ko/net/advanced-signature-techniques/sign-with-multiple-options/
---

# 여러 옵션으로 서명

## 소개
이 자습서에서는 .NET용 GroupDocs.Signature 라이브러리를 사용하여 여러 서명 옵션을 사용하여 문서에 서명하는 방법을 살펴보겠습니다. 텍스트, 바코드, QR 코드, 디지털, 이미지, 메타데이터 서명과 같은 다양한 옵션을 사용하여 문서에 서명하면 다양성을 제공하고 문서 보안을 강화할 수 있습니다.
## 전제 조건
시작하기 전에 다음 필수 구성 요소가 있는지 확인하세요.
1.  .NET 라이브러리용 GroupDocs.Signature: 다음 위치에서 .NET 라이브러리용 GroupDocs.Signature를 다운로드하고 설치합니다.[여기](https://releases.groupdocs.com/signature/net/).
2. 개발 환경: .NET Framework가 설치된 개발 환경을 설정합니다.
3. 서명할 문서: 서명할 문서(예: Sample.docx)를 준비합니다.
4. 인증서 및 이미지: 디지털 및 이미지 서명에 필요한 인증서와 이미지를 준비합니다.

## 네임스페이스 가져오기
먼저 .NET 애플리케이션에서 GroupDocs.Signature 라이브러리를 사용하는 데 필요한 네임스페이스를 가져옵니다.
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 1단계: 문서 로드
```csharp
string filePath = "sample.docx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithMultiple", "SignWithMultiple.docx");
using (Signature signature = new Signature(filePath))
{
    // 코드가 계속됩니다...
}
```
## 2단계: 서명 옵션 정의
텍스트, 바코드, QR 코드, 디지털, 이미지, 메타데이터 서명 등 다양한 유형과 설정의 여러 서명 옵션을 정의합니다.
```csharp
TextSignOptions textOptions = new TextSignOptions("Text signature")
{
    VerticalAlignment = VerticalAlignment.Top,
    HorizontalAlignment = HorizontalAlignment.Left
};
BarcodeSignOptions barcodeOptions = new BarcodeSignOptions("123456")
{
    EncodeType = BarcodeTypes.Code128,
    Left = 0,
    Top = 150,
    Height = 50,
    Width = 200
};
// 기타 서명 옵션 정의(예: QR 코드, 디지털, 이미지, 메타데이터)...
```
## 3단계: 서명 옵션 목록 만들기
이전에 정의된 모든 옵션을 포함하는 서명 옵션 목록을 정의합니다.
```csharp
List<SignOptions> listOptions = new List<SignOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
// 목록에 다른 서명 옵션 추가...
```
## 4단계: 문서에 서명
서명 옵션 목록으로 문서에 서명하고 서명된 문서를 저장합니다.
```csharp
SignResult result = signature.Sign(outputFilePath, listOptions);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## 결론
.NET용 GroupDocs.Signature를 사용하여 다양한 옵션으로 문서에 서명하면 문서 보안과 다양성을 향상시키는 강력한 솔루션이 제공됩니다. 이 자습서에 설명된 단계를 따르면 다양한 서명 유형을 .NET 애플리케이션에 원활하게 통합할 수 있습니다.
## FAQ
### 디지털 서명에 사용자 정의 이미지를 사용할 수 있습니까?
예, GroupDocs.Signature 라이브러리를 사용하여 디지털 서명에 대한 사용자 정의 이미지를 지정할 수 있습니다.
### GroupDocs.Signature는 다른 문서 형식과 호환됩니까?
예, GroupDocs.Signature는 DOCX, PDF, PPTX 등을 포함한 다양한 문서 형식을 지원합니다.
### 텍스트 서명의 모양을 사용자 정의할 수 있나요?
물론 글꼴 크기, 색상, 스타일을 포함하여 텍스트 서명의 모양을 사용자 정의할 수 있습니다.
### GroupDocs.Signature는 디지털 서명에 대한 암호화를 제공합니까?
예, GroupDocs.Signature는 문서 보안을 보장하기 위해 디지털 서명에 대한 암호화 옵션을 제공합니다.
### .NET용 GroupDocs.Signature에 사용할 수 있는 평가판이 있습니까?
 예, 다음에서 .NET용 GroupDocs.Signature 무료 평가판을 다운로드할 수 있습니다.[여기](https://releases.groupdocs.com/).