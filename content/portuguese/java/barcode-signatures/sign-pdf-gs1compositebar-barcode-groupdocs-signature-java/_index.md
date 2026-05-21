---
categories:
- Java PDF Processing
date: '2026-05-21'
description: Aprenda como criar assinatura de barcode Java para PDFs usando GroupDocs.Signature.
  Guia completo com code examples, troubleshooting tips, e real-world use cases para
  document authentication.
keywords:
- create barcode signature java
- barcode signatures java
- pdf barcode signing java
lastmod: '2026-05-21'
linktitle: Assinaturas de barcode PDF em Java
schemas:
- author: GroupDocs
  dateModified: '2026-05-21'
  description: Learn how to create barcode signature Java for PDFs using GroupDocs.Signature.
    Complete guide with code examples, troubleshooting tips, and real-world use cases
    for document authentication.
  headline: How to Create Barcode Signature Java for PDF Documents
  type: TechArticle
- questions:
  - answer: A GS1CompositeBar combines linear and 2D components to store product IDs,
      serial numbers, and other data in a single scannable symbol, widely used in
      retail and logistics.
    question: What is a GS1CompositeBar barcode?
  - answer: Yes—GroupDocs.Signature supports over 60 types, including QR, Code128,
      DataMatrix, PDF417, and Aztec. Switch the `setEncodeType()` value to change
      the format.
    question: Can I use other barcode types besides GS1CompositeBar?
  - answer: A valid GroupDocs license is required for production deployments. A free
      trial is available for development and testing.
    question: Do I need a license for production use?
  - answer: Absolutely, provided the barcode is at least 200 × 100 px and has sufficient
      contrast. Smartphone scanning apps work on‑screen; hardware scanners work on
      printed copies.
    question: Will barcode scanners read barcodes from signed PDFs?
  - answer: Wrap your code in try‑catch blocks, log full stack traces, and always
      call `signature.dispose()` in a finally block to release resources.
    question: How do I handle errors during signing?
  type: FAQPage
tags:
- barcode-signatures
- pdf-signing
- document-authentication
- java-libraries
title: Como criar assinatura de barcode Java para documentos PDF
type: docs
url: /pt/java/barcode-signatures/sign-pdf-gs1compositebar-barcode-groupdocs-signature-java/
weight: 1
---

# Como Criar Assinatura de Código de Barras Java para Documentos PDF

## Introdução

Neste tutorial você aprenderá a **create barcode signature Java** para arquivos PDF usando o GroupDocs.Signature. Seja para incorporar códigos de produto, IDs de auditoria ou quaisquer dados estruturados em um contrato, assinaturas de código de barras permitem adicionar informações legíveis por máquina que podem ser escaneadas instantaneamente, mantendo o documento criptograficamente seguro. Vamos percorrer a configuração, o código, a personalização e dicas de boas práticas para que você possa começar a adicionar assinaturas de código de barras aos seus PDFs em minutos.

## Respostas Rápidas
- **Qual biblioteca adiciona assinaturas de código de barras em Java?** GroupDocs.Signature for Java.  
- **Qual tipo de código de barras é o melhor para varejo?** `GS1CompositeBar` (padrão da indústria para rastreamento de produtos).  
- **Preciso de licença para produção?** Sim – é necessária uma licença GroupDocs adquirida.  
- **Posso adicionar assinaturas digitais e de código de barras?** Absolutamente; combine-as para segurança e escaneabilidade.  
- **O código é compatível com Java 11 e posteriores?** Sim, a API funciona com JDK 8+.  

## O que é create barcode signature java?
`create barcode signature java` refere‑se ao processo de inserir programaticamente um código de barras em um PDF usando código Java. O GroupDocs.Signature fornece uma API simples que gera a imagem do código de barras, posiciona‑a na página e salva o documento assinado em uma única operação contínua.

## Por que usar assinaturas de código de barras?
As assinaturas de código de barras fornecem **metadados legíveis por máquina** dentro de um PDF assinado legalmente. Elas permitem verificação visual instantânea, agilizam a leitura na cadeia de suprimentos e permitem que sistemas downstream extraiam dados estruturados sem abrir o arquivo. Mais de 60 formatos de código de barras são suportados, e o GS1CompositeBar pode codificar identificadores de produto, números de série e códigos de lote em um único símbolo compacto — perfeito para varejo, saúde e finanças.

