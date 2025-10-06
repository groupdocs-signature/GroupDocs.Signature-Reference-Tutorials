---
"description": "Dowiedz się, jak dynamicznie aktualizować podpisy kodów QR w różnych formatach dokumentów dzięki GroupDocs.Signature dla .NET. Kompleksowy przewodnik dla programistów po nowoczesnych rozwiązaniach do zarządzania dokumentami."
"linktitle": "Zaktualizuj kod QR"
"second_title": "GroupDocs.Signature .NET API"
"title": "Aktualizacja podpisów kodów QR w dokumentach"
"url": "/pl/net/update-operations/update-qr-code/"
"weight": 12
type: docs
---
## Wstęp
dzisiejszym cyfrowym środowisku biznesowym kody QR stały się niezbędnym elementem systemów zarządzania dokumentami i uwierzytelniania. Zapewniają wygodny sposób kodowania i dostępu do informacji, od prostych adresów URL po złożone dane strukturalne. GroupDocs.Signature for .NET oferuje kompleksowy zestaw narzędzi, który umożliwia programistom integrację zaawansowanych funkcji podpisu elektronicznego z ich aplikacjami, w tym aktualizację istniejących podpisów kodami QR w dokumentach.

Ten samouczek koncentruje się na aktualizacji podpisów kodów QR w dokumentach za pomocą GroupDocs.Signature dla platformy .NET. Niezależnie od tego, czy chcesz zmodyfikować położenie, rozmiar, czy zakodowane dane istniejących kodów QR, ten przewodnik przeprowadzi Cię przez ten proces krok po kroku, z przejrzystymi przykładami kodu i wyjaśnieniami.

## Wymagania wstępne
Zanim przejdziesz do aktualizacji podpisu kodem QR za pomocą GroupDocs.Signature dla .NET, upewnij się, że spełnione są następujące wymagania wstępne:

