---
"date": "2025-05-08"
"description": "GroupDocs.Signature를 사용하여 Java QR 코드 서명을 구현하는 방법을 알아보세요. 문서 보안을 강화하고, 서명 옵션을 구성하고, Java 애플리케이션에 사용자 지정 암호화를 적용해 보세요."
"title": "Java QR 코드 서명 가이드&#58; GroupDocs.Signature로 문서 보안"
"url": "/ko/java/qr-code-signatures/java-qr-code-signing-groupdocs-signature/"
"weight": 1
---

# Java용 GroupDocs.Signature를 사용하여 Java QR 코드 서명 구현

## 소개

Java 애플리케이션에 QR 코드를 삽입하여 디지털 문서의 보안을 강화하세요. Java용 GroupDocs.Signature를 활용하면 문서의 진위성과 추적성을 효과적으로 보장할 수 있습니다. 이 가이드에서는 사용자 지정 데이터 서명 생성, QR 코드 서명 옵션 구성, 그리고 강력한 암호화를 통한 문서 보안 방법을 안내합니다.

**배울 내용:**
- GroupDocs.Signature를 사용하여 사용자 정의 데이터 서명 클래스를 만드는 방법
- Java 애플리케이션에서 QR 코드 서명 옵션 구성
- QR 코드로 문서 서명 및 사용자 정의 암호화 적용

필수 구성 요소를 살펴보고 이 기능을 프로젝트에 통합해 보겠습니다!

## 필수 조건

시작하기에 앞서, 개발 환경에 필요한 라이브러리와 종속성이 설정되어 있는지 확인하세요.

### 필수 라이브러리 및 버전

Java용 GroupDocs.Signature를 구현하려면 다음 종속성을 포함하세요.

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
implementation 'com.groupdocs:groupdocs-signation:23.12'
```

최신 버전을 다음에서 직접 다운로드할 수도 있습니다. [Java 릴리스용 GroupDocs.Signature](https://releases.groupdocs.com/signature/java/).

### 환경 설정 요구 사항

- 작동하는 Java Development Kit(JDK)가 설치되어 있는지 확인하세요.
- IntelliJ IDEA나 Eclipse와 같은 통합 개발 환경(IDE)을 설정합니다.

### 지식 전제 조건

- Java 프로그래밍과 객체 지향 개념에 대한 기본적인 이해가 있습니다.
- Maven이나 Gradle을 사용하여 종속성을 처리하는 데 익숙합니다.

## Java용 GroupDocs.Signature 설정

시작하려면 위의 설치 지침에 따라 프로젝트에 GroupDocs.Signature를 설정하고 빌드 구성에 포함하세요.

### 라이센스 취득 단계

GroupDocs는 다양한 라이선스 옵션을 제공합니다.
- **무료 체험**: 제한 없이 모든 기능을 테스트하세요.
- **임시 면허**: 평가 목적으로 라이센스를 얻으세요.
- **구입**: 상업적 사용을 위한 정식 라이센스를 취득하세요.

다운로드 후 GroupDocs.Signature를 다음과 같이 초기화합니다.

```java
import com.groupdocs.signature.Signature;

class InitializeGroupDocs {
    public static void main(String[] args) {
        Signature signature = new Signature("path/to/your/document");
        // 이제 서명 객체를 사용하여 문서 작업을 시작할 수 있습니다.
    }
}
```

## 구현 가이드

주요 기능에 초점을 맞춰 구현 과정을 관리 가능한 섹션으로 나누어 보겠습니다.

### 사용자 정의 데이터 서명 클래스

#### 개요
ID, 작성자, 서명 날짜 및 기타 요소와 같은 서명 데이터를 저장하는 사용자 지정 클래스를 만듭니다. 이렇게 하면 서명에 필요한 모든 메타데이터가 캡슐화됩니다.

#### 단계별 구현

**DocumentSignatureData 클래스 정의**

```java
import com.groupdocs.signature.domain.extensions.serialization.FormatAttribute;
import java.util.Date;
import java.math.BigDecimal;

