---
title: Verifique o código QR
linktitle: Verifique o código QR
second_title: API GroupDocs.Signature .NET
description: Aprenda como verificar códigos QR em documentos usando GroupDocs.Signature for .NET. Tutorial abrangente com guia passo a passo.
weight: 12
url: /pt/net/verify-operations/verify-qr-code/
---
## Introdução
No domínio do gerenciamento e autenticação de documentos, garantir a integridade e a validade das assinaturas é fundamental. GroupDocs.Signature for .NET fornece uma solução abrangente para verificar códigos QR incorporados em documentos. Neste tutorial, nos aprofundaremos no processo passo a passo de verificação de códigos QR usando GroupDocs.Signature for .NET.
## Pré-requisitos
Antes de mergulhar no processo de verificação, certifique-se de ter os seguintes pré-requisitos em vigor:
1.  Instalação do GroupDocs.Signature for .NET: Baixe e instale o GroupDocs.Signature for .NET a partir do[Link para Download](https://releases.groupdocs.com/signature/net/).
2. Acesso a um documento contendo códigos QR: Prepare um documento de amostra que contenha códigos QR para verificação. 

## Importar namespaces
Primeiramente, você precisa importar os namespaces necessários para utilizar as funcionalidades fornecidas pelo GroupDocs.Signature for .NET. Siga esses passos:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```


Agora, vamos detalhar o processo de verificação de códigos QR incorporados em um documento usando GroupDocs.Signature for .NET:
## Etapa 1: especificar o caminho do documento
```csharp
string filePath = "sample_multiple_signatures.docx";
```
 Certifique-se de substituir`"sample_multiple_signatures.docx"` com o caminho para o seu documento.
## Etapa 2: inicializar o objeto de assinatura
```csharp
using (Signature signature = new Signature(filePath))
{
    // código de verificação vai aqui
}
```
 Inicialize um`Signature` objeto, fornecendo o caminho para o documento.
## Etapa 3: especifique as opções de verificação
```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // este valor é definido por padrão
    Text = "John",
    MatchType = TextMatchType.Contains
};
```
 Defina opções de verificação, como`AllPages` para verificar todas as páginas,`Text` para especificar o texto a ser correspondido no código QR e`MatchType` para definir os critérios de correspondência.
## Etapa 4: verificar as assinaturas dos documentos
```csharp
VerificationResult result = signature.Verify(options);
```
 Invoque o`Verify` método do`Signature` objeto, passando as opções de verificação.
## Etapa 5: lidar com os resultados da verificação
```csharp
if (result.IsValid)
{
    // Assinatura válida encontrada
}
else
{
    // Assinatura inválida encontrada
}
```
Com base no resultado da verificação, trate os cenários de sucesso ou falha adequadamente.

## Conclusão
Neste tutorial, exploramos o processo de verificação de códigos QR em documentos usando GroupDocs.Signature for .NET. Seguindo essas etapas, você pode integrar perfeitamente a funcionalidade de verificação de código QR em seus aplicativos .NET, garantindo a integridade e autenticidade dos documentos.
## Perguntas frequentes
### O GroupDocs.Signature for .NET pode verificar códigos QR em diferentes formatos de documentos?
Sim, GroupDocs.Signature for .NET oferece suporte a uma ampla variedade de formatos de documentos, incluindo DOCX, PDF e muito mais para verificação de código QR.
### Existe uma avaliação gratuita disponível para GroupDocs.Signature for .NET?
 Sim, você pode aproveitar um teste gratuito no site[página de lançamentos](https://releases.groupdocs.com/).
### Quais opções de suporte estão disponíveis para usuários do GroupDocs.Signature for .NET?
 Os usuários podem acessar o suporte através do[fórum](https://forum.groupdocs.com/c/signature/13) para GroupDocs.Signature.
### Posso adquirir uma licença temporária do GroupDocs.Signature for .NET?
 Sim, licenças temporárias estão disponíveis para compra no[Página de compra do GroupDocs](https://purchase.groupdocs.com/temporary-license/).
### Existe documentação extensa disponível para GroupDocs.Signature for .NET?
 Com certeza, você pode consultar a documentação detalhada fornecida[aqui](https://tutorials.groupdocs.com/signature/net/) para obter orientação abrangente sobre a utilização das funcionalidades do GroupDocs.Signature for .NET.