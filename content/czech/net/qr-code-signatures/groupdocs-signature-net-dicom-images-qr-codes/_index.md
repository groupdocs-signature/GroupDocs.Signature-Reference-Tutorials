---
"date": "2025-05-07"
"description": "Naučte se, jak podepisovat snímky DICOM pomocí QR kódů pomocí GroupDocs.Signature pro .NET. Tato příručka se zabývá nastavením, implementací a ověřováním podpisů QR kódů v lékařském zobrazování."
"title": "Jak podepisovat obrázky DICOM pomocí QR kódů pomocí GroupDocs.Signature pro .NET – Komplexní průvodce"
"url": "/cs/net/qr-code-signatures/groupdocs-signature-net-dicom-images-qr-codes/"
"weight": 1
type: docs
---
# Jak podepisovat obrázky DICOM pomocí QR kódů pomocí GroupDocs.Signature pro .NET: Komplexní průvodce

Hledáte bezpečnou metodu pro ověřování souborů DICOM? Tato podrobná příručka vám ukáže, jak pomocí nástroje GroupDocs.Signature for .NET integrovat podpisy QR kódů do obrázků DICOM. Tento tutoriál, ideální pro zdravotnické pracovníky, vývojáře a kohokoli, kdo pracuje s digitálními lékařskými dokumenty, zahrnuje celý proces od nastavení až po implementaci.

## Co se naučíte:
- Nastavení vývojového prostředí s GroupDocs.Signature pro .NET.
- Podrobné pokyny k podepisování snímků DICOM pomocí QR kódů.
- Metody ověřování a vyhledávání podpisů QR kódů v souborech DICOM.
- Techniky pro generování náhledů podepsaných dokumentů pro účely kontroly.
- Nejlepší postupy pro optimalizaci výkonu a efektivní správu zdrojů.

Začněme s předpoklady!

## Předpoklady

Chcete-li používat GroupDocs.Signature pro .NET, ujistěte se, že je vaše prostředí připraveno. Zde je to, co budete potřebovat:

### Požadované knihovny a verze
- **GroupDocs.Signature pro .NET**Zajistěte kompatibilitu s vaším .NET frameworkem.

### Požadavky na nastavení prostředí
- Vývojové prostředí pro Windows nebo Linux.
- Nainstalované Visual Studio nebo jiné IDE kompatibilní s .NET.

### Předpoklady znalostí
- Základní znalost programování v C#.
- Znalost systémů souborového I/O v .NET aplikacích.

## Nastavení GroupDocs.Signature pro .NET

Nainstalujte knihovnu GroupDocs.Signature pomocí vámi preferované metody:

**Použití .NET CLI:**
```bash
dotnet add package GroupDocs.Signature
```

**Správce balíčků:**
```powershell
Install-Package GroupDocs.Signature
```

**Uživatelské rozhraní Správce balíčků NuGet:**
- Vyhledejte „GroupDocs.Signature“ a nainstalujte nejnovější verzi.

### Získání licence

Začněte s bezplatnou zkušební verzí a prozkoumejte možnosti. Pro delší používání zvažte pořízení dočasné nebo plné licence od [GroupDocs](https://purchase.groupdocs.com/buy).

Po instalaci inicializujte knihovnu:

```csharp
using GroupDocs.Signature;
// Inicializujte objekt Signature cestou k souboru DICOM.
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample.dicom");
```

## Průvodce implementací

### Podepište obrázek DICOM pomocí QR kódu

#### Přehled
Přidejte podpisy s QR kódem pro zajištění pravosti a sledovatelnosti lékařských dokumentů.

**Krok 1: Inicializace objektu podpisu**

```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY\\sample.dicom";
using (Signature signature = new Signature(filePath))
{
    // Pokračovat v operacích podepisování...
}
```

**Krok 2: Vytvořte možnosti podpisu pomocí QR kódu**

Nakonfigurujte vlastnosti, jako je text, velikost a zarovnání.

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

**Krok 3: Přidání metadat XMP**

Vylepšete dokument o další metadata.

```csharp
DicomSaveOptions dicomSaveOptions = new DicomSaveOptions()
{
    XmpEntries = new List<DicomXmpEntry>() { new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4") }
};
```

**Krok 4: Podepište dokument**

Proveďte podepsání a uložte.

```csharp
SignResult signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY\\SignedDicom", options, dicomSaveOptions);
```

### Získat informace o dokumentu

Načtěte metadata z podepsaných souborů DICOM pro zajištění integrity dat.

**Přehled:**
Přístup k informacím o dokumentech a podpisům metadat XMP pro ověření.

**Krok 1: Získání informací o dokumentu**

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    IDocumentInfo signedDocumentInfo = signature.GetDocumentInfo();
}
```

**Krok 2: Iterace a tisk dat XMP**

Zobrazit podrobnosti metadat.

```csharp
foreach (var item in signedDocumentInfo.MetadataSignatures)
{
    Console.WriteLine(item.ToString());
}
```

### Ověření podpisů DICOM

Ověřte pravost podpisů QR kódů v DICOM obrázcích.

**Přehled:**
Ujistěte se, že podpisy jsou správné a pravé.

**Krok 1: Vytvořte možnosti ověření QR kódu**

Nastavte možnosti odpovídající konkrétnímu textu v QR kódech.

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true,
    Text = "Patient #36363393",
    MatchType = TextMatchType.Contains
};
```

**Krok 2: Ověření podpisů**

Zkontrolujte, zda podpisy splňují kritéria.

```csharp
VerificationResult result = signature.Verify(options);

if (result.IsValid)
{
    Console.WriteLine($"DICOM {filePath} has {result.Succeeded.Count} successfully verified signatures!");
}
```

### Hledání podpisů v DICOM

Vyhledejte podpisy QR kódů v podepsaných snímcích DICOM.

**Přehled:**
Efektivně vyhledávejte všechny podpisy QR kódů pro správu pravosti dokumentů.

**Krok 1: Vyhledejte podpisy QR kódů**

```csharp
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

**Krok 2: Iterace a tisk podrobností podpisu**

Zkontrolujte podrobnosti každého nalezeného podpisu.

```csharp
foreach (var QrCodeSignature in signatures)
{
    Console.WriteLine($"QRCode signature found at page {QrCodeSignature.PageNumber} with type {QrCodeSignature.EncodeType.TypeName} and text {QrCodeSignature.Text}");
}
```

### Generovat náhled podepsaného DICOM

Vytvořte vizuální náhledy pro ověření.

**Přehled:**
Generujte náhledy obrázků pro ověření obsahu bez specializovaného softwaru.

**Krok 1: Definování metod streamu**

Nastavení metod pro správu streamu souborů během generování náhledu.

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

**Krok 2: Generování náhledů**

Spusťte proces generování náhledu.

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

## Praktické aplikace

1. **Správa lékařských záznamů**Ověřování záznamů pacientů pomocí podpisů QR kódů pro zajištění souladu s předpisy.
2. **Auditní záznamy ve zdravotnických systémech**Sledujte změny dokumentů a ověřujte jejich pravost pomocí QR kódů.
3. **Bezpečné sdílení dat**Zajistěte bezpečné sdílení lékařských snímků vložením digitálních podpisů.
4. **Ověření shody**Pravidelně ověřujte integritu souborů DICOM, abyste splnili zákonné požadavky.
5. **Integrace se systémy EHR**Bezproblémová integrace podepsaných souborů DICOM do systémů elektronických zdravotních záznamů (EHR) pro efektivnější provoz.