---
"date": "2025-05-08"
"description": "Java용 GroupDocs.Signature를 사용하여 HIBC 데이터를 인코딩하는 QR 코드로 문서에 안전하게 서명하는 방법을 알아보세요. 지금 바로 문서 관리 프로세스를 간소화하세요."
"title": "GroupDocs.Signature for Java를 사용한 QR 코드로 마스터 문서 서명하기&#58; 종합 가이드"
"url": "/ko/java/qr-code-signatures/groupdocs-signature-qr-code-document-signing/"
"weight": 1
---

# Java용 GroupDocs.Signature를 사용하여 QR 코드를 사용한 마스터 문서 서명

## 소개

디지털 시대에 제약 데이터를 효율적으로 관리하고 보호하는 것은 규정 준수 및 운영 효율성에 필수적입니다. 포괄적인 제품 정보를 문서에 통합하는 것은 어려울 수 있습니다. 이 튜토리얼에서는 **Java용 GroupDocs.Signature** QR 코드 내에 건강산업 바코드(HIBC) 데이터를 인코딩하고 원활하게 문서에 서명합니다.

### 배울 내용:
- Java용 GroupDocs.Signature를 설정합니다.
- HIBCLICPrimaryData, HIBCLICSecondaryAdditionalData 및 이를 결합한 형태의 인스턴스를 생성합니다.
- 자세한 제품 정보가 인코딩된 QR 코드를 사용하여 문서에 서명하세요.
- 리소스를 효과적으로 관리하면서 성과를 최적화합니다.

## 필수 조건

### 필수 라이브러리 및 종속성
Java에서 GroupDocs.Signature를 사용하려면 다음이 필요합니다.
- **자바 개발 키트(JDK)**: 버전 8 이상.
- **메이븐** 또는 **그래들**: 종속성 관리를 위해.

### 환경 설정 요구 사항
Maven이나 Gradle을 사용하도록 개발 환경을 구성하여 종속성과 프로젝트 빌드 관리를 간소화하세요.

### 지식 전제 조건
Java 프로그래밍에 대한 지식은 코드 조각과 구현 세부 사항을 이해하는 데 도움이 됩니다.

## Java용 GroupDocs.Signature 설정

### 설치 정보

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

