---
"description": "Opanuj weryfikację podpisów tekstowych w aplikacjach .NET dzięki GroupDocs.Signature. Przewodnik krok po kroku z kompletnymi przykładami kodu i najlepszymi praktykami."
"linktitle": "Zweryfikuj tekst"
"second_title": "GroupDocs.Signature .NET API"
"title": "Weryfikacja podpisów tekstowych w dokumentach"
"url": "/pl/net/verify-operations/verify-text/"
"weight": 13
---

## Wstęp

Podpisy tekstowe, choć często prostsze niż podpisy cyfrowe lub elektroniczne, odgrywają kluczową rolę w zarządzaniu dokumentami i ich weryfikacji. Niezależnie od tego, czy chodzi o znaki wodne, tekst stopki, czy konkretne wzorce treści, weryfikacja obecności i integralności podpisów tekstowych jest ważnym aspektem procesów weryfikacji dokumentów.

GroupDocs.Signature for .NET oferuje zaawansowane API do weryfikacji podpisów tekstowych w dokumentach w szerokiej gamie formatów. Ten kompleksowy samouczek przeprowadzi Cię przez proces wdrażania funkcji weryfikacji tekstu w aplikacjach .NET, zapewniając integralność i autentyczność dokumentów.

## Wymagania wstępne

Przed wdrożeniem funkcji weryfikacji tekstu należy upewnić się, że spełnione są następujące wymagania wstępne:

