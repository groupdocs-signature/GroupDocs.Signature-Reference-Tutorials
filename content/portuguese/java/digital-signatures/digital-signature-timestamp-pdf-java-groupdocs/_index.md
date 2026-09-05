---
date: '2026-09-05'
description: Aprenda a assinar PDF com Java usando GroupDocs.Signature, adicione assinatura
  digital e timestamp. Guia passo a passo com exemplos de código e boas práticas.
keywords:
- how to sign pdf
- add digital signature pdf
- digital signature pdf java
- sign pdf java
- groupdocs signature java
lastmod: '2026-09-05'
linktitle: Adicionar assinatura digital ao PDF Java
og_description: Aprenda a assinar PDF com Java usando GroupDocs.Signature, adicione
  uma assinatura digital e timestamp confiável em poucas linhas de código. Siga instruções
  passo a passo, boas práticas e dicas de solução de problemas.
og_image_alt: Guide showing Java code to add digital signature and timestamp to PDF
  with GroupDocs.Signature
og_title: Como assinar PDF com Java usando GroupDocs.Signature
schemas:
- author: GroupDocs
  dateModified: '2026-09-05'
  description: Learn how to sign PDF with Java using GroupDocs.Signature, add digital
    signature and timestamp. Step-by-step guide with code examples and best practices.
  headline: How to sign PDF with Java and timestamp
  type: TechArticle
