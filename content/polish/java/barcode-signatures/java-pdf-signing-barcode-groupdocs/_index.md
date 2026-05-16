---
categories:
- Java PDF Processing
date: '2026-03-06'
description: Dowiedz się, jak tworzyć podpisy w postaci kodu kreskowego w dokumentach
  PDF przy użyciu języka Java i GroupDocs.Signature. Szczegółowy samouczek krok po
  kroku z przykładami kodu i najlepszymi praktykami.
keywords: sign PDF with barcode Java, Java barcode signature, GroupDocs PDF signing,
  Code128 barcode PDF, add barcode to PDF programmatically
lastmod: '2026-03-06'
linktitle: Create Barcode Signature Java
tags:
- pdf-signing
- barcode-signature
- document-security
- groupdocs
title: Jak utworzyć podpis z kodem kreskowym w PDF przy użyciu Javy
type: docs
url: /pl/java/barcode-signatures/java-pdf-signing-barcode-groupdocs/
weight: 1
---

# Jak utworzyć podpis z kodem kreskowym w PDF przy użyciu Javy

W tym samouczku dowiesz się, jak **utworzyć podpis z kodem kreskowym** w plikach PDF przy użyciu Javy i GroupDocs.Signature. Podpisy z kodem kreskowym osadzają identyfikatory odczytywanych maszynowo, które są jednocześnie odporne na manipulacje i łatwe do zeskanowania — idealne do umów, certyfikatów, faktur i wszelkich dokumentów wymagających niezawodnej weryfikacji.

## Szybkie odpowiedzi
- **Co to jest podpis z kodem kreskowym?** Kod kreskowy osadzony w pliku PDF, który przechowuje ustrukturyzowane dane i może być odczytany przez skanery lub oprogramowanie.  
- **Jaki typ kodu kreskowego jest zalecany?** Code128, ponieważ kompaktowo obsługuje dane alfanumeryczne.  
- **Czy potrzebna jest licencja?** Bezpłatna wersja próbna wystarczy do testów — kup pełną licencję, aby używać w produkcji.  
- **Czy mogę umieścić kod kreskowy na dowolnym rozmiarze strony?** Tak — użyj pozycjonowania opartego na procentach, aby uzyskać automatyczne skalowanie.  
- **Czy kod kreskowy jest wektorowy?** Tak, dodaje jedynie kilka kilobajtów do PDF‑a i pozostaje ostry przy każdej rozdzielczości.  

## Dlaczego podpisy z kodem kreskowym są ważne dla Twoich PDF‑ów

Oto wyzwanie, z którym prawdopodobnie się spotkałeś: musisz dodać unikalne identyfikatory do plików PDF, które są zarówno odczytywalne maszynowo, jak i odporne na manipulacje. Być może pracujesz nad systemem zarządzania dokumentami, przetwarzasz certyfikaty lub obsługujesz umowy wymagające późniejszej weryfikacji.

Właśnie tutaj przydają się podpisy z kodem kreskowym. W przeciwieństwie do prostych pieczątek tekstowych, kody kreskowe pozwalają osadzić ustrukturyzowane dane, które skanery (i Twoje oprogramowanie) mogą odczytać natychmiast. Dodatkowo, gdy połączysz je z podpisywaniem PDF‑ów przy użyciu GroupDocs.Signature dla Javy, otrzymujesz potężny sposób na śledzenie i weryfikację dokumentów bez konieczności dodawania skomplikowanych zapytań do bazy danych.

W tym przewodniku dowiesz się dokładnie, jak wdrożyć podpisy z kodem kreskowym w swoich PDF‑ach Java — od podstawowej konfiguracji po kod gotowy do produkcji z elastycznym pozycjonowaniem. Niezależnie od tego, czy tworzysz system fakturowania, generator certyfikatów czy platformę zarządzania umowami, po zakończeniu będziesz mieć wszystko, czego potrzebujesz.

**Czego się nauczysz:**
- Szybka konfiguracja GroupDocs.Signature dla Javy  
- Tworzenie podpisów z kodem kreskowym Code128 (i dlaczego jest to często najlepszy wybór)  
- Pozycjonowanie kodów kreskowych przy użyciu układów opartych na procentach, działających na dowolnym rozmiarze PDF  
- Unikanie typowych pułapek, które mogą zaskoczyć programistów  
- Poprawne testowanie implementacji  

