---
"description": "Domine a verificação de assinaturas de texto em aplicativos .NET com o GroupDocs.Signature. Guia de implementação passo a passo com exemplos de código completos e práticas recomendadas."
"linktitle": "Verificar texto"
"second_title": "API .NET do GroupDocs.Signature"
"title": "Verificar assinaturas de texto em documentos"
"url": "/pt/net/verify-operations/verify-text/"
"weight": 13
---

## Introdução

Assinaturas de texto, embora frequentemente mais simples do que assinaturas digitais ou eletrônicas, desempenham um papel crucial no gerenciamento e verificação de documentos. Sejam marcas d'água, texto de rodapé ou padrões de conteúdo específicos, validar a presença e a integridade das assinaturas de texto é um aspecto importante dos processos de verificação de documentos.

O GroupDocs.Signature para .NET fornece uma API poderosa para verificar assinaturas de texto em documentos de diversos formatos. Este tutorial abrangente guiará você pela implementação da funcionalidade de verificação de texto em seus aplicativos .NET, garantindo que seus documentos mantenham sua integridade e autenticidade.

## Pré-requisitos

Antes de implementar a funcionalidade de verificação de texto, certifique-se de ter os seguintes pré-requisitos:

1. GroupDocs.Signature para .NET: Baixe e instale a biblioteca do [página de download](https://releases.groupdocs.com/signature/net/).
2. Ambiente de desenvolvimento .NET: Visual Studio ou qualquer ambiente de desenvolvimento .NET compatível.
3. Conhecimento básico: Familiaridade com programação em C# e conceitos do framework .NET.
4. Documento de teste: Um documento contendo assinaturas de texto para fins de verificação.

## Importar namespaces necessários

Comece importando os namespaces necessários para acessar a funcionalidade GroupDocs.Signature:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Vamos dividir o processo de verificação de texto em etapas claras e gerenciáveis:

## Etapa 1: especifique o caminho do documento

```csharp
// Caminho para o documento que contém as assinaturas de texto
string filePath = "sample_multiple_signatures.docx";
```

Certifique-se de substituir o caminho de exemplo pelo caminho real para o seu documento que contém assinaturas de texto.

## Etapa 2: Inicializar o Objeto de Assinatura

```csharp
// Crie uma instância da classe Signature passando o caminho do documento
using (Signature signature = new Signature(filePath))
{
    // código de verificação será implementado aqui
}
```

A classe Signature é o principal ponto de entrada para todas as operações na API GroupDocs.Signature.

## Etapa 3: Configurar opções de verificação de texto

```csharp
// Definir opções de verificação de texto
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = true,                               // Verifique todas as páginas do documento
    SignatureImplementation = TextSignatureImplementation.Native,
    Text = "signature",                            // Texto a ser verificado
    MatchType = TextMatchType.Contains             // Especificar critérios de correspondência
};
```

As opções de verificação permitem que você defina critérios específicos para o processo de verificação:
- `AllPages`: Defina como verdadeiro para verificar todas as páginas do documento
- `SignatureImplementation`: Especifique como o texto é implementado (Nativo ou Adesivo)
- `Text`: O conteúdo do texto a ser correspondido no documento
- `MatchType`: O método para correspondência de texto (Contém, Exato, Começa com, etc.)

## Etapa 4: Executar o processo de verificação

```csharp
// Executar verificação
VerificationResult result = signature.Verify(options);
```

Isso executa o processo de verificação com base nas opções que você especificou.

## Etapa 5: Resultados da verificação do processo

```csharp
// Verifique o resultado da verificação e processe de acordo
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid text signatures!");
    
    // Exibir informações sobre assinaturas bem-sucedidas
    foreach (TextSignature textSignature in result.Succeeded)
    {
        Console.WriteLine($"\nFound valid text signature:");
        Console.WriteLine($"Text: {textSignature.Text}");
        Console.WriteLine($"Location: Page {textSignature.PageNumber}, {textSignature.Left}x{textSignature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

Este código verifica se a verificação foi bem-sucedida e fornece informações detalhadas sobre as assinaturas de texto que foram verificadas.

## Exemplo completo

Aqui está um exemplo prático completo que demonstra a verificação da assinatura de texto:

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
            
            try
            {
                // Inicializar instância de assinatura
                using (Signature signature = new Signature(filePath))
                {
                    // Configurar opções de verificação
                    TextVerifyOptions options = new TextVerifyOptions()
                    {
                        AllPages = true,
                        SignatureImplementation = TextSignatureImplementation.Native,
                        Text = "signature",
                        MatchType = TextMatchType.Contains
                    };
                    
                    // Verificar assinaturas de documentos
                    VerificationResult result = signature.Verify(options);
                    
                    // Resultados da verificação do processo
                    if(result.IsValid)
                    {
                        Console.WriteLine($"\nDocument {filePath} was verified successfully!");
                        foreach (TextSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature is found with text: {item.Text}");
                            Console.WriteLine($"Location: Page {item.PageNumber}, position {item.Left}x{item.Top}");
                        }
                    }
                    else
                    {
                        Console.WriteLine($"\nDocument {filePath} failed verification process.");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

## Cenários de Verificação Avançados

O GroupDocs.Signature fornece opções adicionais para cenários de verificação mais complexos:

### Usando expressões regulares para verificação

Para uma correspondência de padrões mais flexível, você pode usar expressões regulares:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "Invoice\\s+#\\d{5,6}",  // Correspondência de padrões como "Fatura nº 12345"
    MatchType = TextMatchType.Regex
};
```

### Verificando texto em áreas específicas do documento

Você pode restringir a verificação a áreas específicas do documento:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = false,
    PageNumber = 1,  // Verifique apenas na primeira página
    
    // Definir área para pesquisa (coordenadas em pontos)
    PagesSetup = new PagesSetup() 
    { 
        FirstPage = true,
        LastPage = false,
        OddPages = false,
        EvenPages = false 
    },
    
    // Área do retângulo em milímetros
    Rectangle = new Rectangle(10, 10, 100, 30),
    
    Text = "Confidential"
};
```

### Verificando vários padrões de texto simultaneamente

Você pode criar várias opções de verificação para verificar diferentes padrões de texto:

```csharp
// Crie uma lista de opções de verificação
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// Adicionar primeira verificação de texto
listOptions.Add(new TextVerifyOptions()
{
    Text = "Confidential",
    MatchType = TextMatchType.Exact
});

