---
date: '2026-07-15'
description: GroupDocs.Signature를 사용하여 barcode PDF Java를 추가하는 방법을 배웁니다 – Java 문서에서
  barcode 서명을 서명, 검증, 검색, 업데이트 및 삭제하는 단계별 가이드.
keywords:
- add barcode pdf java
- groupdocs barcode signature
- java document signing
lastmod: '2026-07-15'
linktitle: Barcode 서명 Java 가이드
og_description: GroupDocs.Signature를 사용하여 barcode PDF Java를 추가하는 방법을 배웁니다 – Java 문서에서
  barcode 서명을 서명, 검증, 검색, 업데이트 및 삭제하는 단계별 가이드.
og_image_alt: Guide showing how to add barcode PDF Java using GroupDocs.Signature
og_title: Barcode PDF Java 추가 – GroupDocs로 서명 및 검증
schemas:
- author: GroupDocs
  dateModified: '2026-07-15'
  description: Learn how to add barcode PDF Java using GroupDocs.Signature – step‑by‑step
    guide to sign, verify, search, update and delete barcode signatures in Java documents.
  headline: Add Barcode PDF Java – Sign & Verify with GroupDocs
  type: TechArticle
- description: Learn how to add barcode PDF Java using GroupDocs.Signature – step‑by‑step
    guide to sign, verify, search, update and delete barcode signatures in Java documents.
  name: Add Barcode PDF Java – Sign & Verify with GroupDocs
  steps:
  - name: Case mismatch (e.g., “John Smith” vs. “john smith”).
    text: Case mismatch (e.g., “John Smith” vs. “john smith”).
  - name: Extra whitespace in the encoded text.
    text: Extra whitespace in the encoded text.
  - name: Wrong barcode type specified in the verification options.
    text: Wrong barcode type specified in the verification options.
  - name: Searching the wrong page number.
    text: Searching the wrong page number.
  - name: '**Reuse Signature Instances** – Create a single `Signature` object per
      document and reuse it for multiple operations.'
    text: '**Reuse Signature Instances** – Create a single `Signature` object per
      document and reuse it for multiple operations.'
  - name: '**Search Specific Pages Only** – Limit the page range to where barcodes
      are expected.'
    text: '**Search Specific Pages Only** – Limit the page range to where barcodes
      are expected.'
  - name: '**Choose the Simplest Barcode Type** – Simpler barcodes generate faster;
      only use QR or Data Matrix when you truly need the extra capacity.'
    text: '**Choose the Simplest Barcode Type** – Simpler barcodes generate faster;
      only use QR or Data Matrix when you truly need the extra capacity.'
  - name: '**Never Encode Sensitive Personal Data** – Barcodes are easily readable;
      avoid PII such as SSNs or passwords.'
    text: '**Never Encode Sensitive Personal Data** – Barcodes are easily readable;
      avoid PII such as SSNs or passwords.'
  - name: '**Validate Server‑Side** – Never trust client‑side verification alone;
      always re‑verify on a trusted backend.'
    text: '**Validate Server‑Side** – Never trust client‑side verification alone;
      always re‑verify on a trusted backend.'
  - name: '**Add Timestamps** – Include a timestamp in the barcode payload to prevent
      replay attacks.'
    text: '**Add Timestamps** – Include a timestamp in the barcode payload to prevent
      replay attacks.'
  type: HowTo
- questions:
  - answer: Yes – the library is fully compatible with JDK 8, 11, and 17.
    question: Can I use GroupDocs.Signature with Java 17?
  - answer: When you use Code128 or QR with sufficient size and contrast, the barcode
      remains scannable after printing and scanning.
    question: Does the barcode survive a print‑scan cycle?
  - answer: There is no hard limit; however, for optimal performance keep the total
      count below **200** per document.
    question: How many barcodes can a single document contain?
  - answer: A temporary license removes evaluation watermarks; a full license is mandatory
      for any production deployment.
    question: Is a license required for development builds?
  - answer: Yes – provide the password when creating the `Signature` object; the API
      will unlock the file internally.
    question: Can I sign password‑protected PDFs?
  type: FAQPage
tags:
- barcode signature
- groupdocs
- java
- pdf
- document signing
title: Barcode PDF Java 추가 – GroupDocs로 서명 및 검증
type: docs
url: /ko/java/digital-signatures/java-document-signature-groupdocs-signature-barcode/
weight: 1
---

# Java에서 바코드 PDF 추가 – GroupDocs로 서명 및 검증

내부 워크플로우에서 문서를 빠르고 시각적으로 태그해야 할 경우, Java에서 PDF에 바코드를 추가하는 것이 완벽한 솔루션입니다. **GroupDocs.Signature**를 사용하면 전체 PKI 기반 디지털 서명의 복잡성 없이 바코드 서명을 삽입, 검증, 검색, 업데이트 및 삭제할 수 있습니다. 이 튜토리얼은 환경 설정부터 프로덕션 수준의 모범 사례까지 모든 단계를 안내합니다.

## 빠른 답변
- **Java에서 PDF에 바코드를 추가하는 라이브러리는?** GroupDocs.Signature for Java.  
- **PDF, Word, 이미지에 서명할 수 있나요?** 예 – API는 30개 이상의 형식을 지원합니다.  
- **개발에 라이선스가 필요합니까?** 30일 임시 라이선스는 무료이며, 프로덕션에서는 정식 라이선스가 필요합니다.  
- **PDF 서명에 필요한 코드 라인은 몇 줄인가요?** 두 줄뿐입니다: `Signature` 객체를 생성하고 `sign`을 호출합니다.  
- **바코드 검증은 대소문자를 구분하나요?** 예 – 텍스트는 대소문자와 공백을 포함해 정확히 일치해야 합니다.

