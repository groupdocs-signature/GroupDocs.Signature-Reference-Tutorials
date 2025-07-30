---
"date": "2025-05-07"
"description": "GroupDocs.Signature for .NET을 사용하여 HIBC QR 코드가 있는 PDF 문서에 서명하는 방법을 알아보세요. 이 가이드에서는 QR 코드, Aztec 코드, DataMatrix를 포함한 LIC 및 PAS 코드에 대해 설명합니다."
"title": "GroupDocs.Signature for .NET을 사용하여 HIBC QR 코드가 있는 문서에 서명하는 방법&#58; 종합 가이드"
"url": "/ko/net/qr-code-signatures/sign-documents-hibc-qr-groupdocs-dotnet/"
"weight": 1
---

# GroupDocs.Signature for .NET을 사용하여 HIBC QR 코드가 있는 문서에 서명하는 방법

## 소개

오늘날처럼 빠르게 변화하는 비즈니스 환경에서는 문서의 진위성과 무결성을 보장하는 것이 무엇보다 중요합니다. 의약품, 의료 제품 또는 물류 등 어떤 분야를 다루든, 안전한 문서 서명 및 추적 방법을 갖추면 시간을 절약하고 오류를 방지할 수 있습니다. **.NET용 GroupDocs.Signature**HIBC QR 코드를 문서에 원활하게 통합하여 문서 관리 프로세스를 간소화하도록 설계된 강력한 라이브러리입니다.

이 튜토리얼에서는 .NET용 GroupDocs.Signature를 활용하여 QR 코드, Aztec 코드, DataMatrix 등 다양한 유형의 HIBC QR 코드(LIC(라이선스) 및 PAS(제품 인증 시스템))가 있는 PDF 문서에 서명하는 방법을 살펴보겠습니다. 튜토리얼을 마치면 .NET 애플리케이션에서 이러한 솔루션을 구현하는 방법을 확실히 이해하게 될 것입니다.

**배울 내용:**
- .NET용 GroupDocs.Signature를 설정하는 방법
- HIBC LIC QR 코드, Aztec 코드 및 DataMatrix 구현
- HIBC PAS QR 코드, Aztec 코드 및 DataMatrix 추가
- 실제 사용 사례 및 통합 가능성

이러한 기능을 구현하기 전에 전제 조건을 살펴보겠습니다.

## 필수 조건

코딩을 시작하기 전에 다음 사항이 준비되었는지 확인하세요.

- **.NET 환경**: 시스템에 .NET이 설치되어 있는지 확인하세요(가급적 .NET Core 또는 .NET 5/6+).
- **.NET용 GroupDocs.Signature**: 이 라이브러리는 우리의 주요 도구가 될 것입니다. NuGet을 통해 설치할 수 있습니다.
- **기본 프로그래밍 지식**: C#과 .NET에서 파일을 처리하는 것에 익숙하면 좋습니다.

### 필수 라이브러리

.NET에서 GroupDocs.Signature를 사용하려면 다음 방법 중 하나를 사용하여 패키지를 추가해야 합니다.

**.NET CLI**
```bash
dotnet add package GroupDocs.Signature
```

**패키지 관리자**
```powershell
Install-Package GroupDocs.Signature
```

**NuGet 패키지 관리자 UI**
"GroupDocs.Signature"를 검색하여 최신 버전을 설치하세요.

### 라이센스 취득

테스트 목적으로는 무료 체험판 라이선스를 받으실 수 있습니다. 장기간 사용하시려면 구독을 구매하시거나 임시 라이선스를 요청해 보세요.