## Pré‑requisitos

- **Java Development Kit:** JDK 8 ou superior (Java 11, 17, 21 funcionam).  
- **Ferramenta de Build:** Maven ou Gradle — escolha a que preferir.  
- **IDE:** IntelliJ IDEA, Eclipse ou VS Code.  
- **Biblioteca GroupDocs.Signature:** Adicione a dependência conforme mostrado abaixo.  
- **Licença:** Avaliação gratuita para desenvolvimento; licença comprada para produção.  

### Adicionando GroupDocs.Signature ao seu projeto

**Para usuários Maven**, adicione isto ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Para usuários Gradle**, adicione isto ao seu `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Sobre licenciamento:** o GroupDocs oferece uma avaliação gratuita ideal para testes e desenvolvimento. Você pode baixá‑la na sua [página de releases](https://releases.groupdocs.com/signature/java/). Quando estiver pronto para produção, será necessário adquirir uma licença ou solicitar uma temporária no [site do GroupDocs](https://purchase.groupdocs.com/buy). Para uso detalhado da API veja a [Referência da API](https://reference.groupdocs.com/signature/java/), consulte o [Guia do Desenvolvedor](https://docs.groupdocs.com/signature/java/) para instruções passo a passo, e faça perguntas no [Fórum do GroupDocs](https://forum.groupdocs.com/). O mesmo link de compra também está listado como a [página de compra](https://purchase.groupdocs.com/buy).

## Como configurar o GroupDocs.Signature em Java?

A classe `Signature` representa um documento e fornece métodos para aplicar assinaturas, buscar conteúdo e gerenciar recursos. Crie uma instância de `Signature` para abrir seu PDF e prepará‑lo para assinatura. A classe `Signature` é o componente central do GroupDocs.Signature que gerencia o carregamento do documento, o manuseio de recursos e o fluxo de assinatura, garantindo que todas as operações sejam realizadas de forma segura e eficiente.

```java
import com.groupdocs.signature.Signature;

// Point to your PDF file
Signature signature = new Signature("path/to/your/document.pdf");
```

**Importante:** Sempre descarte o objeto `Signature` após o uso — isso libera handles de arquivo e libera memória.

## Como configurar as opções de assinatura de código de barras?

A classe `BarcodeSignOptions` define cada aspecto do código de barras que você está prestes a inserir, desde a carga de dados até o estilo visual. Ela funciona como um contêiner para todas as configurações relacionadas ao código de barras, como tipo, tamanho, cores e posicionamento. Abaixo está uma configuração mínima que cria um código de barras GS1CompositeBar contendo um GTIN e um número de série, demonstrando também como definir margens e cores de fundo para legibilidade ideal.

```java
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