## add barcode pdf java란?
`add barcode pdf java`는 Java 코드를 사용해 바코드(예: Code128, QR, Data Matrix)를 PDF 파일에 삽입하는 과정을 의미합니다. 이 기술은 기계가 읽을 수 있는 태그를 제공하여 스캔하거나 프로그래밍 방식으로 검증할 수 있게 하며, 내부 시스템에서 빠른 문서 추적을 가능하게 합니다.

## 전체 디지털 서명 대신 바코드 서명을 사용하는 이유
바코드 서명은 PKI 기반 디지털 서명에 비해 **30‑50 % 빠르게** 생성 및 검증되며, 인쇄‑스캔 사이클 후에도 안정적으로 동작합니다. 또한 인증서 관리가 필요 없어 대량 내부 워크플로우에 적합합니다.

## 사전 요구 사항

- **Java Development Kit (JDK) 8+** – 성능 향상을 위해 Java 11 또는 17 권장.  
- **IDE** – IntelliJ IDEA 또는 Eclipse (예제는 IntelliJ 구문 사용).  
- **빌드 도구** – Maven 또는 Gradle을 통한 의존성 관리.  

### 프로젝트에 GroupDocs.Signature 추가하기

가장 쉬운 시작 방법은 빌드 도구를 통해 라이브러리를 추가하는 것입니다. 방법은 다음과 같습니다.

