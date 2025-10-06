---
"date": "2025-05-08"
"description": "Java용 GroupDocs.Signature를 사용하여 DICOM 이미지에 안전하게 서명하는 방법을 알아보세요. QR 코드와 메타데이터를 삽입하여 문서 보안을 강화하세요."
"title": "Java용 GroupDocs.Signature를 사용하여 QR 코드 및 메타데이터로 DICOM 이미지에 서명"
"url": "/ko/java/image-signatures/sign-dicom-images-groupdocs-signature-java/"
"weight": 1
type: docs
---
# Java용 GroupDocs.Signature를 사용하여 QR 코드 및 메타데이터가 포함된 DICOM 이미지에 서명하는 방법

## 소개

빠르게 변화하는 디지털 의료 환경에서 환자 데이터를 안전하게 관리하는 것은 매우 중요합니다. 이 튜토리얼에서는 Java용 GroupDocs.Signature를 사용하여 QR 코드와 메타데이터를 사용하여 디지털 의료 영상 및 통신(DICOM) 이미지에 서명하는 강력한 솔루션을 구현하는 방법을 안내합니다. 이러한 기능은 중요한 정보를 의료 이미지에 직접 삽입하여 진위성을 보장하고, 추적성을 향상시키며, 규정 준수를 유지합니다.

### 배울 내용:
- Java용 GroupDocs.Signature를 프로젝트에 통합하는 방법
- QR 코드로 DICOM 이미지에 서명하는 과정.
- 문서 보안을 강화하기 위해 XMP 메타데이터를 추가합니다.
- DICOM 파일 내에서 서명을 검색, 확인 및 검색합니다.
- 서명된 DICOM 이미지의 미리보기를 생성합니다.

시작해 볼까요! 시작하기 전에, 원활하게 따라갈 수 있도록 필요한 모든 것이 있는지 확인해 볼까요?

## 필수 조건

GroupDocs.Signature 기능을 효과적으로 구현하려면 다음 전제 조건을 충족해야 합니다.

### 필수 라이브러리 및 종속성
- **Java용 GroupDocs.Signature**: 이 라이브러리의 23.12 버전 이상이 필요합니다.

### 환경 설정 요구 사항
- **자바 개발 키트(JDK)**: 시스템에 JDK가 설치되어 있는지 확인하세요.
- **IDE**: IntelliJ IDEA나 Eclipse와 같은 통합 개발 환경을 사용하세요.

### 지식 전제 조건
기본적인 이해:
- 자바 프로그래밍과 객체 지향 원칙.
- 종속성 관리를 위한 Maven 또는 Gradle 빌드 도구.

## Java용 GroupDocs.Signature 설정

GroupDocs.Signature를 사용하려면 프로젝트에 종속성으로 추가해야 합니다. 다양한 빌드 도구를 사용하여 이 작업을 수행하는 방법은 다음과 같습니다.

