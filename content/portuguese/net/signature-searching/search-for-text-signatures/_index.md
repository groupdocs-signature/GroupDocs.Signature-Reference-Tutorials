---
"description": "Aprenda como pesquisar assinaturas de texto em documentos de forma eficiente usando o GroupDocs.Signature para .NET com nosso guia passo a passo abrangente e exemplos de código."
"linktitle": "Pesquisar por Assinaturas de Texto"
"second_title": "API .NET do GroupDocs.Signature"
"title": "Pesquisar assinaturas de texto em documentos"
"url": "/pt/net/signature-searching/search-for-text-signatures/"
"weight": 16
type: docs
---
## Introdução

Assinaturas de texto são um método comum para indicar autoria, aprovação ou verificação de documentos. Na gestão de documentos digitais, a capacidade de pesquisar e extrair assinaturas de texto programaticamente é crucial para a validação de documentos, automação do fluxo de trabalho e verificação de conformidade. O GroupDocs.Signature para .NET oferece uma solução abrangente para implementar a funcionalidade de pesquisa de assinaturas de texto em seus aplicativos .NET, com suporte a diversos formatos de documentos e recursos avançados de pesquisa.

Este tutorial guiará você pelo processo de busca de assinaturas de texto em documentos usando o GroupDocs.Signature for .NET, fornecendo explicações detalhadas, instruções passo a passo e exemplos práticos de código.

## Pré-requisitos

Antes de começar a pesquisar assinaturas de texto, certifique-se de ter os seguintes pré-requisitos:

1. GroupDocs.Signature para biblioteca .NET: Baixe e instale a biblioteca do [página de lançamentos](https://releases.groupdocs.com/signature/net/).

2. Ambiente de desenvolvimento: configure um ambiente de desenvolvimento adequado, como o Visual Studio ou qualquer IDE compatível com suporte ao .NET.

3. Documentos de amostra: prepare documentos de teste contendo assinaturas de texto para verificação e teste.

4. Conhecimento básico de C#: Familiaridade com a linguagem de programação C# e conceitos do framework .NET.

## Importar namespaces

Comece importando os namespaces necessários para acessar a funcionalidade GroupDocs.Signature:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Agora, vamos dividir o processo de busca de assinaturas de texto em etapas claras e gerenciáveis:

## Etapa 1: Carregue o documento

Primeiro, defina o caminho do documento e inicialize um `Signature` objeto:

```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);

using (Signature signature = new Signature(filePath))
{
    // O código de pesquisa de assinatura de texto será adicionado aqui
}
```

## Etapa 2: Configurar opções de pesquisa

Criar e configurar `TextSearchOptions` para especificar como as assinaturas de texto devem ser pesquisadas:

```csharp
// Configurar opções de pesquisa de texto
TextSearchOptions options = new TextSearchOptions
{
    // Pesquisar em todas as páginas
    AllPages = true,
    
    // Opcional: especifique o texto a ser correspondido
    // Texto = "Aprovado",
    
    // Opcional: especifique o tipo de correspondência
    // MatchType = TextMatchType.Contém
};
```

## Etapa 3: Executar pesquisa de assinatura de texto

Execute a operação de pesquisa usando as opções configuradas:

```csharp
// Pesquisar assinaturas de texto
List<TextSignature> signatures = signature.Search<TextSignature>(options);
```

## Etapa 4: Processar e exibir resultados

Percorra as assinaturas de texto encontradas e exiba seus detalhes:

```csharp
// Exibir resultados da pesquisa
Console.WriteLine($"\nSource document '{fileName}' contains {signatures.Count} text signature(s):");

foreach (TextSignature textSignature in signatures)
{
    Console.WriteLine($"Text signature found at page {textSignature.PageNumber} with text '{textSignature.Text}'");
    Console.WriteLine($"Location: X={textSignature.Left}, Y={textSignature.Top}, Width={textSignature.Width}, Height={textSignature.Height}");
    Console.WriteLine($"Signature type: {textSignature.SignatureImplementation}");
    Console.WriteLine();
}
```

## Exemplo completo

Aqui está um exemplo prático completo que demonstra como pesquisar assinaturas de texto em um documento:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace TextSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Caminho do documento - atualize com o caminho do seu arquivo
            string filePath = "sample_multiple_signatures.docx";
            string fileName = Path.GetFileName(filePath);
            
            // Inicializar instância de assinatura
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Configurar opções de pesquisa de texto
                    TextSearchOptions options = new TextSearchOptions
                    {
                        // Pesquisar em todas as páginas
                        AllPages = true
                    };
                    
                    // Pesquisar assinaturas de texto
                    List<TextSignature> signatures = signature.Search<TextSignature>(options);
                    
                    // Exibir resultados da pesquisa
                    Console.WriteLine($"\nSource document '{fileName}' contains {signatures.Count} text signature(s):");
                    
                    foreach (TextSignature textSignature in signatures)
                    {
                        Console.WriteLine($"Text signature found at page {textSignature.PageNumber} with text '{textSignature.Text}'");
                        Console.WriteLine($"Location: X={textSignature.Left}, Y={textSignature.Top}, Width={textSignature.Width}, Height={textSignature.Height}");
                        Console.WriteLine($"Signature type: {textSignature.SignatureImplementation}");
                        Console.WriteLine();
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

## Técnicas avançadas de pesquisa de assinaturas de texto

### Pesquisando com critérios de texto específicos

Para pesquisas mais direcionadas, você pode personalizar o `TextSearchOptions` para filtrar por conteúdo de texto específico:

```csharp
// Crie opções de pesquisa com critérios de texto específicos
TextSearchOptions options = new TextSearchOptions
{
    // Pesquisar em todas as páginas
    AllPages = true,
    
    // Pesquisar por texto específico
    Text = "Approved",
    
    // Especifique o tipo de correspondência (Contém, Exato, Começa com, Termina com)
    MatchType = TextMatchType.Contains,
    
    // Pesquisa com diferenciação entre maiúsculas e minúsculas
    MatchCase = true
};
```

### Pesquisando em áreas específicas do documento

Você pode limitar a pesquisa a áreas específicas do documento:

```csharp
// Crie opções de pesquisa para uma área específica do documento
TextSearchOptions options = new TextSearchOptions
{
    // Pesquisar apenas em páginas específicas
    AllPages = false,
    PageNumber = 1,
    
    // Ou especifique várias páginas
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // Defina uma área específica para pesquisar
    Rectangle = new Rectangle(100, 100, 400, 200)
};
```

### Filtragem de texto avançada

Implemente lógica de filtragem personalizada para requisitos de pesquisa mais complexos:

```csharp
// Crie opções de pesquisa com processamento personalizado
TextSearchOptions options = new TextSearchOptions
{
    AllPages = true,
    
    // Defina o processamento personalizado usando um delegado
    ProcessCompleted = (TextSignature signature) =>
    {
        // Lógica de validação personalizada
        bool isValid = signature.Text.Length > 5 && 
                      (signature.Text.Contains("Approved") || signature.Text.Contains("Verified"));
        
        return isValid;
    }
};
```

### Procurando por diferentes estilos de texto

Use propriedades de fonte e estilo para filtrar assinaturas de texto:

```csharp
// Crie opções de pesquisa direcionadas à aparência específica do texto
TextSearchOptions options = new TextSearchOptions
{
    // Filtrar por nome da fonte
    FontName = "Arial",
    
    // Filtrar por intervalo de tamanho de fonte
    MinFontSize = 10,
    MaxFontSize = 14,
    
    // Filtrar por cor da fonte
    ForeColor = System.Drawing.Color.Blue
};
```

### Extraindo Metadados de Assinatura

Extraia e processe metadados associados a assinaturas de texto:

```csharp
foreach (TextSignature signature in signatures)
{
    // Acessar metadados de assinatura
    if (signature.Metadata != null && signature.Metadata.Count > 0)
    {
        Console.WriteLine("Signature Metadata:");
        
        foreach (var item in signature.Metadata)
        {
            Console.WriteLine($"  {item.Key}: {item.Value}");
        }
    }
    
    // Verifique as datas de criação e modificação da assinatura
    if (signature.CreatedOn.HasValue)
    {
        Console.WriteLine($"Created on: {signature.CreatedOn.Value}");
    }
    
    if (signature.ModifiedOn.HasValue)
    {
        Console.WriteLine($"Modified on: {signature.ModifiedOn.Value}");
    }
}
```

## Conclusão

Neste guia abrangente, exploramos como pesquisar assinaturas de texto em documentos usando o GroupDocs.Signature para .NET. De operações básicas de pesquisa a técnicas avançadas, agora você tem o conhecimento necessário para implementar uma funcionalidade robusta de assinatura de texto em seus aplicativos .NET.

O GroupDocs.Signature fornece uma estrutura poderosa e flexível para trabalhar com assinaturas de texto, permitindo que você crie sistemas sofisticados de verificação de documentos, soluções de fluxo de trabalho automatizadas e ferramentas de validação de conformidade.

## Perguntas frequentes

### Posso pesquisar assinaturas de texto em documentos protegidos por senha?

Sim, o GroupDocs.Signature suporta a busca por assinaturas de texto em documentos protegidos por senha. Você pode fornecer a senha ao inicializar o `Signature` objeto:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Pesquisar assinaturas de texto
}
```

### Quais formatos de documento são suportados para pesquisa de assinatura de texto?

GroupDocs.Signature suporta uma ampla variedade de formatos de documentos, incluindo PDF, documentos do Microsoft Office (Word, Excel, PowerPoint), formatos OpenOffice, imagens e muito mais.

### Posso pesquisar assinaturas de texto com formatação específica, como negrito ou itálico?

Sim, você pode pesquisar assinaturas de texto com formatação específica usando o `FontBold` e `FontItalic` propriedades em `TextSearchOptions`:

```csharp
TextSearchOptions options = new TextSearchOptions
{
    FontBold = true,
    FontItalic = true
};
```

### Como posso melhorar o desempenho da pesquisa para documentos grandes?

Para documentos grandes, você pode otimizar o desempenho da pesquisa:

1. Limitar a pesquisa a páginas específicas em vez de pesquisar no documento inteiro
2. Usando critérios de pesquisa mais específicos para reduzir o número de correspondências
3. Especificando uma área de pesquisa usando o `Rectangle` propriedade se você sabe onde as assinaturas normalmente estão localizadas
4. Implementando paginação em seu aplicativo para processar resultados de pesquisa em lotes

### Posso detectar se uma assinatura de texto foi adicionada eletronicamente ou faz parte do conteúdo do documento original?

GroupDocs.Signature consegue distinguir entre diferentes tipos de elementos de texto em documentos. `SignatureImplementation` propriedade de `TextSignature` indica se o texto é uma assinatura formal ou conteúdo regular de um documento. No entanto, a determinação definitiva pode depender de como o texto foi originalmente adicionado ao documento.

## Veja também

* [Referência de API](https://reference.groupdocs.com/signature/net/)
* [Exemplos de código no GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentação do produto](https://docs.groupdocs.com/signature/net/)
* [Página do produto](https://products.groupdocs.com/signature/net/)
* [Baixe a última versão](https://releases.groupdocs.com/signature/net/)
* [Artigos do blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Fórum de Suporte Gratuito](https://forum.groupdocs.com/c/signature/13)
* [Licença Temporária](https://purchase.groupdocs.com/temporary-license/)