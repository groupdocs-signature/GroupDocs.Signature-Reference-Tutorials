---
"date": "2025-05-07"
"description": "Aprenda a assinar imagens DICOM com códigos QR usando o GroupDocs.Signature para .NET. Este guia aborda a configuração, implementação e verificação de assinaturas de códigos QR em imagens médicas."
"title": "Como assinar imagens DICOM com códigos QR usando o GroupDocs.Signature para .NET - Um guia completo"
"url": "/pt/net/qr-code-signatures/groupdocs-signature-net-dicom-images-qr-codes/"
"weight": 1
type: docs
---
# Como assinar imagens DICOM com códigos QR usando o GroupDocs.Signature para .NET: um guia completo

Procurando um método seguro para autenticar seus arquivos DICOM? Este guia detalhado mostrará como usar o GroupDocs.Signature for .NET para integrar assinaturas de código QR em imagens DICOM. Ideal para profissionais de saúde, desenvolvedores e qualquer pessoa que trabalhe com documentos médicos digitais, este tutorial abrange desde a configuração até a implementação.

## O que você aprenderá:
- Configurando seu ambiente de desenvolvimento com GroupDocs.Signature para .NET.
- Instruções passo a passo sobre como assinar imagens DICOM usando códigos QR.
- Métodos para verificar e pesquisar assinaturas de código QR em arquivos DICOM.
- Técnicas para gerar visualizações de documentos assinados para fins de revisão.
- Melhores práticas para otimizar o desempenho e gerenciar recursos de forma eficaz.

Vamos começar com os pré-requisitos!

## Pré-requisitos

Para usar o GroupDocs.Signature para .NET, certifique-se de que seu ambiente esteja pronto. Veja o que você precisa:

### Bibliotecas e versões necessárias
- **GroupDocs.Signature para .NET**Garanta a compatibilidade com seu framework .NET.

### Requisitos de configuração do ambiente
- Um ambiente de desenvolvimento no Windows ou Linux.
- Visual Studio ou outro IDE compatível com .NET instalado.

### Pré-requisitos de conhecimento
- Noções básicas de programação em C#.
- Familiaridade com E/S de arquivos em aplicativos .NET.

## Configurando GroupDocs.Signature para .NET

Instale a biblioteca GroupDocs.Signature usando seu método preferido:

**Usando o .NET CLI:**
```bash
dotnet add package GroupDocs.Signature
```

**Gerenciador de pacotes:**
```powershell
Install-Package GroupDocs.Signature
```

**Interface do Gerenciador de Pacotes NuGet:**
- Procure por "GroupDocs.Signature" e instale a versão mais recente.

### Aquisição de Licença

Comece com um teste gratuito para explorar os recursos. Para uso prolongado, considere adquirir uma licença temporária ou completa da [Documentos do Grupo](https://purchase.groupdocs.com/buy).

Uma vez instalada, inicialize a biblioteca:

```csharp
using GroupDocs.Signature;
// Inicialize o objeto Signature com o caminho do seu arquivo DICOM.
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample.dicom");
```

## Guia de Implementação

### Assine a imagem DICOM com código QR

#### Visão geral
Adicione assinaturas de código QR para garantir autenticidade e rastreabilidade de documentos médicos.

**Etapa 1: Inicializar objeto de assinatura**

```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY\\sample.dicom";
using (Signature signature = new Signature(filePath))
{
    // Prosseguir com as operações de assinatura...
}
```

**Etapa 2: Criar opções de sinalização de código QR**

Configure propriedades como texto, tamanho e alinhamento.

```csharp
QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues")
{
    AllPages = true,
    Width = 100,
    Height = 100,
    VerticalAlignment = VerticalAlignment.Bottom,
    HorizontalAlignment = HorizontalAlignment.Right,
    Margin = new Padding() { Right = 5, Left = 5 }
};
```

**Etapa 3: Adicionar metadados XMP**

Melhore o documento com metadados adicionais.

```csharp
DicomSaveOptions dicomSaveOptions = new DicomSaveOptions()
{
    XmpEntries = new List<DicomXmpEntry>() { new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4") }
};
```

**Etapa 4: Assine o documento**

Execute a assinatura e salve.

```csharp
SignResult signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY\\SignedDicom", options, dicomSaveOptions);
```

### Obter informações do documento

Recupere metadados de arquivos DICOM assinados para garantir a integridade dos dados.

**Visão geral:**
Acesse informações de documentos e assinaturas de metadados XMP para verificação.

**Etapa 1: recuperar informações do documento**

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    IDocumentInfo signedDocumentInfo = signature.GetDocumentInfo();
}
```

**Etapa 2: iterar e imprimir dados XMP**

Exibir detalhes de metadados.

```csharp
foreach (var item in signedDocumentInfo.MetadataSignatures)
{
    Console.WriteLine(item.ToString());
}
```

### Verificar assinaturas DICOM

Valide a autenticidade das assinaturas de código QR em imagens DICOM.

**Visão geral:**
Certifique-se de que as assinaturas estejam corretas e autênticas.

**Etapa 1: Criar opções de verificação de código QR**

Defina opções correspondentes ao texto específico nos códigos QR.

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true,
    Text = "Patient #36363393",
    MatchType = TextMatchType.Contains
};
```

