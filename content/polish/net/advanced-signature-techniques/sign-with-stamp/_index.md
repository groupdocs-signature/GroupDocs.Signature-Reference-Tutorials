---
title: Podpisywanie za pomocą stempla przy użyciu GroupDocs.Signature
linktitle: Podpisanie pieczątką
second_title: GroupDocs.Signature .NET API
description: Dowiedz się, jak łatwo dodawać podpisy pieczęci do dokumentów .NET za pomocą GroupDocs.Signature for .NET. Zwiększ bezpieczeństwo dokumentów.
weight: 16
url: /pl/net/advanced-signature-techniques/sign-with-stamp/
---

# Podpisywanie za pomocą stempla przy użyciu GroupDocs.Signature

## Wstęp
W tym samouczku przeprowadzimy Cię przez proces podpisywania dokumentu pieczątką przy użyciu programu GroupDocs.Signature for .NET. Postępując zgodnie z tymi szczegółowymi instrukcjami, będziesz mógł z łatwością dodać podpis pieczątki do swoich dokumentów.
## Warunki wstępne
Zanim zaczniemy, upewnij się, że masz następujące wymagania wstępne:
1.  GroupDocs.Signature for .NET SDK: Pobierz i zainstaluj zestaw SDK z[strona internetowa](https://releases.groupdocs.com/signature/net/).
2. Środowisko programistyczne: Upewnij się, że masz skonfigurowane odpowiednie środowisko programistyczne do programowania .NET.
3. Dokument do podpisania: Przygotuj dokument (np. PDF), który chcesz podpisać pieczątką.

## Importowanie przestrzeni nazw
Zacznij od zaimportowania niezbędnych przestrzeni nazw do swojego projektu:
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Krok 1: Załaduj dokument
```csharp
string filePath = "sample.pdf";
using (Signature signature = new Signature(filePath))
{
    // Twój kod trafia tutaj
}
```
## Krok 2: Ustaw opcje podpisywania pieczęci
```csharp
StampSignOptions options = new StampSignOptions()
{
    Left = 50,
    Top = 150,                    
    Width = 200,
    Height = 200
};
```
## Krok 3: Skonfiguruj wygląd stempla
```csharp
StampLine outerLine = new StampLine();
outerLine.Text = " * European Union ";
outerLine.TextRepeatType = StampTextRepeatType.FullTextRepeat;
outerLine.Font.Size = 12;
outerLine.Height = 22;
outerLine.TextBottomIntent = 6;
outerLine.TextColor = Color.WhiteSmoke;
outerLine.BackgroundColor = Color.DarkSlateBlue;
options.OuterLines.Add(outerLine);
StampLine innerLine = new StampLine();
innerLine.Text = "John Smith";
innerLine.TextColor = Color.MediumVioletRed;
innerLine.Font.Size = 20;
innerLine.Font.Bold = true;
innerLine.Height = 40;
options.InnerLines.Add(innerLine);
```
## Krok 4: Podpisz dokument
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithStamp", fileName);
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Wniosek
Dodawanie podpisów pieczęci do dokumentów przy użyciu programu GroupDocs.Signature dla platformy .NET jest prostym procesem, jak pokazano w tym samouczku. Dzięki podanym krokom możesz łatwo zwiększyć bezpieczeństwo i autentyczność swoich dokumentów.
## Często zadawane pytania
### Czy mogę dostosować wygląd podpisu na pieczęci?
Tak, możesz dostosować różne aspekty, takie jak tekst, czcionka, kolor i położenie podpisu pieczęci, zgodnie z własnymi wymaganiami.
### Czy GroupDocs.Signature obsługuje podpisywanie wielu formatów dokumentów?
Tak, GroupDocs.Signature obsługuje szeroką gamę formatów dokumentów, w tym PDF, Microsoft Word, Excel, PowerPoint i inne.
### Czy dostępna jest wersja próbna programu GroupDocs.Signature?
 Tak, możesz uzyskać dostęp do bezpłatnej wersji próbnej z[strona internetowa](https://releases.groupdocs.com/).
### Czy mogę dodać wiele podpisów do jednego dokumentu?
Absolutnie GroupDocs.Signature umożliwia dodawanie wielu podpisów, w tym pieczątek, tekstu, obrazów i podpisów cyfrowych, do jednego dokumentu.
### Gdzie mogę znaleźć wsparcie, jeśli napotkam jakiekolwiek problemy podczas wdrożenia?
 Wsparcie i pomoc można znaleźć na forum społeczności GroupDocs.Signature[Tutaj](https://forum.groupdocs.com/c/signature/13).