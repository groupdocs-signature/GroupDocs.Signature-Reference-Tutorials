---
"date": "2025-05-08"
"description": "GroupDocs.Signature를 사용하여 Java에서 안전하고 동적인 QR 코드 서명을 생성하는 방법을 알아보세요. 문서 서명을 간편하게 간소화하세요."
"title": "GroupDocs.Signature for Java를 사용하여 QR 코드 서명 생성하기&#58; 종합 가이드"
"url": "/ko/java/qr-code-signatures/generate-qr-code-signatures-groupdocs-java/"
"weight": 1
---

# Java용 GroupDocs.Signature를 사용하여 QR 코드 서명 생성

## 소개

오늘날의 디지털 시대에는 문서 보안이 무엇보다 중요합니다. 계약서, 송장, 합의서 등 어떤 문서를 다루든 정확하고 안전한 서명을 확보하는 것은 어려울 수 있습니다. **Java용 GroupDocs.Signature** 문서에 디지털 서명을 추가하는 작업을 간소화하는 강력한 솔루션을 제공합니다.

이 튜토리얼에서는 Java용 GroupDocs.Signature를 사용하여 QR 코드 서명을 생성하는 방법을 안내합니다. 이를 통해 문서에 추가 데이터를 삽입할 때 보안과 유연성을 모두 향상시킬 수 있습니다. 다음 내용을 학습하게 됩니다.

- Java용 GroupDocs.Signature 설정 및 구성.
- 정확한 정렬 설정을 통해 QR 코드 서명을 생성하는 기술입니다.
- 서명된 문서를 포괄적으로 볼 수 있도록 서명 미리 보기 옵션을 구성합니다.
- 원활한 파일 처리를 보장하기 위해 서명 스트림을 생성합니다.

Java 애플리케이션에서 이러한 기능을 구현하는 방법을 자세히 살펴보겠습니다. 먼저, 원활하게 시작하기 위한 몇 가지 전제 조건을 살펴보겠습니다.

## 필수 조건

Java용 GroupDocs.Signature를 사용하기 전에 다음 요구 사항을 충족하는지 확인하세요.

- **라이브러리 및 종속성**: 필요한 라이브러리를 설치합니다. Maven이나 Gradle을 사용하여 종속성을 관리합니다.
  
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

- **환경 설정**JDK와 IntelliJ IDEA 또는 Eclipse와 같은 IDE를 갖춘 Java 개발 환경이 있는지 확인하세요.

- **지식 전제 조건**: Java 프로그래밍 개념에 대한 친숙함이 필수적이며, 디지털 서명에 대한 이해도 필요합니다.

다음으로, 프로젝트 환경에서 Java용 GroupDocs.Signature를 설정하는 방법을 안내해 드리겠습니다.

## Java용 GroupDocs.Signature 설정

Java용 GroupDocs.Signature를 사용하려면 다음 단계를 따르세요.

