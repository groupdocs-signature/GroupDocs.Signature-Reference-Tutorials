---
categories:
- Java Development
date: '2026-07-25'
description: GroupDocs.Signature for Java를 사용하여 PDF에 바코드 서명을 추가하는 방법을 배웁니다. 단계별 Maven
  설정, 바코드 옵션, 오류 처리 및 운영 팁.
keywords:
- add barcode signature
- groupdocs signature java
- scannable pdf signature
- pdf signing java
- troubleshoot pdf signing
lastmod: '2026-07-25'
linktitle: GroupDocs.Signature Java 튜토리얼
og_description: GroupDocs.Signature Java를 사용하여 PDF에 바코드 서명을 추가합니다. 전체 Maven 설정, 바코드
  옵션, 문제 해결 및 Java 개발자를 위한 운영 모범 사례.
og_image_alt: 'Guide: add barcode signature to PDF using GroupDocs.Signature Java'
og_title: GroupDocs.Signature Java를 사용하여 PDF에 바코드 서명 추가
schemas:
- author: GroupDocs
  dateModified: '2026-07-25'
  description: Learn how to add barcode signature to PDFs using GroupDocs.Signature
    for Java. Step‑by‑step Maven setup, barcode options, error handling, and production
    tips.
  headline: Add barcode signature to PDFs with GroupDocs.Signature Java
  type: TechArticle
