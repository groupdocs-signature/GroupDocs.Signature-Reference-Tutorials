---
categories:
- Document Signing
- Healthcare Integration
date: '2026-09-15'
description: Dowiedz się, jak podpisać PDF za pomocą kodu kreskowego przy użyciu GroupDocs.Signature
  dla Javy. Przewodnik krok po kroku, jak dodać kody Data Matrix i QR w dokumentach
  medycznych.
keywords:
- sign pdf with barcode
- add qr code pdf
- hibc barcode java
- pdf signing java
- healthcare barcode signing
lastmod: '2026-09-15'
linktitle: Przewodnik po podpisywaniu PDF HIBC w Javie
og_description: Podpisz PDF za pomocą kodu kreskowego przy użyciu GroupDocs.Signature
  dla Javy. Dowiedz się, jak w kilku krokach osadzić kody Data Matrix i QR w dokumentach
  medycznych.
og_image_alt: 'Developer tutorial: sign PDF with HIBC barcode using GroupDocs.Signature
  for Java'
og_title: Podpisz PDF za pomocą kodu kreskowego HIBC w Javie – przewodnik GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-09-15'
  description: Learn how to sign PDF with barcode using GroupDocs.Signature for Java.
    Step‑by‑step guide for adding Data Matrix and QR codes in healthcare documents.
  headline: Sign PDF with barcode using HIBC in Java
  type: TechArticle
- description: Learn how to sign PDF with barcode using GroupDocs.Signature for Java.
    Step‑by‑step guide for adding Data Matrix and QR codes in healthcare documents.
  name: Sign PDF with barcode using HIBC in Java
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
- sign pdf
- barcode
- java
- healthcare
- groupdocs
title: Jak podpisać PDF za pomocą kodu kreskowego HIBC w Javie
type: docs
url: /pl/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/
weight: 1
---

# Podpisz PDF kodem kreskowym przy użyciu HIBC w Javie

Jeśli tworzysz oprogramowanie do logistyki farmaceutycznej lub opieki zdrowotnej, prawdopodobnie natknąłeś się na problem papierowego śledzenia, zagubionych podpisów i koszmarów audytowych. **Podpisywanie PDF kodem kreskowym** — szczególnie Data Matrix lub QR HIBC — tworzy dowód niezmienności, czytelny maszynowo, który przetrwa drukowanie, skanowanie i przegląd regulacyjny. W tym samouczku zobaczysz dokładnie, jak dodać zarówno Data Matrix, jak i QR do PDF przy użyciu GroupDocs.Signature for Java.

## Szybkie odpowiedzi
- **Jakiej biblioteki używać do obsługi kodów HIBC w Javie?** GroupDocs.Signature for Java.  
- **Który format kodu kreskowego jest najbardziej zwarty?** Data Matrix – idealny dla małych etykiet.  
- **Czy mogę dodać zarówno QR, jak i Data Matrix do tego samego PDF?** Tak, wystarczy utworzyć osobne `QrCodeSignOptions`.  
- **Czy potrzebne jest połączenie z internetem w czasie działania?** Nie, biblioteka działa w pełni offline po instalacji.  
- **Jaka wersja Javy jest zalecana?** Java 11+ dla wydajności produkcyjnej.

## Co to jest podpis PDF kodem HIBC?
`Signature` jest podstawową klasą GroupDocs.Signature, która reprezentuje dokument PDF i umożliwia osadzanie podpisów cyfrowych. Klasa `Signature` w GroupDocs.Signature for Java udostępnia metody do osadzania kodów HIBC jako podpisów cyfrowych. Podpisując PDF kodem HIBC, tworzysz weryfikowalny, niezmienny zapis, który może być skanowany w dowolnym miejscu łańcucha dostaw.

