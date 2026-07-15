---
date: '2026-07-15'
description: Aprenda como adicionar barcode PDF Java usando GroupDocs.Signature –
  guia passo a passo para assinar, verificar, pesquisar, atualizar e excluir assinaturas
  de barcode em documentos Java.
keywords:
- add barcode pdf java
- groupdocs barcode signature
- java document signing
lastmod: '2026-07-15'
linktitle: Guia de Barcode Signature Java
og_description: Aprenda como adicionar barcode PDF Java usando GroupDocs.Signature
  – guia passo a passo para assinar, verificar, pesquisar, atualizar e excluir assinaturas
  de barcode em documentos Java.
og_image_alt: Guide showing how to add barcode PDF Java using GroupDocs.Signature
og_title: Adicionar Barcode PDF Java – Assinar e Verificar com GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-07-15'
  description: Learn how to add barcode PDF Java using GroupDocs.Signature – step‑by‑step
    guide to sign, verify, search, update and delete barcode signatures in Java documents.
  headline: Add Barcode PDF Java – Sign & Verify with GroupDocs
  type: TechArticle
- description: Learn how to add barcode PDF Java using GroupDocs.Signature – step‑by‑step
    guide to sign, verify, search, update and delete barcode signatures in Java documents.
  name: Add Barcode PDF Java – Sign & Verify with GroupDocs
  steps:
  - name: Case mismatch (e.g., “John Smith” vs. “john smith”).
    text: Case mismatch (e.g., “John Smith” vs. “john smith”).
  - name: Extra whitespace in the encoded text.
    text: Extra whitespace in the encoded text.
  - name: Wrong barcode type specified in the verification options.
    text: Wrong barcode type specified in the verification options.
  - name: Searching the wrong page number.
    text: Searching the wrong page number.
  - name: '**Reuse Signature Instances** – Create a single `Signature` object per
      document and reuse it for multiple operations.'
    text: '**Reuse Signature Instances** – Create a single `Signature` object per
      document and reuse it for multiple operations.'
  - name: '**Search Specific Pages Only** – Limit the page range to where barcodes
      are expected.'
    text: '**Search Specific Pages Only** – Limit the page range to where barcodes
      are expected.'
  - name: '**Choose the Simplest Barcode Type** – Simpler barcodes generate faster;
      only use QR or Data Matrix when you truly need the extra capacity.'
    text: '**Choose the Simplest Barcode Type** – Simpler barcodes generate faster;
      only use QR or Data Matrix when you truly need the extra capacity.'
  - name: '**Never Encode Sensitive Personal Data** – Barcodes are easily readable;
      avoid PII such as SSNs or passwords.'
    text: '**Never Encode Sensitive Personal Data** – Barcodes are easily readable;
      avoid PII such as SSNs or passwords.'
  - name: '**Validate Server‑Side** – Never trust client‑side verification alone;
      always re‑verify on a trusted backend.'
    text: '**Validate Server‑Side** – Never trust client‑side verification alone;
      always re‑verify on a trusted backend.'
  - name: '**Add Timestamps** – Include a timestamp in the barcode payload to prevent
      replay attacks.'
    text: '**Add Timestamps** – Include a timestamp in the barcode payload to prevent
      replay attacks.'
  type: HowTo
- questions:
  - answer: Yes – the library is fully compatible with JDK 8, 11, and 17.
    question: Can I use GroupDocs.Signature with Java 17?
  - answer: When you use Code128 or QR with sufficient size and contrast, the barcode
      remains scannable after printing and scanning.
    question: Does the barcode survive a print‑scan cycle?
  - answer: There is no hard limit; however, for optimal performance keep the total
      count below **200** per document.
    question: How many barcodes can a single document contain?
  - answer: A temporary license removes evaluation watermarks; a full license is mandatory
      for any production deployment.
    question: Is a license required for development builds?
  - answer: Yes – provide the password when creating the `Signature` object; the API
      will unlock the file internally.
    question: Can I sign password‑protected PDFs?
  type: FAQPage
tags:
- barcode signature
- groupdocs
- java
- pdf
- document signing
title: Adicionar Barcode PDF Java – Assinar e Verificar com GroupDocs
type: docs
url: /pt/java/digital-signatures/java-document-signature-groupdocs-signature-barcode/
weight: 1
---

# Adicionar Barcode PDF Java – Assinar & Verificar com GroupDocs

Se você precisa de uma maneira rápida e visual de marcar documentos para fluxos de trabalho internos, adicionar um barcode a um PDF em Java é a solução perfeita. Com **GroupDocs.Signature**, você pode incorporar, verificar, pesquisar, atualizar e excluir assinaturas de barcode sem a sobrecarga de assinaturas digitais baseadas em PKI. Este tutorial orienta você em cada passo, desde a configuração do ambiente até as melhores práticas prontas para produção.

## Respostas Rápidas
- **Qual biblioteca adiciona barcode a PDFs em Java?** GroupDocs.Signature for Java.  
- **Posso assinar PDF, Word e imagens?** Sim – a API suporta mais de 30 formatos.  
- **Preciso de licença para desenvolvimento?** Uma licença temporária de 30 dias é gratuita; uma licença completa é necessária para produção.  
- **Quantas linhas de código para assinar um PDF?** Apenas duas linhas: criar um objeto `Signature` e chamar `sign`.  
- **A verificação de barcode diferencia maiúsculas/minúsculas?** Sim – o texto deve coincidir exatamente, incluindo maiúsculas/minúsculas e espaços em branco.

