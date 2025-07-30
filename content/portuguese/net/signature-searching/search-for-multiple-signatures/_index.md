---
"description": "Aprenda a pesquisar vários tipos de assinatura em documentos usando o GroupDocs.Signature para .NET. Guia completo com exemplos de código para maior segurança de documentos."
"linktitle": "Pesquisar por assinaturas múltiplas"
"second_title": "API .NET do GroupDocs.Signature"
"title": "Pesquisar vários tipos de assinatura em documentos"
"url": "/pt/net/signature-searching/search-for-multiple-signatures/"
"weight": 14
---

## Introdução

Em sistemas modernos de gerenciamento de documentos, a capacidade de pesquisar e validar vários tipos de assinatura em um único documento é cada vez mais importante. As organizações frequentemente empregam vários tipos de assinatura — como assinaturas digitais, assinaturas de texto, códigos de barras, códigos QR e muito mais — para aumentar a segurança dos documentos e agilizar os processos de verificação. O GroupDocs.Signature para .NET oferece uma estrutura poderosa que permite aos desenvolvedores implementar uma funcionalidade abrangente de pesquisa de assinaturas em vários formatos de documentos.

Este tutorial guiará você pelo processo de pesquisa de vários tipos de assinatura em documentos usando o GroupDocs.Signature for .NET, oferecendo explicações detalhadas e exemplos práticos de código.

## Pré-requisitos

Antes de começar a implementar a funcionalidade de pesquisa de múltiplas assinaturas, certifique-se de ter os seguintes pré-requisitos:

1. Ambiente de desenvolvimento: Visual Studio ou qualquer ambiente de desenvolvimento .NET preferido instalado no seu sistema.
  
2. GroupDocs.Signature para .NET: Baixe e instale a biblioteca GroupDocs.Signature para .NET de [aqui](https://releases.groupdocs.com/signature/net/).

3. Conhecimento básico de C#: Familiaridade com a linguagem de programação C# e conceitos do framework .NET.

4. Documentos de amostra: prepare documentos de teste contendo vários tipos de assinaturas para fins de teste.

## Importar namespaces

Comece importando os namespaces necessários para acessar a funcionalidade GroupDocs.Signature:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Agora, vamos dividir o processo de busca por vários tipos de assinatura em etapas claras e gerenciáveis:

## Etapa 1: Carregue o documento

Primeiro, carregue o documento que contém as assinaturas que você deseja pesquisar:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // O código de pesquisa de múltiplas assinaturas será adicionado aqui
}
```

## Etapa 2: Defina opções de pesquisa para diferentes tipos de assinatura

Crie opções de pesquisa para cada tipo de assinatura que você deseja pesquisar:

```csharp
// Definir opções de pesquisa para assinaturas de texto
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,  // Pesquisar em todas as páginas
    Text = "Signature",  // Opcional: texto a ser encontrado
    MatchType = TextMatchType.Contains  // Critérios de correspondência
};

// Definir opções de pesquisa para assinaturas digitais
DigitalSearchOptions digitalOptions = new DigitalSearchOptions
{
    AllPages = true
};

// Definir opções de pesquisa para assinaturas de código de barras
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
{
    AllPages = true,
    Text = "123456",  // Opcional: texto do código de barras para corresponder
    MatchType = TextMatchType.Exact  // Critérios de correspondência
};

// Definir opções de pesquisa para assinaturas de código QR
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
{
    AllPages = true,
    Text = "John",  // Opcional: texto do código QR correspondente
    MatchType = TextMatchType.Contains  // Critérios de correspondência
};

// Definir opções de pesquisa para assinaturas de metadados
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```

## Etapa 3: Adicionar opções a uma coleção

Adicione todas as opções de pesquisa a uma coleção:

```csharp
// Crie uma lista para conter todas as opções de pesquisa
List<SearchOptions> searchOptions = new List<SearchOptions>
{
    textOptions,
    digitalOptions,
    barcodeOptions,
    qrCodeOptions,
    metadataOptions
};
```

## Etapa 4: Execute a pesquisa e processe os resultados

Execute a pesquisa usando as opções de pesquisa combinadas e processe os resultados:

```csharp
// Pesquise todos os tipos de assinatura usando as opções definidas
SearchResult result = signature.Search(searchOptions);

