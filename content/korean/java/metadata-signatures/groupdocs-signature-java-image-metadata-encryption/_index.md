---
"date": "2025-05-08"
"description": "GroupDocs.Signature for Java를 사용하여 암호화를 통해 이미지 메타데이터를 보호하는 방법을 알아보세요. 단계별 안내를 통해 데이터 무결성과 신뢰성을 확보하세요."
"title": "GroupDocs.Signature를 사용하여 Java로 이미지 메타데이터 서명 및 암호화 구현"
"url": "/ko/java/metadata-signatures/groupdocs-signature-java-image-metadata-encryption/"
"weight": 1
---

# GroupDocs.Signature를 사용하여 Java에서 암호화를 통한 이미지 메타데이터 서명 구현

## 소개

오늘날의 디지털 환경에서는 문서 메타데이터 내의 민감한 정보를 보호하는 것이 무엇보다 중요합니다. 기밀 비즈니스 계약서든 개인 식별 사진이든, 이미지 메타데이터의 무결성과 신뢰성을 유지하면 무단 접근 및 변조를 방지하는 데 도움이 됩니다. **Java용 GroupDocs.Signature** 이미지 메타데이터를 안전하게 서명하고 암호화하는 강력한 솔루션을 제공합니다.

이 튜토리얼에서는 GroupDocs.Signature의 강력한 기능을 활용하여 Java에서 암호화된 이미지 메타데이터 서명을 구현하는 방법을 안내합니다. 다음 단계를 따라 하면 이 기능을 Java 애플리케이션에 효과적으로 통합할 수 있습니다.

**배울 내용:**
- Java용 GroupDocs.Signature를 사용하여 문서 메타데이터 서명
- 암호화를 통한 사용자 정의 객체 서명 구현
- 대칭 키 암호화를 사용하여 보안 환경 설정

## 필수 조건

시작하기 전에 다음 전제 조건이 충족되었는지 확인하세요.

### 필수 라이브러리 및 종속성:
- **Java용 GroupDocs.Signature**: 버전 23.12 이상인지 확인하세요.

### 환경 설정 요구 사항:
- 컴퓨터에 Java Development Kit(JDK)를 설치합니다.
- IntelliJ IDEA, Eclipse 또는 NetBeans와 같은 통합 개발 환경(IDE)을 사용하세요.

### 지식 전제 조건:
- Java 프로그래밍에 대한 기본적인 이해.
- 종속성 관리를 위해 Maven이나 Gradle을 잘 알고 있어야 합니다.

## Java용 GroupDocs.Signature 설정

프로젝트에서 GroupDocs.Signature를 사용하려면 다음과 같이 필요한 종속성을 포함하세요.

