---
"description": "Dowiedz się, jak skutecznie wyszukiwać kody QR w dokumentach przy użyciu GroupDocs.Signature dla .NET dzięki temu kompleksowemu przewodnikowi krok po kroku i przykładom kodu."
"linktitle": "Wyszukaj kody QR"
"second_title": "GroupDocs.Signature .NET API"
"title": "Wyszukaj podpisy w postaci kodu QR w dokumentach"
"url": "/pl/net/signature-searching/search-for-qr-codes/"
"weight": 15
---

## Wstęp

W dzisiejszym ekosystemie dokumentów cyfrowych podpisy kodami QR stały się nieocenionym narzędziem do osadzania informacji, uwierzytelniania i zwiększania bezpieczeństwa dokumentów. GroupDocs.Signature for .NET oferuje programistom zaawansowane API do wyszukiwania i wyodrębniania kodów QR z różnych formatów dokumentów, umożliwiając zaawansowaną analizę i weryfikację dokumentów w aplikacjach .NET.

Ten kompleksowy samouczek przeprowadzi Cię przez proces wdrażania funkcji wyszukiwania kodów QR przy użyciu GroupDocs.Signature dla .NET, zapewniając przejrzyste wyjaśnienia, instrukcje krok po kroku i praktyczne przykłady kodu, które możesz zintegrować we własnych aplikacjach.

## Wymagania wstępne

Zanim zaczniesz szukać podpisów za pomocą kodu QR, upewnij się, że spełniasz następujące wymagania wstępne:

1. GroupDocs.Signature dla .NET SDK: Pobierz i zainstaluj SDK z [strona pobierania](https://releases.groupdocs.com/signature/net/).

2. Środowisko programistyczne: skonfiguruj środowisko programistyczne .NET, takie jak Visual Studio, z zainstalowanym .NET Framework lub .NET Core.

3. Wiedza podstawowa: Znajomość programowania w języku C# i koncepcji rozwoju .NET.

4. Przykładowe dokumenty: Przygotuj dokumenty testowe zawierające kody QR do weryfikacji i testowania.

## Importuj przestrzenie nazw

Zacznij od zaimportowania niezbędnych przestrzeni nazw, aby uzyskać dostęp do funkcjonalności GroupDocs.Signature:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;
```

Teraz omówmy proces wyszukiwania kodów QR na jasne i łatwe do wykonania kroki:

## Krok 1: Zdefiniuj ścieżkę dokumentu

Najpierw określ ścieżkę do dokumentu zawierającego kody QR, które chcesz przeszukać:

```csharp
string filePath = "sample_multiple_signatures.docx";
```

## Krok 2: Zainicjuj obiekt podpisu

Utwórz instancję `Signature` klasę przekazując ścieżkę dokumentu:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Tutaj zostanie dodany kod wyszukiwania kodu QR
}
```

## Krok 3: Wyszukaj podpisy w postaci kodu QR

Użyj `Search` metoda z odpowiednim typem podpisu do znajdowania kodów QR w dokumencie:

```csharp
// Wyszukaj podpisy w postaci kodu QR w dokumencie
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

## Krok 4: Przetwarzanie i wyświetlanie wyników

Przejrzyj znalezione podpisy kodów QR i uzyskaj dostęp do ich właściwości:

```csharp
// Wyświetl informacje o znalezionych kodach QR
Console.WriteLine($"\nSource document contains {signatures.Count} QR code signature(s):");

foreach (var qrCodeSignature in signatures)
{
    Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
    Console.WriteLine($"Content: {qrCodeSignature.Text}");
    Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
    Console.WriteLine();
}
```

## Pełny przykład

Oto kompleksowy przykład działania, który demonstruje cały proces wyszukiwania kodów QR w dokumencie:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;

namespace QrCodeSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Ścieżka dokumentu – zaktualizuj ją, wpisując ścieżkę do pliku
            string filePath = "sample_multiple_signatures.docx";
            
            // Zainicjuj instancję podpisu
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Wyszukaj podpisy w postaci kodu QR w dokumencie
                    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
                    
                    // Wyświetl wyniki wyszukiwania
                    Console.WriteLine($"\nSource document ['{filePath}'] contains {signatures.Count} QR code signature(s):");
                    
                    foreach (var qrCodeSignature in signatures)
                    {
                        Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
                        Console.WriteLine($"Content: {qrCodeSignature.Text}");
                        Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
                        Console.WriteLine();
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

## Zaawansowane techniki wyszukiwania kodów QR

### Wyszukiwanie według określonych kryteriów

Aby uzyskać bardziej szczegółowe wyszukiwania, możesz użyć `QrCodeSearchOptions` aby dostosować kryteria wyszukiwania:

```csharp
// Utwórz opcje wyszukiwania kodów QR z określonymi kryteriami
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    // Szukaj tylko na określonych stronach
    AllPages = false,
    PageNumber = 1,
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // Filtruj według zawartości kodu QR
    Text = "Invoice",
    MatchType = TextMatchType.Contains,
    
    // Filtruj według określonych typów kodów QR
    EncodeType = QrCodeTypes.QR,
    
    // Zdefiniuj konkretny obszar, w którym chcesz przeprowadzić wyszukiwanie
    Rectangle = new Rectangle(100, 100, 400, 400)
};

