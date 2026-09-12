---
categories:
- Java Development
- Document Management
date: '2026-08-25'
description: Aprenda como adicionar Barcode a documentos PDF em Java usando GroupDocs.Signature.
  Este guia step‑by‑step mostra como adicionar códigos de barras GS1DotCode, extrair
  imagens e evitar armadilhas comuns.
keywords:
- how to add barcode
- groupdocs signature java
- pdf document barcode
lastmod: '2026-08-25'
linktitle: Adicionar Barcode a PDF Java
og_description: Aprenda como adicionar Barcode a PDF em Java com GroupDocs.Signature.
  Tutorial step‑by‑step, code examples e troubleshooting tips para códigos de barras
  GS1DotCode.
og_image_alt: Guide showing Java code to embed GS1DotCode barcode into a PDF using
  GroupDocs.Signature
og_title: Como adicionar Barcode a PDF em Java – Guia Completo
schemas:
- author: GroupDocs
  dateModified: '2026-08-25'
  description: Learn how to add barcode to PDF documents in Java using GroupDocs.Signature.
    This step‑by‑step guide shows how to add GS1DotCode barcodes, extract images,
    and avoid common pitfalls.
  headline: How to Add Barcode to PDF in Java
  type: TechArticle
- description: Learn how to add barcode to PDF documents in Java using GroupDocs.Signature.
    This step‑by‑step guide shows how to add GS1DotCode barcodes, extract images,
    and avoid common pitfalls.
  name: How to Add Barcode to PDF in Java
  steps:
  - name: Validate GS1 payloads before encoding.
    text: Validate GS1 payloads before encoding.
  - name: Choose barcode dimensions that balance scan reliability with layout constraints.
    text: Choose barcode dimensions that balance scan reliability with layout constraints.
  - name: Combine barcode signatures with cryptographic signatures for full security
      coverage.
    text: Combine barcode signatures with cryptographic signatures for full security
      coverage.
  type: HowTo
