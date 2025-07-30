---
"description": "Dowiedz się, jak wyszukiwać wiele typów podpisów w dokumentach za pomocą GroupDocs.Signature dla .NET. Kompleksowy przewodnik z przykładami kodu, który zwiększa bezpieczeństwo dokumentów."
"linktitle": "Wyszukaj wiele podpisów"
"second_title": "GroupDocs.Signature .NET API"
"title": "Wyszukaj wiele typów podpisów w dokumentach"
"url": "/pl/net/signature-searching/search-for-multiple-signatures/"
"weight": 14
---

## Wstęp

nowoczesnych systemach zarządzania dokumentami coraz ważniejsza staje się możliwość wyszukiwania i weryfikacji wielu typów podpisów w jednym dokumencie. Organizacje często stosują różne typy podpisów – takie jak podpisy cyfrowe, podpisy tekstowe, kody kreskowe, kody QR i inne – w celu zwiększenia bezpieczeństwa dokumentów i usprawnienia procesów weryfikacji. GroupDocs.Signature for .NET zapewnia zaawansowane środowisko, które umożliwia programistom implementację kompleksowej funkcji wyszukiwania podpisów w różnych formatach dokumentów.

W tym samouczku dowiesz się, jak wyszukiwać różne typy podpisów w dokumentach przy użyciu GroupDocs.Signature dla platformy .NET, a także poznasz szczegółowe wyjaśnienia i praktyczne przykłady kodu.

## Wymagania wstępne

Zanim przejdziesz do implementacji funkcji wyszukiwania wielosygnaturowego, upewnij się, że spełnione są następujące wymagania wstępne:

1. Środowisko programistyczne: Visual Studio lub dowolne preferowane środowisko programistyczne .NET zainstalowane w systemie.
  
2. GroupDocs.Signature dla .NET: Pobierz i zainstaluj bibliotekę GroupDocs.Signature dla .NET z [Tutaj](https://releases.groupdocs.com/signature/net/).

3. Podstawowa wiedza z zakresu języka C#: Znajomość języka programowania C# i koncepcji .NET Framework.

4. Przykładowe dokumenty: Przygotuj dokumenty testowe zawierające różne rodzaje podpisów na potrzeby testowania.

## Importuj przestrzenie nazw

Zacznij od zaimportowania niezbędnych przestrzeni nazw, aby uzyskać dostęp do funkcjonalności GroupDocs.Signature:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Podzielmy teraz proces wyszukiwania różnych typów podpisów na jasne i łatwe do opanowania kroki:

## Krok 1: Załaduj dokument

Najpierw wczytaj dokument zawierający podpisy, które chcesz przeszukać:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Tutaj zostanie dodany kod wyszukiwania wielopodpisowego
}
```

## Krok 2: Zdefiniuj opcje wyszukiwania dla różnych typów podpisów

Utwórz opcje wyszukiwania dla każdego typu podpisu, którego chcesz szukać:

```csharp
// Zdefiniuj opcje wyszukiwania podpisów tekstowych
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,  // Szukaj na wszystkich stronach
    Text = "Signature",  // Opcjonalnie: tekst do znalezienia
    MatchType = TextMatchType.Contains  // Kryteria dopasowania
};

// Zdefiniuj opcje wyszukiwania podpisów cyfrowych
DigitalSearchOptions digitalOptions = new DigitalSearchOptions
{
    AllPages = true
};

// Zdefiniuj opcje wyszukiwania podpisów kodów kreskowych
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
{
    AllPages = true,
    Text = "123456",  // Opcjonalnie: tekst kodu kreskowego do dopasowania
    MatchType = TextMatchType.Exact  // Kryteria dopasowania
};

// Zdefiniuj opcje wyszukiwania podpisów w postaci kodów QR
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
{
    AllPages = true,
    Text = "John",  // Opcjonalnie: tekst kodu QR do dopasowania
    MatchType = TextMatchType.Contains  // Kryteria dopasowania
};

// Zdefiniuj opcje wyszukiwania dla podpisów metadanych
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```

## Krok 3: Dodaj opcje do kolekcji

Dodaj wszystkie opcje wyszukiwania do kolekcji:

```csharp
// Utwórz listę zawierającą wszystkie opcje wyszukiwania
List<SearchOptions> searchOptions = new List<SearchOptions>
{
    textOptions,
    digitalOptions,
    barcodeOptions,
    qrCodeOptions,
    metadataOptions
};
```

## Krok 4: Wykonaj wyszukiwanie i przetwórz wyniki

Wykonaj wyszukiwanie korzystając z opcji wyszukiwania łączonego i przetwórz wyniki:

```csharp
// Wyszukaj wszystkie typy podpisów, korzystając ze zdefiniowanych opcji
SearchResult result = signature.Search(searchOptions);

