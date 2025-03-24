---
title: Usuń podpis kodu QR z dokumentu
linktitle: Usuń podpis kodu QR z dokumentu
second_title: GroupDocs.Signature .NET API
description: Dowiedz się, jak usunąć podpisy kodów QR z dokumentów za pomocą GroupDocs.Signature for .NET. Postępuj zgodnie z naszym przewodnikiem krok po kroku, aby efektywnie zarządzać podpisami.
weight: 16
url: /pl/net/delete-operations/delete-qr-code-signature/
---
## Wstęp
tym samouczku przeprowadzimy Cię przez proces usuwania podpisu w postaci kodu QR z dokumentu za pomocą programu GroupDocs.Signature for .NET. Postępuj zgodnie z tymi instrukcjami krok po kroku, aby skutecznie usunąć podpisy kodów QR.
## Warunki wstępne
Zanim zaczniesz, upewnij się, że masz następujące wymagania wstępne:
-  GroupDocs.Signature dla .NET: Upewnij się, że w projekcie .NET masz zainstalowaną bibliotekę GroupDocs.Signature. Można go pobrać z[Tutaj](https://releases.groupdocs.com/signature/net/).
- Dokument z podpisem w postaci kodu QR: Przygotuj dokument zawierający podpisy w postaci kodu QR, które chcesz usunąć.
- Podstawowa znajomość języka C#: Zapoznaj się z podstawami języka programowania C#.

## Importowanie przestrzeni nazw
Zanim zagłębisz się w kod, zaimportuj niezbędne przestrzenie nazw do pliku C#:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Krok 1: Zdefiniuj ścieżki plików
```csharp
// Ścieżka do katalogu dokumentów.
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
// Zdefiniuj ścieżkę pliku wyjściowego dla zmodyfikowanego dokumentu.
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);
// Skopiuj plik źródłowy, ponieważ metoda Delete działa z tym samym dokumentem.
File.Copy(filePath, outputFilePath, true);
```
## Krok 2: Zainicjuj obiekt podpisu
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Utwórz opcje wyszukiwania podpisów kodów QR.
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    // Wyszukaj podpisy kodem QR w dokumencie.
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```
## Krok 3: Sprawdź, czy istnieje podpis kodu QR
```csharp
    if (signatures.Count > 0)
    {
        // Uzyskaj pierwszy podpis w postaci kodu QR znaleziony w dokumencie.
        QrCodeSignature qrCodeSignature = signatures[0];
```
## Krok 4: Usuń podpis kodu QR
```csharp
        // Usuń podpis w postaci kodu QR z dokumentu.
        bool result = signature.Delete(qrCodeSignature);
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```
Gratulacje! Pomyślnie usunąłeś podpis kodu QR z dokumentu za pomocą GroupDocs.Signature for .NET.

## Wniosek
W tym samouczku dowiedzieliśmy się, jak usunąć podpis w postaci kodu QR z dokumentu za pomocą GroupDocs.Signature for .NET. Wykonując podane kroki, możesz efektywnie zarządzać podpisami i manipulować nimi w aplikacjach .NET.
## Często zadawane pytania
### Czy mogę usunąć wiele podpisów kodów QR z dokumentu?
Tak, możesz zmodyfikować kod, aby przeglądać wszystkie podpisy kodów QR i odpowiednio je usunąć.
### Czy GroupDocs.Signature obsługuje inne typy podpisów oprócz kodów QR?
Tak, GroupDocs.Signature obsługuje różne typy podpisów, takie jak tekst, obraz, kod kreskowy i inne.
### Czy GroupDocs.Signature jest kompatybilny ze wszystkimi formatami dokumentów?
GroupDocs.Signature obsługuje szeroką gamę formatów dokumentów, w tym PDF, Microsoft Word, Excel, PowerPoint i inne.
### Czy mogę dostosować opcje wyszukiwania podpisów?
Tak, możesz dostosować opcje wyszukiwania zgodnie ze swoimi wymaganiami, aby zlokalizować określone podpisy w dokumencie.
### Czy dostępna jest wersja próbna programu GroupDocs.Signature?
 Tak, możesz uzyskać dostęp do bezpłatnej wersji próbnej GroupDocs.Signature z[Tutaj](https://releases.groupdocs.com/).