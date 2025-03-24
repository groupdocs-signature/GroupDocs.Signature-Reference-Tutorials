---
title: Assinar imagem com metadados
linktitle: Assinar imagem com metadados
second_title: API GroupDocs.Signature .NET
description: Aprenda como assinar imagens com metadados em .NET usando GroupDocs.Signature. Solução de assinatura de metadados fácil, eficiente e personalizável.
weight: 10
url: /pt/net/document-signing/sign-image-with-metadata/
---

# Assinar imagem com metadados

## Introdução
GroupDocs.Signature for .NET permite que os desenvolvedores assinem imagens com metadados de forma eficiente. Este tutorial orienta você pelo processo passo a passo.
## Pré-requisitos
Antes de começar, certifique-se de ter o seguinte:
1. GroupDocs.Signature para .NET: Instale o pacote GroupDocs.Signature em seu projeto .NET. Você pode baixá-lo em[aqui](https://releases.groupdocs.com/signature/net/).   
2. Arquivo de imagem: prepare o arquivo de imagem que deseja assinar com metadados.

## Importar namespaces
Certifique-se de importar os namespaces necessários em seu código C#:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Etapa 1: carregar arquivo de imagem
Primeiro, especifique o caminho para o seu arquivo de imagem e o diretório de saída da imagem assinada com metadados:
```csharp
string filePath = "sample.png";            
string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
```
## Etapa 2: criar assinaturas de metadados
Em seguida, crie diferentes assinaturas de metadados e adicione-as à coleção de assinaturas de opções:
```csharp
using (Signature signature = new Signature(filePath))
{
    ushort imgsMetadataId = 41996;
    MetadataSignOptions options = new MetadataSignOptions();
    options
        .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Scherlock Holmes")) // Valor da sequência
        .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Valor de data e hora
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Valor inteiro
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Valor duplo
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Valor decimal
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Valor flutuante
    
    // assinar documento para arquivar
    SignResult result = signature.Sign(outputFilePath, options);
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Conclusão
Neste tutorial, você aprendeu como assinar uma imagem com metadados usando GroupDocs.Signature for .NET. Seguindo essas etapas, você pode incorporar facilmente assinaturas de metadados em seus aplicativos .NET.

## Perguntas frequentes
### Posso assinar várias imagens com metadados usando GroupDocs.Signature for .NET?
Sim, você pode assinar várias imagens com metadados iterando cada arquivo de imagem e aplicando as assinaturas de metadados.
### Existe uma versão de teste disponível para GroupDocs.Signature for .NET?
 Sim, você pode baixar a versão de teste em[aqui](https://releases.groupdocs.com/).
### O GroupDocs.Signature for .NET oferece suporte a outros formatos de arquivo além de imagens?
Sim, GroupDocs.Signature oferece suporte a vários formatos de arquivo, incluindo PDF, Word, Excel e muito mais.
### Posso personalizar a aparência da assinatura de metadados?
Sim, você pode personalizar a aparência da assinatura de metadados, como tamanho da fonte, cor e posição.
### Onde posso obter suporte para GroupDocs.Signature for .NET?
 Você pode obter suporte no fórum GroupDocs.Signature[aqui](https://forum.groupdocs.com/c/signature/13).