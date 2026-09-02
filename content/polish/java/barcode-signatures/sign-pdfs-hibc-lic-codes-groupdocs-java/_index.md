---
categories:
- Document Signing
- Healthcare Integration
date: '2026-05-16'
description: Dowiedz się, jak tworzyć PDF Data Matrix i dodawać PDF z kodem QR przy
  użyciu GroupDocs.Signature for Java. Przewodnik krok po kroku dotyczący podpisywania
  dokumentów medycznych.
keywords:
- create data matrix pdf
- add qr code pdf
- HIBC barcode Java
lastmod: '2026-05-16'
linktitle: Przewodnik podpisywania PDF HIBC w Javie
schemas:
- author: GroupDocs
  dateModified: '2026-05-16'
  description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  headline: Create Data Matrix PDF with HIBC Barcode in Java
  type: TechArticle
- description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  name: Create Data Matrix PDF with HIBC Barcode in Java
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
- java
- pdf-signing
- hibc
- healthcare
- barcode
- pharmaceutical
title: Tworzenie PDF Data Matrix z kodem kreskowym HIBC w Javie
type: docs
url: /pl/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/
weight: 1
---

# Utwórz PDF Data Matrix z kodem kreskowym HIBC w Javie

Jeśli tworzysz oprogramowanie do logistyki farmaceutycznej lub opieki zdrowotnej, prawdopodobnie natknąłeś się na problemy związane z papierowym śledzeniem, utraconymi podpisami i koszmarami audytowymi. **Tworzenie PDF Data Matrix**, który zawiera kod kreskowy HIBC LIC, rozwiązuje te problemy, zapewniając niezmienny, maszynowo odczytywalny ślad, który przetrwa drukowanie, skanowanie i przegląd regulacyjny. W tym samouczku zobaczysz dokładnie, jak **dodać obsługę PDF z kodem QR**, a także formaty Aztec i Data Matrix, używając GroupDocs.Signature for Java.

## Szybkie odpowiedzi
- **Jaką bibliotekę obsługuje kody kreskowe HIBC w Javie?** GroupDocs.Signature for Java.  
- **Jaki format kodu kreskowego jest najbardziej kompaktowy?** Data Matrix – idealny dla małych etykiet.  
- **Czy mogę dodać zarówno QR, jak i Data Matrix do tego samego PDF?** Tak, wystarczy utworzyć osobne `QrCodeSignOptions`.  
- **Czy potrzebuję połączenia internetowego w czasie działania?** Nie, biblioteka działa w pełni offline po instalacji.  
- **Jaką wersję Javy zaleca się?** Java 11+ dla wydajności klasy produkcyjnej.

## Co to jest podpisywanie PDF kodem kreskowym HIBC?
Klasa `Signature` w GroupDocs.Signature for Java reprezentuje dokument PDF i udostępnia metody do osadzania kodów kreskowych HIBC jako podpisów cyfrowych. Podpisując PDF kodem kreskowym HIBC, tworzysz weryfikowalny, niezmienny zapis, który może być skanowany w dowolnym punkcie łańcucha dostaw.

## Dlaczego używać razem Data Matrix i kodów QR?
GroupDocs.Signature obsługuje **ponad 50 formatów wejściowych i wyjściowych** i może przetwarzać wielostronicowe PDF‑y bez ładowania całego pliku do pamięci. Używanie Data Matrix dla gęstych, małych etykiet oraz QR dla większych dokumentów zapewnia najlepszy balans czytelności, pojemności danych (do 4 296 znaków dla QR) i efektywności wykorzystania przestrzeni druku.

## Wymagania wstępne
- **JDK 11 lub wyższy** (Java 8 działa, ale Java 11+ jest zalecana dla optymalnej wydajności).  
- **IDE** takie jak IntelliJ IDEA, Eclipse lub VS Code z rozszerzeniami Java.  
- **Maven lub Gradle** do zarządzania zależnościami (przykłady poniżej).  
- **Przykładowy PDF** (np. `sample.pdf`) do przetestowania implementacji.  
- **Ważna licencja GroupDocs.Signature** (bezpłatna wersja próbna do rozwoju, płatna licencja do produkcji).

## Konfiguracja GroupDocs.Signature dla Javy

### Konfiguracja Maven
Add the dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Konfiguracja Gradle
For Gradle projects, add this to your `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Opcja bezpośredniego pobrania
Możesz również pobrać plik JAR bezpośrednio z [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) i dodać go ręcznie do ścieżki klas swojego projektu. To podejście sprawdza się dobrze w środowiskach o ograniczonym dostępie do sieci.

### Uzyskanie licencji
Poproś o bezpłatną wersję próbną lub tymczasową licencję od GroupDocs, aby usunąć znaki wodne i odblokować wszystkie funkcje. Wdrożenia produkcyjne wymagają zakupionej licencji.

### Podstawowa inicjalizacja
Klasa `Signature` jest punktem wejścia dla wszystkich operacji podpisywania. Ładuje PDF, nakłada kod kreskowy i zapisuje podpisany plik.

```java
import com.groupdocs.signature.Signature;

