---
title: GroupDocs.Signature를 사용하여 Stamp로 서명
linktitle: 스탬프로 서명하기
second_title: GroupDocs.Signature .NET API
description: .NET용 GroupDocs.Signature를 사용하여 .NET 문서에 스탬프 서명을 쉽게 추가하는 방법을 알아보세요. 문서 보안을 강화하세요.
weight: 16
url: /ko/net/advanced-signature-techniques/sign-with-stamp/
---

# GroupDocs.Signature를 사용하여 Stamp로 서명

## 소개
이 자습서에서는 .NET용 GroupDocs.Signature를 사용하여 스탬프로 문서에 서명하는 과정을 안내합니다. 이러한 단계별 지침을 따르면 문서에 스탬프 서명을 쉽게 추가할 수 있습니다.
## 전제 조건
시작하기 전에 다음 전제 조건이 충족되었는지 확인하세요.
1.  .NET SDK용 GroupDocs.Signature: 다음에서 SDK를 다운로드하고 설치합니다.[웹사이트](https://releases.groupdocs.com/signature/net/).
2. 개발 환경: .NET 개발에 적합한 개발 환경이 설정되어 있는지 확인하세요.
3. 서명할 문서: 스탬프로 서명할 문서(예: PDF)를 준비합니다.

## 네임스페이스 가져오기
필요한 네임스페이스를 프로젝트로 가져오는 것부터 시작하세요.
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 1단계: 문서 로드
```csharp
string filePath = "sample.pdf";
using (Signature signature = new Signature(filePath))
{
    // 귀하의 코드는 여기에 있습니다
}
```
## 2단계: 스탬프 서명 옵션 설정
```csharp
StampSignOptions options = new StampSignOptions()
{
    Left = 50,
    Top = 150,                    
    Width = 200,
    Height = 200
};
```
## 3단계: 스탬프 모양 구성
```csharp
StampLine outerLine = new StampLine();
outerLine.Text = " * European Union ";
outerLine.TextRepeatType = StampTextRepeatType.FullTextRepeat;
outerLine.Font.Size = 12;
outerLine.Height = 22;
outerLine.TextBottomIntent = 6;
outerLine.TextColor = Color.WhiteSmoke;
outerLine.BackgroundColor = Color.DarkSlateBlue;
options.OuterLines.Add(outerLine);
StampLine innerLine = new StampLine();
innerLine.Text = "John Smith";
innerLine.TextColor = Color.MediumVioletRed;
innerLine.Font.Size = 20;
innerLine.Font.Bold = true;
innerLine.Height = 40;
options.InnerLines.Add(innerLine);
```
## 4단계: 문서에 서명
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithStamp", fileName);
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## 결론
.NET용 GroupDocs.Signature를 사용하여 문서에 스탬프 서명을 추가하는 것은 이 튜토리얼에서 설명하는 것처럼 간단한 프로세스입니다. 제공된 단계를 통해 문서의 보안과 신뢰성을 쉽게 강화할 수 있습니다.
## FAQ
### 스탬프 서명의 모양을 사용자 정의할 수 있나요?
예, 귀하의 요구 사항에 따라 스탬프 서명의 텍스트, 글꼴, 색상 및 위치 지정과 같은 다양한 측면을 사용자 정의할 수 있습니다.
### GroupDocs.Signature는 여러 문서 형식 서명을 지원합니까?
예, GroupDocs.Signature는 PDF, Microsoft Word, Excel, PowerPoint 등을 포함한 광범위한 문서 형식을 지원합니다.
### GroupDocs.Signature에 사용할 수 있는 평가판이 있습니까?
 예, 다음에서 무료 평가판에 액세스할 수 있습니다.[웹사이트](https://releases.groupdocs.com/).
### 단일 문서에 여러 서명을 추가할 수 있나요?
물론, GroupDocs.Signature를 사용하면 스탬프, 텍스트, 이미지, 디지털 서명을 포함한 여러 서명을 단일 문서에 추가할 수 있습니다.
### 구현 중에 문제가 발생하면 어디서 지원을 받을 수 있나요?
 GroupDocs.Signature 커뮤니티 포럼에서 지원과 지원을 찾을 수 있습니다.[여기](https://forum.groupdocs.com/c/signature/13).