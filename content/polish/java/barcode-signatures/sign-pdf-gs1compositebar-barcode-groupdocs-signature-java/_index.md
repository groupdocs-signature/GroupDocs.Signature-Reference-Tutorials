---
categories:
- Java PDF Processing
date: '2026-05-21'
description: Dowiedz się, jak utworzyć podpis kodu kreskowego w Javie dla plików PDF
  przy użyciu GroupDocs.Signature. Kompletny przewodnik z przykładami kodu, wskazówkami
  rozwiązywania problemów oraz rzeczywistymi przypadkami użycia do uwierzytelniania
  dokumentów.
keywords:
- create barcode signature java
- barcode signatures java
- pdf barcode signing java
lastmod: '2026-05-21'
linktitle: Podpisy kodów kreskowych PDF w Javie
schemas:
- author: GroupDocs
  dateModified: '2026-05-21'
  description: Learn how to create barcode signature Java for PDFs using GroupDocs.Signature.
    Complete guide with code examples, troubleshooting tips, and real-world use cases
    for document authentication.
  headline: How to Create Barcode Signature Java for PDF Documents
  type: TechArticle
- questions:
  - answer: A GS1CompositeBar combines linear and 2D components to store product IDs,
      serial numbers, and other data in a single scannable symbol, widely used in
      retail and logistics.
    question: What is a GS1CompositeBar barcode?
  - answer: Yes—GroupDocs.Signature supports over 60 types, including QR, Code128,
      DataMatrix, PDF417, and Aztec. Switch the `setEncodeType()` value to change
      the format.
    question: Can I use other barcode types besides GS1CompositeBar?
  - answer: A valid GroupDocs license is required for production deployments. A free
      trial is available for development and testing.
    question: Do I need a license for production use?
  - answer: Absolutely, provided the barcode is at least 200 × 100 px and has sufficient
      contrast. Smartphone scanning apps work on‑screen; hardware scanners work on
      printed copies.
    question: Will barcode scanners read barcodes from signed PDFs?
  - answer: Wrap your code in try‑catch blocks, log full stack traces, and always
      call `signature.dispose()` in a finally block to release resources.
    question: How do I handle errors during signing?
  type: FAQPage
tags:
- barcode-signatures
- pdf-signing
- document-authentication
- java-libraries
title: Jak utworzyć podpis kodu kreskowego w Javie dla dokumentów PDF
type: docs
url: /pl/java/barcode-signatures/sign-pdf-gs1compositebar-barcode-groupdocs-signature-java/
weight: 1
---

# Jak utworzyć podpis z kodem kreskowym w Javie dla dokumentów PDF

## Wprowadzenie

W tym samouczku dowiesz się, jak **create barcode signature Java** dla plików PDF przy użyciu GroupDocs.Signature. Niezależnie od tego, czy musisz osadzić kody produktów, identyfikatory audytu, czy jakiekolwiek dane strukturalne w umowie, podpisy kodów kreskowych pozwalają dodać informacje odczytywane maszynowo, które można zeskanować natychmiast, zachowując jednocześnie kryptograficzne bezpieczeństwo dokumentu. Przeprowadzimy Cię przez konfigurację, kod, dostosowanie i wskazówki najlepszych praktyk, abyś mógł zacząć dodawać podpisy kodów kreskowych do swoich PDF‑ów w kilka minut.

## Szybkie odpowiedzi
- **Jaka biblioteka dodaje podpisy kodów kreskowych w Javie?** GroupDocs.Signature for Java.
- **Jaki typ kodu kreskowego jest najlepszy dla handlu detalicznego?** `GS1CompositeBar` (standard branżowy do śledzenia produktów).
- **Czy potrzebna jest licencja do produkcji?** Tak – wymagana jest zakupiona licencja GroupDocs.
- **Czy mogę dodać zarówno podpis cyfrowy, jak i kod kreskowy?** Oczywiście; połącz je dla bezpieczeństwa i możliwości skanowania.
- **Czy kod jest kompatybilny z Java 11 i nowszymi?** Tak, API działa z JDK 8+.

## Co oznacza create barcode signature java?
`create barcode signature java` odnosi się do procesu programowego osadzania kodu kreskowego w PDF przy użyciu kodu Java. GroupDocs.Signature udostępnia prostą API, która generuje obraz kodu kreskowego, pozycjonuje go na stronie i zapisuje podpisany dokument w jednej płynnej operacji.

