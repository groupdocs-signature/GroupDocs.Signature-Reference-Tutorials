---
"date": "2025-05-08"
"description": "Naučte se, jak bezpečně podepisovat snímky DICOM pomocí GroupDocs.Signature pro Javu. Zvyšte zabezpečení dokumentů vložením QR kódů a metadat."
"title": "Podepisování obrázků DICOM pomocí QR kódů a metadat pomocí GroupDocs.Signature pro Javu"
"url": "/cs/java/image-signatures/sign-dicom-images-groupdocs-signature-java/"
"weight": 1
---

# Jak podepsat obrázky DICOM pomocí QR kódů a metadat pomocí GroupDocs.Signature pro Javu

## Zavedení

V rychle se vyvíjejícím prostředí digitálního zdravotnictví je bezpečná správa dat pacientů prvořadá. Tento tutoriál vás provede implementací robustního řešení s využitím GroupDocs.Signature for Java k podepisování snímků DICOM (Digital Imaging and Communications in Medicine) pomocí QR kódů a metadat. Tyto funkce zajišťují autenticitu, zlepšují sledovatelnost a udržují shodu s předpisy tím, že vkládají důležité informace přímo do lékařských snímků.

### Co se naučíte:
- Jak integrovat GroupDocs.Signature pro Javu do vašeho projektu.
- Proces podepisování DICOM snímků pomocí QR kódů.
- Přidání metadat XMP pro zvýšení zabezpečení dokumentů.
- Načítání, ověřování a vyhledávání podpisů v souborech DICOM.
- Generování náhledů podepsaných DICOM snímků.

Pojďme se na to pustit! Než začneme, ujistěte se, že máte vše potřebné k bezproblémovému sledování.

## Předpoklady

Pro efektivní implementaci funkcí GroupDocs.Signature se ujistěte, že splňujete následující předpoklady:

### Požadované knihovny a závislosti
- **GroupDocs.Signature pro Javu**Budete potřebovat tuto knihovnu verze 23.12 nebo novější.

### Požadavky na nastavení prostředí
- **Vývojová sada pro Javu (JDK)**Ujistěte se, že je ve vašem systému nainstalováno JDK.
- **IDE**Použijte integrované vývojové prostředí, jako je IntelliJ IDEA nebo Eclipse.

### Předpoklady znalostí
Základní znalost:
- Programování v Javě a principy objektově orientovaného programování.
- Nástroje pro správu závislostí v Mavenu nebo Gradlu.

## Nastavení GroupDocs.Signature pro Javu

Abyste mohli začít s GroupDocs.Signature, musíte jej přidat jako závislost do svého projektu. Zde je návod, jak to udělat pomocí různých nástrojů pro sestavení:

### Znalec
Přidejte následující úryvek do svého `pom.xml` soubor:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle
Zahrňte toto do svého `build.gradle` soubor:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Přímé stažení
Případně si můžete stáhnout nejnovější verzi z [GroupDocs.Signature pro verze Javy](https://releases.groupdocs.com/signature/java/).

#### Kroky získání licence
1. **Bezplatná zkušební verze**Vyzkoušejte si funkce s časově omezenou bezplatnou zkušební verzí.
2. **Dočasná licence**Získejte dočasnou licenci pro vyzkoušení všech funkcí.
3. **Nákup**Pokud potřebujete dlouhodobý přístup, zakupte si předplatné.

#### Základní inicializace a nastavení

Pro inicializaci GroupDocs.Signature vytvořte instanci třídy `Signature` třída:
```java
import com.groupdocs.signature.Signature;

// Inicializujte objekt podpisu cestou k vašemu souboru DICOM
Signature signature = new Signature(filePath);
```

## Průvodce implementací

### Podepsání obrazu DICOM pomocí QR kódu a metadat

#### Přehled
Tato funkce umožňuje podepisovat snímky DICOM pomocí QR kódu a přidávat metadata XMP, což zvyšuje zabezpečení dokumentů.

#### Krok 1: Nastavení možností podpisu pomocí QR kódu
```java
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.QrCodeSignOptions;

Padding padding = new Padding();
padding.setRight(5);
padding.setLeft(5);

QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues");
options.setAllPages(true);
options.setWidth(100);
options.setHeight(100);
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
options.setMargin(padding);
```
Zde nakonfigurujeme vzhled a umístění QR kódu na obrázku DICOM.

#### Krok 2: Přidání metadat XMP
```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomSaveOptions;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpEntry;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpType;

DicomSaveOptions dicomSaveOptions = new DicomSaveOptions();
List<DicomXmpEntry> xmpEntries = new ArrayList<>();
xmpEntries.add(new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4"));
dicomSaveOptions.setXmpEntries(xmpEntries);
```
Tento úryvek přidává metadata do souboru DICOM a vkládá do nich další informace o pacientovi.

#### Krok 3: Podepište dokument
```java
String outputFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/" + fileName;
signature.sign(outputFilePath, options, dicomSaveOptions);
```
Ten/Ta/To `sign` Metoda zapíše QR kód a metadata do vašeho DICOM souboru a uloží ho na určené místo.

### Načtení informací o podepsaném snímku DICOM

#### Přehled
Extrahujte metadata XMP z podepsaného obrazu DICOM pro účely ověření nebo auditu.
```java
import com.groupdocs.signature.domain.IDocumentInfo;
import com.groupdocs.signature.domain.signatures.MetadataSignature;

IDocumentInfo documentInfo = signature.getDocumentInfo();
for (MetadataSignature item : documentInfo.getMetadataSignatures()) {
    System.out.println(item.toString());
}
```
Tento kód načte a vytiskne všechny podpisy metadat spojených se souborem DICOM.

### Ověření podepsaného DICOM

#### Přehled
Ověřte, zda je na podepsaném obrázku DICOM přítomen podpis QR kódem, abyste potvrdili jeho pravost.
```java
import com.groupdocs.signature.domain.VerificationResult;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;
import com.groupdocs.signature.domain.enums.TextMatchType;

QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();
verifyOptions.setAllPages(true);
verifyOptions.setText("Patient #36363393");
verifyOptions.setMatchType(TextMatchType.Contains);

VerificationResult result = signature.verify(verifyOptions);
if (result.isValid()) {
    System.out.println(filePath + " has successfully verified signatures!");
} else {
    System.out.println(filePath + " failed verification process.");
}
```
Tento krok ověření zajišťuje, že QR kód splňuje očekávaná kritéria, a potvrzuje tak integritu dokumentu.

### Hledání podpisů v podepsaném DICOM

#### Přehled
Vyhledejte všechny podpisy QR kódů v podepsaném obrázku DICOM a zkontrolujte je nebo ověřte.
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.util.List;

List<QrCodeSignature> signatures = signature.search(QrCodeSignature.class);
for (QrCodeSignature qrCodeSignature : signatures) {
    System.out.println("QRCode signature found at page " +
        qrCodeSignature.getPageNumber() + ": " +
        qrCodeSignature.getEncodeType().getTypeName() + ": " +
        qrCodeSignature.getText());
}
```
Tato funkce je užitečná pro skenování všech podpisů QR kódů v dokumentu a poskytuje tak komplexní přehled.

### Generování náhledu podepsaného DICOM

#### Přehled
Vytvořte náhledy pro každou stránku podepsaného obrazu DICOM, což umožňuje rychlou vizuální kontrolu bez nutnosti otevírat celý soubor.
```java
import com.groupdocs.signature.options.PreviewOptions;
import java.io.File;
import java.io.FileOutputStream;
import java.nio.file.Paths;

PreviewOptions previewOption = new PreviewOptions(pageNumber -> {
    try {
        String pageFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/image-" + pageNumber + ".jpg";
        return new FileOutputStream(Paths.get(pageFilePath).toFile());
    } catch (Exception e) {
        throw new RuntimeException(e.getMessage());
    }
});

signature.generatePreview(previewOption);
```
Tento úryvek generuje náhledy obrázků pro každou stránku, což může být užitečné pro rychlé ověření nebo sdílení.

## Praktické aplikace

GroupDocs.Signature pro Javu nabízí několik reálných aplikací:
- **Lékařské zobrazování**Bezpečně podepisujte a spravujte DICOM snímky pacientů pomocí QR kódů a metadat.
- **Správa právních dokumentů**Zvýšit autenticitu a soulad dokumentů v soudních řízeních.
- **Finanční služby**Implementujte zabezpečené elektronické podpisy na citlivých finančních dokumentech.