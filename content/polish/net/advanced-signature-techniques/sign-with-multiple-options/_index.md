---
title: Podpisywanie z wieloma opcjami
linktitle: Podpisywanie z wieloma opcjami
second_title: GroupDocs.Signature .NET API
description: Dowiedz się, jak podpisywać dokumenty przy użyciu wielu opcji przy użyciu GroupDocs.Signature dla .NET. Zwiększ bezpieczeństwo dokumentów za pomocą tekstu, kodu kreskowego, kodu QR, danych cyfrowych i obrazów.
weight: 14
url: /pl/net/advanced-signature-techniques/sign-with-multiple-options/
---
## Wstęp
tym samouczku omówimy, jak podpisać dokument przy użyciu wielu opcji podpisu przy użyciu biblioteki GroupDocs.Signature dla platformy .NET. Podpisywanie dokumentów za pomocą różnych opcji, takich jak podpisy tekstowe, kody kreskowe, kody QR, podpisy cyfrowe, obrazy i metadane, może zapewnić wszechstronność i zwiększyć bezpieczeństwo dokumentów.
## Warunki wstępne
Przed rozpoczęciem upewnij się, że spełnione są następujące wymagania wstępne:
1.  Biblioteka GroupDocs.Signature for .NET: Pobierz i zainstaluj bibliotekę GroupDocs.Signature for .NET ze strony[Tutaj](https://releases.groupdocs.com/signature/net/).
2. Środowisko programistyczne: skonfiguruj środowisko programistyczne z zainstalowaną platformą .NET Framework.
3. Dokument do podpisania: Przygotuj dokument (np. sample.docx), który chcesz podpisać.
4. Certyfikaty i obrazy: Przygotuj wszelkie wymagane certyfikaty i obrazy do podpisów cyfrowych i obrazowych.

## Importuj przestrzenie nazw
Najpierw zaimportuj niezbędne przestrzenie nazw, aby móc korzystać z biblioteki GroupDocs.Signature w aplikacji .NET:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Krok 1: Załaduj dokument
```csharp
string filePath = "sample.docx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithMultiple", "SignWithMultiple.docx");
using (Signature signature = new Signature(filePath))
{
    // Twój kod jest kontynuowany...
}
```
## Krok 2: Zdefiniuj opcje podpisu
Zdefiniuj kilka opcji podpisów różnych typów i ustawień, takich jak podpisy tekstowe, kod kreskowy, kod QR, podpisy cyfrowe, obrazowe i metadane:
```csharp
TextSignOptions textOptions = new TextSignOptions("Text signature")
{
    VerticalAlignment = VerticalAlignment.Top,
    HorizontalAlignment = HorizontalAlignment.Left
};
BarcodeSignOptions barcodeOptions = new BarcodeSignOptions("123456")
{
    EncodeType = BarcodeTypes.Code128,
    Left = 0,
    Top = 150,
    Height = 50,
    Width = 200
};
// Zdefiniuj inne opcje podpisu (np. kod QR, cyfrowy, obraz, metadane)...
```
## Krok 3: Utwórz listę opcji podpisu
Zdefiniuj listę opcji podpisu zawierającą wszystkie wcześniej zdefiniowane opcje:
```csharp
List<SignOptions> listOptions = new List<SignOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
// Dodaj inne opcje podpisu do listy...
```
## Krok 4: Podpisz dokument
Podpisz dokument listą opcji podpisu i zapisz podpisany dokument:
```csharp
SignResult result = signature.Sign(outputFilePath, listOptions);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Wniosek
Podpisywanie dokumentów z wieloma opcjami przy użyciu GroupDocs.Signature dla .NET zapewnia solidne rozwiązanie zwiększające bezpieczeństwo dokumentów i wszechstronność. Wykonując kroki opisane w tym samouczku, możesz bezproblemowo zintegrować różne typy podpisów z aplikacjami .NET.
## Często zadawane pytania
### Czy mogę używać niestandardowych obrazów do podpisów cyfrowych?
Tak, możesz określić niestandardowe obrazy do podpisów cyfrowych, korzystając z biblioteki GroupDocs.Signature.
### Czy GroupDocs.Signature jest kompatybilny z różnymi formatami dokumentów?
Tak, GroupDocs.Signature obsługuje różne formaty dokumentów, w tym DOCX, PDF, PPTX i inne.
### Czy mogę dostosować wygląd podpisów tekstowych?
Oczywiście możesz dostosować wygląd podpisów tekstowych, w tym rozmiar czcionki, kolor i styl.
### Czy GroupDocs.Signature zapewnia szyfrowanie podpisów cyfrowych?
Tak, GroupDocs.Signature oferuje opcje szyfrowania podpisów cyfrowych, aby zapewnić bezpieczeństwo dokumentów.
### Czy dostępna jest wersja próbna programu GroupDocs.Signature for .NET?
 Tak, możesz pobrać bezpłatną wersję próbną GroupDocs.Signature dla .NET ze strony[Tutaj](https://releases.groupdocs.com/).