## O que é add barcode pdf java?
`add barcode pdf java` refere‑se ao processo de usar código Java para incorporar um barcode (como Code128, QR ou Data Matrix) em um arquivo PDF. Essa técnica fornece uma marca legível por máquina que pode ser escaneada ou verificada programaticamente, permitindo rastreamento rápido de documentos em sistemas internos.

## Por que usar assinaturas de barcode em vez de assinaturas digitais completas?
As assinaturas de barcode são **30‑50 % mais rápidas** de gerar e verificar que assinaturas digitais baseadas em PKI, e funcionam de forma confiável após um ciclo de impressão‑digitalização. Elas também não exigem gerenciamento de certificados, tornando‑as ideais para fluxos de trabalho internos de alto volume onde a prova criptográfica não é obrigatória.

## Pré‑requisitos

- **Java Development Kit (JDK) 8+** – Java 11 ou 17 é recomendado para melhor desempenho.  
- **IDE** – IntelliJ IDEA ou Eclipse (os exemplos usam sintaxe do IntelliJ).  
- **Ferramenta de build** – Maven ou Gradle para gerenciamento de dependências.  

### Adicionando GroupDocs.Signature ao Seu Projeto

A maneira mais fácil de começar é adicionar a biblioteca através da sua ferramenta de build. Veja como:

**Usuários Maven** – Adicione isto ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Usuários Gradle** – Adicione isto ao seu `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Download Direto do JAR** – Se preferir configuração manual, obtenha o JAR em [GroupDocs.Signature releases](https://releases.groupdocs.com/signature/java/) e adicione‑o ao seu classpath.

### Obtendo Sua Licença

GroupDocs.Signature não é gratuito para uso em produção, mas você tem opções flexíveis:

- **Teste Gratuito** – Baixe da [página de download do GroupDocs](https://releases.groupdocs.com/signature/java/) para testar recursos (marcas d'água de avaliação são adicionadas).  
- **Licença Temporária** – Obtenha 30 dias de acesso total através da [página de licença temporária do GroupDocs](https://purchase.groupdocs.com/temporary-license/) – ideal para provas de conceito.  
- **Licença Completa** – Para implantações em produção, confira as [opções de compra do GroupDocs](https://purchase.groupdocs.com/buy).  

**Dica profissional:** Comece com a licença temporária para desenvolvimento; ela remove as marcas d'água quando você troca para uma chave permanente.

### Verificação Rápida do Ambiente

Depois de adicionar a dependência, execute um teste simples:

```java
import com.groupdocs.signature.Signature;

public class SignatureTest {
    public static void main(String[] args) {
        try {
            Signature signature = new Signature("test.pdf");
            System.out.println("GroupDocs.Signature initialized successfully!");
            signature.dispose();
        } catch (Exception e) {
            System.err.println("Setup issue: " + e.getMessage());
        }
    }
}
```

Se o programa executar sem erros, seu ambiente está pronto. Se encontrar problemas, verifique a versão do JDK e a versão exata da biblioteca que você adicionou.

## Quando Usar Assinaturas de Barcode

As assinaturas de barcode se destacam em cenários específicos:

- **Fluxos de Trabalho Internos de Documentos** – Rastreie faturas, pedidos de compra ou memorandos através de cadeias de aprovação.  
- **Processamento de Alto Volume** – Assine milhares de documentos rapidamente; a geração de barcode é até **2× mais rápida** que a assinatura digital completa.  
- **Pontes Impressão‑Digitalização** – Barcodes sobrevivem ao ciclo impressão‑digitalização, tornando‑os ideais para processos híbridos papel‑digital.  
- **Integração com Sistemas Legados** – Scanners de barcode existentes podem ler as marcas sem software adicional.  
- **Trilhas de Auditoria** – Incorpore IDs de transação ou timestamps que auditores podem verificar instantaneamente.

Evite assinaturas de barcode para contratos legais, documentos de alta segurança ou trocas com parceiros externos onde assinaturas digitais baseadas em PKI são exigidas.

## Configurando GroupDocs.Signature para Java

### Definição da Classe Principal

A classe `Signature` é o ponto de entrada para todas as operações de assinatura, verificação, pesquisa, atualização e exclusão no GroupDocs.Signature.

```java
import com.groupdocs.signature.Signature;
```

### Inicialização Básica

Crie um objeto `Signature` que aponte para o arquivo alvo:

```java
Signature signature = new Signature("path/to/your/document.pdf");
```

**Observações importantes**

- Os caminhos podem ser absolutos ou relativos; use `System.getProperty("user.home")` para compatibilidade multiplataforma.  
- GroupDocs suporta **30+ formatos de entrada e saída**, incluindo PDF, DOCX, XLSX, PPTX e PNG.  
- Sempre libere recursos com `signature.dispose()` ou um bloco try‑with‑resources:

```java
try (Signature signature = new Signature("path/to/your/document.pdf")) {
    // Your signing operations here
} catch (Exception e) {
    System.err.println("Error working with document: " + e.getMessage());
}
```

Agora você está pronto para adicionar barcodes.

## Como adicionar um barcode a um PDF em Java?

Carregue o PDF de origem com `new Signature("input.pdf")`, configure um objeto `BarcodeSignature` (por exemplo, Code128 com o texto “John Smith”) e chame `sign` para gerar o arquivo assinado – tudo em três linhas concisas de código. Essa abordagem permite incorporar uma marca legível por máquina mantendo o layout original do documento, e funciona para qualquer formato suportado, não apenas PDFs.

### Implementação Passo a Passo

#### 1. Definir Caminhos de Arquivo

Defina as localizações dos arquivos de origem e de saída:

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/signed_sample.docx";
```

#### 2. Criar o Manipulador de Assinatura