- questions:
  - answer: GS1DotCode is a compact 2‑D dot matrix that stores up to **3,116 characters**
      in a smaller footprint than QR codes, making it ideal for tiny labels and high‑speed
      printing.
    question: What is GS1DotCode and why is it different from QR codes?
  - answer: The free trial is limited to evaluation and adds a watermark to output
      files. Production use requires a purchased or temporary 30‑day license.
    question: Can I use a free trial for production deployments?
  - answer: Set `setPageNumber(pageIndex)` on the `BarcodeSignOptions` object, then
      adjust `setLeft()` and `setTop()` to place it precisely.
    question: How do I position the barcode on a specific page?
  - answer: 'Yes. Provide the password when constructing the `Signature` object: `new
      Signature("file.pdf", "password")`.'
    question: Does GroupDocs.Signature support password‑protected PDFs?
  - answer: Aim for at least **108 pt × 108 pt** (1.5 in × 1.5 in). Larger sizes improve
      readability, especially on low‑resolution printers.
    question: What is the minimum barcode size for reliable scanning?
  type: FAQPage
tags:
- java
- pdf-signing
- barcodes
- groupdocs
- document-security
title: Como adicionar Barcode a PDF em Java
type: docs
url: /pt/java/digital-signatures/master-java-document-signing-groupdocs-signature/
weight: 1
---

# Como adicionar código de barras a PDF em Java

## Introdução

Já se pegou lutando com a autenticidade de documentos em sua aplicação Java? Você não está sozinho. Seja construindo um sistema de inventário, gerenciando contratos ou lidando com documentos da cadeia de suprimentos, há uma boa chance de que você precise de uma maneira confiável de assinar e verificar PDFs automaticamente.

Assinaturas digitais tradicionais são ótimas, mas às vezes você precisa de algo mais especializado — como assinaturas de código de barras que funcionam perfeitamente com sistemas de leitura e fluxos de trabalho automatizados. É aí que os códigos de barras GS1DotCode são úteis.

**O que você aprenderá:**
- Como assinar documentos PDF com códigos de barras GS1DotCode em Java
- Como extrair e salvar imagens de assinatura de código de barras
- Quando (e por que) usar assinaturas de código de barras em vez de métodos tradicionais
- Armadilhas comuns e como evitá‑las

Ao final deste guia, você terá uma solução pronta‑para‑uso que pode integrar a qualquer projeto Java.

## Respostas rápidas
- **Qual biblioteca adiciona códigos de barras a PDFs em Java?** GroupDocs.Signature for Java.  
- **Qual formato de código de barras é coberto?** GS1DotCode, uma matriz de pontos 2‑D compacta.  
- **Preciso de uma licença paga?** Um teste gratuito funciona para testes; produção requer licença comercial.  
- **Posso extrair o código de barras como imagem?** Sim, usando a API `BarcodeSignature`.  
- **Qual versão do Java é necessária?** JDK 8 ou superior.

## O que é adicionar código de barras?
*How to add barcode* refere‑se ao processo de inserir programaticamente um gráfico de código de barras legível por máquina em um arquivo PDF, de modo que o código de barras se torne parte do fluxo de conteúdo do documento. Isso envolve gerar a imagem do código de barras, posicioná‑la em uma página e salvar o PDF modificado, garantindo que o código de barras permaneça pesquisável e imprimível.

## Por que escolher códigos de barras GS1DotCode?
GS1DotCode foi projetado para situações onde o espaço é limitado. Ao contrário dos códigos de barras lineares que se estendem horizontalmente, o DotCode cria uma matriz 2‑D de pontos que compacta uma grande quantidade de informação em uma área pequena. Isso o torna perfeito para:

- **Rótulos de produtos pequenos** onde cada milímetro conta  
- **Impressão em alta velocidade** em linhas de produção (o formato foi projetado para isso)  
- **Rastreamento da cadeia de suprimentos** onde você precisa codificar estruturas de dados complexas  

O formato pode lidar com até **3.116 caracteres** em um espaço compacto e lê‑se de forma confiável mesmo em altas velocidades ou com danos parciais. Se você trabalha no varejo ou na logística, seus parceiros provavelmente já usam padrões GS1 — então você está falando a mesma linguagem.

> **Dica de especialista:** Use GS1DotCode quando precisar incorporar mais de 20 caracteres em um rótulo menor que 1 polegada × 1 polegada.

## Pré‑requisitos

Antes de começar a programar, verifique se seu ambiente atende aos requisitos a seguir.

### Bibliotecas e dependências necessárias
- **GroupDocs.Signature for Java** 23.12 ou posterior (suporta **30+** formatos de documento)  
- Maven ou Gradle para gerenciamento de dependências

### Configuração do ambiente
- **JDK 8** ou mais recente instalado e configurado no seu `PATH`  
- Uma IDE como IntelliJ IDEA, Eclipse ou NetBeans  
- Um arquivo PDF de exemplo para experimentar (qualquer PDF não protegido serve)

### Pré‑requisitos de conhecimento
- Sintaxe básica de Java (variáveis, métodos, objetos)  
- Familiaridade com declaração de dependências em Maven ou Gradle  
- Entendimento de I/O de arquivos em Java (por exemplo, `FileInputStream`)

Se algum desses itens estiver faltando, pause e instale‑os agora; as etapas posteriores assumem que eles estão presentes.

## Configurando GroupDocs.Signature para Java

### Maven
Se você usa Maven, adicione a dependência a seguir ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

O Maven baixará a biblioteca e todas as dependências transitivas necessárias automaticamente.

### Gradle
Para usuários de Gradle, insira esta linha no seu arquivo `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

O Gradle resolve o pacote da mesma forma prática.

### Download direto
Se preferir gerenciamento manual, baixe os arquivos JAR na página oficial de lançamentos: [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/). Coloque os JARs no classpath do seu projeto.