- **무료 체험**: 입장 [여기](https://releases.groupdocs.com/signature/net/)
- **임시 면허**: 요청 [이 링크](https://purchase.groupdocs.com/temporary-license/)

### 환경 설정

프로젝트가 적절한 .NET 버전을 대상으로 하고 GroupDocs.Signature에 액세스할 수 있도록 환경을 설정하세요. 다음과 같이 애플리케이션에서 초기화하세요.

```csharp
using GroupDocs.Signature;
```

## .NET용 GroupDocs.Signature 설정

.NET에서 GroupDocs.Signature를 사용하려면 라이브러리를 설치하고 프로젝트 내에서 기본 설정을 구성해야 합니다.

### 설치

위에 언급된 방법 중 하나를 따라 프로젝트에 GroupDocs.Signature를 추가하세요. 설치가 완료되면 코드 파일에서 해당 파일을 참조하여 프로젝트가 해당 파일을 사용하도록 설정되었는지 확인하세요.

### 라이센스 초기화

라이센스를 취득한 후 다음과 같이 초기화합니다.

```csharp
SignatureConfig signConfig = new SignatureConfig();
signConfig.LicensePath = "path/to/your/license.lic";
Signature signature = new Signature("Sample.pdf", signConfig);
```

이렇게 설정하면 GroupDocs.Signature의 모든 기능에 제한 없이 액세스할 수 있습니다.

## 구현 가이드

이제 GroupDocs.Signature for .NET과 함께 HIBC QR 코드를 사용하여 각 기능을 구현하는 방법을 살펴보겠습니다.

### HIBC LIC QR 코드로 문서 서명

#### 개요

HIBC LIC QR 코드로 문서에 서명하면 라이선스 관련 규정 준수 및 추적성이 보장됩니다. 이 섹션에서는 PDF 문서에 QR 코드를 생성하고 삽입하는 방법을 안내합니다.

#### 구현 단계

##### 1단계: 소스 및 출력 경로 구성

원본 문서의 위치와 서명된 출력물의 저장 위치를 정의합니다.

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICQR.pdf");
```

##### 2단계: QR 코드 서명 옵션 만들기

특정 텍스트와 설정으로 QR 코드를 구성하세요.

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_QR_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR)
    {
        Left = 1,
        Top = 1,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    // 이러한 옵션을 사용하여 문서에 서명하세요.
    signature.Sign(destinFilePath, hibcLic_QR_Options);
}
```

**설명**: 
- `QrCodeSignOptions` QR 코드의 모양과 내용을 설정합니다. 여기서는 HIBC LIC QR 코드 유형을 지정하고 문서에 배치합니다.
- `ReturnContent` true로 설정하면 서명된 문서의 렌더링된 이미지를 검색할 수 있습니다.

#### 문제 해결 팁

- 문서 경로가 올바르게 지정되었는지 확인하세요.
- GroupDocs.Signature가 모든 기능을 사용할 수 있도록 적절하게 라이선스가 부여되었는지 확인하세요.

### HIBC LIC Aztec 코드로 문서에 서명하세요

#### 개요

아즈텍 코드는 고밀도 정보 저장에 적합한 또 다른 형태의 인코딩을 제공합니다. 이 섹션에서는 GroupDocs.Signature를 사용하여 문서에 아즈텍 코드를 삽입하는 방법을 중점적으로 설명합니다.

#### 구현 단계

##### 1단계: 경로 구성

이전 기능과 유사하게 파일 경로를 정의합니다.

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICAztec");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICAztec.pdf");
```

##### 2단계: Aztec 코드 옵션 구성

GroupDocs.Signature를 사용하여 Aztec 코드를 설정하세요.

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_AZ_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec)
    {
        Left = 1,
        Top = 200,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    signature.Sign(destinFilePath, hibcLic_AZ_Options);
}
```

**설명**: 
- 그만큼 `QrCodeSignOptions` 여기서도 아즈텍 코드 유형을 사용하여 다시 사용되었습니다.
- 위치 지정(`Top`, `Left`) 및 콘텐츠 검색 설정은 QR 코드와 유사합니다.

#### 문제 해결 팁

- 파일 경로가 정확한지 확인하세요.
- GroupDocs.Signature 버전이 Aztec Code 유형을 지원하는지 확인하세요.

### HIBC LIC DataMatrix로 문서 서명

#### 개요

DataMatrix 코드는 데이터를 저장하는 또 다른 강력한 방법을 제공합니다. 이 섹션에서는 DataMatrix를 PDF 문서에 통합하는 방법을 보여줍니다.

#### 구현 단계

##### 1단계: 파일 경로 설정

이전과 마찬가지로 파일의 위치를 확인하세요.

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICDataMatrix");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICDataMatrix.pdf");
```

##### 2단계: DataMatrix 기호 옵션 만들기

DataMatrix 코드를 구성하고 적용합니다.

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_DM_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix)
    {
        Left = 1,
        Top = 400,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    signature.Sign(destinFilePath, hibcLic_DM_Options);
}
```

**설명**: 
- `QrCodeSignOptions` DataMatrix 코드의 모양과 내용을 설정하는 데 사용됩니다.
- 위치 지정(`Top`, `Left`) 및 검색 설정은 이전 코드와 동일한 패턴을 따릅니다.

#### 문제 해결 팁

- 모든 파일 경로가 올바르게 지정되었는지 확인하세요.
- GroupDocs.Signature가 해당 버전에서 DataMatrix 코드 유형을 지원하는지 확인하세요.

### HIBC PAS QR 코드로 문서 서명

#### 개요

HIBC PAS QR 코드로 문서에 서명하면 제품 추적 및 추적성이 향상됩니다. 이 섹션에서는 GroupDocs.Signature를 사용하여 PDF에 PAS QR 코드를 삽입하는 방법을 안내합니다.

#### 구현 단계

##### 1단계: 소스 및 출력 경로 구성

원본 문서의 위치와 서명된 출력물의 저장 위치를 정의합니다.

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCPASQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCPASQR.pdf");
```

##### 2단계: QR 코드 서명 옵션 만들기

특정 텍스트와 설정으로 PAS QR 코드를 구성하세요.

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcPas_QR_Options = new QrCodeSignOptions("PAS123456789012", QrCodeTypes.HIBCPASQR)
    {
        Left = 1,
        Top = 500,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    // 이러한 옵션을 사용하여 문서에 서명하세요.
    signature.Sign(destinFilePath, hibcPas_QR_Options);
}
```

**설명**: 
- `QrCodeSignOptions` HIBC PAS QR 코드 유형에 맞게 구성되고 문서에 배치됩니다.
- `ReturnContent` true로 설정하면 서명된 문서의 렌더링된 이미지를 검색합니다.

#### 문제 해결 팁

- 모든 경로가 올바르게 지정되었는지 확인하세요.
- GroupDocs.Signature가 해당 버전에서 PAS QR 코드 유형을 지원하는지 확인하세요.

### 결론

이 가이드를 따르면 GroupDocs.Signature for .NET을 사용하여 HIBC LIC 및 PAS QR 코드를 PDF 문서에 효율적으로 통합할 수 있습니다. 이 프로세스는 다양한 산업 분야에서 문서 보안, 추적성 및 규정 준수를 강화합니다. 추가 사용자 정의 및 고급 기능에 대한 자세한 내용은 다음을 참조하십시오. [GroupDocs 문서](https://docs.groupdocs.com/signature/net/).