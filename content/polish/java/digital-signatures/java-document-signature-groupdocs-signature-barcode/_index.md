---
date: '2026-07-15'
description: Dowiedz się, jak dodać kod kreskowy PDF Java przy użyciu GroupDocs.Signature
  – krok po kroku przewodnik po podpisywaniu, weryfikacji, wyszukiwaniu, aktualizacji
  i usuwaniu podpisów kodów kreskowych w dokumentach Java.
keywords:
- add barcode pdf java
- groupdocs barcode signature
- java document signing
lastmod: '2026-07-15'
linktitle: Przewodnik po podpisie kodu kreskowego w Javie
og_description: Dowiedz się, jak dodać kod kreskowy PDF Java przy użyciu GroupDocs.Signature
  – krok po kroku przewodnik po podpisywaniu, weryfikacji, wyszukiwaniu, aktualizacji
  i usuwaniu podpisów kodów kreskowych w dokumentach Java.
og_image_alt: Guide showing how to add barcode PDF Java using GroupDocs.Signature
og_title: Dodaj kod kreskowy PDF Java – Podpisz i zweryfikuj z GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-07-15'
  description: Learn how to add barcode PDF Java using GroupDocs.Signature – step‑by‑step
    guide to sign, verify, search, update and delete barcode signatures in Java documents.
  headline: Add Barcode PDF Java – Sign & Verify with GroupDocs
  type: TechArticle
- description: Learn how to add barcode PDF Java using GroupDocs.Signature – step‑by‑step
    guide to sign, verify, search, update and delete barcode signatures in Java documents.
  name: Add Barcode PDF Java – Sign & Verify with GroupDocs
  steps:
  - name: Case mismatch (e.g., “John Smith” vs. “john smith”).
    text: Case mismatch (e.g., “John Smith” vs. “john smith”).
  - name: Extra whitespace in the encoded text.
    text: Extra whitespace in the encoded text.
  - name: Wrong barcode type specified in the verification options.
    text: Wrong barcode type specified in the verification options.
  - name: Searching the wrong page number.
    text: Searching the wrong page number.
  - name: '**Reuse Signature Instances** – Create a single `Signature` object per
      document and reuse it for multiple operations.'
    text: '**Reuse Signature Instances** – Create a single `Signature` object per
      document and reuse it for multiple operations.'
  - name: '**Search Specific Pages Only** – Limit the page range to where barcodes
      are expected.'
    text: '**Search Specific Pages Only** – Limit the page range to where barcodes
      are expected.'
  - name: '**Choose the Simplest Barcode Type** – Simpler barcodes generate faster;
      only use QR or Data Matrix when you truly need the extra capacity.'
    text: '**Choose the Simplest Barcode Type** – Simpler barcodes generate faster;
      only use QR or Data Matrix when you truly need the extra capacity.'
  - name: '**Never Encode Sensitive Personal Data** – Barcodes are easily readable;
      avoid PII such as SSNs or passwords.'
    text: '**Never Encode Sensitive Personal Data** – Barcodes are easily readable;
      avoid PII such as SSNs or passwords.'
  - name: '**Validate Server‑Side** – Never trust client‑side verification alone;
      always re‑verify on a trusted backend.'
    text: '**Validate Server‑Side** – Never trust client‑side verification alone;
      always re‑verify on a trusted backend.'
  - name: '**Add Timestamps** – Include a timestamp in the barcode payload to prevent
      replay attacks.'
    text: '**Add Timestamps** – Include a timestamp in the barcode payload to prevent
      replay attacks.'
  type: HowTo
- questions:
  - answer: Yes – the library is fully compatible with JDK 8, 11, and 17.
    question: Can I use GroupDocs.Signature with Java 17?
  - answer: When you use Code128 or QR with sufficient size and contrast, the barcode
      remains scannable after printing and scanning.
    question: Does the barcode survive a print‑scan cycle?
  - answer: There is no hard limit; however, for optimal performance keep the total
      count below **200** per document.
    question: How many barcodes can a single document contain?
  - answer: A temporary license removes evaluation watermarks; a full license is mandatory
      for any production deployment.
    question: Is a license required for development builds?
  - answer: Yes – provide the password when creating the `Signature` object; the API
      will unlock the file internally.
    question: Can I sign password‑protected PDFs?
  type: FAQPage
tags:
- barcode signature
- groupdocs
- java
- pdf
- document signing
title: Dodaj kod kreskowy PDF Java – Podpisz i zweryfikuj z GroupDocs
type: docs
url: /pl/java/digital-signatures/java-document-signature-groupdocs-signature-barcode/
weight: 1
---

# Dodaj kod kreskowy PDF Java – Podpisz i zweryfikuj z GroupDocs

Jeśli potrzebujesz szybkiego, wizualnego sposobu oznaczania dokumentów w wewnętrznych przepływach pracy, dodanie kodu kreskowego do PDF w Javie jest doskonałym rozwiązaniem. Dzięki **GroupDocs.Signature** możesz osadzać, weryfikować, wyszukiwać, aktualizować i usuwać podpisy kodów kreskowych bez obciążenia pełnymi podpisami cyfrowymi opartymi na PKI. Ten samouczek przeprowadzi Cię przez każdy krok, od konfiguracji środowiska po gotowe do produkcji najlepsze praktyki.

## Szybkie odpowiedzi
- **Jaką bibliotekę dodaje kod kreskowy do PDF‑ów w Javie?** GroupDocs.Signature for Java.  
- **Czy mogę podpisać PDF, Word i obrazy?** Tak – API obsługuje ponad 30 formatów.  
- **Czy potrzebna jest licencja do rozwoju?** Tymczasowa licencja na 30 dni jest darmowa; pełna licencja jest wymagana w produkcji.  
- **Ile linii kodu potrzebnych jest do podpisania PDF?** Zaledwie dwie: utwórz obiekt `Signature` i wywołaj `sign`.  
- **Czy weryfikacja kodu kreskowego jest rozróżniana pod względem wielkości liter?** Tak – tekst musi dokładnie pasować, łącznie z wielkością liter i spacjami.

