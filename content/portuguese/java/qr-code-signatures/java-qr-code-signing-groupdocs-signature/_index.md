---
"date": "2025-05-08"
"description": "Aprenda a implementar assinatura de código QR em Java usando o GroupDocs.Signature. Aumente a segurança de documentos, configure opções de assinatura e aplique criptografia personalizada em seus aplicativos Java."
"title": "Guia de assinatura de código QR Java - Proteja seus documentos com GroupDocs.Signature"
"url": "/pt/java/qr-code-signatures/java-qr-code-signing-groupdocs-signature/"
"weight": 1
---

# Implementando assinatura de código QR Java com GroupDocs.Signature para Java

## Introdução

Aumente a segurança dos seus documentos digitais incorporando códigos QR em seus aplicativos Java. Utilizar o GroupDocs.Signature para Java permite garantir a autenticidade e a rastreabilidade dos documentos de forma eficaz. Este guia orientará você na criação de assinaturas de dados personalizadas, na configuração de opções de assinatura de código QR e na proteção dos seus documentos com criptografia robusta.

**O que você aprenderá:**
- Como criar uma classe de assinatura de dados personalizada usando GroupDocs.Signature
- Configurando opções de sinalização de código QR em aplicativos Java
- Assinatura de documentos com códigos QR e aplicação de criptografia personalizada

Vamos nos aprofundar nos pré-requisitos e começar a integrar essa funcionalidade aos seus projetos!

## Pré-requisitos

Antes de começar, certifique-se de ter configurado as bibliotecas e dependências necessárias no seu ambiente de desenvolvimento.

### Bibliotecas e versões necessárias

Para implementar GroupDocs.Signature para Java, inclua a seguinte dependência:

**Especialista**
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle**
```gradle
implementation 'com.groupdocs:groupdocs-signation:23.12'
```

Você também pode baixar a versão mais recente diretamente de [GroupDocs.Signature para versões Java](https://releases.groupdocs.com/signature/java/).

### Requisitos de configuração do ambiente

- Certifique-se de ter um Java Development Kit (JDK) instalado.
- Configure seu Ambiente de Desenvolvimento Integrado (IDE), como IntelliJ IDEA ou Eclipse.

### Pré-requisitos de conhecimento

- Noções básicas de programação Java e conceitos orientados a objetos.
- Familiaridade com o tratamento de dependências usando Maven ou Gradle.

## Configurando GroupDocs.Signature para Java

Para começar, configure o GroupDocs.Signature no seu projeto seguindo as instruções de instalação acima para incluí-lo na sua configuração de compilação.

### Etapas de aquisição de licença

O GroupDocs oferece diferentes opções de licenciamento:
- **Teste grátis**: Teste todos os recursos sem limitações.
- **Licença Temporária**: Obtenha uma licença para fins de avaliação.
- **Comprar**: Adquira uma licença completa para uso comercial.

Após o download, inicialize o GroupDocs.Signature assim:

```java
import com.groupdocs.signature.Signature;

class InitializeGroupDocs {
    public static void main(String[] args) {
        Signature signature = new Signature("path/to/your/document");
        // Agora você pode começar a usar o objeto de assinatura para trabalhar com documentos.
    }
}
```

## Guia de Implementação

Vamos dividir o processo de implementação em seções gerenciáveis, com foco nos principais recursos.

### Classe de Assinatura de Dados Personalizada

#### Visão geral
Crie uma classe personalizada para armazenar dados de assinatura, como ID, autor, data da assinatura e fatores adicionais. Isso garante que você tenha todos os metadados necessários encapsulados em suas assinaturas.

#### Implementação passo a passo

**Defina a classe DocumentSignatureData**

```java
import com.groupdocs.signature.domain.extensions.serialization.FormatAttribute;
import java.util.Date;
import java.math.BigDecimal;

class DocumentSignatureData {
    @FormatAttribute(propertyName = "SignID")
    public String ID; // Identificador único para a assinatura
    
    public String getID() { return ID; }
    public void setID(String value) { ID = value; }
    
    @FormatAttribute(propertyName = "SAuth")
    public final String Author; // Autor do documento
    
    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }
    
    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public final Date Signed = new Date(); // Data e hora da assinatura
    
    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }
    
    @FormatAttribute(propertyName = "SDFact", propertyFormat = "N2")
    public final BigDecimal DataFactor = new BigDecimal(0.01); // Fator de dados adicional para assinatura
    
    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```

**Explicação:**
- **Atributo de formato**: Anota propriedades para personalizar a serialização.
- **Propriedades**: Capture detalhes essenciais como ID exclusivo, nome do autor, data de assinatura e fator de dados.

### Configuração de opções de assinatura de código QR

#### Visão geral
Configure as opções de assinatura do código QR para definir como seus códigos QR aparecerão nos documentos, incluindo tamanho, alinhamento e preenchimento.

#### Implementação passo a passo

**Defina a classe QrCodeSignOptionsConfig**

```java
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

class QrCodeSignOptionsConfig {
    public static QrCodeSignOptions setupQrCodeSignOptions(DocumentSignatureData documentSignature) {
        QrCodeSignOptions options = new QrCodeSignOptions();
        
        // Serializar o objeto de dados personalizado em código QR
        options.setData(documentSignature);
        
        // Especificar o tipo de código QR
        options.setEncodeType(QrCodeTypes.QR);
        
        // Configurar preenchimento para alinhamento
        Padding padding = new Padding();
        padding.setRight(10); // Preenchimento direito em pixels
        padding.setBottom(10); // Preenchimento inferior em pixels
        options.setMargin(padding);
        
        // Definir tamanho e posição do código QR
        options.setHeight(100);
        options.setWidth(100);
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        options.setHorizontalAlignment(HorizontalAlignment.Right);
        
        return options;
    }
}
```

**Explicação:**
- **Opções de assinatura de código QR**: Gerencia como o código QR é exibido, incluindo seu tamanho e posição.
- **Preenchimento**Ajusta o alinhamento dentro do documento.

### Assinatura de documentos com código QR e criptografia personalizada

#### Visão geral
Combine códigos QR e criptografia personalizada para assinar documentos com segurança. Isso garante a integridade e a confidencialidade dos dados.

#### Implementação passo a passo

**Assine um documento com código QR**

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.exception.GroupDocsSignatureException;

import java.util.UUID;

class SignDocumentWithQRCode {
    public static void signDocument(String filePath, String outputFilePath) throws Exception {
        try {
            Signature signature = new Signature(filePath);

            // Estratégia de criptografia XOR personalizada
            IDataEncryption encryption = new CustomXOREncryption();

            // Configurar o objeto de dados de assinatura de documento personalizado
            DocumentSignatureData documentSignature = new DocumentSignatureData();
            documentSignature.setID(UUID.randomUUID().toString());
            documentSignature.setAuthor(System.getenv("USERNAME"));
            documentSignature.setSigned(new Date());
            documentSignature.setDataFactor(new BigDecimal("11.22"));

            // Configurar opções de QR-Code
            QrCodeSignOptions options = QrCodeSignOptionsConfig.setupQrCodeSignOptions(documentSignature);

            // Aplique criptografia aos dados dentro do código QR
            options.setDataEncryption(encryption);

            // Assine e salve o documento
            signature.sign(outputFilePath, options);
        } catch (Exception e) {
            throw new GroupDocsSignatureException(e.getMessage());
        }
    }
}
```

**Explicação:**
- **Criptografia XOREnsion personalizada**: Implementa uma estratégia de criptografia personalizada para proteger dados de código QR.
- **UUID**: Gera um identificador exclusivo para cada assinatura.