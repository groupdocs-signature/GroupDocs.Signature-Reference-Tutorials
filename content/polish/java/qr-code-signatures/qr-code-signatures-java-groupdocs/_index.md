---
"date": "2025-05-08"
"description": "Dowiedz się, jak zwiększyć bezpieczeństwo dokumentów, wdrażając i weryfikując podpisy kodem QR w Javie za pomocą GroupDocs.Signature. Postępuj zgodnie z tym przewodnikiem krok po kroku, aby zapewnić bezpieczny proces podpisywania."
"title": "Zabezpiecz swoje dokumenty i wdróż podpisy kodem QR w Javie, używając GroupDocs.Signature"
"url": "/pl/java/qr-code-signatures/qr-code-signatures-java-groupdocs/"
"weight": 1
---

# Zabezpiecz swoje dokumenty: Wdrażaj podpisy kodem QR w Javie za pomocą GroupDocs.Signature

dzisiejszym cyfrowym świecie zapewnienie bezpieczeństwa dokumentów, takich jak umowy, faktury czy poufne dane osobowe, jest kluczowe. Jednym z innowacyjnych sposobów na zwiększenie bezpieczeństwa dokumentów i uproszczenie procesów weryfikacji jest użycie podpisów QR. Ten samouczek przeprowadzi Cię przez proces wdrażania i weryfikacji podpisów QR w dokumentach w Javie za pomocą GroupDocs.Signature.

## Czego się nauczysz
- Jak podpisywać dokumenty za pomocą kodów QR
- Weryfikacja podpisanych dokumentów za pomocą kodów QR
- Wyszukiwanie istniejących podpisów w postaci kodu QR w dokumencie
- Aktualizowanie i usuwanie podpisów w postaci kodów QR z dokumentów

Skonfigurujmy Twoje środowisko i zacznijmy!

### Wymagania wstępne
Przed rozpoczęciem upewnij się, że spełnione są następujące wymagania wstępne:

#### Wymagane biblioteki i zależności
Będziesz potrzebować GroupDocs.Signature dla Javy. Możesz go dodać za pomocą Mavena lub Gradle albo pobrać bezpośrednio.

