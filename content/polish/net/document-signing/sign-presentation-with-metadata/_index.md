---
title: Podpisz prezentację metadanymi
linktitle: Podpisz prezentację metadanymi
second_title: GroupDocs.Signature .NET API
description: Dowiedz się, jak podpisywać pliki prezentacji metadanymi przy użyciu programu GroupDocs.Signature for .NET. Zwiększ integralność dokumentów i dodaj cenne informacje.
weight: 12
url: /pl/net/document-signing/sign-presentation-with-metadata/
---

# Podpisz prezentację metadanymi

## Wstęp
tym samouczku dowiemy się, jak podpisać plik prezentacji (PPTX) metadanymi przy użyciu biblioteki GroupDocs.Signature for .NET. Podpisywanie prezentacji metadanymi dodaje do dokumentu cenne informacje, takie jak imię i nazwisko autora, data utworzenia, identyfikator dokumentu, identyfikator podpisu i różne wartości liczbowe.
## Warunki wstępne
Zanim zaczniemy, upewnij się, że masz następujące elementy:
1.  Biblioteka GroupDocs.Signature dla platformy .NET: Pobierz i zainstaluj bibliotekę z witryny[Tutaj](https://releases.groupdocs.com/signature/net/).
2. Środowisko programistyczne: Upewnij się, że masz skonfigurowane środowisko programistyczne .NET.
3. Plik prezentacji: Przygotuj przykładowy plik prezentacji (w formacie PPTX) do podpisania.
4. Podstawowa znajomość języka C#: Znajomość języka programowania C# będzie korzystna.

## Importuj przestrzenie nazw
Zanim zagłębimy się w kod, zaimportujmy niezbędne przestrzenie nazw:
```csharp
using System;
using System.IO;
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;
    using GroupDocs.Signature.Options;
```
## Krok 1: Załaduj plik prezentacji
```csharp
string filePath = "sample.pptx";
```
 Zastępować`"sample.pptx"` ze ścieżką do pliku prezentacji.
## Krok 2: Określ ścieżkę pliku wyjściowego
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPresentationWithMetadata", "SignedWithMetadata.pptx");
```
Określ katalog, w którym chcesz zapisać podpisany plik prezentacji, wraz z nazwą pliku.
## Krok 3: Zainicjuj obiekt podpisu
```csharp
using (Signature signature = new Signature(filePath))
```
Zainicjuj obiekt Signature, podając ścieżkę do pliku prezentacji.
## Krok 4: Zdefiniuj opcje podpisywania metadanych
```csharp
MetadataSignOptions options = new MetadataSignOptions();
```
Utwórz instancję MetadataSignOptions, aby zdefiniować opcje podpisywania metadanych.
## Krok 5: Utwórz podpisy metadanych
```csharp
PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Author", "Mr.Scherlock Holmes"),
    new PresentationMetadataSignature("CreatedOn", DateTime.Now),
    new PresentationMetadataSignature("DocumentId", 123456),
    new PresentationMetadataSignature("SignatureId", 123.456D),
    new PresentationMetadataSignature("Amount", 123.456M),
    new PresentationMetadataSignature("Total", 123.456F)
};
```
Utwórz tablicę obiektów PrezentacjaMetadataSignature, z których każdy reprezentuje podpis metadanych. Możesz dodać różne typy metadanych, w tym ciąg, datę i godzinę, liczbę całkowitą, liczbę podwójną, dziesiętną i zmiennoprzecinkową.
## Krok 6: Dodaj podpisy do opcji
```csharp
options.Signatures.AddRange(signatures);
```
Dodaj utworzone podpisy metadanych do obiektu MetadataSignOptions.
## Krok 7: Podpisz dokument
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
Podpisz plik prezentacji metadanymi, korzystając z określonych opcji i zapisz podpisany plik w ścieżce wyjściowej.
## Krok 8: Wyświetl wynik
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
Wyświetl komunikat o powodzeniu wraz z liczbą zastosowanych podpisów i ścieżką, w której zapisano podpisany plik.

## Wniosek
W tym samouczku nauczyliśmy się, jak podpisywać plik prezentacji metadanymi przy użyciu biblioteki GroupDocs.Signature for .NET. Dodanie podpisów metadanych zwiększa integralność dokumentu i dostarcza cennych informacji o jego zawartości.

## Często zadawane pytania
### Czy mogę podpisywać metadane w innych formatach dokumentów niż PPTX za pomocą GroupDocs.Signature for .NET?
Tak, GroupDocs.Signature obsługuje różne formaty dokumentów, w tym Word, Excel, PDF i inne, do podpisywania za pomocą metadanych.
### Czy GroupDocs.Signature for .NET jest zgodny z .NET Core?
Tak, biblioteka jest kompatybilna zarówno z .NET Framework, jak i .NET Core.
### Czy mogę dostosować wygląd podpisów metadanych?
Tak, możesz dostosować wygląd, położenie i inne właściwości podpisów metadanych zgodnie ze swoimi wymaganiami.
### Czy GroupDocs.Signature for .NET zapewnia szyfrowanie podpisanych dokumentów?
Tak, GroupDocs.Signature oferuje opcje szyfrowania w celu zabezpieczenia podpisanych dokumentów przed nieautoryzowanym dostępem.
### Czy dostępna jest wersja próbna do przetestowania przed zakupem?
 Tak, możesz skorzystać z bezpłatnej wersji próbnej GroupDocs.Signature for .NET w witrynie[Tutaj](https://releases.groupdocs.com/).