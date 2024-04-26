---
title: Assinando com Stamp usando GroupDocs.Signature
linktitle: Assinando com Carimbo
second_title: API GroupDocs.Signature .NET
description: Aprenda como adicionar assinaturas de carimbo aos seus documentos .NET facilmente com GroupDocs.Signature for .NET. Aumente a segurança dos documentos.
type: docs
weight: 16
url: /pt/net/advanced-signature-techniques/sign-with-stamp/
---
## Introdução
Neste tutorial, orientaremos você no processo de assinatura de um documento com carimbo usando GroupDocs.Signature for .NET. Seguindo estas instruções passo a passo, você poderá adicionar uma assinatura de carimbo aos seus documentos com facilidade.
## Pré-requisitos
Antes de começarmos, certifique-se de ter os seguintes pré-requisitos:
1.  GroupDocs.Signature for .NET SDK: Baixe e instale o SDK do[local na rede Internet](https://releases.groupdocs.com/signature/net/).
2. Ambiente de desenvolvimento: certifique-se de ter um ambiente de desenvolvimento adequado configurado para desenvolvimento .NET.
3. Documento para assinar: Prepare o documento (por exemplo, PDF) que deseja assinar com carimbo.

## Importando Namespaces
Comece importando os namespaces necessários para o seu projeto:
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Etapa 1: carregue o documento
```csharp
string filePath = "sample.pdf";
using (Signature signature = new Signature(filePath))
{
    // Seu código vai aqui
}
```
## Etapa 2: definir opções de sinal de carimbo
```csharp
StampSignOptions options = new StampSignOptions()
{
    Left = 50,
    Top = 150,                    
    Width = 200,
    Height = 200
};
```
## Etapa 3: configurar a aparência do carimbo
```csharp
StampLine outerLine = new StampLine();
outerLine.Text = " * European Union ";
outerLine.TextRepeatType = StampTextRepeatType.FullTextRepeat;
outerLine.Font.Size = 12;
outerLine.Height = 22;
outerLine.TextBottomIntent = 6;
outerLine.TextColor = Color.WhiteSmoke;
outerLine.BackgroundColor = Color.DarkSlateBlue;
options.OuterLines.Add(outerLine);
StampLine innerLine = new StampLine();
innerLine.Text = "John Smith";
innerLine.TextColor = Color.MediumVioletRed;
innerLine.Font.Size = 20;
innerLine.Font.Bold = true;
innerLine.Height = 40;
options.InnerLines.Add(innerLine);
```
## Passo 4: Assine o Documento
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithStamp", fileName);
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Conclusão
Adicionar assinaturas de carimbo aos seus documentos usando GroupDocs.Signature for .NET é um processo simples, conforme demonstrado neste tutorial. Com as etapas fornecidas, você pode aumentar facilmente a segurança e a autenticidade de seus documentos.
## Perguntas frequentes
### Posso personalizar a aparência da assinatura do carimbo?
Sim, você pode personalizar vários aspectos como texto, fonte, cor e posicionamento da assinatura do carimbo de acordo com suas necessidades.
### O GroupDocs.Signature oferece suporte à assinatura de vários formatos de documentos?
Sim, GroupDocs.Signature oferece suporte a uma ampla variedade de formatos de documentos, incluindo PDF, Microsoft Word, Excel, PowerPoint e muito mais.
### Existe uma versão de teste disponível para GroupDocs.Signature?
 Sim, você pode acessar a versão de avaliação gratuita no[local na rede Internet](https://releases.groupdocs.com/).
### Posso adicionar várias assinaturas a um único documento?
Com certeza, GroupDocs.Signature permite adicionar várias assinaturas, incluindo carimbos, texto, imagens e assinaturas digitais, a um único documento.
### Onde posso encontrar suporte se encontrar algum problema durante a implementação?
 Você pode encontrar suporte e assistência no fórum da comunidade GroupDocs.Signature[aqui](https://forum.groupdocs.com/c/signature/13).