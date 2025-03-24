---
title: Excluir assinatura digital do documento
linktitle: Excluir assinatura digital do documento
second_title: API GroupDocs.Signature .NET
description: Aprenda como excluir assinaturas digitais de documentos usando GroupDocs.Signature for .NET. Siga nosso guia passo a passo para um gerenciamento eficiente.
weight: 13
url: /pt/net/delete-operations/delete-digital-signature/
---
## Introdução
No mundo dos documentos digitais, garantir autenticidade e segurança é fundamental. As assinaturas digitais desempenham um papel crucial na verificação da integridade dos documentos eletrônicos. GroupDocs.Signature for .NET oferece ferramentas poderosas para gerenciar assinaturas digitais em aplicativos .NET com eficiência.
## Pré-requisitos
Antes de começar a usar GroupDocs.Signature for .NET para excluir assinaturas digitais de documentos, certifique-se de ter o seguinte:
1. Visual Studio: instale o IDE do Visual Studio em seu sistema.
2.  GroupDocs.Signature for .NET: Baixe e instale GroupDocs.Signature for .NET a partir do[página de download](https://releases.groupdocs.com/signature/net/).
3. Documento de amostra: Prepare um documento de amostra contendo assinaturas digitais para teste.

## Importar namespaces
Para começar, certifique-se de importar os namespaces necessários em seu projeto .NET:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```
## Etapa 1: definir caminhos de arquivo
Comece definindo os caminhos de arquivo para o documento de origem e o documento de saída:
```csharp
string filePath = "sample.pdf"_SIGNED_DIGITAL;
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteDigital", fileName);
```
## Etapa 2: copie o documento de origem
 Desde o`Delete` método funciona com o mesmo documento, é necessário copiar o arquivo fonte para um novo local:
```csharp
File.Copy(filePath, outputFilePath, true);
```
## Etapa 3: inicializar o objeto de assinatura
 Inicialize um`Signature` objeto com o caminho do arquivo de saída:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Seu código vai aqui
}
```
## Passo 4: Procure Assinaturas Digitais
Pesquise assinaturas digitais eletrônicas no documento:
```csharp
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```
## Etapa 5: excluir assinatura digital
Se forem encontradas assinaturas digitais, exclua a primeira assinatura encontrada:
```csharp
if (signatures.Count > 0)
{
    DigitalSignature digitalSignature = signatures[0];
    bool result = signature.Delete(digitalSignature);
    if (result)
    {
        Console.WriteLine($"Digital signature #{digitalSignature.Thumbprint} from {digitalSignature.SignTime.ToShortDateString()} was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature# {digitalSignature.Thumbprint} was not found!");
    }
}
```

## Conclusão
O gerenciamento de assinaturas digitais em aplicativos .NET torna-se fácil com GroupDocs.Signature. Seguindo as etapas simples descritas acima, você pode excluir perfeitamente assinaturas digitais de seus documentos, garantindo a integridade e segurança dos dados.
## Perguntas frequentes
### Posso excluir várias assinaturas digitais de um único documento?
Sim, você pode modificar o código para percorrer todas as assinaturas digitais encontradas e excluí-las adequadamente.
### O GroupDocs.Signature oferece suporte a outros tipos de assinatura além da digital?
Sim, GroupDocs.Signature oferece suporte a vários tipos de assinaturas, incluindo assinaturas eletrônicas, digitais e manuscritas.
### O GroupDocs.Signature é adequado para gerenciamento de documentos de nível empresarial?
Com certeza, GroupDocs.Signature foi projetado para atender às necessidades de desenvolvedores individuais e de aplicativos de nível empresarial, oferecendo recursos robustos e escalabilidade.
### Posso personalizar o processo de exclusão de assinaturas digitais?
Sim, GroupDocs.Signature oferece uma ampla gama de opções e configurações para personalizar o processo de exclusão de assinatura de acordo com seus requisitos específicos.
### Existe uma versão de teste disponível para testar GroupDocs.Signature?
 Sim, você pode baixar uma versão de teste gratuita no site[página de lançamentos](https://releases.groupdocs.com/).