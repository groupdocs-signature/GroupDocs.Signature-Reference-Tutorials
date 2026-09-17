---
categories:
- Document Signing
- Healthcare Integration
date: '2026-09-15'
description: Aprenda a assinar PDF com código de barras usando GroupDocs.Signature
  para Java. Guia passo a passo para adicionar Data Matrix e códigos QR em documentos
  de saúde.
keywords:
- sign pdf with barcode
- add qr code pdf
- hibc barcode java
- pdf signing java
- healthcare barcode signing
lastmod: '2026-09-15'
linktitle: Guia de assinatura de PDF HIBC em Java
og_description: Assine PDF com código de barras usando GroupDocs.Signature para Java.
  Aprenda a incorporar Data Matrix e códigos QR em documentos de saúde em poucos passos.
og_image_alt: 'Developer tutorial: sign PDF with HIBC barcode using GroupDocs.Signature
  for Java'
og_title: Assine PDF com código de barras usando HIBC em Java – Guia GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-09-15'
  description: Learn how to sign PDF with barcode using GroupDocs.Signature for Java.
    Step‑by‑step guide for adding Data Matrix and QR codes in healthcare documents.
  headline: Sign PDF with barcode using HIBC in Java
  type: TechArticle
- description: Learn how to sign PDF with barcode using GroupDocs.Signature for Java.
    Step‑by‑step guide for adding Data Matrix and QR codes in healthcare documents.
  name: Sign PDF with barcode using HIBC in Java
  steps:
  - name: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
    text: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
  - name: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
    text: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
  - name: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
    text: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
  - name: '**Apply the signature** to the PDF.'
    text: '**Apply the signature** to the PDF.'
  - name: '**Dispose of resources** to free file handles and avoid memory leaks.'
    text: '**Dispose of resources** to free file handles and avoid memory leaks.'
  - name: '**Import QR‑specific classes**'
    text: '**Import QR‑specific classes**'
  - name: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
    text: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
  - name: '**Sign the document**'
    text: '**Sign the document**'
  type: HowTo
- questions:
  - answer: Yes, it also supports DOCX, XLSX, PPTX, PNG, JPEG, and TIFF with the same
      barcode‑signing API.
    question: Can GroupDocs.Signature sign file types other than PDF?
  - answer: Verify that your HIBC string follows the exact HIBCC syntax, use the online
      validator, and ensure you’re using the correct `QrCodeTypes` constant for the
      chosen format.
    question: How do I troubleshoot “Invalid barcode content” errors?
  - answer: QR ≈ 4,296 alphanumeric characters, Aztec ≈ 3,832 numeric / 3,067 alphanumeric,
      Data Matrix ≈ 3,116 numeric / 2,335 alphanumeric. Keep codes under 200 characters
      for optimal scan reliability.
    question: What is the maximum data capacity for each HIBC format?
  - answer: Absolutely. Create separate `QrCodeSignOptions` objects with different
      positions and call `signature.sign()` for each. Just ensure they don’t overlap.
    question: Is it possible to embed multiple barcode types in one PDF?
  - answer: No. After the JAR is on the classpath and the license is activated, all
      operations are performed locally.
    question: Do I need an internet connection for signing at runtime?
  type: FAQPage
tags:
- sign pdf
- barcode
- java
- healthcare
- groupdocs
title: Como assinar PDF com código de barras usando HIBC em Java
type: docs
url: /pt/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/
weight: 1
---

# Assinar PDF com código de barras usando HIBC em Java

Se você está desenvolvendo software de logística farmacêutica ou de saúde, provavelmente já se deparou com o problema de rastreamento baseado em papel, assinaturas perdidas e pesadelos de auditoria. **Assinar um PDF com código de barras** — especialmente um Data Matrix ou QR code HIBC — cria um rastro à prova de violação, legível por máquina, que sobrevive à impressão, digitalização e revisão regulatória. Neste tutorial você verá exatamente como adicionar códigos Data Matrix e QR a um PDF usando GroupDocs.Signature para Java.