1. GroupDocs.Signature dla .NET: Pobierz i zainstaluj bibliotekę z [strona pobierania](https://releases.groupdocs.com/signature/net/).
2. Środowisko programistyczne .NET: Visual Studio lub dowolne zgodne środowisko programistyczne .NET.
3. Wiedza podstawowa: Znajomość programowania w języku C# i koncepcji .NET Framework.
4. Dokument testowy: Dokument zawierający podpisy tekstowe służące celom weryfikacji.

## Importuj wymagane przestrzenie nazw

Zacznij od zaimportowania niezbędnych przestrzeni nazw, aby uzyskać dostęp do funkcjonalności GroupDocs.Signature:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Podzielmy proces weryfikacji tekstu na jasne i łatwe do opanowania kroki:

## Krok 1: Określ ścieżkę dokumentu

```csharp
// Ścieżka do dokumentu zawierającego podpisy tekstowe
string filePath = "sample_multiple_signatures.docx";
```

Pamiętaj o zastąpieniu przykładowej ścieżki rzeczywistą ścieżką do dokumentu zawierającego podpisy tekstowe.

## Krok 2: Zainicjuj obiekt podpisu

```csharp
// Utwórz instancję klasy Signature, przekazując ścieżkę dokumentu
using (Signature signature = new Signature(filePath))
{
    // Tutaj zostanie zaimplementowany kod weryfikacyjny
}
```

Klasa Signature stanowi główny punkt wejścia dla wszystkich operacji w interfejsie API GroupDocs.Signature.

## Krok 3: Skonfiguruj opcje weryfikacji tekstu

```csharp
// Zdefiniuj opcje weryfikacji tekstu
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = true,                               // Sprawdź wszystkie strony dokumentu
    SignatureImplementation = TextSignatureImplementation.Native,
    Text = "signature",                            // Tekst do weryfikacji
    MatchType = TextMatchType.Contains             // Określ kryteria dopasowania
};
```

Opcje weryfikacji umożliwiają zdefiniowanie szczegółowych kryteriów procesu weryfikacji:
- `AllPages`: Ustaw na true, aby sprawdzić wszystkie strony dokumentu
- `SignatureImplementation`: Określ sposób implementacji tekstu (natywny lub naklejka)
- `Text`:Zawartość tekstowa, która ma pasować do dokumentu
- `MatchType`:Metoda dopasowywania tekstu (Zawiera, Dokładne, Zaczyna się od itd.)

## Krok 4: Wykonaj proces weryfikacji

```csharp
// Wykonaj weryfikację
VerificationResult result = signature.Verify(options);
```

Na tej podstawie wykonywany jest proces weryfikacji na podstawie określonych opcji.

## Krok 5: Wyniki weryfikacji procesu

```csharp
// Sprawdź wynik weryfikacji i postępuj zgodnie z nim
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid text signatures!");
    
    // Wyświetl informacje o pomyślnych podpisach
    foreach (TextSignature textSignature in result.Succeeded)
    {
        Console.WriteLine($"\nFound valid text signature:");
        Console.WriteLine($"Text: {textSignature.Text}");
        Console.WriteLine($"Location: Page {textSignature.PageNumber}, {textSignature.Left}x{textSignature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

Ten kod sprawdza, czy weryfikacja przebiegła pomyślnie i wyświetla szczegółowe informacje na temat zweryfikowanych podpisów tekstowych.

## Pełny przykład

Oto kompletny przykład działania, który demonstruje weryfikację podpisu tekstowego:

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
            
            try
            {
                // Zainicjuj instancję podpisu
                using (Signature signature = new Signature(filePath))
                {
                    // Skonfiguruj opcje weryfikacji
                    TextVerifyOptions options = new TextVerifyOptions()
                    {
                        AllPages = true,
                        SignatureImplementation = TextSignatureImplementation.Native,
                        Text = "signature",
                        MatchType = TextMatchType.Contains
                    };
                    
                    // Zweryfikuj podpisy dokumentów
                    VerificationResult result = signature.Verify(options);
                    
                    // Wyniki weryfikacji procesu
                    if(result.IsValid)
                    {
                        Console.WriteLine($"\nDocument {filePath} was verified successfully!");
                        foreach (TextSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature is found with text: {item.Text}");
                            Console.WriteLine($"Location: Page {item.PageNumber}, position {item.Left}x{item.Top}");
                        }
                    }
                    else
                    {
                        Console.WriteLine($"\nDocument {filePath} failed verification process.");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

## Zaawansowane scenariusze weryfikacji

GroupDocs.Signature oferuje dodatkowe opcje dla bardziej złożonych scenariuszy weryfikacji:

### Używanie wyrażeń regularnych do weryfikacji

Aby uzyskać bardziej elastyczne dopasowywanie wzorców, możesz użyć wyrażeń regularnych:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "Invoice\\s+#\\d{5,6}",  // Dopasuj wzorce takie jak „Faktura nr 12345”
    MatchType = TextMatchType.Regex
};
```

### Weryfikacja tekstu w określonych obszarach dokumentu

Możesz ograniczyć weryfikację do określonych obszarów dokumentu:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = false,
    PageNumber = 1,  // Zweryfikuj tylko na pierwszej stronie
    
    // Zdefiniuj obszar, w którym chcesz przeprowadzić wyszukiwanie (współrzędne w punktach)
    PagesSetup = new PagesSetup() 
    { 
        FirstPage = true,
        LastPage = false,
        OddPages = false,
        EvenPages = false 
    },
    
    // Pole prostokąta w milimetrach
    Rectangle = new Rectangle(10, 10, 100, 30),
    
    Text = "Confidential"
};
```

### Jednoczesna weryfikacja wielu wzorców tekstu

Możesz utworzyć wiele opcji weryfikacji, aby sprawdzać różne wzorce tekstu:

```csharp
// Utwórz listę opcji weryfikacji
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// Dodaj pierwszą weryfikację tekstową
listOptions.Add(new TextVerifyOptions()
{
    Text = "Confidential",
    MatchType = TextMatchType.Exact
});

// Dodaj drugą weryfikację tekstową
listOptions.Add(new TextVerifyOptions()
{
    Text = "Do not copy",
    MatchType = TextMatchType.Contains
});

// Zweryfikuj za pomocą wielu opcji
VerificationResult result = signature.Verify(listOptions);
```

### Weryfikacja tekstu o określonym wyglądzie

Można również zweryfikować tekst pod kątem określonych cech formatowania:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "APPROVED",
    MatchType = TextMatchType.Exact,
    
    // Sprawdź określone właściwości wyglądu
    ForegroundColorRGB = System.Drawing.Color.Green,
    Font = new SignatureFont() { FontFamily = "Arial", FontSize = 12, Bold = true }
};
```

## Najlepsze praktyki weryfikacji tekstu

1. Wybierz odpowiednie typy dopasowania: Wybierz właściwy typ dopasowania (Zawiera, Dokładne, Wyrażenie regularne) na podstawie wymagań weryfikacji.
2. Optymalizacja pod kątem wydajności: W przypadku obszernych dokumentów lepiej jest sprawdzić poszczególne strony, a nie cały dokument.
3. Obsługa błędów: Wdrożenie odpowiedniej obsługi błędów w celu sprawnego radzenia sobie z nieoczekiwanymi scenariuszami.
4. Weź pod uwagę wielkość liter: Pamiętaj o uwzględnianiu wielkości liter podczas dopasowywania tekstu, zwłaszcza w przypadku weryfikacji krytycznych.
5. Dokładny test: Przetestuj weryfikację przy użyciu różnych formatów dokumentów i wzorców tekstu, aby zapewnić kompatybilność.