// Verifique se as assinaturas foram encontradas
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
    
    // Iterar pelas assinaturas encontradas
    foreach (var foundSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}, ID: {foundSignature.SignatureId}");
        
        // Processar tipos de assinatura específicos
        if (foundSignature is TextSignature textSignature)
        {
            Console.WriteLine($"Text: '{textSignature.Text}'");
        }
        else if (foundSignature is BarcodeSignature barcodeSignature)
        {
            Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
        }
        else if (foundSignature is QrCodeSignature qrCodeSignature)
        {
            Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
        }
        else if (foundSignature is DigitalSignature digitalSignature)
        {
            Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
        }
        else if (foundSignature is MetadataSignature metadataSignature)
        {
            Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
        }
    }
}
else
{
    Console.WriteLine("No signatures were found in the document.");
}
```

## Exemplo completo

Aqui está um exemplo completo e funcional que demonstra a busca por vários tipos de assinatura em um documento:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace MultiSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Caminho do documento
            string filePath = "sample_multiple_signatures.docx";
            
            // Inicializar instância de assinatura
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Definir opções de pesquisa para assinaturas de texto
                    TextSearchOptions textOptions = new TextSearchOptions
                    {
                        AllPages = true,
                        MatchType = TextMatchType.Contains
                    };

                    // Definir opções de pesquisa para assinaturas digitais
                    DigitalSearchOptions digitalOptions = new DigitalSearchOptions
                    {
                        AllPages = true
                    };

                    // Definir opções de pesquisa para assinaturas de código de barras
                    BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Definir opções de pesquisa para assinaturas de código QR
                    QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Definir opções de pesquisa para assinaturas de metadados
                    MetadataSearchOptions metadataOptions = new MetadataSearchOptions();

                    // Crie uma lista para conter todas as opções de pesquisa
                    List<SearchOptions> searchOptions = new List<SearchOptions>
                    {
                        textOptions,
                        digitalOptions,
                        barcodeOptions,
                        qrCodeOptions,
                        metadataOptions
                    };

                    // Pesquisar todos os tipos de assinatura
                    SearchResult result = signature.Search(searchOptions);

                    // Verifique se as assinaturas foram encontradas
                    if (result.Signatures.Count > 0)
                    {
                        Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
                        
                        // Resultados do processo por tipo de assinatura
                        foreach (var foundSignature in result.Signatures)
                        {
                            Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}");
                            
                            // Processar tipos de assinatura específicos
                            switch (foundSignature.SignatureType)
                            {
                                case SignatureType.Text:
                                    var textSignature = foundSignature as TextSignature;
                                    Console.WriteLine($"Text: '{textSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Barcode:
                                    var barcodeSignature = foundSignature as BarcodeSignature;
                                    Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.QrCode:
                                    var qrCodeSignature = foundSignature as QrCodeSignature;
                                    Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Digital:
                                    var digitalSignature = foundSignature as DigitalSignature;
                                    Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
                                    break;
                                    
                                case SignatureType.Metadata:
                                    var metadataSignature = foundSignature as MetadataSignature;
                                    Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
                                    break;
                            }
                            
                            Console.WriteLine(); // Adicionar quebra de linha entre assinaturas
                        }
                    }
                    else
                    {
                        Console.WriteLine("No signatures were found in the document.");
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"Error occurred: {ex.Message}");
                }
            }
            
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## Técnicas avançadas de pesquisa com múltiplas assinaturas

### Filtrando resultados de pesquisa

Você pode implementar filtragem avançada para restringir os resultados da pesquisa:

```csharp
// Filtrar resultados por número de página
var signaturesOnFirstPage = result.Signatures.FindAll(s => s.PageNumber == 1);

// Filtrar resultados por tipo de assinatura
var digitalSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.Digital);
var qrCodeSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.QrCode);

// Filtrar assinaturas de texto contendo conteúdo específico
var approvalSignatures = result.Signatures
    .FindAll(s => s is TextSignature && ((TextSignature)s).Text.Contains("Approved"));