## Co będzie potrzebne przed rozpoczęciem

Upewnij się, że masz gotowe następujące niezbędne elementy:

**Wymagane biblioteki:**
- GroupDocs.Signature dla Javy (zalecana wersja 23.12 lub nowsza)

**Środowisko programistyczne:**
- Zainstalowany JDK 8 lub nowszy  
- Ulubione IDE (IntelliJ IDEA, Eclipse lub VS Code z rozszerzeniami Java)  
- Maven lub Gradle do zarządzania zależnościami

**Poziom umiejętności:**
Powinieneś być zaznajomiony z podstawową składnią Javy i znać operacje na plikach. Jeśli potrafisz stworzyć prostą klasę Java i obsłużyć wyjątki, jesteś gotowy do działania.

## Konfiguracja GroupDocs.Signature w Twoim projekcie

Dodanie biblioteki do projektu jest proste. Wybierz narzędzie budowania:

**Dla użytkowników Maven**, dodaj to do swojego `pom.xml`:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Używasz Gradle?** Dodaj tę linię do swojego `build.gradle`:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Preferujesz ręczną konfigurację?** Pobierz plik JAR bezpośrednio z [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) i dodaj go do classpath.

### Uzyskanie licencji

Zanim przejdziesz do pełnej produkcji, musisz zająć się licencjonowaniem:

- **Bezpłatna wersja próbna:** Idealna do testów — pobierz ją ze strony GroupDocs, aby wypróbować podstawowe funkcje  
- **Licencja tymczasowa:** Potrzebujesz więcej czasu na ocenę? Złóż wniosek o 30‑dniową licencję tymczasową  
- **Pełna licencja:** Gotowy do produkcji? Kup licencję na nieograniczone użycie  

Oto szybki test, aby upewnić się, że wszystko działa:
```java
import com.groupdocs.signature.Signature;

public class QuickTest {
    public static void main(String[] args) {
        try {
            Signature signature = new Signature("test-document.pdf");
            System.out.println("GroupDocs.Signature is ready to go!");
        } catch (Exception e) {
            System.err.println("Setup issue: " + e.getMessage());
        }
    }
}
```

Jeśli uruchomi się bez błędów, wszystko gotowe!

## Jak utworzyć podpis z kodem kreskowym w Javie

Teraz przychodzi ciekawa część — podpiszmy PDF kodem kreskowym. Podzielimy to na małe kroki, abyś dokładnie rozumiał, co dzieje się na każdym etapie.

### Krok 1: Inicjalizacja obiektu Signature

Najpierw musisz poinformować GroupDocs, z którym plikiem PDF pracujesz:
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
Signature signature = new Signature(filePath);
```

**Co się tutaj dzieje:** Obiekt `Signature` ładuje Twój PDF do pamięci i przygotowuje go do modyfikacji. Upewnij się, że ścieżka do pliku jest poprawna — częstym problemem jest używanie odwrotnych ukośników w Windows bez ich escapowania (użyj `\\` lub po prostu ukośników `/`, które działają na wszystkich platformach).

### Krok 2: Konfiguracja opcji kodu kreskowego (Jak dodać kod kreskowy)

Teraz utwórzmy podpis z kodem kreskowym przy użyciu Twoich danych:
```java
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

BarcodeSignOptions options = new BarcodeSignOptions("12345678");
options.setEncodeType(BarcodeTypes.Code128);
```

**Rozbicie na części:**  
- `"12345678"` to dane Twojego kodu kreskowego — może to być numer zamówienia, numer certyfikatu lub dowolny potrzebny identyfikator  
- `Code128` to typ kodowania (więcej o wyborze odpowiedniego typu poniżej)

**Porada:** Code128 obsługuje zarówno liczby, jak i litery, co czyni go uniwersalnym w większości przypadków użycia. Jeśli potrzebujesz tylko liczb, `Code39` może być prostszy, ale Code128 zapewnia większą elastyczność.

### Krok 3: Pozycjonowanie kodu kreskowego (Jak podpisać PDF kodem kreskowym)

Tutaj GroupDocs naprawdę błyszczy — pozycjonowanie oparte na procentach sprawia, że kod kreskowy wygląda dobrze na każdym rozmiarze PDF:
```java
import com.groupdocs.signature.domain.enums.MeasureType;
import com.groupdocs.signature.domain.Padding;

