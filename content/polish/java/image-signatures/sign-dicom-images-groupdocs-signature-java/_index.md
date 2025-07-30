---
"date": "2025-05-08"
"description": "Dowiedz się, jak bezpiecznie podpisywać obrazy DICOM za pomocą GroupDocs.Signature dla Java. Zwiększ bezpieczeństwo dokumentów, osadzając kody QR i metadane."
"title": "Podpisuj obrazy DICOM kodami QR i metadanymi za pomocą GroupDocs.Signature dla języka Java"
"url": "/pl/java/image-signatures/sign-dicom-images-groupdocs-signature-java/"
"weight": 1
---

# Jak podpisywać obrazy DICOM kodami QR i metadanymi za pomocą GroupDocs.Signature dla Java

## Wstęp

W dynamicznie rozwijającym się cyfrowym krajobrazie opieki zdrowotnej, bezpieczne zarządzanie danymi pacjentów ma kluczowe znaczenie. Ten samouczek przeprowadzi Cię przez proces wdrażania niezawodnego rozwiązania z wykorzystaniem GroupDocs.Signature for Java, umożliwiającego podpisywanie obrazów DICOM (Digital Imaging and Communications in Medicine) kodami QR i metadanymi. Funkcje te gwarantują autentyczność, ułatwiają identyfikowalność i zapewniają zgodność z przepisami poprzez osadzanie istotnych informacji bezpośrednio w obrazach medycznych.

### Czego się nauczysz:
- Jak zintegrować GroupDocs.Signature for Java z projektem.
- Proces podpisywania obrazów DICOM za pomocą kodów QR.
- Dodanie metadanych XMP w celu zwiększenia bezpieczeństwa dokumentu.
- Pobieranie, weryfikowanie i wyszukiwanie podpisów w plikach DICOM.
- Generowanie podglądów podpisanych obrazów DICOM.

Zaczynajmy! Zanim zaczniemy, upewnijmy się, że masz wszystko, czego potrzebujesz, aby płynnie przejść przez cały proces.

## Wymagania wstępne

Aby skutecznie wdrożyć funkcje GroupDocs.Signature, należy upewnić się, że spełnione są następujące wymagania wstępne:

### Wymagane biblioteki i zależności
- **GroupDocs.Signature dla Java**:Będziesz potrzebować wersji 23.12 lub nowszej tej biblioteki.

### Wymagania dotyczące konfiguracji środowiska
- **Zestaw narzędzi programistycznych Java (JDK)**: Upewnij się, że JDK jest zainstalowany w Twoim systemie.
- **IDE**:Użyj zintegrowanego środowiska programistycznego, takiego jak IntelliJ IDEA lub Eclipse.

### Wymagania wstępne dotyczące wiedzy
Podstawowa wiedza na temat:
- Programowanie w Javie i zasady obiektowe.
- Narzędzia do budowania Maven i Gradle do zarządzania zależnościami.

## Konfigurowanie GroupDocs.Signature dla języka Java

Aby rozpocząć korzystanie z GroupDocs.Signature, musisz dodać go jako zależność w swoim projekcie. Oto jak możesz to zrobić za pomocą różnych narzędzi do kompilacji:

### Maven
Dodaj następujący fragment kodu do swojego `pom.xml` plik:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle
Uwzględnij to w swoim `build.gradle` plik:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Bezpośrednie pobieranie
Alternatywnie możesz pobrać najnowszą wersję ze strony [GroupDocs.Signature dla wydań Java](https://releases.groupdocs.com/signature/java/).

#### Etapy uzyskania licencji
1. **Bezpłatny okres próbny**:Wypróbuj funkcje dzięki bezpłatnej wersji próbnej o ograniczonym czasie trwania.
2. **Licencja tymczasowa**:Uzyskaj tymczasową licencję, aby móc korzystać ze wszystkich możliwości.
3. **Zakup**:Kup subskrypcję, jeśli potrzebujesz długoterminowego dostępu.

#### Podstawowa inicjalizacja i konfiguracja

Aby zainicjować GroupDocs.Signature, utwórz instancję `Signature` klasa:
```java
import com.groupdocs.signature.Signature;

// Zainicjuj obiekt podpisu ścieżką do pliku DICOM
Signature signature = new Signature(filePath);
```

## Przewodnik wdrażania

### Podpisywanie obrazu DICOM za pomocą kodu QR i metadanych

#### Przegląd
Funkcja ta umożliwia podpisywanie obrazów DICOM kodem QR i dodawanie metadanych XMP, co zwiększa bezpieczeństwo dokumentu.

#### Krok 1: Skonfiguruj opcje podpisu kodem QR
```java
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.QrCodeSignOptions;

Padding padding = new Padding();
padding.setRight(5);
padding.setLeft(5);

QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues");
options.setAllPages(true);
options.setWidth(100);
options.setHeight(100);
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
options.setMargin(padding);
```
Tutaj konfigurujemy wygląd i pozycję kodu QR na obrazie DICOM.

#### Krok 2: Dodaj metadane XMP
```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomSaveOptions;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpEntry;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpType;

DicomSaveOptions dicomSaveOptions = new DicomSaveOptions();
List<DicomXmpEntry> xmpEntries = new ArrayList<>();
xmpEntries.add(new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4"));
dicomSaveOptions.setXmpEntries(xmpEntries);
```
Ten fragment kodu dodaje metadane do pliku DICOM, osadzając dodatkowe informacje o pacjencie.

#### Krok 3: Podpisz dokument
```java
String outputFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/" + fileName;
signature.sign(outputFilePath, options, dicomSaveOptions);
```
Ten `sign` Metoda ta zapisuje kod QR i metadane w pliku DICOM, zapisując je w określonej lokalizacji.

### Pobieranie informacji o podpisanym obrazie DICOM

#### Przegląd
Wyodrębnij metadane XMP z podpisanego obrazu DICOM w celu weryfikacji lub audytu.
```java
import com.groupdocs.signature.domain.IDocumentInfo;
import com.groupdocs.signature.domain.signatures.MetadataSignature;

IDocumentInfo documentInfo = signature.getDocumentInfo();
for (MetadataSignature item : documentInfo.getMetadataSignatures()) {
    System.out.println(item.toString());
}
```
Ten kod pobiera i drukuje wszystkie podpisy metadanych powiązane z plikiem DICOM.

### Weryfikacja podpisanego DICOM

#### Przegląd
Sprawdź, czy na podpisanym obrazie DICOM znajduje się kod QR, aby potwierdzić jego autentyczność.
```java
import com.groupdocs.signature.domain.VerificationResult;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;
import com.groupdocs.signature.domain.enums.TextMatchType;

QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();
verifyOptions.setAllPages(true);
verifyOptions.setText("Patient #36363393");
verifyOptions.setMatchType(TextMatchType.Contains);

VerificationResult result = signature.verify(verifyOptions);
if (result.isValid()) {
    System.out.println(filePath + " has successfully verified signatures!");
} else {
    System.out.println(filePath + " failed verification process.");
}
```
Ten etap weryfikacji gwarantuje, że kod QR spełnia oczekiwane kryteria, potwierdzając integralność dokumentu.

### Wyszukiwanie podpisów w podpisanym pliku DICOM

#### Przegląd
Znajdź wszystkie podpisy kodów QR w podpisanym obrazie DICOM w celu ich przejrzenia lub zweryfikowania.
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.util.List;

List<QrCodeSignature> signatures = signature.search(QrCodeSignature.class);
for (QrCodeSignature qrCodeSignature : signatures) {
    System.out.println("QRCode signature found at page " +
        qrCodeSignature.getPageNumber() + ": " +
        qrCodeSignature.getEncodeType().getTypeName() + ": " +
        qrCodeSignature.getText());
}
```
Funkcja ta jest przydatna przy skanowaniu wszystkich kodów QR podpisów w dokumencie, zapewniając kompleksowy wgląd.

### Generowanie podglądu podpisanego pliku DICOM

#### Przegląd
Utwórz podgląd każdej strony podpisanego obrazu DICOM, co umożliwi szybką wizualną inspekcję bez konieczności otwierania całego pliku.
```java
import com.groupdocs.signature.options.PreviewOptions;
import java.io.File;
import java.io.FileOutputStream;
import java.nio.file.Paths;

PreviewOptions previewOption = new PreviewOptions(pageNumber -> {
    try {
        String pageFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/image-" + pageNumber + ".jpg";
        return new FileOutputStream(Paths.get(pageFilePath).toFile());
    } catch (Exception e) {
        throw new RuntimeException(e.getMessage());
    }
});

signature.generatePreview(previewOption);
```
Ten fragment kodu generuje podgląd obrazu dla każdej strony, co może być przydatne do szybkiej weryfikacji lub udostępniania.

## Zastosowania praktyczne

GroupDocs.Signature dla Java oferuje kilka praktycznych zastosowań:
- **Obrazowanie medyczne**:Bezpiecznie podpisuj i zarządzaj obrazami DICOM pacjentów za pomocą kodów QR i metadanych.
- **Zarządzanie dokumentacją prawną**:Zwiększenie autentyczności dokumentów i zgodności z przepisami w postępowaniach prawnych.
- **Usługi finansowe**:Wprowadź bezpieczne podpisy elektroniczne na poufnych dokumentach finansowych.