Inicialize o manipulador com o documento de origem:

```java
Signature signature = new Signature(filePath);
```

#### 3. Configurar Opções de Barcode

Um objeto `BarcodeSignature` define as propriedades visuais e de dados do barcode a ser incorporado. Defina o tipo de barcode, texto codificado, posição, tamanho, cor e fonte legível opcional:

```java
BarcodeSignOptions signOptions = new BarcodeSignOptions("John Smith", BarcodeTypes.Code128);
signOptions.setVerticalAlignment(VerticalAlignment.Top);
signOptions.setHorizontalAlignment(HorizontalAlignment.Center);
signOptions.setWidth(100);
signOptions.setHeight(40);
signOptions.setMargin(new java.awt.Rectangle(20, 20, 0, 0));
signOptions.setForeColor(Color.RED);

SignatureFont signatureFont = new SignatureFont();
signatureFont.setSize(12);
signatureFont.setFamilyName("Comic Sans MS");
signOptions.setFont(signatureFont);
```

> **Dica profissional:** Se a string codificada exceder 20 caracteres, aumente a largura do barcode para evitar erros de leitura.

#### 4. Aplicar a Assinatura

Execute a operação de assinatura e gere o arquivo de saída:

```java
signature.sign(outputFilePath, signOptions);
```

#### 5. Exemplo do Mundo Real

Em um sistema de aprovação de faturas você pode incorporar o ID do funcionário aprovador e um timestamp:

```java
String invoiceId = "INV-2025-0042";
String approver = "john.smith@company.com";
String timestamp = LocalDateTime.now().toString();

// Combine into barcode data
String barcodeData = invoiceId + "|" + approver + "|" + timestamp;

BarcodeSignOptions signOptions = new BarcodeSignOptions(barcodeData, BarcodeTypes.QR);
signOptions.setVerticalAlignment(VerticalAlignment.Bottom);
signOptions.setHorizontalAlignment(HorizontalAlignment.Right);

signature.sign(outputFilePath, signOptions);
```

O PDF resultante agora contém um barcode escaneável que codifica todos os metadados de aprovação necessários.

## Como posso verificar uma assinatura de barcode em um documento Java?

O método `Signature.verify` verifica um documento em busca de assinaturas de barcode que correspondam às opções fornecidas, retornando um booleano que indica se o barcode esperado está presente. A verificação é útil para fluxos de trabalho automatizados onde você precisa confirmar que um documento foi processado pela parte correta antes de prosseguir.

### Etapas de Verificação

#### 1. Carregar o Documento Assinado

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");
```

#### 2. Definir Critérios de Verificação

Especifique o texto exato, o formato do barcode e o número da página que você espera:

```java
BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
verifyOptions.setAllPages(false); // Only check the first page
verifyOptions.setPageNumber(1);
verifyOptions.setEncodeType(BarcodeTypes.Code128);
verifyOptions.setText("John Smith");
```

#### 3. Executar Verificação

Execute a checagem e trate o resultado:

```java
boolean isValid = signature.verify(verifyOptions) != null;

if (isValid) {
    System.out.println("Document signature verified successfully!");
} else {
    System.out.println("Warning: Signature verification failed!");
}
```

**Padrão comum:** Para simplesmente confirmar que *qualquer* barcode de um tipo dado existe, omita o filtro `setText`:

```java
BarcodeVerifyOptions flexibleOptions = new BarcodeVerifyOptions();
flexibleOptions.setAllPages(true);
flexibleOptions.setEncodeType(BarcodeTypes.Code128);
// No setText() call = accept any text with this barcode type

boolean hasAnySignature = signature.verify(flexibleOptions) != null;
```

Ou verifique apenas o formato do barcode sem se preocupar com o conteúdo:

```java
BarcodeVerifyOptions formatOnly = new BarcodeVerifyOptions();
formatOnly.setEncodeType(BarcodeTypes.QR);
// Confirms a QR code exists, regardless of content
```

> **Aviso:** A verificação diferencia maiúsculas/minúsculas e espaços; sempre faça trim e normalize os dados antes de assinar.

## Como pesquisar assinaturas de barcode dentro de um documento?

O método `Signature.search` varre um documento em busca de assinaturas de barcode que correspondam ao `BarcodeSearchOptions` fornecido, retornando uma coleção que inclui a localização de cada barcode, número da página e valor codificado. Essa capacidade permite extração em massa de metadados sem abrir cada arquivo manualmente.

### Workflow de Pesquisa

#### 1. Inicializar Pesquisa

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");
```

#### 2. Configurar Parâmetros de Pesquisa

Especifique intervalo de páginas, tipo de barcode ou filtros de texto:

```java
BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true); // Search the entire document
```

Opcionalmente restrinja a pesquisa para melhorar o desempenho:

```java
BarcodeSearchOptions narrowSearch = new BarcodeSearchOptions();
narrowSearch.setAllPages(false);
narrowSearch.setPageNumber(1); // Only search page 1
narrowSearch.setEncodeType(BarcodeTypes.Code128); // Only find Code128 barcodes
```

#### 3. Executar Pesquisa

```java
java.util.List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);

System.out.println("Found " + signatures.size() + " barcode signature(s)");

for (BarcodeSignature bcSignature : signatures) {
    System.out.println("Barcode Type: " + bcSignature.getEncodeType().getTypeName());
    System.out.println("Text: " + bcSignature.getText());
    System.out.println("Position: (" + bcSignature.getLeft() + ", " + bcSignature.getTop() + ")");
    System.out.println("Size: " + bcSignature.getWidth() + "x" + bcSignature.getHeight());
    System.out.println("---");
}
```

