---
categories:
- Document Signing
- Healthcare Integration
date: '2026-05-16'
description: Aprenda como criar PDF Data Matrix e adicionar PDF de código QR usando
  GroupDocs.Signature para Java. Guia passo a passo para assinatura de documentos
  de saúde.
keywords:
- create data matrix pdf
- add qr code pdf
- HIBC barcode Java
lastmod: '2026-05-16'
linktitle: Guia de Assinatura de PDF HIBC em Java
schemas:
- author: GroupDocs
  dateModified: '2026-05-16'
  description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  headline: Create Data Matrix PDF with HIBC Barcode in Java
  type: TechArticle
- description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  name: Create Data Matrix PDF with HIBC Barcode in Java
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
- java
- pdf-signing
- hibc
- healthcare
- barcode
- pharmaceutical
title: Criar PDF Data Matrix com Código de Barras HIBC em Java
type: docs
url: /pt/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/
weight: 1
---

# Criar PDF Data Matrix com Código de Barras HIBC em Java

Se você está desenvolvendo software de logística farmacêutica ou de saúde, provavelmente já se deparou com o problema de rastreamento baseado em papel, assinaturas perdidas e pesadelos de auditoria. **Criar um PDF Data Matrix** que incorpora um código de barras HIBC LIC resolve esses problemas ao fornecer um rastro à prova de violação, legível por máquina, que resiste à impressão, digitalização e revisão regulatória. Neste tutorial você verá exatamente como **adicionar suporte a PDF com código QR**, bem como aos formatos Aztec e Data Matrix, usando o GroupDocs.Signature para Java.

## Respostas Rápidas
- **Qual biblioteca manipula códigos de barras HIBC em Java?** GroupDocs.Signature para Java.  
- **Qual formato de código de barras é o mais compacto?** Data Matrix – ideal para rótulos pequenos.  
- **Posso adicionar QR e Data Matrix ao mesmo PDF?** Sim, basta criar `QrCodeSignOptions` separados.  
- **Preciso de conexão com a internet em tempo de execução?** Não, a biblioteca funciona totalmente offline após a instalação.  
- **Qual versão do Java é recomendada?** Java 11+ para desempenho de nível de produção.

## O que é assinatura de PDF com código de barras HIBC?
A classe `Signature` no GroupDocs.Signature para Java representa um documento PDF e fornece métodos para incorporar códigos de barras HIBC como assinaturas digitais. Ao assinar um PDF com um código de barras HIBC, você cria um registro verificável e à prova de violação que pode ser escaneado em qualquer ponto da cadeia de suprimentos.

## Por que usar Data Matrix e códigos QR juntos?
O GroupDocs.Signature suporta **mais de 50 formatos de entrada e saída** e pode processar PDFs com centenas de páginas sem carregar o arquivo inteiro na memória. Usar Data Matrix para rótulos densos e de área pequena e QR para documentos mais espaçosos oferece o melhor equilíbrio entre legibilidade, capacidade de dados (até 4.296 caracteres para QR) e eficiência de espaço de impressão.

## Pré‑requisitos
- **JDK 11 ou superior** (Java 8 funciona, mas Java 11+ é recomendado para desempenho ideal).  
- **IDE** como IntelliJ IDEA, Eclipse ou VS Code com extensões Java.  
- **Maven ou Gradle** para gerenciamento de dependências (exemplos abaixo).  
- **PDF de exemplo** (por exemplo, `sample.pdf`) para testar a implementação.  
- **Licença válida do GroupDocs.Signature** (teste gratuito para desenvolvimento, licença paga para produção).

## Configurando GroupDocs.Signature para Java

### Configuração Maven
Adicione a dependência ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Configuração Gradle
Para projetos Gradle, adicione isto ao seu `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Opção de Download Direto
Você também pode baixar o arquivo JAR diretamente em [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) e adicioná‑lo ao classpath do seu projeto manualmente. Essa abordagem funciona bem em ambientes com rede restrita.

### Obtendo uma Licença
Solicite um teste gratuito ou licença temporária ao GroupDocs para remover marcas d'água e desbloquear todos os recursos. Implantações em produção exigem licença adquirida.

### Inicialização Básica
A classe `Signature` é o ponto de entrada para todas as operações de assinatura. Ela carrega o PDF, aplica o código de barras e grava o arquivo assinado.

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
Carregue seu PDF de origem, configure um objeto `QrCodeSignOptions` para o formato Data Matrix e chame `sign()` – isso é tudo que você precisa para incorporar um código de barras HIBC Data Matrix compatível. As etapas a seguir mostram o código exato necessário. `QrCodeSignOptions` define as configurações para uma assinatura de código de barras, como tipo, conteúdo, tamanho e posição.

1. **Importe as classes necessárias** – elas dão acesso ao motor de assinatura e às opções de Data Matrix.  

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

3. **Configure as opções de Data Matrix** – defina a string HIBC, escolha `QrCodeTypes.HIBCLICDataMatrix` e defina as coordenadas de posicionamento. `QrCodeTypes` enumera os formatos de código de barras suportados para assinaturas HIBC.  

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
Aqui está o fluxo completo em um único bloco (os marcadores representam o código exato que você colará dos trechos anteriores):

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
Para **criar um PDF Data Matrix**, instancie `Signature` com seu PDF de origem, configure `QrCodeSignOptions` para `QrCodeTypes.HIBCLICDataMatrix` e forneça uma string HIBC formatada corretamente, então chame `signature.sign(outputPath, options)`. A biblioteca grava o PDF assinado no destino, preservando o layout e incorporando o código de barras como assinatura à prova de violação.

## Como adicionar QR code PDF usando GroupDocs.Signature?
Carregue o PDF, configure `QrCodeSignOptions` para o formato QR e invoque `sign()`. Esse padrão de duas linhas funciona para qualquer tamanho de PDF e dimensiona automaticamente a imagem QR para legibilidade ótima. `QrCodeSignOptions` configura a assinatura do código QR, incluindo seu conteúdo e propriedades visuais. Ele posiciona o código com base nas coordenadas definidas, garantindo que não sobreponha conteúdo existente e permaneça escaneável após a impressão.

1. **Importe classes específicas de QR**  

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

## Erros Comuns a Evitar

### 1. Esquecer de Liberar Recursos
**Errado:**  
```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  