**Maven 사용자** – `pom.xml`에 아래를 추가하세요:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle 사용자** – `build.gradle`에 아래를 추가하세요:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**직접 JAR 다운로드** – 수동 설정을 선호한다면 [GroupDocs.Signature releases](https://releases.groupdocs.com/signature/java/)에서 JAR를 받아 클래스패스에 추가합니다.

### 라이선스 설정하기

GroupDocs.Signature는 프로덕션 사용에 무료가 아니지만 유연한 옵션을 제공합니다:

- **무료 체험** – [GroupDocs 다운로드 페이지](https://releases.groupdocs.com/signature/java/)에서 기능을 테스트할 수 있으며, 평가 워터마크가 추가됩니다.  
- **임시 라이선스** – [GroupDocs 임시 라이선스 페이지](https://purchase.groupdocs.com/temporary-license/)에서 30일 전체 접근 권한을 얻을 수 있어 PoC에 적합합니다.  
- **정식 라이선스** – 프로덕션 배포를 위해서는 [GroupDocs 구매 옵션](https://purchase.groupdocs.com/buy)을 확인하세요.  

**팁:** 개발 단계에서는 임시 라이선스를 사용하면 영구 키로 전환할 때 워터마크가 사라집니다.

### 빠른 환경 점검

의존성을 추가한 후 간단한 스모크 테스트를 실행하세요:

```java
import com.groupdocs.signature.Signature;

public class SignatureTest {
    public static void main(String[] args) {
        try {
            Signature signature = new Signature("test.pdf");
            System.out.println("GroupDocs.Signature initialized successfully!");
            signature.dispose();
        } catch (Exception e) {
            System.err.println("Setup issue: " + e.getMessage());
        }
    }
}
```

프로그램이 오류 없이 실행되면 환경이 준비된 것입니다. 문제가 발생하면 JDK 버전과 추가한 라이브러리 버전을 확인하세요.

## 바코드 서명을 사용해야 할 때

바코드 서명은 다음 상황에서 특히 유용합니다:

- **내부 문서 워크플로우** – 인보이스, 구매 주문서, 메모 등을 승인 체인에서 추적.  
- **대량 처리** – 수천 개 문서를 빠르게 서명; 바코드 생성은 전체 디지털 서명보다 **2배 빠름**.  
- **인쇄‑스캔 브리지** – 바코드는 인쇄‑스캔 사이클을 견디므로 하이브리드 종이‑디지털 프로세스에 적합.  
- **레거시 시스템 통합** – 기존 바코드 스캐너가 추가 소프트웨어 없이 태그를 읽을 수 있음.  
- **감사 추적** – 거래 ID 또는 타임스탬프를 삽입해 감사자가 즉시 검증 가능.  

법적 계약서, 고보안 문서, 외부 파트너와의 교환 등 PKI 기반 디지털 서명이 요구되는 경우에는 바코드 서명을 사용하지 마세요.

## Java용 GroupDocs.Signature 설정하기

### 핵심 클래스 정의

`Signature` 클래스는 GroupDocs.Signature에서 서명, 검증, 검색, 업데이트, 삭제 작업을 수행하는 진입점입니다.

```java
import com.groupdocs.signature.Signature;
```

### 기본 초기화

대상 파일을 가리키는 `Signature` 객체를 생성합니다:

```java
Signature signature = new Signature("path/to/your/document.pdf");
```

**중요 참고 사항**

- 경로는 절대 또는 상대 경로 모두 가능하며, `System.getProperty("user.home")`를 사용하면 플랫폼 간 호환성을 확보할 수 있습니다.  
- GroupDocs는 PDF, DOCX, XLSX, PPTX, PNG 등 **30개 이상의** 입력·출력 형식을 지원합니다.  
- `signature.dispose()` 혹은 try‑with‑resources 블록을 사용해 리소스를 반드시 해제하세요:

```java
try (Signature signature = new Signature("path/to/your/document.pdf")) {
    // Your signing operations here
} catch (Exception e) {
    System.err.println("Error working with document: " + e.getMessage());
}
```

이제 바코드 추가 준비가 완료되었습니다.

## Java에서 PDF에 바코드를 추가하는 방법은?

`new Signature("input.pdf")`로 원본 PDF를 로드하고, `BarcodeSignature` 객체를 설정한 뒤(`Code128`에 텍스트 “John Smith” 예시) `sign`을 호출하면 서명된 파일이 생성됩니다 – 총 세 줄의 간결한 코드로 구현됩니다. 이 방법은 기계가 읽을 수 있는 태그를 삽입하면서 원본 레이아웃을 유지하고, PDF뿐 아니라 모든 지원 형식에 적용됩니다.

### 단계별 구현

#### 1. 파일 경로 정의

원본 및 출력 파일 위치를 지정합니다:

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/signed_sample.docx";
```

#### 2. 서명 핸들러 생성

소스 문서로 핸들러를 초기화합니다:

```java
Signature signature = new Signature(filePath);
```

#### 3. 바코드 옵션 설정

`BarcodeSignature` 객체는 바코드의 시각적·데이터 속성을 정의합니다. 바코드 유형, 인코딩 텍스트, 위치, 크기, 색상, 선택적 인간 가독성 폰트를 설정하세요:

```java
BarcodeSignOptions signOptions = new BarcodeSignOptions("John Smith", BarcodeTypes.Code128);
signOptions.setVerticalAlignment(VerticalAlignment.Top);
signOptions.setHorizontalAlignment(HorizontalAlignment.Center);
signOptions.setWidth(100);
signOptions.setHeight(40);
signOptions.setMargin(new java.awt.Rectangle(20, 20, 0, 0));
signOptions.setForeColor(Color.RED);

SignatureFont signatureFont = new SignatureFont();
signatureFont.setSize(12);
signatureFont.setFamilyName("Comic Sans MS");
signOptions.setFont(signatureFont);
```

> **팁:** 인코딩 문자열이 20자를 초과하면 스캔 오류를 방지하기 위해 바코드 너비를 늘리세요.

#### 4. 서명 적용

서명 작업을 실행하고 출력 파일을 생성합니다:

```java
signature.sign(outputFilePath, signOptions);
```

#### 5. 실제 예시

인보이스 승인 시스템에서 승인자의 사원 ID와 타임스탬프를 삽입할 수 있습니다:

```java
String invoiceId = "INV-2025-0042";
String approver = "john.smith@company.com";
String timestamp = LocalDateTime.now().toString();

// Combine into barcode data
String barcodeData = invoiceId + "|" + approver + "|" + timestamp;

BarcodeSignOptions signOptions = new BarcodeSignOptions(barcodeData, BarcodeTypes.QR);
signOptions.setVerticalAlignment(VerticalAlignment.Bottom);
signOptions.setHorizontalAlignment(HorizontalAlignment.Right);

signature.sign(outputFilePath, signOptions);
```

이제 생성된 PDF는 필요한 승인 메타데이터를 담은 스캔 가능한 바코드를 포함합니다.

## Java 문서에서 바코드 서명을 검증하는 방법은?

`Signature.verify` 메서드는 제공된 옵션에 따라 문서 내 일치하는 바코드 서명을 검사하고, 기대한 바코드가 존재하는지 여부를 boolean으로 반환합니다. 검증은 자동화된 워크플로우에서 문서가 올바른 당사자에 의해 처리되었는지 확인할 때 유용합니다.

### 검증 단계

#### 1. 서명된 문서 로드

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");
```

#### 2. 검증 기준 설정

예상 텍스트, 바코드 형식, 페이지 번호 등을 정의합니다:

```java
BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
verifyOptions.setAllPages(false); // Only check the first page
verifyOptions.setPageNumber(1);
verifyOptions.setEncodeType(BarcodeTypes.Code128);
verifyOptions.setText("John Smith");
```

#### 3. 검증 실행

검사를 수행하고 결과를 처리합니다:

```java
boolean isValid = signature.verify(verifyOptions) != null;

if (isValid) {
    System.out.println("Document signature verified successfully!");
} else {
    System.out.println("Warning: Signature verification failed!");
}
```

**일반 패턴:** 특정 텍스트 없이 해당 유형의 바코드가 존재하는지만 확인하려면 `setText` 필터를 생략합니다:

```java
BarcodeVerifyOptions flexibleOptions = new BarcodeVerifyOptions();
flexibleOptions.setAllPages(true);
flexibleOptions.setEncodeType(BarcodeTypes.Code128);
// No setText() call = accept any text with this barcode type

boolean hasAnySignature = signature.verify(flexibleOptions) != null;
```

또는 내용에 상관없이 형식만 검증하려면:

```java
BarcodeVerifyOptions formatOnly = new BarcodeVerifyOptions();
formatOnly.setEncodeType(BarcodeTypes.QR);
// Confirms a QR code exists, regardless of content
```

> **경고:** 검증은 대소문자와 공백을 구분하므로 서명 전 데이터를 반드시 트림하고 정규화하세요.

## 문서 내 바코드 서명을 검색하는 방법은?

`Signature.search` 메서드는 제공된 `BarcodeSearchOptions`에 맞는 바코드 서명을 스캔하고, 각 바코드의 위치, 페이지 번호, 인코딩 값을 포함하는 컬렉션을 반환합니다. 이를 통해 파일을 일일이 열지 않고도 메타데이터를 대량 추출할 수 있습니다.

### 검색 워크플로우

#### 1. 검색 초기화

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");
```

#### 2. 검색 매개변수 설정

페이지 범위, 바코드 유형, 텍스트 필터 등을 지정합니다:

```java
BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true); // Search the entire document
```

성능 향상을 위해 검색 범위를 좁히는 것도 가능합니다:

```java
BarcodeSearchOptions narrowSearch = new BarcodeSearchOptions();
narrowSearch.setAllPages(false);
narrowSearch.setPageNumber(1); // Only search page 1
narrowSearch.setEncodeType(BarcodeTypes.Code128); // Only find Code128 barcodes
```

#### 3. 검색 실행

```java
java.util.List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);

System.out.println("Found " + signatures.size() + " barcode signature(s)");

for (BarcodeSignature bcSignature : signatures) {
    System.out.println("Barcode Type: " + bcSignature.getEncodeType().getTypeName());
    System.out.println("Text: " + bcSignature.getText());
    System.out.println("Position: (" + bcSignature.getLeft() + ", " + bcSignature.getTop() + ")");
    System.out.println("Size: " + bcSignature.getWidth() + "x" + bcSignature.getHeight());
    System.out.println("---");
}
```

#### 4. 데이터 추출 예시

인보이스 배치에서 모든 바코드의 승인 데이터를 추출합니다:

```java
List<BarcodeSignature> foundSignatures = signature.search(BarcodeSignature.class, searchOptions);

for (BarcodeSignature sig : foundSignatures) {
    String barcodeData = sig.getText();
    
    // Parse your custom format (remember our invoice example?)
    String[] parts = barcodeData.split("\\|");
    if (parts.length == 3) {
        String invoiceId = parts[0];
        String approver = parts[1];
        String timestamp = parts[2];
        
        System.out.println("Invoice " + invoiceId + " approved by " + approver + " at " + timestamp);
    }
}
```

> **성능 팁:** 100페이지 이상 문서는 바코드가 실제로 존재하는 페이지만 제한하면 실행 시간이 **70 %**까지 단축됩니다.

## 기존 바코드 서명을 업데이트하는 방법은?

`Signature.update` 메서드는 기존 바코드 서명의 시각적 속성(위치, 크기, 색상 등)을 변경하면서 인코딩 데이터는 그대로 유지합니다. 문서 레이아웃이 변경될 때 유용합니다.

### 업데이트 절차

#### 1. 업데이트 대상 서명 찾기

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");

BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true);

List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
```

#### 2. 원하는 속성 수정

```java
List<BarcodeSignature> signaturesToUpdate = new ArrayList<>();

if (!signatures.isEmpty()) {
    BarcodeSignature bcSignature = signatures.get(0); // Update the first found signature
    
    // Move it 100px right and 100px down
    bcSignature.setLeft(bcSignature.getLeft() + 100);
    bcSignature.setTop(bcSignature.getTop() + 100);
    
    // Make it bigger
    bcSignature.setWidth(200);
    bcSignature.setHeight(50);
    
    signaturesToUpdate.add(bcSignature);
}
```

여러 속성을 한 번에 변경할 수 있습니다:

```java
bcSignature.setLeft(50);
bcSignature.setTop(50);
bcSignature.setWidth(150);
bcSignature.setHeight(45);
// Note: You can't change the encoded text or barcode type with update
// For that, you'd need to delete and re-sign
```

#### 3. 변경 사항 저장

```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature.update(outputStream, signaturesToUpdate);

// If you want to save to a file instead:
// signature.update("path/to/updated_document.docx", signaturesToUpdate);
```

#### 4. 실제 시나리오

새로 추가된 회사 로고와 겹치지 않도록 모든 서명을 재배치합니다:

```java
List<BarcodeSignature> allSignatures = signature.search(BarcodeSignature.class, searchOptions);
List<BarcodeSignature> toUpdate = new ArrayList<>();

for (BarcodeSignature sig : allSignatures) {
    // Move all signatures down by 50px to clear space for new logo
    if (sig.getTop() < 100) {
        sig.setTop(sig.getTop() + 50);
        toUpdate.add(sig);
    }
}

if (!toUpdate.isEmpty()) {
    signature.update(outputStream, toUpdate);
    System.out.println("Repositioned " + toUpdate.size() + " signature(s)");
}
```

> **제한 사항:** 인코딩 텍스트를 변경하려면 기존 서명을 삭제하고 새 서명을 삽입해야 합니다.

## 문서에서 바코드 서명을 삭제하는 방법은?

`Signature.delete` 메서드는 선택한 바코드 서명을 영구적으로 제거하여 시각 요소와 인코딩 데이터를 모두 삭제합니다. 테스트 서명을 정리하거나 더 이상 필요 없는 바코드를 제거할 때 사용합니다.

### 삭제 단계

#### 1. 서명 위치 찾기

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");

BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true);

List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
```

#### 2. 선택된 서명 삭제

```java
List<BarcodeSignature> signaturesToDelete = new ArrayList<>();

// Delete all Code128 signatures (for example)
for (BarcodeSignature sig : signatures) {
    if (sig.getEncodeType().equals(BarcodeTypes.Code128)) {
        signaturesToDelete.add(sig);
    }
}

if (!signaturesToDelete.isEmpty()) {
    boolean result = signature.delete(signaturesToDelete);
    
    if (result) {
        System.out.println("Successfully deleted " + signaturesToDelete.size() + " signature(s)");
    } else {
        System.err.println("Failed to delete signatures");
    }
}
```

#### 3. 조건부 삭제 예시

인코딩 텍스트에 타임스탬프가 포함된 경우, 특정 시점 이전의 바코드만 삭제합니다:

```java
LocalDateTime cutoffDate = LocalDateTime.now().minusDays(30);
List<BarcodeSignature> outdatedSignatures = new ArrayList<>();

for (BarcodeSignature sig : signatures) {
    try {
        String text = sig.getText();
        // Assuming format like "data|timestamp"
        String[] parts = text.split("\\|");
        if (parts.length > 1) {
            LocalDateTime sigDate = LocalDateTime.parse(parts[1]);
            if (sigDate.isBefore(cutoffDate)) {
                outdatedSignatures.add(sig);
            }
        }
    } catch (Exception e) {
        // Skip signatures that don't match our format
        continue;
    }
}

if (!outdatedSignatures.isEmpty()) {
    signature.delete(outdatedSignatures);
    System.out.println("Removed " + outdatedSignatures.size() + " outdated signature(s)");
}
```

> **주의:** 삭제는 되돌릴 수 없으므로 테스트 단계에서는 반드시 복사본에서 작업하세요.

#### 4. 배치 삭제 패턴

릴리스 전 테스트 서명을 정리합니다:

```java
// Remove all signatures containing "TEST" in their text
List<BarcodeSignature> testSignatures = signatures.stream()
    .filter(sig -> sig.getText().toUpperCase().contains("TEST"))
    .collect(Collectors.toList());

if (!testSignatures.isEmpty()) {
    signature.delete(testSignatures);
    System.out.println("Cleaned up " + testSignatures.size() + " test signature(s)");
}
```

## 바코드 유형: 실용 가이드

올바른 바코드 선택은 스캔 신뢰성, 데이터 용량, 프린터 호환성에 영향을 미칩니다.

### Code128 (가장 일반적인 선택)

- **사용 시점:** 영숫자 데이터, 고밀도, 인쇄 문서.  
- **장점:** 컴팩트, 표준 스캐너와 호환, 작은 크기에서도 선명하게 인쇄.  
- **단점:** ASCII만 지원, 2‑D 코드보다 오류 복원력이 낮음.  

예시:

```java
BarcodeSignOptions code128 = new BarcodeSignOptions("INV-2025-042", BarcodeTypes.Code128);
```

### QR Code (모바일에 최적)

- **사용 시점:** 모바일 스캔, 대용량 데이터(URL, JSON 등), 손상 가능성이 있는 문서.  
- **장점:** 최대 4 000자, 내장 오류 정정, 스마트폰 친화적.  
- **단점:** 시각적 차지 면적이 크고, 작은 크기에서는 고해상도 필요.  

예시:

```java
String jsonData = "{\"invoice\":\"INV-042\",\"amount\":1500.00,\"approver\":\"john@company.com\"}";
BarcodeSignOptions qrCode = new BarcodeSignOptions(jsonData, BarcodeTypes.QR);
```

### Code39 (오래된 신뢰)

- **사용 시점:** 레거시 스캐너 환경, 인간이 읽을 수 있는 텍스트 필요.  
- **장점:** 폭넓은 레거시 지원, 포맷 단순, 체크섬 불필요.  
- **단점:** 데이터 밀도가 낮고, 문자 집합 제한, 차지 공간이 큼.  

### Data Matrix (초소형 파워하우스)

- **사용 시점:** 극히 제한된 공간, 작은 부품 표기, 고밀도 데이터.  
- **장점:** 매우 컴팩트, 강력한 오류 정정, 곡면에도 적용 가능.  
- **단점:** 고품질 인쇄 필요, 스캐너 지원이 제한적.  

#### 빠른 비교

| Barcode Type | Data Capacity | Best For | Typical Size |
|--------------|---------------|----------|--------------|
| Code128      | ~100 chars    | General‑purpose tagging | Small |
| QR Code      | ~4 000 chars  | Mobile scanning, rich data | Medium |
| Code39       | ~43 chars     | Legacy hardware | Large |
| Data Matrix  | ~3 000 chars  | Tiny spaces, industrial tags | Very small |

**추천:** 간단한 ID는 **Code128**부터 시작하고, URL이나 대용량 페이로드가 필요하면 **QR**로 전환하세요. 레거시 통합이 필요한 경우에만 **Code39**를 사용합니다.

## 흔한 문제 및 해결책

### 문제: “검증 중 바코드가 발견되지 않음”

**증상:** 바코드가 눈에 보이지만 검증이 `false`를 반환합니다.

**주요 원인**
1. 대소문자 불일치(예: “John Smith” vs. “john smith”).  
2. 인코딩 텍스트에 여분 공백 존재.  
3. 검증 옵션에 잘못된 바코드 유형 지정.  
4. 잘못된 페이지 번호 검색.  

**해결:** 서명 및 검증 전에 텍스트를 정규화하고, `setEncodeType`이 원본 유형과 일치하는지 확인하세요.

```java
// Always normalize your data
String signatureText = originalText.trim().toLowerCase();

// When signing:
BarcodeSignOptions signOptions = new BarcodeSignOptions(signatureText, BarcodeTypes.Code128);

// When verifying:
BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
verifyOptions.setText(signatureText); // Use the same normalized text
verifyOptions.setEncodeType(BarcodeTypes.Code128);
```

### 문제: “바코드가 흐리게 보이거나 읽히지 않음”

**증상:** 인쇄된 바코드가 스캔되지 않음.

**원인**
- 인코딩 데이터에 비해 바코드 크기가 너무 작음.  
- 프린터 해상도 낮음.  
- 바코드 색상과 배경 간 대비 부족.  

**해결:** 바코드 너비/높이를 늘리고, 검은색/흰색 고대비 색상을 사용하며, 프린터 DPI를 최소 300 dpi로 설정하세요.

```java
// Increase size for longer strings
int dataLength = barcodeText.length();
int minWidth = Math.max(100, dataLength * 10); // 10px per character minimum

BarcodeSignOptions signOptions = new BarcodeSignOptions(barcodeText, BarcodeTypes.Code128);
signOptions.setWidth(minWidth);
signOptions.setHeight(60); // Taller = easier to scan

// Use high-contrast colors
signOptions.setForeColor(Color.BLACK); // Black on white is most reliable
signOptions.setBackColor(Color.WHITE);
```

### 문제: “대용량 문서에서 OutOfMemoryError 발생”

**증상:** 수백 페이지 PDF 처리 시 애플리케이션이 크래시됩니다.

**원인:** 라이브러리가 전체 문서를 메모리에 로드함.

**해결:** 스트리밍 모드를 활성화하고 페이지를 순차적으로 처리하세요.

```java
// Process pages in batches instead of all at once
BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(false);

List<BarcodeSignature> allSignatures = new ArrayList<>();

for (int page = 1; page <= totalPages; page++) {
    searchOptions.setPageNumber(page);
    List<BarcodeSignature> pageSignatures = signature.search(BarcodeSignature.class, searchOptions);
    allSignatures.addAll(pageSignatures);
    
    // Process and clear as you go
    if (page % 10 == 0) {
        System.gc(); // Suggest garbage collection every 10 pages
    }
}
```

### 문제: “문서 유형에 따라 서명 위치가 일관되지 않음”

**증상:** PDF와 Word 문서에서 바코드가 다른 위치에 표시됨.

**원인:** PDF는 좌하단 원점을, Word는 좌상단 원점을 사용함.

**해결:** 문서 유형을 감지하고 좌표 변환을 적용하세요.

```java
// Use relative positioning instead of absolute
signOptions.setVerticalAlignment(VerticalAlignment.Bottom);
signOptions.setHorizontalAlignment(HorizontalAlignment.Right);

// Then use margins for fine-tuning
Padding margin = new Padding();
margin.setRight(50); // 50px from right edge
margin.setBottom(50); // 50px from bottom
signOptions.setMargin(margin);

// This works consistently across PDF, DOCX, XLSX, etc.
```

### 문제: “업데이트 후 서명 서식이 손실됨”

**증상:** `update` 호출 후 바코드 색상이나 폰트가 예기치 않게 변경됨.

**원인:** 모든 시각 속성이 업데이트 시 유지되지 않음.

**해결:** 업데이트 후 필요한 시각 설정을 다시 적용하세요.

```java
// When updating, explicitly set all visual properties
bcSignature.setLeft(newLeft);
bcSignature.setTop(newTop);
bcSignature.setWidth(originalWidth); // Don't forget these!
bcSignature.setHeight(originalHeight);
// Note: Color and font can't be updated - you'd need to delete and re-sign
```

## 프로덕션을 위한 모범 사례

### 성능 최적화

1. **Signature 인스턴스 재사용** – 문서당 하나의 `Signature` 객체를 생성하고 여러 작업에 재사용합니다.

```java
// Bad - Creates new instance each time
public void processDocument(String path) {
    Signature sig1 = new Signature(path);
    sig1.search(/* ... */);
    
    Signature sig2 = new Signature(path); // Unnecessary reload
    sig2.verify(/* ... */);
}

// Good - Reuse the same instance
public void processDocument(String path) {
    try (Signature signature = new Signature(path)) {
        signature.search(/* ... */);
        signature.verify(/* ... */);
        signature.update(/* ... */);
    }
}
```

2. **특정 페이지만 검색** – 바코드가 존재할 것으로 예상되는 페이지 범위만 제한합니다.

```java
// Slow for 100+ page documents
BarcodeSearchOptions slowSearch = new BarcodeSearchOptions();
slowSearch.setAllPages(true);

// Fast - only check where signatures actually are
BarcodeSearchOptions fastSearch = new BarcodeSearchOptions();
fastSearch.setAllPages(false);
fastSearch.setPageNumber(1); // Only check cover page
```

3. **가장 간단한 바코드 유형 선택** – 단순 바코드가 더 빠르게 생성되므로 QR이나 Data Matrix는 필요할 때만 사용합니다.

```java
// Overkill for simple IDs
BarcodeSignOptions slow = new BarcodeSignOptions("12345", BarcodeTypes.QR);

// Faster and more appropriate
BarcodeSignOptions fast = new BarcodeSignOptions("12345", BarcodeTypes.Code128);
```

### 보안 고려 사항

1. **민감 개인 데이터 절대 인코딩 금지** – 바코드는 쉽게 읽히므로 SSN, 비밀번호 등 PII를 포함하지 마세요.

```java
// Bad - exposes sensitive data
String barcodeData = "SSN:123-45-6789|Password:hunter2";

// Good - use reference IDs
String barcodeData = "USER-REF-7721X"; // Look up sensitive data server-side
```

2. **서버‑사이드 검증** – 클라이언트 검증만 신뢰하지 말고, 반드시 신뢰할 수 있는 백엔드에서 재검증하세요.

```java
// Client scans barcode and extracts "APPROVED-BY-ADMIN"
// Always verify server-side:
public boolean verifyApproval(String documentId, String scannedData) {
    // Load document from secure storage
    Signature signature = new Signature(getSecureDocument(documentId));
    
    BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
    verifyOptions.setText(scannedData);
    
    boolean isValid = signature.verify(verifyOptions) != null;
    
    // Also check against your database
    boolean isInDatabase = checkApprovalDatabase(documentId, scannedData);
    
    return isValid && isInDatabase;
}
```

3. **타임스탬프 추가** – 바코드 페이로드에 타임스탬프를 포함해 재사용 공격을 방지합니다.

```java
import java.time.LocalDateTime;
import java.time.temporal.ChronoUnit;

String timestamp = LocalDateTime.now().truncatedTo(ChronoUnit.SECONDS).toString();
String barcodeData = "APPROVAL|" + userId + "|" + timestamp;

// When verifying, check the timestamp isn't too old
public boolean isSignatureRecent(String barcodeData, int maxAgeHours) {
    String[] parts = barcodeData.split("\\|");
    if (parts.length < 3) return false;
    
    LocalDateTime signatureTime = LocalDateTime.parse(parts[2]);
    LocalDateTime now = LocalDateTime.now();
    
    long hoursSince = ChronoUnit.HOURS.between(signatureTime, now);
    return hoursSince <= maxAgeHours;
}
```

### 오류 처리 패턴

- **Try‑With‑Resources 사용** – `Signature` 객체가 자동으로 해제되도록 합니다.

```java
try (Signature signature = new Signature(documentPath)) {
    // Your operations here
    signature.sign(outputPath, signOptions);
} catch (Exception e) {
    logger.error("Failed to sign document: " + documentPath, e);
    throw new DocumentSigningException("Could not process document", e);
}
```

- **파일 접근 검증** – 서명 시도 전에 파일 접근 권한을 확인합니다.

```java
public void signDocument(String inputPath, String outputPath) {
    File inputFile = new File(inputPath);
    
    if (!inputFile.exists()) {
        throw new IllegalArgumentException("Input file not found: " + inputPath);
    }
    
    if (!inputFile.canRead()) {
        throw new SecurityException("Cannot read input file: " + inputPath);
    }
    
    File outputDir = new File(outputPath).getParentFile();
    if (outputDir != null && !outputDir.exists()) {
        outputDir.mkdirs();
    }
    
    try (Signature signature = new Signature(inputPath)) {
        signature.sign(outputPath, signOptions);
    }
}
```

- **동시 접근 동기화** – 여러 스레드가 동일 파일을 작업할 경우 동기화합니다.

```java
import java.util.concurrent.locks.ReentrantLock;
import java.util.concurrent.ConcurrentHashMap;

public class SignatureManager {
    private final ConcurrentHashMap<String, ReentrantLock> documentLocks = new ConcurrentHashMap<>();
    
    public void signDocument(String documentPath, BarcodeSignOptions options) {
        ReentrantLock lock = documentLocks.computeIfAbsent(documentPath, k -> new ReentrantLock());
        
        lock.lock();
        try (Signature signature = new Signature(documentPath)) {
            signature.sign(documentPath + ".signed", options);
        } finally {
            lock.unlock();
        }
    }
}
```

### 구현 테스트

**단위 테스트 템플릿**

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.io.TempDir;
import static org.junit.jupiter.api.Assertions.*;

public class BarcodeSignatureTest {
    
    @TempDir
    Path tempDir;
    
    @Test
    public void testSignAndVerify() throws Exception {
        // Setup
        String testDoc = "test-document.pdf";
        String outputDoc = tempDir.resolve("signed-test.pdf").toString();
        String testData = "TEST-USER-12345";
        
        // Sign
        try (Signature signature = new Signature(testDoc)) {
            BarcodeSignOptions signOptions = new BarcodeSignOptions(testData, BarcodeTypes.Code128);
            signature.sign(outputDoc, signOptions);
        }
        
        // Verify
        try (Signature signature = new Signature(outputDoc)) {
            BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
            verifyOptions.setText(testData);
            verifyOptions.setEncodeType(BarcodeTypes.Code128);
            
            boolean isValid = signature.verify(verifyOptions) != null;
            assertTrue(isValid, "Signature should be valid");
        }
    }
    
    @Test
    public void testSearchFindsSignature() throws Exception {
        String signedDoc = "signed-document.pdf";
        
        try (Signature signature = new Signature(signedDoc)) {
            BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
            searchOptions.setAllPages(true);
            
            List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
            
            assertFalse(signatures.isEmpty(), "Should find at least one signature");
            assertEquals("TEST-USER-12345", signatures.get(0).getText());
        }
    }
}
```

**통합 체크리스트**

- ✅ 모든 지원 형식(PDF, DOCX, XLSX, PPTX, PNG) 테스트.  
- ✅ 인쇄‑스캔 사이클 후 바코드 가독성 확인.  
- ✅ 최대 길이 데이터 문자열에 대한 스트레스 테스트.  
- ✅ A4, Letter, 맞춤 페이지 크기에서 위치 확인.  
- ✅ 다중 문서 동시 서명 테스트.  
- ✅ 500페이지 이상 문서에 대한 메모리 사용량 모니터링.  
- ✅ 바코드 스캐너가 출력물을 안정적으로 읽는지 확인.  

### 로깅 및 모니터링

각 작업 주변에 의미 있는 로그를 추가하세요:

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class DocumentSigningService {
    private static final Logger logger = LoggerFactory.getLogger(DocumentSigningService.class);
    
    public void signDocument(String docPath, String barcodeData) {
        logger.info("Starting signature process for document: {}", docPath);
        logger.debug("Barcode data length: {} characters", barcodeData.length());
        
        try (Signature signature = new Signature(docPath)) {
            BarcodeSignOptions options = new BarcodeSignOptions(barcodeData, BarcodeTypes.Code128);
            
            long startTime = System.currentTimeMillis();
            signature.sign(docPath + ".signed", options);
            long duration = System.currentTimeMillis() - startTime;
            
            logger.info("Successfully signed document in {}ms", duration);
        } catch (Exception e) {
            logger.error("Failed to sign document: {}", docPath, e);
            throw new RuntimeException("Signature operation failed", e);
        }
    }
}
```

처리 시간, 메모리 사용량, 오류 비율 등 주요 메트릭을 추적합니다:

```java
// Track success/failure rates
metricsService.incrementCounter("signature.sign.success");
metricsService.incrementCounter("signature.verify.failure");

// Track performance
metricsService.recordTimer("signature.sign.duration", duration);

// Track document sizes
metricsService.recordHistogram("signature.document.pages", pageCount);
```

## 실제 사용 사례에서 얻은 팁

**배치 처리 전략**

수백 개 파일을 다룰 때는 배치로 처리하고 진행 상황을 보고합니다:

```java
public void signBatch(List<String> documents, String barcodePrefix) {
    int total = documents.size();
    int completed = 0;
    int failed = 0;
    
    for (String docPath : documents) {
        try {
            String barcodeData = barcodePrefix + "-" + UUID.randomUUID().toString();
            signDocument(docPath, barcodeData);
            completed++;
            
            if (completed % 10 == 0) {
                logger.info("Progress: {}/{} documents signed", completed, total);
            }
        } catch (Exception e) {
            failed++;
            logger.warn("Failed to sign: {}", docPath, e);
        }
    }
    
    logger.info("Batch complete: {} succeeded, {} failed", completed, failed);
}
```

**구성 외부화**

바코드 설정(유형, 크기, 색상)을 프로퍼티 파일에 저장해 재컴파일 없이 튜닝합니다:

```java
public class BarcodeConfig {
    private int defaultWidth = 100;
    private int defaultHeight = 40;
    private String defaultBarcodeType = "Code128";
    private String defaultColor = "BLACK";
    
    // Load from properties file or environment variables
    public BarcodeConfig() {
        this.defaultWidth = Integer.parseInt(
            System.getProperty("barcode.width", "100")
        );
        // ... load other properties
    }
    
    public BarcodeSignOptions createDefaultOptions(String text) {
        BarcodeSignOptions options = new BarcodeSignOptions(text, getBarcodeType());
        options.setWidth(defaultWidth);
        options.setHeight(defaultHeight);
        options.setForeColor(getColor());
        return options;
    }
}
```

**바코드 페이로드 표준화**

`EMPID|TIMESTAMP|DOCID`와 같은 구분자를 사용하면 파싱이 간단하고 일관됩니다:

```java
public class BarcodeDataBuilder {
    private String userId;
    private String action;
    private LocalDateTime timestamp;
    private String documentId;
    
    public BarcodeDataBuilder setUserId(String userId) {
        this.userId = userId;
        return this;
    }
    
    public BarcodeDataBuilder setAction(String action) {
        this.action = action;
        return this;
    }
    
    public BarcodeDataBuilder setDocumentId(String documentId) {
        this.documentId = documentId;
        return this;
    }
    
    public String build() {
        this.timestamp = LocalDateTime.now();
        
        // Format: VERSION|USER|ACTION|DOC_ID|TIMESTAMP|CHECKSUM
        String data = String.join("|",
            "v1",
            userId,
            action,
            documentId,
            timestamp.toString()
        );
        
        // Add simple checksum
        int checksum = data.hashCode();
        return data + "|" + checksum;
    }
    
    public static ParsedBarcodeData parse(String barcodeData) {
        String[] parts = barcodeData.split("\\|");
        if (parts.length != 6 || !parts[0].equals("v1")) {
            throw new IllegalArgumentException("Invalid barcode format");
        }
        
        return new ParsedBarcodeData(parts[1], parts[2], parts[3], 
                                     LocalDateTime.parse(parts[4]));
    }
}

// Usage:
String barcodeData = new BarcodeDataBuilder()
    .setUserId("john.smith")
    .setAction("APPROVED")
    .setDocumentId("INV-2025-042")
    .build();
```

**문서 유형 자동 감지**

대상 파일이 PDF, Word, 이미지인지에 따라 바코드 크기를 자동 조정합니다:

```java
public BarcodeSignOptions getOptimalOptions(String documentPath, String text) {
    String extension = documentPath.substring(documentPath.lastIndexOf(".") + 1).toLowerCase();
    
    BarcodeSignOptions options = new BarcodeSignOptions(text, BarcodeTypes.Code128);
    
    switch (extension) {
        case "pdf":
            // PDFs can handle larger, detailed barcodes
            options.setWidth(150);
            options.setHeight(50);
            break;
        case "docx":
        case "doc":
            // Word docs need compact signatures that don't disrupt flow
            options.setWidth(100);
            options.setHeight(35);
            options.setVerticalAlignment(VerticalAlignment.Bottom);
            break;
        case "xlsx":
        case "xls":
            // Excel needs signatures that don't obscure data
            options.setWidth(80);
            options.setHeight(30);
            options.setHorizontalAlignment(HorizontalAlignment.Right);
            break;
        default:
            // Safe defaults
            options.setWidth(100);
            options.setHeight(40);
    }
    
    return options;
}
```

## 추가 자료

- [GroupDocs.Signature documentation](https://docs.groupdocs.com/signature/java/) – 전체 API 가이드 및 사용 예시.  
- [GroupDocs support forum](https://forum.groupdocs.com/c/signature/13) – 커뮤니티 도움 및 문제 해결.  
- [API reference](https://apireference.groupdocs.com/signature/java) – 상세 메서드 시그니처 및 파라미터 설명.

## 자주 묻는 질문

**Q: Java 17에서도 GroupDocs.Signature를 사용할 수 있나요?**  
A: 예 – 라이브러리는 JDK 8, 11, 17과 완전히 호환됩니다.

**Q: 바코드가 인쇄‑스캔 사이클을 견디나요?**  
A: Code128이나 충분히 큰 QR 코드를 적절한 크기와 대비로 사용하면 인쇄·스캔 후에도 스캔 가능합니다.

**Q: 하나의 문서에 삽입할 수 있는 바코드 수에 제한이 있나요?**  
A: 명확한 제한은 없지만 최적 성능을 위해 **200개** 이하를 권장합니다.

**Q: 개발 빌드에도 라이선스가 필요합니까?**  
A: 임시 라이선스로 평가 워터마크를 제거할 수 있으며, 프로덕션 배포 시에는 정식 라이선스가 필수입니다.

**Q: 비밀번호로 보호된 PDF에 서명할 수 있나요?**  
A: 예 – `Signature` 객체 생성 시 비밀번호를 제공하면 API가 내부적으로 파일을 해제합니다.

---

**마지막 업데이트:** 2026-07-15  
**테스트 환경:** GroupDocs.Signature 23.9 for Java  
**작성자:** GroupDocs  

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

## 관련 튜토리얼

- [How to Verify Barcode Signatures in Java with GroupDocs.Signature](/signature/java/search-verification/groupdocs-signature-java-document-verification/)
- [How to Search Digital Signatures in Java Documents with GroupDocs](/signature/java/search-verification/groupdocs-signature-java-digital-search-tutorial/)
- [Java Barcode Signature Tutorial - Add, Verify & Manage Barcodes in PDFs](/signature/java/barcode-signatures/)