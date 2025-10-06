---
"date": "2025-05-07"
"description": "GroupDocs.Signature for .NET을 사용하여 QR 코드로 DICOM 이미지에 서명하는 방법을 알아보세요. 이 가이드에서는 의료 영상에서 QR 코드 서명의 설정, 구현 및 검증에 대해 다룹니다."
"title": "GroupDocs.Signature for .NET을 사용하여 QR 코드가 있는 DICOM 이미지에 서명하는 방법&#58; 종합 가이드"
"url": "/ko/net/qr-code-signatures/groupdocs-signature-net-dicom-images-qr-codes/"
"weight": 1
type: docs
---
# .NET용 GroupDocs.Signature를 사용하여 QR 코드가 있는 DICOM 이미지에 서명하는 방법: 종합 가이드

DICOM 파일을 안전하게 인증하는 방법을 찾고 계신가요? 이 상세 가이드에서는 .NET용 GroupDocs.Signature를 사용하여 QR 코드 서명을 DICOM 이미지에 통합하는 방법을 보여줍니다. 의료 전문가, 개발자, 그리고 디지털 의료 문서를 다루는 모든 사람에게 이상적인 이 튜토리얼은 설정부터 구현까지 다룹니다.

## 배울 내용:
- .NET용 GroupDocs.Signature를 사용하여 개발 환경을 설정합니다.
- QR 코드를 사용하여 DICOM 이미지에 서명하는 방법에 대한 단계별 지침입니다.
- DICOM 파일에서 QR 코드 서명을 확인하고 검색하는 방법.
- 검토 목적으로 서명된 문서의 미리보기를 생성하는 기술입니다.
- 성능을 최적화하고 리소스를 효과적으로 관리하기 위한 모범 사례입니다.

먼저, 전제 조건부터 살펴보겠습니다!

## 필수 조건

.NET용 GroupDocs.Signature를 사용하려면 환경이 준비되었는지 확인하세요. 필요한 사항은 다음과 같습니다.

### 필수 라이브러리 및 버전
- **.NET용 GroupDocs.Signature**.NET 프레임워크와의 호환성을 보장합니다.

### 환경 설정 요구 사항
- Windows 또는 Linux 기반의 개발 환경.
- Visual Studio 또는 다른 .NET 호환 IDE가 설치되어 있습니다.

### 지식 전제 조건
- C# 프로그래밍에 대한 기본적인 이해.
- .NET 애플리케이션의 파일 I/O에 익숙함.

## .NET용 GroupDocs.Signature 설정

원하는 방법을 사용하여 GroupDocs.Signature 라이브러리를 설치하세요.

**.NET CLI 사용:**
```bash
dotnet add package GroupDocs.Signature
```

**패키지 관리자:**
```powershell
Install-Package GroupDocs.Signature
```

**NuGet 패키지 관리자 UI:**
- "GroupDocs.Signature"를 검색하여 최신 버전을 설치하세요.

### 라이센스 취득

무료 체험판을 통해 기능을 살펴보세요. 장기간 사용하려면 임시 또는 정식 라이선스를 구매하는 것이 좋습니다. [그룹닥스](https://purchase.groupdocs.com/buy).

설치가 완료되면 라이브러리를 초기화합니다.

```csharp
using GroupDocs.Signature;
// DICOM 파일 경로로 Signature 객체를 초기화합니다.
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample.dicom");
```

## 구현 가이드

### QR 코드로 DICOM 이미지 서명

#### 개요
의료 문서의 진위성과 추적성을 보장하기 위해 QR 코드 서명을 추가하세요.

**1단계: Signature 객체 초기화**

```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY\\sample.dicom";
using (Signature signature = new Signature(filePath))
{
    // 서명 작업을 진행하세요.
}
```

**2단계: QR 코드 서명 옵션 만들기**

텍스트, 크기, 정렬과 같은 속성을 구성합니다.

```csharp
QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues")
{
    AllPages = true,
    Width = 100,
    Height = 100,
    VerticalAlignment = VerticalAlignment.Bottom,
    HorizontalAlignment = HorizontalAlignment.Right,
    Margin = new Padding() { Right = 5, Left = 5 }
};
```

**3단계: XMP 메타데이터 추가**

추가 메타데이터로 문서를 강화합니다.

```csharp
DicomSaveOptions dicomSaveOptions = new DicomSaveOptions()
{
    XmpEntries = new List<DicomXmpEntry>() { new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4") }
};
```

**4단계: 문서 서명**

서명을 실행하고 저장합니다.

```csharp
SignResult signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY\\SignedDicom", options, dicomSaveOptions);
```

### 문서 정보 가져오기

서명된 DICOM 파일에서 메타데이터를 검색하여 데이터 무결성을 보장합니다.

**개요:**
검증을 위해 문서 정보와 XMP 메타데이터 서명에 접근합니다.

**1단계: 문서 정보 검색**

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    IDocumentInfo signedDocumentInfo = signature.GetDocumentInfo();
}
```

**2단계: XMP 데이터 반복 및 인쇄**

메타데이터 세부정보를 표시합니다.

```csharp
foreach (var item in signedDocumentInfo.MetadataSignatures)
{
    Console.WriteLine(item.ToString());
}
```

### DICOM 서명 확인

DICOM 이미지 내 QR 코드 서명의 진위성을 검증합니다.

**개요:**
서명이 정확하고 진짜인지 확인하세요.

**1단계: QR 코드 확인 옵션 생성**

QR 코드의 특정 텍스트와 일치하는 옵션을 설정합니다.

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true,
    Text = "Patient #36363393",
    MatchType = TextMatchType.Contains
};
```

