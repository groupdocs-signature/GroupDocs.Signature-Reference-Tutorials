---
title: Podpisywanie tekstowe przy użyciu GroupDocs.Signature dla .NET
linktitle: Podpisywanie tekstem
second_title: GroupDocs.Signature .NET API
description: Dowiedz się, jak podpisywać dokumenty tekstem za pomocą GroupDocs.Signature dla .NET. Przewodnik krok po kroku dotyczący programowego dodawania podpisów tekstowych.
weight: 17
url: /pl/net/advanced-signature-techniques/sign-with-text/
---
## Wstęp
W epoce cyfrowej podpisywanie dokumentów drogą elektroniczną stało się standardową praktyką, oszczędzając czas i zasoby. GroupDocs.Signature dla .NET oferuje kompleksowe rozwiązanie do programowego dodawania podpisów tekstowych do różnych formatów dokumentów. W tym samouczku przeprowadzimy Cię przez proces podpisywania dokumentu tekstem przy użyciu programu GroupDocs.Signature for .NET.
## Warunki wstępne
Zanim przejdziemy do samouczka, upewnij się, że spełniasz następujące wymagania wstępne:
1.  GroupDocs.Signature for .NET: Upewnij się, że masz zainstalowaną bibliotekę GroupDocs.Signature for .NET. Można go pobrać z[Tutaj](https://releases.groupdocs.com/signature/net/).
2. Środowisko programistyczne: Przygotuj środowisko pracy do programowania .NET.
3. Dokument: Przygotuj dokument (np. PDF, Word), który chcesz podpisać tekstem.

## Importuj przestrzenie nazw
Najpierw musisz zaimportować niezbędne przestrzenie nazw do projektu .NET, aby móc korzystać z funkcjonalności GroupDocs.Signature.
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Podzielmy proces podpisywania dokumentu tekstem na kilka etapów:
## Krok 1: Załaduj dokument
Załaduj dokument, który chcesz podpisać tekstem.
```csharp
string filePath = "sample.pdf"; // Ścieżka do dokumentu
string fileName = Path.GetFileName(filePath);
```
## Krok 2: Ustaw ścieżkę pliku wyjściowego
Określ ścieżkę pliku wyjściowego, w którym zostanie zapisany podpisany dokument.
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithText", fileName);
```
## Krok 3: Utwórz opcje podpisu
Skonfiguruj opcje podpisu tekstowego, w tym treść tekstu, położenie, rozmiar, kolor i czcionkę.
```csharp
TextSignOptions options = new TextSignOptions("John Smith")
{
    Left = 50, // Ustaw pozycję podpisu
    Top = 200,
    Width = 100, // Ustaw prostokąt podpisu
    Height = 30,
    ForeColor = Color.Red, // Ustaw kolor tekstu
    Font = new SignatureFont { Size = 14, FamilyName = "Comic Sans MS" } // Ustaw czcionkę
};
```
## Krok 4: Podpisz dokument
Użyj GroupDocs.Signature, aby podpisać dokument przy użyciu określonych opcji i zapisać podpisany dokument w ścieżce pliku wyjściowego.
```csharp
using (Signature signature = new Signature(filePath))
{
    SignResult result = signature.Sign(outputFilePath, options); // Podpisz dokument
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Wniosek
tym samouczku nauczyliśmy się, jak podpisywać dokument tekstem przy użyciu programu GroupDocs.Signature for .NET. Wykonując poniższe kroki, możesz efektywnie i programowo dodawać podpisy tekstowe do swoich dokumentów, zwiększając bezpieczeństwo i autentyczność.
## Często zadawane pytania
### Czy mogę dostosować wygląd podpisu tekstowego?
Tak, możesz dostosować różne parametry, takie jak kolor, czcionka, rozmiar i położenie podpisu tekstowego, zgodnie ze swoimi preferencjami.
### Czy GroupDocs.Signature jest kompatybilny z wieloma formatami dokumentów?
Tak, GroupDocs.Signature obsługuje różne formaty dokumentów, w tym PDF, Word, Excel, PowerPoint i inne.
### Czy mogę dodać wiele podpisów tekstowych do jednego dokumentu?
Oczywiście możesz dodać wiele podpisów tekstowych do dokumentu, każdy z własnym zestawem opcji dostosowywania.
### Czy GroupDocs.Signature zapewnia integralność dokumentu po podpisaniu?
Tak, GroupDocs.Signature wykorzystuje niezawodne algorytmy kryptograficzne, aby zapewnić integralność dokumentów i zapobiec manipulacji po podpisaniu.
### Czy dostępna jest wersja próbna do przetestowania przed zakupem?
 Tak, możesz pobrać bezpłatną wersję próbną ze strony[Tutaj](https://releases.groupdocs.com/) aby zapoznać się z funkcjami przed dokonaniem zakupu.