class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("sample.pdf");
        // Proceed with signing operations...
    }
}
```

## Jak utworzyć PDF Data Matrix z kodem kreskowym HIBC?
Załaduj swój źródłowy PDF, skonfiguruj obiekt `QrCodeSignOptions` dla formatu Data Matrix i wywołaj `sign()` – to wszystko, czego potrzebujesz, aby osadzić zgodny kod kreskowy HIBC Data Matrix. Poniższe kroki przeprowadzą Cię przez dokładny wymagany kod. `QrCodeSignOptions` definiuje ustawienia podpisu kodu kreskowego, takie jak typ, zawartość, rozmiar i pozycja.

1. **Importuj wymagane klasy** – zapewniają dostęp do silnika podpisu i opcji Data Matrix.  

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
```

2. **Utwórz obiekt `Signature`** z bezwzględnymi ścieżkami do plików źródłowego i docelowego.  

```java
String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY";
String destinFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithHIBCLICQR.pdf";

final Signature signature = new Signature(sourceFilePath);
```

3. **Skonfiguruj opcje Data Matrix** – ustaw ciąg HIBC, wybierz `QrCodeTypes.HIBCLICDataMatrix` i określ współrzędne położenia. `QrCodeTypes` wymienia obsługiwane formaty kodów kreskowych dla podpisów HIBC.  

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

5. **Zwolnij zasoby**, aby zwolnić uchwyty plików i uniknąć wycieków pamięci.  

```java
finally {
    if (signature != null) signature.dispose();
}
```

### Kompletny działający przykład
Oto pełny przepływ w jednym bloku (placeholdery reprezentują dokładny kod, który wkleisz z wcześniejszych fragmentów):

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
Aby **utworzyć PDF Data Matrix**, utwórz instancję `Signature` z Twoim źródłowym PDF, ustaw `QrCodeSignOptions` na `QrCodeTypes.HIBCLICDataMatrix` i podaj prawidłowo sformatowany ciąg HIBC, a następnie wywołaj `signature.sign(outputPath, options)`. Biblioteka zapisuje podpisany PDF w miejscu docelowym, zachowując układ i osadzając kod kreskowy jako niezmienny podpis.

## Jak dodać QR code PDF przy użyciu GroupDocs.Signature?
Załaduj PDF, skonfiguruj `QrCodeSignOptions` dla formatu QR i wywołaj `sign()`. Ten dwuliniowy wzorzec działa dla dowolnego rozmiaru PDF i automatycznie skalowuje obraz QR dla optymalnej czytelności. `QrCodeSignOptions` konfiguruje podpis kodu QR, w tym jego zawartość i właściwości wizualne. Pozycjonuje kod na podstawie ustawionych współrzędnych, zapewniając, że nie nakłada się na istniejącą treść i pozostaje skanowalny po wydrukowaniu.

1. **Importuj klasy specyficzne dla QR**  

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

> **Bezpośrednia odpowiedź:** Użyj `QrCodeTypes.HIBCLICQR` w `QrCodeSignOptions`, ustaw ciąg zawartości HIBC, pozycjonuj kod za pomocą `setLeft()` i `setTop()`, a następnie wywołaj `signature.sign(outputPath, options)`. Kod QR zostaje natychmiast osadzony, gotowy do przechwycenia przez smartfon lub skaner.

## Częste błędy do uniknięcia

### 1. Zapomnienie o zwolnieniu zasobów
**Błędny:**  

```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  

**Poprawka:** Owiń użycie `Signature` w blok try‑with‑resources lub wywołaj `close()` w bloku finally.

### 2. Używanie nieprawidłowych ciągów formatu HIBC
**Błędny:** Używanie ogólnych ciągów jak “12345”.  
**Poprawka:** Postępuj zgodnie ze standardem HIBCC (np. `A123PROD30917/75#422011907#GP293`). Zweryfikuj przy użyciu [HIBCC online validator](https://www.hibcc.org/).

