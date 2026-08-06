---
categories:
- Java PDF Processing
date: '2026-07-20'
description: Aprenda como criar assinatura de barcode em documentos PDF usando Java
  e GroupDocs.Signature. Tutorial passo a passo com exemplos de código e boas práticas.
keywords:
- create barcode signature
- how to add barcode
- generate code128 barcode
- add barcode pdf
- tamper evident barcode
lastmod: '2026-07-20'
linktitle: Criar assinatura de barcode em Java
og_description: Crie assinatura de barcode em PDF usando Java com GroupDocs.Signature.
  Aprenda passo a passo como adicionar barcode Code128, posicioná-los e proteger documentos.
og_image_alt: 'Developer guide: Create barcode signature in PDF using Java and GroupDocs'
og_title: Criar assinatura de barcode em PDF usando Java – Guia completo
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to create barcode signature in PDF documents using Java and
    GroupDocs.Signature. Step-by-step tutorial with code examples and best practices.
  headline: How to Create Barcode Signature in PDF using Java
  type: TechArticle
- description: Learn how to create barcode signature in PDF documents using Java and
    GroupDocs.Signature. Step-by-step tutorial with code examples and best practices.
  name: How to Create Barcode Signature in PDF using Java
  steps:
  - name: Initialize the Signature object
    text: '**Definition anchor:** The `Signature` class is GroupDocs.Signature''s
      entry point for loading, modifying, and saving PDF documents. First, you need
      to tell GroupDocs which PDF you''re working with: **What''s happening here:**
      The `Signature` object loads your PDF into memory and prepares it for modifi'
  - name: Configure your barcode options (How to add barcode)
    text: '**Definition anchor:** `BarcodeSignOptions` encapsulates all settings required
      to render a barcode inside a PDF. Now let''s create the barcode signature with
      your data: - `"12345678"` is your barcode data — this could be an order ID,
      certificate number, or any identifier you need. - `Code128` is the '
  - name: Position your barcode (How to sign PDF with barcode)
    text: '**Definition anchor:** `SignatureOptions` provides layout properties such
      as page number, size, and alignment. Here''s where GroupDocs really shines —
      percentage‑based positioning means your barcode looks good on any PDF size:
      **Why percentages matter:** Imagine you''re signing both A4 documents and l'
  - name: Sign and save your document (How to add barcode pdf)
    text: 'Time to actually apply the signature and save your work: **Important note:**
      The output directory must exist before you run this code. GroupDocs won''t create
      nested directories for you, so create them first or handle that in your code:
      **What if something goes wrong?** Wrap this in a try‑catch block'
  type: HowTo
- questions:
  - answer: Yes! Call `signature.sign()` multiple times with different `BarcodeSignOptions`
      for each barcode type. Just ensure they don’t overlap.
    question: Can I use different barcode types in the same PDF?
  - answer: Code128 handles most ASCII characters fine. For Unicode or complex data,
      switch to QR codes—they support UTF‑8 encoding.
    question: How do I handle barcodes that contain special characters?
  - answer: Technically up to 128 characters, but readability drops significantly
      above 30‑40 characters. For larger payloads, use QR codes.
    question: What's the maximum data I can store in a Code128 barcode?
  - answer: Not noticeably—barcodes are vector graphics, typically adding only 5‑20
      KB per barcode depending on size and complexity.
    question: Will adding barcodes significantly increase my PDF file size?
  - answer: Yes! Use `options.setRotationAngle(90)` to rotate your barcode, which
      is handy for margin placement.
    question: Can I rotate barcodes or place them vertically?
  type: FAQPage
tags:
- pdf-signing
- barcode-signature
- document-security
- groupdocs
- java
- pdf
title: Como criar assinatura de barcode em PDF usando Java
type: docs
url: /pt/java/barcode-signatures/java-pdf-signing-barcode-groupdocs/
weight: 1
---

# Como Criar Assinatura de Código de Barras em PDF usando Java

Neste tutorial, você aprenderá como **criar assinatura de código de barras** em arquivos PDF usando Java e GroupDocs.Signature. Assinaturas de código de barras incorporam identificadores legíveis por máquina que são tanto à prova de adulteração quanto fáceis de escanear — perfeitas para contratos, certificados, faturas e qualquer documento que necessite de verificação confiável.

