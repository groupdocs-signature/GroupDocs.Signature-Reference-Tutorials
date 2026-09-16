---
categories:
- Document Signing
- Healthcare Integration
date: '2026-09-15'
description: GroupDocs.Signature for Java를 사용하여 바코드로 PDF에 서명하는 방법을 배웁니다. 의료 문서에 Data
  Matrix와 QR 코드를 추가하는 단계별 가이드.
keywords:
- sign pdf with barcode
- add qr code pdf
- hibc barcode java
- pdf signing java
- healthcare barcode signing
lastmod: '2026-09-15'
linktitle: HIBC PDF 서명 Java 가이드
og_description: GroupDocs.Signature for Java를 사용하여 바코드로 PDF에 서명합니다. 몇 단계만으로 의료 문서에
  Data Matrix와 QR 코드를 삽입하는 방법을 배웁니다.
og_image_alt: 'Developer tutorial: sign PDF with HIBC barcode using GroupDocs.Signature
  for Java'
og_title: Java에서 HIBC를 사용하여 바코드로 PDF 서명 – GroupDocs 가이드
schemas:
- author: GroupDocs
  dateModified: '2026-09-15'
  description: Learn how to sign PDF with barcode using GroupDocs.Signature for Java.
    Step‑by‑step guide for adding Data Matrix and QR codes in healthcare documents.
  headline: Sign PDF with barcode using HIBC in Java
  type: TechArticle
- description: Learn how to sign PDF with barcode using GroupDocs.Signature for Java.
    Step‑by‑step guide for adding Data Matrix and QR codes in healthcare documents.
  name: Sign PDF with barcode using HIBC in Java
  steps:
  - name: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
    text: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
  - name: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
    text: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
  - name: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
    text: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
  - name: '**Apply the signature** to the PDF.'
    text: '**Apply the signature** to the PDF.'
  - name: '**Dispose of resources** to free file handles and avoid memory leaks.'
    text: '**Dispose of resources** to free file handles and avoid memory leaks.'
  - name: '**Import QR‑specific classes**'
    text: '**Import QR‑specific classes**'
  - name: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
    text: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
  - name: '**Sign the document**'
    text: '**Sign the document**'
  type: HowTo
- questions:
  - answer: Yes, it also supports DOCX, XLSX, PPTX, PNG, JPEG, and TIFF with the same
      barcode‑signing API.
    question: Can GroupDocs.Signature sign file types other than PDF?
  - answer: Verify that your HIBC string follows the exact HIBCC syntax, use the online
      validator, and ensure you’re using the correct `QrCodeTypes` constant for the
      chosen format.
    question: How do I troubleshoot “Invalid barcode content” errors?
  - answer: QR ≈ 4,296 alphanumeric characters, Aztec ≈ 3,832 numeric / 3,067 alphanumeric,
      Data Matrix ≈ 3,116 numeric / 2,335 alphanumeric. Keep codes under 200 characters
      for optimal scan reliability.
    question: What is the maximum data capacity for each HIBC format?
  - answer: Absolutely. Create separate `QrCodeSignOptions` objects with different
      positions and call `signature.sign()` for each. Just ensure they don’t overlap.
    question: Is it possible to embed multiple barcode types in one PDF?
  - answer: No. After the JAR is on the classpath and the license is activated, all
      operations are performed locally.
    question: Do I need an internet connection for signing at runtime?
  type: FAQPage
tags:
- sign pdf
- barcode
- java
- healthcare
- groupdocs
title: Java에서 HIBC를 사용하여 바코드로 PDF 서명하는 방법
type: docs
url: /ko/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/
weight: 1
---

# HIBC를 사용한 바코드로 PDF 서명 (Java)

If you’re building pharmaceutical or healthcare logistics software, you’ve probably hit the wall of paper‑based tracking, lost signatures, and audit nightmares. **Signing a PDF with barcode**—especially a HIBC Data Matrix or QR code—creates a tamper‑evident, machine‑readable trail that survives printing, scanning, and regulatory review. In this tutorial you’ll see exactly how to add both Data Matrix and QR barcodes to a PDF using GroupDocs.Signature for Java.