## Respostas rápidas
- **Qual biblioteca manipula códigos de barras HIBC em Java?** GroupDocs.Signature for Java.  
- **Qual formato de código de barras é mais compacto?** Data Matrix – ideal para rótulos pequenos.  
- **Posso adicionar QR e Data Matrix ao mesmo PDF?** Sim, basta criar `QrCodeSignOptions` separados.  
- **Preciso de conexão à internet em tempo de execução?** Não, a biblioteca funciona totalmente offline após a instalação.  
- **Qual versão do Java é recomendada?** Java 11+ para desempenho de nível de produção.

## O que é assinatura de PDF com código de barras HIBC?
`Signature` é a classe central do GroupDocs.Signature que representa um documento PDF e permite a incorporação de assinaturas digitais. A classe `Signature` no GroupDocs.Signature para Java fornece métodos para incorporar códigos de barras HIBC como assinaturas digitais. Ao assinar um PDF com um código de barras HIBC, você cria um registro verificável e à prova de violação que pode ser escaneado em qualquer ponto da cadeia de suprimentos.

## Por que usar Data Matrix e códigos QR juntos?
Data Matrix oferece a menor área ocupada enquanto ainda suporta até 2.335 caracteres alfanuméricos, tornando‑o perfeito para áreas de rótulos densos. Os códigos QR, por outro lado, suportam até 4.296 caracteres e são universalmente legíveis por smartphones. Combinar ambos oferece o melhor equilíbrio entre eficiência de espaço e capacidade de dados, garantindo que todas as partes interessadas — de scanners de armazém a aplicativos móveis — possam ler as informações necessárias.

## Pré-requisitos
- **JDK 11 ou superior** (Java 8 funciona, mas Java 11+ é recomendado para desempenho ideal).  
- **IDE** como IntelliJ IDEA, Eclipse ou VS Code com extensões Java.  
- **Maven ou Gradle** para gerenciamento de dependências (exemplos abaixo).  
- **PDF de exemplo** (por exemplo, `sample.pdf`) para testar a implementação.  
- **Licença válida do GroupDocs.Signature** (teste gratuito para desenvolvimento, licença paga para produção).

## Configurando GroupDocs.Signature para Java

### Configuração Maven
Add the dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Configuração Gradle
For Gradle projects, add this to your `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Opção de download direto
Você também pode baixar o arquivo JAR diretamente de [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) e adicioná‑lo ao classpath do seu projeto manualmente. Esta abordagem funciona bem em ambientes de rede restrita.

### Obtendo uma licença
Solicite um teste gratuito ou licença temporária da GroupDocs para remover marcas d'água e desbloquear todos os recursos. Implantações em produção exigem uma licença adquirida.

### Inicialização básica
`Signature` é o ponto de entrada para todas as operações de assinatura. Ele carrega o PDF, aplica o código de barras e grava o arquivo assinado.

```java
import com.groupdocs.signature.Signature;

class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("sample.pdf");
        // Proceed with signing operations...
    }
}
```

## Como criar um PDF Data Matrix com código de barras HIBC?
Instancie `Signature` com seu PDF de origem, configure `QrCodeSignOptions` para o formato **Data Matrix**, forneça uma string HIBC formatada corretamente e chame `sign()`. A biblioteca grava o PDF assinado no destino, preservando o layout e incorporando o código de barras como uma assinatura à prova de violação.

`QrCodeSignOptions` especifica o tipo de código de barras, conteúdo, tamanho e posicionamento para uma assinatura.

1. **Importe as classes necessárias** – elas dão acesso ao mecanismo de assinatura e às opções de Data Matrix.  

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
```

2. **Instancie o objeto `Signature`** com caminhos absolutos para os arquivos de origem e destino.  

```java
String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY";
String destinFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithHIBCLICQR.pdf";

final Signature signature = new Signature(sourceFilePath);
```

3. **Configure as opções de Data Matrix** – defina a string HIBC, escolha `QrCodeTypes.HIBCLICDataMatrix` e estabeleça as coordenadas de posicionamento. `QrCodeTypes` enumera os formatos de código de barras suportados para assinaturas HIBC.  