// Create barcode with GS1 format data
BarcodeSignOptions options = new BarcodeSignOptions("(01)03212345678906/(21)A1B2C3D4E5F6G7H8");
options.setEncodeType(BarcodeTypes.GS1CompositeBar);
```

A string `"(01)03212345678906/(21)A1B2C3D4E5F6G7H8"` segue o padrão GS1:
- `(01)` = GTIN (identificador global de produto)  
- `03212345678906` = código real do produto  
- `(21)` = identificador de número de série  
- `A1B2C3D4E5F6G7H8` = série única  

Você pode substituir isso por qualquer texto para QR codes, Code128, DataMatrix, etc. Mais de 60 tipos de código de barras são suportados — consulte a documentação do GroupDocs para a lista completa.

## Como posicionar e personalizar o código de barras?

Posicionamento e estilo são controlados através do mesmo objeto `BarcodeSignOptions`. Use `setTop`, `setLeft`, `setWidth` e `setHeight` para definir coordenadas e dimensões exatas. Definir `setAllPages(true)` adiciona o código de barras a todas as páginas automaticamente, enquanto `setPageNumber(1)` direciona a uma página específica. Você também pode girar o código de barras, adicionar uma cor de fundo ou ajustar margens para garantir que o código não sobreponha conteúdo existente.

```java
// Set position and apply to all pages
options.setTop(200); // Set vertical position
options.setAllPages(true);
```

Para layout mais preciso, você pode ainda ancorar o código de barras a uma página específica, girá‑lo ou adicionar uma cor de fundo:

```java
options.setLeft(100);        // 100 pixels from left edge
options.setTop(200);         // 200 pixels from top
options.setWidth(300);       // Barcode width in pixels
options.setHeight(100);      // Barcode height in pixels
options.setPageNumber(1);    // Only sign page 1 (removes setAllPages)
```

A personalização visual (cores de primeiro plano/fundo, margens, rótulos de texto) está disponível via propriedades adicionais:

```java
options.setMargin(new Padding(10));           // Add padding around barcode
options.setBackground(new Background());       // Set background color
options.setForeColor(Color.BLACK);            // Barcode color
options.setBackgroundColor(Color.WHITE);      // Background color
```

## Como assinar o documento com um código de barras?

O método `sign` na instância `Signature` aplica as opções configuradas e grava o documento assinado no disco. Ele retorna um objeto `SignResult` que informa quantas assinaturas foram aplicadas e se ocorreram avisos. Esse método lida com toda a manipulação de PDF de baixo nível, portanto você não precisa trabalhar diretamente com bibliotecas de PDF.

```java
try {
    SignResult signResult = signature.sign(outputPath, options);
    System.out.println("Document signed successfully!");
    System.out.println("Signed document saved to: " + outputPath);
} finally {
    if (signature != null) {
        signature.dispose();
    }
}
```

O bloco `try‑finally` ao redor garante que o objeto `Signature` seja descartado mesmo se uma exceção ocorrer, evitando vazamentos de handles de arquivo.

Você pode inspecionar o `SignResult` para confirmar o sucesso:

```java
if (signResult.getSucceeded().size() > 0) {
    System.out.println("Successfully added " + signResult.getSucceeded().size() + " signature(s)");
}
```

## Exemplo completo em funcionamento

Juntando tudo, aqui está um único método que carrega um PDF, adiciona um código de barras GS1CompositeBar e salva o arquivo assinado:

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

public class BarcodeSigningExample {
    
    public void signPdfWithBarcode(String inputPath, String outputPath) {
        Signature signature = null;
        
        try {
            // Initialize signature
            signature = new Signature(inputPath);
            
            // Configure barcode
            BarcodeSignOptions options = new BarcodeSignOptions(
                "(01)03212345678906/(21)A1B2C3D4E5F6G7H8"
            );
            options.setEncodeType(BarcodeTypes.GS1CompositeBar);
            options.setTop(200);
            options.setAllPages(true);
            
            // Sign and save
            SignResult result = signature.sign(outputPath, options);
            
            System.out.println("Signing completed: " + result.getSucceeded().size() + " signature(s) added");
            
        } catch (Exception e) {
            System.err.println("Error signing document: " + e.getMessage());
            e.printStackTrace();
        } finally {
            if (signature != null) {
                signature.dispose();
            }
        }
    }
}
```

Esse método está pronto para produção: valida a entrada, gerencia recursos e relata o resultado.

## Como adicionar assinaturas digitais e de código de barras?

Para máxima segurança, adicione primeiro uma assinatura digital criptográfica e, em seguida, sobreponha o código de barras. A assinatura digital garante a integridade do documento, enquanto o código de barras fornece verificação visual rápida e dados legíveis por máquina. Use a classe `DigitalSignOptions` para a primeira etapa e depois aplique `BarcodeSignOptions` como mostrado acima.

```java
// First, add digital signature
DigitalSignOptions digitalOptions = new DigitalSignOptions("certificate.pfx");
digitalOptions.setPassword("cert_password");
signature.sign(outputPath, digitalOptions);

// Then, add barcode on top
BarcodeSignOptions barcodeOptions = new BarcodeSignOptions("DATA");
barcodeOptions.setEncodeType(BarcodeTypes.QR);
signature.sign(outputPath, barcodeOptions);
```

O PDF resultante é tanto juridicamente vinculativo (assinatura digital) quanto instantaneamente legível por qualquer scanner de código de barras.

## Trabalhando com diferentes tipos de código de barras

Trocar o formato do código de barras é tão simples quanto mudar um valor de enumeração. Abaixo está um exemplo que substitui o GS1CompositeBar por um QR code:

```java
// Define barcode sign options with sample text
BarcodeSignOptions options = new BarcodeSignOptions("Sample Text");

// Assign specific barcode type
options.setEncodeType(BarcodeTypes.GS1CompositeBar);
```

E aqui está a mesma mudança para um código de barras linear Code128:

```java
options.setEncodeType(BarcodeTypes.QR);           // QR code
options.setEncodeType(BarcodeTypes.Code128);      // Code 128
options.setEncodeType(BarcodeTypes.DataMatrix);   // Data Matrix
```

Lembre‑se de que cada tipo de código de barras tem seus próprios limites de capacidade de dados — QR codes podem armazenar milhares de caracteres, enquanto Code39 é limitado a alfanuméricos.

## Casos de Uso no Mundo Real

### Gerenciamento da Cadeia de Suprimentos
Incorporar um GS1CompositeBar em manifestos de envio permite que a equipe de armazém escaneie números de pedido, destinos e códigos de lote sem abrir o PDF.

```java
BarcodeSignOptions options = new BarcodeSignOptions(
    "(01)" + gtin + "/(21)" + serialNumber + "/(10)" + batchNumber
);
options.setEncodeType(BarcodeTypes.GS1CompositeBar);
```

### Documentação de Saúde
QR codes em formulários de consentimento podem ser escaneados para arquivar automaticamente o documento no registro correto do paciente.

```java
String patientData = "PATIENT_ID:" + patientId + "|DOC_TYPE:CONSENT|DATE:" + dateString;
BarcodeSignOptions options = new BarcodeSignOptions(patientData);
options.setEncodeType(BarcodeTypes.QR);
```

### Serviços Financeiros
IDs de transação codificados em um código de barras permitem que auditores verifiquem conformidade com uma simples leitura.

```java
String complianceData = "TXN:" + transactionId + "|AGENT:" + agentId + "|BRANCH:" + branchCode;
BarcodeSignOptions options = new BarcodeSignOptions(complianceData);
options.setEncodeType(BarcodeTypes.PDF417);
```

### Controle de Qualidade na Manufatura
Relatórios de inspeção assinados com códigos de barras que contêm números de lote e IDs de inspetor tornam a análise de causa raiz instantânea.

```java
String qcData = "BATCH:" + batchNumber + "|INSPECTOR:" + inspectorId + "|RESULT:" + passFailStatus;
BarcodeSignOptions options = new BarcodeSignOptions(qcData);
options.setEncodeType(BarcodeTypes.DataMatrix);
```

## Problemas Comuns de Implementação

### Problema 1: Exceção “File is already in use”
**Resposta:** O arquivo permanece bloqueado se uma instância anterior de `Signature` não foi descartada. Sempre envolva o código de assinatura em um bloco `try‑finally` e chame `signature.dispose()`.

```java
Signature signature = null;
try {
    signature = new Signature(filePath);
    // ... your code ...
} finally {
    if (signature != null) {
        signature.dispose();
    }
}
```

### Problema 2: Código de barras não aparece no PDF
**Resposta:** Verifique se os valores de `setTop`/`setLeft` estão dentro dos limites da página, aumente a largura/altura do código de barras e garanta que as cores de primeiro plano/fundo contrastem com o fundo da página.

```java
// Make sure dimensions are reasonable
options.setTop(100);      // Not 10000
options.setLeft(100);
options.setWidth(300);    // At least 200 pixels for readability
options.setHeight(100);

// Ensure contrast
options.setForeColor(Color.BLACK);
options.setBackgroundColor(Color.WHITE);
```

### Problema 3: Exceção “Invalid Barcode Data”
**Resposta:** Códigos GS1 exigem notação estrita de parênteses. Use os Identificadores de Aplicação corretos (ex.: `(01)`, `(21)`) e evite caracteres não suportados.

```java
// Correct:
"(01)03212345678906/(21)ABC123"

// Incorrect:
"03212345678906ABC123"
```

### Problema 4: OutOfMemoryError com PDFs grandes
**Resposta:** Aumente o heap da JVM (`-Xmx4G`) e considere assinar páginas individualmente em vez de usar `setAllPages(true)` para documentos muito grandes.

```bash
java -Xmx2G -jar your-application.jar
```

### Problema 5: Falha na leitura do código de barras
**Resposta:** Garanta que o código de barras tenha pelo menos 200 × 100 px, use cores de alto contraste e não seja distorcido pela compressão do PDF.

