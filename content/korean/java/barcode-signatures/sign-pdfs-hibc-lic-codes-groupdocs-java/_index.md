---
categories:
- Document Signing
- Healthcare Integration
date: '2026-05-16'
description: GroupDocs.Signature for Java를 사용하여 data matrix PDF를 만들고 QR code PDF를
  추가하는 방법을 배웁니다. 의료 문서 서명을 위한 단계별 가이드.
keywords:
- create data matrix pdf
- add qr code pdf
- HIBC barcode Java
lastmod: '2026-05-16'
linktitle: HIBC PDF 서명 Java 가이드
schemas:
- author: GroupDocs
  dateModified: '2026-05-16'
  description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  headline: Create Data Matrix PDF with HIBC Barcode in Java
  type: TechArticle
- description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  name: Create Data Matrix PDF with HIBC Barcode in Java
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
- java
- pdf-signing
- hibc
- healthcare
- barcode
- pharmaceutical
title: Java에서 HIBC 바코드로 Data Matrix PDF 만들기
type: docs
url: /ko/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/
weight: 1
---

# Java에서 HIBC 바코드가 포함된 데이터 매트릭스 PDF 생성

제약 또는 의료 물류 소프트웨어를 개발하고 있다면, 종이 기반 추적, 서명 분실, 감사 악몽 같은 문제에 직면했을 가능성이 높습니다. **데이터 매트릭스 PDF 생성** 및 HIBC LIC 바코드 삽입은 인쇄, 스캔 및 규제 검토를 견디는 변조 방지 및 기계 판독 가능한 추적 정보를 제공함으로써 이러한 문제를 해결합니다. 이 튜토리얼에서는 GroupDocs.Signature for Java를 사용하여 **QR 코드 PDF** 지원은 물론 Aztec 및 Data Matrix 형식을 **추가하는 방법**을 정확히 보여드립니다.

## 빠른 답변
- **Java에서 HIBC 바코드를 처리하는 라이브러리는?** GroupDocs.Signature for Java.  
- **가장 컴팩트한 바코드 형식은?** Data Matrix – 작은 라벨에 이상적.  
- **같은 PDF에 QR과 Data Matrix를 모두 추가할 수 있나요?** 예, 별도의 `QrCodeSignOptions`를 생성하면 됩니다.  
- **런타임에 인터넷 연결이 필요합니까?** 아니요, 설치 후 라이브러리는 완전히 오프라인으로 작동합니다.  
- **추천 Java 버전은?** 프로덕션 수준 성능을 위해 Java 11+.

## HIBC 바코드 PDF 서명은 무엇인가요?
`Signature` 클래스는 GroupDocs.Signature for Java에서 PDF 문서를 나타내며 HIBC 바코드를 디지털 서명으로 삽입하는 메서드를 제공합니다. PDF에 HIBC 바코드로 서명하면 공급망 어느 단계에서든 스캔할 수 있는 검증 가능하고 변조 방지 기록을 생성합니다.

## Data Matrix와 QR 코드를 함께 사용하는 이유는?
GroupDocs.Signature는 **50개 이상의 입력 및 출력 형식**을 지원하며 전체 파일을 메모리에 로드하지 않고 수백 페이지 PDF를 처리할 수 있습니다. 작은 면적의 고밀도 라벨에는 Data Matrix를, 넓은 문서에는 QR 코드를 사용하면 가독성, 데이터 용량(QR은 최대 4,296자) 및 인쇄 공간 효율성 사이의 최적 균형을 얻을 수 있습니다.

## 사전 요구 사항
- **JDK 11 이상** (Java 8도 동작하지만 최적 성능을 위해 Java 11+ 권장).  
- **IDE** (IntelliJ IDEA, Eclipse, VS Code 등 Java 확장 포함).  
- **Maven 또는 Gradle** (예시는 아래).  
- **샘플 PDF** (예: `sample.pdf`)를 사용해 구현을 테스트합니다.  
- **유효한 GroupDocs.Signature 라이선스** (개발용 무료 체험, 프로덕션용 유료 라이선스).

## GroupDocs.Signature for Java 설정

### Maven 구성
`pom.xml`에 의존성을 추가합니다:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle 구성
Gradle 프로젝트의 `build.gradle`에 다음을 추가합니다:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### 직접 다운로드 옵션
JAR 파일을 직접 [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/)에서 다운로드하고 프로젝트의 클래스패스에 수동으로 추가할 수 있습니다. 이 방법은 네트워크가 제한된 환경에서 잘 작동합니다.

### 라이선스 받기
GroupDocs에 무료 체험 또는 임시 라이선스를 요청하여 워터마크를 제거하고 모든 기능을 사용할 수 있습니다. 프로덕션 배포에는 구매한 라이선스가 필요합니다.

### 기본 초기화
`Signature` 클래스는 모든 서명 작업의 진입점입니다. PDF를 로드하고 바코드를 적용한 뒤 서명된 파일을 작성합니다.

```java
import com.groupdocs.signature.Signature;

class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("sample.pdf");
        // Proceed with signing operations...
    }
}
```