## Dlaczego używać podpisów z kodami kreskowymi?
Podpisy kodów kreskowych dostarczają **metadane odczytywane maszynowo** wewnątrz legalnie podpisanego PDF‑a. Umożliwiają natychmiastową weryfikację wizualną, usprawniają skanowanie w łańcuchu dostaw i pozwalają systemom downstream wyodrębniać dane strukturalne bez otwierania pliku. Obsługiwanych jest ponad 60 formatów kodów kreskowych, a GS1CompositeBar może kodować identyfikatory produktów, numery seryjne i kody partii w jednym zwartym symbolu — idealnym dla handlu detalicznego, opieki zdrowotnej i finansów.

## Wymagania wstępne

- **Java Development Kit:** JDK 8 lub nowszy (Java 11, 17, 21 wszystkie działają).
- **Narzędzie budowania:** Maven lub Gradle – wybierz to, które preferujesz.
- **IDE:** IntelliJ IDEA, Eclipse lub VS Code.
- **Biblioteka GroupDocs.Signature:** Dodaj zależność jak pokazano poniżej.
- **Licencja:** Bezpłatna wersja próbna do rozwoju; zakupiona licencja do produkcji.

### Dodawanie GroupDocs.Signature do projektu

**For Maven users**, add this to your `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**For Gradle users**, add this to your `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**About licensing:** GroupDocs offers a free trial that's perfect for testing and development. You can download it from their [releases page](https://releases.groupdocs.com/signature/java/). When you're ready for production, you'll need to purchase a license or request a temporary one from the [GroupDocs website](https://purchase.groupdocs.com/buy). For detailed API usage see the [API Reference](https://reference.groupdocs.com/signature/java/), consult the [Developer Guide](https://docs.groupdocs.com/signature/java/) for step‑by‑step instructions, and ask questions on the [GroupDocs Forum](https://forum.groupdocs.com/). The same purchase link is also listed as the [purchase page](https://purchase.groupdocs.com/buy).

## Jak skonfigurować GroupDocs.Signature w Javie?

Klasa `Signature` reprezentuje dokument i udostępnia metody do stosowania podpisów, wyszukiwania treści oraz zarządzania zasobami. Utwórz instancję `Signature`, aby otworzyć swój PDF i przygotować go do podpisywania. Klasa `Signature` jest podstawowym komponentem GroupDocs.Signature, który zarządza ładowaniem dokumentu, obsługą zasobów i przepływem pracy podpisywania, zapewniając, że wszystkie operacje są wykonywane bezpiecznie i wydajnie.

```java
import com.groupdocs.signature.Signature;

// Point to your PDF file
Signature signature = new Signature("path/to/your/document.pdf");
```

**Important:** Always dispose of the `Signature` object after use—this releases file handles and frees memory.

## Jak skonfigurować opcje podpisu kodu kreskowego?

Klasa `BarcodeSignOptions` definiuje każdy aspekt kodu kreskowego, który zamierzasz osadzić, od danych po styl wizualny. Działa jako kontener wszystkich ustawień związanych z kodem kreskowym, takich jak typ, rozmiar, kolory i położenie. Poniżej znajduje się minimalna konfiguracja, która tworzy kod GS1CompositeBar zawierający GTIN i numer seryjny, a także pokazuje, jak ustawić marginesy i kolory tła dla optymalnej czytelności.

```java
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

// Create barcode with GS1 format data
BarcodeSignOptions options = new BarcodeSignOptions("(01)03212345678906/(21)A1B2C3D4E5F6G7H8");
options.setEncodeType(BarcodeTypes.GS1CompositeBar);
```

Ciąg `"(01)03212345678906/(21)A1B2C3D4E5F6G7H8"` odpowiada standardowi GS1:
- `(01)` = GTIN (globalny identyfikator produktu)
- `03212345678906` = rzeczywisty kod produktu
- `(21)` = identyfikator numeru seryjnego
- `A1B2C3D4E5F6G7H8` = unikalny numer seryjny

Możesz go zamienić na dowolny tekst dla kodów QR, Code128, DataMatrix itp. Obsługiwanych jest ponad 60 typów kodów kreskowych — zobacz dokumentację GroupDocs, aby poznać pełną listę.

## Jak pozycjonować i dostosować kod kreskowy?