// Szukaj z konkretnymi opcjami
List<QrCodeSignature> filteredSignatures = signature.Search<QrCodeSignature>(options);
```

### Przetwarzanie danych kodu QR

Możesz wdrożyć niestandardowe przetwarzanie danych z kodu QR w oparciu o wymagania swojej aplikacji:

```csharp
foreach (var qrCode in signatures)
{
    // Ekstrakcja i przetwarzanie danych z kodu QR na podstawie treści
    string qrContent = qrCode.Text;
    
    if (qrContent.StartsWith("URL:"))
    {
        // Przetwarzaj dane URL
        string url = qrContent.Substring(4);
        Console.WriteLine($"Found URL in QR code: {url}");
    }
    else if (qrContent.StartsWith("CONTACT:"))
    {
        // Przetwarzaj informacje kontaktowe
        string contact = qrContent.Substring(8);
        Console.WriteLine($"Found contact information in QR code: {contact}");
    }
    else if (qrContent.StartsWith("INVOICE:"))
    {
        // Przetwarzaj informacje o fakturze
        string invoiceData = qrContent.Substring(8);
        Console.WriteLine($"Found invoice information in QR code: {invoiceData}");
        
        // Analizuj i weryfikuj dane faktur
        if (ValidateInvoiceData(invoiceData))
        {
            Console.WriteLine("Invoice data is valid!");
        }
        else
        {
            Console.WriteLine("Warning: Invalid invoice data detected!");
        }
    }
}

// Przykładowa metoda walidacji
static bool ValidateInvoiceData(string data)
{
    // Wdróż swoją logikę walidacji
    return !string.IsNullOrEmpty(data) && data.Contains("ID") && data.Contains("Amount");
}
```

### Wdrażanie weryfikacji bezpieczeństwa

Kody QR są często wykorzystywane do uwierzytelniania. Oto jak wdrożyć podstawową weryfikację bezpieczeństwa:

```csharp
// Sprawdź, czy dokument zawiera prawidłowy kod QR uwierzytelniający
bool hasValidAuthQrCode = false;

foreach (var qrCode in signatures)
{
    if (qrCode.Text.StartsWith("AUTH:"))
    {
        string authCode = qrCode.Text.Substring(5);
        
        // Zweryfikuj kod uwierzytelniający (np. w oparciu o bazę danych lub wstępnie zdefiniowaną listę)
        if (VerifyAuthCode(authCode))
        {
            hasValidAuthQrCode = true;
            Console.WriteLine("Document contains valid authentication QR code!");
            break;
        }
    }
}

if (!hasValidAuthQrCode)
{
    Console.WriteLine("Warning: Document does not contain a valid authentication QR code!");
}

