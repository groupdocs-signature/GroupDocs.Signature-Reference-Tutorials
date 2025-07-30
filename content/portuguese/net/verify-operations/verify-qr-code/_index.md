---
"description": "Aprenda a verificar códigos QR em documentos usando o GroupDocs.Signature para .NET. Guia completo com exemplos de código e práticas recomendadas para autenticação de documentos."
"linktitle": "Verificar código QR"
"second_title": "API .NET do GroupDocs.Signature"
"title": "Verificar código QR em documentos"
"url": "/pt/net/verify-operations/verify-qr-code/"
"weight": 12
---

## Introdução

A segurança de documentos é um aspecto crítico das operações comerciais modernas. Os códigos QR tornaram-se um método cada vez mais popular para incorporar informações em documentos cuja autenticidade pode ser verificada. O GroupDocs.Signature para .NET oferece uma solução poderosa e flexível para verificar códigos QR incorporados em documentos de diversos formatos.

Este tutorial abrangente guiará você pelo processo de implementação da verificação de código QR em seus aplicativos .NET, garantindo que seus documentos mantenham sua integridade e autenticidade.

## Pré-requisitos

Antes de implementar a funcionalidade de verificação de código QR, certifique-se de ter os seguintes pré-requisitos:

1. GroupDocs.Signature para .NET: Baixe e instale a biblioteca do [página de download](https://releases.groupdocs.com/signature/net/).
2. Ambiente de desenvolvimento: Visual Studio ou qualquer ambiente de desenvolvimento .NET compatível.
3. Documento de teste: um documento contendo assinaturas de código QR para fins de verificação.
4. Conhecimento básico: Familiaridade com programação em C# e conceitos do framework .NET.

## Importar namespaces

Comece importando os namespaces necessários para acessar a funcionalidade GroupDocs.Signature:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Processo de verificação de código QR passo a passo

Siga estas etapas detalhadas para verificar os códigos QR em seus documentos:

### Etapa 1: especifique o caminho do documento

```csharp
// Forneça o caminho para o documento que contém as assinaturas do código QR
string filePath = "sample_multiple_signatures.docx";
```

Certifique-se de substituir o caminho de exemplo pelo caminho real para o seu documento.

### Etapa 2: Inicializar o Objeto de Assinatura

```csharp
// Crie uma instância de assinatura passando o caminho do documento
using (Signature signature = new Signature(filePath))
{
    // código de verificação será implementado aqui
}
```

A classe Signature é o principal ponto de entrada para todas as operações na API GroupDocs.Signature.

### Etapa 3: Configurar opções de verificação de código QR

```csharp
// Definir opções de verificação de código QR
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // Verifique todas as páginas do documento
    Text = "John",   // Texto para verificar dentro do código QR
    MatchType = TextMatchType.Contains // Especifique os critérios de correspondência de texto
};
```

As opções de verificação permitem que você defina critérios específicos para o processo de verificação:
- `AllPages`: Defina como verdadeiro para verificar todas as páginas do documento (comportamento padrão)
- `Text`: O conteúdo do texto a ser correspondido dentro do código QR
- `MatchType`: O método para correspondência de texto (Contém, Exato, Começa com, etc.)

### Etapa 4: Executar o processo de verificação

```csharp
// Executar verificação
VerificationResult result = signature.Verify(options);
```

Isso executa o processo de verificação com base nas opções que você especificou.

### Etapa 5: Resultados da verificação do processo

```csharp
// Verifique o resultado da verificação e processe de acordo
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
    
    // Exibir informações sobre assinaturas bem-sucedidas
    foreach (QrCodeSignature signature in result.Succeeded)
    {
        Console.WriteLine($"Found valid QR Code signature with text: {signature.Text}");
        Console.WriteLine($"QR Code type: {signature.EncodeType.TypeName}");
        Console.WriteLine($"Location: Page {signature.PageNumber}, {signature.Left}x{signature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

O tratamento adequado do resultado da verificação permite que seu aplicativo tome as ações apropriadas com base no resultado da verificação.

## Exemplo completo

Aqui está um exemplo completo e funcional que demonstra a verificação do código QR:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace GroupDocs.Signature.Examples
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
                // Configurar opções de verificação
                QrCodeVerifyOptions options = new QrCodeVerifyOptions()
                {
                    AllPages = true,
                    Text = "John",
                    MatchType = TextMatchType.Contains
                };
                
                // Verificar assinaturas de documentos
                VerificationResult result = signature.Verify(options);
                
                // Resultados da verificação do processo
                if (result.IsValid)
                {
                    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
                    
                    foreach (QrCodeSignature qrSignature in result.Succeeded)
                    {
                        Console.WriteLine($"Found valid QR Code with text: {qrSignature.Text}");
                    }
                }
                else
                {
                    Console.WriteLine($"Document {filePath} failed verification process.");
                }
            }
        }
    }
}
```

## Opções de verificação avançadas

O GroupDocs.Signature fornece opções adicionais para cenários de verificação mais complexos:

### Verificando tipos específicos de código QR

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    EncodeType = QrCodeTypes.QR,  // Verifique apenas códigos QR padrão
    Text = "Confidential",
    MatchType = TextMatchType.Exact
};
```

### Verificando em páginas específicas

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = false,
    PageNumber = 2,  // Verifique apenas na página 2
    Text = "Approved"
};
```

