---
title: Recuperare le informazioni sul documento
linktitle: Recuperare le informazioni sul documento
second_title: API GroupDocs.Signature .NET
description: Migliora la gestione dei documenti in .NET con GroupDocs.Signature. Recupera le informazioni sul documento passo dopo passo. Supporta vari formati.
type: docs
weight: 11
url: /it/net/document-preview-operations/retrieve-document-information/
---
## introduzione
Nel campo della documentazione digitale, garantire l'autenticità e l'integrità è fondamentale. GroupDocs.Signature per .NET fornisce una soluzione affidabile per la gestione delle firme dei documenti all'interno dell'ambiente .NET. In questo tutorial, approfondiremo il processo di recupero delle informazioni sui documenti utilizzando GroupDocs.Signature per .NET, analizzando ogni passaggio per una comprensione completa.
## Prerequisiti
Prima di immergerti nel tutorial, assicurati di disporre dei seguenti prerequisiti:
1.  Installazione: installare GroupDocs.Signature per .NET scaricandolo da[Qui](https://releases.groupdocs.com/signature/net/).
2. Ambiente .NET: avere una conoscenza pratica del framework .NET.
3. Documento: preparare un documento di esempio (ad esempio, "sample_multiple_signatures.docx") a scopo di test.

## Importazione di spazi dei nomi
Prima di procedere con il processo di recupero della firma del documento, importa gli spazi dei nomi necessari:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```

## Passaggio 1: impostare il percorso del file del documento:
Definisci il percorso del file per il documento da cui intendi recuperare le informazioni.
```csharp
string filePath = "sample_multiple_signatures.docx";
```
## Passaggio 2: istanziare l'oggetto firma:
 Crea un'istanza di`Signature` class passando il percorso del file del documento.
```csharp
using (Signature signature = new Signature(filePath))
{

}
```
## Passaggio 3: recuperare le informazioni sul documento:
 Utilizza il`GetDocumentInfo()` metodo per recuperare informazioni complete sul documento.
```csharp
IDocumentInfo documentInfo = signature.GetDocumentInfo();
```
## Passaggio 4: Visualizza le proprietà del documento:
Visualizza varie proprietà del documento come formato, estensione, dimensione, numero di pagine, ecc.
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


## Conclusione
GroupDocs.Signature per .NET offre una potente suite di strumenti per la gestione delle firme dei documenti senza problemi all'interno del framework .NET. Seguendo i passaggi descritti in questa guida, puoi recuperare in modo efficiente informazioni complete sui tuoi documenti, facilitando funzionalità avanzate di gestione dei documenti.

## Domande frequenti
### GroupDocs.Signature per .NET può gestire più formati di documenti?
Sì, GroupDocs.Signature supporta un'ampia gamma di formati di documenti, inclusi ma non limitati a DOCX, PDF, PNG e JPEG.
### È disponibile una versione di prova per GroupDocs.Signature per .NET?
 Sì, puoi accedere alla versione di prova da[Qui](https://releases.groupdocs.com/).
### GroupDocs.Signature per .NET fornisce supporto per le firme digitali?
Assolutamente sì, GroupDocs.Signature offre un solido supporto per le firme digitali, garantendo l'autenticità e l'integrità dei documenti.
### Dove posso trovare ulteriore documentazione e supporto per GroupDocs.Signature per .NET?
 È possibile fare riferimento alla documentazione completa[Qui](https://reference.groupdocs.com/signature/net/) e per assistenza, visita il forum GroupDocs[Qui](https://forum.groupdocs.com/c/signature/13).
### È possibile ottenere licenze temporanee per GroupDocs.Signature per .NET?
 Sì, è possibile acquistare licenze temporanee[Qui](https://purchase.groupdocs.com/temporary-license/).