**2단계: 서명 확인**

서명이 기준을 충족하는지 확인하세요.

```csharp
VerificationResult result = signature.Verify(options);

if (result.IsValid)
{
    Console.WriteLine($"DICOM {filePath} has {result.Succeeded.Count} successfully verified signatures!");
}
```

### DICOM에서 서명 검색

서명된 DICOM 이미지 내에서 QR 코드 서명을 찾습니다.

**개요:**
모든 QR 코드 서명을 효율적으로 찾아 문서의 진위성을 관리합니다.

**1단계: QR 코드 서명 검색**

```csharp
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

**2단계: 서명 세부 정보 반복 및 인쇄**

발견된 각 서명의 세부 정보를 검토하세요.

```csharp
foreach (var QrCodeSignature in signatures)
{
    Console.WriteLine($"QRCode signature found at page {QrCodeSignature.PageNumber} with type {QrCodeSignature.EncodeType.TypeName} and text {QrCodeSignature.Text}");
}
```

### 서명된 DICOM의 미리보기 생성

검증을 위해 시각적 미리보기를 만듭니다.

**개요:**
전문 소프트웨어 없이도 이미지 미리보기를 생성하여 콘텐츠를 확인합니다.

**1단계: 스트림 메서드 정의**

미리 보기 생성 중에 파일 스트림 관리 방법을 설정합니다.

```csharp
Stream CreatePageStream(PreviewPageData pageData)
{
    string imageFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignDicomImageAdvanced", $"preview-{pageData.PageNumber}.jpg");
    var folder = Path.GetDirectoryName(imageFilePath);
    if (!Directory.Exists(folder))
    {
        Directory.CreateDirectory(folder);
    }
    return new FileStream(imageFilePath, FileMode.Create);
}

void ReleasePageStream(PreviewPageData pageData, Stream pageStream)
{
    pageStream.Dispose();
}
```

**2단계: 미리보기 생성**

미리보기 생성 프로세스를 실행합니다.

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    PreviewOptions previewOption = new PreviewOptions(CreatePageStream, ReleasePageStream)
    {
        PreviewFormat = PreviewOptions.PreviewFormats.PNG,
    };

    signature.GeneratePreview(previewOption);
}
```

## 실제 응용 프로그램

1. **의료 기록 관리**: 규정 준수를 위해 QR 코드 서명을 사용하여 환자 기록을 인증합니다.
2. **의료 시스템의 감사 추적**: QR 코드를 사용하여 문서 변경 사항을 추적하고 진위 여부를 확인하세요.
3. **안전한 데이터 공유**: 디지털 서명을 내장하여 의료 이미지의 안전한 공유를 보장합니다.
4. **규정 준수 검증**: 법적 요구 사항을 충족하기 위해 DICOM 파일 무결성을 정기적으로 확인합니다.
5. **EHR 시스템과의 통합**: 서명된 DICOM 파일을 전자 건강 기록(EHR) 시스템에 원활하게 통합하여 운영을 간소화합니다.