```java
// Increase size
options.setWidth(400);
options.setHeight(150);

// Maximize contrast
options.setForeColor(Color.BLACK);
options.setBackgroundColor(Color.WHITE);

// Add quiet zone (blank space around barcode)
options.setMargin(new Padding(10));
```

## Segurança e Validação

### As assinaturas de código de barras são seguras?
Um código de barras por si só não é protegido criptograficamente, portanto qualquer pessoa poderia gerar um novo. Combine‑o com uma assinatura digital para garantir autenticidade e escaneabilidade. O padrão de dupla assinatura (digital primeiro, código de barras depois) oferece aplicabilidade legal mais conveniência operacional.

### Validando os dados do código de barras
Após a leitura, verifique se a assinatura digital do documento ainda é válida e se a carga útil do código de barras corresponde aos padrões esperados. Use a API `search()` do GroupDocs com `BarcodeSearchOptions` para extrair e validar o conteúdo do código de barras automaticamente.

```java
public boolean validateScannedBarcode(String scannedData, String documentPath) {
    // Verify digital signature first
    if (!verifyDigitalSignature(documentPath)) {
        return false;
    }
    
    // Validate barcode format
    if (!scannedData.matches("(01)\\d{14}/(21)[A-Z0-9]+")) {
        return false;
    }
    
    // Check against database
    String productId = extractProductId(scannedData);
    return database.productExists(productId);
}
```

## Considerações de Desempenho

### Gerenciamento de Recursos
Sempre descarte objetos `Signature` após cada operação para evitar vazamentos de memória:

```java
signature.dispose();
```

Ao processar muitos arquivos, crie e descarte um novo `Signature` por documento:

```java
for (String filePath : documentPaths) {
    Signature signature = null;
    try {
        signature = new Signature(filePath);
        // ... signing logic ...
    } finally {
        if (signature != null) {
            signature.dispose();
        }
    }
}
```

### Processamento em Lote
Para pequenos lotes (< 100 arquivos), o processamento sequencial é simples:

```java
for (String path : paths) {
    signDocument(path);
}
```

Para cargas de trabalho maiores, o processamento paralelo pode acelerar — mas monitore a pressão de I/O e limite o número de threads a 4‑8:

```java
paths.parallelStream().forEach(path -> signDocument(path));
```

### Otimização de Memória para PDFs Grandes
Aumente o tamanho do heap, processe páginas individualmente e limpe referências após cada etapa. Isso impede `OutOfMemoryError` em documentos maiores que 50 MB.

### Cache de Opções de Código de Barras
Se você reutilizar a mesma configuração de código de barras em muitos arquivos, faça cache da instância `BarcodeSignOptions`:

```java
// Create once, reuse many times
private static BarcodeSignOptions createStandardBarcodeOptions(String data) {
    BarcodeSignOptions options = new BarcodeSignOptions(data);
    options.setEncodeType(BarcodeTypes.GS1CompositeBar);
    options.setTop(200);
    options.setAllPages(true);
    return options;
}
```

## Recursos Avançados

### Múltiplas assinaturas em um documento
Adicione vários códigos de barras (ou misture com assinaturas digitais) chamando `sign` várias vezes com diferentes objetos de opções:

```java
// Add QR code in top-left
BarcodeSignOptions qrOptions = new BarcodeSignOptions("https://example.com");
qrOptions.setEncodeType(BarcodeTypes.QR);
qrOptions.setTop(50);
qrOptions.setLeft(50);
signature.sign(outputPath, qrOptions);

// Add GS1 barcode in bottom-right
BarcodeSignOptions gs1Options = new BarcodeSignOptions("(01)03212345678906");
gs1Options.setEncodeType(BarcodeTypes.GS1CompositeBar);
gs1Options.setTop(700);
gs1Options.setLeft(400);
signature.sign(outputPath, gs1Options);
```

### Conteúdo dinâmico do código de barras
Gere dados do código de barras a partir de metadados do documento, timestamps ou consultas ao banco de dados:

```java
// Extract data from PDF or database
String orderId = extractOrderIdFromPdf(filePath);
String timestamp = LocalDateTime.now().format(DateTimeFormatter.ISO_DATE_TIME);
String barcodeData = String.format("ORDER:%s|TIME:%s", orderId, timestamp);

BarcodeSignOptions options = new BarcodeSignOptions(barcodeData);
```

