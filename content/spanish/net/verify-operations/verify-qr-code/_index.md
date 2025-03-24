---
title: Verificar código QR
linktitle: Verificar código QR
second_title: API GroupDocs.Signature .NET
description: Aprenda a verificar códigos QR dentro de documentos usando GroupDocs.Signature para .NET. Tutorial completo con guía paso a paso.
weight: 12
url: /es/net/verify-operations/verify-qr-code/
---
## Introducción
En el ámbito de la gestión y autenticación de documentos, garantizar la integridad y validez de las firmas es primordial. GroupDocs.Signature para .NET proporciona una solución integral para verificar códigos QR incrustados en documentos. En este tutorial, profundizaremos en el proceso paso a paso de verificar códigos QR usando GroupDocs.Signature para .NET.
## Requisitos previos
Antes de sumergirse en el proceso de verificación, asegúrese de cumplir con los siguientes requisitos previos:
1.  Instalación de GroupDocs.Signature para .NET: Descargue e instale GroupDocs.Signature para .NET desde[enlace de descarga](https://releases.groupdocs.com/signature/net/).
2. Acceso a un documento que contiene códigos QR: prepare un documento de muestra que contenga códigos QR para su verificación. 

## Importar espacios de nombres
En primer lugar, debe importar los espacios de nombres necesarios para utilizar las funcionalidades proporcionadas por GroupDocs.Signature para .NET. Sigue estos pasos:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```


Ahora, analicemos el proceso de verificación de códigos QR incrustados en un documento usando GroupDocs.Signature para .NET:
## Paso 1: especificar la ruta del documento
```csharp
string filePath = "sample_multiple_signatures.docx";
```
 Asegúrese de reemplazar`"sample_multiple_signatures.docx"` con la ruta a su documento.
## Paso 2: inicializar el objeto de firma
```csharp
using (Signature signature = new Signature(filePath))
{
    //El código de verificación va aquí.
}
```
 Inicializar un`Signature` objeto proporcionando la ruta al documento.
## Paso 3: especificar opciones de verificación
```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // este valor está establecido por defecto
    Text = "John",
    MatchType = TextMatchType.Contains
};
```
 Definir opciones de verificación como`AllPages` para verificar todas las páginas,`Text` para especificar el texto que debe coincidir dentro del código QR, y`MatchType` para definir los criterios de coincidencia.
## Paso 4: verificar las firmas de los documentos
```csharp
VerificationResult result = signature.Verify(options);
```
 Invocar el`Verify` método de la`Signature` objeto, pasando las opciones de verificación.
## Paso 5: Manejar los resultados de la verificación
```csharp
if (result.IsValid)
{
    // Se encontró una firma válida
}
else
{
    // Se encontró una firma no válida
}
```
Según el resultado de la verificación, maneje los escenarios de éxito o fracaso en consecuencia.

## Conclusión
En este tutorial, exploramos el proceso de verificación de códigos QR dentro de documentos usando GroupDocs.Signature para .NET. Si sigue estos pasos, podrá integrar perfectamente la funcionalidad de verificación de códigos QR en sus aplicaciones .NET, garantizando la integridad y autenticidad de los documentos.
## Preguntas frecuentes
### ¿Puede GroupDocs.Signature para .NET verificar códigos QR en diferentes formatos de documentos?
Sí, GroupDocs.Signature para .NET admite una amplia gama de formatos de documentos, incluidos DOCX, PDF y más, para la verificación de códigos QR.
### ¿Hay una prueba gratuita disponible para GroupDocs.Signature para .NET?
 Sí, puedes aprovechar una prueba gratuita desde el[página de lanzamientos](https://releases.groupdocs.com/).
### ¿Qué opciones de soporte están disponibles para GroupDocs.Signature para usuarios de .NET?
 Los usuarios pueden acceder al soporte a través del[foro](https://forum.groupdocs.com/c/signature/13) para GroupDocs.Firma.
### ¿Puedo comprar una licencia temporal de GroupDocs.Signature para .NET?
 Sí, las licencias temporales están disponibles para su compra en el[Página de compra de GroupDocs](https://purchase.groupdocs.com/temporary-license/).
### ¿Existe documentación extensa disponible para GroupDocs.Signature para .NET?
 Por supuesto, puede consultar la documentación detallada proporcionada.[aquí](https://tutorials.groupdocs.com/signature/net/) para obtener orientación completa sobre cómo utilizar las funcionalidades de GroupDocs.Signature para .NET.