## Respostas Rápidas
- **O que é uma assinatura de código de barras?** Um código de barras incorporado em um PDF que armazena dados estruturados e pode ser lido por scanners ou softwares.  
- **Qual tipo de código de barras é recomendado?** Code128, porque lida com dados alfanuméricos de forma compacta.  
- **Preciso de uma licença?** Um teste gratuito funciona para testes; uma licença completa é necessária para produção.  
- **Posso posicionar o código de barras em qualquer tamanho de página?** Sim — use posicionamento baseado em porcentagem para dimensionamento automático.  
- **O código de barras é baseado em vetor?** Sim, ele adiciona apenas alguns kilobytes ao PDF e permanece nítido em qualquer resolução.  

## O que é uma assinatura de código de barras?
Uma assinatura de código de barras é um código de barras baseado em vetor incorporado diretamente em uma página PDF, atuando tanto como um elemento visual quanto como uma assinatura criptográfica que pode ser validada posteriormente. Ele armazena dados estruturados, como IDs ou timestamps, e garante a integridade do documento enquanto fornece uma referência legível por máquina.

## Por que assinaturas de código de barras são importantes para seus PDFs
Assinaturas de código de barras dão aos PDFs um identificador compacto, legível por máquina, que pode ser escaneado instantaneamente, eliminando a entrada manual de dados e reduzindo erros. Como são incorporadas como gráficos vetoriais, permanecem nítidas em qualquer resolução e adicionam apenas alguns kilobytes ao arquivo. Essa combinação de legibilidade, resistência à adulteração e tamanho mínimo as torna ideais para contratos, faturas, certificados e qualquer documento que exija verificação confiável.

Aqui está um desafio que você provavelmente já enfrentou: precisar adicionar identificadores únicos a PDFs que sejam tanto legíveis por máquina quanto à prova de adulteração. Talvez você esteja trabalhando em um sistema de gerenciamento de documentos, processando certificados ou lidando com contratos que precisam de verificação no futuro.

É aí que as assinaturas de código de barras são úteis. Ao contrário de carimbos de texto simples, códigos de barras permitem incorporar dados estruturados que scanners (e seu software) podem ler instantaneamente. Além disso, quando você os combina com assinatura de PDF através do GroupDocs.Signature para Java, obtém uma forma poderosa de rastrear e verificar documentos sem adicionar consultas complexas ao banco de dados.

Neste guia, você aprenderá exatamente como implementar assinaturas de código de barras em seus PDFs Java — desde a configuração básica até código pronto para produção com posicionamento flexível. Seja construindo um sistema de faturas, gerador de certificados ou plataforma de gerenciamento de contratos, você terá tudo o que precisa ao final.

**O que você dominará:**
- Configurar o GroupDocs.Signature para Java em minutos  
- Criar assinaturas de código de barras Code128 (e por que elas costumam ser a melhor escolha)  
- Posicionar códigos de barras usando layouts baseados em porcentagem que funcionam em qualquer tamanho de PDF  
- Evitar armadilhas comuns que atrapalham desenvolvedores  
- Testar sua implementação corretamente  

## Como criar assinatura de código de barras em Java
Criar uma assinatura de código de barras em Java envolve carregar o PDF alvo, configurar as opções do código de barras como dados, tipo, tamanho e posição, e então aplicar a assinatura para gerar um novo documento. O GroupDocs.Signature cuida da renderização e do vínculo criptográfico, portanto você só precisa fornecer os parâmetros desejados e gerenciar os caminhos de arquivos.

## Pré-requisitos e lista de verificação do ambiente
Antes de começar, verifique se você tem os seguintes itens prontos:

- **Java Development Kit (JDK) 8 ou mais recente** – necessário para todas as bibliotecas Java do GroupDocs.  
- **Maven ou Gradle** – para gerenciar a dependência do GroupDocs.Signature.  
- **Uma IDE** como IntelliJ IDEA, Eclipse ou VS Code com extensões Java.  
- **GroupDocs.Signature para Java** (versão 23.12 ou mais recente é recomendada).  
- **Conhecimento básico de Java** – você deve estar confortável criando classes, lidando com exceções e trabalhando com I/O de arquivos.  