#### 4. Exemplo de Extração de Dados

Recupere dados de aprovação de cada barcode em um lote de faturas:

```java
List<BarcodeSignature> foundSignatures = signature.search(BarcodeSignature.class, searchOptions);

for (BarcodeSignature sig : foundSignatures) {
    String barcodeData = sig.getText();
    
    // Parse your custom format (remember our invoice example?)
    String[] parts = barcodeData.split("\\|");
    if (parts.length == 3) {
        String invoiceId = parts[0];
        String approver = parts[1];
        String timestamp = parts[2];
        
        System.out.println("Invoice " + invoiceId + " approved by " + approver + " at " + timestamp);
    }
}
```

> **Dica de desempenho:** Para documentos com mais de 100 páginas, sempre limite a pesquisa às páginas que realmente contêm barcodes; isso pode reduzir o tempo de execução em até **70 %**.

## Como atualizar uma assinatura de barcode existente?

O método `Signature.update` modifica atributos visuais de uma assinatura de barcode existente — como posição, tamanho ou cor — preservando os dados codificados originais. Isso é útil quando alterações de layout são necessárias após o documento já ter sido assinado.

### Procedimento de Atualização

#### 1. Encontrar Assinaturas para Atualizar

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");

BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true);

List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
```

#### 2. Modificar Propriedades Desejadas

```java
List<BarcodeSignature> signaturesToUpdate = new ArrayList<>();

if (!signatures.isEmpty()) {
    BarcodeSignature bcSignature = signatures.get(0); // Update the first found signature
    
    // Move it 100px right and 100px down
    bcSignature.setLeft(bcSignature.getLeft() + 100);
    bcSignature.setTop(bcSignature.getTop() + 100);
    
    // Make it bigger
    bcSignature.setWidth(200);
    bcSignature.setHeight(50);
    
    signaturesToUpdate.add(bcSignature);
}
```

Você pode alterar várias atributos de uma vez:

```java
bcSignature.setLeft(50);
bcSignature.setTop(50);
bcSignature.setWidth(150);
bcSignature.setHeight(45);
// Note: You can't change the encoded text or barcode type with update
// For that, you'd need to delete and re-sign
```

#### 3. Salvar Alterações

```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature.update(outputStream, signaturesToUpdate);

// If you want to save to a file instead:
// signature.update("path/to/updated_document.docx", signaturesToUpdate);
```

#### 4. Cenário do Mundo Real

Reposicione todas as assinaturas para evitar sobreposição com um novo logotipo da empresa:

```java
List<BarcodeSignature> allSignatures = signature.search(BarcodeSignature.class, searchOptions);
List<BarcodeSignature> toUpdate = new ArrayList<>();

for (BarcodeSignature sig : allSignatures) {
    // Move all signatures down by 50px to clear space for new logo
    if (sig.getTop() < 100) {
        sig.setTop(sig.getTop() + 50);
        toUpdate.add(sig);
    }
}

if (!toUpdate.isEmpty()) {
    signature.update(outputStream, toUpdate);
    System.out.println("Repositioned " + toUpdate.size() + " signature(s)");
}
```

> **Limitação:** Alterar o texto codificado requer exclusão e inserção de uma nova assinatura.

## Como excluir assinaturas de barcode de um documento?

O método `Signature.delete` remove permanentemente as assinaturas de barcode selecionadas de um documento, apagando tanto o elemento visual quanto seus dados codificados. Use esta operação ao limpar assinaturas de teste ou quando um barcode não for mais relevante.

### Etapas de Exclusão

#### 1. Localizar Assinaturas

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");

BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true);

List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
```

#### 2. Excluir Assinaturas Selecionadas

```java
List<BarcodeSignature> signaturesToDelete = new ArrayList<>();

// Delete all Code128 signatures (for example)
for (BarcodeSignature sig : signatures) {
    if (sig.getEncodeType().equals(BarcodeTypes.Code128)) {
        signaturesToDelete.add(sig);
    }
}

if (!signaturesToDelete.isEmpty()) {
    boolean result = signature.delete(signaturesToDelete);
    
    if (result) {
        System.out.println("Successfully deleted " + signaturesToDelete.size() + " signature(s)");
    } else {
        System.err.println("Failed to delete signatures");
    }
}
```

#### 3. Exemplo de Exclusão Condicional

Remova apenas barcodes mais antigos que um timestamp específico (assumindo que o timestamp faz parte do texto codificado):

```java
LocalDateTime cutoffDate = LocalDateTime.now().minusDays(30);
List<BarcodeSignature> outdatedSignatures = new ArrayList<>();

for (BarcodeSignature sig : signatures) {
    try {
        String text = sig.getText();
        // Assuming format like "data|timestamp"
        String[] parts = text.split("\\|");
        if (parts.length > 1) {
            LocalDateTime sigDate = LocalDateTime.parse(parts[1]);
            if (sigDate.isBefore(cutoffDate)) {
                outdatedSignatures.add(sig);
            }
        }
    } catch (Exception e) {
        // Skip signatures that don't match our format
        continue;
    }
}

if (!outdatedSignatures.isEmpty()) {
    signature.delete(outdatedSignatures);
    System.out.println("Removed " + outdatedSignatures.size() + " outdated signature(s)");
}
```

> **Cuidado:** A exclusão não pode ser desfeita; sempre trabalhe em uma cópia dos arquivos de produção durante testes.

#### 4. Padrão de Exclusão em Lote

Limpe assinaturas de teste antes de um lançamento:

```java
// Remove all signatures containing "TEST" in their text
List<BarcodeSignature> testSignatures = signatures.stream()
    .filter(sig -> sig.getText().toUpperCase().contains("TEST"))
    .collect(Collectors.toList());

if (!testSignatures.isEmpty()) {
    signature.delete(testSignatures);
    System.out.println("Cleaned up " + testSignatures.size() + " test signature(s)");
}
```

## Tipos de Barcode: Um Guia Prático

Escolher o barcode correto impacta a confiabilidade da leitura, a capacidade de dados e a compatibilidade da impressora.

### Code128 (Escolha Mais Comum)

- **Quando usar:** Dados alfanuméricos, alta densidade, documentos impressos.  
- **Prós:** Compacto, funciona com scanners padrão, imprime claramente em tamanhos pequenos.  
- **Contras:** Limitado ao ASCII, menos resistente a erros que códigos 2‑D.  

Exemplo:

```java
BarcodeSignOptions code128 = new BarcodeSignOptions("INV-2025-042", BarcodeTypes.Code128);
```

### QR Code (Melhor para Mobile)

- **Quando usar:** Leitura móvel, grande carga de dados (URLs, JSON, etc.), documentos que podem ser danificados.  
- **Prós:** Até 4 000 caracteres, correção de erro integrada, amigável a smartphones.  
- **Contras:** Pegada visual maior, requer resolução mais alta para tamanhos pequenos.  

Exemplo:

```java
String jsonData = "{\"invoice\":\"INV-042\",\"amount\":1500.00,\"approver\":\"john@company.com\"}";
BarcodeSignOptions qrCode = new BarcodeSignOptions(jsonData, BarcodeTypes.QR);
```

### Code39 (Confiável Antigo)

- **Quando usar:** Ambientes com scanners legados, necessidade de texto legível por humanos.  
- **Prós:** Amplo suporte legado, formato simples, sem necessidade de checksum.  
- **Contras:** Baixa densidade de dados, conjunto de caracteres limitado, ocupa mais espaço.  

### Data Matrix (Potência Compacta)

- **Quando usar:** Espaço extremamente limitado, marcação de itens pequenos, dados de alta densidade.  
- **Prós:** Muito compacto, forte correção de erro, funciona em superfícies curvas.  
- **Contras:** Requer impressão de alta qualidade, suporte de scanner menos comum.  

#### Comparação Rápida

| Tipo de Barcode | Capacidade de Dados | Melhor Uso | Tamanho Típico |
|-----------------|---------------------|------------|----------------|
| Code128         | ~100 chars          | Marcação genérica | Pequeno |
| QR Code         | ~4 000 chars        | Leitura móvel, dados ricos | Médio |
| Code39          | ~43 chars           | Hardware legado | Grande |
| Data Matrix     | ~3 000 chars        | Espaços minúsculos, tags industriais | Muito pequeno |

**Recomendação:** Comece com **Code128** para IDs simples. Troque para **QR** quando precisar incorporar URLs ou payloads maiores. Use **Code39** apenas para integrações legadas.

## Problemas Comuns & Soluções

### Problema: “Barcode Não Encontrado Durante a Verificação”

**Sintomas:** A verificação retorna `false` mesmo que o barcode esteja visível.

**Causas típicas**

1. Diferença de maiúsculas/minúsculas (ex.: “John Smith” vs. “john smith”).  
2. Espaço em branco extra no texto codificado.  
3. Tipo de barcode errado especificado nas opções de verificação.  
4. Pesquisa na página errada.

**Solução:** Normalize o texto antes de assinar e verificar, e assegure que `setEncodeType` corresponda ao tipo original.

```java
// Always normalize your data
String signatureText = originalText.trim().toLowerCase();

// When signing:
BarcodeSignOptions signOptions = new BarcodeSignOptions(signatureText, BarcodeTypes.Code128);

// When verifying:
BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
verifyOptions.setText(signatureText); // Use the same normalized text
verifyOptions.setEncodeType(BarcodeTypes.Code128);
```

### Problema: “Barcode Aparece Borrado ou Illegível”

**Sintomas:** Barcodes impressos não podem ser escaneados.

**Causas**

- Dimensões do barcode muito pequenas para os dados codificados.  
- Configurações de impressora de baixa resolução.  
- Contraste insuficiente entre a cor do barcode e o fundo.

**Solução:** Aumente a largura/altura do barcode, use cores de alto contraste (preto sobre branco) e configure a DPI da impressora para pelo menos 300 dpi.

```java
// Increase size for longer strings
int dataLength = barcodeText.length();
int minWidth = Math.max(100, dataLength * 10); // 10px per character minimum

BarcodeSignOptions signOptions = new BarcodeSignOptions(barcodeText, BarcodeTypes.Code128);
signOptions.setWidth(minWidth);
signOptions.setHeight(60); // Taller = easier to scan

// Use high-contrast colors
signOptions.setForeColor(Color.BLACK); // Black on white is most reliable
signOptions.setBackColor(Color.WHITE);
```

### Problema: “OutOfMemoryError com Documentos Grandes”

**Sintomas:** Aplicação trava ao processar PDFs com centenas de páginas.

**Causa:** A biblioteca carrega todo o documento na memória.

**Solução:** Habilite o modo de streaming e processe as páginas incrementalmente.

```java
// Process pages in batches instead of all at once
BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(false);

List<BarcodeSignature> allSignatures = new ArrayList<>();

for (int page = 1; page <= totalPages; page++) {
    searchOptions.setPageNumber(page);
    List<BarcodeSignature> pageSignatures = signature.search(BarcodeSignature.class, searchOptions);
    allSignatures.addAll(pageSignatures);
    
    // Process and clear as you go
    if (page % 10 == 0) {
        System.gc(); // Suggest garbage collection every 10 pages
    }
}
```