// Przykładowa metoda weryfikacji
static bool VerifyAuthCode(string code)
{
    // Wdróż swoją logikę weryfikacji
    // Może to być wyszukiwanie w bazie danych, wywołanie API lub porównanie z predefiniowanymi wartościami
    return code == "A7B82C3D" || code == "X9Y8Z7W6";
}
```

### Wyodrębnianie obrazów kodów QR

Możesz wyodrębnić obrazy kodów QR z dokumentów w celu dalszego przetwarzania lub wyświetlania:

```csharp
// Zapisz obrazy kodów QR na dysku
foreach (var qrCode in signatures)
{
    if (qrCode.Content != null)
    {
        // Utwórz unikalną nazwę pliku na podstawie numeru strony i pozycji
        string outputPath = $"QrCode_P{qrCode.PageNumber}_X{qrCode.Left}_Y{qrCode.Top}.png";
        
        // Zapisz dane obrazu
        File.WriteAllBytes(outputPath, qrCode.Content);
        Console.WriteLine($"Saved QR code image to {outputPath}");
    }
}
```

## Wniosek

W tym kompleksowym przewodniku omówimy wyszukiwanie podpisów w postaci kodów QR w dokumentach za pomocą GroupDocs.Signature dla platformy .NET. Od podstawowego wyszukiwania po zaawansowane techniki – teraz posiadasz wiedzę niezbędną do wdrożenia sprawnej obsługi kodów QR w aplikacjach .NET. Interfejs API GroupDocs.Signature zapewnia wydajne i elastyczne środowisko do pracy z różnymi typami podpisów, w tym kodami QR, w różnych formatach dokumentów.

Wykorzystując te możliwości, możesz usprawnić procesy weryfikacji dokumentów, wdrożyć systemy uwierzytelniania i wyodrębnić cenne informacje osadzone w kodach QR — wszystko w aplikacjach .NET.

## Najczęściej zadawane pytania

### Jakie formaty kodów QR są obsługiwane przez GroupDocs.Signature?

GroupDocs.Signature obsługuje różne formaty kodów QR, w tym standardowy kod QR, mikrokod QR i inne popularne standardy kodów QR. Dostęp do konkretnego formatu można uzyskać za pomocą `EncodeType` własność `QrCodeSignature` obiekt.

### Czy mogę wyszukiwać kody QR w dokumentach chronionych hasłem?

Tak, GroupDocs.Signature obsługuje wyszukiwanie kodów QR w dokumentach chronionych hasłem poprzez podanie hasła podczas inicjowania. `Signature` obiekt:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Wyszukaj kody QR
}
```

### Jak mogę filtrować kody QR na podstawie ich zawartości?

Możesz filtrować kody QR na podstawie ich zawartości, korzystając z `Text` I `MatchType` właściwości `QrCodeSearchOptions`:

```csharp
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    Text = "Invoice",
    MatchType = TextMatchType.Contains // Inne opcje: Dokładny, Zaczyna się od, Kończy się od
};
```

### Czy GroupDocs.Signature może wykryć uszkodzone lub częściowo widoczne kody QR?

GroupDocs.Signature ma pewną zdolność wykrywania częściowo widocznych kodów QR, ale mocno uszkodzone kody QR mogą nie zostać rozpoznane. Dokładność wykrywania zależy od jakości i widoczności kodu QR w dokumencie.

### Jakie formaty dokumentów są obsługiwane w przypadku wyszukiwania kodów QR?

GroupDocs.Signature obsługuje wyszukiwanie kodów QR w różnych formatach dokumentów, w tym PDF, dokumentach Microsoft Office (Word, Excel, PowerPoint), obrazach (JPEG, PNG, TIFF) i wielu innych.

## Zobacz także

* [Odniesienie do API](https://reference.groupdocs.com/signature/net/)
* [Przykłady kodu na GitHubie](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Dokumentacja produktu](https://docs.groupdocs.com/signature/net/)
* [Strona produktu](https://products.groupdocs.com/signature/net/)
* [Pobierz najnowszą wersję](https://releases.groupdocs.com/signature/net/)
* [Artykuły blogowe](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Bezpłatne forum wsparcia](https://forum.groupdocs.com/c/signature/13)
* [Licencja tymczasowa](https://purchase.groupdocs.com/temporary-license/)