## Configurando o GroupDocs.Signature no seu projeto
Obter a biblioteca para o seu projeto é simples. Escolha sua ferramenta de build:

**Para usuários Maven**, adicione esta dependência ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Usando Gradle?** Adicione esta linha ao seu `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Prefere configuração manual?** Baixe o JAR diretamente de [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) e adicione-o ao seu classpath.

### Obtendo sua licença
Antes de ir para produção completa, você precisará lidar com a licença:

- **Teste gratuito:** Perfeito para testes — obtenha no site da GroupDocs para explorar os recursos principais.  
- **Licença temporária:** Precisa de mais tempo para avaliar? Solicite uma licença temporária de 30 dias.  
- **Licença completa:** Pronto para produção? Compre uma licença para uso ilimitado.  

Aqui está uma verificação rápida para garantir que tudo está funcionando:

```java
Signature signature = new Signature("sample.pdf");
System.out.println("Signature object created successfully.");
```

Se isso executar sem erros, está tudo pronto!

## Como criar assinatura de código de barras em Java
Agora vem a parte divertida — vamos assinar um PDF com um código de barras. Vamos dividir isso em etapas pequenas para que você entenda exatamente o que acontece em cada fase.

### Etapa 1: Inicializar o objeto Signature
**Âncora de definição:** A classe `Signature` é o ponto de entrada do GroupDocs.Signature para carregar, modificar e salvar documentos PDF.

Primeiro, você precisa informar ao GroupDocs qual PDF você está usando:

```java
Signature signature = new Signature("input.pdf");
```

**O que está acontecendo aqui:** O objeto `Signature` carrega seu PDF na memória e o prepara para modificações. Certifique-se de que o caminho do arquivo está correto — um erro comum é usar barras invertidas no Windows sem escapá‑las (use `\\` ou apenas barras normais, que funcionam em todas as plataformas).

### Etapa 2: Configurar suas opções de código de barras (Como adicionar código de barras)
**Âncora de definição:** `BarcodeSignOptions` encapsula todas as configurações necessárias para renderizar um código de barras dentro de um PDF.

Agora vamos criar a assinatura de código de barras com seus dados:

```java
BarcodeSignOptions options = new BarcodeSignOptions("12345678");
options.setEncodeType(BarcodeEncodeType.Code128);
```

- `"12345678"` é o dado do seu código de barras — isso pode ser um ID de pedido, número de certificado ou qualquer identificador que você precisar.  
- `Code128` é o tipo de codificação (mais sobre como escolher o tipo correto abaixo).  

**Dica profissional:** Code128 pode lidar com números e letras, tornando‑o versátil para a maioria dos casos de uso. Se você precisar apenas de números, `Code39` pode ser mais simples, mas Code128 oferece mais flexibilidade.

### Etapa 3: Posicionar seu código de barras (Como assinar PDF com código de barras)
**Âncora de definição:** `SignatureOptions` fornece propriedades de layout como número da página, tamanho e alinhamento.

Aqui é onde o GroupDocs realmente se destaca — o posicionamento baseado em porcentagem faz com que seu código de barras fique bem em qualquer tamanho de PDF:

```java
options.setLeft(10);   // 10% from the left edge
options.setTop(90);    // 90% from the bottom edge (near the footer)
options.setWidth(30);  // 30% of page width
options.setHeight(10); // 10% of page height
options.setPageNumber(1);
```

**Por que as porcentagens importam:** Imagine que você está assinando documentos A4 e formulários tamanho legal. Com posicionamento em porcentagem, seu código de barras escala automaticamente para parecer consistente em ambos. Usar valores fixos em pixels faria seu código de barras ficar muito pequeno em documentos grandes ou muito grande em documentos pequenos.

**Exemplo do mundo real:** Em uma página A4 (595 × 842 pontos), um código de barras com largura de 30% terá aproximadamente 180 pontos de largura. Em uma página tamanho legal (612 × 1008 pontos), terá aproximadamente 184 pontos de largura — automaticamente proporcional.

### Etapa 4: Assinar e salvar seu documento (Como adicionar código de barras ao PDF)
Hora de realmente aplicar a assinatura e salvar seu trabalho:

```java
signature.sign(outputPath, options);
```

**Nota importante:** O diretório de saída deve existir antes de executar este código. O GroupDocs não criará diretórios aninhados para você, então crie‑os primeiro ou trate isso no seu código:

```java
new File("output").mkdirs();
```

**E se algo der errado?** Envolva isso em um bloco try‑catch:

```java
try {
    signature.sign("signed.pdf", options);
} catch (Exception e) {
    e.printStackTrace();
}
```

## Escolhendo o tipo de código de barras correto para suas necessidades (gerar código de barras code128)
O GroupDocs suporta múltiplos formatos de código de barras, e escolher o correto é importante. Aqui está uma comparação prática:

**Code128 (Nossa Escolha Padrão):**
- **Melhor para:** Dados alfanuméricos mistos (IDs como "INV2024-001")  
- **Capacidade:** Até 128 caracteres ASCII  
- **Por que se destaca:** Compacto, amplamente suportado, lida com letras e números  
- **Use quando:** Você precisa de flexibilidade e não sabe que tipo de dado irá codificar  

**Code39:**
- **Melhor para:** Códigos alfanuméricos simples  
- **Capacidade:** 43 caracteres (A‑Z, 0‑9 e alguns símbolos)  
- **Por que considerá‑lo:** Scanners mais antigos frequentemente o suportam melhor  
- **Use quando:** Trabalhando com sistemas legados ou quando a simplicidade importa mais que a densidade de dados  

**QR Code:**
- **Melhor para:** Grandes quantidades de dados (URLs, payloads JSON)  
- **Capacidade:** Até 3 KB de dados  
- **Por que é poderoso:** Pode armazenar estruturas de dados complexas, correção de erro incorporada  
- **Use quando:** Você precisa incorporar dados estruturados ou URLs  

**EAN/UPC:**
- **Melhor para:** Identificação de produtos  
- **Capacidade:** Códigos numéricos de comprimento fixo (8‑13 dígitos)  
- **Use quando:** Você está trabalhando com sistemas de varejo ou inventário  

**Guia rápido de decisão:**  
- Precisa de letras e números? → Code128  
- Apenas números, manter simples? → Code39  
- Muitos dados ou URLs? → QR Code  
- Códigos de varejo/produto? → EAN/UPC  

## Armadilhas comuns e como evitá‑las (código de barras à prova de adulteração)
Aqui estão os problemas que os desenvolvedores mais encontram (para que você não precise):

### Problema 1: Posicionamento do código de barras está errado
**Sintoma:** Seu código de barras aparece em locais inesperados ou é cortado.  
**Causas comuns:**  
- Usar valores em pixels em diferentes tamanhos de página  
- Esquecer que as coordenadas PDF começam do canto inferior esquerdo, não do superior esquerdo  
- Margens empurrando o conteúdo para fora da área visível  

**Solução:** Sempre use posicionamento baseado em porcentagem para consistência:

```java
options.setLeft(5);
options.setTop(95);
options.setWidth(40);
options.setHeight(12);
```

### Problema 2: Texto do código de barras ilegível
**Sintoma:** O texto codificado é exibido, mas os scanners não conseguem lê‑lo.  
**Causas:**  
- Código de barras muito pequeno para a quantidade de dados  
- Tipo de codificação errado para seus dados  
- Baixo contraste entre as barras e o fundo  

**Solução:** Ajuste o tamanho do seu código de barras ao comprimento dos dados. Para Code128 com 10‑15 caracteres, mire em pelo menos 8‑10% da largura da página.

### Problema 3: Exceções de caminho de arquivo
**Sintoma:** `FileNotFoundException` ou erros semelhantes.  
**Causas:**  
- Caminhos Windows codificados com barras invertidas simples  
- Diretório de saída não existe  
- Problemas de permissões de arquivo  

**Solução:** Use barras normais (funcionam em todos os lugares) e crie os diretórios primeiro:

```java
Path output = Paths.get("output/signed.pdf");
Files.createDirectories(output.getParent());
```

### Problema 4: Problemas de memória com PDFs grandes
**Sintoma:** Erros de falta de memória ao processar documentos grandes.  
**Solução:** Feche o objeto `Signature` quando terminar para liberar recursos:

```java
signature.close();
```

## Testando sua implementação de código de barras
Antes de implantar, certifique‑se de que seus códigos de barras realmente funcionam. Aqui está uma lista prática de verificação:

### 1. Teste de inspeção visual
Abra seu PDF assinado e verifique:
- O código de barras está visível e corretamente posicionado?  
- Ele parece nítido (não borrado ou pixelado)?  
- Há espaço branco adequado ao redor dele?

### 2. Teste de escaneamento
Use um aplicativo de scanner de código de barras no seu telefone (como “Barcode Scanner” ou “QR & Barcode Reader”) para verificar:
- O scanner pode ler seu código de barras  
- Os dados decodificados correspondem ao que você codificou  
- Funciona a partir de diferentes ângulos e distâncias

### 3. Teste multiplataforma
Abra seu PDF em diferentes dispositivos:
- Windows (Adobe Reader, Chrome)  
- Mac (Preview, Chrome)  
- Dispositivos móveis (iOS, Android)  

Certifique‑se de que o código de barras seja renderizado corretamente em todos os lugares.

### 4. Código de teste automatizado
Aqui está um teste simples que você pode executar:

```java
Signature testSignature = new Signature("signed.pdf");
List<BarcodeSignature> signatures = testSignature.search(BarcodeSignature.class);
if (signatures.size() > 0) {
    System.out.println("Barcode found: " + signatures.get(0).getText());
}
```

## Casos de uso reais para assinaturas de código de barras
Vamos ver onde essa técnica realmente se destaca em sistemas de produção:

### 1. Geração e verificação de certificados
**Cenário:** Você está construindo uma plataforma de treinamento que emite certificados de conclusão.  
**Implementação:** Gere um ID de certificado único (por exemplo, “CERT‑2024‑00123”) e incorpore‑o como um código de barras Code128 no canto inferior direito. Escanear o código de barras permite que sua API recupere os detalhes do certificado instantaneamente, eliminando a entrada manual de dados.

### 2. Sistemas de rastreamento de faturas
**Cenário:** Sua empresa processa milhares de faturas mensalmente.  
**Implementação:** Adicione o número da fatura e a data de vencimento como um QR code posicionado onde o equipamento de escaneamento possa lê‑lo facilmente. Sistemas de classificação automatizados podem encaminhar faturas sem intervenção humana, reduzindo o tempo de processamento de horas para minutos.

### 3. Gerenciamento de contratos legais
**Cenário:** Um escritório de advocacia precisa rastrear versões e emendas de contratos.  
**Implementação:** Cada versão de contrato recebe um identificador de código de barras único que inclui ID do contrato, número da versão e data da assinatura. Escanear durante auditorias recupera automaticamente o histórico completo de versões.

### 4. Segurança de registros médicos
**Cenário:** Um hospital deseja impedir o acesso não autorizado a registros.  
**Implementação:** Incorpore o ID do paciente e o timestamp de criação do registro em um código de barras. Apenas dispositivos autenticados podem decodificar e acessar o registro completo, e cada escaneamento cria um log de auditoria para conformidade.

## Dicas de otimização de desempenho (segurança de documentos Java)
Quando você está assinando muitos PDFs, o desempenho importa. Aqui estão algumas dicas para manter tudo funcionando suavemente:

### Estratégia de processamento em lote
Ao invés de assinar um documento por vez, processe em lote:

```java
for (String filePath : pdfList) {
    Signature batchSignature = new Signature(filePath);
    batchSignature.sign(outputPath, options);
    batchSignature.close();
}
```

**Por que isso ajuda:** Reutilizar o objeto de opções e fechar recursos adequadamente previne vazamentos de memória.

### Gerenciamento de memória para PDFs grandes
Para PDFs maiores que 50 MB:
- Processá‑los sequencialmente ao invés de carregar vários ao mesmo tempo.  
- Use try‑with‑resources para garantir a limpeza.  
- Monitore o tamanho do heap e ajuste os parâmetros da JVM se necessário: `-Xmx2g`.

### Cache de códigos de barras usados com frequência
Se você assina muitos documentos com o mesmo código de barras, faça cache da instância `BarcodeSignOptions`:

```java
BarcodeSignOptions cachedOptions = new BarcodeSignOptions("STATIC_ID");
cachedOptions.setEncodeType(BarcodeEncodeType.Code128);
```

## Quando usar assinaturas de código de barras (e quando não usar)
**Cenários perfeitos:**
- Você precisa de identificadores de documento legíveis por máquina.  
- Documentos serão escaneados ou processados automaticamente.  
- Você quer rastreamento à prova de adulteração sem certificados digitais.  
- Integração com infraestrutura de código de barras existente é necessária.  

**Não ideal quando:**
- Você precisa de assinaturas digitais juridicamente vinculativas (use certificados digitais em vez disso).  
- Documentos serão visualizados apenas por humanos (uma marca d'água de texto simples pode ser suficiente).  
- Você está trabalhando com documentos extremamente pequenos onde um código de barras dominaria a página.  
- Requisitos de segurança exigem criptografia — códigos de barras são visíveis e escaneáveis por qualquer pessoa.  

**Você pode combinar abordagens?** Absolutamente! Muitos sistemas usam tanto assinaturas de código de barras para rastreamento quanto assinaturas digitais para validade legal.

## Perguntas Frequentes
**Q: Posso usar diferentes tipos de código de barras no mesmo PDF?**  
A: Sim! Chame `signature.sign()` várias vezes com diferentes `BarcodeSignOptions` para cada tipo de código de barras. Apenas certifique‑se de que eles não se sobreponham.

**Q: Como lidar com códigos de barras que contêm caracteres especiais?**  
A: Code128 lida bem com a maioria dos caracteres ASCII. Para Unicode ou dados complexos, troque para QR codes — eles suportam codificação UTF‑8.

**Q: Qual é o máximo de dados que posso armazenar em um código de barras Code128?**  
A: Tecnicamente até 128 caracteres, mas a legibilidade diminui significativamente acima de 30‑40 caracteres. Para cargas maiores, use QR codes.

**Q: A adição de códigos de barras aumentará significativamente o tamanho do meu arquivo PDF?**  
A: Não perceptivelmente — códigos de barras são gráficos vetoriais, tipicamente adicionando apenas 5‑20 KB por código de barras, dependendo do tamanho e complexidade.

**Q: Posso girar códigos de barras ou colocá‑los verticalmente?**  
A: Sim! Use `options.setRotationAngle(90)` para girar seu código de barras, o que é útil para posicionamento nas margens.

**Q: Como faço para que códigos de barras apareçam em todas as páginas de um PDF multipágina?**  
A: Itere pelas páginas e aplique a assinatura em cada uma. Consulte a classe `PagesSetup` na documentação do GroupDocs para controlar quais páginas são assinadas.

**Q: E se meu scanner de código de barras não conseguir ler o código gerado?**  
A: Primeiro, verifique se o scanner suporta o tipo de código de barras escolhido. Em seguida, aumente o tamanho do código de barras — a maioria dos problemas de escaneamento decorre de barras muito pequenas. Mire em pelo menos 1 polegada (2,54 cm) de largura para leituras confiáveis.

## Recursos Adicionais
**Documentação:**  
- [GroupDocs.Signature for Java Docs](https://docs.groupdocs.com/signature/java/)  
- [API Reference Guide](https://reference.groupdocs.com/signature/java/)  

**Downloads e Licenciamento:**  
- [Download Latest Version](https://releases.groupdocs.com/signature/java/)  
- [Free Trial Access](https://releases.groupdocs.com/signature/java/)  
- [Get Temporary License](https://purchase.groupdocs.com/temporary-license/)  
- [Purchase Full License](https://purchase.groupdocs.com/buy)  

**Comunidade e Suporte:**  
- [Support Forum](https://forum.groupdocs.com/c/signature/) - Comunidade ativa com engenheiros da GroupDocs  

---

**Última atualização:** 2026-07-20  
**Testado com:** GroupDocs.Signature 23.12 (Java)  
**Autor:** GroupDocs

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

```java
import com.groupdocs.signature.Signature;

