---
title: Excluir assinatura do código QR do documento
linktitle: Excluir assinatura do código QR do documento
second_title: API GroupDocs.Signature .NET
description: Aprenda como excluir assinaturas de código QR de documentos usando GroupDocs.Signature for .NET. Siga nosso guia passo a passo para um gerenciamento eficiente de assinaturas.
weight: 16
url: /pt/net/delete-operations/delete-qr-code-signature/
---

# Excluir assinatura do código QR do documento

## Introdução
Neste tutorial, orientaremos você no processo de remoção de uma assinatura de código QR de um documento usando GroupDocs.Signature for .NET. Siga estas instruções passo a passo para excluir efetivamente assinaturas de código QR.
## Pré-requisitos
Antes de começar, certifique-se de ter os seguintes pré-requisitos:
-  GroupDocs.Signature para .NET: certifique-se de ter a biblioteca GroupDocs.Signature instalada em seu projeto .NET. Você pode baixá-lo em[aqui](https://releases.groupdocs.com/signature/net/).
- Documento com assinatura de código QR: Prepare um documento contendo assinaturas de código QR que você deseja excluir.
- Conhecimento básico de C#: Familiarize-se com os fundamentos da linguagem de programação C#.

## Importando Namespaces
Antes de mergulhar no código, importe os namespaces necessários para o seu arquivo C#:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Etapa 1: definir caminhos de arquivo
```csharp
// O caminho para o diretório de documentos.
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
// Defina o caminho do arquivo de saída para o documento modificado.
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);
// Copie o arquivo de origem, pois o método Delete funciona com o mesmo documento.
File.Copy(filePath, outputFilePath, true);
```
## Etapa 2: inicializar o objeto de assinatura
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Crie opções para pesquisar assinaturas de códigos QR.
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    // Procure assinaturas de código QR no documento.
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```
## Etapa 3: verifique a existência de assinatura do código QR
```csharp
    if (signatures.Count > 0)
    {
        // Obtenha a primeira assinatura de código QR encontrada no documento.
        QrCodeSignature qrCodeSignature = signatures[0];
```
## Etapa 4: excluir assinatura do código QR
```csharp
        // Exclua a assinatura do código QR do documento.
        bool result = signature.Delete(qrCodeSignature);
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```
Parabéns! Você removeu com êxito a assinatura do código QR do documento usando GroupDocs.Signature for .NET.

## Conclusão
Neste tutorial, aprendemos como excluir uma assinatura de código QR de um documento usando GroupDocs.Signature for .NET. Seguindo as etapas fornecidas, você pode gerenciar e manipular assinaturas com eficiência em seus aplicativos .NET.
## Perguntas frequentes
### Posso excluir várias assinaturas de códigos QR de um documento?
Sim, você pode modificar o código para percorrer todas as assinaturas de código QR e excluí-las adequadamente.
### O GroupDocs.Signature oferece suporte a outros tipos de assinatura além de códigos QR?
Sim, GroupDocs.Signature oferece suporte a vários tipos de assinatura, como texto, imagem, código de barras e muito mais.
### O GroupDocs.Signature é compatível com todos os formatos de documentos?
GroupDocs.Signature oferece suporte a uma ampla variedade de formatos de documentos, incluindo PDF, Microsoft Word, Excel, PowerPoint e muito mais.
### Posso personalizar as opções de pesquisa de assinaturas?
Sim, você pode personalizar as opções de pesquisa de acordo com suas necessidades para localizar assinaturas específicas no documento.
### Existe uma versão de teste disponível para GroupDocs.Signature?
 Sim, você pode acessar uma versão de avaliação gratuita do GroupDocs.Signature em[aqui](https://releases.groupdocs.com/).