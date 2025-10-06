---
"description": "Domine a busca por assinaturas digitais em documentos com o GroupDocs.Signature para .NET. Aumente a segurança e a verificação de documentos com nosso guia passo a passo detalhado."
"linktitle": "Pesquisar por Assinaturas Digitais"
"second_title": "API .NET do GroupDocs.Signature"
"title": "Pesquisar assinaturas digitais em documentos"
"url": "/pt/net/signature-searching/search-for-digital-signatures/"
"weight": 11
type: docs
---
## Introdução

No cenário digital atual, garantir a autenticidade e a integridade de documentos é fundamental para empresas e organizações. As assinaturas digitais fornecem um mecanismo robusto para verificar a autenticidade de documentos e detectar modificações não autorizadas. O GroupDocs.Signature para .NET oferece uma solução abrangente para trabalhar com assinaturas digitais em diversos formatos de documentos, permitindo que os desenvolvedores integrem perfeitamente a funcionalidade de assinatura em seus aplicativos .NET.

Este tutorial guiará você pelo processo de busca de assinaturas digitais em documentos usando o GroupDocs.Signature for .NET, fornecendo explicações detalhadas e exemplos práticos de código.

## Pré-requisitos

Antes de mergulhar nos detalhes da implementação, certifique-se de ter os seguintes pré-requisitos:

1. GroupDocs.Signature para .NET: Baixe e instale a biblioteca de [aqui](https://releases.groupdocs.com/signature/net/).
   
2. Ambiente de desenvolvimento: configure um ambiente de desenvolvimento .NET com o Visual Studio ou seu IDE preferido.
   
3. Documentos de amostra: prepare documentos de amostra contendo assinaturas digitais para fins de teste.

4. Conhecimento básico: Familiaridade com a linguagem de programação C# e os fundamentos do framework .NET.

## Importar namespaces

Comece importando os namespaces necessários para acessar a funcionalidade fornecida pelo GroupDocs.Signature para .NET:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Agora, vamos dividir o processo de busca de assinaturas digitais em etapas claras e gerenciáveis:

## Etapa 1: Inicializar objeto de assinatura

Comece criando uma instância do `Signature` classe, passando o caminho para seu documento:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // O código para pesquisa de assinaturas digitais será adicionado aqui
}
```

## Etapa 2: Pesquisar assinaturas digitais

Em seguida, use o `Search` método com o `SignatureType.Digital` parâmetro para buscar assinaturas digitais no documento:

```csharp
// Pesquisar assinaturas digitais no documento
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```

## Etapa 3: Processar e exibir resultados

Por fim, processe os resultados da pesquisa e exiba informações relevantes sobre as assinaturas digitais encontradas:

```csharp
Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
foreach (var digitalSignature in signatures)
{
    Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
    Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
    Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
    Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
    Console.WriteLine();
}
```

## Exemplo completo

Aqui está um exemplo completo e funcional que demonstra como pesquisar assinaturas digitais em um documento:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SearchDigitalSignatures
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
                // Pesquisar assinaturas digitais no documento
                List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
                
                // Exibir resultados da pesquisa
                Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
                
                if (signatures.Count > 0)
                {
                    foreach (var digitalSignature in signatures)
                    {
                        Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
                        Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
                        Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
                        Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
                        Console.WriteLine();
                    }
                }
                else
                {
                    Console.WriteLine("No digital signatures found in the document.");
                }
            }
        }
    }
}
```

## Opções de pesquisa avançada

Para pesquisas mais direcionadas, você pode usar `DigitalSearchOptions` para personalizar os critérios de pesquisa:

```csharp
// Crie opções de pesquisa digital
DigitalSearchOptions options = new DigitalSearchOptions()
{
    // Pesquise apenas em páginas específicas (por exemplo, páginas 1 e 2)
    PageNumber = 1,
    PagesSetup = new PagesSetup() { Pages = new List<int> { 1, 2 } },
    
    // Filtrar por comentários em assinaturas digitais
    Comments = "Approved",
    
    // Definir intervalo de data e hora para pesquisa
    SignDateTimeFrom = new DateTime(2022, 1, 1),
    SignDateTimeTo = DateTime.Now
};

// Pesquisar com opções específicas
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(options);
```

