---
"description": "Domine la búsqueda de firmas digitales en documentos con GroupDocs.Signature para .NET. Mejore la seguridad y la verificación de documentos con nuestra guía detallada paso a paso."
"linktitle": "Búsqueda de firmas digitales"
"second_title": "API .NET de GroupDocs.Signature"
"title": "Buscar firmas digitales en documentos"
"url": "/es/net/signature-searching/search-for-digital-signatures/"
"weight": 11
---

## Introducción

En el panorama digital actual, garantizar la autenticidad e integridad de los documentos es fundamental para empresas y organizaciones. Las firmas digitales proporcionan un mecanismo robusto para verificar la autenticidad de los documentos y detectar modificaciones no autorizadas. GroupDocs.Signature para .NET ofrece una solución integral para trabajar con firmas digitales en diversos formatos de documentos, lo que permite a los desarrolladores integrar fácilmente la funcionalidad de firma en sus aplicaciones .NET.

Este tutorial lo guiará a través del proceso de búsqueda de firmas digitales dentro de documentos utilizando GroupDocs.Signature para .NET, brindando explicaciones detalladas y ejemplos de código prácticos.

## Prerrequisitos

Antes de profundizar en los detalles de implementación, asegúrese de tener los siguientes requisitos previos:

1. GroupDocs.Signature para .NET: Descargue e instale la biblioteca desde [aquí](https://releases.groupdocs.com/signature/net/).
   
2. Entorno de desarrollo: configure un entorno de desarrollo .NET con Visual Studio o su IDE preferido.
   
3. Documentos de muestra: prepare documentos de muestra que contengan firmas digitales para fines de prueba.

4. Conocimientos básicos: Familiaridad con el lenguaje de programación C# y fundamentos del marco .NET.

## Importar espacios de nombres

Comience importando los espacios de nombres necesarios para acceder a la funcionalidad proporcionada por GroupDocs.Signature para .NET:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Ahora, desglosemos el proceso de búsqueda de firmas digitales en pasos claros y manejables:

## Paso 1: Inicializar el objeto de firma

Comience creando una instancia de la `Signature` clase, pasando la ruta a su documento:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Se agregará aquí el código para buscar firmas digitales.
}
```

## Paso 2: Buscar firmas digitales

A continuación, utilice el `Search` método con el `SignatureType.Digital` parámetro para buscar firmas digitales en el documento:

```csharp
// Buscar firmas digitales en el documento
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```

## Paso 3: Procesar y mostrar resultados

Finalmente, procesa los resultados de la búsqueda y muestra información relevante sobre las firmas digitales encontradas:

```csharp
Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
foreach (var digitalSignature in signatures)
{
    Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
    Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
    Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
    Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
    Console.WriteLine();
}
```

## Ejemplo completo

A continuación se muestra un ejemplo completo y funcional que demuestra cómo buscar firmas digitales en un documento:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SearchDigitalSignatures
{
    class Program
    {
        static void Main(string[] args)
        {
            // Ruta del documento
            string filePath = "sample_multiple_signatures.docx";
            
            // Inicializar instancia de firma
            using (Signature signature = new Signature(filePath))
            {
                // Buscar firmas digitales en el documento
                List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
                
                // Mostrar resultados de búsqueda
                Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
                
                if (signatures.Count > 0)
                {
                    foreach (var digitalSignature in signatures)
                    {
                        Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
                        Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
                        Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
                        Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
                        Console.WriteLine();
                    }
                }
                else
                {
                    Console.WriteLine("No digital signatures found in the document.");
                }
            }
        }
    }
}
```

## Opciones de búsqueda avanzada

Para búsquedas más específicas, puede utilizar `DigitalSearchOptions` Para personalizar los criterios de búsqueda:

```csharp
// Crear opciones de búsqueda digital
DigitalSearchOptions options = new DigitalSearchOptions()
{
    // Buscar sólo en páginas específicas (por ejemplo, páginas 1 y 2)
    PageNumber = 1,
    PagesSetup = new PagesSetup() { Pages = new List<int> { 1, 2 } },
    
    // Filtrar por comentarios en firmas digitales
    Comments = "Approved",
    
    // Establecer un rango de fecha y hora para la búsqueda
    SignDateTimeFrom = new DateTime(2022, 1, 1),
    SignDateTimeTo = DateTime.Now
};

// Buscar con opciones específicas
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(options);
```

