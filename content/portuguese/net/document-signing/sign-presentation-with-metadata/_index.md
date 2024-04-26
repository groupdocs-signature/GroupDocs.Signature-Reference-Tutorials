---
title: Apresentação de assinatura com metadados
linktitle: Apresentação de assinatura com metadados
second_title: API GroupDocs.Signature .NET
description: Aprenda como assinar arquivos de apresentação com metadados usando GroupDocs.Signature for .NET. Melhore a integridade dos documentos e adicione informações valiosas.
type: docs
weight: 12
url: /pt/net/document-signing/sign-presentation-with-metadata/
---
## Introdução
Neste tutorial, aprenderemos como assinar um arquivo de apresentação (PPTX) com metadados usando a biblioteca GroupDocs.Signature for .NET. Assinar apresentações com metadados adiciona informações valiosas ao documento, como nome do autor, data de criação, ID do documento, ID da assinatura e vários valores numéricos.
## Pré-requisitos
Antes de começarmos, certifique-se de ter o seguinte:
1.  Biblioteca GroupDocs.Signature for .NET: Baixe e instale a biblioteca em[aqui](https://releases.groupdocs.com/signature/net/).
2. Ambiente de desenvolvimento: certifique-se de ter um ambiente de desenvolvimento .NET configurado.
3. Arquivo de apresentação: Tenha um arquivo de apresentação de amostra (formato PPTX) pronto para assinatura.
4. Compreensão básica de C#: A familiaridade com a linguagem de programação C# será benéfica.

## Importar namespaces
Antes de mergulhar no código, vamos importar os namespaces necessários:
```csharp
using System;
using System.IO;
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;
    using GroupDocs.Signature.Options;
```
## Etapa 1: carregar arquivo de apresentação
```csharp
string filePath = "sample.pptx";
```
 Substituir`"sample.pptx"` com o caminho para o seu arquivo de apresentação.
## Etapa 2: especificar o caminho do arquivo de saída
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPresentationWithMetadata", "SignedWithMetadata.pptx");
```
Especifique o diretório onde deseja salvar o arquivo de apresentação assinado junto com o nome do arquivo.
## Etapa 3: inicializar o objeto de assinatura
```csharp
using (Signature signature = new Signature(filePath))
```
Inicialize um objeto Signature fornecendo o caminho para o arquivo de apresentação.
## Etapa 4: definir opções de sinalização de metadados
```csharp
MetadataSignOptions options = new MetadataSignOptions();
```
Crie uma instância de MetadataSignOptions para definir opções de assinatura de metadados.
## Etapa 5: criar assinaturas de metadados
```csharp
PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Author", "Mr.Scherlock Holmes"),
    new PresentationMetadataSignature("CreatedOn", DateTime.Now),
    new PresentationMetadataSignature("DocumentId", 123456),
    new PresentationMetadataSignature("SignatureId", 123.456D),
    new PresentationMetadataSignature("Amount", 123.456M),
    new PresentationMetadataSignature("Total", 123.456F)
};
```
Crie uma matriz de objetos PresentationMetadataSignature, cada um representando uma assinatura de metadados. Você pode adicionar vários tipos de metadados, incluindo string, DateTime, inteiro, duplo, decimal e flutuante.
## Etapa 6: adicionar assinaturas às opções
```csharp
options.Signatures.AddRange(signatures);
```
Adicione as assinaturas de metadados criadas ao objeto MetadataSignOptions.
## Etapa 7: assinar o documento
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
Assine o arquivo de apresentação com metadados usando as opções especificadas e salve o arquivo assinado no caminho de saída.
## Etapa 8: exibir resultado
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
Exiba uma mensagem de sucesso junto com o número de assinaturas aplicadas e o caminho onde o arquivo assinado foi salvo.

## Conclusão
Neste tutorial, aprendemos como assinar um arquivo de apresentação com metadados usando a biblioteca GroupDocs.Signature for .NET. A adição de assinaturas de metadados melhora a integridade do documento e fornece informações valiosas sobre seu conteúdo.

## Perguntas frequentes
### Posso assinar outros formatos de documento além do PPTX com metadados usando GroupDocs.Signature for .NET?
Sim, GroupDocs.Signature oferece suporte a vários formatos de documento, incluindo Word, Excel, PDF e muito mais, para assinatura com metadados.
### O GroupDocs.Signature for .NET é compatível com o .NET Core?
Sim, a biblioteca é compatível com .NET Framework e .NET Core.
### Posso personalizar a aparência das assinaturas de metadados?
Sim, você pode personalizar a aparência, a posição e outras propriedades das assinaturas de metadados de acordo com suas necessidades.
### O GroupDocs.Signature for .NET fornece criptografia para documentos assinados?
Sim, GroupDocs.Signature oferece opções de criptografia para proteger documentos assinados contra acesso não autorizado.
### Existe uma versão de teste disponível para teste antes de comprar?
 Sim, você pode aproveitar uma avaliação gratuita do GroupDocs.Signature for .NET em[aqui](https://releases.groupdocs.com/).