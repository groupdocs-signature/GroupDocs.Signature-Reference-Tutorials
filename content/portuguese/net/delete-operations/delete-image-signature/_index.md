---
title: Excluir assinatura de imagem
linktitle: Excluir assinatura de imagem
second_title: API GroupDocs.Signature .NET
description: Aprenda como excluir assinaturas de imagens de documentos usando GroupDocs.Signature for .NET. Siga nosso guia passo a passo para um gerenciamento eficiente de assinaturas.
type: docs
weight: 14
url: /pt/net/delete-operations/delete-image-signature/
---
## Introdução
Neste tutorial, exploraremos como excluir assinaturas de imagens de documentos usando GroupDocs.Signature for .NET. GroupDocs.Signature é uma biblioteca poderosa que permite aos desenvolvedores trabalhar com assinaturas digitais, carimbos e campos de formulário em vários formatos de documentos.
## Pré-requisitos
Antes de começarmos, certifique-se de ter o seguinte:
### 1. GroupDocs.Signature para .NET
 Baixe e instale GroupDocs.Signature for .NET do[local na rede Internet](https://releases.groupdocs.com/signature/net/). Siga as instruções de instalação fornecidas na documentação.
### 2. Estrutura .NET
Certifique-se de ter o .NET Framework instalado em sua máquina.
## Importar namespaces
Inclua os namespaces necessários em seu projeto:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
Vamos dividir o processo de exclusão de assinaturas de imagens em várias etapas:
## Etapa 1: definir caminhos de arquivo
Primeiro, especifique os caminhos para o documento de entrada e o documento de saída após excluir a assinatura:
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteImage", fileName);
```
## Etapa 2: copie o arquivo de origem
 Desde o`Delete`método funciona com o mesmo documento, é essencial copiar o arquivo fonte para outro local:
```csharp
File.Copy(filePath, outputFilePath, true);
```
## Etapa 3: inicializar o objeto de assinatura
 Crie uma instância do`Signature` class e especifique o caminho para o documento de saída:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // O código vai aqui
}
```
## Etapa 4: pesquise assinaturas de imagens
Defina opções de pesquisa e procure assinaturas de imagens no documento:
```csharp
ImageSearchOptions options = new ImageSearchOptions();
List<ImageSignature> signatures = signature.Search<ImageSignature>(options);
```
## Etapa 5: excluir assinatura da imagem
Se forem encontradas assinaturas de imagens, exclua a primeira:
```csharp
if (signatures.Count > 0)
{
    ImageSignature imageSignature = signatures[0];
    bool result = signature.Delete(imageSignature);
    if (result)
    {
        Console.WriteLine($"Image signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was not found!");
    }
}
```
## Conclusão
Neste tutorial, aprendemos como excluir assinaturas de imagens de documentos usando GroupDocs.Signature for .NET. Seguindo o guia passo a passo, os desenvolvedores podem gerenciar com eficiência as assinaturas digitais em seus aplicativos.
## Perguntas frequentes
### Posso excluir várias assinaturas de imagens de um documento?
 Sim, você pode modificar o código para excluir várias assinaturas de imagem iterando sobre o`signatures` lista.
### O GroupDocs.Signature oferece suporte a outros formatos de documento além de DOCX?
Sim, GroupDocs.Signature oferece suporte a uma ampla variedade de formatos de documentos, incluindo PDF, PPT, XLS e muito mais.
### Existe uma versão de teste disponível para GroupDocs.Signature for .NET?
 Sim, você pode baixar uma versão de teste gratuita no site[local na rede Internet](https://releases.groupdocs.com/).
### Como posso obter suporte para GroupDocs.Signature?
 Você pode visitar o[Fórum GroupDocs.Signature](https://forum.groupdocs.com/c/signature/13) para assistência e apoio.
### Posso comprar uma licença temporária para GroupDocs.Signature?
 Sim, você pode comprar uma licença temporária no[página de compra](https://purchase.groupdocs.com/temporary-license/).