### Usando expressões regulares para verificação

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    Text = "INV-\\d{6}",  // Correspondência de números de fatura (por exemplo, INV-123456)
    MatchType = TextMatchType.Regex
};
```

## Melhores práticas para verificação de código QR

1. Sempre valide as entradas: certifique-se de que os caminhos dos documentos e os critérios de verificação sejam válidos antes do processamento.
2. Implemente o tratamento de erros: use blocos try-catch para lidar com possíveis exceções durante a verificação.
3. Considere o desempenho: para documentos grandes, considere verificar páginas específicas em vez do documento inteiro.
4. Resultados da verificação de log: Mantenha registros dos processos de verificação para fins de auditoria.
5. Teste com vários formatos de documentos: certifique-se de que sua verificação funcione em todos os formatos de documentos necessários.

## Conclusão

verificação de códigos QR em documentos é um aspecto essencial para garantir a autenticidade e a integridade dos documentos. O GroupDocs.Signature para .NET fornece uma API abrangente e intuitiva para implementar a verificação de códigos QR em seus aplicativos .NET.

Seguindo este tutorial, você aprendeu como:
- Configurar e inicializar o processo de verificação
- Especifique vários critérios de verificação
- Processar e interpretar os resultados da verificação
- Implementar opções de verificação avançadas

Esse conhecimento permite que você aumente a segurança e a confiabilidade dos seus sistemas de gerenciamento de documentos.

## Perguntas frequentes

### O GroupDocs.Signature pode verificar vários códigos QR em um único documento?
Sim, o GroupDocs.Signature pode verificar vários códigos QR em um único documento. Os resultados da verificação incluirão todos os códigos QR correspondentes.

### Quais formatos de documento são suportados para verificação de código QR?
GroupDocs.Signature suporta uma ampla variedade de formatos de documentos, incluindo PDF, Word (DOC, DOCX), Excel (XLS, XLSX), PowerPoint (PPT, PPTX), imagens e muito mais.

### Posso verificar códigos QR com criptografia ou formatação específica?
Sim, o GroupDocs.Signature oferece opções para verificar códigos QR com tipos específicos de codificação e padrões de formatação de conteúdo.

### É possível verificar códigos QR criados por aplicativos de terceiros?
Sim, o GroupDocs.Signature pode verificar códigos QR padrão gerados pela maioria dos aplicativos, desde que sigam os formatos de código QR padrão.

### Como lidar com códigos QR que contêm dados binários em vez de texto?
O GroupDocs.Signature oferece opções para verificar códigos QR com dados binários por meio de `BinaryData` propriedade das opções de verificação.

### Recursos relacionados
* [Referência da API GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [Downloads do GroupDocs.Signature](https://releases.groupdocs.com/signature/net/)
* [Exemplos de código no GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentação](https://docs.groupdocs.com/signature/net/)
* [Página do produto](https://products.groupdocs.com/signature/net/)
* [Artigos do blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Fórum de Suporte](https://forum.groupdocs.com/c/signature/13)
* [Licença Temporária](https://purchase.groupdocs.com/temporary-license/)