// Use percentages instead of fixed pixels
options.setLocationMeasureType(MeasureType.Percents);
options.setLeft(5);  // 5% from the left edge
options.setTop(5);   // 5% from the top

// Size it proportionally too
options.setSizeMeasureType(MeasureType.Percents);
options.setWidth(10);  // 10% of page width
options.setHeight(5);  // 5% of page height

// Add some breathing room with margins
Padding margins = new Padding();
margins.setLeft(1);
margins.setTop(1);
margins.setRight(1);
options.setMargin(margins);
```

**Dlaczego procenty mają znaczenie:** Wyobraź sobie, że podpisujesz zarówno dokumenty A4, jak i formularze w formacie legal. Dzięki pozycjonowaniu procentowemu Twój kod kreskowy automatycznie skaluje się, aby wyglądał spójnie w obu przypadkach. Użycie stałych wartości w pikselach spowodowałoby, że kod będzie za mały w dużych dokumentach lub za duży w małych.

**Przykład z życia:** Na stronie A4 (595 × 842 punktów) kod o szerokości 10 % będzie miał około 60 punktów. Na stronie legal (612 × 1008 punktów) będzie miał około 61 punktów — automatycznie proporcjonalnie.

### Krok 4: Podpisz i zapisz dokument (Jak dodać kod kreskowy do PDF)

Czas faktycznie zastosować podpis i zapisać swoją pracę:
```java
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithPercents/sample_signed.pdf";
signature.sign(outputFilePath, options);
```

**Ważna uwaga:** Katalog wyjściowy musi istnieć przed uruchomieniem tego kodu. GroupDocs nie utworzy dla Ciebie zagnieżdżonych katalogów, więc utwórz je wcześniej lub obsłuż to w swoim kodzie:
```java
Path outputPath = Paths.get(outputFilePath);
Files.createDirectories(outputPath.getParent());
signature.sign(outputFilePath, options);
```

**Co zrobić, gdy coś pójdzie nie tak?** Owiń to w blok try‑catch:
```java
try {
    signature.sign(outputFilePath, options);
    System.out.println("PDF signed successfully at: " + outputFilePath);
} catch (Exception e) {
    System.err.println("Signing failed: " + e.getMessage());
    e.printStackTrace();
}
```

## Wybór odpowiedniego typu kodu kreskowego dla Twoich potrzeb (code128 pdf barcode)

GroupDocs obsługuje wiele formatów kodów kreskowych, a wybór odpowiedniego ma znaczenie. Oto praktyczne porównanie:

**Code128 (Nasza domyślna opcja):**  
- **Najlepszy dla:** Mieszanych danych alfanumerycznych (identyfikatory typu "INV2024-001")  
- **Pojemność:** Do 128 znaków ASCII  
- **Dlaczego wygrywa:** Kompaktowy, szeroko wspierany, obsługuje zarówno litery, jak i cyfry  
- **Użyj, gdy:** Potrzebujesz elastyczności i nie wiesz, jaki rodzaj danych będziesz kodować  

**Code39:**  
- **Najlepszy dla:** Proste kody alfanumeryczne  
- **Pojemność:** 43 znaki (A‑Z, 0‑9 oraz niektóre symbole)  
- **Dlaczego rozważyć:** Starsze skanery często lepiej go obsługują  
- **Użyj, gdy:** Pracujesz z systemami legacy lub gdy prostota jest ważniejsza niż gęstość danych  

**QR Code:**  
- **Najlepszy dla:** Dużych ilości danych (URL‑e, ładunki JSON)  
- **Pojemność:** Do 3 KB danych  
- **Dlaczego jest potężny:** Może przechowywać złożone struktury danych, wbudowana korekcja błędów  
- **Użyj, gdy:** Musisz osadzić ustrukturyzowane dane lub URL‑e  

**EAN/UPC:**  
- **Najlepszy dla:** Identyfikacji produktów  
- **Pojemność:** Stałej długości kody numeryczne (8‑13 cyfr)  
- **Użyj, gdy:** Pracujesz z systemami detalicznymi lub inwentaryzacyjnymi  

**Szybki przewodnik decyzyjny:**  
- Potrzebujesz liter i cyfr? → Code128  
- Tylko cyfry, zachowaj prostotę? → Code39  
- Dużo danych lub URL‑e? → QR Code  
- Kody detaliczne/produktowe? → EAN/UPC  

## Typowe pułapki i jak ich unikać

Oto problemy, z którymi najczęściej spotykają się programiści (abyś nie musiał tego doświadczać):

### Problem 1: Nieprawidłowe pozycjonowanie kodu kreskowego

**Objaw:** Twój kod kreskowy pojawia się w nieoczekiwanych miejscach lub jest obcięty.  

**Typowe przyczyny:**  
- Używanie wartości w pikselach przy różnych rozmiarach stron  
- Zapomnienie, że współrzędne PDF zaczynają się od lewego dolnego rogu, a nie od lewego górnego  
- Marginesy wypychające zawartość poza widoczny obszar  

**Rozwiązanie:**  
Zawsze używaj pozycjonowania opartego na procentach dla spójności:
```java
options.setLocationMeasureType(MeasureType.Percents);
options.setLeft(5);  // 5% from left works on any page width
```

### Problem 2: Tekst kodu kreskowego jest nieczytelny

**Objaw:** Zakodowany tekst jest wyświetlany, ale skanery nie potrafią go odczytać.  

**Przyczyny:**  
- Kod kreskowy jest za mały w stosunku do ilości danych  
- Nieprawidłowy typ kodowania dla Twoich danych  
- Niska rozdzielczość lub słaby kontrast  

**Rozwiązanie:**  
Dopasuj rozmiar kodu kreskowego do długości danych. Dla Code128 z 10‑15 znakami celuj w co najmniej 8‑10 % szerokości strony:
```java
options.setWidth(10);  // Give it room to breathe
options.setHeight(5);  // Maintain proper aspect ratio
```

### Problem 3: Wyjątki związane ze ścieżką pliku

**Objaw:** `FileNotFoundException` lub podobne błędy.  

**Przyczyny:**  
- Sztywno zakodowane ścieżki Windows z pojedynczymi backslashami  
- Katalog wyjściowy nie istnieje  
- Problemy z uprawnieniami do plików  

**Rozwiązanie:**  
Używaj ukośników (`/`) (działają wszędzie) i najpierw twórz katalogi:
```java
String filePath = "documents/sample.pdf";  // Works on Windows, Mac, Linux
Files.createDirectories(Paths.get("output/signed"));
```

### Problem 4: Problemy z pamięcią przy dużych PDF‑ach

**Objaw:** Błędy braku pamięci przy przetwarzaniu dużych dokumentów.  

**Rozwiązanie:**  
Zamknij obiekt `Signature`, gdy skończysz, aby zwolnić zasoby:
```java
try (Signature signature = new Signature(filePath)) {
    signature.sign(outputFilePath, options);
} // Automatically closes and releases memory
```

## Testowanie implementacji kodu kreskowego

Przed wdrożeniem upewnij się, że Twoje kody kreskowe naprawdę działają. Oto praktyczna lista kontrolna testów:

### 1. Test wizualny

Otwórz podpisany PDF i sprawdź:
- Czy kod kreskowy jest widoczny i prawidłowo umieszczony?  
- Czy wygląda ostro (nie jest rozmyty ani pikselowy)?  
- Czy wokół niego jest wystarczająco dużo białej przestrzeni?

### 2. Test skanowania

Użyj aplikacji skanującej kody kreskowe na telefonie (np. „Barcode Scanner” lub „QR & Barcode Reader”), aby zweryfikować:
- Czy skaner potrafi odczytać Twój kod kreskowy  
- Czy odkodowane dane zgadzają się z tymi, które zakodowałeś  
- Czy działa z różnych kątów i odległości

### 3. Test wieloplatformowy

Otwórz swój PDF na różnych urządzeniach:
- Windows (Adobe Reader, Chrome)  
- Mac (Preview, Chrome)  
- Urządzenia mobilne (iOS, Android)  

Upewnij się, że kod kreskowy renderuje się poprawnie wszędzie.

### 4. Kod testów automatycznych

Oto prosty test, który możesz uruchomić:
```java
import org.junit.Test;
import static org.junit.Assert.*;