class DocumentSignatureData {
    @FormatAttribute(propertyName = "SignID")
    public String ID; // 서명에 대한 고유 식별자
    
    public String getID() { return ID; }
    public void setID(String value) { ID = value; }
    
    @FormatAttribute(propertyName = "SAuth")
    public final String Author; // 문서 작성자
    
    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }
    
    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public final Date Signed = new Date(); // 서명 날짜 및 시간
    
    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }
    
    @FormatAttribute(propertyName = "SDFact", propertyFormat = "N2")
    public final BigDecimal DataFactor = new BigDecimal(0.01); // 서명을 위한 추가 데이터 요소
    
    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```

**설명:**
- **형식 속성**: 직렬화를 사용자 정의하기 위해 속성에 주석을 추가합니다.
- **속성**: 고유 ID, 작성자 이름, 서명 날짜, 데이터 요소와 같은 필수 세부 정보를 수집합니다.

### QR 코드 서명 옵션 구성

#### 개요
QR 코드 기호 옵션을 구성하여 크기, 정렬, 패딩 등 문서에 QR 코드가 표시되는 방식을 정의합니다.

#### 단계별 구현

**QrCodeSignOptionsConfig 클래스 정의**

```java
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

class QrCodeSignOptionsConfig {
    public static QrCodeSignOptions setupQrCodeSignOptions(DocumentSignatureData documentSignature) {
        QrCodeSignOptions options = new QrCodeSignOptions();
        
        // 사용자 정의 데이터 객체를 QR 코드로 직렬화합니다.
        options.setData(documentSignature);
        
        // QR 코드 유형을 지정하세요
        options.setEncodeType(QrCodeTypes.QR);
        
        // 정렬을 위한 패딩 구성
        Padding padding = new Padding();
        padding.setRight(10); // 픽셀 단위 오른쪽 패딩
        padding.setBottom(10); // 픽셀 단위의 하단 패딩
        options.setMargin(padding);
        
        // QR 코드의 크기와 위치 정의
        options.setHeight(100);
        options.setWidth(100);
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        options.setHorizontalAlignment(HorizontalAlignment.Right);
        
        return options;
    }
}
```

**설명:**
- **QR코드 서명 옵션**: QR 코드의 크기와 위치를 포함하여 QR 코드가 표시되는 방식을 관리합니다.
- **심**문서 내에서 정렬을 조정합니다.

### QR 코드 및 사용자 정의 암호화를 사용한 문서 서명

#### 개요
QR 코드와 맞춤형 암호화를 결합하여 문서에 안전하게 서명하세요. 이를 통해 데이터 무결성과 기밀성이 보장됩니다.

#### 단계별 구현

**QR 코드로 문서에 서명하기**

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.exception.GroupDocsSignatureException;

import java.util.UUID;

class SignDocumentWithQRCode {
    public static void signDocument(String filePath, String outputFilePath) throws Exception {
        try {
            Signature signature = new Signature(filePath);

            // 사용자 정의 XOR 암호화 전략
            IDataEncryption encryption = new CustomXOREncryption();

            // 사용자 정의 문서 서명 데이터 개체 구성
            DocumentSignatureData documentSignature = new DocumentSignatureData();
            documentSignature.setID(UUID.randomUUID().toString());
            documentSignature.setAuthor(System.getenv("USERNAME"));
            documentSignature.setSigned(new Date());
            documentSignature.setDataFactor(new BigDecimal("11.22"));

            // QR 코드 옵션 설정
            QrCodeSignOptions options = QrCodeSignOptionsConfig.setupQrCodeSignOptions(documentSignature);

            // QR 코드 내 데이터에 암호화 적용
            options.setDataEncryption(encryption);

            // 문서에 서명하고 저장하세요
            signature.sign(outputFilePath, options);
        } catch (Exception e) {
            throw new GroupDocsSignatureException(e.getMessage());
        }
    }
}
```

**설명:**
- **CustomXOREncryption**: QR 코드 데이터를 보호하기 위해 사용자 지정 암호화 전략을 구현합니다.
- **UUID**: 각 서명에 대한 고유 식별자를 생성합니다.