---
"date": "2025-05-08"
"description": "Aprenda a assinar imagens DICOM com segurança usando o GroupDocs.Signature para Java. Aumente a segurança dos documentos incorporando códigos QR e metadados."
"title": "Assine imagens DICOM com códigos QR e metadados usando GroupDocs.Signature para Java"
"url": "/pt/java/image-signatures/sign-dicom-images-groupdocs-signature-java/"
"weight": 1
---

# Como assinar imagens DICOM com códigos QR e metadados usando GroupDocs.Signature para Java

## Introdução

No cenário da saúde digital em rápida evolução, gerenciar os dados dos pacientes com segurança é fundamental. Este tutorial orienta você na implementação de uma solução robusta usando o GroupDocs.Signature para Java para assinar imagens DICOM (Digital Imaging and Communications in Medicine) com códigos QR e metadados. Esses recursos garantem autenticidade, aprimoram a rastreabilidade e mantêm a conformidade, incorporando informações vitais diretamente nas imagens médicas.

### O que você aprenderá:
- Como integrar o GroupDocs.Signature para Java ao seu projeto.
- processo de assinatura de imagens DICOM com códigos QR.
- Adicionar metadados XMP para aumentar a segurança dos documentos.
- Recuperar, verificar e pesquisar assinaturas em arquivos DICOM.
- Gerando visualizações de imagens DICOM assinadas.

Vamos lá! Antes de começar, vamos garantir que você tenha tudo o que precisa para acompanhar tudo sem problemas.

## Pré-requisitos

Para implementar os recursos do GroupDocs.Signature de forma eficaz, certifique-se de atender aos seguintes pré-requisitos:

### Bibliotecas e dependências necessárias
- **GroupDocs.Signature para Java**: Você precisará da versão 23.12 ou posterior desta biblioteca.

### Requisitos de configuração do ambiente
- **Kit de Desenvolvimento Java (JDK)**: Certifique-se de que o JDK esteja instalado no seu sistema.
- **IDE**: Use um ambiente de desenvolvimento integrado como IntelliJ IDEA ou Eclipse.

### Pré-requisitos de conhecimento
Uma compreensão básica de:
- Programação Java e princípios orientados a objetos.
- Ferramentas de construção Maven ou Gradle para gerenciamento de dependências.

## Configurando GroupDocs.Signature para Java

Para começar a usar o GroupDocs.Signature, você precisa adicioná-lo como uma dependência no seu projeto. Veja como fazer isso usando diferentes ferramentas de compilação:

### Especialista
Adicione o seguinte trecho ao seu `pom.xml` arquivo:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle
Inclua isso em seu `build.gradle` arquivo:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Download direto
Alternativamente, você pode baixar a versão mais recente em [GroupDocs.Signature para versões Java](https://releases.groupdocs.com/signature/java/).

#### Etapas de aquisição de licença
1. **Teste grátis**: Teste os recursos com um teste gratuito por tempo limitado.
2. **Licença Temporária**Obtenha uma licença temporária para explorar todos os recursos.
3. **Comprar**: Compre uma assinatura se precisar de acesso de longo prazo.

#### Inicialização e configuração básicas

Para inicializar GroupDocs.Signature, crie uma instância do `Signature` aula:
```java
import com.groupdocs.signature.Signature;

// Inicialize o objeto de assinatura com o caminho para seu arquivo DICOM
Signature signature = new Signature(filePath);
```

## Guia de Implementação

### Assinando uma imagem DICOM com código QR e metadados

#### Visão geral
Este recurso permite que você assine imagens DICOM com um código QR e adicione metadados XMP, aumentando a segurança do documento.

#### Etapa 1: Configurar opções de assinatura de código QR
```java
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.QrCodeSignOptions;

Padding padding = new Padding();
padding.setRight(5);
padding.setLeft(5);

QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues");
options.setAllPages(true);
options.setWidth(100);
options.setHeight(100);
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
options.setMargin(padding);
```
Aqui, configuramos a aparência e a posição do código QR na imagem DICOM.

#### Etapa 2: adicionar metadados XMP
```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomSaveOptions;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpEntry;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpType;

DicomSaveOptions dicomSaveOptions = new DicomSaveOptions();
List<DicomXmpEntry> xmpEntries = new ArrayList<>();
xmpEntries.add(new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4"));
dicomSaveOptions.setXmpEntries(xmpEntries);
```
Este snippet adiciona metadados ao arquivo DICOM, incorporando informações adicionais do paciente.

#### Etapa 3: Assine o documento
```java
String outputFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/" + fileName;
signature.sign(outputFilePath, options, dicomSaveOptions);
```
O `sign` O método grava o código QR e os metadados no seu arquivo DICOM, salvando-o no local especificado.

### Recuperando informações de imagem DICOM assinada

#### Visão geral
Extraia metadados XMP de uma imagem DICOM assinada para fins de verificação ou auditoria.
```java
import com.groupdocs.signature.domain.IDocumentInfo;
import com.groupdocs.signature.domain.signatures.MetadataSignature;

IDocumentInfo documentInfo = signature.getDocumentInfo();
for (MetadataSignature item : documentInfo.getMetadataSignatures()) {
    System.out.println(item.toString());
}
```
Este código recupera e imprime todas as assinaturas de metadados associadas ao arquivo DICOM.

### Verificando DICOM assinado

#### Visão geral
Verifique se uma assinatura de código QR está presente na imagem DICOM assinada para confirmar sua autenticidade.
```java
import com.groupdocs.signature.domain.VerificationResult;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;
import com.groupdocs.signature.domain.enums.TextMatchType;

QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();
verifyOptions.setAllPages(true);
verifyOptions.setText("Patient #36363393");
verifyOptions.setMatchType(TextMatchType.Contains);

VerificationResult result = signature.verify(verifyOptions);
if (result.isValid()) {
    System.out.println(filePath + " has successfully verified signatures!");
} else {
    System.out.println(filePath + " failed verification process.");
}
```
Esta etapa de verificação garante que o código QR corresponda aos critérios esperados, confirmando a integridade do documento.

### Procurando assinaturas em DICOM assinado

#### Visão geral
Localize todas as assinaturas de código QR em uma imagem DICOM assinada para revisá-las ou auditá-las.
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.util.List;

List<QrCodeSignature> signatures = signature.search(QrCodeSignature.class);
for (QrCodeSignature qrCodeSignature : signatures) {
    System.out.println("QRCode signature found at page " +
        qrCodeSignature.getPageNumber() + ": " +
        qrCodeSignature.getEncodeType().getTypeName() + ": " +
        qrCodeSignature.getText());
}
```
Esse recurso é útil para escanear todas as assinaturas de código QR no documento, fornecendo visibilidade abrangente.

### Gerando visualização do DICOM assinado

#### Visão geral
Crie visualizações para cada página de uma imagem DICOM assinada, permitindo uma inspeção visual rápida sem abrir o arquivo inteiro.
```java
import com.groupdocs.signature.options.PreviewOptions;
import java.io.File;
import java.io.FileOutputStream;
import java.nio.file.Paths;

PreviewOptions previewOption = new PreviewOptions(pageNumber -> {
    try {
        String pageFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/image-" + pageNumber + ".jpg";
        return new FileOutputStream(Paths.get(pageFilePath).toFile());
    } catch (Exception e) {
        throw new RuntimeException(e.getMessage());
    }
});

signature.generatePreview(previewOption);
```
Este snippet gera pré-visualizações de imagens para cada página, o que pode ser útil para verificação ou compartilhamento rápido.

## Aplicações práticas

O GroupDocs.Signature para Java oferece diversas aplicações reais:
- **Imagem Médica**: Assine e gerencie com segurança imagens DICOM de pacientes com códigos QR e metadados.
- **Gestão de Documentos Legais**: Aumentar a autenticidade e a conformidade dos documentos em processos judiciais.
- **Serviços Financeiros**: Implementar assinaturas eletrônicas seguras em documentos financeiros confidenciais.