- description: Learn how to sign PDF with Java using GroupDocs.Signature, add digital
    signature and timestamp. Step-by-step guide with code examples and best practices.
  name: How to sign PDF with Java and timestamp
  steps:
  - name: import required classes
    text: The following imports give you access to signature configuration, positioning,
      and timestamp functionality.
  - name: define your file paths
    text: Set up paths for the input PDF, the certificate (PFX), and the output location.
      Keep the certificate file secure; it contains your private key.
  - name: initialize the Signature object
    text: '`Signature` is the entry point for all signing actions. Creating it loads
      the PDF into memory and prepares the API for further operations.'
  - name: configure signature properties and timestamp
    text: '`DigitalSignature` is the cryptographic seal that will be embedded in the
      PDF. You can also attach a timestamp from a trusted authority. * **ContactInfo**
      – e.g., `john.doe@company.com` * **Location** – e.g., `New York Office` * **Reason**
      – e.g., `Contract Approval` We use FreeTSA (a free timestamp'
  - name: configure digital sign options
    text: '`SignOptions` aggregates the certificate, visual appearance, and placement
      settings for the digital signature.'
  - name: sign and save the document
    text: '`SignResult` provides the outcome of the signing operation, including success
      status and any warnings.'
  type: HowTo
- questions:
  - answer: A digital signature uses cryptographic algorithms to verify identity and
      detect tampering, while an electronic signature can be as simple as a typed
      name.
    question: What's the difference between a digital signature and an electronic
      signature?
  - answer: Only for the timestamp service; the cryptographic signing itself runs
      locally.
    question: Do I need internet connectivity to sign PDFs?
  - answer: Any modification breaks the signature, and PDF viewers will display a
      warning indicating the document has been altered.
    question: Can signed PDFs be edited later?
  - answer: Most PDF readers verify automatically; programmatically, use GroupDocs.Signature's
      verification API to check status, signer details, and timestamp validity.
    question: How do I verify a signed PDF?
  - answer: The embedded timestamp proves the signature was created while the certificate
      was still valid, preserving legal standing.
    question: What happens if my certificate expires after I've signed documents?
  type: FAQPage
tags:
- pdf signing
- digital signatures
- java security
- groupdocs
- java pdf signature
title: Como assinar PDF com Java e timestamp
---

# Como assinar PDF com Java e timestamp

Quando você precisa proteger um contrato, fatura ou qualquer documento crítico contra adulteração, **como assinar PDF** de forma segura torna-se uma prioridade. Neste guia você descobrirá como adicionar uma assinatura digital e um timestamp confiável a um PDF usando GroupDocs.Signature for Java. A abordagem funciona offline, escala para arquivos de até 500 MB e requer apenas algumas linhas de código.

## Respostas rápidas
- **Qual biblioteca simplifica a assinatura de PDF em Java?** GroupDocs.Signature for Java.  
- **Preciso de conexão com a internet?** Apenas para a autoridade de timestamp; a assinatura criptográfica é executada localmente.  
- **Posso usar um certificado autoassinado para testes?** Sim, gere um com `keytool`.  
- **Existe um limite de tamanho?** A biblioteca pode assinar PDFs de até 500 MB sem carregar o arquivo inteiro na memória.  
- **Quantos formatos o GroupDocs suporta?** Mais de 50 formatos de entrada e saída, incluindo DOCX, XLSX, PPTX, HTML e imagens.

## Como assinar PDF com Java?

Carregue o PDF, configure um `DigitalSignature` com seu certificado, opcionalmente anexe um timestamp de um TSA compatível com RFC 3161 e chame `sign()`. O objeto `Signature` grava o arquivo assinado no disco, retornando um `SignResult` que indica se a operação foi bem‑sucedida e lista quaisquer avisos. Esse fluxo de ponta a ponta requer apenas algumas linhas de código Java e lida automaticamente com hashing, validação de certificado e recuperação de timestamp.

## Por que assinaturas digitais são importantes (e por que você precisa de timestamps)

Uma assinatura digital garante **autenticidade** (quem assinou) e **integridade** (o documento não foi alterado). Adicionar um timestamp comprova que a assinatura existia em um momento específico, protegendo você mesmo que o certificado de assinatura expire ou seja revogado posteriormente. Juntas, elas fornecem não‑repúdio — crítico para fluxos de trabalho legais, financeiros e regulatórios.

## Configurando GroupDocs.Signature para Java

### Métodos de integração

Escolha a ferramenta de build que preferir:

**Para usuários Maven**  
Adicione a dependência ao seu `pom.xml`:

As coordenadas Maven a seguir obtêm a versão estável mais recente do GroupDocs.Signature para Java.

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Para usuários Gradle**  
Adicione a linha ao seu `build.gradle`:

O Gradle resolverá a biblioteca a partir do Maven Central.

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Download direto (se preferir)**  
Acesse [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) e faça o download do arquivo JAR. Adicione-o ao classpath do seu projeto manualmente. Consulte a [GroupDocs.Signature Documentation](https://docs.groupdocs.com/signature/java/) para uma referência completa da API. Para a compilação mais recente, veja a [Latest Version & Releases](https://releases.groupdocs.com/signature/java/).

*Dica profissional:* Maven ou Gradle automatizam atualizações de versão e dependências transitivas, economizando tempo quando novos patches de segurança são lançados.

### Obtendo sua licença

GroupDocs oferece três opções de licenciamento:

1. **Teste gratuito** – avalie todos os recursos sem marca d'água. [Download Trial Version](https://releases.groupdocs.com/signature/java/)  
2. **Licença temporária** – chave de acesso total por 30 dias para desenvolvimento.  
3. **Licença comercial** – pronta para produção, uso ilimitado. [Buy License](https://purchase.groupdocs.com/buy)

Se surgir alguma dúvida, a comunidade está ativa no [GroupDocs Forum](https://forum.groupdocs.com/c/signature/).

### Inicialização básica

`Signature` é o objeto de nível superior do GroupDocs.Signature que representa um único arquivo PDF na memória. Depois de criar uma instância, todas as operações de leitura/escrita fluem através dele.

```java
import com.groupdocs.signature.Signature;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
final Signature signature = new Signature(filePath);
```

## Como adicionar assinatura digital a PDF Java: passo a passo

O processo é linear: importe classes, defina caminhos de arquivos, crie um objeto `Signature`, configure um `DigitalSignature` com timestamp opcional, defina `SignOptions` e, então, assine e salve.

### Etapa 1: importar classes necessárias

As importações a seguir dão acesso à configuração da assinatura, posicionamento e funcionalidade de timestamp.

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.PdfDigitalSignature;
import com.groupdocs.signature.domain.structs.TimeStamp;
import com.groupdocs.signature.options.sign.DigitalSignOptions;
```

### Etapa 2: definir os caminhos dos arquivos

Configure os caminhos para o PDF de entrada, o certificado (PFX) e o local de saída. Mantenha o arquivo de certificado seguro; ele contém sua chave privada.

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
String certificatePath = "YOUR_DOCUMENT_DIRECTORY/certificate.pfx";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/digitallySignedTimeStamp.pdf";
```

### Etapa 3: inicializar o objeto Signature

`Signature` é o ponto de entrada para todas as ações de assinatura. Criá‑lo carrega o PDF na memória e prepara a API para operações subsequentes.

```java
final Signature signature = new Signature(filePath);
```

### Etapa 4: configurar propriedades da assinatura e timestamp

`DigitalSignature` é o selo criptográfico que será incorporado ao PDF. Você também pode anexar um timestamp de uma autoridade confiável.

```java
PdfDigitalSignature pdfDigitalSignature = new PdfDigitalSignature();
pdfDigitalSignature.setContactInfo("Contact Information");
pdfDigitalSignature.setLocation("Location Info");
pdfDigitalSignature.setReason("Signing Reason");

// Configure the TimeStamp with URL, User Id, and Password
TimeStamp timeStamp = new TimeStamp("https://freetsa.org/tsr", "User Id", "Password");
pdfDigitalSignature.setTimeStamp(timeStamp);
```

* **ContactInfo** – por exemplo, `john.doe@company.com`  
* **Location** – por exemplo, `New York Office`  
* **Reason** – por exemplo, `Contract Approval`  

Usamos o FreeTSA (uma autoridade de timestamp gratuita) para demonstração. Em produção, escolha um TSA comercial para garantir disponibilidade e validade legal.

### Etapa 5: configurar opções de assinatura digital

`SignOptions` agrega o certificado, aparência visual e configurações de posicionamento para a assinatura digital.

```java
DigitalSignOptions options = new DigitalSignOptions(certificatePath);
options.setPassword("YourCertificatePassword"); // Certificate password
options.setSignature(pdfDigitalSignature); // Attach the PdfDigitalSignature object

// Specify signature alignment (where it appears on the page)
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
```

### Etapa 6: assinar e salvar o documento

`SignResult` fornece o resultado da operação de assinatura, incluindo o status de sucesso e quaisquer avisos.

```java
try {
    SignResult signResult = signature.sign(outputFilePath, options);
    System.out.println("Document signed successfully!");
    System.out.println("Output: " + outputFilePath);
} catch (Exception e) {
    throw new RuntimeException("Error during signing process: " + e.getMessage());
}
```

## Armadilhas comuns a evitar

### 1. problemas de certificado

**Problema:** erros “Invalid certificate”.  
**Correção:** Verifique a senha com `keytool -list -v -keystore your.pfx`.

```bash
keytool -list -v -keystore certificate.pfx -storetype PKCS12
```

### 2. timeouts do serviço de timestamp

**Problema:** timeouts de rede ao contatar o TSA.  
**Correção:** Teste a conectividade (`curl -I https://freetsa.org/tsr`), adicione lógica de repetição ou configure um TSA alternativo.

```java
new File(outputFilePath).getParentFile().mkdirs();
```

### 3. problemas de permissão de arquivo

**Problema:** “Access denied” ao salvar.  
**Correção:** Garanta que o diretório de saída exista e que a aplicação tenha permissões de gravação.

```bash
keytool -genkeypair -alias mykey -keyalg RSA -keysize 2048 -storetype PKCS12 -keystore certificate.pfx -validity 365
```

### 4. problemas de memória com PDFs grandes

**Problema:** `OutOfMemoryError` para arquivos grandes.  
**Correção:** Aumente o heap da JVM (`-Xmx4g`) ou processe arquivos em lotes.

### 5. posicionamento incorreto da assinatura

**Problema:** A assinatura sobrepõe conteúdo existente.  
**Correção:** Teste as configurações de alinhamento primeiro; para posicionamento pixel‑perfeito, use opções baseadas em coordenadas.

## Dicas de gerenciamento de certificados

### Obtendo um certificado para desenvolvimento

Gere um certificado autoassinado com o `keytool` do Java para fins de teste.

```java
   String certPassword = System.getenv("CERT_PASSWORD");
   ```

### Melhores práticas de certificado

1. **Nunca codifique senhas** – use variáveis de ambiente.  
2. **Rotacione certificados** antes que expirem.  
3. **Armazene chaves privadas** em hardware seguro (HSM) para aplicativos de alta segurança.  
4. **Faça backup de certificados** em local protegido.  
5. **Valide certificados** antes de assinar para detectar os expirados ou revogados.

## Melhores práticas de segurança

### 1. proteger chaves privadas

Armazene certificados fora do diretório do projeto, use configurações específicas por ambiente e considere HSMs para implantações corporativas.

### 2. validar PDFs de entrada

Verifique corrupção, assinaturas existentes, limites de tamanho e conformidade de conteúdo antes de assinar.

### 3. implementar registro de auditoria

Registre cada operação de assinatura com timestamp, usuário, nome do documento e status.

```java
try {
    SignResult result = signature.sign(outputFilePath, options);
    logger.info("Document signed: " + filePath + " by " + signerEmail);
} catch (Exception e) {
    logger.error("Signing failed: " + filePath + " - " + e.getMessage());
    // Handle appropriately
}
```

### 4. usar autoridades de timestamp confiáveis

Nunca dependa do horário do sistema local; sempre solicite um timestamp de um TSA compatível com RFC 3161.

### 5. implementar tratamento de erros

Capture exceções sem expor detalhes sensíveis.

```java
try {
    signature.sign(outputFilePath, options);
} catch (Exception e) {
    // Log detailed error internally
    logger.error("Signing error: " + e.getMessage(), e);
    // Return generic error to client
    throw new ApplicationException("Unable to sign document. Please try again.");
}
```

## Casos de uso e aplicações reais

1. **Sistemas de gerenciamento de contratos** – funcionários assinam NDAs e acordos eletronicamente; timestamps comprovam exatamente quando cada contrato foi aceito.  
2. **Processamento de documentos financeiros** – assine em lote faturas e pedidos de compra, fornecendo um rastro de auditoria imutável para reguladores.  
3. **Verificação de credenciais educacionais** – universidades emitem históricos escolares à prova de adulteração que podem ser validados instantaneamente via link de QR‑code.  
4. **Gerenciamento de licenças de software** – gere certificados de licença com assinatura digital e timestamp para prevenir falsificação.  
5. **Conformidade regulatória (FDA 21 CFR Part 11, etc.)** – empresas de dispositivos médicos assinam SOPs e relatórios de validação; timestamps atendem aos requisitos de não‑repúdio.

## Considerações de desempenho e otimização

### Gerenciamento de memória

Processar PDFs grandes em lotes, fechar objetos `Signature` prontamente e aumentar o tamanho do heap quando necessário.

### Otimização de rede para timestamps

Agrupe conexões HTTP, implemente tentativas com backoff exponencial e faça cache de timestamps para assinaturas sucessivas rápidas.

### Melhores práticas de processamento em lote

```java
// Pseudo‑code: process a list of PDFs in parallel, limiting to 5 concurrent TSA calls
```  
*Evite criar muitas threads; 5‑10 assinaturas simultâneas equilibram o throughput e a carga do TSA.*

### Otimização de I/O de disco

Use SSDs para arquivos temporários, minimize ciclos de leitura/gravação e limpe artefatos temporários após cada execução de assinatura.

## Guia de solução de problemas

### Erro: “Invalid certificate password”

**Solução:** Verifique a senha com `keytool -list -keystore your.pfx`.

```java
ExecutorService executor = Executors.newFixedThreadPool(5);
List<Future<SignResult>> futures = new ArrayList<>();

for (String pdfPath : pdfPaths) {
    futures.add(executor.submit(() -> {
        try (Signature sig = new Signature(pdfPath)) {
            return sig.sign(outputPath, options);
        }
    }));
}

// Wait for all to complete
for (Future<SignResult> future : futures) {
    SignResult result = future.get();
    // Process result
}

executor.shutdown();
```

### Erro: “Timestamp authority not responding”

**Solução:** Teste a URL do TSA, verifique regras de firewall e adicione lógica de TSA alternativo.

```bash
keytool -list -v -keystore certificate.pfx -storetype PKCS12
```

### Erro: “PDF is already signed”

**Solução:** Detecte assinaturas existentes primeiro; ou adicione uma contra‑assinatura ou assine uma cópia nova.

### Erro: “Access denied” ao salvar

**Solução:** Garanta que o diretório de saída exista, que o aplicativo tenha direitos de gravação e que nenhum outro processo bloqueie o arquivo.

```java
TimeStamp timeStamp;
try {
    timeStamp = new TimeStamp("https://freetsa.org/tsr", "", "");
} catch (Exception e) {
    // Fallback to alternative TSA
    timeStamp = new TimeStamp("https://alternate-tsa.com/tsr", "", "");
}
```

### Erro: OutOfMemoryError

**Solução:** Aumente o heap da JVM, processe PDFs em lotes menores ou troque para APIs de streaming para arquivos muito grandes.

## Conclusão e próximos passos

Agora você sabe **como assinar PDF** com Java, adicionar um timestamp confiável e evitar armadilhas comuns. Em seguida, você pode:

1. Adicionar múltiplos campos de assinatura para acordos multipartes.  
2. Verificar assinaturas programaticamente com GroupDocs.Signature.  
3. Personalizar a aparência visual das assinaturas (imagens, texto, posicionamento).  
4. Construir um serviço robusto de assinatura em lote com filas e monitoramento.

## Perguntas frequentes

**Q: Qual a diferença entre assinatura digital e assinatura eletrônica?**  
A: Uma assinatura digital usa algoritmos criptográficos para verificar identidade e detectar adulteração, enquanto uma assinatura eletrônica pode ser tão simples quanto um nome digitado.

**Q: Preciso de conexão à internet para assinar PDFs?**  
A: Apenas para o serviço de timestamp; a assinatura criptográfica em si é executada localmente.

**Q: PDFs assinados podem ser editados depois?**  
A: Qualquer modificação quebra a assinatura, e os visualizadores de PDF exibirão um aviso indicando que o documento foi alterado.

**Q: Como verifico um PDF assinado?**  
A: A maioria dos leitores de PDF verifica automaticamente; programaticamente, use a API de verificação do GroupDocs.Signature para checar status, detalhes do assinante e validade do timestamp.

**Q: O que acontece se meu certificado expirar depois que eu assinei documentos?**  
A: O timestamp incorporado prova que a assinatura foi criada enquanto o certificado ainda era válido, preservando a validade legal.

**Q: Posso usar isso com armazenamento em nuvem (S3, Azure Blob, etc.)?**  
A: Sim—baixe o PDF para um local temporário, assine-o e depois faça upload da versão assinada de volta para a nuvem.

**Q: Existem limites de tamanho de arquivo?**  
A: A biblioteca lida com PDFs de até 500 MB sem carregar o arquivo inteiro na memória; arquivos maiores podem exigir streaming.

**Q: Quanto custa o GroupDocs.Signature para uso comercial?**  
A: O preço varia conforme o tipo de implantação; entre em contato com as vendas da GroupDocs para as tarifas mais recentes. Testes gratuitos e licenças temporárias estão disponíveis para avaliação.

**Q: Isso funciona em servidores Linux?**  
A: Absolutamente. GroupDocs.Signature for Java é independente de plataforma e roda em qualquer SO com JRE.

**Última atualização:** 2026-09-05  
**Testado com:** GroupDocs.Signature 23.9 for Java  
**Autor:** GroupDocs

## Tutoriais relacionados

- [Como Verificar Certificados Digitais em Java - Guia Completo com Exemplos de Código](/signature/java/digital-signatures/java-certificate-verification-groupdocs-signature/)
- [Como Assinar PDF Programaticamente em Java com GroupDocs.Signature](/signature/java/digital-signatures/sign-pdfs-groupdocs-signature-java/)
- [Adicionar Assinatura de Imagem a PDF Java com GroupDocs](/signature/java/image-signatures/sign-pdf-image-signature-groupdocs-java/)

```java
File outputFile = new File(outputFilePath);
outputFile.getParentFile().mkdirs(); // Create directories if needed

if (!outputFile.canWrite() && outputFile.exists()) {
    throw new IOException("Cannot write to " + outputFilePath);
}
```