### Integração com Spring Boot
Exponha um endpoint REST que recebe um PDF, adiciona um código de barras e devolve o arquivo assinado:

```java
@Service
public class DocumentSigningService {
    public void signWithBarcode(MultipartFile file, String barcodeData) {
        // ... implementation ...
    }
}
```

### Exemplo de API REST
Um controlador mínimo que delega ao serviço de assinatura:

```java
@PostMapping("/sign-document")
public ResponseEntity<byte[]> signDocument(
    @RequestParam("file") MultipartFile file,
    @RequestParam("barcode") String barcodeData
) {
    // Sign document and return as byte array
}
```

## Perguntas Frequentes

**Q: O que é um código de barras GS1CompositeBar?**  
R: Um GS1CompositeBar combina componentes lineares e 2D para armazenar IDs de produto, números de série e outros dados em um único símbolo escaneável, amplamente usado no varejo e logística.

**Q: Posso usar outros tipos de código de barras além do GS1CompositeBar?**  
R: Sim — o GroupDocs.Signature suporta mais de 60 tipos, incluindo QR, Code128, DataMatrix, PDF417 e Aztec. Altere o valor de `setEncodeType()` para mudar o formato.

**Q: Preciso de licença para uso em produção?**  
R: Uma licença GroupDocs válida é necessária para implantações em produção. Uma avaliação gratuita está disponível para desenvolvimento e testes.

**Q: Scanners de código de barras leem códigos de PDFs assinados?**  
R: Absolutamente, desde que o código de barras tenha pelo menos 200 × 100 px e contraste suficiente. Aplicativos de escaneamento em smartphones funcionam na tela; scanners de hardware funcionam em cópias impressas.

**Q: Como tratar erros durante a assinatura?**  
R: Envolva seu código em blocos try‑catch, registre rastreamentos completos de exceção e sempre chame `signature.dispose()` no bloco finally para liberar recursos.

**Q: Posso assinar outros formatos de documento?**  
R: Sim — o GroupDocs.Signature também suporta DOCX, XLSX, PPTX, imagens e muitos mais. Basta mudar a extensão do arquivo de entrada; a API permanece a mesma.

**Q: Existem limites de tamanho de arquivo?**  
R: Não há limite rígido, mas documentos acima de 50 MB podem exigir um heap JVM maior e processamento página a página para manter a eficiência de memória.

**Q: Como assinar PDFs armazenados em armazenamento em nuvem?**  
R: Baixe o arquivo para um caminho local temporário, aplique a assinatura e, em seguida, faça o upload de volta para seu bucket na nuvem. Limpe os arquivos temporários depois.

## Conclusão

Agora você tem um guia completo e pronto para produção sobre **create barcode signature java** para documentos PDF. Ao combinar assinaturas digitais criptográficas com códigos de barras legíveis por máquina, você obtém tanto a exigibilidade legal quanto a eficiência operacional em casos de uso de cadeia de suprimentos, saúde, finanças e manufatura. Experimente diferentes tipos de código de barras, integre o código aos seus serviços existentes e explore o processamento em lote para implantações em larga escala.

---

**Last Updated:** 2026-05-21  
**Tested With:** GroupDocs.Signature 23.10 for Java  
**Author:** GroupDocs  

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY" + "/sample.pdf";
String fileName = new java.io.File(filePath).getName();
String outputPath = "YOUR_OUTPUT_DIRECTORY" + "/SignedWithBarcodeGS1CompositeBar/" + fileName;
```

```java
String documentDir = System.getenv("DOCUMENT_DIR");
String outputDir = System.getenv("OUTPUT_DIR");
```

```java
Signature signature = new Signature(filePath);
```

## Tutoriais Relacionados

- [Criar Assinatura de Código de Barras em Java – Atualizar Códigos de Barras em PDF](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [Verificar Código de Barras & QR Code em Java - Guia Completo de Segurança de Documentos](/signature/java/search-verification/verify-barcode-qr-code-signatures-groupdocs-java/)
- [Assinatura de PDF com Código de Barras HIBC - Solução Completa para Documentos de Saúde](/signature/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/)