### Maven 사용
이것을 당신의 것에 추가하세요 `pom.xml` 파일:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle 사용하기
이것을 당신의 것에 포함시키세요 `build.gradle` 파일:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### 직접 다운로드
또는 다음에서 최신 버전을 다운로드하세요. [Java 릴리스용 GroupDocs.Signature](https://releases.groupdocs.com/signature/java/).

#### 라이센스 취득 단계
- **무료 체험**: 기능을 탐색하기 위해 체험판을 시작합니다.
- **임시 면허**: 필요한 경우 광범위한 테스트를 신청하세요.
- **구입**: 생산용으로 사용하기 위한 라이센스를 취득합니다. [그룹닥스](https://purchase.groupdocs.com/buy).

## 기본 초기화 및 설정

Java 애플리케이션에서 GroupDocs.Signature를 초기화하는 방법은 다음과 같습니다.

```java
import com.groupdocs.signature.Signature;

public class InitializeSignature {
    public static void main(String[] args) {
        // 문서 경로
        String filePath = "path/to/your/document.jpg";
        
        // Signature의 새 인스턴스를 만듭니다.
        Signature signature = new Signature(filePath);

        System.out.println("GroupDocs.Signature initialized successfully.");
    }
}
```

## 구현 가이드

### 기능: 사용자 정의 객체를 사용한 메타데이터 서명

#### 개요
이 기능을 사용하면 사용자 정의 개체를 사용하여 이미지 메타데이터에 서명하고 암호화하여 보안을 강화할 수 있으며, 권한이 있는 당사자만 메타데이터에 액세스하거나 수정할 수 있습니다.

#### 단계별 구현

##### 1. 문서 서명 데이터 클래스 정의
메타데이터 정보를 보관할 클래스를 만듭니다.

```java
import java.math.BigDecimal;
import java.util.Date;

class DocumentSignatureData {
    private String ID;
    private String Author;
    private Date Signed = new Date();
    private BigDecimal DataFactor = new BigDecimal(0.01);

    public String getID() { return ID; }
    public void setID(String value) { ID = value; }

    @FormatAttribute(propertyName = "SignID")
    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }

    @FormatAttribute(propertyName = "SAuth")
    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }

    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```

##### 2. 서명 논리 구현
암호화를 사용하여 메타데이터에 서명하는 방법은 다음과 같습니다.

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
import com.groupdocs.signature.domain.signatures.metadata.ImageMetadataSignature;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.MetadataSignOptions;

import java.io.File;
import java.nio.file.Paths;
import java.util.UUID;

public class SignMetadataWithCustomObject {
    // 플레이스홀더로 파일 경로 초기화
    String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleImage.jpg";
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", 
                                       "SignedImageWithCustomMetadata/SampleImage_signed.jpg").getPath();

    public void run() throws Exception {
        Signature signature = new Signature(filePath);

        // 암호화를 위한 키와 암호문구를 설정하세요
        String key = "1234567890";
        String salt = "1234567890";
        IDataEncryption encryption = new SymmetricEncryption(
            SymmetricAlgorithmType.Rijndael, key, salt);

        MetadataSignOptions options = new MetadataSignOptions();
        DocumentSignatureData documentSignature = new DocumentSignatureData();
        
        // 사용자 정의 메타데이터 속성 설정
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME"));
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        ImageMetadataSignature mdDocument = new ImageMetadataSignature(41996, documentSignature);
        mdDocument.setDataEncryption(encryption);

        // 옵션에 메타데이터 서명 추가
        options.getSignatures().add(mdDocument);

        signature.sign(outputFilePath, options);
    }
}
```

#### 주요 구성 옵션
- **대칭 암호화**: 암호화를 위해 Rijndael 알고리즘을 활용합니다.
- **메타데이터 서명 옵션**: 서명 프로세스를 구성하고 서명할 메타데이터를 지정합니다.

##### 문제 해결 팁
- 파일 경로가 올바르고 접근 가능한지 확인하세요.
- 환경 변수를 확인하세요 `USERNAME` 올바르게 설정되었습니다.
- GroupDocs.Signature 라이브러리 버전이 코드 종속성과 일치하는지 확인하세요.

### 기능: 암호화를 포함한 메타데이터 서명

#### 개요
이 기능은 이미지 파일 내의 민감한 정보를 보호하기 위해 메타데이터 서명을 암호화하는 데 중점을 둡니다.

#### 단계별 구현
##### 1. 암호화 논리 구현
암호화를 사용하여 메타데이터에 서명하는 방법은 다음과 같습니다.
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.MetadataSignOptions;

import java.io.File;
import java.nio.file.Paths;
import java.util.UUID;

public class SignMetadataWithEncryption {
    // 플레이스홀더로 파일 경로 초기화
    String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleImage.jpg";
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", 
                                       "SignedImageWithEncryption/SampleImage_signed.jpg").getPath();

    public void run() throws Exception {
        Signature signature = new Signature(filePath);

        // 암호화를 위한 키와 암호문구를 설정하세요
        String key = "1234567890";
        String salt = "1234567890";
        IDataEncryption encryption = new SymmetricEncryption(
            SymmetricAlgorithmType.Rijndael, key, salt);

        MetadataSignOptions options = new MetadataSignOptions();
        DocumentSignatureData documentSignature = new DocumentSignatureData();
        
        // 사용자 정의 메타데이터 속성 설정
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME"));
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        ImageMetadataSignature mdDocument = new ImageMetadataSignature(41996, documentSignature);
        mdDocument.setDataEncryption(encryption);

        // 옵션에 메타데이터 서명 추가
        options.getSignatures().add(mdDocument);

        signature.sign(outputFilePath, options);
    }
}
```