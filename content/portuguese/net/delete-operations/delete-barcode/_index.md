---
title: Excluir código de barras do documento
linktitle: Excluir código de barras do documento
second_title: API GroupDocs.Signature .NET
description: Aprenda como excluir código de barras de um documento usando GroupDocs.Signature for .NET. Guia passo a passo com exemplos de código.
weight: 10
url: /pt/net/delete-operations/delete-barcode/
---
## Introdução
GroupDocs.Signature for .NET é uma biblioteca poderosa que permite aos desenvolvedores trabalhar perfeitamente com assinaturas digitais, carimbos e códigos de barras em aplicativos .NET. Neste tutorial, orientaremos você no processo de exclusão de um código de barras de um documento usando GroupDocs.Signature for .NET.
## Pré-requisitos
Antes de começarmos, certifique-se de ter os seguintes pré-requisitos:
- Conhecimento básico da linguagem de programação C#.
- Visual Studio instalado em seu sistema.
-  Biblioteca GroupDocs.Signature para .NET instalada. Você pode baixá-lo em[aqui](https://releases.groupdocs.com/signature/net/).
- Um documento de amostra com um código de barras que você deseja excluir.

## Importar namespaces
Primeiro, certifique-se de importar os namespaces necessários para o seu código C#:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Vamos dividir o processo de exclusão de um código de barras de um documento em etapas simples:
## Etapa 1: definir caminhos de arquivo
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteBarcode", fileName);
```
 Certifique-se de substituir`"sample_multiple_signatures.docx"` com o caminho para o documento que contém o código de barras.
## Etapa 2: copie o arquivo de origem
```csharp
File.Copy(filePath, outputFilePath, true);
```
Esta etapa garante que estamos trabalhando com uma cópia do documento original para preservar o arquivo original.
## Etapa 3: inicializar GroupDocs.Signature
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Seu código vai aqui
}
```
Inicialize o objeto Signature passando o caminho para a cópia do documento criada no passo anterior.
## Etapa 4: pesquise assinaturas de código de barras
```csharp
BarcodeSearchOptions options = new BarcodeSearchOptions();
List<BarcodeSignature> signatures = signature.Search<BarcodeSignature>(options);
```
Crie uma instância de BarcodeSearchOptions e use-a para pesquisar assinaturas de código de barras no documento.
## Etapa 5: excluir assinatura do código de barras
```csharp
if (signatures.Count > 0)
{
    BarcodeSignature barcodeSignature = signatures[0];
    bool result = signature.Delete(barcodeSignature);
    if (result)
    {
        Console.WriteLine($"Signature with Barcode '{barcodeSignature.Text}' and encode type '{barcodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{barcodeSignature.Text}' and encode type '{barcodeSignature.EncodeType.TypeName}' was not found!");
    }
}
```
Verifique se assinaturas de código de barras são encontradas no documento. Se encontrada, exclua a primeira assinatura de código de barras encontrada.

## Conclusão
Neste tutorial, aprendemos como excluir um código de barras de um documento usando GroupDocs.Signature for .NET. Seguindo o guia passo a passo, você pode integrar perfeitamente a funcionalidade de exclusão de código de barras em seus aplicativos .NET.
## Perguntas frequentes
### Posso excluir várias assinaturas de códigos de barras de um documento?
Sim, você pode modificar o código para excluir várias assinaturas de código de barras iterando a lista de assinaturas.
### O GroupDocs.Signature for .NET oferece suporte a outros tipos de assinaturas?
Sim, GroupDocs.Signature for .NET oferece suporte a vários tipos de assinaturas, incluindo assinaturas digitais, carimbos e assinaturas de texto.
### Posso personalizar as opções de pesquisa de assinaturas de código de barras?
Sim, você pode personalizar as opções de pesquisa de acordo com suas necessidades, como especificar tipos de códigos de barras ou áreas de pesquisa no documento.
### O GroupDocs.Signature for .NET é compatível com diferentes formatos de documentos?
Sim, GroupDocs.Signature for .NET oferece suporte a uma ampla variedade de formatos de documentos, incluindo Word, Excel, PDF e muito mais.
### Onde posso encontrar suporte ou recursos adicionais para GroupDocs.Signature for .NET?
 Você pode visitar o fórum GroupDocs.Signature[aqui](https://forum.groupdocs.com/c/signature/13) para qualquer dúvida ou assistência em relação à biblioteca.