## Rozwiązywanie typowych problemów

### Tekst nie został wykryty
- Sprawdź, czy formatowanie lub kodowanie tekstu ma wpływ na wykrywanie
- Upewnij się, że tekst faktycznie znajduje się w dokumencie jako zwykły tekst (a nie obraz)
- Wypróbuj różne kryteria dopasowania (Zawiera zamiast Dokładne)

### Problemy z wydajnością
- Zoptymalizuj weryfikację, kierując ją na określone strony lub obszary
- Używaj bardziej szczegółowych wzorców tekstowych, aby zmniejszyć liczbę fałszywych wyników pozytywnych

### Niepowodzenia weryfikacji
- Sprawdź, czy spacje, znaki specjalne lub formatowanie mają wpływ na dopasowanie
- Sprawdź, czy tekst nie jest częścią zeskanowanego obrazu (co wymaga OCR)
- Upewnij się, że dokument nie został zmodyfikowany od momentu dodania tekstu

## Wniosek

Weryfikacja tekstu to wszechstronne i praktyczne podejście do uwierzytelniania dokumentów, które można stosować samodzielnie lub w połączeniu z innymi metodami weryfikacji. GroupDocs.Signature for .NET oferuje kompleksowe i łatwe w użyciu API do implementacji solidnej funkcjonalności weryfikacji tekstu w aplikacjach .NET.

Dzięki temu przewodnikowi krok po kroku nauczysz się, jak:
- Skonfiguruj i zainicjuj proces weryfikacji tekstu
- Określ różne kryteria weryfikacji
- Przetwarzanie i interpretowanie wyników weryfikacji
- Wdrażanie zaawansowanych scenariuszy weryfikacji

Możliwości te umożliwiają tworzenie bezpiecznych i niezawodnych systemów przetwarzania dokumentów, które potrafią weryfikować autentyczność tekstu w różnych formatach dokumentów.

## Często zadawane pytania

### Czy GroupDocs.Signature może weryfikować tekst w zeskanowanych dokumentach?
GroupDocs.Signature został zaprojektowany przede wszystkim do cyfrowej weryfikacji tekstu. W przypadku zeskanowanych dokumentów konieczne będzie wcześniejsze użycie technologii OCR (Optical Character Recognition), aby przekonwertować zeskanowane obrazy na tekst.

### Jakie formaty dokumentów są obsługiwane w przypadku weryfikacji tekstu?
GroupDocs.Signature obsługuje szeroką gamę formatów dokumentów, w tym pliki PDF, dokumenty Word (DOC, DOCX), arkusze kalkulacyjne Excel (XLS, XLSX), prezentacje PowerPoint (PPT, PPTX), obrazy i wiele innych.

### Czy mogę zweryfikować sformatowany tekst (pogrubienie, kursywa, określone czcionki)?
Tak, GroupDocs.Signature udostępnia opcje weryfikacji tekstu pod kątem określonych cech formatowania, w tym rodziny czcionek, rozmiaru, stylu (pogrubienie, kursywa) i koloru.

### Czy można zweryfikować tekst w dokumentach chronionych hasłem?
Tak, GroupDocs.Signature udostępnia opcje określania haseł dokumentów podczas otwierania zabezpieczonych dokumentów w celu weryfikacji.

### Czy mogę zweryfikować znaki wodne i tekst w tle?
Tak, GroupDocs.Signature może weryfikować różne typy podpisów tekstowych, w tym znaki wodne i tekst tła, w zależności od sposobu ich implementacji w dokumencie.

### Powiązane zasoby
* [Dokumentacja API GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [Pobieranie GroupDocs.Signature](https://releases.groupdocs.com/signature/net/)
* [Przykłady kodu na GitHubie](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Dokumentacja](https://docs.groupdocs.com/signature/net/)
* [Strona produktu](https://products.groupdocs.com/signature/net/)
* [Artykuły blogowe](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Forum wsparcia](https://forum.groupdocs.com/c/signature/13)
* [Licencja tymczasowa](https://purchase.groupdocs.com/temporary-license/)