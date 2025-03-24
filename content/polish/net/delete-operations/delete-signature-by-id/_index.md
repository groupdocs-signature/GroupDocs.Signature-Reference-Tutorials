---
title: Usuń podpis według identyfikatora
linktitle: Usuń podpis według identyfikatora
second_title: GroupDocs.Signature .NET API
description: Dowiedz się, jak usunąć podpis według identyfikatora w dokumentach .NET przy użyciu biblioteki GroupDocs.Signature. Łatwy przewodnik krok po kroku.
weight: 11
url: /pl/net/delete-operations/delete-signature-by-id/
---

# Usuń podpis według identyfikatora

## Wstęp
W tym samouczku dowiemy się, jak usunąć podpis według jego identyfikatora za pomocą GroupDocs.Signature for .NET. GroupDocs.Signature for .NET to potężna biblioteka, która umożliwia programistom dodawanie, usuwanie lub weryfikację podpisów cyfrowych w różnych formatach dokumentów przy użyciu aplikacji .NET.
## Warunki wstępne
Zanim zaczniemy, upewnij się, że masz następujące wymagania wstępne:
1.  Biblioteka GroupDocs.Signature dla platformy .NET: Pobierz i zainstaluj bibliotekę z witryny[Tutaj](https://releases.groupdocs.com/signature/net/).
2. .NET Framework: Upewnij się, że w systemie zainstalowano .NET Framework.
3. Dokument z podpisem: Przygotuj dokument (np. DOCX, PDF) z podpisem, który chcesz usunąć.

## Importuj przestrzenie nazw
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Krok 1: Zdefiniuj ścieżki plików
Najpierw określ ścieżkę pliku dokumentu zawierającego podpis oraz ścieżkę pliku wyjściowego, w którym zostanie zapisany zmodyfikowany dokument.
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteById", fileName);
```
## Krok 2: Skopiuj dokument
 Od`Delete` metoda modyfikuje dokument na miejscu, najlepiej utworzyć kopię oryginalnego dokumentu.
```csharp
File.Copy(filePath, outputFilePath, true);
```
## Krok 3: Usuń podpis według identyfikatora
 Zainicjuj`Signature` obiekt ścieżką pliku dokumentu i użyj metody`Delete` metoda usuwania podpisu po jego identyfikatorze.
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    string id = @"eff64a14-dad9-47b0-88e5-2ee4e3604e71";
    bool result = signature.Delete(id);
    if (result)
    {
        Console.WriteLine($"Signature with Id# '{id}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with id# '{id}' was not found!");
    }
}
```

## Wniosek
W tym samouczku dowiedzieliśmy się, jak usunąć podpis według jego identyfikatora za pomocą GroupDocs.Signature for .NET. Ta biblioteka zapewnia wygodny sposób programowego zarządzania podpisami cyfrowymi w różnych formatach dokumentów.
## Często zadawane pytania
### Czy mogę usunąć wiele podpisów jednocześnie?
 Tak, możesz usunąć wiele podpisów, przeglądając ich identyfikatory i wywołując metodę`Delete` metoda dla każdego identyfikatora.
### Czy GroupDocs.Signature for .NET jest kompatybilny ze wszystkimi formatami dokumentów?
GroupDocs.Signature dla .NET obsługuje szeroką gamę formatów dokumentów, w tym PDF, DOCX, XLSX i inne.
### Czy mogę dostosować wygląd podpisu?
Tak, możesz dostosować wygląd podpisu, w tym jego położenie, rozmiar, czcionkę i kolor.
### Czy dostępna jest wersja próbna?
 Tak, możesz pobrać bezpłatną wersję próbną ze strony[Tutaj](https://releases.groupdocs.com/).
### Gdzie mogę znaleźć pomoc lub wsparcie dotyczące GroupDocs.Signature for .NET?
 Możesz odwiedzić forum pomocy technicznej[Tutaj](https://forum.groupdocs.com/c/signature/13) do pomocy.