## Co to jest add barcode pdf java?
`add barcode pdf java` odnosi się do procesu użycia kodu Java do osadzenia kodu kreskowego (takiego jak Code128, QR lub Data Matrix) w pliku PDF. Technika ta zapewnia znacznik czytelny maszynowo, który może być skanowany lub programowo weryfikowany, umożliwiając szybkie śledzenie dokumentów w systemach wewnętrznych.

## Dlaczego używać podpisów kodów kreskowych zamiast pełnych podpisów cyfrowych?
Podpisy kodów kreskowych są **30‑50 % szybsze** w generowaniu i weryfikacji niż podpisy cyfrowe oparte na PKI i działają niezawodnie po cyklu druk‑skan. Nie wymagają także zarządzania certyfikatami, co czyni je idealnymi dla wysokowolumenowych, wewnętrznych przepływów pracy, gdzie dowód kryptograficzny nie jest obowiązkowy.

## Wymagania wstępne

- **Java Development Kit (JDK) 8+** – zalecane Java 11 lub 17 dla lepszej wydajności.  
- **IDE** – IntelliJ IDEA lub Eclipse (przykłady używają składni IntelliJ).  
- **Narzędzie budowania** – Maven lub Gradle do zarządzania zależnościami.  

### Dodawanie GroupDocs.Signature do projektu

Najłatwiejszy sposób to dodanie biblioteki przez narzędzie budowania. Oto jak:

**Użytkownicy Maven** – Dodaj to do swojego `pom.xml`:

``` 
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```
```

**Użytkownicy Gradle** – Dodaj to do swojego `build.gradle`:

``` 
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```
```