public class QuickTest {
    public static void main(String[] args) {
        try {
            Signature signature = new Signature("test-document.pdf");
            System.out.println("GroupDocs.Signature is ready to go!");
        } catch (Exception e) {
            System.err.println("Setup issue: " + e.getMessage());
        }
    }
}
```

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
Signature signature = new Signature(filePath);
```

```java
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

BarcodeSignOptions options = new BarcodeSignOptions("12345678");
options.setEncodeType(BarcodeTypes.Code128);
```

```java
import com.groupdocs.signature.domain.enums.MeasureType;
import com.groupdocs.signature.domain.Padding;

// Use percentages instead of fixed pixels
options.setLocationMeasureType(MeasureType.Percents);
options.setLeft(5);  // 5% from the left edge
options.setTop(5);   // 5% from the top

// Size it proportionally too
options.setSizeMeasureType(MeasureType.Percents);
options.setWidth(10);  // 10% of page width
options.setHeight(5);  // 5% of page height

// Add some breathing room with margins
Padding margins = new Padding();
margins.setLeft(1);
margins.setTop(1);
margins.setRight(1);
options.setMargin(margins);
```

```java
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithPercents/sample_signed.pdf";
signature.sign(outputFilePath, options);
```

```java
Path outputPath = Paths.get(outputFilePath);
Files.createDirectories(outputPath.getParent());
signature.sign(outputFilePath, options);
```

