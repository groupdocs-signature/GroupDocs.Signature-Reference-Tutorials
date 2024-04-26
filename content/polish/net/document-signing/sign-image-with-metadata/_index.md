---
title: Podpisz obraz metadanymi
linktitle: Podpisz obraz metadanymi
second_title: GroupDocs.Signature .NET API
description: Dowiedz się, jak podpisywać obrazy z metadanymi w platformie .NET przy użyciu GroupDocs.Signature. Łatwe, wydajne i konfigurowalne rozwiązanie do podpisywania metadanych.
type: docs
weight: 10
url: /pl/net/document-signing/sign-image-with-metadata/
---
## Wstęp
GroupDocs.Signature dla .NET umożliwia programistom wydajne podpisywanie obrazów za pomocą metadanych. Ten samouczek przeprowadzi Cię przez proces krok po kroku.
## Warunki wstępne
Zanim zaczniesz, upewnij się, że masz następujące elementy:
1. GroupDocs.Signature dla .NET: Zainstaluj pakiet GroupDocs.Signature w projekcie .NET. Można go pobrać z[Tutaj](https://releases.groupdocs.com/signature/net/).   
2. Plik obrazu: Przygotuj plik obrazu, który chcesz podpisać metadanymi.

## Importuj przestrzenie nazw
Pamiętaj, aby zaimportować niezbędne przestrzenie nazw do kodu C#:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Krok 1: Załaduj plik obrazu
Najpierw określ ścieżkę do pliku obrazu i katalog wyjściowy podpisanego obrazu z metadanymi:
```csharp
string filePath = "sample.png";            
string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
```
## Krok 2: Utwórz podpisy metadanych
Następnie utwórz różne podpisy metadanych i dodaj je do kolekcji podpisów opcji:
```csharp
using (Signature signature = new Signature(filePath))
{
    ushort imgsMetadataId = 41996;
    MetadataSignOptions options = new MetadataSignOptions();
    options
        .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Scherlock Holmes")) // Wartość ciągu
        .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Data Godzina Wartość
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Wartość całkowita
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Podwójna wartość
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Wartość dziesiętna
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Wartość pływająca
    
    // podpisać dokument do pliku
    SignResult result = signature.Sign(outputFilePath, options);
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Wniosek
W tym samouczku nauczyłeś się podpisywać obraz metadanymi przy użyciu programu GroupDocs.Signature for .NET. Wykonując poniższe kroki, można łatwo włączyć podpisy metadanych do aplikacji .NET.

## Często zadawane pytania
### Czy mogę podpisywać wiele obrazów metadanymi przy użyciu GroupDocs.Signature for .NET?
Tak, możesz podpisać wiele obrazów metadanymi, przeglądając każdy plik obrazu i stosując podpisy metadanych.
### Czy dostępna jest wersja próbna programu GroupDocs.Signature for .NET?
 Tak, możesz pobrać wersję próbną ze strony[Tutaj](https://releases.groupdocs.com/).
### Czy GroupDocs.Signature for .NET obsługuje inne formaty plików oprócz obrazów?
Tak, GroupDocs.Signature obsługuje różne formaty plików, w tym PDF, Word, Excel i inne.
### Czy mogę dostosować wygląd podpisu metadanych?
Tak, możesz dostosować wygląd podpisu metadanych, np. rozmiar czcionki, kolor i położenie.
### Gdzie mogę uzyskać pomoc dotyczącą GroupDocs.Signature dla .NET?
 Pomoc można uzyskać na forum GroupDocs.Signature[Tutaj](https://forum.groupdocs.com/c/signature/13).