### Problema: “Posição da Assinatura Inconsistente entre Tipos de Documento”

**Sintomas:** Barcodes aparecem em locais diferentes ao assinar PDFs vs. documentos Word.

**Causa:** PDF usa origem no canto inferior‑esquerdo, enquanto Word usa origem no canto superior‑esquerdo.

**Solução:** Detecte o tipo de documento e aplique a transformação de coordenadas apropriada.

```java
// Use relative positioning instead of absolute
signOptions.setVerticalAlignment(VerticalAlignment.Bottom);
signOptions.setHorizontalAlignment(HorizontalAlignment.Right);

// Then use margins for fine-tuning
Padding margin = new Padding();
margin.setRight(50); // 50px from right edge
margin.setBottom(50); // 50px from bottom
signOptions.setMargin(margin);

// This works consistently across PDF, DOCX, XLSX, etc.
```

### Problema: “Assinaturas Atualizadas Perdem Formatação”

**Sintomas:** Após chamar `update`, a cor ou fonte do barcode muda inesperadamente.

**Causa:** Nem todas as propriedades visuais são preservadas durante a atualização.

**Solução:** Reaplique as configurações visuais após a chamada de atualização.

```java
// When updating, explicitly set all visual properties
bcSignature.setLeft(newLeft);
bcSignature.setTop(newTop);
bcSignature.setWidth(originalWidth); // Don't forget these!
bcSignature.setHeight(originalHeight);
// Note: Color and font can't be updated - you'd need to delete and re-sign
```

## Melhores Práticas para Produção

### Otimização de Performance

1. **Reutilizar Instâncias de Signature** – Crie um único objeto `Signature` por documento e reutilize‑o para múltiplas operações.

```java
// Bad - Creates new instance each time
public void processDocument(String path) {
    Signature sig1 = new Signature(path);
    sig1.search(/* ... */);
    
    Signature sig2 = new Signature(path); // Unnecessary reload
    sig2.verify(/* ... */);
}

// Good - Reuse the same instance
public void processDocument(String path) {
    try (Signature signature = new Signature(path)) {
        signature.search(/* ... */);
        signature.verify(/* ... */);
        signature.update(/* ... */);
    }
}
```

2. **Pesquisar Apenas Páginas Específicas** – Limite o intervalo de páginas onde os barcodes são esperados.

```java
// Slow for 100+ page documents
BarcodeSearchOptions slowSearch = new BarcodeSearchOptions();
slowSearch.setAllPages(true);

// Fast - only check where signatures actually are
BarcodeSearchOptions fastSearch = new BarcodeSearchOptions();
fastSearch.setAllPages(false);
fastSearch.setPageNumber(1); // Only check cover page
```

3. **Escolher o Tipo de Barcode Mais Simples** – Barcodes mais simples são gerados mais rápido; use QR ou Data Matrix somente quando realmente precisar da capacidade extra.

```java
// Overkill for simple IDs
BarcodeSignOptions slow = new BarcodeSignOptions("12345", BarcodeTypes.QR);

// Faster and more appropriate
BarcodeSignOptions fast = new BarcodeSignOptions("12345", BarcodeTypes.Code128);
```

### Considerações de Segurança

1. **Nunca Codificar Dados Pessoais Sensíveis** – Barcodes são facilmente legíveis; evite PII como CPF ou senhas.

```java
// Bad - exposes sensitive data
String barcodeData = "SSN:123-45-6789|Password:hunter2";

// Good - use reference IDs
String barcodeData = "USER-REF-7721X"; // Look up sensitive data server-side
```

2. **Validar no Lado do Servidor** – Nunca confie apenas na verificação do cliente; sempre re‑verifique em um backend confiável.

```java
// Client scans barcode and extracts "APPROVED-BY-ADMIN"
// Always verify server-side:
public boolean verifyApproval(String documentId, String scannedData) {
    // Load document from secure storage
    Signature signature = new Signature(getSecureDocument(documentId));
    
    BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
    verifyOptions.setText(scannedData);
    
    boolean isValid = signature.verify(verifyOptions) != null;
    
    // Also check against your database
    boolean isInDatabase = checkApprovalDatabase(documentId, scannedData);
    
    return isValid && isInDatabase;
}
```

3. **Adicionar Timestamps** – Inclua um timestamp no payload do barcode para prevenir ataques de replay.

```java
import java.time.LocalDateTime;
import java.time.temporal.ChronoUnit;

String timestamp = LocalDateTime.now().truncatedTo(ChronoUnit.SECONDS).toString();
String barcodeData = "APPROVAL|" + userId + "|" + timestamp;

// When verifying, check the timestamp isn't too old
public boolean isSignatureRecent(String barcodeData, int maxAgeHours) {
    String[] parts = barcodeData.split("\\|");
    if (parts.length < 3) return false;
    
    LocalDateTime signatureTime = LocalDateTime.parse(parts[2]);
    LocalDateTime now = LocalDateTime.now();
    
    long hoursSince = ChronoUnit.HOURS.between(signatureTime, now);
    return hoursSince <= maxAgeHours;
}
```

### Padrões de Tratamento de Erros

- **Sempre Use Try‑With‑Resources** para garantir que objetos `Signature` sejam descartados.

```java
try (Signature signature = new Signature(documentPath)) {
    // Your operations here
    signature.sign(outputPath, signOptions);
} catch (Exception e) {
    logger.error("Failed to sign document: " + documentPath, e);
    throw new DocumentSigningException("Could not process document", e);
}
```

- **Validar Acesso ao Arquivo** antes de tentar assinar.

