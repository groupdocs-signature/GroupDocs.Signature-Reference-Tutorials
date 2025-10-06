---
"date": "2025-05-08"
"description": "GroupDocs.Signature for Java를 사용하여 QR 코드 암호화와 디지털 서명을 사용하여 PDF를 보호하는 방법을 알아보세요. 문서 보안을 효과적으로 강화하세요."
"title": "GroupDocs.Signature를 사용하여 Java에서 QR 코드 암호화를 통한 보안 PDF 서명 구현"
"url": "/ko/java/qr-code-signatures/secure-pdf-signing-qr-code-groupdocs-java/"
"weight": 1
type: docs
---
# GroupDocs.Signature를 사용하여 Java에서 QR 코드 암호화를 통한 보안 PDF 서명을 구현하는 방법

오늘날 디지털 시대에는 문서에 담긴 민감한 정보를 보호하는 것이 무엇보다 중요합니다. 사이버 위협의 증가로 인해 데이터 암호화는 문서 관리의 필수적인 부분이 되었습니다. 이 튜토리얼에서는 GroupDocs.Signature for Java를 사용하여 QR 코드 암호화를 활용한 안전한 PDF 서명을 구현하는 방법을 안내합니다. 이 튜토리얼을 마치면 강력한 보안 기능을 애플리케이션에 통합할 수 있는 역량을 갖추게 될 것입니다.

## 배울 내용:
- Java에서 대칭 데이터 암호화 이해하기
- 사용자 정의 서명 클래스 만들기
- 사용자 정의 데이터 및 정렬을 사용하여 QR 코드 서명 구성
- 안전한 PDF 서명을 위한 GroupDocs.Signature 통합

뛰어들 준비되셨나요? 시작해 볼까요!

## 필수 조건
시작하기에 앞서 다음 사항이 있는지 확인하세요.
- **자바 개발 키트(JDK):** 버전 8 이상.
- **Maven 또는 Gradle:** 종속성 관리를 위해 프로젝트 설정에 따라 선택하세요.
- **자바 프로그래밍에 대한 지식:** Java에서의 객체 지향 프로그래밍에 대한 기본적인 이해.

## Java용 GroupDocs.Signature 설정
GroupDocs.Signature를 사용하려면 프로젝트에 종속성으로 추가해야 합니다. 이 라이브러리는 디지털 서명 및 문서 암호화를 관리하는 강력한 도구를 제공합니다.

### Maven 설정
다음 종속성을 추가하세요. `pom.xml` 파일:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle 설정
Gradle 사용자의 경우 다음을 포함합니다. `build.gradle` 파일:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### 직접 다운로드
또는 다음에서 최신 버전을 다운로드하세요. [Java 릴리스용 GroupDocs.Signature](https://releases.groupdocs.com/signature/java/).

### 라이센스 취득
GroupDocs.Signature의 무료 체험판을 통해 기능을 평가해 보세요. 장기간 사용하려면 라이선스를 구매하거나 웹사이트를 통해 임시 라이선스를 신청하는 것이 좋습니다.

## 구현 가이드
이 가이드는 데이터 암호화, 사용자 정의 서명 생성, QR 코드 서명 구성 등을 다루는 주요 섹션으로 구분되어 있습니다.

### 대칭 알고리즘을 사용한 데이터 암호화
데이터를 암호화하면 전송 및 저장 중에도 안전하게 보호됩니다. GroupDocs.Signature를 사용하여 대칭 암호화를 설정하는 방법은 다음과 같습니다.

#### 대칭 암호화 설정
1. **필수 패키지 가져오기:**
   ```java
   import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
   ```
2. **암호화 객체를 초기화합니다.**
   암호화를 위해 안전한 키와 솔트를 사용하세요. `"YOUR_SECURE_KEY"` 본인의 열쇠로.
   ```java
   String key = "YOUR_SECURE_KEY";
   String salt = "YOUR_SECURE_SALT";

   IDataEncryption encryption = new SymmetricEncryption(
       SymmetricAlgorithmType.Rijndael, 
       key, 
       salt
   );
   ```
   - **SymmetricAlgorithmType.Rijndael:** 이는 사용할 대칭 알고리즘의 유형을 지정합니다.
   - **키와 솔트:** 귀하의 애플리케이션에 맞게 고유하고 안전한지 확인하세요.

### 사용자 정의 데이터 서명 클래스
사용자 지정 클래스를 만들면 시그니처 속성을 효과적으로 관리할 수 있습니다. 방법은 다음과 같습니다.

#### 정의 `DocumentSignatureData` 수업
```java
class DocumentSignatureData {
    private String ID;
    private String Author;
    private Date Signed = new Date();
    private BigDecimal DataFactor = new BigDecimal(0.01);

    public String getID() { return ID; }
    public void setID(String value) { ID = value; }

    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }

    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }

    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```
- **신분증, 저자, 서명:** 이러한 필드는 서명의 메타데이터를 저장합니다.
- **데이터 팩터:** 애플리케이션의 논리와 관련된 숫자 값을 보관합니다.

### QR 코드 서명 옵션
QR 코드는 정보를 간편하게 삽입할 수 있는 방법입니다. 사용자 지정 데이터 및 암호화를 설정하세요.

#### QR 코드 서명 설정
1. **초기화 `Signature` 물체:**
   ```java
   import com.groupdocs.signature.Signature;
   
   Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY");
   ```
2. **QR 코드 옵션 구성:**
   ```java
   import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
   import com.groupdocs.signature.options.sign.QrCodeSignOptions;
   import java.util.UUID;

   DocumentSignatureData documentSignature = new DocumentSignatureData();
   documentSignature.setID(UUID.randomUUID().toString());
   documentSignature.setAuthor(System.getenv("USERNAME"));
   documentSignature.setDataFactor(new BigDecimal("11.22"));

   QrCodeSignOptions options = new QrCodeSignOptions();
   options.setData(documentSignature);
   options.setEncodeType(QrCodeTypes.QR);
   options.setDataEncryption(encryption); // 암호화 객체를 사용하세요
   options.setHeight(100);
   options.setWidth(100);
   options.setVerticalAlignment(com.groupdocs.signature.domain.enums.VerticalAlignment.Bottom);
   options.setHorizontalAlignment(com.groupdocs.signature.domain.enums.HorizontalAlignment.Right);

   import com.groupdocs.signature.domain.Padding;
   Padding padding = new Padding();
   padding.setRight(10);
   padding.setBottom(10);
   options.setMargin(padding);
   ```
   - **인코딩 유형:** QR 코드 형식을 지정합니다.
   - **정렬 및 여백:** QR 코드가 문서에 표시되는 방식을 사용자 지정합니다.

### 사용 예
구성된 옵션으로 문서에 서명하려면:
```java
signature.sign("YOUR_OUTPUT_DIRECTORY/QRCodeEncryptedObject.pdf\