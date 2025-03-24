---
title: 메타데이터로 프레젠테이션에 서명
linktitle: 메타데이터로 프레젠테이션에 서명
second_title: GroupDocs.Signature .NET API
description: .NET용 GroupDocs.Signature를 사용하여 메타데이터로 프레젠테이션 파일에 서명하는 방법을 알아보세요. 문서 무결성을 강화하고 귀중한 정보를 추가하세요.
weight: 12
url: /ko/net/document-signing/sign-presentation-with-metadata/
---
## 소개
이 자습서에서는 .NET용 GroupDocs.Signature 라이브러리를 사용하여 메타데이터로 프레젠테이션 파일(PPTX)에 서명하는 방법을 알아봅니다. 메타데이터로 프레젠테이션에 서명하면 작성자 이름, 생성 날짜, 문서 ID, 서명 ID 및 다양한 숫자 값과 같은 중요한 정보가 문서에 추가됩니다.
## 전제 조건
시작하기 전에 다음 사항이 있는지 확인하세요.
1.  .NET 라이브러리용 GroupDocs.Signature: 다음에서 라이브러리를 다운로드하고 설치합니다.[여기](https://releases.groupdocs.com/signature/net/).
2. 개발 환경: .NET 개발 환경이 설정되어 있는지 확인하세요.
3. 프리젠테이션 파일: 서명할 샘플 프리젠테이션 파일(PPTX 형식)을 준비합니다.
4. C#에 대한 기본 이해: C# 프로그래밍 언어에 익숙하면 도움이 됩니다.

## 네임스페이스 가져오기
코드를 살펴보기 전에 필요한 네임스페이스를 가져오겠습니다.
```csharp
using System;
using System.IO;
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;
    using GroupDocs.Signature.Options;
```
## 1단계: 프리젠테이션 파일 로드
```csharp
string filePath = "sample.pptx";
```
 바꾸다`"sample.pptx"` 프레젠테이션 파일의 경로를 사용하세요.
## 2단계: 출력 파일 경로 지정
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPresentationWithMetadata", "SignedWithMetadata.pptx");
```
파일 이름과 함께 서명된 프레젠테이션 파일을 저장할 디렉터리를 지정합니다.
## 3단계: 서명 개체 초기화
```csharp
using (Signature signature = new Signature(filePath))
```
프리젠테이션 파일의 경로를 제공하여 Signature 객체를 초기화합니다.
## 4단계: 메타데이터 서명 옵션 정의
```csharp
MetadataSignOptions options = new MetadataSignOptions();
```
메타데이터 서명 옵션을 정의하려면 MetadataSignOptions 인스턴스를 생성하세요.
## 5단계: 메타데이터 서명 생성
```csharp
PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Author", "Mr.Scherlock Holmes"),
    new PresentationMetadataSignature("CreatedOn", DateTime.Now),
    new PresentationMetadataSignature("DocumentId", 123456),
    new PresentationMetadataSignature("SignatureId", 123.456D),
    new PresentationMetadataSignature("Amount", 123.456M),
    new PresentationMetadataSignature("Total", 123.456F)
};
```
각각 메타데이터 서명을 나타내는 PresentationMetadataSignature 개체의 배열을 만듭니다. 문자열, 날짜/시간, 정수, 실수, 소수, 부동 소수점 등 다양한 유형의 메타데이터를 추가할 수 있습니다.
## 6단계: 옵션에 서명 추가
```csharp
options.Signatures.AddRange(signatures);
```
생성된 메타데이터 서명을 MetadataSignOptions 개체에 추가합니다.
## 7단계: 문서에 서명
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
지정된 옵션을 사용하여 메타데이터로 프레젠테이션 파일에 서명하고 서명된 파일을 출력 경로에 저장합니다.
## 8단계: 결과 표시
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
적용된 서명 수 및 서명된 파일이 저장되는 경로와 함께 성공 메시지를 표시합니다.

## 결론
이 자습서에서는 .NET용 GroupDocs.Signature 라이브러리를 사용하여 메타데이터로 프레젠테이션 파일에 서명하는 방법을 배웠습니다. 메타데이터 서명을 추가하면 문서의 무결성이 향상되고 해당 콘텐츠에 대한 귀중한 정보가 제공됩니다.

## FAQ
### .NET용 GroupDocs.Signature를 사용하여 메타데이터로 PPTX 외에 다른 문서 형식에 서명할 수 있습니까?
예, GroupDocs.Signature는 메타데이터 서명을 위해 Word, Excel, PDF 등 다양한 문서 형식을 지원합니다.
### .NET용 GroupDocs.Signature는 .NET Core와 호환됩니까?
예, 라이브러리는 .NET Framework 및 .NET Core 모두와 호환됩니다.
### 메타데이터 서명의 모양을 사용자 정의할 수 있습니까?
예, 요구 사항에 따라 메타데이터 서명의 모양, 위치 및 기타 속성을 사용자 정의할 수 있습니다.
### .NET용 GroupDocs.Signature는 서명된 문서에 대한 암호화를 제공합니까?
예, GroupDocs.Signature는 서명된 문서를 무단 액세스로부터 보호하는 암호화 옵션을 제공합니다.
### 구매하기 전에 테스트할 수 있는 평가판이 있나요?
 예, 다음에서 .NET용 GroupDocs.Signature 무료 평가판을 이용할 수 있습니다.[여기](https://releases.groupdocs.com/).