1. **종속성 추가**: 위에 표시된 대로 Maven이나 Gradle을 사용하여 종속성을 포함합니다.
2. **라이센스 취득**:
   - 무료 평가판을 다운로드하여 시작하세요. [GroupDocs 릴리스](https://releases.groupdocs.com/signature/java/).
   - 장기 사용을 위해서는 라이센스 구매 또는 임시 라이센스 신청을 고려해 보세요. [구매 페이지](https://purchase.groupdocs.com/buy).
3. **기본 초기화**:
   Java 애플리케이션에서 라이브러리를 초기화하여 해당 기능을 사용해보세요.

   ```java
   import com.groupdocs.signature.Signature;
   
   // Signature 객체 초기화
   Signature signature = new Signature("sample.pdf");
   ```

Java용 GroupDocs.Signature를 구성했으니 QR 코드 서명을 생성할 준비가 되었습니다. 자세한 내용을 살펴보겠습니다.

## 구현 가이드

### QR 코드 서명 생성

QR 코드 서명을 만드는 데는 몇 가지 주요 단계가 필요합니다. 각 단계는 문서에 데이터가 삽입되고 표시되는 방식을 사용자 지정하는 데 도움이 됩니다.

#### 개요
QR 코드 서명은 다재다능하여 주소, URL 또는 이진 데이터와 같은 복잡한 정보를 문서에 직접 삽입할 수 있습니다. Java용 GroupDocs.Signature를 사용하여 특정 정렬 설정을 적용한 서명을 생성하는 방법을 살펴보겠습니다.

#### 단계별 구현

##### 1. QR 코드 옵션 구성
설정으로 시작하세요 `QrCodeSignOptions` 객체입니다. 여기에서 QR 코드의 유형과 포함할 데이터를 지정합니다.

```java
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.extensions.serialization.Address;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

QrCodeSignOptions signOptions = new QrCodeSignOptions();
signOptions.setEncodeType(QrCodeTypes.QR);

// Address 객체를 사용하여 데이터 설정
Address address = new Address();
address.setStreet("221B Baker Street");
address.setCity("London");
address.setState("NW");
address.setZIP("NW16XE");
address.setCountry("England");

signOptions.setData(address);
```
**설명**: 여기서는 QR코드 유형을 표준으로 설정합니다. `QR` 주소 정보를 입력하세요. 이러한 데이터 캡슐화를 통해 문서 내에서 중요한 세부 정보를 쉽게 확인할 수 있습니다.

##### 2. QR 코드 정렬
QR 코드가 문서 페이지에 나타나는 위치를 제어하려면 정렬 설정을 조정하세요.

```java
signOptions.setHorizontalAlignment(HorizontalAlignment.Left);
signOptions.setVerticalAlignment(VerticalAlignment.Center);
signOptions.setWidth(100);
signOptions.setHeight(100);
```
**설명**: 정렬 옵션 (`HorizontalAlignment` 그리고 `VerticalAlignment`) QR 코드를 정확하게 배치할 수 있습니다. 이 단계를 통해 QR 코드가 보기에도 좋고, 최적의 스캔을 위해 전략적으로 배치됩니다.

##### 3. 여백 설정
QR 코드 주위에 여백을 정의하여 스캔 안정성을 위해 중요할 수 있는 문서 가장자리에 코드가 닿지 않도록 하세요.

```java
signOptions.setMargin(new Padding(10));
```
**설명**: 여백은 다음을 사용하여 설정됩니다. `Padding`QR 코드와 문서 가장자리 사이에 공간을 확보하여 스캔성을 향상시킵니다.

### 서명 미리 보기 옵션 구성

미리보기 옵션을 설정하면 서명을 완성하기 전에 어떻게 보일지 미리 볼 수 있습니다. 방법은 다음과 같습니다.

#### 개요
미리 보기 설정은 문서 내에서 서명이 어떻게 표시되는지 확인하는 데 중요합니다.

#### 단계별 구현

##### 1. PreviewOptions 생성 및 구성
활용하다 `PreviewSignatureOptions` 서명을 미리 보는 방법을 정의합니다.

```java
import com.groupdocs.signature.options.PreviewSignatureOptions;
import com.groupdocs.signature.options.preview.PreviewFormats;
import java.util.UUID;

PreviewSignatureOptions previewOption = new PreviewSignatureOptions(signOptions);
previewOption.setSignatureId(UUID.randomUUID().toString());
previewOption.setPreviewFormat(PreviewFormats.JPEG);
```
**설명**: 그 `PreviewSignatureOptions` 객체는 QR 코드의 JPEG 미리보기를 생성하도록 구성됩니다. 각 서명에 대한 고유 식별자(`UUID`)을 통해 여러 서명을 효율적으로 추적하고 관리할 수 있습니다.

### 서명 스트림 생성

스트림을 생성하면 서명된 문서가 제대로 저장되거나 전송됩니다.

#### 개요
파일 스트림을 생성하면 서명된 문서를 원활하게 처리할 수 있으며, 지정된 디렉토리에 올바르게 저장되도록 할 수 있습니다.

#### 단계별 구현

##### 1. 출력 디렉토리 정의 및 스트림 생성
파일 쓰기 중 오류를 방지하려면 스트림을 생성하기 전에 출력 디렉토리가 있는지 확인하세요.

```java
import java.io.FileOutputStream;
import java.io.OutputStream;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

public OutputStream generateSignatureStream(PreviewSignatureOptions previewOptions) {
    try {
        Path path = Paths.get("YOUR_OUTPUT_DIRECTORY");
        if (!Files.exists(path)) {
            Files.createDirectories(path);
        }
        
        // 서명된 문서를 저장하기 위한 출력 스트림을 생성합니다.
        return new FileOutputStream(path.resolve("signedDocument.pdf"));
    } catch (Exception e) {
        e.printStackTrace();
        return null;
    }
}
```
**설명**이 메서드는 지정된 디렉터리가 있는지 확인하고 필요한 경우 디렉터리를 생성한 다음, 문서를 저장하기 위한 파일 출력 스트림을 반환합니다. 디렉터리를 처리하면 서명된 문서가 체계적으로 저장됩니다.

## 결론

이 가이드를 따라 GroupDocs.Signature for Java를 사용하여 QR 코드 서명을 생성하는 방법을 익혔습니다. 이를 통해 문서에 추가 데이터를 삽입할 때 보안과 유연성을 모두 향상시킬 수 있습니다. 이러한 단계를 통해 Java 애플리케이션에서 디지털 서명 기능을 안전하게 구현할 수 있습니다.

더 자세히 알아보려면 다양한 유형의 서명을 실험하거나 Java용 GroupDocs.Signature가 제공하는 다른 기능을 살펴보세요.