## Dlaczego używać razem Data Matrix i QR?
Data Matrix zajmuje najmniej miejsca, a jednocześnie może pomieścić do 2 335 znaków alfanumerycznych, co czyni go idealnym dla gęsto oznakowanych obszarów etykiet. Kody QR natomiast obsługują do 4 296 znaków i są powszechnie odczytywane przez smartfony. Połączenie obu zapewnia najlepszy kompromis między efektywnością przestrzeni a pojemnością danych, umożliwiając wszystkim interesariuszom — od skanerów magazynowych po aplikacje mobilne — odczytanie potrzebnych informacji.

## Wymagania wstępne
- **JDK 11 lub wyższy** (Java 8 działa, ale Java 11+ jest zalecana dla optymalnej wydajności).  
- **IDE** takie jak IntelliJ IDEA, Eclipse lub VS Code z rozszerzeniami Java.  
- **Maven lub Gradle** do zarządzania zależnościami (przykłady poniżej).  
- **Przykładowy PDF** (np. `sample.pdf`) do przetestowania implementacji.  
- **Ważna licencja GroupDocs.Signature** (bezpłatna wersja próbna do rozwoju, płatna licencja do produkcji).

## Konfiguracja GroupDocs.Signature for Java

### Konfiguracja Maven
Dodaj zależność do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Konfiguracja Gradle
Dla projektów Gradle dodaj to do swojego `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Opcja pobrania bezpośredniego
Możesz również pobrać plik JAR bezpośrednio z [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) i dodać go ręcznie do classpathu projektu. To podejście sprawdza się w środowiskach o ograniczonym dostępie do sieci.

### Uzyskanie licencji
Poproś o bezpłatną wersję próbną lub tymczasową licencję w GroupDocs, aby usunąć znaki wodne i odblokować wszystkie funkcje. Wdrożenia produkcyjne wymagają zakupionej licencji.

### Podstawowa inicjalizacja
`Signature` jest punktem wejścia dla wszystkich operacji podpisywania. Ładuje PDF, nakłada kod kreskowy i zapisuje podpisany plik.

```java
import com.groupdocs.signature.Signature;

class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("sample.pdf");
        // Proceed with signing operations...
    }
}
```

## Jak utworzyć PDF Data Matrix z kodem HIBC?
Utwórz obiekt `Signature` z plikiem źródłowym PDF, ustaw `QrCodeSignOptions` na format **Data Matrix**, podaj prawidłowo sformatowany ciąg HIBC i wywołaj `sign()`. Biblioteka zapisuje podpisany PDF w miejscu docelowym, zachowując układ i osadzając kod jako niezmienny podpis.

`QrCodeSignOptions` określa typ kodu, treść, rozmiar i położenie podpisu.

1. **Zaimportuj wymagane klasy** – dają dostęp do silnika podpisu i opcji Data Matrix.  

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
```

2. **Utwórz obiekt `Signature`** z pełnymi ścieżkami do plików źródłowego i docelowego.  

```java
String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY";
String destinFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithHIBCLICQR.pdf";

final Signature signature = new Signature(sourceFilePath);
```

3. **Skonfiguruj opcje Data Matrix** – ustaw ciąg HIBC, wybierz `QrCodeTypes.HIBCLICDataMatrix` i określ współrzędne położenia. `QrCodeTypes` wylicza obsługiwane formaty kodów dla podpisów HIBC.  

