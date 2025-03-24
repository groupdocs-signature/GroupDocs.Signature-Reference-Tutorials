---
title: Assinando documentos com código QR usando GroupDocs.Signature
linktitle: Assinando com QR Code
second_title: API GroupDocs.Signature .NET
description: Aprenda como adicionar assinaturas de código QR aos seus documentos com GroupDocs.Signature for .NET. Aumente a segurança e a autenticação sem esforço.
weight: 15
url: /pt/net/advanced-signature-techniques/sign-with-qr-code/
---
## Introdução
Neste tutorial, percorreremos o processo de assinatura de documentos com um código QR usando GroupDocs.Signature for .NET. GroupDocs.Signature for .NET é uma API poderosa que permite aos desenvolvedores adicionar vários tipos de assinaturas a documentos digitais de forma programática. Assinar documentos com códigos QR pode fornecer uma camada adicional de segurança e autenticação aos seus documentos.
## Pré-requisitos
Antes de começarmos, certifique-se de ter os seguintes pré-requisitos instalados:
1.  GroupDocs.Signature for .NET: você pode baixar a biblioteca do[local na rede Internet](https://releases.groupdocs.com/signature/net/).
2. Ambiente de desenvolvimento: certifique-se de ter um ambiente de desenvolvimento .NET configurado em sua máquina.
3. Documento de amostra: Prepare um documento de amostra (por exemplo, PDF) que deseja assinar com um código QR.

## Importando Namespaces Necessários
Antes de mergulhar no código, vamos importar os namespaces necessários:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Etapa 1: definir caminhos de arquivo
```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "SignWithQRCode", fileName);
```
 Certifique-se de substituir`"Your Document Directory"` com o caminho para o diretório onde deseja salvar o documento assinado.
## Etapa 2: inicializar o objeto de assinatura
```csharp
using (Signature signature = new Signature(filePath))
{
    // código para assinatura vai aqui
}
```
 Inicialize um`Signature` objeto com o caminho para o documento que você deseja assinar.
## Etapa 3: Criar QRCodeSignOptions
```csharp
QrCodeSignOptions options = new QrCodeSignOptions("JohnSmith")
{
    EncodeType = QrCodeTypes.QR,
    Left = 50,
    Top = 150,
    Width = 200,
    Height = 200
};
```
 Criar uma`QrCodeSignOptions` objeto com as configurações desejadas para a assinatura do código QR. Você pode personalizar parâmetros como texto a codificar, posição e dimensões do código QR.
## Passo 4: Assine o Documento
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
 Use o`Sign` método do`Signature` objeto para assinar o documento com as opções especificadas. Este método retorna um`SignResult` objeto contendo informações sobre o processo de assinatura.
## Etapa 5: exibir resultado
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
Exiba uma mensagem indicando o sucesso do processo de assinatura e o local onde o documento assinado foi salvo.

## Conclusão
Neste tutorial, aprendemos como assinar documentos com um código QR usando GroupDocs.Signature for .NET. Seguindo estas etapas simples, você pode adicionar assinaturas de código QR aos seus documentos digitais, aumentando a segurança e a autenticação.

## Perguntas frequentes
### Posso personalizar a aparência do código QR?
Sim, você pode personalizar vários parâmetros, como tamanho, posição e tipo de codificação do código QR, de acordo com suas necessidades.
### Quais formatos de documentos são compatíveis com assinatura com códigos QR?
GroupDocs.Signature for .NET oferece suporte a uma ampla variedade de formatos de documentos, incluindo PDF, Word, Excel, PowerPoint e muito mais.
### É possível assinar vários documentos em um processo em lote?
Com certeza, você pode usar GroupDocs.Signature for .NET para assinar vários documentos simultaneamente, agilizando seu fluxo de trabalho.
### Posso verificar a autenticidade de um documento assinado com um código QR?
Sim, o GroupDocs.Signature for .NET fornece mecanismos de verificação para garantir a integridade e autenticidade dos documentos assinados.
### Existe uma versão de teste disponível para testar a funcionalidade antes de comprar?
 Sim, você pode baixar uma versão de teste gratuita no site[local na rede Internet](https://releases.groupdocs.com/) para avaliar os recursos e capacidades do GroupDocs.Signature for .NET.