1. Środowisko programistyczne: działające środowisko programistyczne .NET, takie jak Visual Studio 2017 lub nowszy.
2. Biblioteka GroupDocs.Signature: Pobierz i zainstaluj bibliotekę GroupDocs.Signature dla platformy .NET z [strona pobierania](https://releases.groupdocs.com/signature/net/).
3. Licencja (opcjonalnie): Do użytku produkcyjnego potrzebna jest ważna licencja. Do celów testowych można użyć [tymczasowa licencja](https://purchase.groupdocs.com/temporary-license/).
4. Przykładowy dokument: Dokument zawierający podpisy w postaci kodu QR, które chcesz zaktualizować.
5. Podstawowa wiedza z zakresu języka C#: Znajomość koncepcji programowania w języku C#.

## Importuj przestrzenie nazw
Zacznij od zaimportowania niezbędnych przestrzeni nazw, aby uzyskać dostęp do funkcjonalności GroupDocs.Signature:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Podzielmy proces aktualizacji podpisów kodów QR na jasne i łatwe do opanowania kroki:

## Krok 1: Skonfiguruj ścieżki dokumentów
Najpierw zdefiniuj ścieżki do dokumentu źródłowego i miejsce, w którym zostanie zapisany zaktualizowany dokument:

```csharp
// Ścieżka do dokumentu źródłowego z podpisami w postaci kodu QR
string filePath = "sample_multiple_signatures.docx";

// Pobierz nazwę pliku wyjściowego
string fileName = Path.GetFileName(filePath);

// Zdefiniuj katalog wyjściowy i ścieżkę pliku
string outputDirectory = Path.Combine("Your Document Directory", "UpdateQRCode");
string outputFilePath = Path.Combine(outputDirectory, fileName);

// Upewnij się, że katalog wyjściowy istnieje
Directory.CreateDirectory(outputDirectory);
```

## Krok 2: Skopiuj dokument źródłowy
Ponieważ operacja aktualizacji modyfikuje dokument bezpośrednio, utwórz kopię oryginalnego dokumentu, aby go zachować:

```csharp
// Utwórz kopię oryginalnego dokumentu
File.Copy(filePath, outputFilePath, true);
```

## Krok 3: Zainicjuj instancję podpisu
Utwórz instancję `Signature` klasa do pracy z dokumentem:

```csharp
// Zainicjuj instancję podpisu ze ścieżką pliku wyjściowego
using (Signature signature = new Signature(outputFilePath))
{
    // Tutaj będą wykonywane operacje podpisu
}
```

## Krok 4: Skonfiguruj opcje wyszukiwania kodu QR
Skonfiguruj opcje wyszukiwania, aby znaleźć istniejące podpisy w postaci kodu QR w dokumencie:

```csharp
// Konfigurowanie opcji wyszukiwania podpisów w postaci kodów QR
QrCodeSearchOptions options = new QrCodeSearchOptions();

// W razie potrzeby możesz dostosować opcje wyszukiwania
// options.AllPages = true; // Szukaj na wszystkich stronach
// options.PageNumber = 1; // Wyszukaj na określonej stronie
// options.EncodeType = QrCodeTypes.QR; // Wyszukaj konkretny typ kodu QR
```

## Krok 5: Wyszukaj podpisy w postaci kodu QR
Aby znaleźć podpisy w postaci kodu QR w dokumencie, skorzystaj z skonfigurowanych opcji wyszukiwania:

```csharp
// Wyszukaj podpisy w postaci kodu QR
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```

## Krok 6: Zaktualizuj właściwości podpisu kodu QR
Jeśli zostaną znalezione podpisy w postaci kodu QR, zaktualizuj ich właściwości w razie potrzeby:

```csharp
// Sprawdź, czy znaleziono podpisy
if (signatures.Count > 0)
{
    // Zdobądź pierwszy podpis za pomocą kodu QR
    QrCodeSignature qrCodeSignature = signatures[0];
    
    // Aktualizuj pozycję
    qrCodeSignature.Left = 200;
    qrCodeSignature.Top = 250;
    
    // Rozmiar aktualizacji
    qrCodeSignature.Width = 200;
    qrCodeSignature.Height = 200;
    
    // W razie potrzeby możesz również zaktualizować dane kodu QR
    // qrCodeSignature.Text = "Zaktualizowane dane kodu QR";
    
    // Zastosuj aktualizacje
    bool result = signature.Update(qrCodeSignature);
    
    // Sprawdź wynik
    if (result)
    {
        Console.WriteLine($"QR Code signature was successfully updated in the document '{fileName}'.");
        Console.WriteLine($"New position: {qrCodeSignature.Left}x{qrCodeSignature.Top}");
        Console.WriteLine($"New size: {qrCodeSignature.Width}x{qrCodeSignature.Height}");
    }
    else
    {
        Console.WriteLine($"Failed to update QR Code signature in the document!");
    }
}
else
{
    Console.WriteLine("No QR Code signatures found in the document.");
}
```

## Pełny przykład
Oto kompletny, funkcjonalny przykład pokazujący, jak zaktualizować podpis w postaci kodu QR w dokumencie:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace UpdateQRCodeSignatureExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Ścieżka dokumentu
            string filePath = "sample_multiple_signatures.docx";
            
            // Zdefiniuj ścieżkę wyjściową
            string fileName = Path.GetFileName(filePath);
            string outputDirectory = Path.Combine(Environment.CurrentDirectory, "UpdateQRCode");
            string outputFilePath = Path.Combine(outputDirectory, fileName);
            
            // Upewnij się, że katalog wyjściowy istnieje
            Directory.CreateDirectory(outputDirectory);
            
            // Utwórz kopię oryginalnego dokumentu
            File.Copy(filePath, outputFilePath, true);
            
            // Zainicjuj instancję podpisu
            using (Signature signature = new Signature(outputFilePath))
            {
                // Konfiguruj opcje wyszukiwania
                QrCodeSearchOptions options = new QrCodeSearchOptions();
                
                // Wyszukaj podpisy w postaci kodu QR
                List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
                
                // Sprawdź, czy znaleziono podpisy
                if (signatures.Count > 0)
                {
                    // Zdobądź pierwszy podpis
                    QrCodeSignature qrCodeSignature = signatures[0];
                    
                    // Zaktualizuj pozycję i rozmiar
                    qrCodeSignature.Left = 200;
                    qrCodeSignature.Top = 250;
                    qrCodeSignature.Width = 200;
                    qrCodeSignature.Height = 200;
                    
                    // Zastosuj aktualizacje
                    bool result = signature.Update(qrCodeSignature);
                    
                    // Sprawdź wynik
                    if (result)
                    {
                        Console.WriteLine($"QR Code signature was successfully updated in document '{fileName}'.");
                        Console.WriteLine($"New position: {qrCodeSignature.Left}x{qrCodeSignature.Top}");
                        Console.WriteLine($"New size: {qrCodeSignature.Width}x{qrCodeSignature.Height}");
                        Console.WriteLine($"Output file path: {outputFilePath}");
                    }
                    else
                    {
                        Console.WriteLine("Failed to update QR Code signature!");
                    }
                }
                else
                {
                    Console.WriteLine("No QR Code signatures found in the document.");
                }
            }
            
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## Zaawansowana personalizacja podpisu za pomocą kodu QR
GroupDocs.Signature udostępnia dodatkowe opcje dostosowywania podpisów kodów QR wykraczające poza podstawowe położenie i rozmiar:

### Aktualizowanie zakodowanych danych
Możesz zaktualizować rzeczywiste dane zakodowane w kodzie QR:

```csharp
// Zaktualizuj zakodowane dane
qrCodeSignature.Text = "https://www.updated-website.com";
```

### Dostosowywanie właściwości wyglądu
Dostosuj aspekty wizualne kodu QR:

```csharp
// Ustaw kolor pierwszego planu (kolor kodu QR)
qrCodeSignature.ForeColor = System.Drawing.Color.Blue;

// Ustaw kolor tła
qrCodeSignature.BackgroundColor = System.Drawing.Color.LightYellow;

// Dostosuj przezroczystość
qrCodeSignature.Opacity = 0.8;
```

### Dodawanie obramowań
Ulepsz kod QR za pomocą niestandardowych obramowań:

```csharp
qrCodeSignature.Border.Color = System.Drawing.Color.Red;
qrCodeSignature.Border.DashStyle = System.Drawing.Drawing2D.DashStyle.Dash;
qrCodeSignature.Border.Weight = 2;
qrCodeSignature.Border.Visible = true;
```

### Obrót kodu QR
Obróć podpis w postaci kodu QR pod określonym kątem:

```csharp
qrCodeSignature.Angle = 30; // Obróć o 30 stopni
```

## Praca z różnymi formatami dokumentów
GroupDocs.Signature obsługuje aktualizację podpisów kodów QR w różnych formatach dokumentów:

- Dokumenty PDF
- Dokumenty Microsoft Word (DOC, DOCX)
- Arkusze kalkulacyjne Microsoft Excel (XLS, XLSX)
- Prezentacje Microsoft PowerPoint (PPT, PPTX)
- Formaty OpenDocument
- Formaty obrazów

Ten sam kod można wykorzystać w tych formatach, wprowadzając jedynie niewielkie modyfikacje.

## Wniosek
GroupDocs.Signature for .NET to wydajne i elastyczne rozwiązanie do aktualizacji podpisów kodów QR w dokumentach. Postępując zgodnie z instrukcjami opisanymi w tym samouczku, programiści mogą sprawnie wdrożyć funkcję aktualizacji podpisów kodów QR w swoich aplikacjach .NET, usprawniając zarządzanie dokumentami i możliwości uwierzytelniania.

Dzięki kompleksowemu zestawowi funkcji i intuicyjnemu interfejsowi API GroupDocs.Signature umożliwia deweloperom tworzenie zaawansowanych rozwiązań do podpisywania dokumentów, które spełniają wymagania nowoczesnych aplikacji biznesowych, a jednocześnie zapewniają integralność i dostępność dokumentów.

## Najczęściej zadawane pytania
### Czy mogę aktualizować wiele podpisów kodami QR w jednym dokumencie?
Tak, GroupDocs.Signature pozwala na aktualizację wielu podpisów kodem QR w tym samym dokumencie. Po wyszukaniu podpisów możesz przejrzeć listę wyników i zaktualizować każdy podpis kodem QR osobno.

### Czy GroupDocs.Signature obsługuje różne typy kodów QR?
Tak, GroupDocs.Signature obsługuje różne typy kodów QR, w tym standardowe QR, mikro QR i inne. Możesz określić typ kodu QR za pomocą `EncodeType` nieruchomość.

### Czy jest dostępna wersja próbna GroupDocs.Signature dla .NET?
Tak, możesz pobrać bezpłatną wersję próbną ze strony [Strona internetowa GroupDocs](https://releases.groupdocs.com/signature/net/) aby ocenić możliwości biblioteki przed dokonaniem zakupu.

### Czy mogę programowo zmienić poziom korekcji błędów kodu QR?
Tak, możesz zmienić poziom korekcji błędów podczas dodawania nowych kodów QR, ale aktualizacja tej właściwości w przypadku istniejących kodów QR może nie być obsługiwana we wszystkich formatach dokumentów.

### Gdzie mogę znaleźć dodatkowe wsparcie dla GroupDocs.Signature dla .NET?
Kompleksowe wsparcie możesz uzyskać, korzystając z następujących źródeł:
- [Dokumentacja API](https://docs.groupdocs.com/signature/net/)
- [Odniesienie do API](https://reference.groupdocs.com/signature/net/)
- [Przykłady GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Forum wsparcia](https://forum.groupdocs.com/c/signature/13)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)