Pozycjonowanie i stylizacja są kontrolowane przez ten sam obiekt `BarcodeSignOptions`. Użyj `setTop`, `setLeft`, `setWidth` i `setHeight`, aby określić dokładne współrzędne i wymiary. Ustawienie `setAllPages(true)` dodaje kod kreskowy automatycznie na każdej stronie, natomiast `setPageNumber(1)` celuje w konkretną stronę. Możesz także obrócić kod, dodać kolor tła lub dostosować marginesy, aby kod nie nakładał się na istniejącą treść.

```java
// Set position and apply to all pages
options.setTop(200); // Set vertical position
options.setAllPages(true);
```

For more precise layout, you can also anchor the barcode to a specific page, rotate it, or add a background color:

```java
options.setLeft(100);        // 100 pixels from left edge
options.setTop(200);         // 200 pixels from top
options.setWidth(300);       // Barcode width in pixels
options.setHeight(100);      // Barcode height in pixels
options.setPageNumber(1);    // Only sign page 1 (removes setAllPages)
```

Visual customization (foreground/background colors, margins, text labels) is available via additional properties:

```java
options.setMargin(new Padding(10));           // Add padding around barcode
options.setBackground(new Background());       // Set background color
options.setForeColor(Color.BLACK);            // Barcode color
options.setBackgroundColor(Color.WHITE);      // Background color
```

## Jak podpisać dokument kodem kreskowym?

Metoda `sign` na instancji `Signature` stosuje skonfigurowane opcje i zapisuje podpisany dokument na dysku. Zwraca obiekt `SignResult`, który informuje, ile podpisów zostało zastosowanych i czy wystąpiły ostrzeżenia. Ta metoda obsługuje całą niskopoziomową manipulację PDF, więc nie musisz pracować bezpośrednio z bibliotekami PDF.

```java
try {
    SignResult signResult = signature.sign(outputPath, options);
    System.out.println("Document signed successfully!");
    System.out.println("Signed document saved to: " + outputPath);
} finally {
    if (signature != null) {
        signature.dispose();
    }
}
```

The surrounding try‑finally block guarantees the `Signature` object is disposed even if an exception occurs, preventing file‑handle leaks.

Możesz sprawdzić `SignResult`, aby potwierdzić sukces:

```java
if (signResult.getSucceeded().size() > 0) {
    System.out.println("Successfully added " + signResult.getSucceeded().size() + " signature(s)");
}
```

## Kompletny działający przykład

Łącząc wszystko razem, oto pojedyncza metoda, która ładuje PDF, dodaje kod GS1CompositeBar i zapisuje podpisany plik:

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

public class BarcodeSigningExample {
    
    public void signPdfWithBarcode(String inputPath, String outputPath) {
        Signature signature = null;
        
        try {
            // Initialize signature
            signature = new Signature(inputPath);
            
            // Configure barcode
            BarcodeSignOptions options = new BarcodeSignOptions(
                "(01)03212345678906/(21)A1B2C3D4E5F6G7H8"
            );
            options.setEncodeType(BarcodeTypes.GS1CompositeBar);
            options.setTop(200);
            options.setAllPages(true);
            
            // Sign and save
            SignResult result = signature.sign(outputPath, options);
            
            System.out.println("Signing completed: " + result.getSucceeded().size() + " signature(s) added");
            
        } catch (Exception e) {
            System.err.println("Error signing document: " + e.getMessage());
            e.printStackTrace();
        } finally {
            if (signature != null) {
                signature.dispose();
            }
        }
    }
}
```

This method is production‑ready: it validates input, manages resources, and reports the outcome.

## Jak dodać zarówno podpis cyfrowy, jak i kod kreskowy?

Dla maksymalnego bezpieczeństwa najpierw dodaj kryptograficzny podpis cyfrowy, a następnie nałóż kod kreskowy. Podpis cyfrowy gwarantuje integralność dokumentu, podczas gdy kod kreskowy zapewnia szybką weryfikację wizualną i dane odczytywane maszynowo. Użyj klasy `DigitalSignOptions` w pierwszym kroku, a potem zastosuj `BarcodeSignOptions` jak pokazano powyżej.

```java
// First, add digital signature
DigitalSignOptions digitalOptions = new DigitalSignOptions("certificate.pfx");
digitalOptions.setPassword("cert_password");
signature.sign(outputPath, digitalOptions);

