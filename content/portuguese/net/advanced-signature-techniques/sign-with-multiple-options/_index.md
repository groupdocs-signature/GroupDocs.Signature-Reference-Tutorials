---
title: Assinando com múltiplas opções
linktitle: Assinando com múltiplas opções
second_title: API GroupDocs.Signature .NET
description: Aprenda como assinar documentos com múltiplas opções usando GroupDocs.Signature for .NET. Aumente a segurança dos documentos com texto, código de barras, código QR, digital e imagem.
weight: 14
url: /pt/net/advanced-signature-techniques/sign-with-multiple-options/
---

# Assinando com múltiplas opções

## Introdução
Neste tutorial, exploraremos como assinar um documento usando várias opções de assinatura usando a biblioteca GroupDocs.Signature para .NET. Assinar documentos com várias opções, como texto, código de barras, código QR, assinatura digital, imagem e metadados, pode fornecer versatilidade e aumentar a segurança dos documentos.
## Pré-requisitos
Antes de começar, certifique-se de ter os seguintes pré-requisitos:
1.  Biblioteca GroupDocs.Signature for .NET: Baixe e instale a biblioteca GroupDocs.Signature for .NET em[aqui](https://releases.groupdocs.com/signature/net/).
2. Ambiente de Desenvolvimento: Configure um ambiente de desenvolvimento com o .NET Framework instalado.
3. Documento para assinar: Prepare o documento (por exemplo, sample.docx) que deseja assinar.
4. Certificados e imagens: Prepare quaisquer certificados e imagens necessários para assinaturas digitais e de imagem.

## Importar namespaces
Primeiro, importe os namespaces necessários para usar a biblioteca GroupDocs.Signature em seu aplicativo .NET:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Etapa 1: carregue o documento
```csharp
string filePath = "sample.docx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithMultiple", "SignWithMultiple.docx");
using (Signature signature = new Signature(filePath))
{
    // Seu código continua...
}
```
## Etapa 2: definir opções de assinatura
Defina diversas opções de assinatura de diferentes tipos e configurações, como texto, código de barras, código QR, digital, imagem e assinaturas de metadados:
```csharp
TextSignOptions textOptions = new TextSignOptions("Text signature")
{
    VerticalAlignment = VerticalAlignment.Top,
    HorizontalAlignment = HorizontalAlignment.Left
};
BarcodeSignOptions barcodeOptions = new BarcodeSignOptions("123456")
{
    EncodeType = BarcodeTypes.Code128,
    Left = 0,
    Top = 150,
    Height = 50,
    Width = 200
};
// Defina outras opções de assinatura (ex.: código QR, digital, imagem, metadados)...
```
## Etapa 3: crie uma lista de opções de assinatura
Defina uma lista de opções de assinatura contendo todas as opções definidas anteriormente:
```csharp
List<SignOptions> listOptions = new List<SignOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
// Adicione outras opções de assinatura à lista...
```
## Passo 4: Assine o Documento
Assine o documento com a lista de opções de assinatura e salve o documento assinado:
```csharp
SignResult result = signature.Sign(outputFilePath, listOptions);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Conclusão
Assinar documentos com múltiplas opções usando GroupDocs.Signature for .NET fornece uma solução robusta para aprimorar a segurança e versatilidade de documentos. Seguindo as etapas descritas neste tutorial, você pode integrar perfeitamente vários tipos de assinatura em seus aplicativos .NET.
## Perguntas frequentes
### Posso usar imagens personalizadas para assinaturas digitais?
Sim, você pode especificar imagens personalizadas para assinaturas digitais usando a biblioteca GroupDocs.Signature.
### O GroupDocs.Signature é compatível com diferentes formatos de documentos?
Sim, GroupDocs.Signature oferece suporte a vários formatos de documento, incluindo DOCX, PDF, PPTX e muito mais.
### Posso personalizar a aparência das assinaturas de texto?
Com certeza, você pode personalizar a aparência das assinaturas de texto, incluindo tamanho, cor e estilo da fonte.
### O GroupDocs.Signature fornece criptografia para assinaturas digitais?
Sim, GroupDocs.Signature oferece opções de criptografia para assinaturas digitais para garantir a segurança dos documentos.
### Existe uma versão de teste disponível para GroupDocs.Signature for .NET?
 Sim, você pode baixar uma versão de avaliação gratuita do GroupDocs.Signature for .NET em[aqui](https://releases.groupdocs.com/).