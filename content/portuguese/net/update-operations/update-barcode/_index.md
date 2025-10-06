---
"description": "Aprenda a atualizar programaticamente assinaturas de código de barras em vários formatos de documento usando o GroupDocs.Signature para .NET. Tutorial completo para desenvolvedores que criam soluções de gerenciamento de documentos."
"linktitle": "Atualizar código de barras"
"second_title": "API .NET do GroupDocs.Signature"
"title": "Atualizar assinaturas de código de barras em documentos"
"url": "/pt/net/update-operations/update-barcode/"
"weight": 10
type: docs
---
## Introdução
Assinaturas de código de barras são amplamente utilizadas em fluxos de trabalho de documentos digitais para codificar dados estruturados, permitindo rastreamento, identificação e validação eficientes. O GroupDocs.Signature para .NET é uma solução abrangente de assinatura de documentos que permite aos desenvolvedores integrar funcionalidades avançadas de assinatura em seus aplicativos, incluindo a capacidade de atualizar assinaturas de código de barras existentes em documentos.

Este tutorial se concentra especificamente na atualização de assinaturas de código de barras em documentos usando o GroupDocs.Signature para .NET. Se você precisa modificar a posição, o tamanho ou os dados codificados de códigos de barras existentes, este guia o guiará pelo processo com exemplos de código e explicações claras.

## Pré-requisitos
Antes de implementar atualizações de assinatura de código de barras com o GroupDocs.Signature para .NET, certifique-se de ter os seguintes pré-requisitos:

1. Ambiente de desenvolvimento: um ambiente de desenvolvimento .NET funcional, como o Visual Studio 2017 ou posterior.
2. Biblioteca GroupDocs.Signature: A biblioteca GroupDocs.Signature para .NET, que você pode baixar do [página de download](https://releases.groupdocs.com/signature/net/).
3. Conhecimento básico de C#: Familiaridade com conceitos de programação em C#.
4. Documentos de amostra: Documento(s) contendo assinaturas de código de barras que você deseja atualizar.

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

Agora, vamos dividir o processo de atualização de assinaturas de código de barras em etapas gerenciáveis:

## Etapa 1: Configurar caminhos de documentos
Primeiro, defina os caminhos para o seu documento de origem e onde o documento atualizado será salvo:

```csharp
// Caminho para o documento de origem com assinaturas de código de barras
string filePath = "sample_multiple_signatures.docx";

// Obter o nome do arquivo para saída
string fileName = Path.GetFileName(filePath);

// Defina o diretório de saída e o caminho do arquivo
string outputDirectory = Path.Combine("Your Document Directory", "UpdateBarcode");
string outputFilePath = Path.Combine(outputDirectory, fileName);

// Certifique-se de que o diretório de saída exista
Directory.CreateDirectory(outputDirectory);
```

## Etapa 2: Copie o documento de origem
Como a operação de atualização modifica o documento diretamente, crie uma cópia do documento original para preservá-lo:

```csharp
// Crie uma cópia do documento original
File.Copy(filePath, outputFilePath, true);
```

## Etapa 3: Inicializar a instância de assinatura
Crie uma instância do `Signature` classe para trabalhar com o documento:

```csharp
// Inicialize a instância da assinatura com o caminho do arquivo de saída
using (Signature signature = new Signature(outputFilePath))
{
    // As operações de assinatura serão realizadas aqui
}
```

## Etapa 4: Configurar opções de pesquisa de código de barras
Configure as opções de pesquisa para encontrar assinaturas de código de barras existentes no documento:

```csharp
// Configurar opções de pesquisa para assinaturas de código de barras
BarcodeSearchOptions options = new BarcodeSearchOptions()
{
    // Você pode filtrar por conteúdo de texto
    Text = "12345",
    MatchType = TextMatchType.Contains
    
    // Descomente para pesquisar em todas as páginas
    // AllPages = verdadeiro
};
```

## Etapa 5: Pesquisar assinaturas de código de barras
Use as opções de pesquisa configuradas para encontrar assinaturas de código de barras no documento:

```csharp
// Pesquisar assinaturas de código de barras
List<BarcodeSignature> signatures = signature.Search<BarcodeSignature>(options);
```

## Etapa 6: Atualizar propriedades de assinatura de código de barras
Se assinaturas de código de barras forem encontradas, atualize suas propriedades conforme necessário:

```csharp
// Verifique se as assinaturas foram encontradas
if (signatures.Count > 0)
{
    // Obtenha a primeira assinatura de código de barras
    BarcodeSignature barcodeSignature = signatures[0];
    
    // Atualizar posição
    barcodeSignature.Left = 100;
    barcodeSignature.Top = 100;
    
    // Atualizar tamanho
    barcodeSignature.Width = 400;
    barcodeSignature.Height = 100;
    
    // Aplicar as atualizações
    bool result = signature.Update(barcodeSignature);
    
    // Verifique o resultado
    if (result)
    {
        Console.WriteLine($"Signature with Barcode '{barcodeSignature.Text}' and encode type '{barcodeSignature.EncodeType.TypeName}' was updated in the document ['{fileName}'].");
    }
    else
    {
        Console.WriteLine($"Signature was not updated in the document! Signature with Barcode '{barcodeSignature.Text}' and encode type '{barcodeSignature.EncodeType.TypeName}' was not found!");
    }
}
else
{
    Console.WriteLine("No barcode signatures found in the document.");
}
```

## Exemplo completo
Aqui está um exemplo completo e funcional que demonstra como atualizar uma assinatura de código de barras em um documento:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace UpdateBarcodeSignatureExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Caminho do documento
            string filePath = "sample_multiple_signatures.docx";
            
            // Definir caminho de saída
            string fileName = Path.GetFileName(filePath);
            string outputDirectory = Path.Combine(Environment.CurrentDirectory, "UpdateBarcode");
            string outputFilePath = Path.Combine(outputDirectory, fileName);
            
            // Garantir que o diretório de saída exista
            Directory.CreateDirectory(outputDirectory);
            
            // Crie uma cópia do documento original
            File.Copy(filePath, outputFilePath, true);
            
            // Inicializar instância de assinatura
            using (Signature signature = new Signature(outputFilePath))
            {
                // Configurar opções de pesquisa
                BarcodeSearchOptions options = new BarcodeSearchOptions
                {
                    Text = "12345",
                    MatchType = TextMatchType.Contains
                };
                
                // Pesquisar assinaturas de código de barras
                List<BarcodeSignature> signatures = signature.Search<BarcodeSignature>(options);
                
                // Verifique se as assinaturas foram encontradas
                if (signatures.Count > 0)
                {
                    // Obtenha a primeira assinatura
                    BarcodeSignature barcodeSignature = signatures[0];
                    
                    // Atualizar posição e tamanho
                    barcodeSignature.Left = 100;
                    barcodeSignature.Top = 100;
                    barcodeSignature.Width = 400;
                    barcodeSignature.Height = 100;
                    
                    // Aplicar as atualizações
                    bool result = signature.Update(barcodeSignature);
                    
                    // Verifique o resultado
                    if (result)
                    {
                        Console.WriteLine($"Barcode signature was successfully updated in document '{fileName}'.");
                        Console.WriteLine($"Barcode text: {barcodeSignature.Text}");
                        Console.WriteLine($"Encode type: {barcodeSignature.EncodeType.TypeName}");
                        Console.WriteLine($"New position: {barcodeSignature.Left}x{barcodeSignature.Top}");
                        Console.WriteLine($"New size: {barcodeSignature.Width}x{barcodeSignature.Height}");
                        Console.WriteLine($"Output file path: {outputFilePath}");
                    }
                    else
                    {
                        Console.WriteLine("Failed to update barcode signature!");
                    }
                }
                else
                {
                    Console.WriteLine("No barcode signatures found in the document.");
                }
            }
            
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## Personalização avançada de assinatura de código de barras
O GroupDocs.Signature oferece opções adicionais para personalizar assinaturas de código de barras além da posição e tamanho básicos:

### Ajustando propriedades de aparência
Personalize os aspectos visuais do código de barras:

```csharp
// Definir cor de primeiro plano (cor do código de barras)
barcodeSignature.ForeColor = System.Drawing.Color.Blue;

// Definir cor de fundo
barcodeSignature.BackgroundColor = System.Drawing.Color.LightYellow;

// Ajustar transparência
barcodeSignature.Opacity = 0.8;
```

### Adicionando Bordas
Melhore o código de barras com bordas personalizadas:

```csharp
barcodeSignature.Border.Color = System.Drawing.Color.Red;
barcodeSignature.Border.DashStyle = System.Drawing.Drawing2D.DashStyle.Dash;
barcodeSignature.Border.Weight = 2;
barcodeSignature.Border.Visible = true;
```

### Girando o código de barras
Gire a assinatura do código de barras para um ângulo específico:

```csharp
barcodeSignature.Angle = 30; // Girar 30 graus
```

## Conclusão
O GroupDocs.Signature para .NET oferece uma solução poderosa e flexível para atualizar assinaturas de código de barras em documentos. Seguindo as etapas descritas neste tutorial, os desenvolvedores podem implementar com eficiência a funcionalidade de atualização de assinaturas de código de barras em seus aplicativos .NET, aprimorando os recursos de gerenciamento e automação de documentos.

Com seu conjunto abrangente de recursos e API intuitiva, o GroupDocs.Signature permite que os desenvolvedores criem soluções sofisticadas de assinatura de documentos que atendem aos requisitos de aplicativos empresariais modernos, garantindo ao mesmo tempo a integridade e a acessibilidade dos documentos.

## Perguntas frequentes
### Posso atualizar várias assinaturas de código de barras em um único documento?
Sim, o GroupDocs.Signature permite atualizar várias assinaturas de código de barras no mesmo documento. Após pesquisar assinaturas, você pode iterar pela lista resultante e atualizar cada assinatura de código de barras individualmente.

### O GroupDocs.Signature suporta diferentes formatos de código de barras?
Sim, o GroupDocs.Signature suporta uma ampla variedade de formatos de código de barras, incluindo códigos de barras lineares (Código 128, Código 39, EAN, UPC, etc.) e códigos de barras 2D (Código QR, Matriz de Dados, PDF417, etc.).

### Existe uma versão de teste disponível para o GroupDocs.Signature para .NET?
Sim, você pode baixar uma versão de teste gratuita no [Site do GroupDocs](https://releases.groupdocs.com/signature/net/) para avaliar os recursos da biblioteca antes de fazer uma compra.

### Posso converter um tipo de código de barras para outro ao atualizar?
A conversão direta entre tipos de código de barras não é suportada durante as atualizações. No entanto, você pode fazer isso excluindo o código de barras existente e adicionando um novo com o formato desejado.

### A atualização de um código de barras afeta sua capacidade de leitura?
Ao atualizar propriedades do código de barras, como tamanho e posição, o GroupDocs.Signature mantém a integridade da leitura do código de barras. No entanto, tamanhos extremamente pequenos ou ângulos de rotação substanciais podem afetar o desempenho da leitura com alguns leitores.

### Onde posso encontrar suporte adicional para GroupDocs.Signature para .NET?
Você pode encontrar suporte abrangente por meio dos seguintes recursos:
- [Documentação da API](https://docs.groupdocs.com/signature/net/)
- [Referência de API](https://reference.groupdocs.com/signature/net/)
- [Exemplos do GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Fórum de Suporte](https://forum.groupdocs.com/c/signature/13)
- [Blogue](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Suporte gratuito](https://forum.groupdocs.com/c/signature)
- [Licença Temporária](https://purchase.groupdocs.com/temporary-license/)