```java
public void signDocument(String inputPath, String outputPath) {
    File inputFile = new File(inputPath);
    
    if (!inputFile.exists()) {
        throw new IllegalArgumentException("Input file not found: " + inputPath);
    }
    
    if (!inputFile.canRead()) {
        throw new SecurityException("Cannot read input file: " + inputPath);
    }
    
    File outputDir = new File(outputPath).getParentFile();
    if (outputDir != null && !outputDir.exists()) {
        outputDir.mkdirs();
    }
    
    try (Signature signature = new Signature(inputPath)) {
        signature.sign(outputPath, signOptions);
    }
}
```

- **Sincronizar Acesso** se múltiplas threads puderem trabalhar no mesmo arquivo.

```java
import java.util.concurrent.locks.ReentrantLock;
import java.util.concurrent.ConcurrentHashMap;

public class SignatureManager {
    private final ConcurrentHashMap<String, ReentrantLock> documentLocks = new ConcurrentHashMap<>();
    
    public void signDocument(String documentPath, BarcodeSignOptions options) {
        ReentrantLock lock = documentLocks.computeIfAbsent(documentPath, k -> new ReentrantLock());
        
        lock.lock();
        try (Signature signature = new Signature(documentPath)) {
            signature.sign(documentPath + ".signed", options);
        } finally {
            lock.unlock();
        }
    }
}
```

### Testando Sua Implementação

**Modelo de Teste Unitário**

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.io.TempDir;
import static org.junit.jupiter.api.Assertions.*;

public class BarcodeSignatureTest {
    
    @TempDir
    Path tempDir;
    
    @Test
    public void testSignAndVerify() throws Exception {
        // Setup
        String testDoc = "test-document.pdf";
        String outputDoc = tempDir.resolve("signed-test.pdf").toString();
        String testData = "TEST-USER-12345";
        
        // Sign
        try (Signature signature = new Signature(testDoc)) {
            BarcodeSignOptions signOptions = new BarcodeSignOptions(testData, BarcodeTypes.Code128);
            signature.sign(outputDoc, signOptions);
        }
        
        // Verify
        try (Signature signature = new Signature(outputDoc)) {
            BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
            verifyOptions.setText(testData);
            verifyOptions.setEncodeType(BarcodeTypes.Code128);
            
            boolean isValid = signature.verify(verifyOptions) != null;
            assertTrue(isValid, "Signature should be valid");
        }
    }
    
    @Test
    public void testSearchFindsSignature() throws Exception {
        String signedDoc = "signed-document.pdf";
        
        try (Signature signature = new Signature(signedDoc)) {
            BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
            searchOptions.setAllPages(true);
            
            List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
            
            assertFalse(signatures.isEmpty(), "Should find at least one signature");
            assertEquals("TEST-USER-12345", signatures.get(0).getText());
        }
    }
}
```

**Checklist de Integração**

- ✅ Testar todos os formatos suportados (PDF, DOCX, XLSX, PPTX, PNG).  
- ✅ Verificar se os barcodes sobrevivem ao ciclo impressão‑digitalização.  
- ✅ Stress‑test com strings de dados de comprimento máximo.  
- ✅ Confirmar posicionamento em tamanhos A4, Letter e personalizados.  
- ✅ Executar assinaturas concorrentes em múltiplos documentos.  
- ✅ Monitorar uso de memória para documentos > 500 páginas.  
- ✅ Garantir que scanners de barcode leiam a saída de forma confiável.

### Registro e Monitoramento

Adicione logs significativos ao redor de cada operação:

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class DocumentSigningService {
    private static final Logger logger = LoggerFactory.getLogger(DocumentSigningService.class);
    
    public void signDocument(String docPath, String barcodeData) {
        logger.info("Starting signature process for document: {}", docPath);
        logger.debug("Barcode data length: {} characters", barcodeData.length());
        
        try (Signature signature = new Signature(docPath)) {
            BarcodeSignOptions options = new BarcodeSignOptions(barcodeData, BarcodeTypes.Code128);
            
            long startTime = System.currentTimeMillis();
            signature.sign(docPath + ".signed", options);
            long duration = System.currentTimeMillis() - startTime;
            
            logger.info("Successfully signed document in {}ms", duration);
        } catch (Exception e) {
            logger.error("Failed to sign document: {}", docPath, e);
            throw new RuntimeException("Signature operation failed", e);
        }
    }
}
```

Monitore métricas chave como tempo de processamento, consumo de memória e taxa de erros:

```java
// Track success/failure rates
metricsService.incrementCounter("signature.sign.success");
metricsService.incrementCounter("signature.verify.failure");

// Track performance
metricsService.recordTimer("signature.sign.duration", duration);

// Track document sizes
metricsService.recordHistogram("signature.document.pages", pageCount);
```

## Dicas Profissionais de Uso Real

**Estratégia de Processamento em Lote**

Ao lidar com centenas de arquivos, processe‑os em lotes e reporte o progresso:

```java
public void signBatch(List<String> documents, String barcodePrefix) {
    int total = documents.size();
    int completed = 0;
    int failed = 0;
    
    for (String docPath : documents) {
        try {
            String barcodeData = barcodePrefix + "-" + UUID.randomUUID().toString();
            signDocument(docPath, barcodeData);
            completed++;
            
            if (completed % 10 == 0) {
                logger.info("Progress: {}/{} documents signed", completed, total);
            }
        } catch (Exception e) {
            failed++;
            logger.warn("Failed to sign: {}", docPath, e);
        }
    }
    
    logger.info("Batch complete: {} succeeded, {} failed", completed, failed);
}
```

**Externalizar Configuração**

