---
"date": "2025-05-07"
"description": "Naučte se, jak podepisovat dokumenty PDF pomocí QR kódů HIBC pomocí GroupDocs.Signature pro .NET. Tato příručka se zabývá kódy LIC a PAS, včetně QR kódů, Aztec kódů a DataMatrix."
"title": "Jak podepisovat dokumenty pomocí QR kódů HIBC pomocí GroupDocs.Signature pro .NET – Komplexní průvodce"
"url": "/cs/net/qr-code-signatures/sign-documents-hibc-qr-groupdocs-dotnet/"
"weight": 1
---

# Jak podepisovat dokumenty pomocí QR kódů HIBC pomocí GroupDocs.Signature pro .NET

## Zavedení

V dnešním rychle se měnícím obchodním prostředí je zajištění pravosti a integrity dokumentů prvořadé. Ať už manipulujete s léčivy, zdravotnickými produkty nebo logistikou, bezpečná metoda podepisování a sledování dokumentů vám může ušetřit čas a předejít chybám. Zadejte **GroupDocs.Signature pro .NET**, výkonná knihovna navržená pro zefektivnění procesů správy dokumentů tím, že umožňuje bezproblémovou integraci QR kódů HIBC do vašich dokumentů.

V tomto tutoriálu se podíváme na to, jak můžete využít GroupDocs.Signature for .NET k podepisování PDF dokumentů pomocí různých typů QR kódů HIBC – LIC (License) a PAS (Product Authentication System) – včetně QR kódů, Aztec kódů a DataMatrix. Na konci budete mít důkladné znalosti o implementaci těchto řešení ve vašich .NET aplikacích.

**Co se naučíte:**
- Jak nastavit GroupDocs.Signature pro .NET
- Implementace QR kódů HIBC LIC, Aztec kódů a DataMatrix
- Přidávání QR kódů HIBC PAS, Aztec kódů a DataMatrix
- Praktické případy použití a možnosti integrace

Než začneme s implementací těchto funkcí, pojďme se ponořit do předpokladů.

## Předpoklady

Než začneme s kódováním, ujistěte se, že máte připraveno následující:

- **Prostředí .NET**Ujistěte se, že máte v systému nainstalované rozhraní .NET (nejlépe .NET Core nebo .NET 5/6+).
- **GroupDocs.Signature pro .NET**Tato knihovna bude naším primárním nástrojem. Můžete si ji nainstalovat pomocí NuGetu.
- **Základní znalosti programování**Doporučuje se znalost jazyka C# a práce se soubory v .NET.

### Požadované knihovny

Chcete-li použít GroupDocs.Signature pro .NET, je třeba přidat balíček pomocí jedné z těchto metod:

**Rozhraní příkazového řádku .NET**
```bash
dotnet add package GroupDocs.Signature
```

**Správce balíčků**
```powershell
Install-Package GroupDocs.Signature
```

**Uživatelské rozhraní Správce balíčků NuGet**
Vyhledejte „GroupDocs.Signature“ a nainstalujte nejnovější verzi.

### Získání licence

Pro testovací účely si můžete pořídit bezplatnou zkušební licenci. Pro delší používání zvažte zakoupení předplatného nebo požádání o dočasnou licenci:

- **Bezplatná zkušební verze**Přístup [zde](https://releases.groupdocs.com/signature/net/)
- **Dočasná licence**Žádost na [tento odkaz](https://purchase.groupdocs.com/temporary-license/)

### Nastavení prostředí

Nastavte si prostředí tak, že se ujistíte, že váš projekt cílí na správnou verzi .NET a má přístup k souboru GroupDocs.Signature. Inicializujte jej ve své aplikaci, jak je znázorněno:

```csharp
using GroupDocs.Signature;
```

## Nastavení GroupDocs.Signature pro .NET

Abyste mohli začít používat GroupDocs.Signature pro .NET, je třeba nainstalovat knihovnu a nakonfigurovat základní nastavení v rámci projektu.

### Instalace

Pro přidání souboru GroupDocs.Signature do projektu použijte jednu z výše uvedených metod. Po instalaci se ujistěte, že je váš projekt nakonfigurován pro jeho použití, a to tak, že se na něj odkážete v souborech kódu.

### Inicializace licence

Po získání licence ji inicializujte takto:

```csharp
SignatureConfig signConfig = new SignatureConfig();
signConfig.LicensePath = "path/to/your/license.lic";
Signature signature = new Signature("Sample.pdf", signConfig);
```

Toto nastavení vám umožní přístup ke všem funkcím GroupDocs.Signature bez omezení.

## Průvodce implementací

Nyní se ponoříme do implementace jednotlivých funkcí pomocí QR kódů HIBC s GroupDocs.Signature pro .NET.

### Podepište dokument pomocí QR kódu HIBC LIC

#### Přehled

Podepsání dokumentu pomocí QR kódu HIBC LIC zajišťuje shodu s předpisy a sledovatelnost v licenčních situacích. Tato část vás provede vytvořením a vložením QR kódu do vašich PDF dokumentů.

#### Kroky implementace

##### Krok 1: Konfigurace zdrojové a výstupní cesty

Definujte, kde se nachází zdrojový dokument a kam se má uložit podepsaný výstup:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICQR.pdf");
```

##### Krok 2: Vytvořte možnosti podpisu pomocí QR kódu

Nakonfigurujte si QR kód s konkrétním textem a nastavením:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_QR_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR)
    {
        Left = 1,
        Top = 1,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    // Podepište dokument s těmito možnostmi.
    signature.Sign(destinFilePath, hibcLic_QR_Options);
}
```

**Vysvětlení**: 
- `QrCodeSignOptions` nastavuje vzhled a obsah QR kódu. Zde určíme typ QR kódu HIBC LIC a umístíme jej v dokumentu.
- `ReturnContent` Nastavení na hodnotu true umožňuje načíst vykreslený obraz podepsaného dokumentu.

#### Tipy pro řešení problémů

- Ujistěte se, že je cesta k dokumentu správně zadána.
- Ověřte, zda je GroupDocs.Signature řádně licencován pro plnou funkčnost.

### Podepsat dokument s kódem HIBC LIC Aztec

#### Přehled

Aztécký kód nabízí další formu kódování, vhodnou pro ukládání informací s vysokou hustotou. Tato část se zaměřuje na vkládání aztéckého kódu do vašich dokumentů pomocí GroupDocs.Signature.

#### Kroky implementace

##### Krok 1: Konfigurace cest

Podobně jako u předchozí funkce definujte cesty k souborům:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICAztec");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICAztec.pdf");
```

##### Krok 2: Konfigurace možností kódu Aztec

Nastavte si aztécký kód pomocí GroupDocs.Signature:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_AZ_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec)
    {
        Left = 1,
        Top = 200,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    signature.Sign(destinFilePath, hibcLic_AZ_Options);
}
```

**Vysvětlení**: 
- Ten/Ta/To `QrCodeSignOptions` se zde používá znovu, ale s typem kódu Aztec.
- Polohování (`Top`, `Left`) a nastavení načítání obsahu jsou podobná jako u QR kódů.

#### Tipy pro řešení problémů

- Ověřte, zda jsou cesty k souborům správné.
- Ujistěte se, že verze GroupDocs.Signature podporuje typy Aztec Code.

### Podepsat dokument s HIBC LIC DataMatrix

#### Přehled

Kód DataMatrix poskytuje další robustní metodu pro ukládání dat. Tato část ukazuje, jak integrovat DataMatrix do vašich PDF dokumentů.

#### Kroky implementace

##### Krok 1: Nastavení cest k souborům

Stejně jako dříve zjistěte, kde se vaše soubory nacházejí:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICDataMatrix");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICDataMatrix.pdf");
```

##### Krok 2: Vytvoření možností podpisu DataMatrix

Nakonfigurujte a aplikujte kód DataMatrix:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_DM_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix)
    {
        Left = 1,
        Top = 400,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    signature.Sign(destinFilePath, hibcLic_DM_Options);
}
```

**Vysvětlení**: 
- `QrCodeSignOptions` se používá k nastavení vzhledu a obsahu kódu DataMatrix.
- Polohování (`Top`, `Left`) a nastavení načítání se řídí stejným vzorem jako předchozí kódy.

#### Tipy pro řešení problémů

- Ujistěte se, že jsou všechny cesty k souborům správně zadány.
- Ověřte, zda GroupDocs.Signature ve vaší verzi podporuje typy kódů DataMatrix.

### Podepište dokument pomocí QR kódu HIBC PAS

#### Přehled

Podepisování dokumentů pomocí QR kódu HIBC PAS zlepšuje sledování a dohledatelnost produktů. Tato část vás provede vkládáním QR kódu PAS do PDF souborů pomocí GroupDocs.Signature.

#### Kroky implementace

##### Krok 1: Konfigurace zdrojové a výstupní cesty

Definujte, kde se nachází zdrojový dokument a kam se má uložit podepsaný výstup:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCPASQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCPASQR.pdf");
```

##### Krok 2: Vytvořte možnosti podpisu pomocí QR kódu

Nakonfigurujte si QR kód PAS s konkrétním textem a nastavením:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcPas_QR_Options = new QrCodeSignOptions("PAS123456789012", QrCodeTypes.HIBCPASQR)
    {
        Left = 1,
        Top = 500,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    // Podepište dokument s těmito možnostmi.
    signature.Sign(destinFilePath, hibcPas_QR_Options);
}
```

**Vysvětlení**: 
- `QrCodeSignOptions` je nakonfigurován pro typ QR kódu HIBC PAS a umístěn v dokumentu.
- `ReturnContent` Nastavením na hodnotu true se načte vykreslený obraz podepsaného dokumentu.

#### Tipy pro řešení problémů

- Ujistěte se, že všechny cesty jsou správně zadány.
- Ověřte, zda GroupDocs.Signature ve vaší verzi podporuje typy QR kódů PAS.

### Závěr

Dodržováním tohoto návodu můžete efektivně integrovat QR kódy HIBC LIC a PAS do PDF dokumentů pomocí GroupDocs.Signature pro .NET. Tento proces zvyšuje zabezpečení dokumentů, sledovatelnost a dodržování předpisů v různých odvětvích. Další možnosti přizpůsobení a pokročilé funkce naleznete v [Dokumentace GroupDocs](https://docs.groupdocs.com/signature/net/).