### 3. Hard‑kodowanie ścieżek plików
**Błędny:**  
```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  

**Poprawka:** Przechowuj ścieżki w pliku konfiguracyjnym lub zmiennej środowiskowej i odczytuj je w czasie działania.

### 4. Ignorowanie konfliktów pozycji kodu kreskowego
Umieszczaj kody kreskowe z dala od istniejącego tekstu lub podpisów. Używaj współrzędnych PDF (pochodzenie w lewym dolnym rogu) i testuj na wydrukowanej próbce.

### 5. Brak testów na rzeczywistych skanerach
Wydrukuj podpisany PDF i zeskanuj go przy użyciu dokładnie tego sprzętu, który jest używany w Twoim procesie. Zweryfikuj czytelność przy różnych jakościach druku.

## Praktyczne zastosowania w opiece zdrowotnej

| Scenariusz | Zalecany kod kreskowy | Dlaczego pasuje |
|------------|-----------------------|-----------------|
| **Dystrybucja farmaceutyczna** | QR Code | Wysoka pojemność danych, szeroko skanowany przez smartfony. |
| **Zarządzanie zapasami** | Data Matrix | Mały rozmiar, idealny dla gęstych etykiet półkowych. |
| **Zgodność regulacyjna (FDA 21 CFR Part 11)** | QR + Data Matrix | Podwójny format zapewnia redundancję i możliwość audytu. |
| **Śledzenie wyrobów medycznych** | Aztec Code | Kompaktowy rozmiar działa na opakowaniach o ograniczonej przestrzeni. |

## Rozważania dotyczące wydajności i najlepsze praktyki

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

- Utwórz nową instancję `Signature` dla każdego pliku, aby utrzymać niskie zużycie pamięci.  
- Użyj stałej puli wątków (`Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() - 1)`) do przetwarzania równoległego, ale monitoruj rozmiar sterty, ponieważ każda `Signature` trzyma pełny PDF w pamięci.

### Aktualizuj biblioteki
Wydania GroupDocs zwiększają prędkość przetwarzania nawet o **20 %** i dodają nowe funkcje zgodności HIBC. Planuj kwartalne kontrole zależności.

### Buforowanie szablonów
Załaduj szablon PDF raz, sklonuj go dla każdej wariacji kodu kreskowego i podpisz klony. To zmniejsza I/O i przyspiesza przepływy pracy o dużej objętości.

## Najczęściej zadawane pytania

**Q: Czy GroupDocs.Signature może podpisywać typy plików inne niż PDF?**  
A: Tak, obsługuje również DOCX, XLSX, PPTX, PNG, JPEG i TIFF przy użyciu tego samego API do podpisywania kodów kreskowych.

**Q: Jak rozwiązać problemy z błędami „Invalid barcode content”?**  
A: Zweryfikuj, czy Twój ciąg HIBC spełnia dokładną składnię HIBCC, użyj walidatora online i upewnij się, że używasz właściwej stałej `QrCodeTypes` dla wybranego formatu.

**Q: Jaka jest maksymalna pojemność danych dla każdego formatu HIBC?**  
A: QR ≈ 4 296 znaków alfanumerycznych, Aztec ≈ 3 832 numerycznych / 3 067 alfanumerycznych, Data Matrix ≈ 3 116 numerycznych / 2 335 alfanumerycznych. Trzymaj kody poniżej 200 znaków dla optymalnej niezawodności skanowania.

**Q: Czy można osadzić wiele typów kodów kreskowych w jednym PDF?**  
A: Oczywiście. Utwórz osobne obiekty `QrCodeSignOptions` z różnymi pozycjami i wywołaj `signature.sign()` dla każdego. Upewnij się tylko, że się nie nakładają.

**Q: Czy potrzebuję połączenia internetowego do podpisywania w czasie działania?**  
A: Nie. Po umieszczeniu JAR-a w ścieżce klas i aktywacji licencji wszystkie operacje są wykonywane lokalnie.

## Dodatkowe zasoby

- [Dokumentacja GroupDocs.Signature for Java](https://docs.groupdocs.com/signature/java/)  
- [Przewodnik po API](https://reference.groupdocs.com/signature/java/)  
- [Najnowsze pobrania wersji](https://releases.groupdocs.com/signature/java/)  
- [Zakup licencji](https://purchase.groupdocs.com/buy)  
- [Uzyskaj bezpłatną wersję próbną](https://releases.groupdocs.com/signature/java/)  
- [Poproś o tymczasową licencję](https://purchase.groupdocs.com/temporary-license/)  
- [Forum GroupDocs](https://forum.groupdocs.com/c/signature/)

---

**Ostatnia aktualizacja:** 2026-05-16  
**Testowano z:** GroupDocs.Signature 23.12 for Java  
**Autor:** GroupDocs  

```java
signature.sign(destinFilePath, hibcLic_DM);
```

## Powiązane samouczki

- [Utwórz podpis kodu kreskowego PDF w Javie – Przewodnik GroupDocs](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)
- [Utwórz podpis kodu kreskowego w Javie – Aktualizacja kodów kreskowych PDF](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [Jak odczytać QR code PDF przy użyciu Javy i GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)