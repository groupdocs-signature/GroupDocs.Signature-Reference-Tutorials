---
title: Assinar planilha com metadados
linktitle: Assinar planilha com metadados
second_title: API GroupDocs.Signature .NET
description: Aprenda como assinar planilhas com metadados usando Groupdocs.Signature for .NET. Melhore a integridade e verificação de documentos com assinaturas de metadados.
weight: 13
url: /pt/net/document-signing/sign-spreadsheet-with-metadata/
---
## Introdução
Neste tutorial, percorreremos o processo de assinatura de uma planilha com metadados usando Groupdocs.Signature for .NET. A assinatura de metadados permite incorporar informações adicionais em seus documentos, fornecendo contexto ou verificação. Ao final deste guia, você poderá aplicar assinaturas de metadados às suas planilhas sem esforço.
## Pré-requisitos
Antes de começarmos, certifique-se de ter os seguintes pré-requisitos:
1.  Groupdocs.Signature for .NET: Instale a biblioteca Groupdocs.Signature for .NET. Você pode baixá-lo em[aqui](https://releases.groupdocs.com/signature/net/).
2. Ambiente .NET: certifique-se de ter um ambiente .NET configurado em seu sistema.
3. Documento de planilha: tenha em mãos um exemplo de documento de planilha que você deseja assinar com metadados.
## Importar namespaces
Antes de implementar o código, importe os namespaces necessários para acessar as classes e métodos necessários:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
Agora, vamos dividir o código de exemplo em várias etapas para uma compreensão mais clara:
## Etapa 1: carregar o documento da planilha
```csharp
string filePath = "sample.xlsx";
string outputFilePath = Path.Combine("Your Document Directory", "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");
using (Signature signature = new Signature(filePath))
{
```
## Etapa 2: definir opções de sinalização de metadados
```csharp
	// criar opção de metadados com texto de metadados predefinido
	MetadataSignOptions options = new MetadataSignOptions();
```
## Etapa 3: criar assinaturas de metadados
```csharp
	// Crie algumas assinaturas de metadados de planilha
	SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
	{
		new SpreadsheetMetadataSignature("Author", "Mr.Scherlock Holmes"), // Valor da sequência
		new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now), // Valores de data e hora
		new SpreadsheetMetadataSignature("DocumentId", 123456), // Valor inteiro
		new SpreadsheetMetadataSignature("SignatureId", 123.456D), // Valor duplo
		new SpreadsheetMetadataSignature("Amount", 123.456M), // Valor decimal
		new SpreadsheetMetadataSignature("Total", 123.456F) // Valor flutuante
	};
	options.Signatures.AddRange(signatures);
```
## Passo 4: Assine o Documento
```csharp
	// assinar documento para arquivar
	SignResult result = signature.Sign(outputFilePath, options);
	Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```
## Conclusão
Parabéns! Você aprendeu como assinar uma planilha com metadados usando Groupdocs.Signature for .NET. A assinatura de metadados melhora a integridade do documento e fornece informações adicionais para fins de verificação. Comece hoje mesmo a aplicar assinaturas de metadados às suas planilhas e garanta a autenticidade e o contexto dos seus documentos.
## Perguntas frequentes
### O que é assinatura de metadados?
A assinatura de metadados envolve a incorporação de informações adicionais, como nome do autor, data de criação ou ID do documento, em um documento para fins de verificação.
### Posso personalizar as assinaturas de metadados?
Sim, você pode personalizar assinaturas de metadados de acordo com suas necessidades, incluindo texto, datas, inteiros, duplos, decimais e flutuantes.
### O Groupdocs.Signature for .NET é compatível com outros formatos de documentos?
Sim, Groupdocs.Signature for .NET oferece suporte a vários formatos de documentos, incluindo planilhas, apresentações, PDFs e muito mais.
### Como posso verificar assinaturas de metadados?
Você pode verificar assinaturas de metadados usando Groupdocs.Signature ou outro software compatível que suporte extração de metadados.
### Posso aplicar assinaturas de metadados programaticamente?
Sim, você pode aplicar assinaturas de metadados programaticamente usando a biblioteca Groupdocs.Signature for .NET em seus aplicativos .NET.