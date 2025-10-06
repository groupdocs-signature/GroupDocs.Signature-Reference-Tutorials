---
"description": "Proteja e aprimore planilhas do Excel incorporando assinaturas de metadados usando o GroupDocs.Signature para .NET. Adicione informações do autor, carimbos de data/hora e dados personalizados para melhorar a rastreabilidade e a autenticidade dos documentos."
"linktitle": "Planilha de Assinatura com Metadados"
"second_title": "API .NET do GroupDocs.Signature"
"title": "Adicionar assinaturas de metadados a planilhas do Excel em C# .NET"
"url": "/pt/net/document-signing/sign-spreadsheet-with-metadata/"
"weight": 13
type: docs
---
## Introdução

Planilhas do Excel geralmente contêm dados comerciais críticos, informações financeiras e cálculos importantes. Garantir sua autenticidade, rastrear sua origem e proteger sua integridade é crucial em muitos ambientes profissionais. Uma abordagem eficaz para aumentar a segurança e a rastreabilidade das planilhas é incorporar assinaturas de metadados.

Este tutorial abrangente guiará você pelo processo de assinatura de planilhas do Excel com metadados usando o GroupDocs.Signature para .NET. Ao adicionar assinaturas de metadados, você pode incorporar informações valiosas, como detalhes do autor, carimbos de data/hora de criação, identificadores de documentos e outras propriedades personalizadas, diretamente na estrutura do arquivo da planilha.

## Pré-requisitos

Antes de prosseguir com este tutorial, certifique-se de ter o seguinte:

1. [GroupDocs.Signature para .NET](https://releases.groupdocs.com/signature/net/) - Baixe e instale a biblioteca
2. Ambiente de desenvolvimento - Visual Studio ou qualquer outro IDE compatível com .NET
3. Planilha do Excel - Um arquivo de planilha de exemplo (XLSX, XLS, etc.)
4. Conhecimento básico de C# - Familiaridade com a linguagem de programação C#

## Importar namespaces

Comece importando os namespaces necessários para acessar a funcionalidade GroupDocs.Signature:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Etapa 1: Configurar caminhos de arquivo

Defina os caminhos para sua planilha de origem e onde a saída assinada deve ser salva:

```csharp
// Especifique o caminho para o seu arquivo Excel
string filePath = "sample.xlsx";

// Defina o diretório de saída e o nome do arquivo para a planilha assinada
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");

// Certifique-se de que o diretório de saída exista
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Etapa 2: Inicializar o Objeto de Assinatura

Crie uma instância da classe Signature com seu arquivo de planilha de origem:

```csharp
using (Signature signature = new Signature(filePath))
{
    // O resto do código irá aqui
}
```

## Etapa 3: Criar e configurar assinaturas de metadados

Em seguida, defina as opções de metadados e crie uma matriz de assinaturas de metadados da planilha:

```csharp
// Criar objeto de opções de metadados
MetadataSignOptions options = new MetadataSignOptions();

// Crie uma matriz de assinaturas de metadados de planilha com diferentes tipos de dados
SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // Valor da sequência de caracteres
    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // Valor de data e hora
    new SpreadsheetMetadataSignature("DocumentId", 123456),           // Valor inteiro
    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // Valor duplo
    new SpreadsheetMetadataSignature("Amount", 123.456M),             // Valor decimal
    new SpreadsheetMetadataSignature("Total", 123.456F)               // Valor flutuante
};

// Adicionar coleta de assinaturas às opções
options.Signatures.AddRange(signatures);
```

## Etapa 4: Assine a planilha com metadados

Aplique as assinaturas de metadados à planilha e salve o resultado:

```csharp
// Assine o documento e salve no caminho do arquivo de saída
SignResult result = signature.Sign(outputFilePath, options);

// Exibir mensagem de sucesso
Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed spreadsheet saved at: {outputFilePath}");
```

## Exemplo completo

Aqui está o exemplo de código completo que reúne todas as etapas:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignSpreadsheetWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Especificar caminhos de arquivo
            string filePath = "sample.xlsx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");
            
            // Certifique-se de que o diretório de saída exista
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Assine a planilha com metadados
            using (Signature signature = new Signature(filePath))
            {
                // Criar objeto de opções de metadados
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Crie uma matriz de assinaturas de metadados de planilha com diferentes tipos de dados
                SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
                {
                    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // Valor da sequência de caracteres
                    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // Valor de data e hora
                    new SpreadsheetMetadataSignature("DocumentId", 123456),           // Valor inteiro
                    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // Valor duplo
                    new SpreadsheetMetadataSignature("Amount", 123.456M),             // Valor decimal
                    new SpreadsheetMetadataSignature("Total", 123.456F)               // Valor flutuante
                };
                
                // Adicionar coleta de assinaturas às opções
                options.Signatures.AddRange(signatures);
                
                // Assine o documento e salve em arquivo
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Exibir resultados
                Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Técnicas avançadas de metadados de planilha

### Trabalhando com propriedades de planilha personalizadas e integradas

As planilhas do Excel possuem propriedades integradas e personalizadas que podem ser acessadas por meio da caixa de diálogo de propriedades do arquivo. O GroupDocs.Signature permite que você trabalhe com ambos:

```csharp
// Adicionar propriedades integradas
signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Company", "Sherlock Holmes Consulting"),
    new SpreadsheetMetadataSignature("Category", "Financial"),
    new SpreadsheetMetadataSignature("Keywords", "budget,forecast,analysis"),
    new SpreadsheetMetadataSignature("Comments", "This spreadsheet contains confidential information"),
    new SpreadsheetMetadataSignature("Manager", "John Watson")
};
options.Signatures.AddRange(signatures);