**Dica de especialista:** Maven ou Gradle simplificam futuras atualizações — basta aumentar o número da versão.

### Aquisição de licença
GroupDocs oferece três opções de licenciamento:

- **Teste gratuito** – sem cartão de crédito, marcas d'água aplicadas à saída  
- **Licença temporária** – avaliação completa por 30 dias  
- **Licença comercial** – remove limites de teste e concede direitos de produção  

Após obter o arquivo de licença, coloque‑o na pasta de recursos do seu projeto e carregue‑o antes de criar qualquer objeto `Signature`.

`License.setLicense` carrega o arquivo de licença do GroupDocs, habilitando operação completa sem restrições de teste.

Execute o trecho a seguir para verificar se a biblioteca foi carregada corretamente:

```java
import com.groupdocs.signature.Signature;

public class InitializeGroupDocs {
    public static void main(String[] args) {
        // Create an instance of Signature
        Signature signature = new Signature("path/to/your/document.pdf");
        
        System.out.println("Initialization successful!");
    }
}
```

Se aparecer “Initialization successful!” a configuração está concluída. Caso contrário, verifique o classpath e o caminho da licença.

## Guia de implementação

Cobriremos duas funcionalidades principais: (1) assinar um PDF com um código de barras GS1DotCode e (2) extrair esse código de barras como um arquivo de imagem.

### Recurso 1: assinar documento com código de barras GS1DotCode

#### Como assinar um PDF com um código de barras GS1DotCode em Java?

Carregue o PDF alvo com `new Signature("source.pdf")`, configure um objeto `BarcodeSignOptions` contendo dados formatados em GS1 e chame `sign()` para produzir um novo PDF que incorpora o código de barras. Essa operação grava o código de barras diretamente no fluxo de conteúdo do PDF, preservando‑o em impressão e re‑digitalização.

O processo envolve três etapas concisas: criar uma instância `Signature`, configurar `BarcodeSignOptions` e invocar `sign()`. O código abaixo demonstra cada passo.

##### 1. inicializar o objeto de assinatura
A classe `Signature` é o ponto de entrada para todas as operações de processamento de documentos no GroupDocs.Signature.

```java
import com.groupdocs.signature.Signature;

String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY/document.pdf";
final Signature signature = new Signature(sourceFilePath);
```

> **Por que isso importa:** O objeto `Signature` abstrai o manuseio de arquivos, transmitindo PDFs grandes de forma eficiente sem carregar todo o arquivo na memória.

##### 2. configurar opções de código de barras
`BarcodeSignOptions` permite especificar o tipo de código de barras, os dados codificados, a posição e as dimensões.

```java
import com.groupdocs.signature.domain.signatures.BarcodeSignature;
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

BarcodeSignOptions gs1DotCodeOptions = new BarcodeSignOptions("(01)04912345123459(15)970331(30)128(10)ABC123", BarcodeTypes.GS1DotCode);
gs1DotCodeOptions.setLeft(100); // Set barcode position
gs1DotCodeOptions.setTop(100);
gs1DotCodeOptions.setHeight(150);
gs1DotCodeOptions.setWidth(200);
```

> **Pontos chave:**  
> - A string codificada segue os Identificadores de Aplicação (AIs) do GS1, como `(01)` para GTIN, `(15)` para data de validade, etc.  
> - `setLeft()` e `setTop()` usam pontos (72 pts = 1 in).  
> - O tamanho mínimo recomendado para escaneamento confiável é **108 pt × 108 pt** (1,5 in × 1,5 in).

##### 3. assinar o documento
Adicione as opções configuradas a uma lista (você pode combinar vários tipos de assinatura) e chame `sign()`.

```java
import java.util.ArrayList;
import java.util.List;

List<com.groupdocs.signature.options.sign.SignOptions> listOptions = new ArrayList<>();
listOptions.add(gs1DotCodeOptions);
signature.sign("YOUR_OUTPUT_DIRECTORY/signed_document_with_gs1dotcode.pdf", listOptions);
```