```

### Validando múltiplas assinaturas

Implementar lógica de validação para diferentes tipos de assinatura:

```csharp
bool ValidateAllSignatures(SearchResult result)
{
    bool isDocumentValid = true;
    
    // Verifique se o documento possui uma assinatura digital válida
    bool hasValidDigitalSignature = result.Signatures
        .Any(s => s is DigitalSignature && ((DigitalSignature)s).IsValid);
    
    if (!hasValidDigitalSignature)
    {
        Console.WriteLine("Warning: Document does not contain a valid digital signature");
        isDocumentValid = false;
    }
    
    // Verifique se o documento possui o código QR necessário
    bool hasRequiredQRCode = result.Signatures
        .Any(s => s is QrCodeSignature && ((QrCodeSignature)s).Text.Contains("Auth-Code"));
    
    if (!hasRequiredQRCode)
    {
        Console.WriteLine("Warning: Document does not contain the required authentication QR code");
        isDocumentValid = false;
    }
    
    return isDocumentValid;
}
```

### Pesquisando com processamento personalizado

Você pode definir uma lógica de processamento personalizada para operações de pesquisa:

```csharp
// Crie opções de pesquisa com processamento personalizado
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,
    
    // Defina o processamento personalizado usando um delegado
    ProcessCompleted = (signature) =>
    {
        // Lógica de validação personalizada - aceitar apenas assinaturas em páginas especificadas
        TextSignature textSignature = signature as TextSignature;
        return textSignature != null && (textSignature.PageNumber == 1 || textSignature.PageNumber == 2);
    }
};
```

## Conclusão

Neste guia abrangente, exploramos como pesquisar vários tipos de assinatura em documentos usando o GroupDocs.Signature para .NET. Da configuração de opções de pesquisa para diferentes tipos de assinatura ao processamento e validação dos resultados, agora você tem o conhecimento necessário para implementar uma funcionalidade robusta de pesquisa de assinaturas em seus aplicativos .NET.

A capacidade de pesquisar vários tipos de assinatura simultaneamente aprimora os processos de verificação de documentos, reforça as medidas de segurança e agiliza os fluxos de trabalho de validação de documentos. O GroupDocs.Signature oferece uma estrutura poderosa e flexível para trabalhar com vários tipos de assinatura em diferentes formatos de documento, tornando-se uma excelente opção para aplicativos de processamento de documentos.

## Perguntas frequentes

### Posso pesquisar assinaturas em documentos protegidos por senha?

Sim, o GroupDocs.Signature suporta a busca de assinaturas em documentos protegidos por senha. Você pode fornecer a senha ao inicializar o `Signature` objeto:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Pesquisar assinaturas
}
```

### Quais formatos de documento são suportados para pesquisa de assinaturas?

O GroupDocs.Signature suporta uma ampla variedade de formatos de documentos, incluindo PDF, documentos do Microsoft Office (Word, Excel, PowerPoint), formatos OpenOffice, imagens e muito mais.

### Posso limitar a pesquisa a páginas específicas de um documento?

Sim, cada tipo de opção de pesquisa tem propriedades que permitem especificar quais páginas pesquisar:

```csharp
TextSearchOptions options = new TextSearchOptions
{
    AllPages = false,  // Não pesquise em todas as páginas
    PageNumber = 1,    // Pesquisar apenas na página 1
    
    // Ou especifique várias páginas
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } }
};
```

### Como posso otimizar o desempenho ao pesquisar em documentos grandes?

Para documentos grandes, você pode otimizar o desempenho:

1. Limitando a pesquisa a páginas ou intervalos de páginas específicos
2. Usando critérios de pesquisa mais específicos para reduzir o número de correspondências potenciais
3. Implementando paginação na exibição de resultados
4. Pesquisar um tipo de assinatura por vez se você não precisar de resultados simultâneos

### Posso estender o GroupDocs.Signature para oferecer suporte a tipos de assinatura personalizados?

Embora o GroupDocs.Signature forneça suporte integrado para tipos comuns de assinatura, você pode estender sua funcionalidade:

1. Criação de classes de opções de pesquisa personalizadas derivadas de `SearchOptions`
2. Implementando lógica de processamento personalizada usando o `ProcessCompleted` delegar
3. Desenvolvimento de classes wrapper que combinam múltiplas pesquisas de assinatura com lógica de negócios avançada

## Veja também

* [Referência de API](https://reference.groupdocs.com/signature/net/)
* [Exemplos de código no GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentação do produto](https://docs.groupdocs.com/signature/net/)
* [Página do produto](https://products.groupdocs.com/signature/net/)
* [Baixe a última versão](https://releases.groupdocs.com/signature/net/)
* [Artigos do blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Fórum de Suporte Gratuito](https://forum.groupdocs.com/c/signature/13)
* [Licença Temporária](https://purchase.groupdocs.com/temporary-license/)