// Adicionar propriedades personalizadas
options.Signatures.Add(new SpreadsheetMetadataSignature("Department", "Finance"));
options.Signatures.Add(new SpreadsheetMetadataSignature("SecurityLevel", "Confidential"));
```

### Procurando metadados em planilhas assinadas

Após a assinatura, você pode querer verificar ou extrair os metadados:

```csharp
// Crie opções de pesquisa para metadados
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Pesquisar assinaturas de metadados
SearchResult searchResult = signature.Search(searchOptions);

// Exibir assinaturas encontradas
Console.WriteLine($"Found {searchResult.Signatures.Count} metadata signatures:");
foreach (var foundSignature in searchResult.Signatures)
{
    MetadataSignature metadataSignature = foundSignature as MetadataSignature;
    if (metadataSignature != null)
    {
        Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value} ({metadataSignature.Value.GetType().Name})");
    }
}
```

### Atualizando Metadados Existentes

Você pode atualizar metadados existentes em planilhas usando os mesmos nomes de propriedade:

```csharp
// Atualizar metadados existentes
options.Signatures.Add(new SpreadsheetMetadataSignature("Author", "Updated Author Name"));
```

## Conclusão

Neste tutorial abrangente, você aprendeu a assinar planilhas do Excel com metadados usando o GroupDocs.Signature para .NET. A incorporação de metadados em arquivos de planilha melhora a rastreabilidade do documento, fornece contexto valioso e ajuda a estabelecer a autenticidade.

Assinaturas de metadados em planilhas são particularmente úteis em ambientes corporativos onde a origem, a autoria e o rastreamento de versões do documento são importantes. Os metadados incorporados podem incluir informações sobre o autor, a data de criação, os identificadores do documento e propriedades personalizadas relevantes para as necessidades da sua organização.

Ao implementar assinaturas de metadados com o GroupDocs.Signature, você pode garantir que suas planilhas do Excel mantenham sua integridade e forneçam informações verificáveis durante todo o seu ciclo de vida.

## Perguntas frequentes

### Posso adicionar metadados a planilhas que já tenham algumas propriedades definidas?

Sim, você pode adicionar novos metadados ou atualizar os existentes em planilhas. O GroupDocs.Signature cuidará da integração, adicionando novas propriedades ou atualizando as existentes com os mesmos nomes.

### Quais formatos de planilha são suportados para assinatura de metadados?

GroupDocs.Signature para .NET oferece suporte à assinatura de metadados para vários formatos de planilha, incluindo XLSX, XLS, XLSM, ODS e outros. Para obter uma lista completa, consulte o [documentação oficial](https://docs.groupdocs.com/signature/net/).

### As assinaturas de metadados em planilhas são visíveis para os usuários?

As assinaturas de metadados não são visíveis no conteúdo da planilha. No entanto, podem ser visualizadas no painel de propriedades do documento no Excel ou em outros aplicativos compatíveis.

### Posso validar programaticamente se uma planilha foi adulterada após adicionar metadados?

Sim, o GroupDocs.Signature fornece recursos de verificação que podem ajudar a detectar se um documento foi modificado após a assinatura, incluindo alterações nos metadados.

### A adição de metadados afeta a funcionalidade da planilha?

Adicionar metadados tem impacto mínimo no tamanho do arquivo e nenhum impacto na funcionalidade da planilha. É uma maneira simples de aprimorar as propriedades do documento sem afetar cálculos, fórmulas ou outros recursos do Excel.

### Onde posso encontrar mais recursos e suporte?

- [Referência de API](https://reference.groupdocs.com/signature/net/)
- [Transferências](https://releases.groupdocs.com/signature/net/)
- [Exemplos](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Documentação](https://docs.groupdocs.com/signature/net/)
- [Página do produto](https://products.groupdocs.com/signature/net/)
- [Blogue](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Fórum de Suporte](https://forum.groupdocs.com/c/signature/13)
- [Licença Temporária](https://purchase.groupdocs.com/temporary-license/)