```java
QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR);
hibcLic_QR.setLeft(1); // Set the position from left
hibcLic_QR.setTop(1);   // Set the position from top
hibcLic_QR.setReturnContent(true); // Return content after signing
hibcLic_QR.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

4. **Zastosuj podpis** do PDF.  

```java
signature.sign(destinFilePath, hibcLic_QR);
```

5. **Zwolnij zasoby**, aby zamknąć uchwyty plików i uniknąć wycieków pamięci.  

```java
finally {
    if (signature != null) signature.dispose();
}
```

### Kompletny działający przykład
Oto pełny przepływ w jednym bloku (symboliczne miejsca zastąpisz rzeczywistym kodem z wcześniejszych fragmentów):

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

#### Bezpośrednia odpowiedź (40–70 słów)
Aby **utworzyć PDF Data Matrix**, utwórz `Signature` z plikiem źródłowym PDF, ustaw `QrCodeSignOptions` na `QrCodeTypes.HIBCLICDataMatrix` i podaj prawidłowo sformatowany ciąg HIBC, a następnie wywołaj `signature.sign(outputPath, options)`. Biblioteka zapisuje podpisany PDF w miejscu docelowym, zachowując układ i osadzając kod jako niezmienny podpis.

## Jak dodać kod QR do PDF przy użyciu GroupDocs.Signature?
Wczytaj PDF, skonfiguruj `QrCodeSignOptions` dla formatu QR i wywołaj `sign()`. Biblioteka skaluje obraz QR dla czytelności i pozycjonuje go zgodnie z podanymi współrzędnymi, unikając nakładania się na istniejącą treść. Dzięki temu kod pozostaje skanowalny po wydrukowaniu i spełnia standardy HIBC.

`QrCodeSignOptions` definiuje treść, rozmiar i pozycję kodu QR.

1. **Zaimportuj klasy specyficzne dla QR**  

```java
QrCodeSignOptions hibcLic_AZ = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec);
hibcLic_AZ.setLeft(1); // Set the position from left
hibcLic_AZ.setTop(200); // Set the position from top
hibcLic_AZ.setReturnContent(true); // Return content after signing
hibcLic_AZ.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

2. **Utwórz i skonfiguruj opcje QR** – zwróć uwagę na użycie `QrCodeTypes.HIBCLICQR`.  

```java
signature.sign(destinFilePath, hibcLic_AZ);
```

3. **Podpisz dokument**  

```java
QrCodeSignOptions hibcLic_DM = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix);
hibcLic_DM.setLeft(1); // Set the position from left
hibcLic_DM.setTop(400); // Set the position from top
hibcLic_DM.setReturnContent(true); // Return content after signing
hibcLic_DM.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

> **Bezpośrednia odpowiedź:** Użyj `QrCodeTypes.HIBCLICQR` w `QrCodeSignOptions`, ustaw ciąg HIBC, pozycjonuj kod metodami `setLeft()` i `setTop()`, a następnie wywołaj `signature.sign(outputPath, options)`. Kod QR zostanie osadzony natychmiast, gotowy do przechwycenia przez smartfon lub skaner.

## Typowe błędy, których należy unikać

### 1. Zapominanie o zwalnianiu zasobów
**Błąd:**  
```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  

**Poprawka:** Owiń użycie `Signature` w blok try‑with‑resources lub wywołaj `close()` w sekcji finally.