> **Observação de desempenho:** Reutilizar uma única instância `Signature` para operações em lote reduz a sobrecarga de criação de objetos e melhora a taxa de processamento.

### Recurso 2: salvar o conteúdo da assinatura de código de barras em arquivo

#### Como extrair uma imagem de código de barras de um PDF assinado em Java?

`BarcodeSignature` representa um objeto de assinatura de código de barras extraído de um documento assinado, fornecendo acesso aos seus dados e ao conteúdo da imagem.

Crie uma instância `BarcodeSignature` (ou recupere‑a via `search()`), leia seus dados de imagem codificados em Base64 através de `getContent()`, decodifique‑os e grave os bytes em um arquivo PNG. Isso gera uma imagem independente que pode ser exibida em uma UI ou enviada a uma impressora de rótulos.

##### 1. simular a criação da assinatura de código de barras
Em cenários reais você obteria o `BarcodeSignature` a partir de um resultado de busca; aqui o instanciamos manualmente para ilustração.

```java
import com.groupdocs.signature.domain.signatures.BarcodeSignature;
import java.io.FileOutputStream;

String base64String = "SampleBase64EncodedData";
BarcodeSignature barcodeSignature = new BarcodeSignature(base64String);
```

##### 2. salvar o conteúdo em um arquivo
Decodifique a string Base64 e grave os bytes resultantes no disco usando um bloco try‑with‑resources.

```java
int imageNumber = 1;
String formatExtension = ".png";  // Assume PNG format

try (FileOutputStream outputStream = new FileOutputStream("YOUR_OUTPUT_DIRECTORY/barcode_image" + imageNumber + formatExtension)) {
    byte[] byteArray = barcodeSignature.getContent();
    if (byteArray != null) {
        outputStream.write(byteArray);
    }
}
```

> **Atenção:** `getContent()` pode retornar `null` se a assinatura foi criada sem incorporar uma imagem. Sempre verifique se o valor é `null` antes de gravar.

## Problemas comuns e soluções

### Problema: o código de barras não escaneia
**Sintomas:** O código de barras parece correto no visualizador de PDF, mas os scanners retornam erros.

**Soluções:**
- Aumente o tamanho do código de barras para pelo menos **108 pt × 108 pt**.  
- Garanta que a resolução da impressora seja **≥ 300 dpi**.  
- Verifique se a string de dados GS1 segue a sintaxe correta de AI; um parêntese ausente quebra o scanner.

### Problema: OutOfMemoryError em PDFs grandes
**Sintomas:** Processar documentos maiores que **50 MB** provoca falhas de heap.

**Soluções:**
- Inicie a JVM com heap maior, por exemplo, `-Xmx2g`.  
- Processar documentos em lotes menores.  
- Dispor explicitamente dos objetos `Signature`: `signature.dispose()` após cada arquivo.

### Problema: o código de barras aparece borrado
**Sintomas:** O código de barras renderizado parece pixelado no PDF de saída.

**Soluções:**
- Use dimensões maiores; a biblioteca renderiza gráficos vetoriais quando possível, mas redimensionar após a geração introduz artefatos.  
- Evite conversões raster‑para‑vetor; deixe o GroupDocs renderizar diretamente a partir da definição vetorial.

### Problema: exceções de licença
**Sintomas:** Erros como “License not found” ou “Trial limitations exceeded”.

**Soluções:**
- Coloque o arquivo de licença na raiz do classpath (`src/main/resources`).  
- Chame `License.setLicense("GroupDocs.Signature.lic")` **antes** de qualquer instanciação de `Signature`.  
- Para licenças temporárias, confirme a data de expiração (30 dias a partir da emissão).

## Quando usar esta abordagem

