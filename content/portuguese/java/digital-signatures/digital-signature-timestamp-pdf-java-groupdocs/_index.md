---
categories:
- Java Development
date: '2026-06-11'
description: Aprenda a assinar PDF com Java usando GroupDocs.Signature, adicionar
  assinatura digital e carimbo de tempo. Guia passo a passo com exemplos de código
  e boas práticas.
keywords:
- how to sign pdf
- add digital signature pdf
- timestamp pdf signature
- java pdf signature library
- groupdocs signature java
lastmod: '2026-06-11'
linktitle: Adicionar assinatura digital ao PDF Java
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to sign PDF with Java using GroupDocs.Signature, add digital
    signature and timestamp. Step-by-step guide with code examples and best practices.
  headline: 'How to Sign PDF with Java: Add Digital Signature and Timestamp'
  type: TechArticle
- description: Learn how to sign PDF with Java using GroupDocs.Signature, add digital
    signature and timestamp. Step-by-step guide with code examples and best practices.
  name: 'How to Sign PDF with Java: Add Digital Signature and Timestamp'
  steps:
  - name: Import Required Classes
    text: The following imports give you access to signature configuration, positioning,
      and timestamp functionality.
  - name: Define Your File Paths
    text: Set up paths for your input PDF, certificate, and where you want the signed
      PDF saved. Keep the certificate file secure; it contains your private key.
  - name: Initialize the Signature Object
    text: Create a `Signature` instance pointing to the PDF you want to sign. This
      loads the PDF into memory and prepares it for signing.
  - name: Configure Signature Properties and Timestamp
    text: The `DigitalSignature` class represents the cryptographic seal that will
      be embedded in the PDF. You can also attach a timestamp from a trusted authority.
      * **ContactInfo** – e.g., `john.doe@company.com` * **Location** – e.g., `New
      York Office` * **Reason** – e.g., `Contract Approval` We use FreeTSA
  - name: Configure Digital Sign Options
    text: The `SignOptions` class ties together the certificate, signature properties,
      and visual placement. Alignment enums control where the signature appears.
  - name: Sign and Save the Document
    text: Execute the signing process and write the signed PDF to disk. The returned
      `SignResult` object tells you whether the operation succeeded and lists any
      warnings.
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
- pdf-signing
- digital-signatures
- java-security
- groupdocs
title: 'Como assinar PDF com Java: adicionar assinatura digital e carimbo de tempo'
type: docs
url: /pt/java/digital-signatures/digital-signature-timestamp-pdf-java-groupdocs/
weight: 1
---

# Como Assinar PDF com Java e Carimbo de Tempo

Já enviou um documento importante e ficou preocupado se alguém poderia adulterá‑lo depois? Você não está sozinho. Seja construindo um sistema corporativo de gerenciamento de documentos, criando uma plataforma de assinatura de contratos ou apenas precisando proteger seus arquivos PDF programaticamente, **como assinar PDF** com um carimbo de tempo confiável é a solução. Adicionar uma assinatura digital não apenas comprova quem assinou o arquivo, mas também cria um registro imutável de *exatamente* quando a assinatura ocorreu.

## Respostas Rápidas
- **Qual biblioteca simplifica a assinatura de PDF em Java?** GroupDocs.Signature para Java.  
- **Preciso de conexão com a internet?** Apenas para a autoridade de carimbo de tempo; a assinatura em si funciona offline.  
- **Posso usar um certificado autoassinado para testes?** Sim, gere um com `keytool`.  
- **Existe limite de tamanho?** A biblioteca pode assinar PDFs de até 500 MB sem carregar todo o arquivo na memória.  
- **Quantos formatos o GroupDocs suporta?** Mais de 50 formatos de entrada e saída, incluindo DOCX, XLSX, PPTX, HTML e imagens.

## Por que Assinaturas Digitais Importam (E Por que Você Precisa de Carimbos de Tempo)

Carregue seu PDF, aplique um selo criptográfico e incorpore um carimbo de tempo confiável — esse processo de duas etapas garante autenticação, integridade e não‑repúdio. O carimbo de tempo comprova que a assinatura existia em um momento específico, mesmo que o certificado de assinatura expire ou seja revogado posteriormente.

## Como Assinar PDF com Java?

Carregue seu PDF com `new Signature("input.pdf")`, configure um objeto `DigitalSignature`, anexe um carimbo de tempo de uma autoridade confiável e chame `sign()` — toda a operação é concluída em poucas linhas de código. GroupDocs.Signature trata do parsing do certificado, cálculo de hash e recuperação do carimbo de tempo automaticamente, permitindo que você foque na lógica de negócios ao invés de criptografia.

## Configurando GroupDocs.Signature para Java

### Métodos de Integração

Escolha a ferramenta de build que estiver usando:

**Para Usuários Maven:**  
Adicione esta dependência ao seu `pom.xml`:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Para Usuários Gradle:**  
Adicione isto ao seu `build.gradle`:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Download Direto (Se Preferir):**  
Acesse [Lançamentos do GroupDocs.Signature para Java](https://releases.groupdocs.com/signature/java/) e baixe o arquivo JAR. Adicione‑o ao classpath do seu projeto manualmente. Consulte a [Documentação do GroupDocs.Signature](https://docs.groupdocs.com/signature/java/) para referência detalhada da API. Para a versão mais recente, veja [Versão Mais Recente & Lançamentos](https://releases.groupdocs.com/signature/java/).

Dica: Use Maven ou Gradle sempre que possível — isso facilita o gerenciamento de dependências e atualizações ao longo do tempo.

### Obtendo Sua Licença

GroupDocs oferece algumas opções, dependendo da fase do seu projeto:

1. **Teste Gratuito** – Ideal para avaliação. [Baixar Versão de Teste](https://releases.groupdocs.com/signature/java/) e experimentar todos os recursos.  
2. **Licença Temporária** – Precisa de acesso total para desenvolvimento sem a marca d'água de teste? Obtenha uma licença temporária de 30 dias.  
3. **Licença Comercial** – Para uso em produção, [Comprar Licença](https://purchase.groupdocs.com/buy). O preço varia conforme o tipo de implantação.

Precisa de ajuda? Visite o [Fórum do GroupDocs](https://forum.groupdocs.com/c/signature/).

### Inicialização Básica

A classe `Signature` é o objeto de nível superior do GroupDocs.Signature que representa um único arquivo PDF na memória. Após a instanciação, todas as operações de leitura e escrita passam por esse objeto.

```java
import com.groupdocs.signature.Signature;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
final Signature signature = new Signature(filePath);
```

Simples, não? Basta apontar para o seu arquivo PDF e você está pronto. O objeto `Signature` é sua interface principal para todas as operações de assinatura.

## Como Adicionar Assinatura Digital a PDF Java: Passo a Passo

Carregue seu PDF, configure os detalhes da assinatura, anexe um carimbo de tempo e salve o documento assinado — tudo em um fluxo claro e linear.

### Etapa 1: Importar Classes Necessárias

As importações a seguir dão acesso à configuração da assinatura, posicionamento e funcionalidade de carimbo de tempo.

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.PdfDigitalSignature;
import com.groupdocs.signature.domain.structs.TimeStamp;
import com.groupdocs.signature.options.sign.DigitalSignOptions;
```

### Etapa 2: Definir Seus Caminhos de Arquivo

Configure os caminhos para o PDF de entrada, o certificado e onde o PDF assinado será salvo. Mantenha o arquivo de certificado seguro; ele contém sua chave privada.

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
String certificatePath = "YOUR_DOCUMENT_DIRECTORY/certificate.pfx";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/digitallySignedTimeStamp.pdf";
```

### Etapa 3: Inicializar o Objeto Signature

Crie uma instância `Signature` apontando para o PDF que deseja assinar. Isso carrega o PDF na memória e o prepara para a assinatura.

```java
final Signature signature = new Signature(filePath);
```

### Etapa 4: Configurar Propriedades da Assinatura e Carimbo de Tempo

A classe `DigitalSignature` representa o selo criptográfico que será incorporado ao PDF. Você também pode anexar um carimbo de tempo de uma autoridade confiável.

```java
PdfDigitalSignature pdfDigitalSignature = new PdfDigitalSignature();
pdfDigitalSignature.setContactInfo("Contact Information");
pdfDigitalSignature.setLocation("Location Info");
pdfDigitalSignature.setReason("Signing Reason");

// Configure the TimeStamp with URL, User Id, and Password
TimeStamp timeStamp = new TimeStamp("https://freetsa.org/tsr", "User Id", "Password");
pdfDigitalSignature.setTimeStamp(timeStamp);
```

* **ContactInfo** – ex.: `john.doe@company.com`  
* **Location** – ex.: `New York Office`  
* **Reason** – ex.: `Contract Approval`  

Usamos o FreeTSA (uma autoridade de carimbo de tempo gratuita) para demonstração. Em produção, escolha um TSA comercial para garantir disponibilidade e validade jurídica.

### Etapa 5: Configurar Opções de Assinatura Digital

A classe `SignOptions` reúne o certificado, as propriedades da assinatura e o posicionamento visual. Os enums de alinhamento controlam onde a assinatura aparecerá.

```java
DigitalSignOptions options = new DigitalSignOptions(certificatePath);
options.setPassword("YourCertificatePassword"); // Certificate password
options.setSignature(pdfDigitalSignature); // Attach the PdfDigitalSignature object

// Specify signature alignment (where it appears on the page)
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
```

### Etapa 6: Assinar e Salvar o Documento

Execute o processo de assinatura e grave o PDF assinado no disco. O objeto `SignResult` retornado indica se a operação foi bem‑sucedida e lista eventuais avisos.

```java
try {
    SignResult signResult = signature.sign(outputFilePath, options);
    System.out.println("Document signed successfully!");
    System.out.println("Output: " + outputFilePath);
} catch (Exception e) {
    throw new RuntimeException("Error during signing process: " + e.getMessage());
}
```

## Armadilhas Comuns a Evitar

### 1. Problemas com Certificado
**Problema:** Erros “Invalid certificate”.  
**Correção:** Verifique a senha com `keytool -list -v -keystore your.pfx`.

```bash
keytool -list -v -keystore certificate.pfx -storetype PKCS12
```

### 2. Timeouts no Serviço de Carimbo de Tempo
**Problema:** Timeouts de rede ao contatar o TSA.  
**Correção:** Teste a conectividade (`curl -I https://freetsa.org/tsr`), adicione lógica de retry ou configure um TSA alternativo.

```java
new File(outputFilePath).getParentFile().mkdirs();
```

### 3. Problemas de Permissão de Arquivo
**Problema:** “Access denied” ao salvar.  
**Correção:** Garanta que o diretório de saída exista e que a aplicação tenha permissão de escrita.

```bash
keytool -genkeypair -alias mykey -keyalg RSA -keysize 2048 -storetype PKCS12 -keystore certificate.pfx -validity 365
```

### 4. Problemas de Memória com PDFs Grandes
**Problema:** `OutOfMemoryError` para arquivos volumosos.  
**Correção:** Aumente o heap da JVM (`-Xmx4g`) ou processe arquivos em lotes.

### 5. Posicionamento Incorreto da Assinatura
**Problema:** A assinatura sobrepõe conteúdo existente.  
**Correção:** Teste as configurações de alinhamento primeiro; para posicionamento pixel‑perfeito, use opções baseadas em coordenadas.

## Dicas de Gerenciamento de Certificados

### Obtendo um Certificado para Desenvolvimento

Genere um certificado autoassinado com o `keytool` do Java para fins de teste.

```java
   String certPassword = System.getenv("CERT_PASSWORD");
   ```

### Melhores Práticas com Certificados

1. **Nunca codifique senhas** – use variáveis de ambiente.  
2. **Rotacione certificados** antes que expirem.  
3. **Armazene chaves privadas** em hardware seguro (HSM) para aplicativos de alta segurança.  
4. **Faça backup dos certificados** em local protegido.  
5. **Valide certificados** antes de assinar para detectar expirados ou revogados.

## Melhores Práticas de Segurança

### 1. Proteger Chaves Privadas
Armazene certificados fora do diretório do projeto, use configurações específicas por ambiente e considere HSMs para implantações corporativas.

### 2. Validar PDFs de Entrada
Verifique corrupção, assinaturas existentes, limites de tamanho e conformidade de conteúdo antes de assinar.

### 3. Implementar Registro de Auditoria
Registre cada operação de assinatura com carimbo de tempo, usuário, nome do documento e status.

```java
try {
    SignResult result = signature.sign(outputFilePath, options);
    logger.info("Document signed: " + filePath + " by " + signerEmail);
} catch (Exception e) {
    logger.error("Signing failed: " + filePath + " - " + e.getMessage());
    // Handle appropriately
}
```

### 4. Usar Autoridades de Carimbo de Tempo Confiáveis
Nunca dependa do horário do sistema local; sempre solicite um carimbo de tempo de um TSA compatível com RFC 3161.

### 5. Implementar Tratamento de Erros
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

## Casos de Uso e Aplicações no Mundo Real

### 1. Sistemas de Gerenciamento de Contratos
Funcionários assinam NDAs e acordos eletronicamente; os carimbos de tempo provam exatamente quando cada contrato foi aceito.

### 2. Processamento de Documentos Financeiros
Assine em lote faturas e pedidos de compra, fornecendo um rastro de auditoria imutável para reguladores.

### 3. Verificação de Credenciais Educacionais
Universidades emitem históricos acadêmicos à prova de adulteração que podem ser validados instantaneamente via link em QR‑code.

### 4. Gerenciamento de Licenças de Software
Gere certificados de licença com assinatura digital e carimbo de tempo para impedir falsificações.

### 5. Conformidade Regulatória (FDA 21 CFR Part 11, etc.)
Empresas de dispositivos médicos assinam SOPs e relatórios de validação; os carimbos de tempo atendem aos requisitos de não‑repúdio.

## Considerações de Performance e Otimização

### Gerenciamento de Memória
Processe PDFs grandes em lotes, feche objetos `Signature` prontamente e aumente o heap quando necessário.

### Otimização de Rede para Carimbos de Tempo
Faça pool de conexões HTTP, implemente retries com backoff exponencial e faça cache de carimbos de tempo para assinaturas sucessivas rápidas.

### Melhores Práticas para Processamento em Lote
```java
// Pseudo‑code: process a list of PDFs in parallel, limiting to 5 concurrent TSA calls
```
*Evite criar muitas threads; 5‑10 assinaturas simultâneas equilibram throughput e carga no TSA.*

### Otimização de I/O de Disco
Use SSDs para arquivos temporários, minimize ciclos de leitura/escrita e limpe artefatos temporários após cada execução de assinatura.

## Guia de Solução de Problemas

### Erro: “Invalid Certificate Password”
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

### Erro: “Timestamp Authority Not Responding”
**Solução:** Teste a URL do TSA, verifique regras de firewall e adicione lógica de fallback para outro TSA.

```bash
keytool -list -v -keystore certificate.pfx -storetype PKCS12
```

### Erro: “PDF is Already Signed”
**Solução:** Detecte assinaturas existentes primeiro; adicione uma contra‑assinatura ou assine uma cópia nova.

### Erro: “Access Denied” Ao Salvar
**Solução:** Garanta que o diretório de saída exista, que o aplicativo tenha permissão de escrita e que nenhum outro processo esteja bloqueando o arquivo.

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
**Solução:** Aumente o heap da JVM, processe PDFs em lotes menores ou use APIs de streaming para arquivos muito grandes.

## Conclusão e Próximos Passos

Você aprendeu **como assinar PDF** com Java, adicionar um carimbo de tempo confiável e lidar com armadilhas comuns. Em seguida, explore:

1. Adicionar múltiplos campos de assinatura para acordos multipartes.  
2. Verificar assinaturas programaticamente com GroupDocs.Signature.  
3. Personalizar a aparência da assinatura (imagens, texto, posicionamento).  
4. Construir um serviço robusto de assinatura em lote com filas e monitoramento.

## Perguntas Frequentes

**P: Qual a diferença entre assinatura digital e assinatura eletrônica?**  
R: Uma assinatura digital usa algoritmos criptográficos para verificar identidade e detectar adulteração, enquanto uma assinatura eletrônica pode ser tão simples quanto um nome digitado.

**P: Preciso de conexão à internet para assinar PDFs?**  
R: Apenas para o serviço de carimbo de tempo; a assinatura criptográfica em si ocorre localmente.

**P: PDFs assinados podem ser editados depois?**  
R: Qualquer modificação quebra a assinatura, e os visualizadores de PDF exibem um aviso indicando que o documento foi alterado.

**P: Como verifico um PDF assinado?**  
R: A maioria dos leitores de PDF verifica automaticamente; programaticamente, use a API de verificação do GroupDocs.Signature para checar status, detalhes do assinante e validade do carimbo de tempo.

**P: O que acontece se meu certificado expirar após eu ter assinado documentos?**  
R: O carimbo de tempo incorporado prova que a assinatura foi criada enquanto o certificado ainda era válido, preservando a validade legal.

**P: Posso usar isso com armazenamento em nuvem (S3, Azure Blob, etc.)?**  
R: Sim — baixe o PDF para um local temporário, assine-o e depois faça upload da versão assinada de volta para a nuvem.

**P: Existem limites de tamanho de arquivo?**  
R: A biblioteca manipula PDFs de até 500 MB sem carregar todo o arquivo na memória; arquivos maiores podem exigir streaming.

**P: Quanto custa o GroupDocs.Signature para uso comercial?**  
R: O preço varia conforme o tipo de implantação; entre em contato com as vendas do GroupDocs para obter as tarifas mais recentes. Versões de teste e licenças temporárias estão disponíveis para avaliação.

**P: Isso funciona em servidores Linux?**  
R: Absolutamente. GroupDocs.Signature para Java é independente de plataforma e roda em qualquer OS com JRE.

---

**Última Atualização:** 2026-06-11  
**Testado Com:** GroupDocs.Signature 23.9 para Java  
**Autor:** GroupDocs

```java
File outputFile = new File(outputFilePath);
outputFile.getParentFile().mkdirs(); // Create directories if needed

if (!outputFile.canWrite() && outputFile.exists()) {
    throw new IOException("Cannot write to " + outputFilePath);
}
```

## Tutoriais Relacionados

- [Como Verificar Certificados Digitais em Java - Guia Completo com Exemplos de Código](/signature/java/digital-signatures/java-certificate-verification-groupdocs-signature/)
- [Como Assinar PDF Programaticamente em Java com GroupDocs.Signature](/signature/java/digital-signatures/sign-pdfs-groupdocs-signature-java/)
- [Adicionar Assinatura de Imagem a PDF Java com GroupDocs](/signature/java/image-signatures/sign-pdf-image-signature-groupdocs-java/)