### 2. Używanie nieprawidłowych ciągów HIBC
**Błąd:** Używanie ogólnych ciągów jak „12345”.  
**Poprawka:** Stosuj standard HIBCC (np. `A123PROD30917/75#422011907#GP293`). Waliduj przy pomocy [HIBCC online validator](https://www.hibcc.org/).

### 3. Hard‑kodowanie ścieżek plików
**Błąd:**  
```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  

**Poprawka:** Przechowuj ścieżki w pliku konfiguracyjnym lub zmiennej środowiskowej i odczytuj je w czasie działania.

### 4. Ignorowanie konfliktów położenia kodów
Umieszczaj kody z dala od istniejącego tekstu lub podpisów. Używaj współrzędnych PDF (pochodzących z lewego dolnego rogu) i testuj na wydrukowanej próbce.

### 5. Brak testów na rzeczywistych skanerach
Wydrukuj podpisany PDF i zeskanuj go przy użyciu dokładnie tego sprzętu, który jest używany w Twoim procesie. Sprawdź czytelność przy różnych jakościach druku.

## Praktyczne zastosowania w opiece zdrowotnej

| Scenariusz | Zalecany kod kreskowy | Dlaczego pasuje |
|------------|----------------------|-----------------|
| **Dystrybucja leków** | QR Code | Wysoka pojemność danych, szeroko skanowany przez smartfony. |
| **Zarządzanie zapasami** | Data Matrix | Mały rozmiar, idealny dla gęstych etykiet półek. |
| **Zgodność regulacyjna (FDA 21 CFR Part 11)** | QR + Data Matrix | Format podwójny zapewnia redundancję i audytowalność. |
| **Śledzenie wyrobów medycznych** | Aztec Code | Kompaktowy rozmiar działa na ograniczonej przestrzeni opakowań. |

## Rozważania wydajnościowe i najlepsze praktyki

### Wzorzec przetwarzania wsadowego
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

- Twórz nową instancję `Signature` dla każdego pliku, aby utrzymać niskie zużycie pamięci.  
- Używaj stałej puli wątków (`Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() - 1)`) do przetwarzania równoległego, ale monitoruj rozmiar sterty, ponieważ każda instancja `Signature` trzyma cały PDF w pamięci.  

### Aktualizuj biblioteki
Wydania GroupDocs zwiększają prędkość przetwarzania nawet o **20 %** i dodają nowe funkcje zgodności HIBC. Planuj kwartalne przeglądy zależności.

### Buforowanie szablonów
Wczytaj szablon PDF raz, sklonuj go dla każdej wariacji kodu i podpisz klony. To zmniejsza I/O i przyspiesza przepływy o dużej objętości.

## Najczęściej zadawane pytania

**Q: Czy GroupDocs.Signature może podpisywać typy plików inne niż PDF?**  
A: Tak, obsługuje także DOCX, XLSX, PPTX, PNG, JPEG i TIFF przy użyciu tego samego API do podpisywania kodami.

**Q: Jak rozwiązać problem „Invalid barcode content”?**  
A: Sprawdź, czy ciąg HIBC dokładnie spełnia składnię HIBCC, użyj walidatora online i upewnij się, że używasz właściwej stałej `QrCodeTypes` dla wybranego formatu.

**Q: Jaka jest maksymalna pojemność danych dla każdego formatu HIBC?**  
A: QR ≈ 4 296 znaków alfanumerycznych, Aztec ≈ 3 832 cyfrowe / 3 067 alfanumerycznych, Data Matrix ≈ 3 116 cyfrowe / 2 335 alfanumerycznych. Trzymaj kody poniżej 200 znaków dla optymalnej niezawodności skanowania.

**Q: Czy można osadzić wiele typów kodów w jednym PDF?**  
A: Oczywiście. Utwórz osobne obiekty `QrCodeSignOptions` z różnymi pozycjami i wywołaj `signature.sign()` dla każdego. Upewnij się tylko, że się nie nakładają.

**Q: Czy potrzebne jest połączenie z internetem podczas podpisywania w czasie działania?**  
A: Nie. Po umieszczeniu JAR‑a w classpathie i aktywacji licencji wszystkie operacje odbywają się lokalnie.

## Dodatkowe zasoby

- [GroupDocs.Signature for Java Documentation](https://docs.groupdocs.com/signature/java/)  
- [API Reference Guide](https://reference.groupdocs.com/signature/java/)  
- [Latest Release Downloads](https://releases.groupdocs.com/signature/java/)  
- [Purchase License](https://purchase.groupdocs.com/buy)  
- [Get Free Trial](https://releases.groupdocs.com/signature/java/)  
- [Request Temporary License](https://purchase.groupdocs.com/temporary-license/)  
- [GroupDocs Forum](https://forum.groupdocs.com/c/signature/)  

---

**Ostatnia aktualizacja:** 2026-09-15  
**Testowane z:** GroupDocs.Signature 23.12 for Java  
**Autor:** GroupDocs  

---

## Powiązane samouczki

- [Create Barcode Signature PDF in Java – GroupDocs Guide](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)
- [Create Barcode Signature in Java – Update PDF Barcodes](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [How to read QR code PDF using Java and GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)