### 메이븐
다음 스니펫을 추가하세요. `pom.xml` 파일:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### 그래들
이것을 당신의 것에 포함시키세요 `build.gradle` 파일:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### 직접 다운로드
또는 다음에서 최신 버전을 다운로드할 수 있습니다. [Java 릴리스용 GroupDocs.Signature](https://releases.groupdocs.com/signature/java/).

#### 라이센스 취득 단계
1. **무료 체험**: 기간 한정 무료 체험판을 통해 기능을 테스트해 보세요.
2. **임시 면허**모든 기능을 탐색할 수 있는 임시 라이센스를 얻으세요.
3. **구입**: 장기적으로 이용하고 싶다면 구독을 구매하세요.

#### 기본 초기화 및 설정

GroupDocs.Signature를 초기화하려면 인스턴스를 생성하세요. `Signature` 수업:
```java
import com.groupdocs.signature.Signature;

// DICOM 파일 경로로 서명 객체를 초기화합니다.
Signature signature = new Signature(filePath);
```

## 구현 가이드

### QR 코드 및 메타데이터를 사용하여 DICOM 이미지 서명

#### 개요
이 기능을 사용하면 QR 코드로 DICOM 이미지에 서명하고 XMP 메타데이터를 추가하여 문서 보안을 강화할 수 있습니다.

#### 1단계: QR 코드 서명 옵션 설정
```java
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.QrCodeSignOptions;

Padding padding = new Padding();
padding.setRight(5);
padding.setLeft(5);

QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues");
options.setAllPages(true);
options.setWidth(100);
options.setHeight(100);
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
options.setMargin(padding);
```
여기서는 DICOM 이미지에서 QR 코드의 모양과 위치를 구성합니다.

#### 2단계: XMP 메타데이터 추가
```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomSaveOptions;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpEntry;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpType;

DicomSaveOptions dicomSaveOptions = new DicomSaveOptions();
List<DicomXmpEntry> xmpEntries = new ArrayList<>();
xmpEntries.add(new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4"));
dicomSaveOptions.setXmpEntries(xmpEntries);
```
이 스니펫은 DICOM 파일에 메타데이터를 추가하여 환자에 대한 추가 정보를 포함합니다.

#### 3단계: 문서에 서명하기
```java
String outputFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/" + fileName;
signature.sign(outputFilePath, options, dicomSaveOptions);
```
그만큼 `sign` 이 방법은 QR 코드와 메타데이터를 DICOM 파일에 쓰고 지정된 위치에 저장합니다.

### 서명된 DICOM 이미지 정보 검색

#### 개요
검증 또는 감사 목적으로 서명된 DICOM 이미지에서 XMP 메타데이터를 추출합니다.
```java
import com.groupdocs.signature.domain.IDocumentInfo;
import com.groupdocs.signature.domain.signatures.MetadataSignature;

IDocumentInfo documentInfo = signature.getDocumentInfo();
for (MetadataSignature item : documentInfo.getMetadataSignatures()) {
    System.out.println(item.toString());
}
```
이 코드는 DICOM 파일과 관련된 모든 메타데이터 서명을 검색하여 인쇄합니다.

### 서명된 DICOM 확인

#### 개요
서명된 DICOM 이미지에 QR 코드 서명이 있는지 확인하여 진위 여부를 확인하세요.
```java
import com.groupdocs.signature.domain.VerificationResult;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;
import com.groupdocs.signature.domain.enums.TextMatchType;

QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();
verifyOptions.setAllPages(true);
verifyOptions.setText("Patient #36363393");
verifyOptions.setMatchType(TextMatchType.Contains);

VerificationResult result = signature.verify(verifyOptions);
if (result.isValid()) {
    System.out.println(filePath + " has successfully verified signatures!");
} else {
    System.out.println(filePath + " failed verification process.");
}
```
이 검증 단계에서는 QR 코드가 예상 기준과 일치하는지 확인하고 문서 무결성을 확인합니다.

### 서명된 DICOM에서 서명 검색

#### 개요
서명된 DICOM 이미지 내의 모든 QR 코드 서명을 찾아 검토하거나 감사합니다.
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.util.List;

List<QrCodeSignature> signatures = signature.search(QrCodeSignature.class);
for (QrCodeSignature qrCodeSignature : signatures) {
    System.out.println("QRCode signature found at page " +
        qrCodeSignature.getPageNumber() + ": " +
        qrCodeSignature.getEncodeType().getTypeName() + ": " +
        qrCodeSignature.getText());
}
```
이 기능은 문서 내의 모든 QR 코드 서명을 스캔하여 포괄적인 가시성을 제공하는 데 유용합니다.

### 서명된 DICOM의 미리보기 생성

#### 개요
서명된 DICOM 이미지의 각 페이지에 대한 미리보기를 생성하면 전체 파일을 열지 않고도 빠르게 시각적으로 검사할 수 있습니다.
```java
import com.groupdocs.signature.options.PreviewOptions;
import java.io.File;
import java.io.FileOutputStream;
import java.nio.file.Paths;

PreviewOptions previewOption = new PreviewOptions(pageNumber -> {
    try {
        String pageFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/image-" + pageNumber + ".jpg";
        return new FileOutputStream(Paths.get(pageFilePath).toFile());
    } catch (Exception e) {
        throw new RuntimeException(e.getMessage());
    }
});

signature.generatePreview(previewOption);
```
이 스니펫은 각 페이지에 대한 이미지 미리보기를 생성하는데, 이는 빠른 확인이나 공유에 유용할 수 있습니다.

## 실제 응용 프로그램

Java용 GroupDocs.Signature는 여러 가지 실제 응용 프로그램을 제공합니다.
- **의료 영상**: QR 코드와 메타데이터를 사용하여 환자 DICOM 이미지에 안전하게 서명하고 관리합니다.
- **법률 문서 관리**: 법적 절차에서 문서의 진위성과 규정 준수를 강화합니다.
- **금융 서비스**: 민감한 금융 문서에 안전한 전자 서명을 구현합니다.