**직접 다운로드**: 최신 버전을 다운로드하세요 [Java 릴리스용 GroupDocs.Signature](https://releases.groupdocs.com/signature/java/).

### 라이센스 취득 단계
1. **무료 체험**: 기본 기능을 테스트하려면 평가판을 다운로드하세요.
2. **임시 면허**: 평가 기간 동안 제한 없이 모든 기능에 액세스하세요.
3. **구입**: 장기 프로젝트의 경우 라이선스 구매를 고려하세요.

#### 기본 초기화 및 설정
설치 후 초기화 `Signature` 서명하려는 문서의 파일 경로를 포함하는 객체:
```java
String filePath = "Sample.pdf";
Signature signature = new Signature(filePath);
```

## 구현 가이드

### HIBC LIC 기본 데이터 생성
**개요**: 이 섹션에서는 인스턴스를 생성하고 구성하는 방법을 보여줍니다. `HIBCLICPrimaryData`, 필수적인 제품 정보를 담고 있습니다.

#### 1단계: 기본 데이터 개체 초기화
```java
HIBCLICPrimaryData primaryData = new HIBCLICPrimaryData();
```

#### 2단계: 필수 속성 설정
- **제품 또는 카탈로그 번호**: 제품의 고유 식별자입니다.
- **라벨러 식별 코드**: 제조업체를 식별합니다.
- **측정 단위 ID**: 측정 단위를 지정합니다.

```java
primaryData.setProductOrCatalogNumber("12345");
primaryData.setLabelerIdentificationCode("A999");
primaryData.setUnitOfMeasureID(1);
```

### HIBC LIC 보조 추가 데이터 생성
**개요**: 이 섹션에서는 인스턴스 생성 및 구성에 대해 다룹니다. `HIBCLICSecondaryAdditionalData`여기에는 유통기한 및 로트 번호와 같은 추가 세부 정보가 포함됩니다.

#### 1단계: 보조 데이터 개체 초기화
```java
HIBCLICSecondaryAdditionalData secondaryData = new HIBCLICSecondaryAdditionalData();
```

#### 2단계: 추가 속성 설정
- **만료일**: 데모를 위해 현재 날짜를 사용합니다.
- **수량, 로트 번호, 일련 번호**: 제품의 세부 사항을 정의합니다.
- **제조일자 및 링크 문자**: 제조 세부 사항을 확립합니다.

```java
secondaryData.setExpiryDate(new Date());
secondaryData.setExpiryDateFormat(HIBCLICDateFormat.MMDDYY);
secondaryData.setQuantity(30);
secondaryData.setLotNumber("LOT123");
secondaryData.setSerialNumber("SERIAL123");
secondaryData.setDateOfManufacture(new Date());
secondaryData.setLinkCharacter('S');
```

### HIBC LIC 1차 및 2차 데이터 결합
**개요**: 1차 데이터와 2차 데이터를 하나로 병합하는 방법을 알아보세요. `HIBCLICCombinedData` 간소화된 처리를 위한 객체입니다.

#### 1단계: 결합된 데이터 객체 초기화
```java
HIBCLICCombinedData combinedData = new HIBCLICCombinedData();
```

#### 2단계: 기본 및 보조 데이터 설정
- 두 데이터 세트를 연결하여 완전한 데이터 구조를 형성합니다.

```java
combinedData.setPrimaryData(primaryData);
combinedData.setSecondaryAdditionalData(secondaryData);
```

### HIBC LIC 결합 데이터가 포함된 QR 코드로 문서에 서명하세요
**개요**: 이 마지막 섹션에서는 HIBC 데이터를 결합한 QR 코드를 사용하여 문서에 서명하는 방법을 보여줍니다.

#### 1단계: 파일 경로 정의
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/Sample.pdf";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithQRCodeHIBCLICCombinedData/" + fileName;
```

#### 2단계: QR 코드 서명 옵션 설정
- **인코딩 유형**: 사용 `QrCodeTypes.HIBCLICQR` 인코딩 유형을 지정합니다.
- **데이터 할당**: QR 코드에 포함할 결합된 데이터를 전달합니다.

```java
Signature signature = new Signature(filePath);
try {
    QrCodeSignOptions options = new QrCodeSignOptions();
    options.setEncodeType(QrCodeTypes.HIBCLICQR);
    options.setData(combinedData);

    // 문서에 서명하고 저장하세요
    signature.sign(outputFilePath, options);
} finally {
    if (signature != null) signature.dispose();
}
```

## 실제 응용 프로그램
1. **제약품 규정 준수**이 통합을 사용하여 규제 표준 준수를 간소화합니다.
2. **공급망 관리**: 문서의 QR 코드를 통해 제약품의 추적성을 강화합니다.
3. **의료 시스템 통합**: 환자 안전을 강화하기 위해 의료 기록에 포괄적인 제품 데이터를 포함합니다.

## 성능 고려 사항
- **리소스 사용 최적화**: 효율적인 메모리 관리를 보장합니다. `Signature` 객체 사후 작업.
- **모범 사례**: 성능 개선 및 버그 수정을 위해 최신 GroupDocs.Signature 버전으로 정기적으로 업데이트하세요.

## 결론
이 가이드를 따라 HIBC LIC 기본 및 보조 데이터 객체를 생성하고, 이를 단일 엔터티로 결합하고, Java용 GroupDocs.Signature를 사용하여 QR 코드로 문서에 서명하는 방법을 알아보았습니다. 이러한 기술은 제약 산업의 문서 보안을 강화하고 규정 준수를 보장합니다.

### 다음 단계
- GroupDocs.Signature의 추가 기능을 살펴보세요.
- 기존 시스템에 이 솔루션을 통합하여 문서 서명 프로세스를 자동화하세요.

## FAQ 섹션
1. **HIBC 데이터란 무엇인가요?**
   - 건강산업 바코드(HIBC) 데이터에는 의료 및 제약 산업에서 사용되는 필수적인 제품 정보가 포함되어 있습니다.
2. **다른 유형의 바코드에도 GroupDocs.Signature를 사용할 수 있나요?**
   - 네, GroupDocs.Signature는 QR 코드 외에도 다양한 바코드 형식을 지원합니다.
3. **내 문서 형식이 PDF가 아닌 경우는 어떻게 되나요?**
   - GroupDocs.Signature는 Word, Excel 등 다양한 문서 형식을 지원합니다.
4. **서명하는 동안 예외를 어떻게 처리합니까?**
   - 예외를 효과적으로 관리하고 리소스 정리를 보장하려면 try-catch 블록을 구현합니다.
5. **문서당 QR 코드 수에 제한이 있나요?**
   - 본질적인 제한은 없습니다. 그러나 많은 코드를 추가할 때 성능에 미치는 영향을 고려하세요.

## 자원
- **선적 서류 비치**: [Java 문서용 GroupDocs.Signature](https://docs.groupdocs.com/signature/java/)
- **API 참조**: [GroupDocs API 참조](https://reference.groupdocs.com/signature/java/)
- **다운로드**: [최신 GroupDocs.Releases](https://releases.groupdocs.com/signature/java/)
- **구입**: [라이센스 구매](https://purchase.groupdocs.com/buy)
- **무료 체험**: [무료로 체험해보세요](https://releases.groupdocs.com/signature/java/)
- **임시 면허**: [여기에서 신청하세요](https://purchase.groupdocs.com/temporary-license/)