**Etapa 2: Verificar assinaturas**

Verifique se as assinaturas atendem aos critérios.

```csharp
VerificationResult result = signature.Verify(options);

if (result.IsValid)
{
    Console.WriteLine($"DICOM {filePath} has {result.Succeeded.Count} successfully verified signatures!");
}
```

### Pesquisar assinaturas no DICOM

Localize assinaturas de código QR em imagens DICOM assinadas.

**Visão geral:**
Encontre com eficiência todas as assinaturas de código QR para gerenciar a autenticidade dos documentos.

**Etapa 1: Pesquisar assinaturas de código QR**

```csharp
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

**Etapa 2: iterar e imprimir detalhes da assinatura**

Revise os detalhes de cada assinatura encontrada.

```csharp
foreach (var QrCodeSignature in signatures)
{
    Console.WriteLine($"QRCode signature found at page {QrCodeSignature.PageNumber} with type {QrCodeSignature.EncodeType.TypeName} and text {QrCodeSignature.Text}");
}
```

### Gerar visualização do DICOM assinado

Crie visualizações prévias para verificação.

**Visão geral:**
Gere visualizações de imagens para verificar conteúdo sem software especializado.

**Etapa 1: Definir métodos de fluxo**

Configure métodos para gerenciamento de fluxo de arquivos durante a geração de visualização.

```csharp
Stream CreatePageStream(PreviewPageData pageData)
{
    string imageFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignDicomImageAdvanced", $"preview-{pageData.PageNumber}.jpg");
    var folder = Path.GetDirectoryName(imageFilePath);
    if (!Directory.Exists(folder))
    {
        Directory.CreateDirectory(folder);
    }
    return new FileStream(imageFilePath, FileMode.Create);
}

void ReleasePageStream(PreviewPageData pageData, Stream pageStream)
{
    pageStream.Dispose();
}
```

**Etapa 2: gerar visualizações**

Execute o processo de geração de pré-visualização.

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    PreviewOptions previewOption = new PreviewOptions(CreatePageStream, ReleasePageStream)
    {
        PreviewFormat = PreviewOptions.PreviewFormats.PNG,
    };

    signature.GeneratePreview(previewOption);
}
```

## Aplicações práticas

1. **Gestão de Registros Médicos**: Autentique registros de pacientes usando assinaturas de código QR para conformidade.
2. **Trilhas de auditoria em sistemas de saúde**: Acompanhe alterações em documentos e verifique a autenticidade com códigos QR.
3. **Compartilhamento Seguro de Dados**: Garanta o compartilhamento seguro de imagens médicas incorporando assinaturas digitais.
4. **Verificação de conformidade**: Verifique regularmente a integridade dos arquivos DICOM para atender aos requisitos legais.
5. **Integração com sistemas EHR**: Integre perfeitamente arquivos DICOM assinados em sistemas de Registros Eletrônicos de Saúde (EHR) para operações simplificadas.