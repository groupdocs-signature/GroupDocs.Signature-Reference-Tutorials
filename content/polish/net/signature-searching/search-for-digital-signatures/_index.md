---
"description": "Opanuj wyszukiwanie podpisów cyfrowych w dokumentach dzięki GroupDocs.Signature dla .NET. Zwiększ bezpieczeństwo i weryfikację dokumentów dzięki naszemu szczegółowemu przewodnikowi krok po kroku."
"linktitle": "Wyszukaj podpisy cyfrowe"
"second_title": "GroupDocs.Signature .NET API"
"title": "Wyszukaj podpisy cyfrowe w dokumentach"
"url": "/pl/net/signature-searching/search-for-digital-signatures/"
"weight": 11
---

## Wstęp

W dzisiejszym cyfrowym świecie zapewnienie autentyczności i integralności dokumentów ma kluczowe znaczenie dla firm i organizacji. Podpisy cyfrowe zapewniają niezawodny mechanizm weryfikacji autentyczności dokumentów i wykrywania nieautoryzowanych modyfikacji. GroupDocs.Signature for .NET oferuje kompleksowe rozwiązanie do pracy z podpisami cyfrowymi w różnych formatach dokumentów, umożliwiając programistom bezproblemową integrację funkcji podpisu z aplikacjami .NET.

tym samouczku dowiesz się, jak wyszukiwać podpisy cyfrowe w dokumentach za pomocą GroupDocs.Signature dla platformy .NET, a także poznasz szczegółowe wyjaśnienia i praktyczne przykłady kodu.

## Wymagania wstępne

Zanim zagłębisz się w szczegóły implementacji, upewnij się, że spełnione są następujące wymagania wstępne:

1. GroupDocs.Signature dla .NET: Pobierz i zainstaluj bibliotekę ze strony [Tutaj](https://releases.groupdocs.com/signature/net/).
   
2. Środowisko programistyczne: skonfiguruj środowisko programistyczne .NET za pomocą programu Visual Studio lub preferowanego środowiska IDE.
   
3. Przykładowe dokumenty: Przygotuj przykładowe dokumenty zawierające podpisy cyfrowe w celach testowych.

4. Podstawowa wiedza: Znajomość języka programowania C# i podstaw .NET Framework.

## Importuj przestrzenie nazw

Zacznij od zaimportowania wymaganych przestrzeni nazw, aby uzyskać dostęp do funkcjonalności zapewnianej przez GroupDocs.Signature dla .NET:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Podzielmy teraz proces wyszukiwania podpisów cyfrowych na jasne i łatwe do opanowania kroki:

## Krok 1: Zainicjuj obiekt podpisu

Zacznij od utworzenia instancji `Signature` klasa, przekazując ścieżkę do swojego dokumentu:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Tutaj zostanie dodany kod do wyszukiwania podpisów cyfrowych
}
```

## Krok 2: Wyszukaj podpisy cyfrowe

Następnie użyj `Search` metoda z `SignatureType.Digital` parametr umożliwiający wyszukiwanie podpisów cyfrowych w dokumencie:

```csharp
// Wyszukaj podpisy cyfrowe w dokumencie
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```

## Krok 3: Przetwarzanie i wyświetlanie wyników

Na koniec przetwórz wyniki wyszukiwania i wyświetl istotne informacje na temat znalezionych podpisów cyfrowych:

```csharp
Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
foreach (var digitalSignature in signatures)
{
    Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
    Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
    Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
    Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
    Console.WriteLine();
}
```

## Pełny przykład

Oto kompletny, działający przykład pokazujący, jak wyszukiwać podpisy cyfrowe w dokumencie:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SearchDigitalSignatures
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
                // Wyszukaj podpisy cyfrowe w dokumencie
                List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
                
                // Wyświetl wyniki wyszukiwania
                Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
                
                if (signatures.Count > 0)
                {
                    foreach (var digitalSignature in signatures)
                    {
                        Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
                        Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
                        Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
                        Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
                        Console.WriteLine();
                    }
                }
                else
                {
                    Console.WriteLine("No digital signatures found in the document.");
                }
            }
        }
    }
}
```

## Zaawansowane opcje wyszukiwania

Aby uzyskać bardziej szczegółowe wyszukiwania, możesz użyć `DigitalSearchOptions` aby dostosować kryteria wyszukiwania:

```csharp
// Utwórz opcje wyszukiwania cyfrowego
DigitalSearchOptions options = new DigitalSearchOptions()
{
    // Szukaj tylko na określonych stronach (np. na stronach 1 i 2)
    PageNumber = 1,
    PagesSetup = new PagesSetup() { Pages = new List<int> { 1, 2 } },
    
    // Filtruj według komentarzy w podpisach cyfrowych
    Comments = "Approved",
    
    // Ustaw zakres dat i godzin dla wyszukiwania
    SignDateTimeFrom = new DateTime(2022, 1, 1),
    SignDateTimeTo = DateTime.Now
};

// Szukaj z konkretnymi opcjami
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(options);
```

## Praca z informacjami o certyfikacie

Podpisy cyfrowe zawierają cenne informacje o certyfikacie, do których można uzyskać dostęp i które można zweryfikować:

```csharp
foreach (var digitalSignature in signatures)
{
    if (digitalSignature.Certificate != null)
    {
        // Dostęp do właściwości certyfikatu
        Console.WriteLine($"Certificate Valid From: {digitalSignature.Certificate.NotBefore}");
        Console.WriteLine($"Certificate Valid To: {digitalSignature.Certificate.NotAfter}");
        
        // Sprawdź, czy certyfikat mieści się w prawidłowym przedziale dat
        bool isDateValid = DateTime.Now >= digitalSignature.Certificate.NotBefore && 
                          DateTime.Now <= digitalSignature.Certificate.NotAfter;
        
        Console.WriteLine($"Certificate Date Validity: {isDateValid}");
        
        // Uzyskaj dostęp do szczegółów wystawcy certyfikatu
        Console.WriteLine($"Certificate Issuer: {digitalSignature.Certificate.IssuerName}");
    }
}
```

## Wniosek

GroupDocs.Signature for .NET to wydajne i elastyczne rozwiązanie do wyszukiwania i walidacji podpisów cyfrowych w dokumentach. W tym samouczku omówimy krok po kroku proces wdrażania funkcji wyszukiwania podpisów cyfrowych w aplikacjach .NET, wyposażając Cię w wiedzę niezbędną do zwiększenia bezpieczeństwa dokumentów i weryfikacji ich integralności.

Korzystając z GroupDocs.Signature, możesz zbudować solidny system zarządzania dokumentami, który zagwarantuje autentyczność i integralność Twoich dokumentów cyfrowych, wzmacniając zaufanie i zgodność z przepisami w procesach biznesowych.

## Najczęściej zadawane pytania

### Czy GroupDocs.Signature może zweryfikować ważność podpisów cyfrowych?

Tak, GroupDocs.Signature automatycznie weryfikuje podpisy cyfrowe podczas procesu wyszukiwania i zapewnia status weryfikacji za pomocą `IsValid` własność `DigitalSignature` klasa.

### Które formaty dokumentów obsługują wyszukiwanie podpisów cyfrowych?

GroupDocs.Signature obsługuje wyszukiwanie podpisów cyfrowych w różnych formatach, w tym PDF, dokumentach pakietu Microsoft Office (Word, Excel, PowerPoint), formatach OpenOffice i innych.

### Czy mogę wyszukiwać podpisy cyfrowe w dokumentach chronionych hasłem?

Tak, możesz wyszukiwać podpisy cyfrowe w dokumentach chronionych hasłem, podając hasło podczas inicjowania. `Signature` obiekt:

```csharp
LoadOptions loadOptions = new LoadOptions() { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Wyszukaj podpisy cyfrowe
}
```

### Jak mogę sprawdzić, czy podpis cyfrowy został złożony przez konkretną osobę?

Możesz sprawdzić nazwę podmiotu i inne właściwości certyfikatu, aby zweryfikować tożsamość osoby podpisującej:

```csharp
foreach (var signature in signatures)
{
    if (signature.Certificate?.SubjectName?.Contains("John Doe") == true)
    {
        Console.WriteLine("Found signature by John Doe");
    }
}
```

### Czy mogę wyodrębnić klucz publiczny z certyfikatu podpisu cyfrowego?

Tak, dostęp do informacji o kluczu publicznym można uzyskać za pomocą właściwości certyfikatu:

```csharp
if (signature.Certificate != null)
{
    // Dostęp do informacji o kluczu publicznym
    Console.WriteLine($"Public Key: {signature.Certificate.GetPublicKeyString()}");
}
```

## Zobacz także

* [Odniesienie do API](https://reference.groupdocs.com/signature/net/)
* [Przykłady kodu](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Dokumentacja produktu](https://docs.groupdocs.com/signature/net/)
* [Strona produktu](https://products.groupdocs.com/signature/net/)
* [Pobierz najnowszą wersję](https://releases.groupdocs.com/signature/net/)
* [Artykuły blogowe](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Forum wsparcia](https://forum.groupdocs.com/c/signature/13)
* [Licencja tymczasowa](https://purchase.groupdocs.com/temporary-license/)