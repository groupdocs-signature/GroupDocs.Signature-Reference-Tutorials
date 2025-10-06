---
"description": "Integre assinaturas de metadados em documentos PDF usando o GroupDocs.Signature para .NET. Aprenda a incorporar informações do autor, carimbos de data/hora e dados personalizados para aprimorar a autenticidade e a rastreabilidade do PDF."
"linktitle": "Assinar PDF com metadados"
"second_title": "API .NET do GroupDocs.Signature"
"title": "Adicionar assinaturas de metadados a documentos PDF em C# .NET"
"url": "/pt/net/document-signing/sign-pdf-with-metadata/"
"weight": 11
type: docs
---
## Introdução

Documentos PDF (Portable Document Format) são amplamente utilizados em diversos setores devido à sua consistência e independência de plataforma. Garantir a autenticidade e a rastreabilidade desses documentos é crucial em muitos ambientes profissionais. Uma maneira eficaz de conseguir isso é incorporar metadados aos próprios arquivos PDF.

Neste tutorial abrangente, exploraremos como assinar documentos PDF com metadados usando o GroupDocs.Signature para .NET. As assinaturas de metadados permitem que você incorpore informações adicionais ao documento, como detalhes do autor, carimbos de data/hora de criação, identificadores de documento e valores personalizados, sem alterar visivelmente a aparência do documento.

## Pré-requisitos

Antes de começar, certifique-se de ter o seguinte em mãos:

1. [GroupDocs.Signature para .NET](https://releases.groupdocs.com/signature/net/) - Baixe e instale a biblioteca
2. Ambiente de desenvolvimento - Visual Studio ou qualquer outro IDE compatível com .NET
3. Documento PDF - Um arquivo PDF de exemplo para assinatura
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

Primeiro, defina o caminho para o seu documento PDF e especifique onde deseja salvar a saída assinada:

```csharp
// Especifique o caminho para o seu documento PDF
string filePath = "sample.pdf";

// Definir diretório de saída e caminho do arquivo
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignPdfWithMetadata", "SignedWithMetadata.pdf");

// Certifique-se de que o diretório de saída exista
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Etapa 2: Inicializar o Objeto de Assinatura

Crie uma instância da classe Signature com seu documento PDF de origem:

```csharp
using (Signature signature = new Signature(filePath))
{
    // O código para assinatura irá aqui
}
```

## Etapa 3: Definir opções de metadados

Crie e configure as opções de metadados, adicionando vários tipos de assinaturas de metadados:

```csharp
// Criar objeto de opções de metadados
MetadataSignOptions options = new MetadataSignOptions();

// Adicione vários tipos de metadados usando a interface fluente
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Valor da sequência de caracteres
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Valor de data e hora
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Valor inteiro
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Valor duplo
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Valor decimal
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Valor flutuante
```

## Etapa 4: Assine o PDF com metadados

Aplique as assinaturas de metadados ao documento PDF e salve o resultado:

```csharp
// Assine o documento e salve no caminho de saída
SignResult result = signature.Sign(outputFilePath, options);

// Exibir mensagem de sucesso
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed document saved at: {outputFilePath}");
```

## Exemplo completo

Aqui está o exemplo de código completo que reúne todas as etapas:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignPdfWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Especificar caminhos de arquivo
            string filePath = "sample.pdf";
            string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
            
            // Certifique-se de que o diretório de saída exista
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Assine o PDF com metadados
            using (Signature signature = new Signature(filePath))
            {
                // Criar objeto de opções de metadados
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Adicionar diferentes tipos de assinaturas de metadados
                options
                    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Valor da sequência de caracteres
                    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Valor de data e hora
                    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Valor inteiro
                    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Valor duplo
                    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Valor decimal
                    .Add(new PdfMetadataSignature("Total", 123.456F));              // Valor flutuante
                
                // Assine o documento e salve em arquivo
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Exibir resultados
                Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Operações avançadas de metadados PDF

### Adicionando metadados personalizados com suporte a namespace

Documentos PDF oferecem suporte a metadados personalizados com suporte a namespace XML:

```csharp
// Adicionar metadados personalizados com namespace
options.Add(new PdfMetadataSignature("CustomProperty", "Custom Value")
{
    NamespaceUri = "http://seu-namespace.com/schema"
});
```

### Procurando metadados em PDFs assinados

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

### Trabalhando com metadados PDF padrão

Os documentos PDF têm campos de metadados padrão que podem ser acessados e modificados:

```csharp
// Definir campos de metadados PDF padrão
options
    .Add(new PdfMetadataSignature("Title", "Important Contract"))
    .Add(new PdfMetadataSignature("Subject", "Legal Agreement"))
    .Add(new PdfMetadataSignature("Keywords", "contract, agreement, legal, binding"))
    .Add(new PdfMetadataSignature("Creator", "Legal Department"))
    .Add(new PdfMetadataSignature("Producer", "GroupDocs.Signature"));
```

## Conclusão

Neste tutorial, você aprendeu a assinar documentos PDF com metadados usando o GroupDocs.Signature para .NET. Incorporar metadados em arquivos PDF é uma excelente maneira de aprimorar a autenticidade dos documentos, adicionar informações críticas e aprimorar os fluxos de trabalho de gerenciamento de documentos.

Assinaturas de metadados em PDFs são particularmente valiosas em ambientes corporativos onde a rastreabilidade e a verificação de autenticidade de documentos são essenciais. Os metadados incorporados podem incluir informações sobre a origem, o autor, a data de criação, a versão e as propriedades personalizadas do documento relevantes para o fluxo de trabalho da sua organização.

Ao implementar assinaturas de metadados com o GroupDocs.Signature, você pode garantir que seus documentos PDF mantenham sua integridade e forneçam informações verificáveis durante todo o seu ciclo de vida.

## Perguntas frequentes

### Posso modificar metadados existentes em um documento PDF?

Sim, você pode modificar metadados existentes em documentos PDF. Ao aplicar novas assinaturas de metadados com os mesmos nomes das existentes, os valores serão atualizados de acordo.

### As assinaturas de metadados em documentos PDF são visíveis para o usuário final?

As assinaturas de metadados não são visíveis no conteúdo do documento em si. No entanto, podem ser visualizadas no painel de propriedades do documento em leitores de PDF como o Adobe Acrobat ou usando ferramentas especializadas para visualização de metadados.

### Posso criptografar ou proteger os metadados em PDFs?

O GroupDocs.Signature oferece opções para proteger documentos, incluindo criptografia. Você pode aplicar criptografia em nível de documento para proteger todo o PDF, incluindo seus metadados.

### Existe um limite para a quantidade de metadados que posso adicionar a um PDF?

Embora não haja um limite estrito imposto pela especificação do PDF, adicionar quantidades excessivas de metadados pode aumentar o tamanho do arquivo. Recomenda-se incluir apenas informações relevantes e necessárias nos metadados.

### Posso validar programaticamente se um PDF foi adulterado após adicionar metadados?

Sim, o GroupDocs.Signature fornece recursos de verificação que podem ajudar a detectar se um documento foi modificado após a assinatura, incluindo alterações nos metadados.

### Onde posso encontrar mais recursos e suporte?

- [Referência de API](https://reference.groupdocs.com/signature/net/)
- [Transferências](https://releases.groupdocs.com/signature/net/)
- [Exemplos](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Documentação](https://docs.groupdocs.com/signature/net/)
- [Página do produto](https://products.groupdocs.com/signature/net/)
- [Blogue](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Fórum de Suporte](https://forum.groupdocs.com/c/signature/13)
- [Licença Temporária](https://purchase.groupdocs.com/temporary-license/)