// Then, add barcode on top
BarcodeSignOptions barcodeOptions = new BarcodeSignOptions("DATA");
barcodeOptions.setEncodeType(BarcodeTypes.QR);
signature.sign(outputPath, barcodeOptions);
```

Resulting PDF is both legally binding (digital signature) and instantly readable by any barcode scanner.

## Praca z różnymi typami kodów kreskowych

Zmiana formatu kodu kreskowego jest tak prosta, jak zmiana jednej wartości wyliczeniowej. Poniżej przykład, który zamienia GS1CompositeBar na kod QR:

```java
// Define barcode sign options with sample text
BarcodeSignOptions options = new BarcodeSignOptions("Sample Text");

// Assign specific barcode type
options.setEncodeType(BarcodeTypes.GS1CompositeBar);
```

A oto ta sama zmiana dla liniowego kodu Code128:

```java
options.setEncodeType(BarcodeTypes.QR);           // QR code
options.setEncodeType(BarcodeTypes.Code128);      // Code 128
options.setEncodeType(BarcodeTypes.DataMatrix);   // Data Matrix
```

Pamiętaj, że każdy typ kodu ma własne limity pojemności danych — kody QR mogą pomieścić tysiące znaków, podczas gdy Code39 jest ograniczony do znaków alfanumerycznych.

## Praktyczne przypadki użycia

### Zarządzanie łańcuchem dostaw
Osadzenie GS1CompositeBar na listach przewozowych pozwala pracownikom magazynu skanować numery zamówień, miejsca docelowe i kody partii bez otwierania PDF‑a.

```java
BarcodeSignOptions options = new BarcodeSignOptions(
    "(01)" + gtin + "/(21)" + serialNumber + "/(10)" + batchNumber
);
options.setEncodeType(BarcodeTypes.GS1CompositeBar);
```

### Dokumentacja medyczna
Kody QR na formularzach zgody mogą być skanowane, aby automatycznie archiwizować dokument pod właściwym rekordem pacjenta.

```java
String patientData = "PATIENT_ID:" + patientId + "|DOC_TYPE:CONSENT|DATE:" + dateString;
BarcodeSignOptions options = new BarcodeSignOptions(patientData);
options.setEncodeType(BarcodeTypes.QR);
```

### Usługi finansowe
Identyfikatory transakcji zakodowane w kodzie kreskowym umożliwiają audytorom weryfikację zgodności prostym skanowaniem.

```java
String complianceData = "TXN:" + transactionId + "|AGENT:" + agentId + "|BRANCH:" + branchCode;
BarcodeSignOptions options = new BarcodeSignOptions(complianceData);
options.setEncodeType(BarcodeTypes.PDF417);
```

### Kontrola jakości w produkcji
Raporty inspekcyjne podpisane kodami kreskowymi zawierającymi numery partii i identyfikatory inspektorów sprawiają, że analiza przyczynowa jest natychmiastowa.

```java
String qcData = "BATCH:" + batchNumber + "|INSPECTOR:" + inspectorId + "|RESULT:" + passFailStatus;
BarcodeSignOptions options = new BarcodeSignOptions(qcData);
options.setEncodeType(BarcodeTypes.DataMatrix);
```

## Typowe problemy implementacyjne

### Problem 1: wyjątek „Plik jest już używany”
**Answer:** The file remains locked if a previous `Signature` instance wasn’t disposed. Always wrap signing code in a try‑finally block and call `signature.dispose()`.

```java
Signature signature = null;
try {
    signature = new Signature(filePath);
    // ... your code ...
} finally {
    if (signature != null) {
        signature.dispose();
    }
}
```

### Problem 2: kod kreskowy nie pojawia się w PDF
**Answer:** Verify that `setTop`/`setLeft` values are within page bounds, increase the barcode’s width/height, and ensure foreground/background colors contrast with the page background.

```java
// Make sure dimensions are reasonable
options.setTop(100);      // Not 10000
options.setLeft(100);
options.setWidth(300);    // At least 200 pixels for readability
options.setHeight(100);

// Ensure contrast
options.setForeColor(Color.BLACK);
options.setBackgroundColor(Color.WHITE);
```

### Problem 3: wyjątek „Nieprawidłowe dane kodu kreskowego”
**Answer:** GS1 barcodes require strict parentheses notation. Use the correct Application Identifiers (e.g., `(01)`, `(21)`) and avoid unsupported characters.

```java
// Correct:
"(01)03212345678906/(21)ABC123"

