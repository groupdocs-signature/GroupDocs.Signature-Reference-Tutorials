---
title: Pobierz informacje o dokumencie
linktitle: Pobierz informacje o dokumencie
second_title: GroupDocs.Signature .NET API
description: Usprawnij zarządzanie dokumentami w .NET dzięki GroupDocs.Signature. Pobieraj informacje o dokumencie krok po kroku. Obsługuje różne formaty.
type: docs
weight: 11
url: /pl/net/document-preview-operations/retrieve-document-information/
---
## Wstęp
W dziedzinie dokumentacji cyfrowej zapewnienie autentyczności i integralności jest sprawą najwyższej wagi. GroupDocs.Signature for .NET zapewnia solidne rozwiązanie do zarządzania podpisami dokumentów w środowisku .NET. W tym samouczku zagłębiamy się w proces odzyskiwania informacji o dokumencie przy użyciu GroupDocs.Signature dla .NET, dzieląc każdy krok w celu zapewnienia pełnego zrozumienia.
## Warunki wstępne
Zanim przejdziesz do samouczka, upewnij się, że spełniasz następujące wymagania wstępne:
1.  Instalacja: Zainstaluj GroupDocs.Signature for .NET, pobierając go ze strony[Tutaj](https://releases.groupdocs.com/signature/net/).
2. Środowisko .NET: Posiadaj praktyczną wiedzę na temat platformy .NET.
3. Dokument: Przygotuj przykładowy dokument (np. „sample_multiple_signatures.docx”) do celów testowych.

## Importowanie przestrzeni nazw
Przed przystąpieniem do procesu odzyskiwania podpisu dokumentu zaimportuj niezbędne przestrzenie nazw:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```

## Krok 1: Ustaw ścieżkę pliku dokumentu:
Zdefiniuj ścieżkę pliku dokumentu, z którego chcesz pobrać informacje.
```csharp
string filePath = "sample_multiple_signatures.docx";
```
## Krok 2: Utwórz instancję obiektu podpisu:
 Utwórz instancję`Signature` class, przekazując ścieżkę pliku dokumentu.
```csharp
using (Signature signature = new Signature(filePath))
{

}
```
## Krok 3: Pobierz informacje o dokumencie:
 Skorzystaj z`GetDocumentInfo()` metoda pobierania kompleksowych informacji o dokumencie.
```csharp
IDocumentInfo documentInfo = signature.GetDocumentInfo();
```
## Krok 4: Wyświetl właściwości dokumentu:
Wyprowadź różne właściwości dokumentu, takie jak format, rozszerzenie, rozmiar, liczba stron itp.
```csharp
Console.WriteLine($"Document properties {Path.GetFileName(filePath)}:");
Console.WriteLine($" - format : {documentInfo.FileType.FileFormat}");
Console.WriteLine($" - extension : {documentInfo.FileType.Extension}");
Console.WriteLine($" - size : {documentInfo.Size}");
Console.WriteLine($" - page count : {documentInfo.PageCount}");
Console.WriteLine($" - Form Fields count : {documentInfo.FormFields.Count}");
Console.WriteLine($" - Text signatures count : {documentInfo.TextSignatures.Count}");
Console.WriteLine($" - Image signatures count : {documentInfo.ImageSignatures.Count}");
Console.WriteLine($" - Digital signatures count : {documentInfo.DigitalSignatures.Count}");
Console.WriteLine($" - Barcode signatures count : {documentInfo.BarcodeSignatures.Count}");
Console.WriteLine($" - QrCode signatures count : {documentInfo.QrCodeSignatures.Count}");
Console.WriteLine($" - FormField signatures count : {documentInfo.FormFieldSignatures.Count}");
foreach (PageInfo pageInfo in documentInfo.Pages)
{
   Console.WriteLine($" - page-{pageInfo.PageNumber} Width {pageInfo.Width}, Height {pageInfo.Height}");
}
```


## Wniosek
GroupDocs.Signature for .NET oferuje potężny zestaw narzędzi do płynnego zarządzania podpisami dokumentów w środowisku .NET. Wykonując kroki opisane w tym przewodniku, możesz skutecznie uzyskać kompleksowe informacje o swoich dokumentach, ułatwiając ulepszone możliwości zarządzania dokumentami.

## Często zadawane pytania
### Czy GroupDocs.Signature for .NET obsługuje wiele formatów dokumentów?
Tak, GroupDocs.Signature obsługuje szeroką gamę formatów dokumentów, w tym między innymi DOCX, PDF, PNG i JPEG.
### Czy dostępna jest wersja próbna programu GroupDocs.Signature for .NET?
 Tak, możesz uzyskać dostęp do wersji próbnej z[Tutaj](https://releases.groupdocs.com/).
### Czy GroupDocs.Signature for .NET zapewnia obsługę podpisów cyfrowych?
Absolutnie GroupDocs.Signature oferuje solidną obsługę podpisów cyfrowych, zapewniając autentyczność i integralność dokumentów.
### Gdzie mogę znaleźć dodatkową dokumentację i wsparcie dla GroupDocs.Signature dla .NET?
 Możesz zapoznać się z obszerną dokumentacją[Tutaj](https://reference.groupdocs.com/signature/net/) i aby uzyskać pomoc, odwiedź forum GroupDocs[Tutaj](https://forum.groupdocs.com/c/signature/13).
### Czy można uzyskać licencje tymczasowe dla GroupDocs.Signature for .NET?
 Tak, można kupić licencje tymczasowe[Tutaj](https://purchase.groupdocs.com/temporary-license/).