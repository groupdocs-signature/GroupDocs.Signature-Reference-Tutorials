---
"date": "2025-05-08"
"description": "Aprenda a proteger PDFs usando criptografia de código QR e assinaturas digitais com o GroupDocs.Signature para Java. Aumente a segurança dos seus documentos com eficiência."
"title": "Implementar assinatura segura de PDF com criptografia de código QR em Java usando GroupDocs.Signature"
"url": "/pt/java/qr-code-signatures/secure-pdf-signing-qr-code-groupdocs-java/"
"weight": 1
---

# Como implementar assinatura segura de PDF com criptografia de código QR em Java usando GroupDocs.Signature

Na era digital atual, proteger informações confidenciais em documentos é fundamental. O aumento das ameaças cibernéticas tornou a criptografia de dados uma parte essencial do gerenciamento de documentos. Este tutorial orienta você na implementação de assinatura segura de PDF usando criptografia de código QR com o GroupDocs.Signature para Java. Ao final deste artigo, você estará preparado para integrar recursos de segurança robustos aos seus aplicativos.

## O que você aprenderá:
- Compreendendo a criptografia simétrica de dados em Java
- Criando uma classe de assinatura personalizada
- Configurando assinaturas de código QR com dados e alinhamento personalizados
- Integrando GroupDocs.Signature para assinatura segura de PDF

Pronto para começar? Vamos começar!

## Pré-requisitos
Antes de começar, certifique-se de ter o seguinte:
- **Kit de Desenvolvimento Java (JDK):** Versão 8 ou superior.
- **Maven ou Gradle:** Para gerenciamento de dependências. Escolha com base na configuração do seu projeto.
- **Conhecimento de programação Java:** Noções básicas de programação orientada a objetos em Java.

## Configurando GroupDocs.Signature para Java
Para começar a usar o GroupDocs.Signature, você precisará adicioná-lo como uma dependência ao seu projeto. Esta biblioteca oferece ferramentas poderosas para gerenciar assinaturas digitais e criptografia de documentos.

### Configuração do Maven
Adicione a seguinte dependência ao seu `pom.xml` arquivo:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Configuração do Gradle
Para usuários do Gradle, inclua isso em seu `build.gradle` arquivo:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Download direto
Alternativamente, baixe a versão mais recente em [GroupDocs.Signature para versões Java](https://releases.groupdocs.com/signature/java/).

### Aquisição de Licença
Você pode começar com um teste gratuito do GroupDocs.Signature para avaliar seus recursos. Para uso prolongado, considere adquirir uma licença ou solicitar uma licença temporária pelo site.

## Guia de Implementação
Este guia é dividido em seções principais que abrangem criptografia de dados, criação de assinatura personalizada e configuração de assinatura de código QR.

### Criptografia de dados com algoritmo simétrico
Criptografar seus dados garante que eles permaneçam seguros durante a transmissão e o armazenamento. Veja como configurar a criptografia simétrica usando o GroupDocs.Signature:

#### Configurando Criptografia Simétrica
1. **Importar pacotes necessários:**
   ```java
   import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
   ```
2. **Inicialize o objeto de criptografia:**
   Use uma chave segura e sal para criptografia. Substitua `"YOUR_SECURE_KEY"` com suas próprias chaves.
   ```java
   String key = "YOUR_SECURE_KEY";
   String salt = "YOUR_SECURE_SALT";

   IDataEncryption encryption = new SymmetricEncryption(
       SymmetricAlgorithmType.Rijndael, 
       key, 
       salt
   );
   ```
   - **SymmetricAlgorithmType.Rijndael:** Isso especifica o tipo de algoritmo simétrico a ser usado.
   - **Chave e Sal:** Certifique-se de que eles sejam exclusivos e seguros para sua aplicação.

### Classe de Assinatura de Dados Personalizada
Criar uma classe personalizada permite gerenciar propriedades de assinatura com eficiência. Veja como:

#### Definindo o `DocumentSignatureData` Aula
```java
class DocumentSignatureData {
    private String ID;
    private String Author;
    private Date Signed = new Date();
    private BigDecimal DataFactor = new BigDecimal(0.01);

    public String getID() { return ID; }
    public void setID(String value) { ID = value; }

    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }

    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }

    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```
- **ID, Autor, Assinatura:** Esses campos armazenam os metadados da assinatura.
- **Fator de Dados:** Contém um valor numérico relevante para a lógica do seu aplicativo.

### Opções de assinatura de código QR
Os códigos QR oferecem uma maneira compacta de incorporar informações. Configure-os com dados personalizados e criptografia:

#### Configurando assinaturas de código QR
1. **Inicializar `Signature` Objeto:**
   ```java
   import com.groupdocs.signature.Signature;
   
   Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY");
   ```
2. **Configurar opções de código QR:**
   ```java
   import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
   import com.groupdocs.signature.options.sign.QrCodeSignOptions;
   import java.util.UUID;

   DocumentSignatureData documentSignature = new DocumentSignatureData();
   documentSignature.setID(UUID.randomUUID().toString());
   documentSignature.setAuthor(System.getenv("USERNAME"));
   documentSignature.setDataFactor(new BigDecimal("11.22"));

   QrCodeSignOptions options = new QrCodeSignOptions();
   options.setData(documentSignature);
   options.setEncodeType(QrCodeTypes.QR);
   options.setDataEncryption(encryption); // Use o objeto de criptografia
   options.setHeight(100);
   options.setWidth(100);
   options.setVerticalAlignment(com.groupdocs.signature.domain.enums.VerticalAlignment.Bottom);
   options.setHorizontalAlignment(com.groupdocs.signature.domain.enums.HorizontalAlignment.Right);

   import com.groupdocs.signature.domain.Padding;
   Padding padding = new Padding();
   padding.setRight(10);
   padding.setBottom(10);
   options.setMargin(padding);
   ```
   - **Tipo de codificação:** Especifica o formato do código QR.
   - **Alinhamento e Margem:** Personalize como o código QR aparece no documento.

### Exemplo de uso
Para assinar um documento com suas opções configuradas:
```java
signature.sign("YOUR_OUTPUT_DIRECTORY/QRCodeEncryptedObject.pdf\