// Incorrect:
"03212345678906ABC123"
```

### Problem 4: OutOfMemoryError przy dużych PDF
**Answer:** Increase the JVM heap (`-Xmx4G`) and consider signing pages individually instead of using `setAllPages(true)` for very large documents.

```bash
java -Xmx2G -jar your-application.jar
```

### Problem 5: skanowanie kodu kreskowego nie powodzi się
**Answer:** Ensure the barcode is at least 200 × 100 px, uses high contrast colors, and isn’t distorted by PDF compression.

```java
// Increase size
options.setWidth(400);
options.setHeight(150);

// Maximize contrast
options.setForeColor(Color.BLACK);
options.setBackgroundColor(Color.WHITE);

// Add quiet zone (blank space around barcode)
options.setMargin(new Padding(10));
```

## Bezpieczeństwo i weryfikacja

### Czy podpisy z kodami kreskowymi są bezpieczne?
Sam kod kreskowy nie jest chroniony kryptograficznie, więc każdy może wygenerować nowy. Połącz go z podpisem cyfrowym, aby zapewnić zarówno autentyczność, jak i możliwość skanowania. Wzorzec podwójnego podpisu (najpierw cyfrowy, potem kod kreskowy) daje wymagalność prawną oraz wygodę operacyjną.

### Weryfikacja danych kodu kreskowego
Po zeskanowaniu zweryfikuj, czy cyfrowy podpis dokumentu nadal jest ważny i czy ładunek kodu kreskowego odpowiada oczekiwanym wzorcom. Użyj API `search()` z `BarcodeSearchOptions`, aby automatycznie wyodrębnić i zweryfikować zawartość kodu kreskowego.

```java
public boolean validateScannedBarcode(String scannedData, String documentPath) {
    // Verify digital signature first
    if (!verifyDigitalSignature(documentPath)) {
        return false;
    }
    
    // Validate barcode format
    if (!scannedData.matches("(01)\\d{14}/(21)[A-Z0-9]+")) {
        return false;
    }
    
    // Check against database
    String productId = extractProductId(scannedData);
    return database.productExists(productId);
}
```

## Rozważania dotyczące wydajności

### Zarządzanie zasobami
Always dispose of `Signature` objects after each operation to avoid memory leaks:

```java
signature.dispose();
```

When processing many files, create and dispose a new `Signature` per document:

```java
for (String filePath : documentPaths) {
    Signature signature = null;
    try {
        signature = new Signature(filePath);
        // ... signing logic ...
    } finally {
        if (signature != null) {
            signature.dispose();
        }
    }
}
```

### Przetwarzanie wsadowe
For small batches (< 100 files), sequential processing is simple:

```java
for (String path : paths) {
    signDocument(path);
}
```

For larger workloads, parallel processing can speed things up—but monitor I/O pressure and limit threads to 4‑8:

```java
paths.parallelStream().forEach(path -> signDocument(path));
```

### Optymalizacja pamięci dla dużych PDF
Increase heap size, process pages individually, and clear references after each step. This prevents `OutOfMemoryError` on documents larger than 50 MB.

### Buforowanie opcji kodu kreskowego
If you reuse the same barcode configuration across many files, cache the `BarcodeSignOptions` instance:

```java
// Create once, reuse many times
private static BarcodeSignOptions createStandardBarcodeOptions(String data) {
    BarcodeSignOptions options = new BarcodeSignOptions(data);
    options.setEncodeType(BarcodeTypes.GS1CompositeBar);
    options.setTop(200);
    options.setAllPages(true);
    return options;
}
```

## Zaawansowane funkcje

### Wiele podpisów w jednym dokumencie
Add several barcodes (or mix with digital signatures) by calling `sign` multiple times with different option objects:

```java
// Add QR code in top-left
BarcodeSignOptions qrOptions = new BarcodeSignOptions("https://example.com");
qrOptions.setEncodeType(BarcodeTypes.QR);
qrOptions.setTop(50);
qrOptions.setLeft(50);
signature.sign(outputPath, qrOptions);