Armazene as configurações de barcode (tipo, tamanho, cor) em um arquivo de propriedades para ajuste fácil sem recompilar:

```java
public class BarcodeConfig {
    private int defaultWidth = 100;
    private int defaultHeight = 40;
    private String defaultBarcodeType = "Code128";
    private String defaultColor = "BLACK";
    
    // Load from properties file or environment variables
    public BarcodeConfig() {
        this.defaultWidth = Integer.parseInt(
            System.getProperty("barcode.width", "100")
        );
        // ... load other properties
    }
    
    public BarcodeSignOptions createDefaultOptions(String text) {
        BarcodeSignOptions options = new BarcodeSignOptions(text, getBarcodeType());
        options.setWidth(defaultWidth);
        options.setHeight(defaultHeight);
        options.setForeColor(getColor());
        return options;
    }
}
```

**Padronizar Payload de Barcode**

Use um formato delimitado como `EMPID|TIMESTAMP|DOCID` para simplificar e tornar consistente o parsing:

```java
public class BarcodeDataBuilder {
    private String userId;
    private String action;
    private LocalDateTime timestamp;
    private String documentId;
    
    public BarcodeDataBuilder setUserId(String userId) {
        this.userId = userId;
        return this;
    }
    
    public BarcodeDataBuilder setAction(String action) {
        this.action = action;
        return this;
    }
    
    public BarcodeDataBuilder setDocumentId(String documentId) {
        this.documentId = documentId;
        return this;
    }
    
    public String build() {
        this.timestamp = LocalDateTime.now();
        
        // Format: VERSION|USER|ACTION|DOC_ID|TIMESTAMP|CHECKSUM
        String data = String.join("|",
            "v1",
            userId,
            action,
            documentId,
            timestamp.toString()
        );
        
        // Add simple checksum
        int checksum = data.hashCode();
        return data + "|" + checksum;
    }
    
    public static ParsedBarcodeData parse(String barcodeData) {
        String[] parts = barcodeData.split("\\|");
        if (parts.length != 6 || !parts[0].equals("v1")) {
            throw new IllegalArgumentException("Invalid barcode format");
        }
        
        return new ParsedBarcodeData(parts[1], parts[2], parts[3], 
                                     LocalDateTime.parse(parts[4]));
    }
}

// Usage:
String barcodeData = new BarcodeDataBuilder()
    .setUserId("john.smith")
    .setAction("APPROVED")
    .setDocumentId("INV-2025-042")
    .build();
```

**Detectar Tipo de Documento Automaticamente**

Ajuste as dimensões do barcode com base se o alvo é PDF, Word ou uma imagem:

```java
public BarcodeSignOptions getOptimalOptions(String documentPath, String text) {
    String extension = documentPath.substring(documentPath.lastIndexOf(".") + 1).toLowerCase();
    
    BarcodeSignOptions options = new BarcodeSignOptions(text, BarcodeTypes.Code128);
    
    switch (extension) {
        case "pdf":
            // PDFs can handle larger, detailed barcodes
            options.setWidth(150);
            options.setHeight(50);
            break;
        case "docx":
        case "doc":
            // Word docs need compact signatures that don't disrupt flow
            options.setWidth(100);
            options.setHeight(35);
            options.setVerticalAlignment(VerticalAlignment.Bottom);
            break;
        case "xlsx":
        case "xls":
            // Excel needs signatures that don't obscure data
            options.setWidth(80);
            options.setHeight(30);
            options.setHorizontalAlignment(HorizontalAlignment.Right);
            break;
        default:
            // Safe defaults
            options.setWidth(100);
            options.setHeight(40);
    }
    
    return options;
}
```

## Recursos Adicionais

- [GroupDocs.Signature documentation](https://docs.groupdocs.com/signature/java/) – Guia completo da API e exemplos de uso.  
- [GroupDocs support forum](https://forum.groupdocs.com/c/signature/13) – Ajuda da comunidade e solução de problemas.  
- [API reference](https://apireference.groupdocs.com/signature/java) – Descrições detalhadas de métodos e parâmetros.

## Perguntas Frequentes

**P: Posso usar GroupDocs.Signature com Java 17?**  
R: Sim – a biblioteca é totalmente compatível com JDK 8, 11 e 17.

**P: O barcode sobrevive ao ciclo impressão‑digitalização?**  
R: Quando você usa Code128 ou QR com tamanho e contraste suficientes, o barcode permanece escaneável após impressão e digitalização.

**P: Quantos barcodes um único documento pode conter?**  
R: Não há limite rígido; porém, para desempenho ideal mantenha o total abaixo de **200** por documento.

**P: Uma licença é necessária para builds de desenvolvimento?**  
R: Uma licença temporária remove as marcas d'água de avaliação; uma licença completa é obrigatória para qualquer implantação em produção.

**P: Posso assinar PDFs protegidos por senha?**  
R: Sim – forneça a senha ao criar o objeto `Signature`; a API desbloqueará o arquivo internamente.

**Última Atualização:** 2026-07-15  
**Testado com:** GroupDocs.Signature 23.9 for Java  
**Autor:** GroupDocs  

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

## Tutoriais Relacionados

- [Como Verificar Assinaturas de Barcode em Java com GroupDocs.Signature](/signature/java/search-verification/groupdocs-signature-java-document-verification/)
- [Como Pesquisar Assinaturas Digitais em Documentos Java com GroupDocs](/signature/java/search-verification/groupdocs-signature-java-digital-search-tutorial/)
- [Tutorial de Assinatura de Barcode Java - Adicionar, Verificar & Gerenciar Barcodes em PDFs](/signature/java/barcode-signatures/)