**Maven**
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle**
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Bezpośrednie pobieranie**
Pobierz najnowszą wersję z [GroupDocs.Signature dla wydań Java](https://releases.groupdocs.com/signature/java/).

#### Wymagania dotyczące konfiguracji środowiska
- Upewnij się, że masz zainstalowany Java Development Kit (JDK) 8 lub nowszy.
- Użyj środowiska IDE, takiego jak IntelliJ IDEA, Eclipse lub NetBeans.

#### Wymagania wstępne dotyczące wiedzy
Przydatna będzie podstawowa znajomość programowania w Javie i przetwarzania dokumentów.

## Konfigurowanie GroupDocs.Signature dla języka Java
Aby użyć GroupDocs.Signature w swoim projekcie, wykonaj następujące kroki:
1. **Instalacja**: Wybierz pomiędzy Maven, Gradle lub bezpośrednim pobraniem, w zależności od konfiguracji.
2. **Nabycie licencji**:
   - Zacznij od bezpłatnego okresu próbnego dostępnego na [Strona internetowa GroupDocs](https://releases.groupdocs.com/signature/java/).
   - Rozważ uzyskanie tymczasowej licencji na rozszerzone testowanie i rozwój od [Tutaj](https://purchase.groupdocs.com/temporary-license/).
3. **Podstawowa inicjalizacja**: 
    Oto jak zainicjować GroupDocs.Signature:

    ```java
    Signature signature = new Signature("YOUR_DOCUMENT_PATH");
    ```

Przygotowuje to do wdrożenia podpisów za pomocą kodów QR.

## Przewodnik wdrażania

### Podpisz dokument za pomocą kodu QR
#### Przegląd
Podpisanie dokumentu za pomocą kodu QR polega na wklejeniu unikalnego kodu, który reprezentuje Twój podpis cyfrowy. Ten proces zabezpiecza dokument i umożliwia łatwą weryfikację jego autentyczności w późniejszym czasie.

##### Krok 1: Skonfiguruj opcje podpisywania
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
**Wyjaśnienie**: `QrCodeSignOptions` jest skonfigurowany do tworzenia kodu QR z określonym tekstem i wyrównaniem. Dostosuj szerokość i wysokość w razie potrzeby.

##### Krok 2: Dostosuj wygląd podpisu
```java
import java.awt.Color;

signOptions.setForeColor(Color.RED); // Ustaw kolor kodu QR
com.groupdocs.signature.domain.SignatureFont signatureFont = new com.groupdocs.signature.domain.SignatureFont();
signatureFont.setSize(12);
signatureFont.setFamilyName("Comic Sans MS");
signOptions.setFont(signatureFont);
```
**Wyjaśnienie**:Dostosowanie czcionki i koloru poprawia identyfikację wizualną.

##### Krok 3: Podpisz dokument
```java
import java.util.ArrayList;
import java.util.List;

List<String> signatureIds = new ArrayList<>();
List<com.groupdocs.signature.domain.BaseSignature> signedSignatures = signature.sign("YOUR_OUTPUT_PATH", signOptions).getSucceeded();

for (com.groupdocs.signature.domain.BaseSignature temp : signedSignatures) {
    signatureIds.add(temp.getSignatureId());
}
```
**Wyjaśnienie**:Ten krok powoduje podpisanie dokumentu i zapisanie identyfikatorów podpisu do wykorzystania w przyszłości.

### Zweryfikuj dokument za pomocą podpisu z kodem QR
#### Przegląd
Weryfikacja gwarantuje, że dokument został podpisany zgodnie z prawem. Oto jak zweryfikować podpis w dokumencie za pomocą kodu QR.

##### Krok 1: Skonfiguruj opcje weryfikacji
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();

verifyOptions.setEncodeType(QrCodeTypes.QR);
verifyOptions.setText("John Smith"); // Tekst do weryfikacji
verifyOptions.setAllPages(false); 
verifyOptions.setPageNumber(1);
```
**Wyjaśnienie**Opcje weryfikacji określają, jakiego typu kodu QR i tekstu należy szukać, zapewniając w ten sposób, że podpis będzie zgodny z Twoimi oczekiwaniami.

##### Krok 2: Przeprowadź weryfikację
```java
boolean isValid = signature2.verify(verifyOptions).isValid();
System.out.println("Is Signature Valid? " + isValid);
```
**Wyjaśnienie**: Sprawdza, czy dokument zawiera prawidłowy kod QR odpowiadający Twoim kryteriom.

### Wyszukaj dokument w celu uzyskania podpisu za pomocą kodu QR
#### Przegląd
Zlokalizowanie istniejących podpisów w dokumencie jest czasami konieczne. Oto jak możesz je wyszukać za pomocą GroupDocs.Signature.

##### Krok 1: Skonfiguruj opcje wyszukiwania
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import com.groupdocs.signature.options.search.QrCodeSearchOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeSearchOptions searchOptions = new QrCodeSearchOptions();
searchOptions.setAllPages(true);
```
**Wyjaśnienie**:Narzędzie zostanie wówczas skonfigurowane do skanowania wszystkich stron w celu znalezienia podpisów w postaci kodów QR.

##### Krok 2: Wykonaj wyszukiwanie
```java
List<QrCodeSignature> signatures = signature2.search(QrCodeSignature.class, searchOptions);

for (QrCodeSignature qrSignature : signatures) {
    System.out.println("Found Signature ID: " + qrSignature.getSignatureId());
}
```
**Wyjaśnienie**:Pobiera wszystkie podpisy w postaci kodów QR znalezione w dokumencie.

### Aktualizacja dokumentu Podpis kodu QR
#### Przegląd
Aktualizacja podpisu wiąże się ze zmianą jego właściwości, takich jak położenie czy rozmiar. Oto jak to zrobić:

##### Krok 1: Przygotuj podpisy do aktualizacji
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.io.ByteArrayOutputStream;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
List<QrCodeSignature> signaturesToUpdate = new ArrayList<>();

// Zakładając, że „podpisy” to lista obiektów QrCodeSignature uzyskana z wyszukiwania
for (QrCodeSignature qrSignature : signatures) {
    qrSignature.setLeft(qrSignature.getLeft() + 100);
    qrSignature.setTop(qrSignature.getTop() + 100);
    qrSignature.setWidth(200);
    qrSignature.setHeight(50);
    signaturesToUpdate.add(qrSignature);
}
```
**Wyjaśnienie**:Dostosowuje pozycję i rozmiar każdego podpisu.

##### Krok 2: Aktualizacja dokumentu
```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature2.update(outputStream, signaturesToUpdate);
```
**Wyjaśnienie**:Dokument został zaktualizowany o zmodyfikowane podpisy kodów QR.

### Usuń kod QR dokumentu Podpis według ID
#### Przegląd
Usunięcie podpisu może być konieczne, jeśli nie jest już potrzebny lub został dodany przez pomyłkę. Oto, jak możesz go usunąć, używając jego unikalnego identyfikatora.

##### Krok 1: Zidentyfikuj podpisy do usunięcia
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
**Wyjaśnienie**: Ta opcja wyszukuje i usuwa podpis kodu QR według jego unikalnego identyfikatora.

## Wniosek
Ten przewodnik przeprowadzi Cię przez proces zabezpieczania dokumentów za pomocą podpisów kodem QR w Javie z wykorzystaniem GroupDocs.Signature. Postępując zgodnie z tymi krokami, możesz mieć pewność, że Twoje dokumenty są podpisane bezpiecznie i łatwo zweryfikować ich autentyczność.