```java
QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR);
hibcLic_QR.setLeft(1); // Set the position from left
hibcLic_QR.setTop(1);   // Set the position from top
hibcLic_QR.setReturnContent(true); // Return content after signing
hibcLic_QR.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

4. **Aplique a assinatura** ao PDF.  

```java
signature.sign(destinFilePath, hibcLic_QR);
```

5. **Libere os recursos** para fechar manipuladores de arquivos e evitar vazamentos de memória.  

```java
finally {
    if (signature != null) signature.dispose();
}
```

### Exemplo completo em funcionamento
Aqui está o fluxo completo em um único bloco (os placeholders representam o código exato que você colará dos trechos anteriores):

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;

public class HibcQrSigning {
    public static void main(String[] args) {
        String sourceFilePath = "sample.pdf";
        String destinFilePath = "output/SignWithHIBCLICQR.pdf";
        
        Signature signature = null;
        try {
            signature = new Signature(sourceFilePath);
            
            QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions(
                "A123PROD30917/75#422011907#GP293", 
                QrCodeTypes.HIBCLICQR
            );
            hibcLic_QR.setLeft(1);
            hibcLic_QR.setTop(1);
            hibcLic_QR.setReturnContent(true);
            hibcLic_QR.setReturnContentType(FileType.PNG);
            
            signature.sign(destinFilePath, hibcLic_QR);
            System.out.println("PDF signed successfully with HIBC QR code");
            
        } catch (Exception e) {
            System.err.println("Error signing PDF: " + e.getMessage());
            e.printStackTrace();
        } finally {
            if (signature != null) signature.dispose();
        }
    }
}
```

#### Resposta direta (40–70 palavras)
Para **criar um PDF Data Matrix**, instancie `Signature` com seu PDF de origem, configure `QrCodeSignOptions` para `QrCodeTypes.HIBCLICDataMatrix` e forneça uma string HIBC formatada corretamente, então chame `signature.sign(outputPath, options)`. A biblioteca grava o PDF assinado no destino, preservando o layout e incorporando o código de barras como uma assinatura à prova de violação.

## Como adicionar QR code a PDF usando GroupDocs.Signature?
Carregue o PDF, configure `QrCodeSignOptions` para o formato QR e chame `sign()`. A biblioteca dimensiona a imagem QR para legibilidade e a posiciona com base nas coordenadas definidas, evitando sobreposição com conteúdo existente. Isso garante que o código de barras permaneça escaneável após a impressão e esteja em conformidade com os padrões HIBC.

`QrCodeSignOptions` define o conteúdo, tamanho e posição do código QR.

1. **Importe as classes específicas de QR**  

```java
QrCodeSignOptions hibcLic_AZ = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec);
hibcLic_AZ.setLeft(1); // Set the position from left
hibcLic_AZ.setTop(200); // Set the position from top
hibcLic_AZ.setReturnContent(true); // Return content after signing
hibcLic_AZ.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

2. **Crie e configure as opções de QR** – observe o uso de `QrCodeTypes.HIBCLICQR`.  

```java
signature.sign(destinFilePath, hibcLic_AZ);
```

3. **Assine o documento**  

```java
QrCodeSignOptions hibcLic_DM = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix);
hibcLic_DM.setLeft(1); // Set the position from left
hibcLic_DM.setTop(400); // Set the position from top
hibcLic_DM.setReturnContent(true); // Return content after signing
hibcLic_DM.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

> **Resposta direta:** Use `QrCodeTypes.HIBCLICQR` em `QrCodeSignOptions`, defina a string de conteúdo HIBC, posicione o código com `setLeft()` e `setTop()`, então chame `signature.sign(outputPath, options)`. O código QR é incorporado instantaneamente, pronto para captura por smartphone ou scanner.

## Erros comuns a evitar

### 1. Esquecer de liberar recursos
**Errado:**  
```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  

**Correção:** Envolva o uso de `Signature` em um bloco try‑with‑resources ou chame explicitamente `close()` em um bloco finally.

### 2. Usar strings de formato HIBC incorretas
**Errado:** Usar strings genéricas como “12345”.  
**Correção:** Siga o padrão HIBCC (por exemplo, `A123PROD30917/75#422011907#GP293`). Valide com o [validador online HIBCC](https://www.hibcc.org/).