## 빠른 답변
- **Java에서 HIBC 바코드를 처리하는 라이브러리는?** GroupDocs.Signature for Java.  
- **가장 작은 크기의 바코드 포맷은?** Data Matrix – 작은 라벨에 이상적.  
- **같은 PDF에 QR과 Data Matrix를 모두 추가할 수 있나요?** 예, 별도의 `QrCodeSignOptions`를 생성하면 됩니다.  
- **런타임에 인터넷 연결이 필요합니까?** 아니요, 설치 후 라이브러리는 완전히 오프라인으로 작동합니다.  
- **추천 Java 버전은?** 프로덕션 수준 성능을 위해 Java 11+.

## HIBC 바코드 PDF 서명이란?
`Signature` is GroupDocs.Signature's core class that represents a PDF document and enables embedding of digital signatures. The `Signature` class in GroupDocs.Signature for Java provides methods to embed HIBC barcodes as digital signatures. By signing a PDF with an HIBC barcode you create a verifiable, tamper‑evident record that can be scanned at any point in the supply chain.

## Data Matrix와 QR 코드를 함께 사용하는 이유는?
Data Matrix offers the smallest footprint while still holding up to 2,335 alphanumeric characters, making it perfect for dense label areas. QR codes, on the other hand, support up to 4,296 characters and are universally readable by smartphones. Combining both gives you the best balance of space efficiency and data capacity, ensuring every stakeholder—from warehouse scanners to mobile apps—can read the information they need.

## 사전 요구 사항
- **JDK 11 이상** (Java 8도 동작하지만 최적 성능을 위해 Java 11+ 권장).  
- **IDE** (IntelliJ IDEA, Eclipse, VS Code 등 Java 확장 포함).  
- **Maven 또는 Gradle** (예제는 아래).  
- **샘플 PDF** (`sample.pdf` 등 구현 테스트용).  
- **유효한 GroupDocs.Signature 라이선스** (개발용 무료 체험, 프로덕션용 유료 라이선스).

## GroupDocs.Signature for Java 설정

### Maven 구성
Add the dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle 구성
For Gradle projects, add this to your `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### 직접 다운로드 옵션
You can also download the JAR file directly from [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) and add it to your project’s classpath manually. This approach works well in restricted‑network environments.

### 라이선스 받기
Request a free trial or temporary license from GroupDocs to remove watermarks and unlock all features. Production deployments require a purchased license.

### 기본 초기화
`Signature` is the entry point for all signing operations. It loads the PDF, applies the barcode, and writes the signed file.

```java
import com.groupdocs.signature.Signature;

class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("sample.pdf");
        // Proceed with signing operations...
    }
}
```

## HIBC 바코드가 포함된 Data Matrix PDF 만들기
Instantiate `Signature` with your source PDF, set `QrCodeSignOptions` to the **Data Matrix** format, provide a correctly formatted HIBC string, and call `sign()`. The library writes the signed PDF to the destination, preserving layout and embedding the barcode as a tamper‑evident signature.

`QrCodeSignOptions` specifies the barcode type, content, size, and placement for a signature.

1. **필요한 클래스 가져오기** – 서명 엔진 및 Data Matrix 옵션에 접근할 수 있습니다.  

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
```

2. **절대 경로를 사용해 `Signature` 객체 인스턴스화** – 소스와 대상 파일 경로를 지정합니다.  

```java
String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY";
String destinFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithHIBCLICQR.pdf";

final Signature signature = new Signature(sourceFilePath);
```

3. **Data Matrix 옵션 구성** – HIBC 문자열을 설정하고 `QrCodeTypes.HIBCLICDataMatrix`를 선택한 뒤 배치 좌표를 정의합니다. `QrCodeTypes`는 HIBC 서명을 위한 지원 바코드 포맷을 열거합니다.  

