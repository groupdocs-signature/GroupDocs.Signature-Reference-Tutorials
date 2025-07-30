---
"date": "2025-05-07"
"description": "Aprenda a firmar imágenes DICOM con códigos QR usando GroupDocs.Signature para .NET. Esta guía abarca la configuración, implementación y verificación de firmas de códigos QR en imágenes médicas."
"title": "Cómo firmar imágenes DICOM con códigos QR usando GroupDocs.Signature para .NET&#58; una guía completa"
"url": "/es/net/qr-code-signatures/groupdocs-signature-net-dicom-images-qr-codes/"
"weight": 1
---

# Cómo firmar imágenes DICOM con códigos QR usando GroupDocs.Signature para .NET: una guía completa

¿Busca un método seguro para autenticar sus archivos DICOM? Esta guía detallada le mostrará cómo usar GroupDocs.Signature para .NET para integrar firmas de códigos QR en imágenes DICOM. Ideal para profesionales de la salud, desarrolladores y cualquier persona que trabaje con documentos médicos digitales, este tutorial abarca desde la configuración hasta la implementación.

## Lo que aprenderás:
- Configurar su entorno de desarrollo con GroupDocs.Signature para .NET.
- Instrucciones paso a paso sobre cómo firmar imágenes DICOM mediante códigos QR.
- Métodos para verificar y buscar firmas de códigos QR en archivos DICOM.
- Técnicas para generar vistas previas de documentos firmados para fines de revisión.
- Mejores prácticas para optimizar el rendimiento y gestionar los recursos de forma eficaz.

¡Comencemos con los prerrequisitos!

## Prerrequisitos

Para usar GroupDocs.Signature para .NET, asegúrese de que su entorno esté preparado. Necesitará lo siguiente:

### Bibliotecas y versiones requeridas
- **GroupDocs.Signature para .NET**:Asegure la compatibilidad con su marco .NET.

### Requisitos de configuración del entorno
- Un entorno de desarrollo en Windows o Linux.
- Visual Studio u otro IDE compatible con .NET instalado.

### Requisitos previos de conocimiento
- Comprensión básica de programación en C#.
- Familiaridad con la E/S de archivos en aplicaciones .NET.

## Configuración de GroupDocs.Signature para .NET

Instale la biblioteca GroupDocs.Signature utilizando su método preferido:

**Usando la CLI .NET:**
```bash
dotnet add package GroupDocs.Signature
```

**Administrador de paquetes:**
```powershell
Install-Package GroupDocs.Signature
```

**Interfaz de usuario del administrador de paquetes NuGet:**
- Busque "GroupDocs.Signature" e instale la última versión.

### Adquisición de licencias

Comience con una prueba gratuita para explorar las funciones. Para un uso prolongado, considere adquirir una licencia temporal o completa de [Documentos de grupo](https://purchase.groupdocs.com/buy).

Una vez instalada, inicialice la biblioteca:

```csharp
using GroupDocs.Signature;
// Inicialice el objeto Firma con la ruta del archivo DICOM.
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample.dicom");
```

## Guía de implementación

### Firmar imagen DICOM con código QR

#### Descripción general
Agregue firmas de código QR para garantizar la autenticidad y trazabilidad de los documentos médicos.

**Paso 1: Inicializar el objeto de firma**

```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY\\sample.dicom";
using (Signature signature = new Signature(filePath))
{
    // Proceder con las operaciones de firma...
}
```

**Paso 2: Crear opciones de señalización con código QR**

Configure propiedades como texto, tamaño y alineación.

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

**Paso 3: Agregar metadatos XMP**

Mejore el documento con metadatos adicionales.

```csharp
DicomSaveOptions dicomSaveOptions = new DicomSaveOptions()
{
    XmpEntries = new List<DicomXmpEntry>() { new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4") }
};
```

**Paso 4: Firmar el documento**

Ejecutar firma y guardar.

```csharp
SignResult signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY\\SignedDicom", options, dicomSaveOptions);
```

### Obtener información del documento

Recupere metadatos de archivos DICOM firmados para garantizar la integridad de los datos.

**Descripción general:**
Acceda a la información del documento y a las firmas de metadatos XMP para su verificación.

**Paso 1: Recuperar información del documento**

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    IDocumentInfo signedDocumentInfo = signature.GetDocumentInfo();
}
```

**Paso 2: Iterar e imprimir datos XMP**

Mostrar detalles de metadatos.

```csharp
foreach (var item in signedDocumentInfo.MetadataSignatures)
{
    Console.WriteLine(item.ToString());
}
```

### Verificar firmas DICOM

Validar la autenticidad de las firmas de códigos QR dentro de las imágenes DICOM.

**Descripción general:**
Asegúrese de que las firmas sean correctas y auténticas.

**Paso 1: Crear código QR Verificar opciones**

Establecer opciones que coincidan con texto específico en los códigos QR.

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true,
    Text = "Patient #36363393",
    MatchType = TextMatchType.Contains
};
```

**Paso 2: Verificar firmas**

Comprobar si las firmas cumplen los criterios.

```csharp
VerificationResult result = signature.Verify(options);

if (result.IsValid)
{
    Console.WriteLine($"DICOM {filePath} has {result.Succeeded.Count} successfully verified signatures!");
}
```

### Búsqueda de firmas en DICOM

Localice firmas de códigos QR dentro de imágenes DICOM firmadas.

**Descripción general:**
Encuentre de forma eficiente todas las firmas de códigos QR para gestionar la autenticidad de los documentos.

**Paso 1: Buscar firmas de códigos QR**

```csharp
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

**Paso 2: Iterar e imprimir los detalles de la firma**

Revise los detalles de cada firma encontrada.

```csharp
foreach (var QrCodeSignature in signatures)
{
    Console.WriteLine($"QRCode signature found at page {QrCodeSignature.PageNumber} with type {QrCodeSignature.EncodeType.TypeName} and text {QrCodeSignature.Text}");
}
```

### Generar vista previa de DICOM firmado

Crear vistas previas visuales para verificación.

**Descripción general:**
Genere vistas previas de imágenes para verificar contenido sin software especializado.

**Paso 1: Definir métodos de transmisión**

Configurar métodos para la gestión del flujo de archivos durante la generación de la vista previa.

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

**Paso 2: Generar vistas previas**

Ejecutar el proceso de generación de vista previa.

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

## Aplicaciones prácticas

1. **Gestión de registros médicos**:Autenticar registros de pacientes utilizando firmas de código QR para cumplimiento.
2. **Registros de auditoría en los sistemas de salud**:Realice un seguimiento de los cambios en los documentos y verifique la autenticidad con códigos QR.
3. **Intercambio seguro de datos**:Garantice el intercambio seguro de imágenes médicas mediante la incorporación de firmas digitales.
4. **Verificación de cumplimiento**:Verifique periódicamente la integridad de los archivos DICOM para cumplir con los requisitos legales.
5. **Integración con sistemas EHR**:Integre sin problemas archivos DICOM firmados en los sistemas de registros médicos electrónicos (EHR) para optimizar las operaciones.