### Casos de uso recomendados
- **Rastreamento da cadeia de suprimentos** – incorporar IDs de produto, números de lote e datas de validade diretamente em documentos de envio.  
- **Impressão automática de rótulos** – gerar códigos de barras sob demanda para cada fatura PDF.  
- **Indústrias regulamentadas** – padrões GS1 são obrigatórios em muitos ambientes de varejo e saúde.

### Quando considerar alternativas
- Se precisar apenas de integridade criptográfica, uma assinatura digital PKI padrão é mais adequada.  
- Para anotações visuais simples, uma assinatura de texto ou selo de imagem pode ser suficiente.  
- Quando o tamanho do documento for crítico, evite adicionar imagens de código de barras em alta resolução; prefira QR codes, que podem ser menores para densidade de dados comparável.

## Melhores práticas de segurança

### Validação de dados
Sanitize quaisquer dados fornecidos pelo usuário antes de codificá‑los em um código de barras. Strings GS1 malformadas podem causar erros de escaneamento downstream ou, em casos extremos, provocar estouros de buffer em firmware de scanners legados.

### Controle de acesso
Implemente controle de acesso baseado em funções (RBAC) para que apenas usuários autorizados possam invocar a API de assinatura. Armazene o arquivo de licença de forma segura e restrinja permissões de sistema de arquivos.

### Registro de auditoria
Registre cada operação de assinatura com detalhes como ID do usuário, timestamp, caminho do arquivo fonte e a carga útil GS1 exata. Exemplo de trecho de registro:

```java
// Simple logging example (use a proper logging framework in production)
System.out.println("Document signed by: " + userId + " at " + new Date());
System.out.println("Barcode data: " + barcodeData);
```

### Detecção de adulteração
Combine uma assinatura de código de barras com uma assinatura digital criptográfica. O código de barras fornece dados legíveis por máquina, enquanto a assinatura digital garante integridade e não‑repúdio.

## Aplicações práticas

### 1. gerenciamento da cadeia de suprimentos
Cada nota fiscal recebe um código de barras GS1DotCode que codifica GTIN, lote e destino da remessa. Scanners em cada ponto de controle atualizam automaticamente o sistema ERP, reduzindo erros de entrada manual em **98 %**.

### 2. controle de inventário
Ao receber mercadorias, o PDF de recebimento é assinado com um código de barras que contém o número da PO e as quantidades de itens. Funcionários escaneiam o código e o banco de dados de inventário é atualizado em tempo real.

### 3. ponto de venda no varejo
Faturas impressas com código de barras permitem que caixas processem devoluções escaneando a fatura em vez de inserir manualmente o ID da transação, reduzindo o tempo médio de checkout em **30 segundos** por devolução.

### 4. documentação de saúde
Prescrições assinadas com código de barras GS1DotCode incorporam ID do paciente, código do medicamento e instruções de dosagem. Farmácias escaneiam o código, eliminando erros de transcrição que causam eventos adversos de medicamentos.

## Considerações de desempenho

### Gerenciamento de memória
GroupDocs.Signature transmite dados PDF, mas ainda assim você deve fechar recursos prontamente:

```java
try (Signature signature = new Signature(sourceFilePath)) {
    // Do your signing operations here
} // Signature automatically disposed here
```

Usar try‑with‑resources garante que o objeto `Signature` libere os manipuladores de arquivo mesmo se ocorrer uma exceção.

### Dicas de processamento em lote
- Reutilize a mesma instância `BarcodeSignOptions` quando a carga útil for idêntica em vários documentos.  
- Paralelize a assinatura com `ExecutorService` para cargas de trabalho CPU‑intensivas; um servidor típico de 8 núcleos pode assinar **≈ 150 PDFs por minuto** quando cada arquivo tem menos de 5 MB.  
- Regule chamadas externas de validação de licença para evitar limites de taxa.

