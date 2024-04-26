---
title: Excluir múltiplas assinaturas do documento
linktitle: Excluir múltiplas assinaturas do documento
second_title: API GroupDocs.Signature .NET
description: Exclua facilmente várias assinaturas de documentos usando GroupDocs.Signature for .NET. Simplifique seu fluxo de trabalho de gerenciamento de documentos.
type: docs
weight: 15
url: /pt/net/delete-operations/delete-multiple-signatures/
---
## Introdução
No mundo digital, a gestão de documentos envolve frequentemente o tratamento de várias assinaturas. Excluir várias assinaturas de um documento de forma programática pode agilizar os fluxos de trabalho e aumentar a eficiência. Com GroupDocs.Signature for .NET, essa tarefa se torna simples e direta. Este tutorial irá guiá-lo passo a passo pelo processo de exclusão de múltiplas assinaturas de um documento.
## Pré-requisitos
Antes de mergulhar no tutorial, certifique-se de ter os seguintes pré-requisitos:
- Compreensão básica da linguagem de programação C#.
- Biblioteca GroupDocs.Signature for .NET instalada.
- Exemplo de documento com múltiplas assinaturas para teste.

## Importar namespaces
Comece importando os namespaces necessários para acessar a funcionalidade do GroupDocs.Signature for .NET:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Etapa 1: definir o caminho do documento e o nome do arquivo
Defina o caminho do arquivo do documento que contém múltiplas assinaturas. Certifique-se de ter o caminho e o nome de arquivo apropriados:
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
```
## Etapa 2: copie o documento para processamento
Para evitar modificar o documento original, crie uma cópia para processamento:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "DeleteMultiple", fileName);
File.Copy(filePath, outputFilePath, true);
```
## Etapa 3: inicializar o objeto de assinatura
Instancie um objeto Signature usando o caminho do arquivo de saída:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // O código de processamento de assinatura vai aqui
}
```
## Etapa 4: definir opções de pesquisa
Defina várias opções de pesquisa para identificar assinaturas no documento. As opções incluem pesquisa de texto, pesquisa de imagens, pesquisa de código de barras e pesquisa de código QR:
```csharp
TextSearchOptions textSearchOptions = new TextSearchOptions();
ImageSearchOptions imageSearchOptions = new ImageSearchOptions();
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions();
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions();
// Adicionar opções à lista
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textSearchOptions);
listOptions.Add(imageSearchOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
```
## Etapa 5: procure por assinaturas
Execute uma operação de pesquisa para encontrar todas as assinaturas no documento com base nas opções de pesquisa definidas:
```csharp
SearchResult result = signature.Search(listOptions);
```
## Etapa 6: excluir assinaturas
Se forem encontradas assinaturas, prossiga para excluí-las:
```csharp
if (result.Signatures.Count > 0)
{
    // Tente excluir todas as assinaturas
    DeleteResult deleteResult = signature.Delete(result.Signatures);
    //Verifique se a exclusão foi bem-sucedida
    if(deleteResult.Succeeded.Count == result.Signatures.Count)
    {
        Console.WriteLine("\nAll signatures were successfully deleted!");                        
    }
    else
    {
        Console.WriteLine($"Successfully deleted signatures : {deleteResult.Succeeded.Count}");
        Helper.WriteError($"Not deleted signatures : {deleteResult.Failed.Count}");
    }
    // Exibir informações sobre assinaturas excluídas
    Console.WriteLine("\nList of deleted signatures:");
    int number = 1;
    foreach(BaseSignature temp in deleteResult.Succeeded)
    {
        Console.WriteLine($"Signature #{number++}: Type: {temp.SignatureType} Id:{temp.SignatureId}, Location: {temp.Left}x{temp.Top}. Size: {temp.Width}x{temp.Height}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## Conclusão
Excluir múltiplas assinaturas de um documento de forma programática é uma tarefa crucial no gerenciamento de documentos. Com GroupDocs.Signature for .NET, esse processo se torna eficiente e confiável. Seguindo as etapas descritas neste tutorial, você pode integrar facilmente a funcionalidade de exclusão de assinatura em seus aplicativos .NET.
## Perguntas frequentes
### O GroupDocs.Signature for .NET pode lidar com vários formatos de documentos?
Sim, GroupDocs.Signature for .NET oferece suporte a uma ampla variedade de formatos de documentos, incluindo DOCX, PDF, PPTX, XLSX e muito mais.
### É possível personalizar as opções de pesquisa para detecção de assinaturas?
Com certeza, você pode personalizar opções de pesquisa, como pesquisa de texto, pesquisa de imagens, pesquisa de código de barras e pesquisa de código QR para atender às suas necessidades específicas.
### O GroupDocs.Signature for .NET fornece mecanismos de tratamento de erros?
Sim, a biblioteca oferece recursos robustos de tratamento de erros para garantir a execução tranquila das tarefas de processamento de documentos.
### Posso integrar GroupDocs.Signature for .NET com outras bibliotecas de terceiros?
Certamente, GroupDocs.Signature for .NET foi projetado para integração perfeita com outras bibliotecas .NET, proporcionando flexibilidade e extensibilidade.
### Onde posso encontrar suporte e recursos adicionais para GroupDocs.Signature for .NET?
 Você pode visitar o GroupDocs[fórum](https://forum.groupdocs.com/c/signature/13) dedicado a discussões relacionadas a assinaturas e busca assistência da comunidade e de especialistas.