## Trabajar con información del certificado

Las firmas digitales contienen información valiosa del certificado a la que puede acceder y validar:

```csharp
foreach (var digitalSignature in signatures)
{
    if (digitalSignature.Certificate != null)
    {
        // Propiedades del certificado de acceso
        Console.WriteLine($"Certificate Valid From: {digitalSignature.Certificate.NotBefore}");
        Console.WriteLine($"Certificate Valid To: {digitalSignature.Certificate.NotAfter}");
        
        // Comprobar si el certificado está en un rango de fechas válido
        bool isDateValid = DateTime.Now >= digitalSignature.Certificate.NotBefore && 
                          DateTime.Now <= digitalSignature.Certificate.NotAfter;
        
        Console.WriteLine($"Certificate Date Validity: {isDateValid}");
        
        // Acceder a los detalles del emisor del certificado
        Console.WriteLine($"Certificate Issuer: {digitalSignature.Certificate.IssuerName}");
    }
}
```

## Conclusión

GroupDocs.Signature para .NET ofrece una solución potente y flexible para la búsqueda y validación de firmas digitales en documentos. En este tutorial, exploramos paso a paso la implementación de la función de búsqueda de firmas digitales en aplicaciones .NET, brindándole los conocimientos necesarios para mejorar la seguridad y la verificación de la integridad de los documentos.

Al aprovechar GroupDocs.Signature, puede crear sistemas sólidos de gestión de documentos que garanticen la autenticidad e integridad de sus documentos digitales, fomentando la confianza y el cumplimiento en sus procesos comerciales.

## Preguntas frecuentes

### ¿Puede GroupDocs.Signature verificar la validez de las firmas digitales?

Sí, GroupDocs.Signature valida automáticamente las firmas digitales durante el proceso de búsqueda y proporciona el estado de validación a través de `IsValid` propiedad de la `DigitalSignature` clase.

### ¿Qué formatos de documentos admiten la búsqueda de firmas digitales?

GroupDocs.Signature admite la búsqueda de firmas digitales en varios formatos, incluidos PDF, documentos de Microsoft Office (Word, Excel, PowerPoint), formatos OpenOffice y más.

### ¿Puedo buscar firmas digitales en documentos protegidos con contraseña?

Sí, puede buscar firmas digitales en documentos protegidos con contraseña proporcionando la contraseña al inicializar el documento. `Signature` objeto:

```csharp
LoadOptions loadOptions = new LoadOptions() { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Búsqueda de firmas digitales
}
```

### ¿Cómo puedo verificar si una firma digital fue creada por una persona específica?

Puede examinar el nombre del sujeto del certificado y otras propiedades para verificar la identidad del firmante:

```csharp
foreach (var signature in signatures)
{
    if (signature.Certificate?.SubjectName?.Contains("John Doe") == true)
    {
        Console.WriteLine("Found signature by John Doe");
    }
}
```

### ¿Puedo extraer la clave pública de un certificado de firma digital?

Sí, puede acceder a la información de la clave pública a través de las propiedades del certificado:

```csharp
if (signature.Certificate != null)
{
    // Acceder a la información de clave pública
    Console.WriteLine($"Public Key: {signature.Certificate.GetPublicKeyString()}");
}
```

## Ver también

* [Referencia de API](https://reference.groupdocs.com/signature/net/)
* [Ejemplos de código](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentación del producto](https://docs.groupdocs.com/signature/net/)
* [Página del producto](https://products.groupdocs.com/signature/net/)
* [Descargar la última versión](https://releases.groupdocs.com/signature/net/)
* [Artículos del blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Foro de soporte](https://forum.groupdocs.com/c/signature/13)
* [Licencia temporal](https://purchase.groupdocs.com/temporary-license/)