```java
QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR);
hibcLic_QR.setLeft(1); // Set the position from left
hibcLic_QR.setTop(1);   // Set the position from top
hibcLic_QR.setReturnContent(true); // Return content after signing
hibcLic_QR.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

4. **PDF에 서명 적용**  

```java
signature.sign(destinFilePath, hibcLic_QR);
```

5. **리소스 해제** – 파일 핸들을 해제하고 메모리 누수를 방지합니다.  

```java
finally {
    if (signature != null) signature.dispose();
}
```

### 전체 작업 예제
Here’s the full flow in a single block (the placeholders represent the exact code you’ll paste from the earlier snippets):

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;

public class HibcQrSigning {
    public static void main(String[] args) {
        String sourceFilePath = "sample.pdf";
        String destinFilePath = "output/SignWithHIBCLICQR.pdf";
        
        Signature signature = null;
        try {
            signature = new Signature(sourceFilePath);
            
            QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions(
                "A123PROD30917/75#422011907#GP293", 
                QrCodeTypes.HIBCLICQR
            );
            hibcLic_QR.setLeft(1);
            hibcLic_QR.setTop(1);
            hibcLic_QR.setReturnContent(true);
            hibcLic_QR.setReturnContentType(FileType.PNG);
            
            signature.sign(destinFilePath, hibcLic_QR);
            System.out.println("PDF signed successfully with HIBC QR code");
            
        } catch (Exception e) {
            System.err.println("Error signing PDF: " + e.getMessage());
            e.printStackTrace();
        } finally {
            if (signature != null) signature.dispose();
        }
    }
}
```

#### 직접 답변 (40–70 단어)
To **create a Data Matrix PDF**, instantiate `Signature` with your source PDF, set `QrCodeSignOptions` to `QrCodeTypes.HIBCLICDataMatrix` and provide a correctly formatted HIBC string, then call `signature.sign(outputPath, options)`. The library writes the signed PDF to the destination, preserving layout and embedding the barcode as a tamper‑evident signature.

## GroupDocs.Signature를 사용해 QR 코드 PDF 추가하기
Load the PDF, configure `QrCodeSignOptions` for the QR format, and call `sign()`. The library scales the QR image for readability and positions it based on the coordinates you set, avoiding overlap with existing content. This ensures the barcode remains scannable after printing and complies with HIBC standards.

`QrCodeSignOptions` defines the QR barcode’s content, size, and position.

1. **QR‑전용 클래스 가져오기**  

```java
QrCodeSignOptions hibcLic_AZ = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec);
hibcLic_AZ.setLeft(1); // Set the position from left
hibcLic_AZ.setTop(200); // Set the position from top
hibcLic_AZ.setReturnContent(true); // Return content after signing
hibcLic_AZ.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

2. **QR 옵션 생성 및 구성** – `QrCodeTypes.HIBCLICQR` 사용에 유의합니다.  

```java
signature.sign(destinFilePath, hibcLic_AZ);
```

3. **문서 서명**  

```java
QrCodeSignOptions hibcLic_DM = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix);
hibcLic_DM.setLeft(1); // Set the position from left
hibcLic_DM.setTop(400); // Set the position from top
hibcLic_DM.setReturnContent(true); // Return content after signing
hibcLic_DM.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

> **Direct answer:** Use `QrCodeTypes.HIBCLICQR` in `QrCodeSignOptions`, set the HIBC content string, position the code with `setLeft()` and `setTop()`, then call `signature.sign(outputPath, options)`. The QR barcode is embedded instantly, ready for smartphone or scanner capture.

## 피해야 할 일반적인 실수

### 1. 리소스 해제 누락
**Wrong:**  
```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  

**Fix:** Wrap the `Signature` usage in a try‑with‑resources block or explicitly call `close()` in a finally clause.

### 2. 잘못된 HIBC 형식 문자열 사용
**Wrong:** Using generic strings like “12345”.  
**Fix:** Follow the HIBCC standard (e.g., `A123PROD30917/75#422011907#GP293`). Validate with the [HIBCC online validator](https://www.hibcc.org/).