// Sprawdź, czy znaleziono podpisy
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
    
    // Przejrzyj znalezione podpisy
    foreach (var foundSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}, ID: {foundSignature.SignatureId}");
        
        // Typy podpisów specyficzne dla procesu
        if (foundSignature is TextSignature textSignature)
        {
            Console.WriteLine($"Text: '{textSignature.Text}'");
        }
        else if (foundSignature is BarcodeSignature barcodeSignature)
        {
            Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
        }
        else if (foundSignature is QrCodeSignature qrCodeSignature)
        {
            Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
        }
        else if (foundSignature is DigitalSignature digitalSignature)
        {
            Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
        }
        else if (foundSignature is MetadataSignature metadataSignature)
        {
            Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
        }
    }
}
else
{
    Console.WriteLine("No signatures were found in the document.");
}
```

## Pełny przykład

Oto kompletny, działający przykład demonstrujący wyszukiwanie wielu typów podpisów w dokumencie:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace MultiSignatureSearch
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
                try
                {
                    // Zdefiniuj opcje wyszukiwania podpisów tekstowych
                    TextSearchOptions textOptions = new TextSearchOptions
                    {
                        AllPages = true,
                        MatchType = TextMatchType.Contains
                    };

                    // Zdefiniuj opcje wyszukiwania podpisów cyfrowych
                    DigitalSearchOptions digitalOptions = new DigitalSearchOptions
                    {
                        AllPages = true
                    };

                    // Zdefiniuj opcje wyszukiwania podpisów kodów kreskowych
                    BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Zdefiniuj opcje wyszukiwania podpisów w postaci kodów QR
                    QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Zdefiniuj opcje wyszukiwania dla podpisów metadanych
                    MetadataSearchOptions metadataOptions = new MetadataSearchOptions();

                    // Utwórz listę zawierającą wszystkie opcje wyszukiwania
                    List<SearchOptions> searchOptions = new List<SearchOptions>
                    {
                        textOptions,
                        digitalOptions,
                        barcodeOptions,
                        qrCodeOptions,
                        metadataOptions
                    };

                    // Wyszukaj wszystkie typy podpisów
                    SearchResult result = signature.Search(searchOptions);

                    // Sprawdź, czy znaleziono podpisy
                    if (result.Signatures.Count > 0)
                    {
                        Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
                        
                        // Wyniki procesu według typu podpisu
                        foreach (var foundSignature in result.Signatures)
                        {
                            Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}");
                            
                            // Typy podpisów specyficzne dla procesu
                            switch (foundSignature.SignatureType)
                            {
                                case SignatureType.Text:
                                    var textSignature = foundSignature as TextSignature;
                                    Console.WriteLine($"Text: '{textSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Barcode:
                                    var barcodeSignature = foundSignature as BarcodeSignature;
                                    Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.QrCode:
                                    var qrCodeSignature = foundSignature as QrCodeSignature;
                                    Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Digital:
                                    var digitalSignature = foundSignature as DigitalSignature;
                                    Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
                                    break;
                                    
                                case SignatureType.Metadata:
                                    var metadataSignature = foundSignature as MetadataSignature;
                                    Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
                                    break;
                            }
                            
                            Console.WriteLine(); // Dodaj podział wiersza między podpisami
                        }
                    }
                    else
                    {
                        Console.WriteLine("No signatures were found in the document.");
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"Error occurred: {ex.Message}");
                }
            }
            
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## Zaawansowane techniki wyszukiwania wielosygnaturowego

### Filtrowanie wyników wyszukiwania

Aby zawęzić wyniki wyszukiwania, możesz zastosować zaawansowane filtrowanie:

```csharp
// Filtruj wyniki według numeru strony
var signaturesOnFirstPage = result.Signatures.FindAll(s => s.PageNumber == 1);

// Filtruj wyniki według typu podpisu
var digitalSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.Digital);
var qrCodeSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.QrCode);

// Filtruj podpisy tekstowe zawierające określoną treść
var approvalSignatures = result.Signatures
    .FindAll(s => s is TextSignature && ((TextSignature)s).Text.Contains("Approved"));
