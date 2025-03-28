---
title: Firmar con Stamp usando GroupDocs.Signature
linktitle: Firmar con sello
second_title: API GroupDocs.Signature .NET
description: Aprenda cómo agregar firmas de sello a sus documentos .NET fácilmente con GroupDocs.Signature para .NET. Mejorar la seguridad de los documentos.
weight: 16
url: /es/net/advanced-signature-techniques/sign-with-stamp/
---

# Firmar con Stamp usando GroupDocs.Signature

## Introducción
En este tutorial, lo guiaremos a través del proceso de firmar un documento con un sello usando GroupDocs.Signature para .NET. Si sigue estas instrucciones paso a paso, podrá agregar un sello de firma a sus documentos con facilidad.
## Requisitos previos
Antes de comenzar, asegúrese de tener los siguientes requisitos previos:
1.  GroupDocs.Signature para .NET SDK: descargue e instale el SDK desde[sitio web](https://releases.groupdocs.com/signature/net/).
2. Entorno de desarrollo: asegúrese de tener un entorno de desarrollo adecuado configurado para el desarrollo .NET.
3. Documento para firmar: prepare el documento (p. ej., PDF) que desea firmar con un sello.

## Importando espacios de nombres
Comience importando los espacios de nombres necesarios a su proyecto:
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Paso 1: cargue el documento
```csharp
string filePath = "sample.pdf";
using (Signature signature = new Signature(filePath))
{
    // Tu código va aquí
}
```
## Paso 2: configurar las opciones de signo de sello
```csharp
StampSignOptions options = new StampSignOptions()
{
    Left = 50,
    Top = 150,                    
    Width = 200,
    Height = 200
};
```
## Paso 3: configurar la apariencia del sello
```csharp
StampLine outerLine = new StampLine();
outerLine.Text = " * European Union ";
outerLine.TextRepeatType = StampTextRepeatType.FullTextRepeat;
outerLine.Font.Size = 12;
outerLine.Height = 22;
outerLine.TextBottomIntent = 6;
outerLine.TextColor = Color.WhiteSmoke;
outerLine.BackgroundColor = Color.DarkSlateBlue;
options.OuterLines.Add(outerLine);
StampLine innerLine = new StampLine();
innerLine.Text = "John Smith";
innerLine.TextColor = Color.MediumVioletRed;
innerLine.Font.Size = 20;
innerLine.Font.Bold = true;
innerLine.Height = 40;
options.InnerLines.Add(innerLine);
```
## Paso 4: Firme el documento
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithStamp", fileName);
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Conclusión
Agregar firmas de sello a sus documentos usando GroupDocs.Signature para .NET es un proceso sencillo, como se demuestra en este tutorial. Con los pasos proporcionados, puede mejorar fácilmente la seguridad y autenticidad de sus documentos.
## Preguntas frecuentes
### ¿Puedo personalizar la apariencia de la firma del sello?
Sí, puede personalizar varios aspectos como el texto, la fuente, el color y la ubicación de la firma del sello según sus requisitos.
### ¿GroupDocs.Signature admite la firma de múltiples formatos de documentos?
Sí, GroupDocs.Signature admite una amplia gama de formatos de documentos, incluidos PDF, Microsoft Word, Excel, PowerPoint y más.
### ¿Existe una versión de prueba disponible para GroupDocs.Signature?
 Sí, puedes acceder a la versión de prueba gratuita desde[sitio web](https://releases.groupdocs.com/).
### ¿Puedo agregar varias firmas a un solo documento?
Por supuesto, GroupDocs.Signature le permite agregar varias firmas, incluidos sellos, texto, imágenes y firmas digitales, a un solo documento.
### ¿Dónde puedo encontrar soporte si encuentro algún problema durante la implementación?
 Puede encontrar soporte y asistencia en el foro de la comunidad GroupDocs.Signature.[aquí](https://forum.groupdocs.com/c/signature/13).