### Otimização de formato de arquivo
- Prefira PDF/A‑1b para arquivamento; ele comprime fluxos e reduz o tamanho do arquivo em até **40 %**.  
- Mantenha as dimensões do código de barras no mínimo necessário; um código de 1,5 in × 1,5 in adiciona aproximadamente **15 KB** a um PDF de 2 MB.

## Conclusão

Agora você possui um fluxo de trabalho completo e pronto para produção para adicionar assinaturas de código de barras GS1DotCode a arquivos PDF em Java, extrair esses códigos como imagens e integrar o processo a pipelines maiores de gerenciamento de documentos. Lembre‑se de:

1. Validar as cargas úteis GS1 antes da codificação.  
2. Escolher dimensões de código de barras que equilibrem confiabilidade de escaneamento com restrições de layout.  
3. Combinar assinaturas de código de barras com assinaturas digitais criptográficas para cobertura total de segurança.  

Próximos passos: explore outros tipos de assinatura oferecidos pelo GroupDocs.Signature — códigos QR, carimbos de texto e certificados digitais — todos com uma API consistente.

---

## Perguntas frequentes

**Q: O que é GS1DotCode e por que ele é diferente dos códigos QR?**  
A: GS1DotCode é uma matriz de pontos 2‑D compacta que armazena até **3.116 caracteres** em um espaço menor que códigos QR, tornando‑o ideal para rótulos minúsculos e impressão em alta velocidade.

**Q: Posso usar o teste gratuito em implantações de produção?**  
A: O teste gratuito é limitado à avaliação e adiciona marca d'água aos arquivos de saída. Uso em produção requer licença comprada ou temporária de 30 dias.

**Q: Como posicionar o código de barras em uma página específica?**  
A: Defina `setPageNumber(pageIndex)` no objeto `BarcodeSignOptions`, depois ajuste `setLeft()` e `setTop()` para posicionamento preciso.

**Q: O GroupDocs.Signature suporta PDFs protegidos por senha?**  
A: Sim. Forneça a senha ao construir o objeto `Signature`: `new Signature("file.pdf", "password")`.

**Q: Como verificar se uma assinatura de código de barras foi adicionada corretamente?**  
`Signature.search()` procura assinaturas em um documento, retornando uma coleção de objetos de assinatura correspondentes. Use `Signature.search()` com `BarcodeSearchOptions`. Os objetos `BarcodeSignature` retornados contêm os dados codificados e o conteúdo da imagem para verificação.

**Q: Qual é o tamanho mínimo do código de barras para escaneamento confiável?**  
A: Recomenda‑se pelo menos **108 pt × 108 pt** (1,5 in × 1,5 in). Tamanhos maiores melhoram a legibilidade, especialmente em impressoras de baixa resolução.

**Q: Posso assinar vários PDFs simultaneamente?**  
A: Sim. Crie um pool de threads e instancie um objeto `Signature` separado por thread; a biblioteca é thread‑safe quando cada thread trabalha em seu próprio documento.

**Q: Existe um limite para quantos códigos de barras posso incorporar em um único PDF?**  
A: Não há limite rígido, mas cada código de barras adiciona cerca de **15 KB** de dados. Para PDFs maiores que **100 MB**, considere processamento em lote para gerenciar o uso de memória.

**Q: A biblioteca funciona em plataformas não Windows?**  
A: GroupDocs.Signature for Java é independente de plataforma e roda em qualquer OS com JRE compatível, incluindo Linux e macOS.

**Última atualização:** 2026-08-25  
**Testado com:** GroupDocs.Signature 23.12 for Java  
**Autor:** GroupDocs

## Tutoriais Relacionados

- [How to Verify Barcode Signatures in Java Using GroupDocs.Signature](/signature/java/barcode-signatures/verify-barcode-signatures-groupdocs-signature-java/)
- [Create Barcode Signature Java – Update PDF Barcodes](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [Add QR Code to PDF Java - Complete Guide with GroupDocs.Signature](/signature/java/qr-code-signatures/qr-code-signatures-java-groupdocs/)