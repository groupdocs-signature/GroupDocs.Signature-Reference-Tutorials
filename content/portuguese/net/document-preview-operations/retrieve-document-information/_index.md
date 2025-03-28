---
title: Recuperar informações do documento
linktitle: Recuperar informações do documento
second_title: API GroupDocs.Signature .NET
description: Aprimore o gerenciamento de documentos em .NET com GroupDocs.Signature. Recupere informações do documento passo a passo. Suporta vários formatos.
weight: 11
url: /pt/net/document-preview-operations/retrieve-document-information/
---

# Recuperar informações do documento

## Introdução
No domínio da documentação digital, garantir a autenticidade e a integridade é fundamental. GroupDocs.Signature for .NET fornece uma solução robusta para gerenciar assinaturas de documentos no ambiente .NET. Neste tutorial, nos aprofundamos no processo de recuperação de informações de documentos usando GroupDocs.Signature for .NET, detalhando cada etapa para uma compreensão abrangente.
## Pré-requisitos
Antes de mergulhar no tutorial, certifique-se de ter os seguintes pré-requisitos em vigor:
1.  Instalação: Instale GroupDocs.Signature for .NET baixando-o em[aqui](https://releases.groupdocs.com/signature/net/).
2. Ambiente .NET: Tenha um conhecimento prático do framework .NET.
3. Documento: Prepare um documento de amostra (por exemplo, "sample_multiple_signatures.docx") para fins de teste.

## Importando Namespaces
Antes de prosseguir com o processo de recuperação de assinatura de documento, importe os namespaces necessários:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```

## Etapa 1: definir o caminho do arquivo do documento:
Defina o caminho do arquivo do documento do qual você pretende recuperar informações.
```csharp
string filePath = "sample_multiple_signatures.docx";
```
## Etapa 2: instanciar objeto de assinatura:
 Crie uma instância do`Signature` class passando o caminho do arquivo do documento.
```csharp
using (Signature signature = new Signature(filePath))
{

}
```
## Etapa 3: recuperar informações do documento:
 Utilize o`GetDocumentInfo()` método para buscar informações abrangentes sobre o documento.
```csharp
IDocumentInfo documentInfo = signature.GetDocumentInfo();
```
## Etapa 4: Exibir propriedades do documento:
Produza várias propriedades do documento, como formato, extensão, tamanho, contagem de páginas, etc.
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


## Conclusão
GroupDocs.Signature for .NET oferece um poderoso conjunto de ferramentas para gerenciar assinaturas de documentos perfeitamente dentro da estrutura .NET. Seguindo as etapas descritas neste guia, você pode recuperar com eficiência informações abrangentes sobre seus documentos, facilitando recursos aprimorados de gerenciamento de documentos.

## Perguntas frequentes
### O GroupDocs.Signature for .NET pode lidar com vários formatos de documentos?
Sim, GroupDocs.Signature oferece suporte a uma ampla variedade de formatos de documentos, incluindo, entre outros, DOCX, PDF, PNG e JPEG.
### Existe uma versão de teste disponível para GroupDocs.Signature for .NET?
 Sim, você pode acessar a versão de teste em[aqui](https://releases.groupdocs.com/).
### O GroupDocs.Signature for .NET oferece suporte para assinaturas digitais?
Com certeza, GroupDocs.Signature oferece suporte robusto para assinaturas digitais, garantindo a autenticidade e integridade do documento.
### Onde posso encontrar documentação adicional e suporte para GroupDocs.Signature for .NET?
 Você pode consultar a documentação abrangente[aqui](https://tutorials.groupdocs.com/signature/net/) e para suporte, visite o fórum GroupDocs[aqui](https://forum.groupdocs.com/c/signature/13).
### Podem ser obtidas licenças temporárias para GroupDocs.Signature for .NET?
 Sim, licenças temporárias estão disponíveis para compra[aqui](https://purchase.groupdocs.com/temporary-license/).