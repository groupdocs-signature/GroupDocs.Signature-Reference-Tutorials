---
title: Zweryfikuj kod QR
linktitle: Zweryfikuj kod QR
second_title: GroupDocs.Signature .NET API
description: Dowiedz się, jak weryfikować kody QR w dokumentach za pomocą GroupDocs.Signature dla .NET. Obszerny samouczek z przewodnikiem krok po kroku.
weight: 12
url: /pl/net/verify-operations/verify-qr-code/
---

# Zweryfikuj kod QR

## Wstęp
dziedzinie zarządzania dokumentami i uwierzytelniania zapewnienie integralności i ważności podpisów jest sprawą najwyższej wagi. GroupDocs.Signature for .NET zapewnia kompleksowe rozwiązanie do weryfikacji kodów QR osadzonych w dokumentach. W tym samouczku szczegółowo omówimy proces weryfikacji kodów QR za pomocą programu GroupDocs.Signature for .NET.
## Warunki wstępne
Zanim przystąpisz do procesu weryfikacji, upewnij się, że spełnione są następujące wymagania wstępne:
1.  Instalacja GroupDocs.Signature dla .NET: Pobierz i zainstaluj GroupDocs.Signature dla .NET z[link do pobrania](https://releases.groupdocs.com/signature/net/).
2. Dostęp do dokumentu zawierającego kody QR: Przygotuj przykładowy dokument zawierający kody QR do weryfikacji. 

## Importuj przestrzenie nazw
W pierwszej kolejności należy zaimportować niezbędne przestrzenie nazw, aby móc korzystać z funkcjonalności udostępnianych przez GroupDocs.Signature for .NET. Wykonaj następujące kroki:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```


Rozłóżmy teraz proces weryfikacji kodów QR osadzonych w dokumencie za pomocą GroupDocs.Signature for .NET:
## Krok 1: Określ ścieżkę dokumentu
```csharp
string filePath = "sample_multiple_signatures.docx";
```
 Pamiętaj o wymianie`"sample_multiple_signatures.docx"` ze ścieżką do dokumentu.
## Krok 2: Zainicjuj obiekt podpisu
```csharp
using (Signature signature = new Signature(filePath))
{
    //Tutaj znajduje się kod weryfikacyjny
}
```
 Zainicjuj a`Signature` obiekt, podając ścieżkę do dokumentu.
## Krok 3: Określ opcje weryfikacji
```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // ta wartość jest ustawiona domyślnie
    Text = "John",
    MatchType = TextMatchType.Contains
};
```
 Zdefiniuj opcje weryfikacji, takie jak`AllPages` aby zweryfikować wszystkie strony,`Text` określić tekst, który ma być dopasowany w kodzie QR, oraz`MatchType` w celu zdefiniowania kryteriów dopasowania.
## Krok 4: Sprawdź podpisy dokumentów
```csharp
VerificationResult result = signature.Verify(options);
```
 Wywołaj`Verify` metoda`Signature` obiekt, przekazując opcje weryfikacji.
## Krok 5: Obsługa wyników weryfikacji
```csharp
if (result.IsValid)
{
    // Znaleziono prawidłowy podpis
}
else
{
    // Znaleziono nieprawidłowy podpis
}
```
W oparciu o wynik weryfikacji odpowiednio obsłuż scenariusze sukcesu lub niepowodzenia.

## Wniosek
W tym samouczku omówiliśmy proces weryfikowania kodów QR w dokumentach przy użyciu programu GroupDocs.Signature dla platformy .NET. Wykonując poniższe kroki, możesz bezproblemowo zintegrować funkcję weryfikacji kodów QR z aplikacjami .NET, zapewniając integralność i autentyczność dokumentów.
## Często zadawane pytania
### Czy GroupDocs.Signature for .NET może weryfikować kody QR w różnych formatach dokumentów?
Tak, GroupDocs.Signature for .NET obsługuje szeroką gamę formatów dokumentów, w tym DOCX, PDF i inne, w celu weryfikacji za pomocą kodu QR.
### Czy dostępna jest bezpłatna wersja próbna programu GroupDocs.Signature for .NET?
 Tak, możesz skorzystać z bezpłatnego okresu próbnego w witrynie[strona z wydaniami](https://releases.groupdocs.com/).
### Jakie opcje pomocy są dostępne dla użytkowników GroupDocs.Signature for .NET?
 Użytkownicy mogą uzyskać dostęp do pomocy za pośrednictwem[forum](https://forum.groupdocs.com/c/signature/13) dla GroupDocs.Signature.
### Czy mogę kupić tymczasową licencję na GroupDocs.Signature dla .NET?
 Tak, licencje tymczasowe można kupić w witrynie[Strona zakupu GroupDocs](https://purchase.groupdocs.com/temporary-license/).
### Czy dostępna jest obszerna dokumentacja programu GroupDocs.Signature for .NET?
 Oczywiście możesz zapoznać się z dostarczoną szczegółową dokumentacją[Tutaj](https://tutorials.groupdocs.com/signature/net/) aby uzyskać kompleksowe wskazówki dotyczące korzystania z funkcjonalności GroupDocs.Signature dla .NET.