```java
try {
    signature.sign(outputFilePath, options);
    System.out.println("PDF signed successfully at: " + outputFilePath);
} catch (Exception e) {
    System.err.println("Signing failed: " + e.getMessage());
    e.printStackTrace();
}
```

```java
options.setLocationMeasureType(MeasureType.Percents);
options.setLeft(5);  // 5% from left works on any page width
```

```java
options.setWidth(10);  // Give it room to breathe
options.setHeight(5);  // Maintain proper aspect ratio
```

```java
String filePath = "documents/sample.pdf";  // Works on Windows, Mac, Linux
Files.createDirectories(Paths.get("output/signed"));
```

```java
try (Signature signature = new Signature(filePath)) {
    signature.sign(outputFilePath, options);
} // Automatically closes and releases memory
```

```java
import org.junit.Test;
import static org.junit.Assert.*;

public class BarcodeSignatureTest {
    
    @Test
    public void testBarcodeSigning() {
        String testPdf = "test-data/sample.pdf";
        String output = "test-output/signed.pdf";
        
        try (Signature signature = new Signature(testPdf)) {
            BarcodeSignOptions options = new BarcodeSignOptions("TEST123");
            options.setEncodeType(BarcodeTypes.Code128);
            
            signature.sign(output, options);
            
            // Verify output file exists
            assertTrue(new File(output).exists());
            
            // Verify file size increased (signature was added)
            long originalSize = new File(testPdf).length();
            long signedSize = new File(output).length();
            assertTrue(signedSize > originalSize);
            
        } catch (Exception e) {
            fail("Signing should not throw exception: " + e.getMessage());
        }
    }
}
```

```java
List<String> pdfFiles = Arrays.asList("doc1.pdf", "doc2.pdf", "doc3.pdf");

for (String pdfFile : pdfFiles) {
    try (Signature signature = new Signature(pdfFile)) {
        BarcodeSignOptions options = createBarcodeOptions(); // Reuse options
        signature.sign(getOutputPath(pdfFile), options);
    }
}
```

```java
// Create options once, reuse many times
BarcodeSignOptions templateOptions = createStandardBarcodeOptions();

// For each document, clone and customize
BarcodeSignOptions documentOptions = templateOptions.clone();
documentOptions.setText(uniqueDocumentId);
```

## Tutoriais Relacionados

- [Tutorial de Assinatura de Código de Barras Java - Adicionar, Verificar e Gerenciar Códigos de Barras em PDFs](/signature/java/barcode-signatures/)
- [Criar Assinatura de Código de Barras em Java – Atualizar Códigos de Barras PDF](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [Como ler QR code de PDF usando Java e GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)