```

### Sprawdzanie wiarygodności wielu podpisów

Wdrożenie logiki walidacji dla różnych typów podpisów:

```csharp
bool ValidateAllSignatures(SearchResult result)
{
    bool isDocumentValid = true;
    
    // Sprawdź, czy dokument ma ważny podpis cyfrowy
    bool hasValidDigitalSignature = result.Signatures
        .Any(s => s is DigitalSignature && ((DigitalSignature)s).IsValid);
    
    if (!hasValidDigitalSignature)
    {
        Console.WriteLine("Warning: Document does not contain a valid digital signature");
        isDocumentValid = false;
    }
    
    // Sprawdź, czy dokument ma wymagany kod QR
    bool hasRequiredQRCode = result.Signatures
        .Any(s => s is QrCodeSignature && ((QrCodeSignature)s).Text.Contains("Auth-Code"));
    
    if (!hasRequiredQRCode)
    {
        Console.WriteLine("Warning: Document does not contain the required authentication QR code");
        isDocumentValid = false;
    }
    
    return isDocumentValid;
}
```

### Wyszukiwanie z przetwarzaniem niestandardowym

Można zdefiniować niestandardową logikę przetwarzania dla operacji wyszukiwania:

```csharp
// Utwórz opcje wyszukiwania z niestandardowym przetwarzaniem
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,
    
    // Zdefiniuj przetwarzanie niestandardowe za pomocą delegata
    ProcessCompleted = (signature) =>
    {
        // Niestandardowa logika walidacji – akceptuj podpisy tylko na określonych stronach
        TextSignature textSignature = signature as TextSignature;
        return textSignature != null && (textSignature.PageNumber == 1 || textSignature.PageNumber == 2);
    }
};
```

## Wniosek

W tym kompleksowym przewodniku omówimy, jak wyszukiwać wiele typów podpisów w dokumentach za pomocą GroupDocs.Signature dla platformy .NET. Od konfigurowania opcji wyszukiwania dla różnych typów podpisów, po przetwarzanie i weryfikację wyników – teraz posiadasz wiedzę niezbędną do wdrożenia zaawansowanej funkcji wyszukiwania podpisów w aplikacjach .NET.

Możliwość jednoczesnego wyszukiwania wielu typów podpisów usprawnia procesy weryfikacji dokumentów, wzmacnia środki bezpieczeństwa i usprawnia przepływy pracy związane z walidacją dokumentów. GroupDocs.Signature zapewnia wydajne i elastyczne środowisko do pracy z różnymi typami podpisów w różnych formatach dokumentów, co czyni je doskonałym wyborem dla aplikacji do przetwarzania dokumentów.

## Najczęściej zadawane pytania

### Czy mogę wyszukiwać podpisy w dokumentach chronionych hasłem?

Tak, GroupDocs.Signature obsługuje wyszukiwanie podpisów w dokumentach chronionych hasłem. Hasło można podać podczas inicjalizacji. `Signature` obiekt:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Wyszukaj podpisy
}
```

### Które formaty dokumentów są obsługiwane w przypadku wyszukiwania podpisów?

GroupDocs.Signature obsługuje szeroką gamę formatów dokumentów, w tym pliki PDF, dokumenty pakietu Microsoft Office (Word, Excel, PowerPoint), formaty OpenOffice, obrazy i inne.

### Czy mogę ograniczyć wyszukiwanie do konkretnych stron w dokumencie?

Tak, każdy typ opcji wyszukiwania ma właściwości pozwalające określić, na których stronach chcesz przeprowadzić wyszukiwanie:

```csharp
TextSearchOptions options = new TextSearchOptions
{
    AllPages = false,  // Nie przeszukuj wszystkich stron
    PageNumber = 1,    // Szukaj tylko na stronie 1
    
    // Lub określ wiele stron
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } }
};
```

### Jak mogę zoptymalizować wydajność wyszukiwania w dużych dokumentach?

W przypadku dużych dokumentów wydajność można zoptymalizować poprzez:

1. Ograniczanie wyszukiwania do określonych stron lub zakresów stron
2. Korzystanie z bardziej szczegółowych kryteriów wyszukiwania w celu ograniczenia liczby potencjalnych dopasowań
3. Wdrażanie paginacji w wyświetlaniu wyników
4. Wyszukiwanie jednego typu podpisu na raz, jeśli nie potrzebujesz jednoczesnych wyników

### Czy mogę rozszerzyć GroupDocs.Signature o obsługę niestandardowych typów podpisów?

Chociaż GroupDocs.Signature zapewnia wbudowaną obsługę popularnych typów podpisów, możesz rozszerzyć jej funkcjonalność poprzez:

1. Tworzenie niestandardowych klas opcji wyszukiwania pochodzących z `SearchOptions`
2. Implementacja niestandardowej logiki przetwarzania przy użyciu `ProcessCompleted` delegat
3. Opracowywanie klas opakowujące łączące wyszukiwanie wielu sygnatur z zaawansowaną logiką biznesową

## Zobacz także

* [Odniesienie do API](https://reference.groupdocs.com/signature/net/)
* [Przykłady kodu na GitHubie](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Dokumentacja produktu](https://docs.groupdocs.com/signature/net/)
* [Strona produktu](https://products.groupdocs.com/signature/net/)
* [Pobierz najnowszą wersję](https://releases.groupdocs.com/signature/net/)
* [Artykuły blogowe](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Bezpłatne forum wsparcia](https://forum.groupdocs.com/c/signature/13)
* [Licencja tymczasowa](https://purchase.groupdocs.com/temporary-license/)