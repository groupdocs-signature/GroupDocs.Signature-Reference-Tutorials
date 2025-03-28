---
title: Assinar PDF com metadados
linktitle: Assinar PDF com metadados
second_title: API GroupDocs.Signature .NET
description: Aprenda como assinar documentos PDF com metadados usando GroupDocs.Signature for .NET. Melhore facilmente a rastreabilidade e a autenticidade dos documentos.
weight: 11
url: /pt/net/document-signing/sign-pdf-with-metadata/
---

# Assinar PDF com metadados

## Introdução
Neste tutorial, aprenderemos como assinar um documento PDF com metadados usando GroupDocs.Signature for .NET. Adicionar metadados a um PDF pode fornecer informações adicionais sobre o documento, como autoria, data de criação, ID do documento e muito mais.
## Pré-requisitos
Antes de começarmos, certifique-se de ter o seguinte:
1.  GroupDocs.Signature for .NET: você pode baixá-lo em[aqui](https://releases.groupdocs.com/signature/net/).
2. Um documento PDF: tenha um arquivo PDF de amostra pronto para assinar.
3. Conhecimento básico de programação C#: é necessária familiaridade com a sintaxe C# para entender os exemplos de código.
## Importar namespaces
Primeiro, certifique-se de importar os namespaces necessários para acessar as classes e métodos necessários:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Passo 1: Carregue o Documento PDF
Carregue o documento PDF que deseja assinar:
```csharp
string filePath = "sample.pdf";
```
## Etapa 2: especificar o caminho do arquivo de saída
Defina o caminho do arquivo de saída onde o PDF assinado com metadados será salvo:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
```
## Passo 3: Criar Instância de Assinatura
Inicialize uma instância de Signature fornecendo o caminho para o documento PDF:
```csharp
using (Signature signature = new Signature(filePath))
{
    // O código relacionado à assinatura irá aqui
}
```
## Etapa 4: definir opções de metadados
Crie MetadataSignOptions e adicione campos de metadados com seus respectivos valores:
```csharp
MetadataSignOptions options = new MetadataSignOptions();
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Valor da sequência
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Valores de data e hora
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Valor inteiro
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Valor duplo
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Valor decimal
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Valor flutuante
```
## Etapa 5: Assine o Documento
Assine o documento PDF com as opções de metadados especificadas e salve o documento assinado:
```csharp
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Conclusão
Neste tutorial, abordamos como assinar um documento PDF com metadados usando GroupDocs.Signature for .NET. Seguindo o guia passo a passo, você pode adicionar facilmente informações de metadados, como autoria, data de criação e muito mais, aos seus arquivos PDF, melhorando sua utilidade e rastreabilidade.
## Perguntas frequentes
### Posso adicionar campos de metadados personalizados aos meus documentos PDF?
Sim, você pode adicionar campos de metadados personalizados especificando o nome do campo e seu valor correspondente usando GroupDocs.Signature for .NET.
### O GroupDocs.Signature for .NET é compatível com todas as versões do .NET Framework?
GroupDocs.Signature for .NET é compatível com várias versões do .NET Framework, garantindo flexibilidade e facilidade de integração.
### O GroupDocs.Signature oferece suporte à assinatura de outros formatos de documento além do PDF?
Sim, GroupDocs.Signature oferece suporte a uma ampla variedade de formatos de documentos, incluindo Word, Excel, PowerPoint e muito mais.
### Posso assinar vários documentos em massa usando GroupDocs.Signature for .NET?
Sim, você pode assinar vários documentos em massa iterando uma lista de arquivos e aplicando o processo de assinatura programaticamente.
### O suporte técnico está disponível para usuários do GroupDocs.Signature?
 Sim, o GroupDocs fornece suporte técnico dedicado por meio de seus fóruns. Você pode acessar o fórum de suporte[aqui](https://forum.groupdocs.com/c/signature/13).