## Trabalhando com informações de certificado

Assinaturas digitais contêm informações valiosas de certificado que você pode acessar e validar:

```csharp
foreach (var digitalSignature in signatures)
{
    if (digitalSignature.Certificate != null)
    {
        // Propriedades do certificado de acesso
        Console.WriteLine($"Certificate Valid From: {digitalSignature.Certificate.NotBefore}");
        Console.WriteLine($"Certificate Valid To: {digitalSignature.Certificate.NotAfter}");
        
        // Verifique se o certificado está em um intervalo de datas válido
        bool isDateValid = DateTime.Now >= digitalSignature.Certificate.NotBefore && 
                          DateTime.Now <= digitalSignature.Certificate.NotAfter;
        
        Console.WriteLine($"Certificate Date Validity: {isDateValid}");
        
        // Detalhes do emissor do certificado de acesso
        Console.WriteLine($"Certificate Issuer: {digitalSignature.Certificate.IssuerName}");
    }
}
```

## Conclusão

O GroupDocs.Signature para .NET oferece uma solução poderosa e flexível para pesquisa e validação de assinaturas digitais em documentos. Neste tutorial, exploramos o processo passo a passo de implementação da funcionalidade de pesquisa de assinaturas digitais em aplicativos .NET, equipando você com o conhecimento necessário para aprimorar a segurança e a verificação de integridade de documentos.

Ao utilizar o GroupDocs.Signature, você pode criar sistemas robustos de gerenciamento de documentos que garantem a autenticidade e a integridade dos seus documentos digitais, promovendo confiança e conformidade nos seus processos de negócios.

## Perguntas frequentes

### GroupDocs.Signature pode verificar a validade das assinaturas digitais?

Sim, o GroupDocs.Signature valida automaticamente as assinaturas digitais durante o processo de pesquisa e fornece o status de validação por meio do `IsValid` propriedade do `DigitalSignature` aula.

### Quais formatos de documento suportam pesquisa de assinatura digital?

O GroupDocs.Signature suporta pesquisa de assinatura digital em vários formatos, incluindo PDF, documentos do Microsoft Office (Word, Excel, PowerPoint), formatos OpenOffice e muito mais.

### Posso pesquisar assinaturas digitais em documentos protegidos por senha?

Sim, você pode pesquisar assinaturas digitais em documentos protegidos por senha, fornecendo a senha ao inicializar o `Signature` objeto:

```csharp
LoadOptions loadOptions = new LoadOptions() { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Pesquisar assinaturas digitais
}
```

### Como posso verificar se uma assinatura digital foi criada por uma pessoa específica?

Você pode examinar o nome do assunto do certificado e outras propriedades para verificar a identidade do signatário:

```csharp
foreach (var signature in signatures)
{
    if (signature.Certificate?.SubjectName?.Contains("John Doe") == true)
    {
        Console.WriteLine("Found signature by John Doe");
    }
}
```

### Posso extrair a chave pública de um certificado de assinatura digital?

Sim, você pode acessar as informações da chave pública por meio das propriedades do certificado:

```csharp
if (signature.Certificate != null)
{
    // Acessar informações de chave pública
    Console.WriteLine($"Public Key: {signature.Certificate.GetPublicKeyString()}");
}
```

## Veja também

* [Referência de API](https://reference.groupdocs.com/signature/net/)
* [Exemplos de código](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentação do produto](https://docs.groupdocs.com/signature/net/)
* [Página do produto](https://products.groupdocs.com/signature/net/)
* [Baixe a última versão](https://releases.groupdocs.com/signature/net/)
* [Artigos do blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Fórum de Suporte](https://forum.groupdocs.com/c/signature/13)
* [Licença Temporária](https://purchase.groupdocs.com/temporary-license/)