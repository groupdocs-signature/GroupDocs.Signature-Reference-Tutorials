---
title: Assinando com texto usando GroupDocs.Signature for .NET
linktitle: Assinando com Texto
second_title: API GroupDocs.Signature .NET
description: Aprenda como assinar documentos com texto usando GroupDocs.Signature for .NET. Guia passo a passo para adicionar assinaturas de texto programaticamente.
weight: 17
url: /pt/net/advanced-signature-techniques/sign-with-text/
---
## Introdução
Na era digital, assinar documentos eletronicamente tornou-se uma prática padrão, economizando tempo e recursos. GroupDocs.Signature for .NET oferece uma solução abrangente para adicionar assinaturas de texto a vários formatos de documentos de forma programática. Neste tutorial, orientaremos você no processo de assinatura de um documento com texto usando GroupDocs.Signature for .NET.
## Pré-requisitos
Antes de mergulharmos no tutorial, certifique-se de ter os seguintes pré-requisitos:
1.  GroupDocs.Signature for .NET: certifique-se de ter a biblioteca GroupDocs.Signature for .NET instalada. Você pode baixá-lo em[aqui](https://releases.groupdocs.com/signature/net/).
2. Ambiente de Desenvolvimento: Tenha um ambiente de trabalho configurado para desenvolvimento .NET.
3. Documento: Prepare o documento (por exemplo, PDF, Word) que deseja assinar com texto.

## Importar namespaces
Primeiro, você precisa importar os namespaces necessários para o seu projeto .NET para usar as funcionalidades do GroupDocs.Signature.
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Vamos dividir o processo de assinatura de um documento com texto em várias etapas:
## Etapa 1: carregar o documento
Carregue o documento que deseja assinar com texto.
```csharp
string filePath = "sample.pdf"; // Caminho para o documento
string fileName = Path.GetFileName(filePath);
```
## Etapa 2: definir o caminho do arquivo de saída
Defina o caminho do arquivo de saída onde o documento assinado será salvo.
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithText", fileName);
```
## Etapa 3: criar opções de assinatura
Configure as opções de assinatura de texto, incluindo conteúdo, posição, tamanho, cor e fonte do texto.
```csharp
TextSignOptions options = new TextSignOptions("John Smith")
{
    Left = 50, // Definir posição da assinatura
    Top = 200,
    Width = 100, // Definir retângulo de assinatura
    Height = 30,
    ForeColor = Color.Red, // Definir cor do texto
    Font = new SignatureFont { Size = 14, FamilyName = "Comic Sans MS" } // Definir fonte
};
```
## Etapa 4: assinar o documento
Use GroupDocs.Signature para assinar o documento com as opções especificadas e salvar o documento assinado no caminho do arquivo de saída.
```csharp
using (Signature signature = new Signature(filePath))
{
    SignResult result = signature.Sign(outputFilePath, options); // Assinar documento
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Conclusão
Neste tutorial, aprendemos como assinar um documento com texto usando GroupDocs.Signature for .NET. Seguindo essas etapas, você pode adicionar assinaturas de texto aos seus documentos de maneira eficiente e programática, aumentando a segurança e a autenticidade.
## Perguntas frequentes
### Posso personalizar a aparência da assinatura do texto?
Sim, você pode personalizar vários parâmetros como cor, fonte, tamanho e posição da assinatura do texto de acordo com suas preferências.
### O GroupDocs.Signature é compatível com vários formatos de documentos?
Sim, GroupDocs.Signature oferece suporte a vários formatos de documentos, incluindo PDF, Word, Excel, PowerPoint e muito mais.
### Posso adicionar várias assinaturas de texto a um único documento?
Com certeza, você pode adicionar várias assinaturas de texto a um documento, cada uma com seu próprio conjunto de opções de personalização.
### O GroupDocs.Signature garante a integridade do documento após a assinatura?
Sim, GroupDocs.Signature emprega algoritmos criptográficos robustos para garantir a integridade do documento e evitar adulterações após a assinatura.
### Existe uma versão de teste disponível para teste antes de comprar?
 Sim, você pode baixar uma versão de avaliação gratuita em[aqui](https://releases.groupdocs.com/) para explorar os recursos antes de fazer uma compra.