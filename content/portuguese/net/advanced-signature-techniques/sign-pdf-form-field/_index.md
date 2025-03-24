---
title: Assinando PDF com campo de formulário
linktitle: Assinando PDF com campo de formulário
second_title: API GroupDocs.Signature .NET
description: Aprenda como assinar documentos PDF com campos de formulário usando GroupDocs.Signature for .NET. Garanta a autenticidade e integridade dos documentos sem esforço.
weight: 10
url: /pt/net/advanced-signature-techniques/sign-pdf-form-field/
---

# Assinando PDF com campo de formulário

## Introdução
As assinaturas digitais fornecem uma forma segura e juridicamente vinculativa de assinar documentos eletronicamente, garantindo sua autenticidade e integridade. Neste tutorial, aprenderemos como assinar um documento PDF que contém campos de formulário usando a biblioteca GroupDocs.Signature for .NET.
## Pré-requisitos
Antes de começarmos, certifique-se de ter os seguintes pré-requisitos:
1.  Biblioteca GroupDocs.Signature for .NET: Baixe e instale a biblioteca em[aqui](https://releases.groupdocs.com/signature/net/).
2. Ambiente de desenvolvimento: configure um ambiente de desenvolvimento .NET.
3. Documento PDF: Tenha um documento PDF com campos de formulário prontos para assinatura.

## Importar namespaces
Certifique-se de importar os namespaces necessários para o seu projeto:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Passo 1: Carregue o Documento PDF
Primeiro, especifique o caminho para o seu documento PDF:
```csharp
string filePath = "sample.pdf";
```
## Etapa 2: definir o caminho de saída
Defina o caminho onde o documento assinado será salvo:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithFormField", "SignedWithFormField.pdf");
```
## Etapa 3: inicializar o objeto de assinatura
 Crie uma instância do`Signature` class e passe o caminho do arquivo PDF para ela:
```csharp
using (Signature signature = new Signature(filePath))
{
    // O código de assinatura irá aqui
}
```
## Etapa 4: instanciar assinatura do campo do formulário
A seguir, instancie uma assinatura de campo de formulário de texto com o nome e valor do campo desejado:
```csharp
FormFieldSignature textSignature = new TextFormFieldSignature("FieldText", "Value1");
```
## Etapa 5: configurar opções de assinatura
Crie opções de assinatura com base na assinatura do campo do formulário de texto. Você pode especificar a posição e o tamanho da assinatura:
```csharp
FormFieldSignOptions options = new FormFieldSignOptions(textSignature)
{
    Top = 150,
    Left = 50,
    Height = 50,
    Width = 200
};
```
## Etapa 6: Assine o Documento
Assine o documento usando as opções especificadas e salve o documento assinado no caminho de saída:
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```

## Conclusão
Neste tutorial, aprendemos como assinar um documento PDF contendo campos de formulário usando GroupDocs.Signature for .NET. As assinaturas digitais são essenciais para garantir a autenticidade e integridade dos documentos em diversos setores.
## Perguntas frequentes
### Posso assinar documentos PDF programaticamente usando GroupDocs.Signature for .NET?
Sim, você pode assinar documentos PDF programaticamente usando GroupDocs.Signature for .NET conforme demonstrado neste tutorial.
### O GroupDocs.Signature for .NET é adequado para aplicativos de nível empresarial?
Absolutamente! GroupDocs.Signature for .NET é robusto e escalonável, tornando-o adequado para aplicativos de nível empresarial.
### O GroupDocs.Signature for .NET oferece suporte a outros formatos de documento além do PDF?
Sim, GroupDocs.Signature for .NET oferece suporte a uma ampla variedade de formatos de documentos, incluindo Word, Excel, PowerPoint e muito mais.
### Posso personalizar a aparência da assinatura?
Sim, você pode personalizar a aparência da assinatura ajustando vários parâmetros como cor, fonte, tamanho e posição.
### Existe uma versão de teste disponível para GroupDocs.Signature for .NET?
 Sim, você pode baixar uma versão de avaliação gratuita do GroupDocs.Signature for .NET em[aqui](https://releases.groupdocs.com/).