---
"date": "2025-05-08"
"description": "Aprenda a proteger metadados de imagens usando criptografia com o GroupDocs.Signature para Java. Garanta a integridade e a autenticidade dos dados com orientações passo a passo."
"title": "Implementar assinatura e criptografia de metadados de imagem em Java com GroupDocs.Signature"
"url": "/pt/java/metadata-signatures/groupdocs-signature-java-image-metadata-encryption/"
"weight": 1
---

# Implementar assinatura de metadados de imagem com criptografia em Java usando GroupDocs.Signature

## Introdução

No cenário digital atual, proteger informações sensíveis contidas em metadados de documentos é fundamental. Seja lidando com contratos comerciais confidenciais ou fotos de identificação pessoal, manter a integridade e a autenticidade dos metadados de imagem ajuda a prevenir acesso não autorizado e adulteração. **GroupDocs.Signature para Java** fornece uma solução robusta para assinar e criptografar metadados de imagem com segurança.

Este tutorial orienta você na implementação da assinatura de metadados de imagem com criptografia em Java usando os poderosos recursos do GroupDocs.Signature. Seguindo estes passos, você integrará essa funcionalidade aos seus aplicativos Java de forma eficaz.

**O que você aprenderá:**
- Assinando metadados de documentos usando GroupDocs.Signature para Java
- Implementando assinaturas de objetos personalizadas com criptografia
- Configurando um ambiente seguro usando criptografia de chave simétrica

## Pré-requisitos

Antes de começar, certifique-se de que os seguintes pré-requisitos sejam atendidos:

### Bibliotecas e dependências necessárias:
- **GroupDocs.Signature para Java**: Certifique-se de ter a versão 23.12 ou posterior.

### Requisitos de configuração do ambiente:
- Instale o Java Development Kit (JDK) na sua máquina.
- Use um Ambiente de Desenvolvimento Integrado (IDE) como IntelliJ IDEA, Eclipse ou NetBeans.

### Pré-requisitos de conhecimento:
- Noções básicas de programação Java.
- Familiaridade com Maven ou Gradle para gerenciamento de dependências.

## Configurando GroupDocs.Signature para Java

Para usar GroupDocs.Signature em seu projeto, inclua as dependências necessárias da seguinte maneira:

### Usando Maven
Adicione isso ao seu `pom.xml` arquivo:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Usando Gradle
Inclua isso em seu `build.gradle` arquivo:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Download direto
Alternativamente, baixe a versão mais recente em [GroupDocs.Signature para versões Java](https://releases.groupdocs.com/signature/java/).

#### Etapas de aquisição de licença
- **Teste grátis**: Comece com um teste para explorar os recursos.
- **Licença Temporária**: Solicite testes extensivos, se necessário.
- **Comprar**: Adquira uma licença para uso de produção de [Documentos do Grupo](https://purchase.groupdocs.com/buy).

## Inicialização e configuração básicas

Veja como você pode inicializar GroupDocs.Signature em seu aplicativo Java:

```java
import com.groupdocs.signature.Signature;

public class InitializeSignature {
    public static void main(String[] args) {
        // Caminho para o documento
        String filePath = "path/to/your/document.jpg";
        
        // Crie uma nova instância de Signature
        Signature signature = new Signature(filePath);

        System.out.println("GroupDocs.Signature initialized successfully.");
    }
}
```

## Guia de Implementação

### Recurso: Assinatura de metadados com objeto personalizado

#### Visão geral
Esse recurso permite assinar metadados de imagem usando um objeto personalizado e criptografá-los para maior segurança, garantindo que somente partes autorizadas possam acessar ou modificar os metadados.

#### Implementação passo a passo

##### 1. Defina a classe de dados da assinatura do seu documento
Crie uma classe para armazenar suas informações de metadados:

```java
import java.math.BigDecimal;
import java.util.Date;

class DocumentSignatureData {
    private String ID;
    private String Author;
    private Date Signed = new Date();
    private BigDecimal DataFactor = new BigDecimal(0.01);

    public String getID() { return ID; }
    public void setID(String value) { ID = value; }

    @FormatAttribute(propertyName = "SignID")
    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }

    @FormatAttribute(propertyName = "SAuth")
    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }

    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```

##### 2. Implementar a lógica de assinatura
Veja como assinar metadados usando criptografia:

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
import com.groupdocs.signature.domain.signatures.metadata.ImageMetadataSignature;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.MetadataSignOptions;

import java.io.File;
import java.nio.file.Paths;
import java.util.UUID;

public class SignMetadataWithCustomObject {
    // Inicializar caminhos de arquivo com marcadores de posição
    String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleImage.jpg";
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", 
                                       "SignedImageWithCustomMetadata/SampleImage_signed.jpg").getPath();

    public void run() throws Exception {
        Signature signature = new Signature(filePath);

        // Configurar chave e senha para criptografia
        String key = "1234567890";
        String salt = "1234567890";
        IDataEncryption encryption = new SymmetricEncryption(
            SymmetricAlgorithmType.Rijndael, key, salt);

        MetadataSignOptions options = new MetadataSignOptions();
        DocumentSignatureData documentSignature = new DocumentSignatureData();
        
        // Definir propriedades de metadados personalizadas
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME"));
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        ImageMetadataSignature mdDocument = new ImageMetadataSignature(41996, documentSignature);
        mdDocument.setDataEncryption(encryption);

        // Adicionar assinaturas de metadados às opções
        options.getSignatures().add(mdDocument);

        signature.sign(outputFilePath, options);
    }
}
```

#### Opções de configuração de teclas
- **Criptografia Simétrica**: Utiliza o algoritmo Rijndael para criptografia.
- **Opções de Sinal de Metadados**: Configura o processo de assinatura e especifica quais metadados assinar.

##### Dicas para solução de problemas
- Certifique-se de que os caminhos dos seus arquivos estejam corretos e acessíveis.
- Verifique se a variável de ambiente `USERNAME` está configurado corretamente.
- Verifique se a versão da biblioteca GroupDocs.Signature corresponde às suas dependências de código.

### Recurso: Assinatura de metadados com criptografia

#### Visão geral
Este recurso se concentra na criptografia de assinaturas de metadados para proteger informações confidenciais em arquivos de imagem.

#### Implementação passo a passo
##### 1. Implementar a lógica de criptografia
Veja como assinar metadados usando criptografia:
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.MetadataSignOptions;

import java.io.File;
import java.nio.file.Paths;
import java.util.UUID;

public class SignMetadataWithEncryption {
    // Inicializar caminhos de arquivo com marcadores de posição
    String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleImage.jpg";
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", 
                                       "SignedImageWithEncryption/SampleImage_signed.jpg").getPath();

    public void run() throws Exception {
        Signature signature = new Signature(filePath);

        // Configurar chave e senha para criptografia
        String key = "1234567890";
        String salt = "1234567890";
        IDataEncryption encryption = new SymmetricEncryption(
            SymmetricAlgorithmType.Rijndael, key, salt);

        MetadataSignOptions options = new MetadataSignOptions();
        DocumentSignatureData documentSignature = new DocumentSignatureData();
        
        // Definir propriedades de metadados personalizadas
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME"));
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        ImageMetadataSignature mdDocument = new ImageMetadataSignature(41996, documentSignature);
        mdDocument.setDataEncryption(encryption);

        // Adicionar assinaturas de metadados às opções
        options.getSignatures().add(mdDocument);

        signature.sign(outputFilePath, options);
    }
}
```