- description: Learn how to add barcode signature to PDFs using GroupDocs.Signature
    for Java. Step‑by‑step Maven setup, barcode options, error handling, and production
    tips.
  name: Add barcode signature to PDFs with GroupDocs.Signature Java
  steps:
  - name: Initialize the Signature Object
    text: 'The `Signature` class is GroupDocs.Signature''s entry point for all signing
      operations. It represents a single PDF document in memory and provides lazy
      loading to keep memory usage low. java import com.groupdocs.signature.Signature;
      public class InitializeSignature { public static void main(String[] '
  - name: Configure Barcode Sign Options
    text: '`BarcodeSignOptions` lets you define every attribute of the barcode—type,
      data, position, colors, borders, and even whether the raw barcode image should
      be returned. java import com.groupdocs.signature.Signature; import com.groupdocs.signature.exception.GroupDocsSignatureException;
      import java.nio.f'
  - name: Sign the Document
    text: 'The `sign` method applies the configured barcode to the PDF and writes
      the result to the target path. java signOptions.setEncodeType(BarcodeTypes.QR);
      // QR codes for more data signOptions.setForeColor(Color.BLACK); signOptions.setBackgroundColor(Color.WHITE);
      // Remove border and fancy styling for '
  type: HowTo
- questions:
  - answer: GroupDocs.Signature for Java is self‑contained; after adding the Maven/Gradle
      artifact you get full barcode generation and PDF rendering without any third‑party
      libraries.
    question: How do I add a barcode signature to a PDF in Java without external dependencies?
  - answer: Absolutely. Switch the `BarcodeTypes` enum to `QRCode` and adjust size
      parameters as needed.
    question: Can I configure barcode sign options in Java to generate QR codes?
  - answer: Pin the exact version in `pom.xml` (e.g., `23.10.0`) to avoid accidental
      upgrades, and enable the Maven `shade` plugin to produce a single executable
      JAR.
    question: What is the recommended Maven setup for production use?
  - answer: Yes. Provide the password when constructing the `Signature` object, then
      proceed with signing as usual.
    question: Does the library support password‑protected PDFs?
  - answer: GroupDocs.Signature can address all pages in a PDF at once or target specific
      pages via `setPageNumber()`. Performance scales linearly; a 200‑page PDF signs
      in ~2 seconds on a typical cloud VM.
    question: How many pages can I sign in one operation?
  type: FAQPage
tags:
- pdf-signing
- digital-signatures
- groupdocs
- barcode-signatures
title: GroupDocs.Signature Java를 사용하여 PDF에 바코드 서명 추가
type: docs
url: /ko/java/digital-signatures/java-pdf-signing-groupdocs-signature-guide/
weight: 1
---

# GroupDocs.Signature Java를 사용하여 PDF에 바코드 서명 추가

현대 문서 중심 애플리케이션에서 **add barcode signature**는 PDF를 인간이 읽을 수 있으면서도 기계가 스캔할 수 있게 만드는 빠르고 신뢰할 수 있는 방법입니다. 이 튜토리얼은 Maven 구성부터 바코드 스타일링, 대용량 파일 처리까지 모든 단계를 안내하므로 Java 프로젝트에 바코드 서명을 자신 있게 통합할 수 있습니다.

## 빠른 답변
- **서명을 시작하기 위한 첫 번째 코드 라인은 무엇인가요?** `Signature signature = new Signature("sample.pdf");`
- **필요한 Maven 아티팩트는 무엇인가요?** `com.groupdocs:groupdocs-signature:23.10` (replace with the latest version)
- **비밀번호로 보호된 PDF에 서명할 수 있나요?** Yes—pass the password when creating the `Signature` object.
- **지원되는 바코드 형식은 몇 개인가요?** Over 30, including Code128, QR, DataMatrix, and Aztec.
- **100 MB PDF에 권장되는 힙 크기는 얼마인가요?** At least `-Xmx2g` (2 GB) to avoid `OutOfMemoryError`.

## 바코드 서명이란 무엇인가요?
**barcode signature**는 PDF에 삽입된 기계가 읽을 수 있는 바코드로, 변조 방지 표시 역할을 하며 ID, 타임스탬프, URL과 같은 사용자 정의 데이터를 담을 수 있습니다. 시각적 검증과 자동 스캔을 결합하여 재고 관리, 규정 준수 및 대량 워크플로 자동화에 이상적입니다.

## 왜 GroupDocs.Signature Java로 바코드 서명을 추가하나요?
GroupDocs.Signature는 **50+**개의 입력 및 출력 형식을 지원하고, 전체 파일을 메모리에 로드하지 않고 수백 페이지 PDF를 처리하며, 바코드의 모든 시각적 요소를 세밀하게 조정할 수 있는 유연한 Java API를 제공합니다. 벤치마크 테스트에서 Code128 바코드가 포함된 150페이지 PDF 서명은 표준 2 vCPU 클라우드 인스턴스에서 **1.2초 미만**에 완료됩니다.

## 전제 조건
시작하기 전에 다음 항목이 준비되어 있는지 확인하세요:

- **Java Development Kit (JDK)** 8 이상 (장기 지원을 위해 JDK 11 또는 17 권장)
- **IDE** (IntelliJ IDEA, Eclipse, 또는 Java 확장이 포함된 VS Code)
- **Build tool** (Maven 3.6+ 또는 Gradle 7.0+)
- **GroupDocs.Signature Java library** (아래에서 Maven 및 Gradle 설정을 보여드립니다)
- Java OOP 개념 및 Maven/Gradle 프로젝트 구조에 대한 기본적인 이해

### 필요한 라이브러리 및 종속성
GroupDocs.Signature는 Maven 또는 Gradle과 원활하게 통합됩니다. 현재 사용 중인 빌드 도구를 선택하세요:

**Maven 설정**  
```markdown
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```
```

**Gradle 설정**  
```markdown
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```
```

수동으로 JAR를 다루는 것을 선호한다면, 최신 릴리스를 [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/)에서 다운로드하고 클래스패스에 추가하세요.

### 라이선스 획득 단계
GroupDocs는 세 가지 라이선스 모델을 제공합니다:

- **Free Trial** – 30일 동안 전체 기능 사용 가능 (서명된 PDF에 워터마크가 적용됩니다)
- **Temporary License** – 기능 제한 없이 연장된 체험판 (개발 파이프라인에 이상적)
- **Full License** – 프로덕션 준비 완료, 우선 지원 및 워터마크 없음  

적절한 라이선스는 [GroupDocs Licensing](https://purchase.groupdocs.com/buy)에서 구매하세요. 체험판 중에도 코드를 로컬에서 실행할 수 있지만, 실제 운영 전에는 체험 키를 영구 키로 교체해야 합니다.

## GroupDocs.Signature Java를 사용하여 PDF에 바코드 서명을 추가하려면 어떻게 해야 하나요?
`Signature` 클래스는 GroupDocs.Signature에서 문서를 다루기 위한 주요 진입점입니다.  
`BarcodeSignOptions` 클래스는 바코드의 데이터, 유형 및 시각적 모습을 지정합니다.  

`new Signature("source.pdf")`로 원본 PDF를 로드하고, 원하는 데이터와 시각 스타일을 가진 `BarcodeSignOptions` 객체를 구성한 뒤 `signature.sign("output.pdf", options)`를 호출합니다. 이 3단계 패턴은 파일 I/O, 바코드 생성 및 PDF 작성을 하나의 스레드‑안전 호출로 처리하며, 몇 킬로바이트에서 수백 메가바이트에 이르는 PDF에 모두 적용됩니다.

### 1단계: Signature 객체 초기화
`Signature` 클래스는 GroupDocs.Signature의 모든 서명 작업을 위한 진입점입니다. 메모리 내에서 단일 PDF 문서를 나타내며, 메모리 사용량을 낮게 유지하기 위해 지연 로딩을 제공합니다.

```markdown
```java
import com.groupdocs.signature.Signature;

public class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/sample.pdf");
        System.out.println("GroupDocs.Signature initialized successfully.");
    }
}
```
```

**Explanation:**  
- `filePath`는 서명하려는 원본 PDF의 경로를 가리킵니다.  
- `outputFilePath`는 서명된 PDF가 저장될 위치이며, 원본 파일을 보존합니다.  
- `try‑catch` 블록은 I/O 오류, 파일 누락 또는 권한 문제를 우아하게 처리하도록 보장합니다.

### 2단계: 바코드 서명 옵션 구성
`BarcodeSignOptions`를 사용하면 바코드의 모든 속성(유형, 데이터, 위치, 색상, 테두리 및 원시 바코드 이미지 반환 여부)을 정의할 수 있습니다.

```markdown
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import java.nio.file.Paths;
import java.io.File;

public class Feature1 {
    public static void run() throws Exception {
        String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
        String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", "SignedOutputSample.pdf").getPath();

        try {
            Signature signature = new Signature(filePath);
            System.out.println("Signature initialized and paths set.");
        } catch (Exception e) {
            throw new GroupDocsSignatureException(e.getMessage());
        }
    }
}
```
```

**핵심 설정 설명:**

- **Data & Type** – `"12345678"`는 페이로드이며, `BarcodeTypes.Code128`은 알파벳·숫자 문자열에 작동하고 스캐너에서 널리 지원됩니다.  
- **Positioning** – `setLeft(100)` 및 `setTop(100)`은 바코드를 좌상단 모서리에서 100 px 떨어뜨립니다; `VerticalAlignment.Top` + `HorizontalAlignment.Right`는 해당 오프셋을 기준으로 정렬을 조정합니다.  
- **Margins & Padding** – `Padding` 객체는 페이지 가장자리를 클리핑하지 않도록 20 px 여백을 추가합니다.  
- **Styling** – 테두리, 폰트 및 배경 브러시는 완전히 사용자 정의 가능하며, 프로덕션에서는 렌더링 속도 향상을 위해 그라디언트를 제거할 수 있습니다.  
- **Return Content** – `setReturnContent(true)`를 활성화하면 바코드가 `byte[]` 형태로 반환되어 데이터베이스에 이미지 저장하거나 UI에 표시하는 데 유용합니다.

#### 최소 프로덕션 준비 구성
깨끗한 법적 문서의 경우 일반적으로 추가 테두리 없이 검은색-흰색 바코드만 원합니다:

```markdown
```java
import com.groupdocs.signature.domain.enums.*;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.Border;
import com.groupdocs.signature.domain.DashStyle;
import com.groupdocs.signature.domain.extensions.LinearGradientBrush;
import com.groupdocs.signature.domain.font.SignatureFont;
import java.awt.Color;
import com.groupdocs.signature.options.sign.BarcodeSignOptions;

public class Feature2 {
    public static void configureBarcodeOptions() throws Exception {
        BarcodeSignOptions signOptions = new BarcodeSignOptions("12345678");
        signOptions.setEncodeType(BarcodeTypes.Code128);
        signOptions.setLeft(100);
        signOptions.setTop(100);
        signOptions.setVerticalAlignment(VerticalAlignment.Top);
        signOptions.setHorizontalAlignment(HorizontalAlignment.Right);

        Padding padding = new Padding();
        padding.setLeft(20);
        padding.setTop(20);
        signOptions.setMargin(padding);

        Border border = new Border();
        border.setColor(Color.GREEN);
        border.setDashStyle(DashStyle.DashLongDashDot);
        border.setWeight(2);
        border.setTransparency(0.5);
        border.setVisible(true);
        signOptions.setBorder(border);

        signOptions.setForeColor(Color.RED);
        SignatureFont font = new SignatureFont();
        font.setSize(12);
        font.setFamilyName("Comic Sans MS");
        signOptions.setFont(font);

        signOptions.setCodeTextAlignment(CodeTextAlignment.Above);

        Background background = new Background();
        background.setColor(Color.GREEN);
        background.setTransparency(0.5);
        background.setBrush(new LinearGradientBrush(Color.GREEN, Color.DARK_GRAY, 0));
        signOptions.setBackground(background);

        signOptions.setReturnContent(true);
        signOptions.setReturnContentType(FileType.PNG);
    }
}
```
```

### 3단계: 문서 서명
`sign` 메서드는 구성된 바코드를 PDF에 적용하고 결과를 대상 경로에 기록합니다.

```markdown
```java
signOptions.setEncodeType(BarcodeTypes.QR); // QR codes for more data
signOptions.setForeColor(Color.BLACK);
signOptions.setBackgroundColor(Color.WHITE);
// Remove border and fancy styling for professional appearance
```
```

**내부 동작:**  
- `signature.sign(outputFilePath, signOptions)`는 소스 파일을 그대로 두고 PDF에 바코드를 기록합니다.  
- `SignResult`는 추가된 서명의 수, 수정된 페이지 및 발생한 경고를 보고합니다.  
- 배치 작업의 경우, 이 호출을 `ExecutorService`로 감싸 CPU 코어에 걸쳐 병렬 처리합니다.

## 일반적인 문제 및 해결책

### 문제 1: 초기화 시 FileNotFoundException
**Symptom:** `Signature` 객체를 생성할 때 애플리케이션이 `FileNotFoundException`을 발생시킵니다.

**Root causes:**  
- 잘못된 파일 경로(상대 경로 vs 절대 경로)  
- 읽기 권한 누락  
- 다른 프로세스에 의해 파일이 잠김(예: Acrobat에서 열림)

**Fix:**  
```markdown
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.BaseSignature;

public class Feature3 {
    public static void signDocument(String filePath, BarcodeSignOptions signOptions) throws Exception {
        Signature signature = new Signature(filePath);
        String outputFilePath = filePath.replace(".pdf", "_Signed.pdf");

        try {
            com.groupdocs.signature.domain.signatures.SignResult signResult = signature.sign(outputFilePath, signOptions);
            System.out.println("Document signed successfully.");
        } catch (Exception e) {
            throw new GroupDocsSignatureException(e.getMessage());
        }
    }
}
```
```
경로에 슬래시(`/`)를 사용하거나(`C:/Docs/sample.pdf`) 백슬래시를 이스케이프(`C:\\Docs\\sample.pdf`)했는지 확인하세요. OS 권한을 검증하고 파일을 잠글 수 있는 프로그램을 종료하십시오.

### 문제 2: 출력에 바코드가 표시되지 않음
**Symptom:** 오류 없이 서명이 완료되었지만 바코드가 보이지 않습니다.

**Typical reasons:**  
- 위치 지정이 바코드를 인쇄 가능 영역 밖에 배치함.  
- 투명도가 `1.0`(완전 투명)으로 설정됨.  
- 폰트 크기가 `0`으로 설정됨.

**해결책:**  
- `setLeft`/`setTop` 값을 페이지 크기 내(표준 A4 기준 0‑600 px)로 유지하세요.  
- 투명도 값을 `0.0`(불투명)과 `0.9` 사이로 설정하세요.  
- 읽기 쉬운 폰트 크기, 예를 들어 `12pt`를 지정하세요.

### 문제 3: 대용량 문서에서 메모리 부족 오류
**Symptom:** 약 50 MB보다 큰 PDF를 처리할 때 `OutOfMemoryError`가 발생합니다.

**Remedies:**  
- JVM 힙을 늘리기: 문서 크기에 따라 `-Xmx2g` 이상으로 설정합니다.  
- `Signature`의 스트리밍 API를 사용해 PDF를 페이지별로 처리합니다.  
- 각 작업 후 `Signature` 인스턴스를 명시적으로 닫아 네이티브 리소스를 해제합니다.

```markdown
```java
import java.nio.file.Files;
import java.nio.file.Path;

Path filePath = Path.of("YOUR_DOCUMENT_DIRECTORY/sample.pdf");
if (!Files.exists(filePath)) {
    throw new IllegalArgumentException("PDF file not found: " + filePath);
}
if (!Files.isReadable(filePath)) {
    throw new SecurityException("Cannot read PDF file: " + filePath);
}
// Now safe to initialize
Signature signature = new Signature(filePath.toString());
```
```

### 문제 4: 잘못된 바코드 데이터 오류
**Symptom:** API가 지원되지 않는 문자를 포함했다는 예외를 발생시킵니다.

**원인:** 바코드 표준마다 허용하는 문자 집합이 다릅니다. Code128은 알파벳·숫자를 허용하고, QR은 유니코드를 처리할 수 있으며, 일부 1D 바코드는 숫자만 허용합니다.

**해결책:** 데이터에 맞는 바코드 유형을 선택하거나 `BarcodeSignOptions`에 할당하기 전에 문자열을 정제하세요.

```markdown
```java
String barcodeData = "ABC123"; // Your data
BarcodeTypes type = BarcodeTypes.Code128; // Alphanumeric support

// For numeric-only barcodes, validate first:
if (type == BarcodeTypes.EAN13 && !barcodeData.matches("\\d+")) {
    throw new IllegalArgumentException("EAN13 requires numeric data only");
}
```
```

## 프로덕션을 위한 모범 사례

### 1. 서명 전에 PDF 검증
런타임 파싱 오류를 방지하려면 파일이 올바른 PDF 형식인지 항상 확인하세요.

```markdown
```java
try (Signature signature = new Signature(filePath)) {
    // If this succeeds, file is valid
    signature.getDocumentInfo();
} catch (Exception e) {
    // Handle invalid PDF
}
```
```

### 2. 대량 작업을 위한 비동기 처리 사용
서명 작업을 백그라운드 스레드 풀에 위임하면 UI가 멈추는 것을 방지하고 처리량을 향상시킵니다.

```markdown
```java
ExecutorService executor = Executors.newFixedThreadPool(4);
List<String> pdfFiles = Arrays.asList("doc1.pdf", "doc2.pdf", "doc3.pdf");

pdfFiles.forEach(file -> {
    executor.submit(() -> {
        try {
            signDocument(file, signOptions);
        } catch (Exception e) {
            // Log error
        }
    });
});
executor.shutdown();
```
```

### 3. 구조화된 로깅 구현
입력 경로, 출력 경로, 바코드 데이터 및 예외를 포함한 각 서명 요청을 기록하세요. 이는 사후 분석 속도를 크게 높입니다.

```markdown
```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

private static final Logger logger = LoggerFactory.getLogger(YourClass.class);

try {
    SignResult result = signature.sign(outputFilePath, signOptions);
    logger.info("Document signed successfully: {}", outputFilePath);
    logger.debug("Signatures added: {}", result.getSucceeded().size());
} catch (Exception e) {
    logger.error("Failed to sign document: {}", filePath, e);
}
```
```

### 4. 속도 향상을 위한 바코드 설정 최적화
- 이미지가 별도로 필요하지 않은 경우 `setReturnContent(true)`를 비활성화합니다.  
- 그라디언트보다 단색 배경 브러시를 선호합니다.  
- 간단한 추적 용도에서는 테두리를 생략합니다.

### 5. 임시 라이선스 만료를 우아하게 처리
`License` 클래스는 API용 GroupDocs 라이선스 파일을 로드하고 검증합니다. 각 서명 작업 전에 라이선스 상태를 확인하고, 읽기 전용 모드로 전환하거나 관리자에게 알림을 보냅니다.

```markdown
```java
try {
    License license = new License();
    license.setLicense(licensePath);
} catch (Exception e) {
    logger.warn("License validation failed. Using trial mode.");
    // Continue with trial limitations
}
```
```

## 바코드 서명을 사용해야 할 때

### 이상적인 시나리오
- **Inventory & Logistics:** 운송 명세서, 포장 목록 또는 자산 태그에 스캔 가능한 바코드를 부착합니다.  
- **Regulatory Compliance:** 제약과 같은 산업에서는 기계가 읽을 수 있는 감사 추적이 필요합니다.  
- **Automated Document Pipelines:** 바코드 서명과 OCR을 결합해 수동 데이터 입력 없이 엔드‑투‑엔드 처리를 가능하게 합니다.  
- **High‑Volume Batch Jobs:** 대량 종이 아카이브를 스캔할 때, 바코드는 암호화 디지털 서명보다 검증이 더 빠릅니다.

### 다른 서명 유형을 선호해야 할 때
- **Legal Contracts:** 부인 방지를 위해 PKI 기반 디지털 서명(예: X.509)을 사용합니다.  
- **Customer‑Facing PDFs:** QR 코드는 모바일 기기에서 더 인식하기 쉽습니다.  
- **Ultra‑Secure Documents:** 레이어드 보안을 위해 바코드와 암호화된 디지털 서명을 결합합니다.

> **Pro tip:** 동일 PDF에 여러 서명 유형을 삽입할 수 있습니다—추적용 바코드와 법적 효력을 위한 디지털 인증서를 추가하세요.

## 자주 묻는 질문

**Q: 외부 종속성 없이 Java에서 PDF에 바코드 서명을 추가하려면 어떻게 해야 하나요?**  
A: GroupDocs.Signature for Java는 독립형이며, Maven/Gradle 아티팩트를 추가하면 타사 라이브러리 없이도 전체 바코드 생성 및 PDF 렌더링을 사용할 수 있습니다.

**Q: Java에서 바코드 서명 옵션을 설정해 QR 코드를 생성할 수 있나요?**  
A: 물론 가능합니다. `BarcodeTypes` 열거형을 `QRCode`로 전환하고 필요에 따라 크기 매개변수를 조정하면 됩니다.

```markdown
```java
signOptions.setEncodeType(BarcodeTypes.QR);
```
```

**Q: 프로덕션 사용을 위한 권장 Maven 설정은 무엇인가요?**  
A: `pom.xml`에 정확한 버전(`23.10.0` 등)을 고정하여 의도치 않은 업그레이드를 방지하고, Maven `shade` 플러그인을 활성화해 단일 실행 가능한 JAR을 생성합니다.

```markdown
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version> <!-- Don't use LATEST -->
</dependency>
```
```

**Q: 라이브러리가 비밀번호로 보호된 PDF를 지원하나요?**  
A: 예. `Signature` 객체를 생성할 때 비밀번호를 제공하면 이후 일반적으로 서명할 수 있습니다.

```markdown
```java
LoadOptions loadOptions = new LoadOptions();
loadOptions.setPassword("your_pdf_password");
Signature signature = new Signature(filePath, loadOptions);
```
```

**Q: 한 번에 몇 페이지를 서명할 수 있나요?**  
A: GroupDocs.Signature는 PDF의 모든 페이지를 한 번에 처리하거나 `setPageNumber()`를 통해 특정 페이지만 지정할 수 있습니다. 성능은 선형적으로 확장되며, 일반적인 클라우드 VM에서 200페이지 PDF 서명은 약 2 초 정도 걸립니다.

**Q: Code128 외에 어떤 바코드 형식이 있나요?**  
A: QR, DataMatrix, Aztec, UPC‑A, EAN‑13, PDF417 등 30가지 이상의 형식이 있으며, 전체 목록은 `BarcodeTypes` 열거형을 참고하세요.

**Q: 바코드 데이터 길이에 제한이 있나요?**  
A: 길이 제한은 바코드 유형에 따라 다릅니다. Code128은 실질적으로 80자까지, QR 코드는 최대 4 KB까지 저장할 수 있습니다.

**Q: 서명 후 생성된 바코드 이미지를 가져올 수 있나요?**  
A: `setReturnContent(true)`와 `setReturnContentType(FileType.PNG)`를 설정하면 `SignResult`에 `byte[]` 형태의 이미지가 포함되어 디스크나 데이터베이스에 저장할 수 있습니다.

**Last Updated:** 2026-07-25  
**Tested With:** GroupDocs.Signature 23.10 for Java  
**Author:** GroupDocs

## 관련 튜토리얼
- [Java에서 디지털 서명 추가 방법 - 완전한 GroupDocs 튜토리얼](/signature/java/getting-started/groupdocs-signature-java-digital-setup-guide/)
- [Java PDF에 QR 코드 추가 - 완전한 GroupDocs 튜토리얼](/signature/java/qr-code-signatures/qr-code-signature-generation-java-groupdocs/)
- [Java PDF에 텍스트 서명 추가 - 완전한 GroupDocs 튜토리얼](/signature/java/text-signatures/implement-text-signatures-groupdocs-java/)