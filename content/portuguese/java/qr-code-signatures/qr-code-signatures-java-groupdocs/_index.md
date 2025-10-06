---
"date": "2025-05-08"
"description": "Aprenda a aumentar a segurança de documentos implementando e verificando assinaturas de código QR em Java com o GroupDocs.Signature. Siga este guia passo a passo para um processo de assinatura seguro."
"title": "Proteja seus documentos&#58; implemente assinaturas de código QR em Java usando GroupDocs.Signature"
"url": "/pt/java/qr-code-signatures/qr-code-signatures-java-groupdocs/"
"weight": 1
type: docs
---
# Proteja seus documentos: implemente assinaturas de código QR em Java usando GroupDocs.Signature

No cenário digital atual, garantir a segurança de documentos como contratos, faturas ou informações pessoais sensíveis é crucial. Uma abordagem inovadora para aumentar a segurança de documentos e simplificar os processos de verificação é o uso de assinaturas de código QR. Este tutorial guiará você na implementação e verificação de assinaturas de código QR para seus documentos em Java usando o GroupDocs.Signature.

## O que você aprenderá
- Como assinar documentos usando códigos QR
- Verificação de documentos assinados com códigos QR
- Pesquisando assinaturas de QR Code existentes em um documento
- Atualizando e excluindo assinaturas de QR Code de seus documentos

Vamos configurar seu ambiente e começar!

### Pré-requisitos
Antes de começar, certifique-se de ter os seguintes pré-requisitos:

#### Bibliotecas e dependências necessárias
Você precisará do GroupDocs.Signature para Java. Você pode incluí-lo via Maven ou Gradle, ou baixá-lo diretamente.

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
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Download direto**
Baixe a versão mais recente em [GroupDocs.Signature para versões Java](https://releases.groupdocs.com/signature/java/).

#### Requisitos de configuração do ambiente
- Certifique-se de ter o Java Development Kit (JDK) 8 ou superior instalado.
- Use um IDE como IntelliJ IDEA, Eclipse ou NetBeans.

#### Pré-requisitos de conhecimento
Um conhecimento básico de programação Java e processamento de documentos é benéfico.

## Configurando GroupDocs.Signature para Java
Para usar o GroupDocs.Signature no seu projeto, siga estas etapas:
1. **Instalação**: Escolha entre Maven, Gradle ou download direto com base na sua configuração.
2. **Aquisição de Licença**:
   - Comece com um teste gratuito disponível em [Site do GroupDocs](https://releases.groupdocs.com/signature/java/).
   - Considere obter uma licença temporária para testes e desenvolvimento prolongados de [aqui](https://purchase.groupdocs.com/temporary-license/).
3. **Inicialização básica**: 
    Veja como inicializar GroupDocs.Signature:

    ```java
    Signature signature = new Signature("YOUR_DOCUMENT_PATH");
    ```

Isso prepara você para implementar assinaturas de QR Code.

## Guia de Implementação

### Assinar documento com assinatura de código QR
#### Visão geral
Assinar um documento usando um QR Code envolve a incorporação de um código exclusivo que representa sua assinatura digital. Esse processo protege o documento e permite a fácil verificação de sua autenticidade posteriormente.

##### Etapa 1: configure suas opções de assinatura
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

Signature signature = new Signature("YOUR_DOCUMENT_PATH");
QrCodeSignOptions signOptions = new QrCodeSignOptions("John Smith", com.groupdocs.signature.domain.qrcodes.QrCodeTypes.QR);

signOptions.setVerticalAlignment(VerticalAlignment.Top);
signOptions.setHorizontalAlignment(HorizontalAlignment.Center);
signOptions.setWidth(100);
signOptions.setHeight(40);
```
**Explicação**: `QrCodeSignOptions` está configurado para criar um QR Code com texto e alinhamento específicos. Ajuste a largura e a altura conforme necessário.

##### Etapa 2: personalizar a aparência da assinatura
```java
import java.awt.Color;

signOptions.setForeColor(Color.RED); // Definir cor do código QR
com.groupdocs.signature.domain.SignatureFont signatureFont = new com.groupdocs.signature.domain.SignatureFont();
signatureFont.setSize(12);
signatureFont.setFamilyName("Comic Sans MS");
signOptions.setFont(signatureFont);
```
**Explicação**: Personalizar a fonte e a cor melhora a identificação visual.

##### Etapa 3: Assine o documento
```java
import java.util.ArrayList;
import java.util.List;

List<String> signatureIds = new ArrayList<>();
List<com.groupdocs.signature.domain.BaseSignature> signedSignatures = signature.sign("YOUR_OUTPUT_PATH", signOptions).getSucceeded();

for (com.groupdocs.signature.domain.BaseSignature temp : signedSignatures) {
    signatureIds.add(temp.getSignatureId());
}
```
**Explicação**: Esta etapa assina o documento e armazena as IDs de assinatura para referência futura.

### Verificar documento com assinatura de código QR
#### Visão geral
A verificação garante que um documento foi assinado legitimamente. Veja como verificar uma assinatura de QR Code em um documento.

##### Etapa 1: Configurar opções de verificação
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();

verifyOptions.setEncodeType(QrCodeTypes.QR);
verifyOptions.setText("John Smith"); // Texto para verificar
verifyOptions.setAllPages(false); 
verifyOptions.setPageNumber(1);
```
**Explicação**As opções de verificação especificam qual tipo de QR Code e texto procurar, garantindo que a assinatura corresponda às suas expectativas.

##### Etapa 2: Executar verificação
```java
boolean isValid = signature2.verify(verifyOptions).isValid();
System.out.println("Is Signature Valid? " + isValid);
```
**Explicação**: Isso verifica se o documento contém um QR Code válido que corresponde aos seus critérios.

### Pesquisar documento para assinatura de código QR
#### Visão geral
Às vezes, é necessário localizar assinaturas existentes em um documento. Veja como você pode procurá-las usando GroupDocs.Signature.

##### Etapa 1: Configurar opções de pesquisa
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import com.groupdocs.signature.options.search.QrCodeSearchOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeSearchOptions searchOptions = new QrCodeSearchOptions();
searchOptions.setAllPages(true);
```
**Explicação**: Isso configura a ferramenta para escanear todas as páginas em busca de assinaturas de QR Code.

##### Etapa 2: Executar pesquisa
```java
List<QrCodeSignature> signatures = signature2.search(QrCodeSignature.class, searchOptions);

for (QrCodeSignature qrSignature : signatures) {
    System.out.println("Found Signature ID: " + qrSignature.getSignatureId());
}
```
**Explicação**: Isso recupera todas as assinaturas de QR Code encontradas no documento.

### Atualizar assinatura do código QR do documento
#### Visão geral
Atualizar uma assinatura envolve alterar suas propriedades, como posição ou tamanho. Veja como fazer:

##### Etapa 1: preparar assinaturas para atualização
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.io.ByteArrayOutputStream;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
List<QrCodeSignature> signaturesToUpdate = new ArrayList<>();

// Supondo que 'assinaturas' seja uma lista de objetos QrCodeSignature obtidos da pesquisa
for (QrCodeSignature qrSignature : signatures) {
    qrSignature.setLeft(qrSignature.getLeft() + 100);
    qrSignature.setTop(qrSignature.getTop() + 100);
    qrSignature.setWidth(200);
    qrSignature.setHeight(50);
    signaturesToUpdate.add(qrSignature);
}
```
**Explicação**: Isso ajusta a posição e o tamanho de cada assinatura.

##### Etapa 2: Atualizar o documento
```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature2.update(outputStream, signaturesToUpdate);
```
**Explicação**: O documento é atualizado com as assinaturas do QR Code modificadas.

### Excluir assinatura de código QR do documento por ID
#### Visão geral
Pode ser necessário excluir uma assinatura caso ela não seja mais necessária ou tenha sido adicionada por engano. Veja como você pode removê-la usando seu ID exclusivo.

##### Etapa 1: identificar assinaturas a serem excluídas
```java
import com.groupdocs.signature.domain.SignatureCollection;
import java.util.Arrays;

SignatureCollection signaturesToDelete = signature2.search(QrCodeSignature.class);
Arrays.stream(signaturesToDelete).forEach(signature -> {
    if (signature.getSignatureId().equals("YOUR_SIGNATURE_ID")) {
        signature.delete();
    }
});
```
**Explicação**: Isso localiza e exclui a assinatura do código QR por seu ID exclusivo.

## Conclusão
Este guia orientou você na proteção de documentos usando assinaturas de código QR em Java com o GroupDocs.Signature. Seguindo esses passos, você pode garantir que seus documentos sejam assinados com segurança e verificar sua autenticidade facilmente.