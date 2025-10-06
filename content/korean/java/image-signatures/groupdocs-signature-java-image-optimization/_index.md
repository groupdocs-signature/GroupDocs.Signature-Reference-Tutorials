---
"date": "2025-05-08"
"description": "GroupDocs.Signature for Java를 사용하여 QR 코드 서명 및 고급 이미지 저장 옵션을 포함한 이미지에 안전하게 서명하는 방법을 알아보세요. 비즈니스 전문가와 개발자에게 적합합니다."
"title": "Java용 GroupDocs.Signature를 사용한 마스터 이미지 서명 및 최적화"
"url": "/ko/java/image-signatures/groupdocs-signature-java-image-optimization/"
"weight": 1
type: docs
---
# Java용 GroupDocs.Signature를 활용한 이미지 서명 및 최적화 마스터링

오늘날의 디지털 환경에서는 문서에 안전하게 서명하는 것이 필수적입니다. 계약서를 인증하는 비즈니스 전문가든 이미지를 보호하는 개인이든, 강력한 서명 기능은 필수적입니다. **Java용 GroupDocs.Signature** QR 코드 서명을 생성하고 이미지 저장 옵션을 원활하게 최적화하는 강력한 기능을 제공합니다. 이 튜토리얼에서는 이러한 기능을 활용하여 효과적인 문서 관리를 수행하는 방법을 안내합니다.

### 배울 내용:
- 이미지에 QR 코드 서명을 생성합니다.
- 고급 BMP, GIF, JPEG, PNG, TIFF 저장 옵션을 구성합니다.
- 프로젝트에서 Java용 GroupDocs.Signature를 구현합니다.
- 이러한 기능의 실제 적용 사례.

모든 것이 올바르게 설정되었는지 확인해 보세요!

## 필수 조건

구현 세부 사항을 살펴보기 전에 다음 사항을 확인하세요.

### 필수 라이브러리 및 종속성
Java용 GroupDocs.Signature를 사용하려면 해당 라이브러리를 프로젝트에 통합하세요. 빌드 시스템에 따라 라이브러리를 포함하는 방법은 다음과 같습니다.

**메이븐**
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**그래들**
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

