---
"description": "Aprenda como pesquisar códigos QR em documentos de forma eficiente usando o GroupDocs.Signature para .NET com este guia passo a passo abrangente e exemplos de código."
"linktitle": "Pesquisar por códigos QR"
"second_title": "API .NET do GroupDocs.Signature"
"title": "Pesquisar assinaturas de código QR em documentos"
"url": "/pt/net/signature-searching/search-for-qr-codes/"
"weight": 15
type: docs
---
## Introdução

No ecossistema de documentos digitais atual, as assinaturas de código QR tornaram-se uma ferramenta inestimável para incorporar informações, autenticar e aprimorar a segurança de documentos. O GroupDocs.Signature para .NET oferece aos desenvolvedores uma API poderosa para pesquisar e extrair códigos QR de vários formatos de documentos, permitindo recursos avançados de análise e verificação de documentos em aplicativos .NET.

Este tutorial abrangente guiará você pelo processo de implementação da funcionalidade de pesquisa de código QR usando o GroupDocs.Signature para .NET, fornecendo explicações claras, instruções passo a passo e exemplos práticos de código que você pode integrar em seus próprios aplicativos.

## Pré-requisitos

Antes de começar a pesquisar assinaturas de código QR, certifique-se de ter os seguintes pré-requisitos:

1. GroupDocs.Signature para .NET SDK: Baixe e instale o SDK do [página de download](https://releases.groupdocs.com/signature/net/).

2. Ambiente de desenvolvimento: configure um ambiente de desenvolvimento .NET, como o Visual Studio, com o .NET Framework ou o .NET Core instalado.

3. Conhecimento básico: Familiaridade com programação em C# e conceitos de desenvolvimento .NET.

4. Documentos de exemplo: prepare documentos de teste contendo códigos QR para verificação e teste.

## Importar namespaces

Comece importando os namespaces necessários para acessar a funcionalidade GroupDocs.Signature:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;
```

Agora, vamos dividir o processo de busca de códigos QR em etapas claras e fáceis de seguir:

## Etapa 1: Defina o caminho do documento

Primeiro, especifique o caminho para o documento que contém os códigos QR que você deseja pesquisar:

```csharp
string filePath = "sample_multiple_signatures.docx";
```

## Etapa 2: Inicializar o Objeto de Assinatura

Crie uma instância do `Signature` classe passando o caminho do documento:

```csharp
using (Signature signature = new Signature(filePath))
{
    // O código de pesquisa do código QR será adicionado aqui
}
```

## Etapa 3: Pesquisar assinaturas de código QR

Use o `Search` método com o tipo de assinatura apropriado para encontrar códigos QR no documento:

```csharp
// Pesquise assinaturas de código QR dentro do documento
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

## Etapa 4: Processar e exibir resultados

Percorra as assinaturas de código QR encontradas e acesse suas propriedades:

```csharp
// Exibir informações sobre códigos QR encontrados
Console.WriteLine($"\nSource document contains {signatures.Count} QR code signature(s):");

foreach (var qrCodeSignature in signatures)
{
    Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
    Console.WriteLine($"Content: {qrCodeSignature.Text}");
    Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
    Console.WriteLine();
}
```

## Exemplo completo

Aqui está um exemplo prático abrangente que demonstra o processo completo de busca de códigos QR em um documento:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;

namespace QrCodeSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Caminho do documento - atualize com o caminho do seu arquivo
            string filePath = "sample_multiple_signatures.docx";
            
            // Inicializar instância de assinatura
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Pesquisar assinaturas de código QR no documento
                    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
                    
                    // Exibir resultados da pesquisa
                    Console.WriteLine($"\nSource document ['{filePath}'] contains {signatures.Count} QR code signature(s):");
                    
                    foreach (var qrCodeSignature in signatures)
                    {
                        Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
                        Console.WriteLine($"Content: {qrCodeSignature.Text}");
                        Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
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

## Técnicas avançadas de pesquisa de código QR

### Pesquisando com critérios específicos

Para pesquisas mais direcionadas, você pode usar `QrCodeSearchOptions` para personalizar seus critérios de pesquisa:

```csharp
// Crie opções de pesquisa de código QR com critérios específicos
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    // Pesquisar apenas em páginas específicas
    AllPages = false,
    PageNumber = 1,
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // Filtrar por conteúdo do código QR
    Text = "Invoice",
    MatchType = TextMatchType.Contains,
    
    // Filtrar por tipos específicos de código QR
    EncodeType = QrCodeTypes.QR,
    
    // Defina uma área específica para pesquisar
    Rectangle = new Rectangle(100, 100, 400, 400)
};

// Pesquisar com opções específicas
List<QrCodeSignature> filteredSignatures = signature.Search<QrCodeSignature>(options);
```

### Processando dados de código QR

Você pode implementar o processamento personalizado para dados de código QR com base nos requisitos do seu aplicativo:

```csharp
foreach (var qrCode in signatures)
{
    // Extraia e processe dados de código QR com base no conteúdo
    string qrContent = qrCode.Text;
    
    if (qrContent.StartsWith("URL:"))
    {
        // Processar dados de URL
        string url = qrContent.Substring(4);
        Console.WriteLine($"Found URL in QR code: {url}");
    }
    else if (qrContent.StartsWith("CONTACT:"))
    {
        // Informações de contato do processo
        string contact = qrContent.Substring(8);
        Console.WriteLine($"Found contact information in QR code: {contact}");
    }
    else if (qrContent.StartsWith("INVOICE:"))
    {
        // Processar informações de fatura
        string invoiceData = qrContent.Substring(8);
        Console.WriteLine($"Found invoice information in QR code: {invoiceData}");
        
        // Analisar e validar dados da fatura
        if (ValidateInvoiceData(invoiceData))
        {
            Console.WriteLine("Invoice data is valid!");
        }
        else
        {
            Console.WriteLine("Warning: Invalid invoice data detected!");
        }
    }
}

// Exemplo de método de validação
static bool ValidateInvoiceData(string data)
{
    // Implemente sua lógica de validação
    return !string.IsNullOrEmpty(data) && data.Contains("ID") && data.Contains("Amount");
}
```

### Implementando a verificação de segurança

Os códigos QR são frequentemente usados para fins de autenticação. Veja como implementar a verificação básica de segurança:

```csharp
// Verifique se o documento contém um código QR de autenticação válido
bool hasValidAuthQrCode = false;

foreach (var qrCode in signatures)
{
    if (qrCode.Text.StartsWith("AUTH:"))
    {
        string authCode = qrCode.Text.Substring(5);
        
        // Verifique o código de autenticação (por exemplo, em um banco de dados ou lista predefinida)
        if (VerifyAuthCode(authCode))
        {
            hasValidAuthQrCode = true;
            Console.WriteLine("Document contains valid authentication QR code!");
            break;
        }
    }
}

if (!hasValidAuthQrCode)
{
    Console.WriteLine("Warning: Document does not contain a valid authentication QR code!");
}

// Exemplo de método de verificação
static bool VerifyAuthCode(string code)
{
    // Implemente sua lógica de verificação
    // Isso pode ser uma consulta de banco de dados, chamada de API ou comparação com valores predefinidos
    return code == "A7B82C3D" || code == "X9Y8Z7W6";
}
```

### Extraindo imagens de código QR

Você pode extrair imagens de código QR de documentos para processamento ou exibição posterior:

```csharp
// Salvar imagens de código QR no disco
foreach (var qrCode in signatures)
{
    if (qrCode.Content != null)
    {
        // Crie um nome de arquivo exclusivo com base no número da página e na posição
        string outputPath = $"QrCode_P{qrCode.PageNumber}_X{qrCode.Left}_Y{qrCode.Top}.png";
        
        // Salvar os dados da imagem
        File.WriteAllBytes(outputPath, qrCode.Content);
        Console.WriteLine($"Saved QR code image to {outputPath}");
    }
}
```

## Conclusão

Neste guia completo, exploramos como pesquisar assinaturas de código QR em documentos usando o GroupDocs.Signature para .NET. Da pesquisa básica às técnicas avançadas, agora você tem o conhecimento necessário para implementar um tratamento robusto de código QR em seus aplicativos .NET. A API do GroupDocs.Signature fornece uma estrutura poderosa e flexível para trabalhar com vários tipos de assinatura, incluindo códigos QR, em diferentes formatos de documento.

Ao aproveitar esses recursos, você pode aprimorar os processos de verificação de documentos, implementar sistemas de autenticação e extrair informações valiosas incorporadas em códigos QR, tudo dentro de seus aplicativos .NET.

## Perguntas frequentes

### Quais formatos de código QR são suportados pelo GroupDocs.Signature?

GroupDocs.Signature suporta vários formatos de código QR, incluindo código QR padrão, micro código QR e outros padrões comuns de código QR. O formato específico pode ser acessado através do `EncodeType` propriedade do `QrCodeSignature` objeto.

### Posso pesquisar códigos QR em documentos protegidos por senha?

Sim, o GroupDocs.Signature oferece suporte à pesquisa de códigos QR em documentos protegidos por senha, fornecendo a senha ao inicializar o `Signature` objeto:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Pesquisar por códigos QR
}
```

### Como posso filtrar códigos QR com base em seu conteúdo?

Você pode filtrar códigos QR com base em seu conteúdo usando o `Text` e `MatchType` propriedades de `QrCodeSearchOptions`:

```csharp
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    Text = "Invoice",
    MatchType = TextMatchType.Contains // Outras opções: Exato, Começa com, Termina com
};
```

### O GroupDocs.Signature pode detectar códigos QR danificados ou parcialmente visíveis?

O GroupDocs.Signature tem alguma capacidade de detectar códigos QR parcialmente visíveis, mas códigos QR muito danificados podem não ser reconhecidos. A precisão da detecção depende da qualidade e da visibilidade do código QR no documento.

### Quais formatos de documento são suportados para pesquisa de código QR?

O GroupDocs.Signature suporta pesquisa de código QR em vários formatos de documentos, incluindo PDF, documentos do Microsoft Office (Word, Excel, PowerPoint), imagens (JPEG, PNG, TIFF) e muitos outros.

## Veja também

* [Referência de API](https://reference.groupdocs.com/signature/net/)
* [Exemplos de código no GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentação do produto](https://docs.groupdocs.com/signature/net/)
* [Página do produto](https://products.groupdocs.com/signature/net/)
* [Baixe a última versão](https://releases.groupdocs.com/signature/net/)
* [Artigos do blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Fórum de Suporte Gratuito](https://forum.groupdocs.com/c/signature/13)
* [Licença Temporária](https://purchase.groupdocs.com/temporary-license/)