---
title: Podpisywanie dokumentów kodem QR za pomocą GroupDocs.Signature
linktitle: Podpisywanie za pomocą kodu QR
second_title: GroupDocs.Signature .NET API
description: Dowiedz się, jak dodawać podpisy kodem QR do swoich dokumentów za pomocą GroupDocs.Signature for .NET. Bez wysiłku zwiększ bezpieczeństwo i uwierzytelnianie.
weight: 15
url: /pl/net/advanced-signature-techniques/sign-with-qr-code/
---

# Podpisywanie dokumentów kodem QR za pomocą GroupDocs.Signature

## Wstęp
tym samouczku omówimy proces podpisywania dokumentów kodem QR przy użyciu programu GroupDocs.Signature for .NET. GroupDocs.Signature dla .NET to potężny interfejs API, który umożliwia programistom programowe dodawanie różnych typów podpisów do dokumentów cyfrowych. Podpisywanie dokumentów kodami QR może zapewnić dodatkową warstwę bezpieczeństwa i uwierzytelniania dokumentów.
## Warunki wstępne
Zanim zaczniemy, upewnij się, że masz zainstalowane następujące wymagania wstępne:
1.  GroupDocs.Signature dla .NET: Bibliotekę można pobrać z witryny[strona internetowa](https://releases.groupdocs.com/signature/net/).
2. Środowisko programistyczne: Upewnij się, że na komputerze jest skonfigurowane środowisko programistyczne .NET.
3. Przykładowy dokument: Przygotuj przykładowy dokument (np. PDF), który chcesz podpisać kodem QR.

## Importowanie niezbędnych przestrzeni nazw
Zanim zagłębimy się w kod, zaimportujmy niezbędne przestrzenie nazw:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Krok 1: Zdefiniuj ścieżki plików
```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "SignWithQRCode", fileName);
```
 Pamiętaj o wymianie`"Your Document Directory"` ze ścieżką do katalogu, w którym chcesz zapisać podpisany dokument.
## Krok 2: Zainicjuj obiekt podpisu
```csharp
using (Signature signature = new Signature(filePath))
{
    //Kod do podpisania znajduje się tutaj
}
```
 Zainicjuj a`Signature` obiekt ze ścieżką do dokumentu, który chcesz podpisać.
## Krok 3: Utwórz opcje QRCodeSign
```csharp
QrCodeSignOptions options = new QrCodeSignOptions("JohnSmith")
{
    EncodeType = QrCodeTypes.QR,
    Left = 50,
    Top = 150,
    Width = 200,
    Height = 200
};
```
 Stwórz`QrCodeSignOptions` obiekt z żądanymi ustawieniami podpisu w postaci kodu QR. Możesz dostosować parametry, takie jak tekst do zakodowania, położenie i wymiary kodu QR.
## Krok 4: Podpisz dokument
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
 Użyj`Sign` metoda`Signature` obiekt, aby podpisać dokument z określonymi opcjami. Ta metoda zwraca a`SignResult` obiekt zawierający informację o procesie podpisywania.
## Krok 5: Wyświetl wynik
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
Wyświetl komunikat informujący o powodzeniu procesu podpisywania i lokalizacji, w której zapisano podpisany dokument.

## Wniosek
W tym samouczku nauczyliśmy się podpisywać dokumenty kodem QR przy użyciu programu GroupDocs.Signature for .NET. Wykonując te proste kroki, możesz dodać podpisy kodów QR do swoich dokumentów cyfrowych, zwiększając bezpieczeństwo i uwierzytelnianie.

## Często zadawane pytania
### Czy mogę dostosować wygląd kodu QR?
Tak, możesz dostosować różne parametry, takie jak rozmiar, położenie i typ kodowania kodu QR, zgodnie z własnymi wymaganiami.
### Jakie formaty dokumentów są obsługiwane przy podpisywaniu kodami QR?
GroupDocs.Signature dla .NET obsługuje szeroką gamę formatów dokumentów, w tym PDF, Word, Excel, PowerPoint i inne.
### Czy możliwe jest podpisanie wielu dokumentów w procesie wsadowym?
Oczywiście możesz używać GroupDocs.Signature for .NET do jednoczesnego podpisywania wielu dokumentów, usprawniając przepływ pracy.
### Czy mogę zweryfikować autentyczność dokumentu podpisanego kodem QR?
Tak, GroupDocs.Signature for .NET udostępnia mechanizmy weryfikacji zapewniające integralność i autentyczność podpisanych dokumentów.
### Czy dostępna jest wersja próbna umożliwiająca przetestowanie funkcjonalności przed zakupem?
 Tak, możesz pobrać bezpłatną wersję próbną ze strony[strona internetowa](https://releases.groupdocs.com/) aby ocenić funkcje i możliwości GroupDocs.Signature dla .NET.