---
"date": "2025-05-07"
"description": "Dowiedz się, jak podpisywać obrazy DICOM kodami QR za pomocą GroupDocs.Signature dla platformy .NET. Ten przewodnik obejmuje konfigurację, implementację i weryfikację podpisów kodami QR w obrazowaniu medycznym."
"title": "Jak podpisywać obrazy DICOM kodami QR za pomocą GroupDocs.Signature dla platformy .NET? Kompleksowy przewodnik"
"url": "/pl/net/qr-code-signatures/groupdocs-signature-net-dicom-images-qr-codes/"
"weight": 1
type: docs
---
# Jak podpisywać obrazy DICOM kodami QR za pomocą GroupDocs.Signature dla platformy .NET: kompleksowy przewodnik

Szukasz bezpiecznej metody uwierzytelniania plików DICOM? Ten szczegółowy przewodnik pokaże Ci, jak używać GroupDocs.Signature dla platformy .NET do integracji podpisów kodów QR z obrazami DICOM. Ten samouczek, idealny dla pracowników służby zdrowia, programistów i wszystkich osób pracujących z cyfrową dokumentacją medyczną, obejmuje cały proces konfiguracji i wdrożenia.

## Czego się nauczysz:
- Konfigurowanie środowiska programistycznego przy użyciu GroupDocs.Signature dla .NET.
- Instrukcja krok po kroku dotycząca podpisywania obrazów DICOM za pomocą kodów QR.
- Metody weryfikacji i wyszukiwania podpisów kodów QR w plikach DICOM.
- Techniki generowania podglądów podpisanych dokumentów w celu ich przeglądu.
- Najlepsze praktyki optymalizacji wydajności i efektywnego zarządzania zasobami.

Zacznijmy od warunków wstępnych!

## Wymagania wstępne

Aby użyć GroupDocs.Signature dla .NET, upewnij się, że Twoje środowisko jest gotowe. Oto, czego będziesz potrzebować:

### Wymagane biblioteki i wersje
- **GroupDocs.Signature dla .NET**:Zapewnij zgodność z platformą .NET Framework.

### Wymagania dotyczące konfiguracji środowiska
- Środowisko programistyczne w systemie Windows lub Linux.
- Zainstalowany program Visual Studio lub inne środowisko IDE zgodne z platformą .NET.

### Wymagania wstępne dotyczące wiedzy
- Podstawowa znajomość programowania w języku C#.
- Znajomość operacji wejścia/wyjścia plików w aplikacjach .NET.

## Konfigurowanie GroupDocs.Signature dla platformy .NET

Zainstaluj bibliotekę GroupDocs.Signature, korzystając z preferowanej metody:

**Korzystanie z interfejsu wiersza poleceń .NET:**
```bash
dotnet add package GroupDocs.Signature
```

**Menedżer pakietów:**
```powershell
Install-Package GroupDocs.Signature
```

**Interfejs użytkownika Menedżera pakietów NuGet:**
- Wyszukaj „GroupDocs.Signature” i zainstaluj najnowszą wersję.

### Nabycie licencji

Zacznij od bezpłatnego okresu próbnego, aby poznać możliwości. W przypadku dłuższego użytkowania rozważ nabycie licencji tymczasowej lub pełnej od [Dokumenty grupy](https://purchase.groupdocs.com/buy).

Po zainstalowaniu zainicjuj bibliotekę:

```csharp
using GroupDocs.Signature;
// Zainicjuj obiekt Signature przy użyciu ścieżki pliku DICOM.
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample.dicom");
```

## Przewodnik wdrażania

### Podpisz obraz DICOM kodem QR

#### Przegląd
Dodaj podpisy w postaci kodu QR, aby zagwarantować autentyczność i możliwość śledzenia dokumentów medycznych.

**Krok 1: Zainicjuj obiekt podpisu**

```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY\\sample.dicom";
using (Signature signature = new Signature(filePath))
{
    // Kontynuuj operacje podpisywania...
}
```

**Krok 2: Utwórz opcje podpisu kodem QR**

Skonfiguruj właściwości, takie jak tekst, rozmiar i wyrównanie.

```csharp
QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues")
{
    AllPages = true,
    Width = 100,
    Height = 100,
    VerticalAlignment = VerticalAlignment.Bottom,
    HorizontalAlignment = HorizontalAlignment.Right,
    Margin = new Padding() { Right = 5, Left = 5 }
};
```

**Krok 3: Dodaj metadane XMP**

Ulepsz dokument, dodając dodatkowe metadane.

```csharp
DicomSaveOptions dicomSaveOptions = new DicomSaveOptions()
{
    XmpEntries = new List<DicomXmpEntry>() { new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4") }
};
```

**Krok 4: Podpisz dokument**

Wykonaj podpisywanie i zapisz.

```csharp
SignResult signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY\\SignedDicom", options, dicomSaveOptions);
```

### Uzyskaj informacje o dokumencie

Pobieranie metadanych z podpisanych plików DICOM w celu zapewnienia integralności danych.

**Przegląd:**
Uzyskaj dostęp do informacji o dokumencie i podpisów metadanych XMP w celu weryfikacji.

**Krok 1: Pobierz informacje o dokumencie**

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    IDocumentInfo signedDocumentInfo = signature.GetDocumentInfo();
}
```

**Krok 2: Iteracja i drukowanie danych XMP**

Wyświetl szczegóły metadanych.

```csharp
foreach (var item in signedDocumentInfo.MetadataSignatures)
{
    Console.WriteLine(item.ToString());
}
```

### Zweryfikuj podpisy DICOM

Sprawdź autentyczność podpisów w postaci kodów QR na obrazach DICOM.

**Przegląd:**
Upewnij się, że podpisy są poprawne i autentyczne.

**Krok 1: Utwórz opcje weryfikacji kodu QR**

Ustaw opcje odpowiadające konkretnemu tekstowi w kodach QR.

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true,
    Text = "Patient #36363393",
    MatchType = TextMatchType.Contains
};
```

