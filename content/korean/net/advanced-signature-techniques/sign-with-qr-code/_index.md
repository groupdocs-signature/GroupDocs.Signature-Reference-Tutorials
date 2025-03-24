---
title: GroupDocs.Signature를 사용하여 QR 코드로 문서 서명
linktitle: QR 코드로 서명
second_title: GroupDocs.Signature .NET API
description: .NET용 GroupDocs.Signature를 사용하여 문서에 QR 코드 서명을 추가하는 방법을 알아보세요. 보안과 인증을 손쉽게 강화하세요.
weight: 15
url: /ko/net/advanced-signature-techniques/sign-with-qr-code/
---
## 소개
이 자습서에서는 .NET용 GroupDocs.Signature를 사용하여 QR 코드로 문서에 서명하는 과정을 안내합니다. .NET용 GroupDocs.Signature는 개발자가 프로그래밍 방식으로 디지털 문서에 다양한 유형의 서명을 추가할 수 있는 강력한 API입니다. QR 코드로 문서에 서명하면 문서에 대한 추가 보안 및 인증 계층을 제공할 수 있습니다.
## 전제 조건
시작하기 전에 다음 필수 구성 요소가 설치되어 있는지 확인하세요.
1.  .NET용 GroupDocs.Signature: 다음에서 라이브러리를 다운로드할 수 있습니다.[웹사이트](https://releases.groupdocs.com/signature/net/).
2. 개발 환경: 컴퓨터에 .NET 개발 환경이 설정되어 있는지 확인하세요.
3. 샘플 문서: QR 코드로 서명하려는 샘플 문서(예: PDF)를 준비합니다.

## 필요한 네임스페이스 가져오기
코드를 살펴보기 전에 필요한 네임스페이스를 가져오겠습니다.
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## 1단계: 파일 경로 정의
```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "SignWithQRCode", fileName);
```
 교체를 확인하세요`"Your Document Directory"` 서명된 문서를 저장하려는 디렉터리의 경로를 사용하세요.
## 2단계: 서명 개체 초기화
```csharp
using (Signature signature = new Signature(filePath))
{
    //서명 코드는 여기에 표시됩니다.
}
```
 초기화`Signature` 서명하려는 문서의 경로가 있는 개체입니다.
## 3단계: QRCodeSignOptions 생성
```csharp
QrCodeSignOptions options = new QrCodeSignOptions("JohnSmith")
{
    EncodeType = QrCodeTypes.QR,
    Left = 50,
    Top = 150,
    Width = 200,
    Height = 200
};
```
 만들기`QrCodeSignOptions` QR 코드 서명에 대해 원하는 설정을 가진 개체입니다. 인코딩할 텍스트, 위치, QR 코드 크기 등의 매개변수를 사용자 정의할 수 있습니다.
## 4단계: 문서에 서명
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
 사용`Sign` 의 방법`Signature` 지정된 옵션을 사용하여 문서에 서명하는 개체입니다. 이 메소드는`SignResult` 서명 프로세스에 대한 정보가 포함된 개체입니다.
## 5단계: 결과 표시
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
서명 프로세스의 성공 여부와 서명된 문서가 저장된 위치를 나타내는 메시지를 표시합니다.

## 결론
이 자습서에서는 .NET용 GroupDocs.Signature를 사용하여 QR 코드로 문서에 서명하는 방법을 배웠습니다. 이러한 간단한 단계를 따르면 디지털 문서에 QR 코드 서명을 추가하여 보안과 인증을 강화할 수 있습니다.

## FAQ
### QR 코드의 모양을 사용자 정의할 수 있나요?
예. 요구사항에 따라 QR 코드의 크기, 위치, 인코딩 유형 등 다양한 매개변수를 사용자 정의할 수 있습니다.
### QR 코드 서명에는 어떤 문서 형식이 지원됩니까?
.NET용 GroupDocs.Signature는 PDF, Word, Excel, PowerPoint 등을 포함한 광범위한 문서 형식을 지원합니다.
### 일괄 처리로 여러 문서에 서명할 수 있습니까?
물론 .NET용 GroupDocs.Signature를 사용하면 여러 문서에 동시에 서명하여 작업 흐름을 간소화할 수 있습니다.
### QR 코드로 서명된 문서의 진위 여부를 확인할 수 있나요?
예, .NET용 GroupDocs.Signature는 서명된 문서의 무결성과 신뢰성을 보장하는 확인 메커니즘을 제공합니다.
### 구매하기 전에 기능을 테스트할 수 있는 평가판이 있습니까?
 예, 다음에서 무료 평가판을 다운로드할 수 있습니다.[웹사이트](https://releases.groupdocs.com/) .NET용 GroupDocs.Signature의 기능을 평가합니다.