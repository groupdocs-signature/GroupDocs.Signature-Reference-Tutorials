---
title: Pesquise várias assinaturas
linktitle: Pesquise várias assinaturas
second_title: API GroupDocs.Signature .NET
description: Aprenda como pesquisar várias assinaturas em documentos .NET usando GroupDocs.Signature para segurança e integridade eficientes de documentos.
weight: 14
url: /pt/net/signature-searching/search-for-multiple-signatures/
---
## Introdução
GroupDocs.Signature for .NET é uma biblioteca poderosa que permite aos desenvolvedores adicionar, pesquisar e remover vários tipos de assinaturas em formatos de documentos populares usando aplicativos .NET. Neste tutorial, nos concentraremos na pesquisa de várias assinaturas em um documento usando GroupDocs.Signature for .NET.
## Pré-requisitos
Antes de começarmos, certifique-se de ter os seguintes pré-requisitos:
- Visual Studio instalado em seu sistema.
- Compreensão básica da linguagem de programação C#.
- Biblioteca GroupDocs.Signature for .NET instalada em seu projeto. Você pode baixá-lo em[aqui](https://releases.groupdocs.com/signature/net/).

## Importar namespaces
Primeiro, você precisa importar os namespaces necessários para acessar as classes e métodos fornecidos pelo GroupDocs.Signature for .NET.
```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Etapa 1: carregue o documento
Carregue o documento onde deseja pesquisar múltiplas assinaturas. Certifique-se de fornecer o caminho de arquivo correto.
```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Seu código vai aqui
}
```
## Etapa 2: definir opções de pesquisa
Defina opções de pesquisa para vários tipos de assinaturas, como texto, digital, código de barras, código QR e metadados. Você pode especificar critérios de pesquisa, como texto a ser correspondido, tipo de correspondência e pesquisa em todas as páginas.
```csharp
// Definir opções de pesquisa
TextSearchOptions textOptions = new TextSearchOptions()
{
    AllPages = true
};
DigitalSearchOptions digitalOptions = new DigitalSearchOptions()
{
    AllPages = true
};
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions()
{
    AllPages = true,
    Text = "123456",
    MatchType = TextMatchType.Exact
};
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions()
{
    AllPages = true,
    Text = "John",
    MatchType = TextMatchType.Contains
};
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```
## Etapa 3: adicionar opções de pesquisa à lista
Adicione as opções de pesquisa definidas a uma lista.
```csharp
// Adicionar opções à lista
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
listOptions.Add(metadataOptions);
listOptions.Add(digitalOptions);
```
## Etapa 4: procure por assinaturas
Pesquise assinaturas no documento usando as opções de pesquisa definidas.
```csharp
// Procure assinaturas no documento
SearchResult result = signature.Search(listOptions);
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains following signatures.");
    foreach (var resSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found at page {resSignature.PageNumber} with type {resSignature.SignatureType} and Id#: {resSignature.SignatureId}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## Conclusão
Neste tutorial, aprendemos como pesquisar várias assinaturas em um documento usando GroupDocs.Signature for .NET. Seguindo as etapas fornecidas, você pode localizar com eficiência vários tipos de assinaturas em seus documentos, aumentando a segurança e a integridade dos documentos.
## Perguntas frequentes
### Posso procurar assinaturas em diferentes formatos de documentos?
Sim, GroupDocs.Signature for .NET oferece suporte a uma ampla variedade de formatos de documentos, incluindo Word, PDF, Excel e muito mais.
### É possível personalizar critérios de pesquisa de assinaturas?
Com certeza, você pode personalizar os critérios de pesquisa de acordo com suas necessidades, como especificar correspondências exatas de texto ou pesquisar em todas as páginas.
### O GroupDocs.Signature for .NET oferece suporte para assinaturas digitais?
Sim, você pode pesquisar assinaturas digitais, bem como outros tipos, como texto, código de barras e assinaturas de código QR.
### Posso integrar facilmente a funcionalidade de pesquisa de assinaturas em meus aplicativos .NET?
Sim, GroupDocs.Signature for .NET fornece uma API direta que simplifica o processo de integração.
### Onde posso encontrar suporte ou assistência adicional?
 Você pode visitar o fórum GroupDocs.Signature[aqui](https://forum.groupdocs.com/c/signature/13) para qualquer dúvida ou assistência.