// Add GS1 barcode in bottom-right
BarcodeSignOptions gs1Options = new BarcodeSignOptions("(01)03212345678906");
gs1Options.setEncodeType(BarcodeTypes.GS1CompositeBar);
gs1Options.setTop(700);
gs1Options.setLeft(400);
signature.sign(outputPath, gs1Options);
```

### Dynamiczna zawartość kodu kreskowego
Generate barcode data from document metadata, timestamps, or database lookups:

```java
// Extract data from PDF or database
String orderId = extractOrderIdFromPdf(filePath);
String timestamp = LocalDateTime.now().format(DateTimeFormatter.ISO_DATE_TIME);
String barcodeData = String.format("ORDER:%s|TIME:%s", orderId, timestamp);

BarcodeSignOptions options = new BarcodeSignOptions(barcodeData);
```

### Integracja ze Spring Boot
Expose a REST endpoint that receives a PDF, adds a barcode, and returns the signed file:

```java
@Service
public class DocumentSigningService {
    public void signWithBarcode(MultipartFile file, String barcodeData) {
        // ... implementation ...
    }
}
```

### Przykład REST API
A minimal controller that delegates to the signing service:

```java
@PostMapping("/sign-document")
public ResponseEntity<byte[]> signDocument(
    @RequestParam("file") MultipartFile file,
    @RequestParam("barcode") String barcodeData
) {
    // Sign document and return as byte array
}
```

## Najczęściej zadawane pytania

**Q: What is a GS1CompositeBar barcode?**  
A: A GS1CompositeBar combines linear and 2D components to store product IDs, serial numbers, and other data in a single scannable symbol, widely used in retail and logistics.

**Q: Can I use other barcode types besides GS1CompositeBar?**  
A: Yes—GroupDocs.Signature supports over 60 types, including QR, Code128, DataMatrix, PDF417, and Aztec. Switch the `setEncodeType()` value to change the format.

**Q: Do I need a license for production use?**  
A: A valid GroupDocs license is required for production deployments. A free trial is available for development and testing.

**Q: Will barcode scanners read barcodes from signed PDFs?**  
A: Absolutely, provided the barcode is at least 200 × 100 px and has sufficient contrast. Smartphone scanning apps work on‑screen; hardware scanners work on printed copies.

**Q: How do I handle errors during signing?**  
A: Wrap your code in try‑catch blocks, log full stack traces, and always call `signature.dispose()` in a finally block to release resources.

**Q: Can I sign other document formats?**  
A: Yes—GroupDocs.Signature also supports DOCX, XLSX, PPTX, images, and many more. Just change the input file extension; the API remains the same.

**Q: Are there file‑size limits?**  
A: No hard limit, but documents over 50 MB may require a larger JVM heap and page‑by‑page processing to stay memory‑efficient.

**Q: How do I sign PDFs stored in cloud storage?**  
A: Download the file to a temporary local path, apply the signature, then upload it back to your cloud bucket. Clean up temporary files afterward.

## Podsumowanie

Masz teraz kompletny, gotowy do produkcji przewodnik, jak **create barcode signature java** dla dokumentów PDF. Łącząc kryptograficzne podpisy cyfrowe z maszynowo odczytywanymi kodami kreskowymi, osiągasz zarówno prawne wymogi, jak i efektywność operacyjną w łańcuchu dostaw, opiece zdrowotnej, finansach i produkcji. Eksperymentuj z różnymi typami kodów, integruj kod z istniejącymi usługami i rozważ przetwarzanie wsadowe dla dużych wdrożeń.

---

**Last Updated:** 2026-05-21  
**Tested With:** GroupDocs.Signature 23.10 for Java  
**Author:** GroupDocs  

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY" + "/sample.pdf";
String fileName = new java.io.File(filePath).getName();
String outputPath = "YOUR_OUTPUT_DIRECTORY" + "/SignedWithBarcodeGS1CompositeBar/" + fileName;
```

```java
String documentDir = System.getenv("DOCUMENT_DIR");
String outputDir = System.getenv("OUTPUT_DIR");
```

```java
Signature signature = new Signature(filePath);
```

## Powiązane samouczki

- [Create Barcode Signature in Java – Update PDF Barcodes](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [Verify Barcode & QR Code in Java - Complete Document Security Guide](/signature/java/search-verification/verify-barcode-qr-code-signatures-groupdocs-java/)
- [HIBC Barcode PDF Signing with Java - Complete Healthcare Document Solution](/signature/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/)