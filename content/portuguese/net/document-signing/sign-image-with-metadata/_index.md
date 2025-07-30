---
"description": "Aprenda a assinar e incorporar metadados em imagens usando o GroupDocs.Signature para .NET. Adicione informações do autor, carimbos de data/hora e dados personalizados para aprimorar a autenticidade e a rastreabilidade das imagens."
"linktitle": "Imagem de sinal com metadados"
"second_title": "API .NET do GroupDocs.Signature"
"title": "Assinar imagens com metadados em C# .NET"
"url": "/pt/net/document-signing/sign-image-with-metadata/"
"weight": 10
---

## Introdução

assinatura digital de imagens com metadados está se tornando cada vez mais importante para estabelecer autenticidade, propriedade e rastreabilidade. O GroupDocs.Signature para .NET oferece uma solução poderosa e fácil de usar para adicionar assinaturas de metadados a diversos formatos de imagem. Este tutorial guia você por todo o processo de assinatura de imagens com metadados usando C#.

Assinaturas de metadados permitem que você incorpore informações valiosas diretamente em arquivos de imagem, como informações sobre o autor, carimbos de data e hora de criação, identificadores exclusivos e muito mais. Essas informações se tornam parte do próprio arquivo de imagem, fornecendo um método confiável para rastrear e verificar a autenticidade da imagem.

## Pré-requisitos

Antes de prosseguir com este tutorial, certifique-se de ter o seguinte:

1. [GroupDocs.Signature para .NET](https://releases.groupdocs.com/signature/net/) - Baixe e instale a biblioteca
2. Ambiente de desenvolvimento - Visual Studio ou qualquer IDE compatível com suporte .NET
3. Arquivo de imagem - Um arquivo de imagem de amostra em um formato compatível (PNG, JPG, TIFF, etc.)
4. Conhecimento básico de programação em C# - Familiaridade com conceitos de programação em C#

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

Defina os caminhos para sua imagem de origem e onde a saída assinada deve ser salva:

```csharp
// Especifique o caminho para o seu arquivo de imagem de origem
string filePath = "sample.png";

// Defina o diretório de saída e o nome do arquivo para a imagem assinada
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignImageWithMetadata", "SignedWithMetadata.png");

// Certifique-se de que o diretório de saída exista
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Etapa 2: Inicializar o Objeto de Assinatura

Crie uma instância da classe Signature com seu arquivo de imagem de origem:

```csharp
using (Signature signature = new Signature(filePath))
{
    // O resto do código irá aqui
}
```

## Etapa 3: Criar e configurar assinaturas de metadados

Em seguida, defina os metadados que deseja incorporar à imagem. O GroupDocs.Signature suporta vários tipos de dados para metadados:

```csharp
// Inicializar ID de metadados (específico para formato de imagem)
ushort imgsMetadataId = 41996;

// Criar objeto de opções de metadados
MetadataSignOptions options = new MetadataSignOptions();

// Adicionar vários tipos de assinaturas de metadados
options
    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes"))  // Valor da sequência de caracteres
    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Valor de data e hora
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Valor inteiro
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Valor duplo
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Valor decimal
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Valor flutuante
```

## Etapa 4: Assine a imagem com metadados

Aplique as assinaturas de metadados à imagem e salve o resultado:

```csharp
// Assine o documento e salve no caminho do arquivo de saída
SignResult result = signature.Sign(outputFilePath, options);

// Exibir mensagem de sucesso
Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed image saved at: {outputFilePath}");
```

## Exemplo completo

Aqui está o exemplo de código completo que reúne todas as etapas:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignImageWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Especificar caminhos de arquivo
            string filePath = "sample.png";            
            string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
            
            // Certifique-se de que o diretório de saída exista
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Assine a imagem com metadados
            using (Signature signature = new Signature(filePath))
            {
                // Inicializar ID de metadados (específico para formato de imagem)
                ushort imgsMetadataId = 41996;
                
                // Criar opções de metadados
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Adicionar diferentes tipos de assinaturas de metadados
                options
                    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes")) // Valor da sequência de caracteres
                    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Valor de data e hora
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Valor inteiro
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Valor duplo
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Valor decimal
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Valor flutuante
                
                // Assine o documento e salve em arquivo
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Exibir resultados
                Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Técnicas avançadas de assinatura de metadados

### Trabalhando com metadados personalizados

Você também pode criar campos de metadados personalizados com IDs específicos:

```csharp
// Crie metadados personalizados com ID específico
options.Add(new ImageMetadataSignature(42000, "CustomValue"));
```

### Verificando Assinaturas de Metadados

Após a assinatura, você pode querer verificar as assinaturas de metadados:

```csharp
// Criar opções de verificação
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Pesquisar assinaturas de metadados
SearchResult result = signature.Search(searchOptions);

// Exibir assinaturas encontradas
Console.WriteLine($"Found {result.Signatures.Count} metadata signatures:");
foreach(var metadataSignature in result.Signatures)
{
    Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value}");
}
```

## Conclusão

Neste tutorial, você aprendeu a assinar imagens com metadados usando o GroupDocs.Signature para .NET. Incorporar metadados em imagens é uma excelente maneira de aprimorar a autenticidade das imagens, adicionar informações críticas e aprimorar os fluxos de trabalho de gerenciamento de documentos. O processo é simples, porém eficiente, permitindo personalização com base nas suas necessidades específicas.

Os metadados incorporados no arquivo de imagem podem ser usados para diversos fins, como proteção de direitos autorais, rastreamento da origem da imagem, adição de informações descritivas e estabelecimento de cadeia de custódia digital. Ao implementar assinaturas de metadados, você garante que suas imagens mantenham sua integridade e autenticidade durante todo o seu ciclo de vida.

## Perguntas frequentes

### Posso adicionar metadados a imagens assinadas existentes?

Sim, você pode adicionar metadados adicionais a imagens que já contêm assinaturas de metadados. Os metadados existentes serão preservados e novos metadados serão adicionados conforme necessário.

### Quais formatos de imagem são suportados para assinatura de metadados?

O GroupDocs.Signature para .NET oferece suporte à assinatura de metadados para vários formatos de imagem, incluindo PNG, JPEG, TIFF, BMP, GIF e outros. Para obter uma lista completa, consulte o [documentação oficial](https://docs.groupdocs.com/signature/net/).

### É possível criptografar os metadados em imagens?

Sim, o GroupDocs.Signature oferece opções para criptografar metadados para maior segurança. Você pode usar as opções de criptografia fornecidas pela biblioteca para proteger informações de metadados confidenciais.

### Posso validar programaticamente a autenticidade de imagens assinadas?

Com certeza. Você pode usar os métodos de verificação em GroupDocs.Signature para validar assinaturas de metadados e confirmar a autenticidade de imagens assinadas.

### Existe alguma limitação de tamanho de arquivo ao assinar imagens com metadados?

Não há limite específico de tamanho de arquivo imposto pela biblioteca em si, mas arquivos muito grandes podem exigir mais tempo de processamento e memória. Recomenda-se considerar os recursos do sistema ao trabalhar com imagens extremamente grandes.

### Como posso obter uma licença temporária para fins de testes?

Você pode obter um [licença temporária](https://purchase.groupdocs.com/temporary-license/) para testar o GroupDocs.Signature antes de fazer uma compra.

### Onde posso encontrar mais recursos e suporte?

- [Referência de API](https://reference.groupdocs.com/signature/net/)
- [Transferências](https://releases.groupdocs.com/signature/net/)
- [Exemplos](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Documentação](https://docs.groupdocs.com/signature/net/)
- [Página do produto](https://products.groupdocs.com/signature/net/)
- [Blogue](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Fórum de Suporte](https://forum.groupdocs.com/c/signature/13)