### 3. Codificar caminhos de arquivos diretamente
**Errado:**  
```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  

**Correção:** Armazene caminhos em um arquivo de configuração ou variável de ambiente e leia‑os em tempo de execução.

### 4. Ignorar conflitos de posicionamento de código de barras
Posicione os códigos de barras longe de texto ou assinaturas existentes. Use coordenadas PDF (origem é canto inferior esquerdo) e teste com uma amostra impressa.

### 5. Não testar com scanners reais
Imprima o PDF assinado e escaneie‑o com o hardware exato usado em seu fluxo de trabalho. Verifique a legibilidade em diferentes qualidades de impressão.

## Aplicações práticas na área de saúde

| Cenário | Código de barras recomendado | Por que se adequa |
|----------|-----------------------------|-------------------|
| **Distribuição farmacêutica** | Código QR | Alta capacidade de dados, amplamente escaneado por smartphones. |
| **Gestão de inventário** | Data Matrix | Pequena área ocupada, ideal para etiquetas de prateleira densas. |
| **Conformidade regulatória (FDA 21 CFR Part 11)** | QR + Data Matrix | Formato duplo fornece redundância e auditabilidade. |
| **Rastreamento de dispositivos médicos** | Aztec Code | Tamanho compacto funciona em embalagens com espaço limitado. |

## Considerações de desempenho e boas práticas

### Padrão de processamento em lote
```java
List<String> filesToSign = getFileList();
for (String filePath : filesToSign) {
    Signature signature = null;
    try {
        signature = new Signature(filePath);
        // Sign and save
    } finally {
        if (signature != null) signature.dispose();
    }
}
```

- Crie uma nova instância de `Signature` por arquivo para manter o uso de memória baixo.  
- Use um pool de threads fixo (`Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() - 1)`) para processamento paralelo, mas monitore o tamanho do heap, pois cada `Signature` mantém o PDF completo na memória.  

### Mantenha as bibliotecas atualizadas
As versões do GroupDocs melhoram a velocidade de processamento em até **20 %** e adicionam novos recursos de conformidade HIBC. Agende verificações de dependências trimestrais.

### Cache de modelos
Carregue um modelo PDF uma vez, clone‑o para cada variante de código de barras e assine os clones. Isso reduz I/O e acelera fluxos de trabalho de alto volume.

## Perguntas frequentes

**Q: O GroupDocs.Signature pode assinar tipos de arquivo além de PDF?**  
A: Sim, também suporta DOCX, XLSX, PPTX, PNG, JPEG e TIFF com a mesma API de assinatura de código de barras.

**Q: Como solucionar erros “Invalid barcode content”?**  
A: Verifique se sua string HIBC segue exatamente a sintaxe HIBCC, use o validador online e assegure‑se de usar a constante `QrCodeTypes` correta para o formato escolhido.

**Q: Qual é a capacidade máxima de dados para cada formato HIBC?**  
A: QR ≈ 4.296 caracteres alfanuméricos, Aztec ≈ 3.832 numéricos / 3.067 alfanuméricos, Data Matrix ≈ 3.116 numéricos / 2.335 alfanuméricos. Mantenha os códigos com menos de 200 caracteres para confiabilidade de escaneamento ideal.

**Q: É possível incorporar múltiplos tipos de código de barras em um PDF?**  
A: Absolutamente. Crie objetos `QrCodeSignOptions` separados com posições diferentes e chame `signature.sign()` para cada um. Apenas garanta que não se sobreponham.

**Q: Preciso de conexão à internet para assinar em tempo de execução?**  
A: Não. Depois que o JAR está no classpath e a licença está ativada, todas as operações são realizadas localmente.

## Recursos adicionais

- [Documentação do GroupDocs.Signature para Java](https://docs.groupdocs.com/signature/java/)  
- [Guia de Referência da API](https://reference.groupdocs.com/signature/java/)  
- [Downloads da Última Versão](https://releases.groupdocs.com/signature/java/)  
- [Comprar Licença](https://purchase.groupdocs.com/buy)  
- [Obter Teste Gratuito](https://releases.groupdocs.com/signature/java/)  
- [Solicitar Licença Temporária](https://purchase.groupdocs.com/temporary-license/)  
- [Fórum GroupDocs](https://forum.groupdocs.com/c/signature/)  

---

**Última atualização:** 2026-09-15  
**Testado com:** GroupDocs.Signature 23.12 para Java  
**Autor:** GroupDocs  

## Tutoriais relacionados

- [Criar assinatura de código de barras PDF em Java – Guia GroupDocs](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)
- [Criar assinatura de código de barras em Java – Atualizar códigos de barras PDF](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [Como ler PDF com código QR usando Java e GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)