**Krok 2: Zweryfikuj podpisy**

Sprawdź czy podpisy spełniają kryteria.

```csharp
VerificationResult result = signature.Verify(options);

if (result.IsValid)
{
    Console.WriteLine($"DICOM {filePath} has {result.Succeeded.Count} successfully verified signatures!");
}
```

### Wyszukaj podpisy w DICOM

Znajdź podpisy w postaci kodu QR na podpisanych obrazach DICOM.

**Przegląd:**
Skuteczne wyszukiwanie wszystkich podpisów za pomocą kodów QR w celu zapewnienia autentyczności dokumentów.

**Krok 1: Wyszukaj podpisy w postaci kodu QR**

```csharp
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

**Krok 2: Powtórz i wydrukuj szczegóły podpisu**

Przejrzyj szczegóły każdego znalezionego podpisu.

```csharp
foreach (var QrCodeSignature in signatures)
{
    Console.WriteLine($"QRCode signature found at page {QrCodeSignature.PageNumber} with type {QrCodeSignature.EncodeType.TypeName} and text {QrCodeSignature.Text}");
}
```

### Wygeneruj podgląd podpisanego pliku DICOM

Utwórz podgląd wizualny w celu weryfikacji.

**Przegląd:**
Generuj podglądy obrazów w celu weryfikacji treści bez użycia specjalistycznego oprogramowania.

**Krok 1: Zdefiniuj metody strumieniowe**

Skonfiguruj metody zarządzania strumieniem plików podczas generowania podglądu.

```csharp
Stream CreatePageStream(PreviewPageData pageData)
{
    string imageFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignDicomImageAdvanced", $"preview-{pageData.PageNumber}.jpg");
    var folder = Path.GetDirectoryName(imageFilePath);
    if (!Directory.Exists(folder))
    {
        Directory.CreateDirectory(folder);
    }
    return new FileStream(imageFilePath, FileMode.Create);
}

void ReleasePageStream(PreviewPageData pageData, Stream pageStream)
{
    pageStream.Dispose();
}
```

**Krok 2: Generowanie podglądów**

Wykonaj proces generowania podglądu.

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    PreviewOptions previewOption = new PreviewOptions(CreatePageStream, ReleasePageStream)
    {
        PreviewFormat = PreviewOptions.PreviewFormats.PNG,
    };

    signature.GeneratePreview(previewOption);
}
```

## Zastosowania praktyczne

1. **Zarządzanie dokumentacją medyczną**:Uwierzytelnianie dokumentacji medycznej przy użyciu podpisów kodów QR w celu zapewnienia zgodności.
2. **Ślady audytu w systemach opieki zdrowotnej**: Śledź zmiany w dokumentach i sprawdzaj ich autentyczność za pomocą kodów QR.
3. **Bezpieczne udostępnianie danych**:Zapewnij bezpieczne udostępnianie obrazów medycznych poprzez osadzanie podpisów cyfrowych.
4. **Weryfikacja zgodności**:Regularnie weryfikuj integralność pliku DICOM, aby spełnić wymogi prawne.
5. **Integracja z systemami EHR**:Bezproblemowa integracja podpisanych plików DICOM z systemami Elektronicznej Dokumentacji Medycznej (EHR) w celu usprawnienia działania.