---
title: Excluir assinatura por ID
linktitle: Excluir assinatura por ID
second_title: API GroupDocs.Signature .NET
description: Aprenda como excluir uma assinatura por ID em documentos .NET usando a biblioteca GroupDocs.Signature. Guia passo a passo fácil.
type: docs
weight: 11
url: /pt/net/delete-operations/delete-signature-by-id/
---
## Introdução
Neste tutorial, exploraremos como excluir uma assinatura por seu ID usando GroupDocs.Signature for .NET. GroupDocs.Signature for .NET é uma biblioteca poderosa que permite aos desenvolvedores adicionar, remover ou verificar assinaturas digitais em vários formatos de documentos usando aplicativos .NET.
## Pré-requisitos
Antes de começarmos, certifique-se de ter os seguintes pré-requisitos:
1.  Biblioteca GroupDocs.Signature for .NET: Baixe e instale a biblioteca em[aqui](https://releases.groupdocs.com/signature/net/).
2. .NET Framework: certifique-se de ter o .NET Framework instalado em seu sistema.
3. Documento com Assinatura: Prepare um documento (por exemplo, DOCX, PDF) com uma assinatura que você deseja excluir.

## Importar namespaces
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Etapa 1: definir caminhos de arquivo
Primeiro, especifique o caminho do arquivo do documento que contém a assinatura e o caminho do arquivo de saída onde o documento modificado será salvo.
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteById", fileName);
```
## Etapa 2: copie o documento
 Desde o`Delete` método modifica o documento no local, é melhor criar uma cópia do documento original.
```csharp
File.Copy(filePath, outputFilePath, true);
```
## Etapa 3: excluir assinatura por ID
 Inicialize o`Signature` objeto com o caminho do arquivo do documento e use o`Delete` método para remover a assinatura por seu ID.
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    string id = @"eff64a14-dad9-47b0-88e5-2ee4e3604e71";
    bool result = signature.Delete(id);
    if (result)
    {
        Console.WriteLine($"Signature with Id# '{id}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with id# '{id}' was not found!");
    }
}
```

## Conclusão
Neste tutorial, aprendemos como excluir uma assinatura por seu ID usando GroupDocs.Signature for .NET. Esta biblioteca fornece uma maneira conveniente de gerenciar programaticamente assinaturas digitais em vários formatos de documentos.
## Perguntas frequentes
### Posso excluir várias assinaturas de uma vez?
 Sim, você pode excluir várias assinaturas iterando seus IDs e chamando o método`Delete` método para cada ID.
### O GroupDocs.Signature for .NET é compatível com todos os formatos de documentos?
GroupDocs.Signature for .NET oferece suporte a uma ampla variedade de formatos de documentos, incluindo PDF, DOCX, XLSX e muito mais.
### Posso personalizar a aparência da assinatura?
Sim, você pode personalizar a aparência da assinatura, incluindo posição, tamanho, fonte e cor.
### Existe uma versão de teste disponível?
 Sim, você pode baixar uma versão de avaliação gratuita em[aqui](https://releases.groupdocs.com/).
### Onde posso encontrar ajuda ou suporte para GroupDocs.Signature for .NET?
 Você pode visitar o fórum de suporte[aqui](https://forum.groupdocs.com/c/signature/13) para assistência.