### 3. 파일 경로 하드코딩
**Wrong:**  
```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  

**Fix:** Store paths in a configuration file or environment variable and read them at runtime.

### 4. 바코드 위치 충돌 무시
Place barcodes away from existing text or signatures. Use PDF coordinates (origin is bottom‑left) and test with a printed sample.

### 5. 실제 스캐너로 테스트 안 함
Print the signed PDF and scan it with the exact hardware used in your workflow. Verify readability at different print qualities.

## 의료 분야 실용 사례

| 시나리오 | 권장 바코드 | 이유 |
|----------|--------------------|--------------|
| **제약 유통** | QR 코드 | 높은 데이터 용량, 스마트폰으로 널리 스캔 가능. |
| **재고 관리** | Data Matrix | 작은 발자국, 밀집된 선반 라벨에 이상적. |
| **규제 준수 (FDA 21 CFR Part 11)** | QR + Data Matrix | 이중 포맷으로 중복성과 감사 가능성 제공. |
| **의료기기 추적** | Aztec 코드 | 제한된 공간 포장에 적합한 컴팩트 사이즈. |

## 성능 고려 사항 및 모범 사례

### 배치 처리 패턴
```java
List<String> filesToSign = getFileList();
for (String filePath : filesToSign) {
    Signature signature = null;
    try {
        signature = new Signature(filePath);
        // Sign and save
    } finally {
        if (signature != null) signature.dispose();
    }
}
```

- Create a new `Signature` instance per file to keep memory usage low.  
- Use a fixed thread pool (`Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() - 1)`) for parallel processing, but monitor heap size because each `Signature` holds the full PDF in memory.  

### 라이브러리 최신 상태 유지
GroupDocs releases improve processing speed by up to **20 %** and add new HIBC compliance features. Schedule quarterly dependency checks.

### 템플릿 캐싱
Load a PDF template once, clone it for each barcode variant, and sign the clones. This reduces I/O and speeds up high‑volume workflows.

## 자주 묻는 질문

**Q: GroupDocs.Signature가 PDF 외 다른 파일 형식을 서명할 수 있나요?**  
A: Yes, it also supports DOCX, XLSX, PPTX, PNG, JPEG, and TIFF with the same barcode‑signing API.

**Q: “Invalid barcode content” 오류를 어떻게 해결하나요?**  
A: Verify that your HIBC string follows the exact HIBCC syntax, use the online validator, and ensure you’re using the correct `QrCodeTypes` constant for the chosen format.

**Q: 각 HIBC 포맷의 최대 데이터 용량은 얼마인가요?**  
A: QR ≈ 4,296 alphanumeric characters, Aztec ≈ 3,832 numeric / 3,067 alphanumeric, Data Matrix ≈ 3,116 numeric / 2,335 alphanumeric. Keep codes under 200 characters for optimal scan reliability.

**Q: 하나의 PDF에 여러 바코드 유형을 삽입할 수 있나요?**  
A: Absolutely. Create separate `QrCodeSignOptions` objects with different positions and call `signature.sign()` for each. Just ensure they don’t overlap.

**Q: 런타임에 서명할 때 인터넷 연결이 필요합니까?**  
A: No. After the JAR is on the classpath and the license is activated, all operations are performed locally.

## 추가 자료

- [GroupDocs.Signature for Java 문서](https://docs.groupdocs.com/signature/java/)  
- [API Reference Guide](https://reference.groupdocs.com/signature/java/)  
- [Latest Release Downloads](https://releases.groupdocs.com/signature/java/)  
- [Purchase License](https://purchase.groupdocs.com/buy)  
- [Get Free Trial](https://releases.groupdocs.com/signature/java/)  
- [Request Temporary License](https://purchase.groupdocs.com/temporary-license/)  
- [GroupDocs Forum](https://forum.groupdocs.com/c/signature/)  

---

**마지막 업데이트:** 2026-09-15  
**테스트 환경:** GroupDocs.Signature 23.12 for Java  
**작성자:** GroupDocs  

## 관련 튜토리얼

- [Java에서 바코드 서명 PDF 만들기 – GroupDocs 가이드](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)
- [Java에서 바코드 서명 만들기 – PDF 바코드 업데이트](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [Java와 GroupDocs.Signature를 사용해 QR 코드 PDF 읽기](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)

```java
signature.sign(destinFilePath, hibcLic_DM);
```

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}