또는 다음을 수행할 수 있습니다. [최신 버전을 직접 다운로드하세요](https://releases.groupdocs.com/signature/java/) 프로젝트 설정에 필요한 경우.

### 환경 설정 요구 사항
- Java Development Kit(JDK)가 설치되고 올바르게 구성되었습니다.
- 코드 개발을 위한 IntelliJ IDEA나 Eclipse와 같은 IDE.

### 지식 전제 조건
Java 프로그래밍에 대한 기본적인 이해가 권장됩니다. Maven/Gradle 빌드 도구에 대한 지식이 있으면 도움이 되지만, 설정 과정을 안내해 드리므로 필수는 아닙니다.

## Java용 GroupDocs.Signature 설정

GroupDocs.Signature 작업을 시작하려면 다음 단계를 따르세요.

1. **종속성 설치**: 적절한 종속성을 추가하세요. `pom.xml` 또는 `build.gradle` 위에 표시된 대로 파일입니다.
2. **라이센스 취득**:
   - 획득하다 [무료 체험](https://releases.groupdocs.com/signature/java/) 도서관의 모든 기능을 살펴보세요.
   - 장기 사용을 위해서는 라이센스 구매 또는 임시 라이센스 신청을 고려해 보세요. [구매 페이지](https://purchase.groupdocs.com/buy).

### 기본 초기화 및 설정
환경을 설정한 후 GroupDocs.Signature 인스턴스를 생성하여 초기화합니다. `Signature` 수업. 방법은 다음과 같습니다.

```java
import com.groupdocs.signature.Signature;

public class SignatureSetup {
    public static void main(String[] args) throws Exception {
        // 문서 디렉토리에 대한 파일 경로로 초기화합니다.
        String filePath = "YOUR_DOCUMENT_DIRECTORY/sampleImage.jpg";
        Signature signature = new Signature(filePath);
        
        System.out.println("GroupDocs.Signature initialized successfully!");
    }
}
```

## 구현 가이드

이제 필요한 설정이 완료되었으므로 Java용 GroupDocs.Signature를 사용하여 특정 기능을 구현하는 방법을 알아보겠습니다.

### 이미지에 QR 코드 서명 만들기

#### 개요
이 섹션에서는 이미지 문서에 QR 코드 서명을 생성하는 방법을 안내합니다. 특히 메타데이터나 정보를 이미지에 직접 삽입할 때 유용합니다.

##### 1단계: Signature 객체 초기화
먼저, 다음을 생성하세요. `Signature` 대상 파일을 가리키는 객체입니다.
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sampleImage.jpg";
Signature signature = new Signature(filePath);
```

##### 2단계: QR 코드 서명 옵션 설정
QR 코드 서명 옵션을 구성하세요. 콘텐츠 및 위치와 같은 세부 정보를 지정합니다.

```java
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

QrCodeSignOptions signOptions = new QrCodeSignOptions("JohnSmith");
signOptions.setEncodeType(QrCodeTypes.QR);
signOptions.setLeft(100);  // 왼쪽 여백에서의 위치
signOptions.setTop(100);   // 상단 여백에서의 위치
```

##### 3단계: 문서에 서명하기
마지막으로, QR 코드 서명을 문서에 적용합니다.

```java
signature.sign("output/imageWithQR.jpg", signOptions);
System.out.println("QR Code Signature Applied Successfully!");
```

### 고급 이미지 저장 옵션 구성

#### BMP 저장 옵션 구성
이 구성을 사용하면 BMP 형식으로 이미지가 저장되는 방식을 사용자 지정할 수 있습니다. 필요에 따라 압축률, 해상도 및 기타 매개변수를 조정하세요.

```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.BmpSaveOptions;
import com.groupdocs.signature.domain.enums.BitmapCompression;

BmpSaveOptions bmpSaveOptions = new BmpSaveOptions();
bmpSaveOptions.setAddMissingExtenstion(true);
bmpSaveOptions.setCompression(BitmapCompression.Rgb);
bmpSaveOptions.setHorizontalResolution(7);
bmpSaveOptions.setVerticalResolution(7);
bmpSaveOptions.setBitsPerPixel(16);
bmpSaveOptions.setOverwriteExistingFiles(true);
```

#### GIF 저장 옵션 구성
이미지를 GIF로 저장할 때 배경색, 팔레트 정렬 등의 측면을 제어할 수 있습니다.

```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.GifSaveOptions;

GifSaveOptions gifSaveOptions = new GifSaveOptions();
gifSaveOptions.setBackgroundColorIndex((byte) 2);
gifSaveOptions.setColorResolution((byte) 7);
gifSaveOptions.setDoPaletteCorrection(true);
gifSaveOptions.setTrailer(true);
gifSaveOptions.setInterlaced(false);
gifSaveOptions.setPaletteSorted(true);
gifSaveOptions.setPixelAspectRatio((byte) 24);
gifSaveOptions.setAddMissingExtenstion(true);
```

#### JPEG 저장 옵션 구성
품질, 색상 유형, 압축 모드 설정을 통해 JPEG 이미지 저장을 최적화하세요.

```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.JpegSaveOptions;
import com.groupdocs.signature.domain.enums.JpegCompressionColorMode;
import com.groupdocs.signature.domain.enums.JpegCompressionMode;
import com.groupdocs.signature.domain.enums.JpegRoundingMode;

JpegSaveOptions jpegSaveOptions = new JpegSaveOptions();
jpegSaveOptions.setAddMissingExtenstion(true);
jpegSaveOptions.setBitsPerChannel((byte) 8);
jpegSaveOptions.setColorType(JpegCompressionColorMode.Rgb);
jpegSaveOptions.setComment("signed jpeg file");
jpegSaveOptions.setCompressionType(JpegCompressionMode.Lossless);
jpegSaveOptions.setQuality(100);
jpegSaveOptions.setSampleRoundingMode(JpegRoundingMode.Extrapolate);
```

#### PNG 저장 옵션 구성
PNG를 사용하면 필요에 맞게 비트 심도와 압축 수준을 정의할 수 있습니다.

```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.PngSaveOptions;
import com.groupdocs.signature.domain.enums.PngColorType;
import com.groupdocs.signature.domain.enums.PngFilterType;

PngSaveOptions pngSaveOptions = new PngSaveOptions();
pngSaveOptions.setBitDepth((byte) 8);
pngSaveOptions.setColorType(PngColorType.Grayscale);
pngSaveOptions.setCompressionLevel(9);
pngSaveOptions.setFilterType(PngFilterType.Adaptive);
pngSaveOptions.setProgressive(true);
pngSaveOptions.setAddMissingExtenstion(true);
```

#### TIFF 저장 옵션 구성
TIFF 이미지의 경우 형식 및 기타 관련 설정을 지정할 수 있습니다.

```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.TiffSaveOptions;
import com.groupdocs.signature.domain.enums.TiffFormat;

TiffSaveOptions tiffSaveOptions = new TiffSaveOptions();
tiffSaveOptions.setExpectedTiffFormat(TiffFormat.TiffNoCompressionBw);
tiffSaveOptions.setAddMissingExtenstion(true);
```

## 실제 응용 프로그램

### 실제 사용 사례
1. **계약 서명**: 빠른 확인을 위해 계약서 이미지에 QR 코드를 삽입합니다.
2. **마케팅 자료**: QR 코드를 사용하여 브랜드 정보를 홍보 자료에 직접 추가합니다.
3. **이미지 보관**: 보관하는 동안 품질을 유지하고 파일 크기를 줄이기 위해 이미지 저장 설정을 최적화합니다.