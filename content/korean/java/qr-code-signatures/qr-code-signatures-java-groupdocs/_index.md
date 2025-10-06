---
"date": "2025-05-08"
"description": "GroupDocs.Signature를 사용하여 Java로 QR 코드 서명을 구현하고 검증하여 문서 보안을 강화하는 방법을 알아보세요. 안전한 서명 프로세스를 위한 단계별 가이드를 따라해 보세요."
"title": "문서 보안&#58; GroupDocs.Signature를 사용하여 Java로 QR 코드 서명 구현"
"url": "/ko/java/qr-code-signatures/qr-code-signatures-java-groupdocs/"
"weight": 1
type: docs
---
# 문서 보안: GroupDocs.Signature를 사용하여 Java로 QR 코드 서명 구현

오늘날의 디지털 환경에서는 계약서, 송장 또는 민감한 개인 정보와 같은 문서의 보안을 유지하는 것이 매우 중요합니다. 문서 보안을 강화하고 검증 절차를 간소화하는 혁신적인 방법 중 하나는 QR 코드 서명을 사용하는 것입니다. 이 튜토리얼에서는 GroupDocs.Signature를 사용하여 Java에서 문서의 QR 코드 서명을 구현하고 검증하는 방법을 안내합니다.

## 당신이 배울 것
- QR 코드를 사용하여 문서에 서명하는 방법
- QR 코드를 사용하여 서명된 문서 확인
- 문서 내에서 기존 QR 코드 서명 검색
- 문서에서 QR 코드 서명 업데이트 및 삭제

환경을 설정하고 시작해 보세요!

### 필수 조건
시작하기 전에 다음 전제 조건이 충족되었는지 확인하세요.

#### 필수 라이브러리 및 종속성
Java용 GroupDocs.Signature가 필요합니다. Maven이나 Gradle을 통해 포함하거나 직접 다운로드할 수 있습니다.

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