## HIBC 바코드가 포함된 Data Matrix PDF를 만드는 방법은?
소스 PDF를 로드하고 Data Matrix 형식을 위한 `QrCodeSignOptions` 객체를 구성한 뒤 `sign()`을 호출하면 규격에 맞는 HIBC Data Matrix 바코드를 삽입할 수 있습니다. 아래 단계에서 정확한 코드를 안내합니다. `QrCodeSignOptions`는 바코드 서명의 유형, 내용, 크기 및 위치와 같은 설정을 정의합니다.

1. **필요한 클래스를 가져옵니다** – 서명 엔진 및 Data Matrix 옵션에 접근할 수 있습니다.  

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
```

2. **`Signature` 객체를 인스턴스화합니다** – 소스와 대상 파일의 절대 경로를 사용합니다.  

```java
String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY";
String destinFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithHIBCLICQR.pdf";

final Signature signature = new Signature(sourceFilePath);
```

3. **Data Matrix 옵션을 구성합니다** – HIBC 문자열을 설정하고 `QrCodeTypes.HIBCLICDataMatrix`를 선택한 뒤 배치 좌표를 정의합니다. `QrCodeTypes`는 HIBC 서명을 위한 지원 바코드 형식을 열거합니다.  

```java
QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR);
hibcLic_QR.setLeft(1); // Set the position from left
hibcLic_QR.setTop(1);   // Set the position from top
hibcLic_QR.setReturnContent(true); // Return content after signing
hibcLic_QR.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

4. **PDF에 서명을 적용합니다**.  

```java
signature.sign(destinFilePath, hibcLic_QR);
```

5. **리소스를 해제합니다** – 파일 핸들을 해제하고 메모리 누수를 방지합니다.  

```java
finally {
    if (signature != null) signature.dispose();
}
```

### 전체 작업 예제
전체 흐름을 하나의 블록에 정리했습니다(플레이스홀더는 앞서의 스니펫에서 복사한 정확한 코드를 의미합니다):

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
**Data Matrix PDF를 생성하려면** `Signature`를 소스 PDF와 함께 인스턴스화하고 `QrCodeSignOptions`를 `QrCodeTypes.HIBCLICDataMatrix`로 설정한 뒤 올바르게 포맷된 HIBC 문자열을 제공한 후 `signature.sign(outputPath, options)`를 호출합니다. 라이브러리는 서명된 PDF를 대상 위치에 기록하고 레이아웃을 보존하면서 바코드를 변조 방지 서명으로 삽입합니다.

## GroupDocs.Signature를 사용하여 QR 코드 PDF를 추가하는 방법은?
PDF를 로드하고 QR 형식을 위한 `QrCodeSignOptions`를 구성한 뒤 `sign()`을 호출합니다. 이 두 줄 패턴은 모든 PDF 크기에 적용 가능하며 QR 이미지를 최적 가독성을 위해 자동으로 스케일합니다. `QrCodeSignOptions`는 QR 바코드 서명의 내용 및 시각적 속성을 구성합니다. 설정한 좌표에 따라 코드를 배치하여 기존 콘텐츠와 겹치지 않으며 인쇄 후에도 스캔 가능하도록 합니다.

1. **QR 전용 클래스를 가져옵니다**  

```java
QrCodeSignOptions hibcLic_AZ = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec);
hibcLic_AZ.setLeft(1); // Set the position from left
hibcLic_AZ.setTop(200); // Set the position from top
hibcLic_AZ.setReturnContent(true); // Return content after signing
hibcLic_AZ.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

2. **QR 옵션을 생성하고 구성합니다** – `QrCodeTypes.HIBCLICQR` 사용에 유의하세요.  

```java
signature.sign(destinFilePath, hibcLic_AZ);
```

3. **문서에 서명합니다**  

```java
QrCodeSignOptions hibcLic_DM = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix);
hibcLic_DM.setLeft(1); // Set the position from left
hibcLic_DM.setTop(400); // Set the position from top
hibcLic_DM.setReturnContent(true); // Return content after signing
hibcLic_DM.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

> **Direct answer:** `QrCodeSignOptions`에 `QrCodeTypes.HIBCLICQR`를 사용하고 HIBC 내용 문자열을 설정한 뒤 `setLeft()`와 `setTop()`으로 코드를 배치하고 `signature.sign(outputPath, options)`를 호출합니다. QR 바코드가 즉시 삽입되어 스마트폰이나 스캐너로 캡처할 수 있습니다.

## 피해야 할 일반적인 실수

### 1. 리소스 해제 누락
**Wrong:**  
```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  

**Fix:** `Signature` 사용을 try‑with‑resources 블록으로 감싸거나 finally 절에서 명시적으로 `close()`를 호출합니다.

### 2. 잘못된 HIBC 형식 문자열 사용
**Wrong:** Using generic strings like “12345”.  
**Fix:** HIBCC 표준을 따르세요(예: `A123PROD30917/75#422011907#GP293`). [HIBCC online validator](https://www.hibcc.org/)로 검증합니다.