**Bezpośrednie pobranie JAR** – Jeśli wolisz ręczną konfigurację, pobierz JAR z [GroupDocs.Signature releases](https://releases.groupdocs.com/signature/java/) i dodaj go do classpath.

### Uzyskanie licencji

GroupDocs.Signature nie jest darmowy w użyciu produkcyjnym, ale masz elastyczne opcje:

- **Bezpłatna wersja próbna** – Pobierz z [GroupDocs download page](https://releases.groupdocs.com/signature/java/) aby przetestować funkcje (dodawane są znaki wodne oceny).  
- **Licencja tymczasowa** – Uzyskaj 30 dni pełnego dostępu przez [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/) – idealne do proof‑of‑concept.  
- **Pełna licencja** – Dla wdrożeń produkcyjnych, sprawdź [GroupDocs purchase options](https://purchase.groupdocs.com/buy).  

**Wskazówka:** Zacznij od licencji tymczasowej w fazie rozwoju; usuwa ona znaki wodne po przejściu na stały klucz.

### Szybka kontrola środowiska

Po dodaniu zależności uruchom prosty test dymny:

``` 
```java
import com.groupdocs.signature.Signature;

public class SignatureTest {
    public static void main(String[] args) {
        try {
            Signature signature = new Signature("test.pdf");
            System.out.println("GroupDocs.Signature initialized successfully!");
            signature.dispose();
        } catch (Exception e) {
            System.err.println("Setup issue: " + e.getMessage());
        }
    }
}
```
```

Jeśli program uruchomi się bez błędów, środowisko jest gotowe. W razie problemów sprawdź wersję JDK oraz dokładną wersję biblioteki, którą dodałeś.

## Kiedy używać podpisów kodów kreskowych

Podpisy kodów kreskowych wyróżniają się w określonych scenariuszach:

- **Wewnętrzne przepływy dokumentów** – Śledź faktury, zamówienia lub notatki w łańcuchu zatwierdzeń.  
- **Przetwarzanie wysokich wolumenów** – Podpisuj tysiące dokumentów szybko; generowanie kodu kreskowego jest do **2× szybsze** niż pełne podpisy cyfrowe.  
- **Mosty druk‑skan** – Kody kreskowe przetrwają cykl druk‑skan, co czyni je idealnymi dla hybrydowych procesów papier‑cyfrowych.  
- **Integracja z systemami legacy** – Istniejące skanery kodów kreskowych mogą odczytać tagi bez dodatkowego oprogramowania.  
- **Ścieżki audytu** – Osadzaj identyfikatory transakcji lub znaczniki czasu, które audytorzy mogą natychmiast zweryfikować.

Unikaj podpisów kodów kreskowych w umowach prawnych, dokumentach wysokiego bezpieczeństwa lub wymianach z partnerami zewnętrznymi, gdzie wymagane są podpisy cyfrowe oparte na PKI.

## Konfiguracja GroupDocs.Signature dla Java

### Definicja klasy podstawowej

Klasa `Signature` jest punktem wejścia dla wszystkich operacji podpisywania, weryfikacji, wyszukiwania, aktualizacji i usuwania w GroupDocs.Signature.

``` 
```java
import com.groupdocs.signature.Signature;
```
```

### Podstawowa inicjalizacja

Utwórz obiekt `Signature`, który wskazuje na docelowy plik:

``` 
```java
Signature signature = new Signature("path/to/your/document.pdf");
```
```

**Ważne uwagi**

- Ścieżki mogą być bezwzględne lub względne; użyj `System.getProperty("user.home")` dla kompatybilności wieloplatformowej.  
- GroupDocs obsługuje **ponad 30 formatów wejścia i wyjścia**, w tym PDF, DOCX, XLSX, PPTX i PNG.  
- Zawsze zwalniaj zasoby przy pomocy `signature.dispose()` lub bloku try‑with‑resources:

``` 
```java
try (Signature signature = new Signature("path/to/your/document.pdf")) {
    // Your signing operations here
} catch (Exception e) {
    System.err.println("Error working with document: " + e.getMessage());
}
```
```

Teraz możesz dodawać kody kreskowe.

## Jak dodać kod kreskowy do PDF w Javie?

Załaduj źródłowy PDF przy pomocy `new Signature("input.pdf")`, skonfiguruj obiekt `BarcodeSignature` (np. Code128 z tekstem „John Smith”) i wywołaj `sign`, aby uzyskać podpisany plik – wszystko w trzech zwięzłych linijkach kodu. To podejście pozwala osadzić znacznik czytelny maszynowo, zachowując oryginalny układ dokumentu, i działa dla każdego obsługiwanego formatu, nie tylko PDF‑ów.

### Implementacja krok po kroku

#### 1. Definicja ścieżek plików

Ustaw lokalizacje plików źródłowego i wyjściowego:

``` 
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/signed_sample.docx";
```
```

#### 2. Utworzenie obsługi podpisu

Zainicjuj obsługę z dokumentem źródłowym:

``` 
```java
Signature signature = new Signature(filePath);
```
```

#### 3. Konfiguracja opcji kodu kreskowego

Obiekt `BarcodeSignature` definiuje właściwości wizualne i danych kodu kreskowego. Ustaw typ kodu, zakodowany tekst, pozycję, rozmiar, kolor oraz opcjonalną czcionkę czytelną dla człowieka:

``` 
```java
BarcodeSignOptions signOptions = new BarcodeSignOptions("John Smith", BarcodeTypes.Code128);
signOptions.setVerticalAlignment(VerticalAlignment.Top);
signOptions.setHorizontalAlignment(HorizontalAlignment.Center);
signOptions.setWidth(100);
signOptions.setHeight(40);
signOptions.setMargin(new java.awt.Rectangle(20, 20, 0, 0));
signOptions.setForeColor(Color.RED);

SignatureFont signatureFont = new SignatureFont();
signatureFont.setSize(12);
signatureFont.setFamilyName("Comic Sans MS");
signOptions.setFont(signatureFont);
```
```

> **Wskazówka:** Jeśli zakodowany ciąg przekracza 20 znaków, zwiększ szerokość kodu, aby uniknąć błędów skanowania.

#### 4. Zastosowanie podpisu

Wykonaj operację podpisywania i wygeneruj plik wyjściowy:

``` 
```java
signature.sign(outputFilePath, signOptions);
```
```

#### 5. Przykład z życia

W systemie zatwierdzania faktur możesz osadzić identyfikator pracownika zatwierdzającego oraz znacznik czasu:

``` 
```java
String invoiceId = "INV-2025-0042";
String approver = "john.smith@company.com";
String timestamp = LocalDateTime.now().toString();

// Combine into barcode data
String barcodeData = invoiceId + "|" + approver + "|" + timestamp;

BarcodeSignOptions signOptions = new BarcodeSignOptions(barcodeData, BarcodeTypes.QR);
signOptions.setVerticalAlignment(VerticalAlignment.Bottom);
signOptions.setHorizontalAlignment(HorizontalAlignment.Right);

signature.sign(outputFilePath, signOptions);
```
```

Wynikowy PDF zawiera teraz skanowalny kod kreskowy, który koduje wszystkie niezbędne metadane zatwierdzenia.

## Jak zweryfikować podpis kodu kreskowego w dokumencie Java?

Metoda `Signature.verify` sprawdza dokument pod kątem pasujących podpisów kodów kreskowych na podstawie podanych opcji, zwracając wartość boolean wskazującą, czy oczekiwany kod jest obecny. Weryfikacja jest przydatna w automatycznych przepływach, gdzie trzeba potwierdzić, że dokument został przetworzony przez właściwą stronę przed dalszymi działaniami.

### Kroki weryfikacji

#### 1. Załaduj podpisany dokument

``` 
```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");
```
```

#### 2. Ustaw kryteria weryfikacji

Zdefiniuj dokładny tekst, format kodu i numer strony, którego oczekujesz:

``` 
```java
BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
verifyOptions.setAllPages(false); // Only check the first page
verifyOptions.setPageNumber(1);
verifyOptions.setEncodeType(BarcodeTypes.Code128);
verifyOptions.setText("John Smith");
```
```

#### 3. Uruchom weryfikację

Wykonaj sprawdzenie i obsłuż wynik:

``` 
```java
boolean isValid = signature.verify(verifyOptions) != null;

if (isValid) {
    System.out.println("Document signature verified successfully!");
} else {
    System.out.println("Warning: Signature verification failed!");
}
```
```

**Typowy wzorzec:** Aby po prostu potwierdzić, że *dowolny* kod danego typu istnieje, pomiń filtr `setText`:

``` 
```java
BarcodeVerifyOptions flexibleOptions = new BarcodeVerifyOptions();
flexibleOptions.setAllPages(true);
flexibleOptions.setEncodeType(BarcodeTypes.Code128);
// No setText() call = accept any text with this barcode type

boolean hasAnySignature = signature.verify(flexibleOptions) != null;
```
```

Albo zweryfikuj tylko format kodu, nie zwracając uwagi na zawartość:

``` 
```java
BarcodeVerifyOptions formatOnly = new BarcodeVerifyOptions();
formatOnly.setEncodeType(BarcodeTypes.QR);
// Confirms a QR code exists, regardless of content
```
```

> **Ostrzeżenie:** Weryfikacja jest wrażliwa na wielkość liter i spacje; zawsze przycinaj i normalizuj dane przed podpisaniem.

## Jak wyszukać podpisy kodów kreskowych w dokumencie?

Metoda `Signature.search` skanuje dokument w poszukiwaniu podpisów kodów kreskowych spełniających podane `BarcodeSearchOptions`, zwracając kolekcję zawierającą lokalizację każdego kodu, numer strony i zakodowaną wartość. Dzięki temu można masowo wyodrębniać metadane bez ręcznego otwierania każdego pliku.

### Przebieg wyszukiwania

#### 1. Inicjalizacja wyszukiwania

``` 
```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");
```
```

#### 2. Konfiguracja parametrów wyszukiwania

Określ zakres stron, typ kodu lub filtry tekstowe:

``` 
```java
BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true); // Search the entire document
```
```

Opcjonalnie zawęź zakres, aby poprawić wydajność:

``` 
```java
BarcodeSearchOptions narrowSearch = new BarcodeSearchOptions();
narrowSearch.setAllPages(false);
narrowSearch.setPageNumber(1); // Only search page 1
narrowSearch.setEncodeType(BarcodeTypes.Code128); // Only find Code128 barcodes
```
```

#### 3. Wykonaj wyszukiwanie

``` 
```java
java.util.List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);

System.out.println("Found " + signatures.size() + " barcode signature(s)");

for (BarcodeSignature bcSignature : signatures) {
    System.out.println("Barcode Type: " + bcSignature.getEncodeType().getTypeName());
    System.out.println("Text: " + bcSignature.getText());
    System.out.println("Position: (" + bcSignature.getLeft() + ", " + bcSignature.getTop() + ")");
    System.out.println("Size: " + bcSignature.getWidth() + "x" + bcSignature.getHeight());
    System.out.println("---");
}
```
```

#### 4. Przykład wyodrębniania danych

Pobierz dane zatwierdzenia z każdego kodu w partii faktur:

``` 
```java
List<BarcodeSignature> foundSignatures = signature.search(BarcodeSignature.class, searchOptions);

for (BarcodeSignature sig : foundSignatures) {
    String barcodeData = sig.getText();
    
    // Parse your custom format (remember our invoice example?)
    String[] parts = barcodeData.split("\\|");
    if (parts.length == 3) {
        String invoiceId = parts[0];
        String approver = parts[1];
        String timestamp = parts[2];
        
        System.out.println("Invoice " + invoiceId + " approved by " + approver + " at " + timestamp);
    }
}
```
```

> **Wskazówka wydajnościowa:** Dla dokumentów powyżej 100 stron zawsze ograniczaj wyszukiwanie do stron, które faktycznie zawierają kody; może to skrócić czas wykonania nawet o **70 %**.

## Jak zaktualizować istniejący podpis kodu kreskowego?

Metoda `Signature.update` modyfikuje atrybuty wizualne istniejącego podpisu kodu kreskowego — takie jak pozycja, rozmiar czy kolor — zachowując pierwotne zakodowane dane. Przydatne, gdy po podpisaniu wymagane są zmiany układu.

### Procedura aktualizacji

#### 1. Znajdź podpisy do aktualizacji

``` 
```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");

BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true);

List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
```
```

#### 2. Zmodyfikuj żądane właściwości

``` 
```java
List<BarcodeSignature> signaturesToUpdate = new ArrayList<>();

if (!signatures.isEmpty()) {
    BarcodeSignature bcSignature = signatures.get(0); // Update the first found signature
    
    // Move it 100px right and 100px down
    bcSignature.setLeft(bcSignature.getLeft() + 100);
    bcSignature.setTop(bcSignature.getTop() + 100);
    
    // Make it bigger
    bcSignature.setWidth(200);
    bcSignature.setHeight(50);
    
    signaturesToUpdate.add(bcSignature);
}
```
```

Możesz zmienić kilka atrybutów jednocześnie:

``` 
```java
bcSignature.setLeft(50);
bcSignature.setTop(50);
bcSignature.setWidth(150);
bcSignature.setHeight(45);
// Note: You can't change the encoded text or barcode type with update
// For that, you'd need to delete and re-sign
```
```

#### 3. Zapisz zmiany

``` 
```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature.update(outputStream, signaturesToUpdate);

// If you want to save to a file instead:
// signature.update("path/to/updated_document.docx", signaturesToUpdate);
```
```

#### 4. Przykład z życia

Przemieść wszystkie podpisy, aby nie nachodziły na nowo dodane logo firmy:

``` 
```java
List<BarcodeSignature> allSignatures = signature.search(BarcodeSignature.class, searchOptions);
List<BarcodeSignature> toUpdate = new ArrayList<>();

for (BarcodeSignature sig : allSignatures) {
    // Move all signatures down by 50px to clear space for new logo
    if (sig.getTop() < 100) {
        sig.setTop(sig.getTop() + 50);
        toUpdate.add(sig);
    }
}

if (!toUpdate.isEmpty()) {
    signature.update(outputStream, toUpdate);
    System.out.println("Repositioned " + toUpdate.size() + " signature(s)");
}
```
```

> **Ograniczenie:** Zmiana zakodowanego tekstu wymaga usunięcia i ponownego wstawienia podpisu.

## Jak usunąć podpisy kodów kreskowych z dokumentu?

Metoda `Signature.delete` trwale usuwa wybrane podpisy kodów kreskowych z dokumentu, usuwając zarówno element wizualny, jak i zakodowane dane. Użyj tej operacji przy czyszczeniu testowych podpisów lub gdy kod przestał być potrzebny.

### Kroki usuwania

#### 1. Zlokalizuj podpisy

``` 
```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");

BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true);

List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
```
```

#### 2. Usuń wybrane podpisy

``` 
```java
List<BarcodeSignature> signaturesToDelete = new ArrayList<>();

// Delete all Code128 signatures (for example)
for (BarcodeSignature sig : signatures) {
    if (sig.getEncodeType().equals(BarcodeTypes.Code128)) {
        signaturesToDelete.add(sig);
    }
}

if (!signaturesToDelete.isEmpty()) {
    boolean result = signature.delete(signaturesToDelete);
    
    if (result) {
        System.out.println("Successfully deleted " + signaturesToDelete.size() + " signature(s)");
    } else {
        System.err.println("Failed to delete signatures");
    }
}
```
```

#### 3. Przykład warunkowego usuwania

Usuń tylko kody starsze niż określony znacznik czasu (zakładając, że znacznik czasu jest częścią zakodowanego tekstu):

``` 
```java
LocalDateTime cutoffDate = LocalDateTime.now().minusDays(30);
List<BarcodeSignature> outdatedSignatures = new ArrayList<>();

for (BarcodeSignature sig : signatures) {
    try {
        String text = sig.getText();
        // Assuming format like "data|timestamp"
        String[] parts = text.split("\\|");
        if (parts.length > 1) {
            LocalDateTime sigDate = LocalDateTime.parse(parts[1]);
            if (sigDate.isBefore(cutoffDate)) {
                outdatedSignatures.add(sig);
            }
        }
    } catch (Exception e) {
        // Skip signatures that don't match our format
        continue;
    }
}

if (!outdatedSignatures.isEmpty()) {
    signature.delete(outdatedSignatures);
    System.out.println("Removed " + outdatedSignatures.size() + " outdated signature(s)");
}
```
```

> **Uwaga:** Usunięcie nie może być cofnięte; zawsze pracuj na kopii plików produkcyjnych podczas testów.

#### 4. Wzorzec usuwania wsadowego

Wyczyść testowe podpisy przed wydaniem:

``` 
```java
// Remove all signatures containing "TEST" in their text
List<BarcodeSignature> testSignatures = signatures.stream()
    .filter(sig -> sig.getText().toUpperCase().contains("TEST"))
    .collect(Collectors.toList());

if (!testSignatures.isEmpty()) {
    signature.delete(testSignatures);
    System.out.println("Cleaned up " + testSignatures.size() + " test signature(s)");
}
```
```

## Typy kodów kreskowych: Praktyczny przewodnik

Wybór odpowiedniego kodu wpływa na niezawodność skanowania, pojemność danych i kompatybilność z drukarką.

### Code128 (najczęstszy wybór)

- **Kiedy używać:** Dane alfanumeryczne, wysoka gęstość, dokumenty drukowane.  
- **Zalety:** Kompaktowy, działa ze standardowymi skanerami, wyraźny przy małych rozmiarach.  
- **Wady:** Ograniczony do ASCII, mniej odporny na błędy niż kody 2‑D.  

Przykład:

``` 
```java
BarcodeSignOptions code128 = new BarcodeSignOptions("INV-2025-042", BarcodeTypes.Code128);
```
```

### QR Code (najlepszy dla mobilnych)

- **Kiedy używać:** Skanowanie mobilne, duże ładunki danych (URL, JSON itp.), dokumenty narażone na uszkodzenia.  
- **Zalety:** Do 4 000 znaków, wbudowana korekcja błędów, przyjazny smartfonom.  
- **Wady:** Większy ślad wizualny, wymaga wyższej rozdzielczości przy małych rozmiarach.  

Przykład:

``` 
```java
String jsonData = "{\"invoice\":\"INV-042\",\"amount\":1500.00,\"approver\":\"john@company.com\"}";
BarcodeSignOptions qrCode = new BarcodeSignOptions(jsonData, BarcodeTypes.QR);
```
```

### Code39 (stary, niezawodny)

- **Kiedy używać:** Środowiska ze starszymi skanerami, potrzeba czytelnego tekstu dla człowieka.  
- **Zalety:** Szerokie wsparcie legacy, prosty format, brak wymogu sumy kontrolnej.  
- **Wady:** Niska gęstość danych, ograniczony zestaw znaków, zajmuje więcej miejsca.  

### Data Matrix (kompaktowy potężny)

- **Kiedy używać:** Bardzo ograniczona przestrzeń, znakowanie małych przedmiotów, dane wysokiej gęstości.  
- **Zalety:** Bardzo kompaktowy, silna korekcja błędów, działa na powierzchniach zakrzywionych.  
- **Wady:** Wymaga wysokiej jakości druku, mniej powszechne wsparcie skanerów.  

#### Szybkie porównanie

| Typ kodu      | Pojemność danych | Najlepsze zastosowanie | Typowy rozmiar |
|---------------|-------------------|------------------------|----------------|
| Code128       | ~100 znaków       | Uniwersalne tagowanie  | Mały |
| QR Code       | ~4 000 znaków     | Skanowanie mobilne, bogate dane | Średni |
| Code39        | ~43 znaki         | Sprzęt legacy          | Duży |
| Data Matrix   | ~3 000 znaków     | Małe przestrzenie, tagi przemysłowe | Bardzo mały |

**Rekomendacja:** Zacznij od **Code128** dla prostych identyfikatorów. Przejdź na **QR**, gdy potrzebujesz osadzić URL lub większy ładunek. **Code39** używaj wyłącznie w integracjach legacy.

## Typowe problemy i rozwiązania

### Problem: „Kod nie został znaleziony podczas weryfikacji”

**Objawy:** Weryfikacja zwraca `false`, mimo że kod jest widoczny.

**Typowe przyczyny**
1. Rozbieżność wielkości liter (np. „John Smith” vs. „john smith”).  
2. Dodatkowe spacje w zakodowanym tekście.  
3. Nieprawidłowy typ kodu podany w opcjach weryfikacji.  
4. Wyszukiwanie na niewłaściwym numerze strony.

**Rozwiązanie:** Normalizuj tekst przed podpisaniem i weryfikacją oraz upewnij się, że `setEncodeType` odpowiada oryginalnemu typowi.

``` 
```java
// Always normalize your data
String signatureText = originalText.trim().toLowerCase();

// When signing:
BarcodeSignOptions signOptions = new BarcodeSignOptions(signatureText, BarcodeTypes.Code128);

// When verifying:
BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
verifyOptions.setText(signatureText); // Use the same normalized text
verifyOptions.setEncodeType(BarcodeTypes.Code128);
```
```

### Problem: „Kod jest rozmazany lub nieczytelny”

**Objawy:** Wydrukowane kody nie mogą być zeskanowane.

**Przyczyny**
- Zbyt małe wymiary kodu względem ilości danych.  
- Ustawienia drukarki o niskiej rozdzielczości.  
- Niewystarczający kontrast między kolorem kodu a tłem.

**Rozwiązanie:** Zwiększ szerokość/wysokość kodu, użyj wysokiego kontrastu (czarny na białym) i ustaw DPI drukarki przynajmniej na 300 dpi.

``` 
```java
// Increase size for longer strings
int dataLength = barcodeText.length();
int minWidth = Math.max(100, dataLength * 10); // 10px per character minimum

BarcodeSignOptions signOptions = new BarcodeSignOptions(barcodeText, BarcodeTypes.Code128);
signOptions.setWidth(minWidth);
signOptions.setHeight(60); // Taller = easier to scan

// Use high-contrast colors
signOptions.setForeColor(Color.BLACK); // Black on white is most reliable
signOptions.setBackColor(Color.WHITE);
```
```

### Problem: „OutOfMemoryError przy dużych dokumentach”

**Objawy:** Aplikacja się wyłącza przy przetwarzaniu PDF‑ów setek stron.

**Przyczyna:** Biblioteka ładuje cały dokument do pamięci.

**Rozwiązanie:** Włącz tryb strumieniowy i przetwarzaj strony partiami.

``` 
```java
// Process pages in batches instead of all at once
BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(false);

List<BarcodeSignature> allSignatures = new ArrayList<>();

for (int page = 1; page <= totalPages; page++) {
    searchOptions.setPageNumber(page);
    List<BarcodeSignature> pageSignatures = signature.search(BarcodeSignature.class, searchOptions);
    allSignatures.addAll(pageSignatures);
    
    // Process and clear as you go
    if (page % 10 == 0) {
        System.gc(); // Suggest garbage collection every 10 pages
    }
}
```
```

### Problem: „Pozycja podpisu niezgodna między typami dokumentów”

**Objawy:** Kody pojawiają się w różnych miejscach przy podpisywaniu PDF‑ów vs. dokumentów Word.

**Przyczyna:** PDF używa układu pochodzenia w lewym dolnym rogu, a Word w lewym górnym.

**Rozwiązanie:** Wykryj typ dokumentu i zastosuj odpowiednią transformację współrzędnych.

``` 
```java
// Use relative positioning instead of absolute
signOptions.setVerticalAlignment(VerticalAlignment.Bottom);
signOptions.setHorizontalAlignment(HorizontalAlignment.Right);

// Then use margins for fine-tuning
Padding margin = new Padding();
margin.setRight(50); // 50px from right edge
margin.setBottom(50); // 50px from bottom
signOptions.setMargin(margin);

// This works consistently across PDF, DOCX, XLSX, etc.
```
```

### Problem: „Zaktualizowane podpisy tracą formatowanie”

**Objawy:** Po wywołaniu `update` kolor lub czcionka kodu zmienia się nieoczekiwanie.

**Przyczyna:** Nie wszystkie właściwości wizualne są zachowywane podczas aktualizacji.

**Rozwiązanie:** Ponownie zastosuj ustawienia wizualne po wywołaniu `update`.

``` 
```java
// When updating, explicitly set all visual properties
bcSignature.setLeft(newLeft);
bcSignature.setTop(newTop);
bcSignature.setWidth(originalWidth); // Don't forget these!
bcSignature.setHeight(originalHeight);
// Note: Color and font can't be updated - you'd need to delete and re-sign
```
```

## Najlepsze praktyki dla produkcji

### Optymalizacja wydajności

1. **Wielokrotne użycie obiektów Signature** – Utwórz jeden obiekt `Signature` na dokument i używaj go do wielu operacji.

``` 
```java
// Bad - Creates new instance each time
public void processDocument(String path) {
    Signature sig1 = new Signature(path);
    sig1.search(/* ... */);
    
    Signature sig2 = new Signature(path); // Unnecessary reload
    sig2.verify(/* ... */);
}

// Good - Reuse the same instance
public void processDocument(String path) {
    try (Signature signature = new Signature(path)) {
        signature.search(/* ... */);
        signature.verify(/* ... */);
        signature.update(/* ... */);
    }
}
```
```

2. **Wyszukiwanie tylko na konkretnych stronach** – Ogranicz zakres stron do tych, gdzie spodziewasz się kodów.

``` 
```java
// Slow for 100+ page documents
BarcodeSearchOptions slowSearch = new BarcodeSearchOptions();
slowSearch.setAllPages(true);

// Fast - only check where signatures actually are
BarcodeSearchOptions fastSearch = new BarcodeSearchOptions();
fastSearch.setAllPages(false);
fastSearch.setPageNumber(1); // Only check cover page
```
```

3. **Wybieraj najprostszy typ kodu** – Prostsze kody generują się szybciej; używaj QR lub Data Matrix tylko wtedy, gdy naprawdę potrzebujesz większej pojemności.

``` 
```java
// Overkill for simple IDs
BarcodeSignOptions slow = new BarcodeSignOptions("12345", BarcodeTypes.QR);

// Faster and more appropriate
BarcodeSignOptions fast = new BarcodeSignOptions("12345", BarcodeTypes.Code128);
```
```

### Rozważania bezpieczeństwa

1. **Nigdy nie koduj wrażliwych danych osobowych** – Kody kreskowe są łatwo czytelne; unikaj SSN, haseł itp.

``` 
```java
// Bad - exposes sensitive data
String barcodeData = "SSN:123-45-6789|Password:hunter2";

// Good - use reference IDs
String barcodeData = "USER-REF-7721X"; // Look up sensitive data server-side
```
```

2. **Walidacja po stronie serwera** – Nie polegaj wyłącznie na weryfikacji po stronie klienta; zawsze ponownie weryfikuj na zaufanym backendzie.

``` 
```java
// Client scans barcode and extracts "APPROVED-BY-ADMIN"
// Always verify server-side:
public boolean verifyApproval(String documentId, String scannedData) {
    // Load document from secure storage
    Signature signature = new Signature(getSecureDocument(documentId));
    
    BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
    verifyOptions.setText(scannedData);
    
    boolean isValid = signature.verify(verifyOptions) != null;
    
    // Also check against your database
    boolean isInDatabase = checkApprovalDatabase(documentId, scannedData);
    
    return isValid && isInDatabase;
}
```
```

3. **Dodawaj znaczniki czasu** – Umieść znacznik czasu w ładunku kodu, aby zapobiec atakom powtórzeniowym.

``` 
```java
import java.time.LocalDateTime;
import java.time.temporal.ChronoUnit;

String timestamp = LocalDateTime.now().truncatedTo(ChronoUnit.SECONDS).toString();
String barcodeData = "APPROVAL|" + userId + "|" + timestamp;

// When verifying, check the timestamp isn't too old
public boolean isSignatureRecent(String barcodeData, int maxAgeHours) {
    String[] parts = barcodeData.split("\\|");
    if (parts.length < 3) return false;
    
    LocalDateTime signatureTime = LocalDateTime.parse(parts[2]);
    LocalDateTime now = LocalDateTime.now();
    
    long hoursSince = ChronoUnit.HOURS.between(signatureTime, now);
    return hoursSince <= maxAgeHours;
}
```
```

### Wzorce obsługi błędów

- **Zawsze używaj try‑with‑resources**, aby zapewnić zwolnienie obiektów `Signature`.

``` 
```java
try (Signature signature = new Signature(documentPath)) {
    // Your operations here
    signature.sign(outputPath, signOptions);
} catch (Exception e) {
    logger.error("Failed to sign document: " + documentPath, e);
    throw new DocumentSigningException("Could not process document", e);
}
```
```

- **Waliduj dostęp do plików** przed próbą podpisania.

``` 
```java
public void signDocument(String inputPath, String outputPath) {
    File inputFile = new File(inputPath);
    
    if (!inputFile.exists()) {
        throw new IllegalArgumentException("Input file not found: " + inputPath);
    }
    
    if (!inputFile.canRead()) {
        throw new SecurityException("Cannot read input file: " + inputPath);
    }
    
    File outputDir = new File(outputPath).getParentFile();
    if (outputDir != null && !outputDir.exists()) {
        outputDir.mkdirs();
    }
    
    try (Signature signature = new Signature(inputPath)) {
        signature.sign(outputPath, signOptions);
    }
}
```
```

- **Synchronizuj dostęp**, jeśli wiele wątków może pracować na tym samym pliku.

``` 
```java
import java.util.concurrent.locks.ReentrantLock;
import java.util.concurrent.ConcurrentHashMap;

public class SignatureManager {
    private final ConcurrentHashMap<String, ReentrantLock> documentLocks = new ConcurrentHashMap<>();
    
    public void signDocument(String documentPath, BarcodeSignOptions options) {
        ReentrantLock lock = documentLocks.computeIfAbsent(documentPath, k -> new ReentrantLock());
        
        lock.lock();
        try (Signature signature = new Signature(documentPath)) {
            signature.sign(documentPath + ".signed", options);
        } finally {
            lock.unlock();
        }
    }
}
```
```

### Testowanie implementacji

**Szablon testu jednostkowego**

``` 
```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.io.TempDir;
import static org.junit.jupiter.api.Assertions.*;

public class BarcodeSignatureTest {
    
    @TempDir
    Path tempDir;
    
    @Test
    public void testSignAndVerify() throws Exception {
        // Setup
        String testDoc = "test-document.pdf";
        String outputDoc = tempDir.resolve("signed-test.pdf").toString();
        String testData = "TEST-USER-12345";
        
        // Sign
        try (Signature signature = new Signature(testDoc)) {
            BarcodeSignOptions signOptions = new BarcodeSignOptions(testData, BarcodeTypes.Code128);
            signature.sign(outputDoc, signOptions);
        }
        
        // Verify
        try (Signature signature = new Signature(outputDoc)) {
            BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
            verifyOptions.setText(testData);
            verifyOptions.setEncodeType(BarcodeTypes.Code128);
            
            boolean isValid = signature.verify(verifyOptions) != null;
            assertTrue(isValid, "Signature should be valid");
        }
    }
    
    @Test
    public void testSearchFindsSignature() throws Exception {
        String signedDoc = "signed-document.pdf";
        
        try (Signature signature = new Signature(signedDoc)) {
            BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
            searchOptions.setAllPages(true);
            
            List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
            
            assertFalse(signatures.isEmpty(), "Should find at least one signature");
            assertEquals("TEST-USER-12345", signatures.get(0).getText());
        }
    }
}
```
```

**Lista kontrolna integracji**

- ✅ Testuj wszystkie obsługiwane formaty (PDF, DOCX, XLSX, PPTX, PNG).  
- ✅ Sprawdź, czy kody przetrwają cykl druk‑skan.  
- ✅ Przeprowadź testy obciążeniowe z maksymalnymi długościami danych.  
- ✅ Potwierdź pozycjonowanie na A4, Letter i niestandardowych rozmiarach stron.  
- ✅ Uruchom równoległe podpisy na wielu dokumentach.  
- ✅ Monitoruj zużycie pamięci przy dokumentach > 500 stron.  
- ✅ Upewnij się, że skanery kodów odczytują wynik reliably.

### Logowanie i monitorowanie

Dodaj znaczące logi wokół każdej operacji:

``` 
```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class DocumentSigningService {
    private static final Logger logger = LoggerFactory.getLogger(DocumentSigningService.class);
    
    public void signDocument(String docPath, String barcodeData) {
        logger.info("Starting signature process for document: {}", docPath);
        logger.debug("Barcode data length: {} characters", barcodeData.length());
        
        try (Signature signature = new Signature(docPath)) {
            BarcodeSignOptions options = new BarcodeSignOptions(barcodeData, BarcodeTypes.Code128);
            
            long startTime = System.currentTimeMillis();
            signature.sign(docPath + ".signed", options);
            long duration = System.currentTimeMillis() - startTime;
            
            logger.info("Successfully signed document in {}ms", duration);
        } catch (Exception e) {
            logger.error("Failed to sign document: {}", docPath, e);
            throw new RuntimeException("Signature operation failed", e);
        }
    }
}
```
```

Śledź kluczowe metryki, takie jak czas przetwarzania, zużycie pamięci i wskaźniki błędów:

``` 
```java
// Track success/failure rates
metricsService.incrementCounter("signature.sign.success");
metricsService.incrementCounter("signature.verify.failure");

// Track performance
metricsService.recordTimer("signature.sign.duration", duration);

// Track document sizes
metricsService.recordHistogram("signature.document.pages", pageCount);
```
```

## Wskazówki od praktyków

**Strategia przetwarzania wsadowego**

Przy obsłudze setek plików przetwarzaj je w partiach i raportuj postęp:

``` 
```java
public void signBatch(List<String> documents, String barcodePrefix) {
    int total = documents.size();
    int completed = 0;
    int failed = 0;
    
    for (String docPath : documents) {
        try {
            String barcodeData = barcodePrefix + "-" + UUID.randomUUID().toString();
            signDocument(docPath, barcodeData);
            completed++;
            
            if (completed % 10 == 0) {
                logger.info("Progress: {}/{} documents signed", completed, total);
            }
        } catch (Exception e) {
            failed++;
            logger.warn("Failed to sign: {}", docPath, e);
        }
    }
    
    logger.info("Batch complete: {} succeeded, {} failed", completed, failed);
}
```
```

**Externalizacja konfiguracji**

Przechowuj ustawienia kodu (typ, rozmiar, kolor) w pliku properties, aby łatwo je dostroić bez rekompilacji:

``` 
```java
public class BarcodeConfig {
    private int defaultWidth = 100;
    private int defaultHeight = 40;
    private String defaultBarcodeType = "Code128";
    private String defaultColor = "BLACK";
    
    // Load from properties file or environment variables
    public BarcodeConfig() {
        this.defaultWidth = Integer.parseInt(
            System.getProperty("barcode.width", "100")
        );
        // ... load other properties
    }
    
    public BarcodeSignOptions createDefaultOptions(String text) {
        BarcodeSignOptions options = new BarcodeSignOptions(text, getBarcodeType());
        options.setWidth(defaultWidth);
        options.setHeight(defaultHeight);
        options.setForeColor(getColor());
        return options;
    }
}
```
```

**Standaryzacja ładunku kodu**

Używaj formatu rozdzielanego, np. `EMPID|TIMESTAMP|DOCID`, aby parsowanie było proste i spójne:

``` 
```java
public class BarcodeDataBuilder {
    private String userId;
    private String action;
    private LocalDateTime timestamp;
    private String documentId;
    
    public BarcodeDataBuilder setUserId(String userId) {
        this.userId = userId;
        return this;
    }
    
    public BarcodeDataBuilder setAction(String action) {
        this.action = action;
        return this;
    }
    
    public BarcodeDataBuilder setDocumentId(String documentId) {
        this.documentId = documentId;
        return this;
    }
    
    public String build() {
        this.timestamp = LocalDateTime.now();
        
        // Format: VERSION|USER|ACTION|DOC_ID|TIMESTAMP|CHECKSUM
        String data = String.join("|",
            "v1",
            userId,
            action,
            documentId,
            timestamp.toString()
        );
        
        // Add simple checksum
        int checksum = data.hashCode();
        return data + "|" + checksum;
    }
    
    public static ParsedBarcodeData parse(String barcodeData) {
        String[] parts = barcodeData.split("\\|");
        if (parts.length != 6 || !parts[0].equals("v1")) {
            throw new IllegalArgumentException("Invalid barcode format");
        }
        
        return new ParsedBarcodeData(parts[1], parts[2], parts[3], 
                                     LocalDateTime.parse(parts[4]));
    }
}

// Usage:
String barcodeData = new BarcodeDataBuilder()
    .setUserId("john.smith")
    .setAction("APPROVED")
    .setDocumentId("INV-2025-042")
    .build();
```
```

**Automatyczne wykrywanie typu dokumentu**

Dostosuj wymiary kodu w zależności od tego, czy celem jest PDF, Word czy obraz:

``` 
```java
public BarcodeSignOptions getOptimalOptions(String documentPath, String text) {
    String extension = documentPath.substring(documentPath.lastIndexOf(".") + 1).toLowerCase();
    
    BarcodeSignOptions options = new BarcodeSignOptions(text, BarcodeTypes.Code128);
    
    switch (extension) {
        case "pdf":
            // PDFs can handle larger, detailed barcodes
            options.setWidth(150);
            options.setHeight(50);
            break;
        case "docx":
        case "doc":
            // Word docs need compact signatures that don't disrupt flow
            options.setWidth(100);
            options.setHeight(35);
            options.setVerticalAlignment(VerticalAlignment.Bottom);
            break;
        case "xlsx":
        case "xls":
            // Excel needs signatures that don't obscure data
            options.setWidth(80);
            options.setHeight(30);
            options.setHorizontalAlignment(HorizontalAlignment.Right);
            break;
        default:
            // Safe defaults
            options.setWidth(100);
            options.setHeight(40);
    }
    
    return options;
}
```
```

## Dodatkowe zasoby

- [GroupDocs.Signature documentation](https://docs.groupdocs.com/signature/java/) – Pełny przewodnik API i przykłady użycia.  
- [GroupDocs support forum](https://forum.groupdocs.com/c/signature/13) – Pomoc społeczności i rozwiązywanie problemów.  
- [API reference](https://apireference.groupdocs.com/signature/java) – Szczegółowe sygnatury metod i opisy parametrów.

## Najczęściej zadawane pytania

**P: Czy mogę używać GroupDocs.Signature z Java 17?**  
O: Tak – biblioteka jest w pełni kompatybilna z JDK 8, 11 i 17.

**P: Czy kod kreskowy przetrwa cykl druk‑skan?**  
O: Gdy użyjesz Code128 lub QR o odpowiednim rozmiarze i kontraście, kod pozostaje skanowalny po wydrukowaniu i zeskanowaniu.

**P: Ile kodów kreskowych może zawierać pojedynczy dokument?**  
O: Nie ma sztywnego limitu; jednak dla optymalnej wydajności utrzymuj łączną liczbę poniżej **200** na dokument.

**P: Czy licencja jest wymagana dla wersji deweloperskich?**  
O: Tymczasowa licencja usuwa znaki wodne oceny; pełna licencja jest obowiązkowa w każdej produkcyjnej implementacji.

**P: Czy mogę podpisać PDF zabezpieczony hasłem?**  
O: Tak – podaj hasło przy tworzeniu obiektu `Signature`; API odblokuje plik wewnętrznie.

---

**Ostatnia aktualizacja:** 2026-07-15  
**Testowane z:** GroupDocs.Signature 23.9 for Java  
**Autor:** GroupDocs  

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

## Powiązane samouczki

- [How to Verify Barcode Signatures in Java with GroupDocs.Signature](/signature/java/search-verification/groupdocs-signature-java-document-verification/)
- [How to Search Digital Signatures in Java Documents with GroupDocs](/signature/java/search-verification/groupdocs-signature-java-digital-search-tutorial/)
- [Java Barcode Signature Tutorial - Add, Verify & Manage Barcodes in PDFs](/signature/java/barcode-signatures/)