public class BarcodeSignatureTest {
    
    @Test
    public void testBarcodeSigning() {
        String testPdf = "test-data/sample.pdf";
        String output = "test-output/signed.pdf";
        
        try (Signature signature = new Signature(testPdf)) {
            BarcodeSignOptions options = new BarcodeSignOptions("TEST123");
            options.setEncodeType(BarcodeTypes.Code128);
            
            signature.sign(output, options);
            
            // Verify output file exists
            assertTrue(new File(output).exists());
            
            // Verify file size increased (signature was added)
            long originalSize = new File(testPdf).length();
            long signedSize = new File(output).length();
            assertTrue(signedSize > originalSize);
            
        } catch (Exception e) {
            fail("Signing should not throw exception: " + e.getMessage());
        }
    }
}
```

## Praktyczne zastosowania podpisów z kodem kreskowym

Spójrzmy, gdzie ta technika naprawdę błyszczy w systemach produkcyjnych:

### 1. Generowanie i weryfikacja certyfikatów

**Scenariusz:** Tworzysz platformę szkoleniową, która wydaje certyfikaty ukończenia.  
**Implementacja:** Wygeneruj unikalny identyfikator certyfikatu (np. „CERT‑2024‑00123”) i osadź go jako kod Code128 w prawym dolnym rogu. Skanowanie kodu pozwala Twojemu API natychmiast pobrać szczegóły certyfikatu, eliminując ręczne wprowadzanie danych.

### 2. Systemy śledzenia faktur

**Scenariusz:** Twoja firma przetwarza tysiące faktur miesięcznie.  
**Implementacja:** Dodaj numer faktury i termin płatności jako kod QR umieszczony w miejscu, które łatwo odczytują urządzenia skanujące. Systemy sortowania automatycznego mogą kierować faktury bez udziału człowieka, skracając czas przetwarzania z godzin do minut.

### 3. Zarządzanie umowami prawnymi

**Scenariusz:** Kancelaria prawna musi śledzić wersje umów i ich zmiany.  
**Implementacja:** Każda wersja umowy otrzymuje unikalny identyfikator kodu kreskowego, który zawiera ID umowy, numer wersji i datę podpisu. Skanowanie podczas audytów automatycznie wyświetla pełną historię wersji.

### 4. Bezpieczeństwo dokumentacji medycznej

**Scenariusz:** Szpital chce zapobiec nieautoryzowanemu dostępowi do dokumentacji.  
**Implementacja:** Osadź w kodzie kreskowym ID pacjenta oraz znacznik czasu utworzenia dokumentu. Tylko uwierzytelnione urządzenia mogą odszyfrować i uzyskać dostęp do pełnego rekordu, a każde skanowanie tworzy dziennik audytu dla zgodności.

## Wskazówki dotyczące optymalizacji wydajności

Podczas podpisywania wielu PDF‑ów wydajność ma znaczenie. Oto kilka wskazówek, aby wszystko działało płynnie:

### Strategia przetwarzania wsadowego

Zamiast podpisywać jeden dokument po drugim, przetwarzaj je wsadowo:
```java
List<String> pdfFiles = Arrays.asList("doc1.pdf", "doc2.pdf", "doc3.pdf");