**Correção:** Envolva o uso de `Signature` em um bloco try‑with‑resources ou chame explicitamente `close()` em um bloco finally.

### 2. Usar Strings de Formato HIBC Incorretas
**Errado:** Usar strings genéricas como “12345”.  
**Correção:** Siga o padrão HIBCC (por exemplo, `A123PROD30917/75#422011907#GP293`). Valide com o [validador online HIBCC](https://www.hibcc.org/).

### 3. Codificar Caminhos de Arquivo
**Errado:**  
```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  

**Correção:** Armazene caminhos em um arquivo de configuração ou variável de ambiente e leia‑os em tempo de execução.

### 4. Ignorar Conflitos de Posicionamento de Código de Barras
Coloque os códigos de barras longe de texto ou assinaturas existentes. Use coordenadas PDF (origem no canto inferior esquerdo) e teste com uma amostra impressa.

### 5. Não Testar com Scanners Reais
Imprima o PDF assinado e escaneie‑o com o hardware exato usado no seu fluxo de trabalho. Verifique a legibilidade em diferentes qualidades de impressão.

## Aplicações Práticas na Saúde

| Cenário | Código de Barras Recomendado | Por que se adequa |
|----------|------------------------------|-------------------|
| **Distribuição farmacêutica** | QR Code | Alta capacidade de dados, amplamente escaneado por smartphones. |
| **Gestão de inventário** | Data Matrix | Pequena pegada, ideal para rótulos de prateleira densos. |
| **Conformidade regulatória (FDA 21 CFR Part 11)** | QR + Data Matrix | Formato duplo fornece redundância e auditabilidade. |
| **Rastreamento de dispositivos médicos** | Aztec Code | Tamanho compacto funciona em embalagens com espaço limitado. |

## Considerações de Desempenho e Melhores Práticas

### Padrão de Processamento em Lote
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

- Crie uma nova instância `Signature` por arquivo para manter o uso de memória baixo.  
- Use um pool de threads fixo (`Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() - 1)`) para processamento paralelo, mas monitore o tamanho do heap, pois cada `Signature` mantém o PDF completo na memória.  

### Mantenha as Bibliotecas Atualizadas
As versões do GroupDocs melhoram a velocidade de processamento em até **20 %** e adicionam novos recursos de conformidade HIBC. Agende verificações de dependências trimestrais.

### Cache de Modelos
Carregue um modelo PDF uma única vez, clone‑o para cada variante de código de barras e assine os clones. Isso reduz I/O e acelera fluxos de trabalho de alto volume.

## Perguntas Frequentes

**P: O GroupDocs.Signature pode assinar tipos de arquivo além de PDF?**  
R: Sim, também suporta DOCX, XLSX, PPTX, PNG, JPEG e TIFF com a mesma API de assinatura de código de barras.

**P: Como solucionar erros “Conteúdo de código de barras inválido”?**  
R: Verifique se sua string HIBC segue exatamente a sintaxe HIBCC, use o validador online e assegure‑se de estar usando a constante `QrCodeTypes` correta para o formato escolhido.

**P: Qual é a capacidade máxima de dados para cada formato HIBC?**  
R: QR ≈ 4.296 caracteres alfanuméricos, Aztec ≈ 3.832 numéricos / 3.067 alfanuméricos, Data Matrix ≈ 3.116 numéricos / 2.335 alfanuméricos. Mantenha os códigos abaixo de 200 caracteres para confiabilidade de escaneamento ideal.

**P: É possível incorporar vários tipos de código de barras em um único PDF?**  
R: Absolutamente. Crie objetos `QrCodeSignOptions` separados com posições diferentes e chame `signature.sign()` para cada um. Apenas garanta que não se sobreponham.

**P: Preciso de conexão com a internet para assinar em tempo de execução?**  
R: Não. Após o JAR estar no classpath e a licença ativada, todas as operações são realizadas localmente.

## Recursos Adicionais

- [Documentação do GroupDocs.Signature para Java](https://docs.groupdocs.com/signature/java/)  
- [Guia de Referência da API](https://reference.groupdocs.com/signature/java/)  
- [Downloads da Última Versão](https://releases.groupdocs.com/signature/java/)  
- [Comprar Licença](https://purchase.groupdocs.com/buy)  
- [Obter Teste Gratuito](https://releases.groupdocs.com/signature/java/)  
- [Solicitar Licença Temporária](https://purchase.groupdocs.com/temporary-license/)  
- [Fórum do GroupDocs](https://forum.groupdocs.com/c/signature/)

---

**Última Atualização:** 2026-05-16  
**Testado Com:** GroupDocs.Signature 23.12 para Java  
**Autor:** GroupDocs  

---

```java
signature.sign(destinFilePath, hibcLic_DM);
```

## Tutoriais Relacionados

- [Criar Assinatura de Código de Barras PDF em Java – Guia GroupDocs](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)
- [Criar Assinatura de Código de Barras em Java – Atualizar Códigos de Barras PDF](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [Como ler QR code PDF usando Java e GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)