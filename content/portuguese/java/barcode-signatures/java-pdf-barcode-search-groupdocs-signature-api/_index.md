---
categories:
- Java Development
- Document Processing
date: '2026-03-01'
description: Aprenda como ler arquivos PDF com código QR usando Java e GroupDocs.Signature.
  Guia passo a passo, exemplos de código, solução de problemas e cenários do mundo
  real.
keywords: read qr code pdf, Java barcode verification PDF, GroupDocs barcode search
  tutorial, extract barcode data from PDF Java, Java PDF barcode scanner
lastmod: '2026-03-01'
linktitle: Search PDF Barcodes Java
tags:
- barcode-search
- pdf-processing
- groupdocs
- java-tutorial
- document-verification
title: Como ler PDF com código QR usando Java e GroupDocs.Signature
type: docs
url: /pt/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/
weight: 1
---

# Como ler PDF com código QR usando Java

## Introdução

Já precisou extrair informações de código de barras de centenas de faturas PDF, etiquetas de envio ou documentos de inventário? A digitalização manual das páginas é tediosa e propensa a erros. Seja construindo um sistema automatizado de processamento de documentos ou verificando a autenticidade de produtos, encontrar códigos de barras de forma eficiente em PDFs pode ser desafiador.

Neste guia, você aprenderá como **ler PDFs com código QR** de forma eficiente usando a API GroupDocs.Signature. Esta poderosa API transforma o que poderia ser horas de trabalho manual em apenas algumas linhas de código. Você pode escanear documentos inteiros, localizar tipos específicos de códigos de barras (como QR codes ou Code128) e extrair seus dados automaticamente.

**O que você aprenderá:**
- Configurar o GroupDocs.Signature para Java em minutos  
- Pesquisar assinaturas de código de barras em documentos PDF  
- Configurar opções de pesquisa para resultados precisos e direcionados  
- Manipular diferentes tipos de códigos de barras (QR codes, EAN, Code128, etc.)  
- Resolver problemas comuns e otimizar o desempenho  

Vamos começar!

## Respostas Rápidas
- **O GroupDocs.Signature pode ler códigos QR de PDFs?** Sim, ele detecta QR, Data Matrix, PDF417 e muitos códigos de barras 1D.  
- **Preciso de licença para uso em produção?** É necessária uma licença comercial; um teste gratuito está disponível para avaliação.  
- **Qual versão do Java é necessária?** Java 8+ (Java 11+ recomendado).  
- **Como limitar a pesquisa a páginas específicas?** Use `BarcodeSearchOptions.setAllPages(false)` e defina `setPageNumber()`.  
- **A API é thread‑safe para processamento em lote?** Sim, quando você cria uma instância separada de `Signature` por thread.

## Por que pesquisar códigos de barras em PDFs?

Antes de entrarmos na parte técnica, veja por que isso importa em aplicações do mundo real:

**Cenários de Negócio Comuns**
- **Processamento de Faturas** – Extrair automaticamente números de pedido ou códigos de rastreamento de faturas de fornecedores.  
- **Gestão de Inventário** – Escanear catálogos de produtos e extrair códigos de barras SKU para atualizações de banco de dados.  
- **Envio & Logística** – Verificar códigos de rastreamento de pacotes em manifestos de envio.  
- **Autenticação de Documentos** – Validar documentos assinados verificando códigos de barras de segurança incorporados.  
- **Registros de Saúde** – Extrair IDs de pacientes ou códigos de prescrição de documentos médicos.  

A API GroupDocs.Signature cuida do trabalho pesado — você não precisa se preocupar com processamento de imagens, algoritmos de decodificação de códigos de barras ou complexidades de renderização de PDF. Tudo está embutido.

## Pré-requisitos

Antes de iniciar este tutorial, certifique-se de que você tem o seguinte pronto:

### Bibliotecas e Dependências Necessárias

Você precisará incluir a biblioteca GroupDocs.Signature em seu projeto Java. Veja como adicioná‑la usando Maven ou Gradle:

**Maven:**  
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle:**  
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Nota:** Sempre verifique a versão mais recente em [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/). Usar a versão mais recente garante que você obtenha correções de bugs e novos recursos.

### Configuração do Ambiente

- **JDK 8 ou superior** – O GroupDocs.Signature requer no mínimo Java 8 (Java 11+ recomendado para melhor desempenho).  
- **IDE** – Qualquer editor de texto funciona, mas IntelliJ IDEA ou Eclipse facilitarão sua vida com autocomplete e depuração.  
- **Documento PDF** – Tenha um PDF de teste com códigos de barras pronto (faturas, etiquetas de envio ou catálogos de produtos funcionam bem).

### Pré-requisitos de Conhecimento

Você deve estar confortável com:
- Sintaxe básica de Java e conceitos orientados a objetos  
- Manipulação de exceções com blocos `try‑catch`  
- Trabalhar com bibliotecas externas em sua IDE  

Se você é novo em bibliotecas Java de terceiros, não se preocupe — vamos percorrer tudo passo a passo.

## Configurando o GroupDocs.Signature para Java

Começar com o GroupDocs.Signature leva apenas alguns minutos. Aqui está o processo completo de configuração:

### Passo 1: Adicionar a Dependência

Use Maven ou Gradle para incluir a biblioteca (veja o código acima). Após adicionar a dependência, atualize seu projeto para baixar os arquivos JAR.

### Passo 2: Aquisição de Licença

GroupDocs oferece várias opções de licenciamento:

- **Teste Gratuito** – Perfeito para testes. Baixe em [GroupDocs releases](https://releases.groupdocs.com/signature/java/).  
- **Licença Temporária** – Obtenha 30 dias de acesso total via a [Temporary License Page](https://purchase.groupdocs.com/temporary-license/).  
- **Licença Comercial** – Para uso em produção, compre uma licença em [GroupDocs Purchase](https://purchase.groupdocs.com/).  

**Dica Pro:** Comece com o teste gratuito para construir seu proof‑of‑concept, depois faça upgrade se a API atender às suas necessidades.

### Passo 3: Inicialização Básica

Veja como criar um objeto `Signature` para trabalhar com seu PDF:

```java
import com.groupdocs.signature.Signature;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample_signed.pdf"; // Replace with your PDF path
Signature signature = new Signature(filePath);
```

A classe `Signature` é seu ponto de entrada principal. Ela carrega o PDF na memória e fornece métodos para pesquisar, verificar e extrair dados de assinatura (incluindo códigos de barras).

**Importante**: Certifique‑se de que o caminho do arquivo está correto e o PDF existe. Erro comum de iniciantes? Usar barras invertidas no Windows sem escapá‑las (`C:\\Documents\\file.pdf` e não `C:\Documents\file.pdf`).

## Guia de Implementação

Agora vem a parte divertida — vamos escrever o código para pesquisar códigos de barras no seu PDF.

### Pesquisando Assinaturas de Código de Barras em um Documento

Esta seção mostra como escanear um PDF e localizar todas as assinaturas de código de barras. Vamos dividir em etapas digeríveis com explicações para cada parte.

#### Passo 1: Inicializar o Objeto Signature

Comece carregando seu documento PDF:

```java
import com.groupdocs.signature.Signature;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample_signed.pdf"; // Replace with actual file path
Signature signature = new Signature(filePath);
```

**O que está acontecendo aqui**  
A classe `Signature` abre seu PDF e o prepara para processamento. Pense nisso como abrir um arquivo em um editor de texto — você está carregando o documento na memória para poder trabalhar com ele.

**Nota do Mundo Real**  
Se você estiver processando PDFs de uploads de usuários, sempre valide o caminho do arquivo e verifique se ele existe antes de criar o objeto `Signature`. Isso evita erros crípticos mais tarde.

#### Passo 2: Criar BarcodeSearchOptions

Configure como você deseja pesquisar códigos de barras:

```java
import com.groupdocs.signature.options.search.BarcodeSearchOptions;

// Configure options for searching barcodes
BarcodeSearchOptions options = new BarcodeSearchOptions();
options.setAllPages(true); // Search every page in the document
```

**Opções de Configuração Principais**

- `setAllPages(true)`: Varre todas as páginas. Defina como `false` se você quiser verificar apenas páginas específicas (configure com `setPageNumber()`).
- **Por que isso importa**: Se você estiver processando faturas onde os códigos de barras estão sempre na página 1, pesquisar todas as páginas desperdiça recursos. Para manifestos de envio com várias páginas, você precisará de `setAllPages(true)`.

**Dica Pro**: Você também pode filtrar por tipo de código de barras (mais detalhes na seção **Tipos de Código de Barras Suportados** abaixo). Isso acelera as pesquisas quando você sabe exatamente o formato que procura.

#### Passo 3: Executar a Pesquisa e Manipular os Resultados

Agora execute a pesquisa e processe os resultados:

```java
import com.groupdocs.signature.domain.signatures.BarcodeSignature;
import java.util.List;

try {
    // Execute the barcode search
    List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, options);
    
    // Check if any barcodes were found
    if (signatures.isEmpty()) {
        System.out.println("No barcode signatures found in the document.");
    } else {
        System.out.println("Found " + signatures.size() + " barcode signature(s):\n");
        
        // Loop through each barcode and display details
        for (BarcodeSignature barcodeSignature : signatures) {
            System.out.println("----------------------------------------");
            System.out.println("Barcode Type: " + barcodeSignature.getEncodeType().getTypeName());
            System.out.println("Barcode Text: " + barcodeSignature.getText());
            System.out.println("Page Number: " + barcodeSignature.getPageNumber());
            System.out.println("Position: X=" + barcodeSignature.getLeft() + 
                             ", Y=" + barcodeSignature.getTop());
            System.out.println("Size: Width=" + barcodeSignature.getWidth() + 
                             ", Height=" + barcodeSignature.getHeight());
            System.out.println("----------------------------------------\n");
        }
    }
} catch (Exception e) {
    System.err.println("Error searching for barcodes: " + e.getMessage());
    e.printStackTrace();
} finally {
    // Always dispose of the signature object to free resources
    if (signature != null) {
        signature.dispose();
    }
}
```

**O que está acontecendo neste código**

1. **Execução da Pesquisa** – `signature.search()` varre o PDF e retorna uma lista de objetos `BarcodeSignature`.
2. **Verificação de Vazio** – Verifica se códigos de barras foram realmente encontrados (previne exceções de ponteiro nulo).
3. **Extração de Dados** – Para cada código de barras, extraímos:
   - **Tipo** – O formato do código de barras (QR Code, Code128, EAN13, etc.)
   - **Texto** – Os dados decodificados (número do pedido, código de rastreamento, SKU, etc.)
   - **Localização** – Número da página e coordenadas X/Y
   - **Dimensões** – Largura e altura (útil para validação)
4. **Tratamento de Erros** – O `try‑catch` impede falhas se algo der errado (PDF corrompido, arquivo ausente, etc.).
5. **Limpeza de Recursos** – O bloco `finally` garante que o objeto `Signature` seja descartado corretamente, liberando memória.

**Aplicação no Mundo Real**  
Suponha que você esteja processando etiquetas de envio. Você extrairia o valor `getText()` (número de rastreamento) e o armazenaria em seu banco de dados. O número da página indica qual etiqueta corresponde a qual remessa se você estiver processando documentos em lote.

### Filtrando por Tipo de Código de Barras

Você pode acelerar as pesquisas especificando o tipo de código de barras que está procurando:

```java
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

BarcodeSearchOptions options = new BarcodeSearchOptions();
options.setEncodeType(BarcodeTypes.QR); // Only search for QR codes
options.setAllPages(true);
```

**Quando Filtrar**  
Se você sabe que suas faturas contêm apenas códigos de barras Code128, filtrar por tipo reduz o tempo de processamento em 30‑50 % em documentos grandes.

## Tipos de Código de Barras Suportados

O GroupDocs.Signature pode detectar uma ampla gama de formatos de código de barras. Veja o que você pode pesquisar:

**Códigos de Barras 1D (Lineares)**
- **Code128** – Comum em envio e embalagem  
- **Code39** – Usado nas indústrias automotiva e de defesa  
- **EAN13/EAN8** – Códigos de barras de produtos de varejo (você vê esses em todos os produtos)  
- **UPC‑A/UPC‑E** – Padrão de varejo da América do Norte  
- **Interleaved2of5** – Armazém e distribuição  

**Códigos de Barras 2D (Matriz)**
- **QR Code** – O mais popular — usado para URLs, senhas de Wi‑Fi, informações de pagamento  
- **Data Matrix** – Formato compacto para itens pequenos (componentes eletrônicos)  
- **PDF417** – IDs governamentais, cartões de embarque, carteiras de motorista  
- **Aztec Code** – Bilhetes de transporte  

Filtrar por Tipo (exemplo mostrado anteriormente) ajuda a focar no formato exato que você precisa.

## Casos de Uso no Mundo Real

Veja como desenvolvedores estão usando a pesquisa de códigos de barras em produção:

### 1. Processamento Automatizado de Faturas

**Cenário** – Um departamento contábil recebe mais de 500 faturas de fornecedores por dia em PDFs.  
**Solução** – Escaneie cada PDF em busca de códigos de barras Code39 contendo números de fatura, correspondendo‑os automaticamente a pedidos de compra no sistema ERP. Isso elimina a entrada manual de dados e reduz erros.

```java
// Pseudo-code workflow
for (PDF invoice : invoiceBatch) {
    List<BarcodeSignature> barcodes = searchBarcodes(invoice);
    String invoiceNumber = barcodes.get(0).getText();
    updateERPSystem(invoiceNumber, invoice);
}
```

### 2. Atualizações de Inventário em Armazém

**Cenário** – Um armazém recebe remessas com listas de embalagem em PDF contendo SKUs de produtos como códigos de barras EAN13.  
**Solução** – Extraia todos os códigos de barras das listas de embalagem, atualize as contagens de inventário automaticamente e sinalize discrepâncias para revisão.

### 3. Autenticação de Documentos

**Cenário** – Documentos legais incluem códigos QR com assinaturas criptográficas para verificação de autenticidade.  
**Solução** – Pesquise códigos QR em contratos assinados, decodifique os dados da assinatura e verifique contra uma autoridade certificadora confiável. Isso garante que os documentos não foram adulterados.

### 4. Gestão de Registros de Saúde

**Cenário** – Arquivos de pacientes em hospitais contêm relatórios de laboratório em PDF com códigos de barras Code128 para IDs de amostras.  
**Solução** – Extraia automaticamente IDs de amostras e vincule resultados de laboratório aos registros de pacientes no sistema de informação hospitalar (HIS).

## Problemas Comuns e Soluções

Aqui estão problemas que você pode encontrar e como corrigi‑los:

### Problema 1: “Nenhum Código de Barras Encontrado” (Mas Você Sabe que Eles Existem)

**Causas Possíveis**
- A qualidade da imagem do código de barras está muito baixa (digitalizações borradas, pixeladas)  
- O PDF é baseado em imagem, mas o código de barras é muito pequeno  
- Você está pesquisando o tipo de código de barras errado  

**Soluções**
1. **Verifique a Resolução da Imagem** – Códigos de barras precisam de pelo menos 200 DPI para detecção confiável. Se você estiver digitalizando documentos, use 300 DPI ou mais.  
2. **Remova o Filtro de Tipo** – Tente pesquisar todos os tipos de códigos de barras primeiro (não defina `setEncodeType()`), depois restrinja quando identificar o que está no documento.  
3. **Verifique a Qualidade do Código de Barras** – Abra o PDF no Adobe Acrobat e dê zoom. Se o código de barras parecer borrado para você, será difícil para a API também.

### Problema 2: `OutOfMemoryError` com PDFs Grandes

**Causa** – Carregar um PDF de 500 páginas com imagens de alta resolução consome muita memória.  

**Solução**
1. **Processar Páginas em Lotes** – Em vez de `setAllPages(true)`, processe 50 páginas por vez:

```java
for (int startPage = 1; startPage <= totalPages; startPage += 50) {
    BarcodeSearchOptions options = new BarcodeSearchOptions();
    options.setPageNumber(startPage);
    options.setPagesSetup(new PagesSetup());
    options.getPagesSetup().setLastPage(Math.min(startPage + 49, totalPages));
    
    List<BarcodeSignature> batchResults = signature.search(BarcodeSignature.class, options);
    // Process results...
}
```

2. **Aumente o Tamanho do Heap da JVM** – Adicione `-Xmx4g` ao seu comando Java para alocar 4 GB de memória (ajuste conforme suas necessidades).

### Problema 3: Desempenho Lento em Documentos com Múltiplas Páginas

**Causa** – Pesquisar todas as páginas sequencialmente leva tempo, especialmente com códigos de barras complexos como PDF417.  

**Soluções**
1. **Processamento Paralelo** – Se os códigos de barras estiverem sempre em páginas específicas (ex.: página 1 de faturas), pesquise apenas essas páginas.  
2. **Cache de Resultados** – Se você estiver processando o mesmo documento várias vezes, faça cache dos dados dos códigos de barras para evitar re‑varredura.  
3. **Use SSDs** – A velocidade de I/O importa ao carregar PDFs grandes. SSDs reduzem o tempo de carregamento em 60‑70 % comparado a HDDs.

### Problema 4: Falsos Positivos (Detectando Padrões Aleatórios como Códigos de Barras)

**Causa** – Tabelas, grades ou padrões de linhas podem ser identificados erroneamente como códigos de barras.  

**Solução** – Valide os resultados verificando o comprimento e o formato do texto decodificado:

```java
for (BarcodeSignature barcode : signatures) {
    String text = barcode.getText();
    
    // Example: Invoice numbers are always 10 digits
    if (text.matches("\\d{10}")) {
        // Valid invoice number
        processBarcode(barcode);
    } else {
        System.out.println("Skipping invalid barcode: " + text);
    }
}
```

## Dicas de Desempenho para Documentos Grandes

Processando milhares de PDFs? Veja como otimizar:

### 1. Estratégia de Processamento em Lote

Em vez de processar arquivos um a um, use um pool de threads para lidar com vários PDFs simultaneamente:

```java
ExecutorService executor = Executors.newFixedThreadPool(4); // 4 parallel threads

for (String pdfPath : pdfFiles) {
    executor.submit(() -> {
        try (Signature sig = new Signature(pdfPath)) {
            List<BarcodeSignature> results = sig.search(BarcodeSignature.class, options);
            // Process results...
        } catch (Exception e) {
            e.printStackTrace();
        }
    });
}

executor.shutdown();
executor.awaitTermination(1, TimeUnit.HOURS);
```

**Ganho de Desempenho** – Processar 1 000 arquivos cai de ~2 horas para ~30 minutos em uma máquina quad‑core.

### 2. Reduzir o Escopo da Pesquisa

Se sua lógica de negócios permitir, limite a área de pesquisa:

```java
// Only search the top‑right corner where barcodes are typically placed
options.setRectangle(new Rectangle(400, 50, 150, 150)); // X, Y, Width, Height
```

**Ganho de Desempenho** – 40‑60 % mais rápido em documentos onde as localizações dos códigos de barras são consistentes.

### 3. Monitorar Uso de Memória

Para processos em lote de longa duração, monitore o uso do heap e sugira explicitamente a coleta de lixo se necessário:

```java
Runtime runtime = Runtime.getRuntime();
long usedMemory = runtime.totalMemory() - runtime.freeMemory();

if (usedMemory > (runtime.maxMemory() * 0.8)) {
    System.gc(); // Suggest garbage collection
}
```

## Melhores Práticas

Siga estas diretrizes para código pronto para produção:

### 1. Sempre Liberar Objetos Signature

Envolva seu código em try‑with‑resources (Java 7+) para fechar recursos automaticamente:

```java
try (Signature signature = new Signature(filePath)) {
    // Your search code here...
} // Automatically disposed
```

### 2. Validar Arquivos de Entrada

Antes de processar, verifique se o arquivo existe e é um PDF válido:

```java
File pdfFile = new File(filePath);
if (!pdfFile.exists() || !pdfFile.canRead()) {
    throw new FileNotFoundException("PDF not found or not readable: " + filePath);
}

// Optional: Verify it's actually a PDF (check magic bytes)
```

### 3. Registrar Resultados da Detecção de Código de Barras

Para depuração e auditoria, registre o que você encontrar:

```java
Logger logger = Logger.getLogger(BarcodeSearcher.class.getName());

for (BarcodeSignature barcode : signatures) {
    logger.info(String.format("Detected %s barcode '%s' on page %d at (%.2f, %.2f)",
        barcode.getEncodeType().getTypeName(),
        barcode.getText(),
        barcode.getPageNumber(),
        barcode.getLeft(),
        barcode.getTop()));
}
```

### 4. Manipular Diferentes Formatos de Código de Barras

Diferentes indústrias usam padrões diferentes. Torne seu código flexível:

```java
switch (barcode.getEncodeType().getTypeName()) {
    case "QR":
        // QR codes might contain URLs or JSON data
        processQRCode(barcode.getText());
        break;
    case "Code128":
        // Code128 typically contains alphanumeric order/tracking numbers
        processTrackingNumber(barcode.getText());
        break;
    default:
        logger.warning("Unexpected barcode type: " + barcode.getEncodeType());
}
```

### 5. Testar com Documentos do Mundo Real

Não teste apenas com PDFs de exemplo perfeitos. Use documentos reais do seu ambiente de produção:
- Faturas escaneadas com manchas de café  
- Etiquetas de envio enviadas por fax com ruído  
- Fotos de telefone móvel de baixa resolução convertidas em PDF  

Isso revela casos extremos que você não encontrará em demonstrações.

## Perguntas Frequentes

**P: Posso ler arquivos PDF com código QR sem licença?**  
R: Um teste gratuito permite ler arquivos PDF com código QR para avaliação, mas uma licença comercial é necessária para implantações em produção.

**P: A API suporta PDFs protegidos por senha?**  
R: Sim. Você pode passar a senha ao criar o objeto `Signature`: `new Signature(filePath, "password")`.

**P: Como melhorar a detecção em digitalizações de baixa resolução?**  
R: Aumente o DPI da digitalização de origem (mínimo 200 DPI) e considere filtrar por tipo de código de barras para reduzir falsos positivos.

**P: A pesquisa é thread‑safe para processamento paralelo?**  
R: Cada thread deve usar sua própria instância de `Signature`. A própria API é thread‑safe quando usada dessa forma.

**P: Qual versão do GroupDocs.Signature foi testada com este tutorial?**  
R: O código foi validado com GroupDocs.Signature 23.12.

## Conclusão

Você acabou de aprender como **ler PDFs com código QR** usando Java e a API GroupDocs.Signature. Aqui está o que cobrimos:

✅ **Configuração** – Adicionar GroupDocs.Signature ao seu projeto e opções de licenciamento  
✅ **Implementação** – Código completo para pesquisar, extrair e processar dados de códigos de barras  
✅ **Tipos de Código de Barras** – Entender quais formatos são suportados (1D e 2D)  
✅ **Casos de Uso no Mundo Real** – Processamento de faturas, gestão de inventário, autenticação de documentos, registros de saúde  
✅ **Resolução de Problemas** – Resolver problemas comuns como erros de memória e falsos positivos  
✅ **Desempenho** – Otimizar pesquisas para processamento de documentos em grande escala  

A API GroupDocs.Signature lida com a complexidade da análise de PDFs e detecção de códigos de barras, permitindo que você se concentre em construir sua lógica de negócios. Seja automatizando o processamento de faturas, verificando etiquetas de envio ou extraindo dados de inventário, agora você tem uma solução robusta.

---

**Última atualização:** 2026-03-01  
**Testado com:** GroupDocs.Signature 23.12  
**Autor:** GroupDocs