for (String pdfFile : pdfFiles) {
    try (Signature signature = new Signature(pdfFile)) {
        BarcodeSignOptions options = createBarcodeOptions(); // Reuse options
        signature.sign(getOutputPath(pdfFile), options);
    }
}
```

**Dlaczego to pomaga:** Ponowne użycie obiektu opcji i prawidłowe zamykanie zasobów zapobiega wyciekom pamięci.

### Zarządzanie pamięcią

Dla bardzo dużych PDF‑ów (powyżej 50 MB):
- Przetwarzaj je kolejno, zamiast ładować wiele jednocześnie  
- Używaj try‑with‑resources, aby zapewnić czyszczenie  
- Monitoruj rozmiar sterty i w razie potrzeby dostosuj parametry JVM: `-Xmx2g`

### Strategia buforowania

Jeśli wielokrotnie podpisujesz tym samym kodem kreskowym:
```java
// Create options once, reuse many times
BarcodeSignOptions templateOptions = createStandardBarcodeOptions();

// For each document, clone and customize
BarcodeSignOptions documentOptions = templateOptions.clone();
documentOptions.setText(uniqueDocumentId);
```

## Kiedy używać podpisów z kodem kreskowym (i kiedy nie)

**Idealne scenariusze:**
- Potrzebujesz maszynowo odczytywalnych identyfikatorów dokumentów  
- Dokumenty będą skanowane lub przetwarzane automatycznie  
- Chcesz śledzenia odpornego na manipulacje bez certyfikatów cyfrowych  
- Integracja z istniejącą infrastrukturą kodów kreskowych  

**Nieodpowiednie, gdy:**
- Potrzebujesz prawnie wiążących podpisów cyfrowych (użyj certyfikatów cyfrowych zamiast tego)  
- Dokumenty będą oglądane wyłącznie przez ludzi (prosta znak wodny tekstowy może wystarczyć)  
- Pracujesz z bardzo małymi dokumentami, w których kod kreskowy zdominowałby stronę  
- Wymagania bezpieczeństwa nakazują szyfrowanie (kody kreskowe są widoczne i skanowalne przez każdego)

**Czy można łączyć podejścia?** Oczywiście! Wiele systemów używa zarówno podpisów z kodem kreskowym do śledzenia, jak i podpisów cyfrowych dla ważności prawnej.

## Najczęściej zadawane pytania

**P:** Czy mogę używać różnych typów kodów kreskowych w tym samym PDF?  
**O:** Tak! Wywołaj `signature.sign()` wielokrotnie z różnymi `BarcodeSignOptions` dla każdego typu kodu kreskowego. Upewnij się tylko, że się nie nakładają.

**P:** Jak obsłużyć kody kreskowe zawierające znaki specjalne?  
**O:** Code128 obsługuje większość znaków ASCII. Dla Unicode lub złożonych danych przejdź na kody QR — obsługują kodowanie UTF‑8.

**P:** Jaka jest maksymalna ilość danych, którą mogę przechowywać w kodzie Code128?  
**O:** Technicznie do 128 znaków, ale czytelność znacznie spada powyżej 30‑40 znaków. Dla większych ładunków danych użyj kodów QR.

**P:** Czy dodanie kodów kreskowych znacząco zwiększy rozmiar mojego pliku PDF?  
**O:** Niezauważalnie — kody kreskowe są grafiką wektorową, zazwyczaj dodają jedynie 5‑20 KB na kod, w zależności od rozmiaru i złożoności.

**P:** Czy mogę obracać kody kreskowe lub umieszczać je pionowo?  
**O:** Tak! Użyj `options.setRotationAngle(90)`, aby obrócić kod kreskowy, co jest przydatne przy umieszczaniu go na marginesie.

**P:** Jak sprawić, aby kody kreskowe pojawiały się na każdej stronie wielostronicowego PDF?  
**O:** Iteruj przez strony i zastosuj podpis do każdej z nich. Sprawdź klasę `PagesSetup` w dokumentacji GroupDocs, aby kontrolować, które strony mają być podpisane.

**P:** Co zrobić, jeśli mój skaner kodów kreskowych nie odczytuje wygenerowanego kodu?  
**O:** Najpierw sprawdź, czy skaner obsługuje wybrany typ kodu. Następnie zwiększ rozmiar kodu — większość problemów ze skanowaniem wynika z zbyt małych pasków. Celuj w co najmniej 1 cal (2,54 cm) szerokości, aby zapewnić niezawodne odczyty.

## Dodatkowe zasoby

**Dokumentacja:**  
- [GroupDocs.Signature for Java Docs](https://docs.groupdocs.com/signature/java/)  
- [API Reference Guide](https://reference.groupdocs.com/signature/java/)  

**Pobieranie i licencjonowanie:**  
- [Download Latest Version](https://releases.groupdocs.com/signature/java/)  
- [Free Trial Access](https://releases.groupdocs.com/signature/java/)  
- [Get Temporary License](https://purchase.groupdocs.com/temporary-license/)  
- [Purchase Full License](https://purchase.groupdocs.com/buy)  

**Społeczność i wsparcie:**  
- [Support Forum](https://forum.groupdocs.com/c/signature/) - Aktywna społeczność z inżynierami GroupDocs  

---

**Ostatnia aktualizacja:** 2026-03-06  
**Testowano z:** GroupDocs.Signature 23.12 (Java)  
**Autor:** GroupDocs