**직접 다운로드**
최신 버전을 다운로드하세요 [Java 릴리스용 GroupDocs.Signature](https://releases.groupdocs.com/signature/java/).

#### 환경 설정 요구 사항
- Java Development Kit(JDK) 8 이상이 설치되어 있는지 확인하세요.
- IntelliJ IDEA, Eclipse 또는 NetBeans와 같은 IDE를 사용하세요.

#### 지식 전제 조건
Java 프로그래밍과 문서 처리에 대한 기본적인 이해가 도움이 됩니다.

## Java용 GroupDocs.Signature 설정
프로젝트에서 GroupDocs.Signature를 사용하려면 다음 단계를 따르세요.
1. **설치**: 설정에 따라 Maven, Gradle 또는 직접 다운로드 중에서 선택하세요.
2. **라이센스 취득**:
   - 무료 체험판을 이용해 시작하세요 [GroupDocs 웹사이트](https://releases.groupdocs.com/signature/java/).
   - 확장된 테스트 및 개발을 위해 임시 라이센스를 취득하는 것을 고려하십시오. [여기](https://purchase.groupdocs.com/temporary-license/).
3. **기본 초기화**: 
    GroupDocs.Signature를 초기화하는 방법은 다음과 같습니다.

    ```java
    Signature signature = new Signature("YOUR_DOCUMENT_PATH");
    ```

이를 통해 QR 코드 서명을 구현할 준비가 됩니다.

## 구현 가이드

### QR 코드 서명으로 문서에 서명
#### 개요
QR 코드를 사용하여 문서에 서명하려면 디지털 서명을 나타내는 고유 코드를 삽입해야 합니다. 이 과정을 통해 문서의 보안이 강화되고 나중에 진위 여부를 쉽게 확인할 수 있습니다.

##### 1단계: 서명 옵션 설정
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

Signature signature = new Signature("YOUR_DOCUMENT_PATH");
QrCodeSignOptions signOptions = new QrCodeSignOptions("John Smith", com.groupdocs.signature.domain.qrcodes.QrCodeTypes.QR);

signOptions.setVerticalAlignment(VerticalAlignment.Top);
signOptions.setHorizontalAlignment(HorizontalAlignment.Center);
signOptions.setWidth(100);
signOptions.setHeight(40);
```
**설명**: `QrCodeSignOptions` 특정 텍스트와 정렬을 사용하여 QR 코드를 생성하도록 구성되어 있습니다. 필요에 따라 너비와 높이를 조정하세요.

##### 2단계: 서명 모양 사용자 지정
```java
import java.awt.Color;

signOptions.setForeColor(Color.RED); // QR 코드 색상 설정
com.groupdocs.signature.domain.SignatureFont signatureFont = new com.groupdocs.signature.domain.SignatureFont();
signatureFont.setSize(12);
signatureFont.setFamilyName("Comic Sans MS");
signOptions.setFont(signatureFont);
```
**설명**: 글꼴과 색상을 사용자 지정하면 시각적 식별이 향상됩니다.

##### 3단계: 문서에 서명하기
```java
import java.util.ArrayList;
import java.util.List;

List<String> signatureIds = new ArrayList<>();
List<com.groupdocs.signature.domain.BaseSignature> signedSignatures = signature.sign("YOUR_OUTPUT_PATH", signOptions).getSucceeded();

for (com.groupdocs.signature.domain.BaseSignature temp : signedSignatures) {
    signatureIds.add(temp.getSignatureId());
}
```
**설명**: 이 단계에서는 문서에 서명하고 향후 참조를 위해 서명 ID를 저장합니다.

### QR 코드 서명으로 문서 확인
#### 개요
검증은 문서가 합법적으로 서명되었는지 확인하는 것입니다. 문서의 QR 코드 서명을 검증하는 방법은 다음과 같습니다.

##### 1단계: 확인 옵션 설정
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();

verifyOptions.setEncodeType(QrCodeTypes.QR);
verifyOptions.setText("John Smith"); // 확인 문자
verifyOptions.setAllPages(false); 
verifyOptions.setPageNumber(1);
```
**설명**검증 옵션은 어떤 QR 코드 유형과 텍스트를 찾아야 하는지 지정하여 서명이 기대에 부합하는지 확인합니다.

##### 2단계: 검증 수행
```java
boolean isValid = signature2.verify(verifyOptions).isValid();
System.out.println("Is Signature Valid? " + isValid);
```
**설명**: 이는 해당 문서에 기준에 맞는 유효한 QR 코드가 포함되어 있는지 확인합니다.

### QR 코드 서명을 위한 문서 검색
#### 개요
문서 내에서 기존 서명을 찾는 것이 필요할 때가 있습니다. GroupDocs.Signature를 사용하여 서명을 검색하는 방법은 다음과 같습니다.

##### 1단계: 검색 옵션 구성
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import com.groupdocs.signature.options.search.QrCodeSearchOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeSearchOptions searchOptions = new QrCodeSearchOptions();
searchOptions.setAllPages(true);
```
**설명**: 이렇게 하면 모든 페이지에서 QR 코드 서명을 스캔하는 도구가 설정됩니다.

##### 2단계: 검색 실행
```java
List<QrCodeSignature> signatures = signature2.search(QrCodeSignature.class, searchOptions);

for (QrCodeSignature qrSignature : signatures) {
    System.out.println("Found Signature ID: " + qrSignature.getSignatureId());
}
```
**설명**: 문서에서 발견된 모든 QR 코드 서명을 검색합니다.

### 문서 업데이트 QR 코드 서명
#### 개요
서명을 업데이트하려면 위치나 크기와 같은 속성을 변경해야 합니다. 방법은 다음과 같습니다.

##### 1단계: 업데이트를 위한 서명 준비
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.io.ByteArrayOutputStream;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
List<QrCodeSignature> signaturesToUpdate = new ArrayList<>();

// 'signatures'가 검색을 통해 얻은 QrCodeSignature 객체의 목록이라고 가정합니다.
for (QrCodeSignature qrSignature : signatures) {
    qrSignature.setLeft(qrSignature.getLeft() + 100);
    qrSignature.setTop(qrSignature.getTop() + 100);
    qrSignature.setWidth(200);
    qrSignature.setHeight(50);
    signaturesToUpdate.add(qrSignature);
}
```
**설명**: 각 서명의 위치와 크기를 조정합니다.

##### 2단계: 문서 업데이트
```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature2.update(outputStream, signaturesToUpdate);
```
**설명**: 이 문서는 수정된 QR 코드 서명으로 업데이트되었습니다.

### ID로 문서 QR 코드 서명 삭제
#### 개요
더 이상 필요하지 않거나 실수로 추가된 서명은 삭제해야 할 수 있습니다. 고유 ID를 사용하여 서명을 삭제하는 방법은 다음과 같습니다.

##### 1단계: 삭제할 서명 식별
```java
import com.groupdocs.signature.domain.SignatureCollection;
import java.util.Arrays;

SignatureCollection signaturesToDelete = signature2.search(QrCodeSignature.class);
Arrays.stream(signaturesToDelete).forEach(signature -> {
    if (signature.getSignatureId().equals("YOUR_SIGNATURE_ID")) {
        signature.delete();
    }
});
```
**설명**: 고유 ID로 QR 코드 서명을 찾아 삭제합니다.

## 결론
이 가이드에서는 GroupDocs.Signature를 사용하여 Java에서 QR 코드 서명을 사용하여 문서를 보호하는 방법을 안내했습니다. 다음 단계를 따라 문서가 안전하게 서명되었는지 확인하고 진위 여부를 쉽게 확인할 수 있습니다.