### 3. 파일 경로 하드코딩
**Wrong:**  
```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  

**Fix:** 경로를 설정 파일이나 환경 변수에 저장하고 런타임에 읽어옵니다.

### 4. 바코드 위치 충돌 무시
기존 텍스트나 서명과 떨어진 위치에 바코드를 배치하세요. PDF 좌표계(원점은 왼쪽 하단)를 사용하고 인쇄된 샘플로 테스트합니다.

### 5. 실제 스캐너로 테스트하지 않음
서명된 PDF를 인쇄하고 워크플로우에서 사용하는 정확한 하드웨어로 스캔합니다. 다양한 인쇄 품질에서 가독성을 확인합니다.

## 의료 분야 실용 사례

| 시나리오 | 추천 바코드 | 적합한 이유 |
|----------|--------------------|--------------|
| **제약 유통** | QR Code | 데이터 용량이 크고 스마트폰으로 널리 스캔됩니다. |
| **재고 관리** | Data Matrix | 작은 공간 차지, 밀집된 선반 라벨에 이상적. |
| **규제 준수 (FDA 21 CFR Part 11)** | QR + Data Matrix | 이중 형식으로 중복성과 감사 가능성을 제공합니다. |
| **의료기기 추적** | Aztec Code | 컴팩트한 크기로 제한된 공간 포장에 적용됩니다. |

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

- 파일당 새로운 `Signature` 인스턴스를 생성하여 메모리 사용량을 낮게 유지합니다.  
- 병렬 처리를 위해 고정 스레드 풀(`Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() - 1)`)을 사용하되, 각 `Signature`이 전체 PDF를 메모리에 보관하므로 힙 크기를 모니터링합니다.  
- 라이브러리를 최신 상태로 유지하세요. GroupDocs 릴리스는 처리 속도를 최대 **20 %**까지 개선하고 새로운 HIBC 준수 기능을 추가합니다. 분기별 의존성 검사를 일정에 포함합니다.  
- 템플릿 캐싱: PDF 템플릿을 한 번 로드하고 각 바코드 변형마다 복제한 뒤 서명합니다. 이렇게 하면 I/O를 줄이고 대량 워크플로우 속도를 높일 수 있습니다.

## 자주 묻는 질문

**Q: GroupDocs.Signature가 PDF 외의 파일 유형에도 서명할 수 있나요?**  
A: 예, 동일한 바코드 서명 API로 DOCX, XLSX, PPTX, PNG, JPEG, TIFF도 지원합니다.

**Q: “Invalid barcode content”(잘못된 바코드 내용) 오류를 어떻게 해결하나요?**  
A: HIBC 문자열이 정확히 HIBCC 구문을 따르는지 확인하고 온라인 검증기를 사용하며, 선택한 형식에 맞는 `QrCodeTypes` 상수를 사용했는지 점검합니다.

**Q: 각 HIBC 형식의 최대 데이터 용량은 얼마인가요?**  
A: QR ≈ 4,296 알파벳·숫자 문자, Aztec ≈ 3,832 숫자 / 3,067 알파벳·숫자, Data Matrix ≈ 3,116 숫자 / 2,335 알파벳·숫자. 최적 스캔 신뢰성을 위해 200자 이하로 유지하세요.

**Q: 하나의 PDF에 여러 바코드 유형을 삽입할 수 있나요?**  
A: 가능합니다. 서로 다른 위치에 별도의 `QrCodeSignOptions` 객체를 만들고 각각 `signature.sign()`을 호출하면 됩니다. 단, 겹치지 않도록 주의하세요.

**Q: 런타임에 서명하려면 인터넷 연결이 필요합니까?**  
A: 아닙니다. JAR가 클래스패스에 있고 라이선스가 활성화되면 모든 작업이 로컬에서 수행됩니다.

## 추가 자료

- [GroupDocs.Signature for Java 문서](https://docs.groupdocs.com/signature/java/)  
- [API 레퍼런스 가이드](https://reference.groupdocs.com/signature/java/)  
- [최신 릴리스 다운로드](https://releases.groupdocs.com/signature/java/)  
- [라이선스 구매](https://purchase.groupdocs.com/buy)  
- [무료 체험 받기](https://releases.groupdocs.com/signature/java/)  
- [임시 라이선스 요청](https://purchase.groupdocs.com/temporary-license/)  
- [GroupDocs 포럼](https://forum.groupdocs.com/c/signature/)

---

**마지막 업데이트:** 2026-05-16  
**테스트 환경:** GroupDocs.Signature 23.12 for Java  
**작성자:** GroupDocs  

```java
signature.sign(destinFilePath, hibcLic_DM);
```

## 관련 튜토리얼

- [Java에서 바코드 서명 PDF 만들기 – GroupDocs 가이드](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)
- [Java에서 바코드 서명 만들기 – PDF 바코드 업데이트](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [Java와 GroupDocs.Signature를 사용해 QR 코드 PDF 읽는 방법](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)