// Adicionar segunda verificação de texto
listOptions.Add(new TextVerifyOptions()
{
    Text = "Do not copy",
    MatchType = TextMatchType.Contains
});

// Verifique com várias opções
VerificationResult result = signature.Verify(listOptions);
```

### Verificando texto com aparência específica

Você também pode verificar texto com características de formatação específicas:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "APPROVED",
    MatchType = TextMatchType.Exact,
    
    // Verifique propriedades de aparência específicas
    ForegroundColorRGB = System.Drawing.Color.Green,
    Font = new SignatureFont() { FontFamily = "Arial", FontSize = 12, Bold = true }
};
```

## Melhores práticas para verificação de texto

1. Escolha os tipos de correspondência apropriados: selecione o tipo de correspondência correto (Contém, Exato, Regex) com base nos seus requisitos de verificação.
2. Otimize o desempenho: para documentos grandes, considere verificar páginas específicas em vez do documento inteiro.
3. Tratamento de erros: implemente o tratamento de erros adequado para gerenciar cenários inesperados com elegância.
4. Considere a diferenciação entre maiúsculas e minúsculas: tenha cuidado com a diferenciação entre maiúsculas e minúsculas na correspondência de texto, especialmente para verificações críticas.
5. Teste completamente: teste a verificação com vários formatos de documentos e padrões de texto para garantir a compatibilidade.

## Solução de problemas comuns

### Texto não detectado
- Verifique se a formatação ou codificação do texto está afetando a detecção
- Garanta que o texto esteja realmente presente no documento como texto normal (não como imagem)
- Experimente diferentes critérios de correspondência (Contém em vez de Exato)

### Problemas de desempenho
- Otimize a verificação segmentando páginas ou áreas específicas
- Use padrões de texto mais específicos para reduzir falsos positivos

### Falhas de verificação
- Verifique se espaços, caracteres especiais ou formatação estão afetando a correspondência
- Verifique se o texto não faz parte de uma imagem digitalizada (o que requer OCR)
- Garantir que o documento não foi modificado desde que o texto foi adicionado

## Conclusão

A verificação de texto é uma abordagem versátil e prática para autenticação de documentos que pode ser usada isoladamente ou em combinação com outros métodos de verificação. O GroupDocs.Signature para .NET fornece uma API abrangente e fácil de usar para implementar funcionalidades robustas de verificação de texto em seus aplicativos .NET.

Seguindo este guia passo a passo, você aprendeu como:
- Configurar e inicializar o processo de verificação de texto
- Especifique vários critérios de verificação
- Processar e interpretar os resultados da verificação
- Implementar cenários de verificação avançados

Esses recursos permitem que você crie sistemas de processamento de documentos seguros e confiáveis que podem verificar a autenticidade do texto em vários formatos de documento.

## Perguntas frequentes

### O GroupDocs.Signature pode verificar texto em documentos digitalizados?
O GroupDocs.Signature foi projetado principalmente para verificação de texto digital. Para documentos digitalizados, você precisa usar a tecnologia OCR (Reconhecimento Óptico de Caracteres) primeiro para converter as imagens digitalizadas em texto.

### Quais formatos de documento são suportados para verificação de texto?
O GroupDocs.Signature suporta uma ampla variedade de formatos de documentos, incluindo PDF, documentos do Word (DOC, DOCX), planilhas do Excel (XLS, XLSX), apresentações do PowerPoint (PPT, PPTX), imagens e muito mais.

### Posso verificar o texto formatado (negrito, itálico, fontes específicas)?
Sim, o GroupDocs.Signature oferece opções para verificar texto com características de formatação específicas, incluindo família de fonte, tamanho, estilo (negrito, itálico) e cor.

### É possível verificar texto em documentos protegidos por senha?
Sim, o GroupDocs.Signature fornece opções para especificar senhas de documentos ao abrir documentos protegidos para verificação.

### Posso verificar marcas d'água e texto de fundo?
Sim, o GroupDocs.Signature pode verificar vários tipos de assinaturas de texto, incluindo marcas d'água e texto de fundo, dependendo de como foram implementadas no documento.

### Recursos relacionados
* [Referência da API GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [Downloads do GroupDocs.Signature](https://releases.groupdocs.com/signature/net/)
* [Exemplos de código no GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentação](https://docs.groupdocs.com/signature/net/)
* [Página do produto](https://products.groupdocs.com/signature/net/)
* [Artigos do blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Fórum de Suporte](https://forum.groupdocs.com/c/signature/13)
* [Licença Temporária](https://purchase.groupdocs.com/temporary-license/)