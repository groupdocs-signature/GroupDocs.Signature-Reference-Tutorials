---
"description": "Dowiedz się, jak weryfikować kody QR w dokumentach za pomocą GroupDocs.Signature dla .NET. Kompletny przewodnik z przykładami kodu i najlepszymi praktykami uwierzytelniania dokumentów."
"linktitle": "Zweryfikuj kod QR"
"second_title": "GroupDocs.Signature .NET API"
"title": "Zweryfikuj kod QR w dokumentach"
"url": "/pl/net/verify-operations/verify-qr-code/"
"weight": 12
---

## Wstęp

Bezpieczeństwo dokumentów jest kluczowym aspektem nowoczesnego funkcjonowania firm. Kody QR stają się coraz popularniejszą metodą osadzania informacji w dokumentach, których autentyczność można zweryfikować. GroupDocs.Signature for .NET to wydajne i elastyczne rozwiązanie do weryfikacji kodów QR osadzonych w dokumentach w różnych formatach.

Ten kompleksowy samouczek przeprowadzi Cię przez proces wdrażania weryfikacji kodów QR w aplikacjach .NET, zapewniając integralność i autentyczność Twoich dokumentów.

## Wymagania wstępne

Przed wdrożeniem funkcji weryfikacji za pomocą kodu QR upewnij się, że spełnione są następujące wymagania wstępne:

1. GroupDocs.Signature dla .NET: Pobierz i zainstaluj bibliotekę z [strona pobierania](https://releases.groupdocs.com/signature/net/).
2. Środowisko programistyczne: Visual Studio lub dowolne zgodne środowisko programistyczne .NET.
3. Dokument testowy: Dokument zawierający podpisy w postaci kodu QR służące celom weryfikacji.
4. Wiedza podstawowa: Znajomość programowania w języku C# i koncepcji .NET Framework.

## Importuj przestrzenie nazw

Zacznij od zaimportowania wymaganych przestrzeni nazw, aby uzyskać dostęp do funkcjonalności GroupDocs.Signature:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Proces weryfikacji kodu QR krok po kroku

Aby zweryfikować kody QR w dokumentach, wykonaj poniższe szczegółowe czynności:

### Krok 1: Określ ścieżkę dokumentu

```csharp
// Podaj ścieżkę do dokumentu zawierającego podpisy w postaci kodu QR
string filePath = "sample_multiple_signatures.docx";
```

Pamiętaj o zastąpieniu przykładowej ścieżki rzeczywistą ścieżką do dokumentu.

### Krok 2: Zainicjuj obiekt podpisu

```csharp
// Utwórz instancję podpisu, przekazując ścieżkę dokumentu
using (Signature signature = new Signature(filePath))
{
    // Tutaj zostanie zaimplementowany kod weryfikacyjny
}
```

Klasa Signature stanowi główny punkt wejścia dla wszystkich operacji w interfejsie API GroupDocs.Signature.

### Krok 3: Skonfiguruj opcje weryfikacji kodu QR

```csharp
// Zdefiniuj opcje weryfikacji kodu QR
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // Sprawdź wszystkie strony dokumentu
    Text = "John",   // Tekst do weryfikacji w kodzie QR
    MatchType = TextMatchType.Contains // Określ kryteria dopasowania tekstu
};
```

Opcje weryfikacji umożliwiają zdefiniowanie szczegółowych kryteriów procesu weryfikacji:
- `AllPages`: Ustaw na true, aby sprawdzić wszystkie strony dokumentu (domyślne zachowanie)
- `Text`:Treść tekstu do dopasowania w kodzie QR
- `MatchType`:Metoda dopasowywania tekstu (Zawiera, Dokładne, Zaczyna się od itd.)

### Krok 4: Wykonaj proces weryfikacji

```csharp
// Wykonaj weryfikację
VerificationResult result = signature.Verify(options);
```

Na tej podstawie wykonywany jest proces weryfikacji na podstawie określonych opcji.

### Krok 5: Wyniki weryfikacji procesu

```csharp
// Sprawdź wynik weryfikacji i postępuj zgodnie z nim
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
    
    // Wyświetl informacje o pomyślnych podpisach
    foreach (QrCodeSignature signature in result.Succeeded)
    {
        Console.WriteLine($"Found valid QR Code signature with text: {signature.Text}");
        Console.WriteLine($"QR Code type: {signature.EncodeType.TypeName}");
        Console.WriteLine($"Location: Page {signature.PageNumber}, {signature.Left}x{signature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

Prawidłowe postępowanie z wynikami weryfikacji pozwala aplikacji na podjęcie odpowiednich działań na podstawie rezultatu weryfikacji.

## Pełny przykład

Oto kompletny, działający przykład demonstrujący weryfikację za pomocą kodu QR:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace GroupDocs.Signature.Examples
{
    class Program
    {
        static void Main(string[] args)
        {
            // Ścieżka dokumentu
            string filePath = "sample_multiple_signatures.docx";
            
            // Zainicjuj instancję podpisu
            using (Signature signature = new Signature(filePath))
            {
                // Skonfiguruj opcje weryfikacji
                QrCodeVerifyOptions options = new QrCodeVerifyOptions()
                {
                    AllPages = true,
                    Text = "John",
                    MatchType = TextMatchType.Contains
                };
                
                // Zweryfikuj podpisy dokumentów
                VerificationResult result = signature.Verify(options);
                
                // Wyniki weryfikacji procesu
                if (result.IsValid)
                {
                    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
                    
                    foreach (QrCodeSignature qrSignature in result.Succeeded)
                    {
                        Console.WriteLine($"Found valid QR Code with text: {qrSignature.Text}");
                    }
                }
                else
                {
                    Console.WriteLine($"Document {filePath} failed verification process.");
                }
            }
        }
    }
}
```

## Zaawansowane opcje weryfikacji

GroupDocs.Signature oferuje dodatkowe opcje dla bardziej złożonych scenariuszy weryfikacji:

### Weryfikacja określonych typów kodów QR

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    EncodeType = QrCodeTypes.QR,  // Weryfikuj tylko standardowe kody QR
    Text = "Confidential",
    MatchType = TextMatchType.Exact
};
```

### Weryfikacja na określonych stronach

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = false,
    PageNumber = 2,  // Sprawdź tylko na stronie 2
    Text = "Approved"
};
```

### Używanie wyrażeń regularnych do weryfikacji

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    Text = "INV-\\d{6}",  // Dopasuj numery faktur (np. INV-123456)
    MatchType = TextMatchType.Regex
};
```

## Najlepsze praktyki weryfikacji kodów QR

1. Zawsze sprawdzaj poprawność danych wejściowych: przed przetworzeniem upewnij się, że ścieżki dokumentów i kryteria weryfikacji są prawidłowe.
2. Wdrażanie obsługi błędów: używanie bloków try-catch do obsługi potencjalnych wyjątków podczas weryfikacji.
3. Weź pod uwagę wydajność: w przypadku obszernych dokumentów rozważ weryfikację poszczególnych stron, a nie całego dokumentu.
4. Rejestrowanie wyników weryfikacji: prowadzenie rejestrów procesów weryfikacji na potrzeby audytu.
5. Przetestuj przy użyciu różnych formatów dokumentów: Upewnij się, że weryfikacja działa we wszystkich wymaganych formatach dokumentów.

## Wniosek

Weryfikacja kodów QR w dokumentach jest kluczowym aspektem zapewnienia autentyczności i integralności dokumentów. GroupDocs.Signature for .NET oferuje kompleksowe i przyjazne dla użytkownika API do implementacji weryfikacji kodów QR w aplikacjach .NET.

Dzięki temu samouczkowi nauczyłeś się:
- Skonfiguruj i zainicjuj proces weryfikacji
- Określ różne kryteria weryfikacji
- Przetwarzanie i interpretowanie wyników weryfikacji
- Wdrożenie zaawansowanych opcji weryfikacji

Dzięki tej wiedzy możesz zwiększyć bezpieczeństwo i niezawodność swoich systemów zarządzania dokumentami.

## Najczęściej zadawane pytania

### Czy GroupDocs.Signature może zweryfikować wiele kodów QR w jednym dokumencie?
Tak, GroupDocs.Signature może zweryfikować wiele kodów QR w jednym dokumencie. Wyniki weryfikacji będą obejmować wszystkie pasujące kody QR.

### Jakie formaty dokumentów są obsługiwane w przypadku weryfikacji za pomocą kodu QR?
GroupDocs.Signature obsługuje szeroką gamę formatów dokumentów, w tym PDF, Word (DOC, DOCX), Excel (XLS, XLSX), PowerPoint (PPT, PPTX), obrazy i inne.

### Czy mogę zweryfikować kody QR za pomocą określonego szyfrowania lub formatowania?
Tak, GroupDocs.Signature udostępnia opcje weryfikacji kodów QR przy użyciu określonych typów kodowania i wzorców formatowania treści.

### Czy można weryfikować kody QR utworzone przez aplikacje innych firm?
Tak, GroupDocs.Signature może weryfikować standardowe kody QR generowane przez większość aplikacji, pod warunkiem że są zgodne ze standardowymi formatami kodów QR.

### Jak postępować w przypadku kodów QR zawierających dane binarne zamiast tekstu?
GroupDocs.Signature zapewnia opcje weryfikacji kodów QR za pomocą danych binarnych za pomocą `BinaryData` właściwość opcji weryfikacji.

### Powiązane zasoby
* [Dokumentacja API GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [Pobieranie GroupDocs.Signature](https://releases.groupdocs.com/signature/net/)
* [Przykłady kodu na GitHubie](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Dokumentacja](https://docs.groupdocs.com/signature/net/)
* [Strona produktu](https://products.groupdocs.com/signature/net/)
* [Artykuły blogowe](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Forum wsparcia](https://forum.groupdocs.com/c/signature/13)
* [Licencja tymczasowa](https://purchase.groupdocs.com/temporary-license/)