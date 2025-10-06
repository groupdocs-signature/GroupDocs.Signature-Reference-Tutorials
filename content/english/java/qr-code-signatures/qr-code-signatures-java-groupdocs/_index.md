---
title: "Secure Your Documents&#58; Implement QR Code Signatures in Java Using GroupDocs.Signature"
description: "Learn how to enhance document security by implementing and verifying QR code signatures in Java with GroupDocs.Signature. Follow this step-by-step guide for a secure signing process."
date: "2025-05-08"
weight: 1
url: "/java/qr-code-signatures/qr-code-signatures-java-groupdocs/"
keywords:
- QR Code Signatures
- Document Security in Java
- GroupDocs Signature
type: docs
---
# Secure Your Documents: Implement QR Code Signatures in Java Using GroupDocs.Signature

In today's digital landscape, ensuring the security of documents such as contracts, invoices, or sensitive personal information is crucial. One innovative approach to enhance document security and simplify verification processes is by using QR code signatures. This tutorial will guide you through implementing and verifying QR code signatures for your documents in Java using GroupDocs.Signature.

## What You’ll Learn
- How to sign documents using QR Codes
- Verifying signed documents with QR Codes
- Searching for existing QR Code signatures within a document
- Updating and deleting QR Code signatures from your documents

Let’s set up your environment and get started!

### Prerequisites
Before beginning, ensure you have the following prerequisites:

#### Required Libraries and Dependencies
You'll need GroupDocs.Signature for Java. You can include it via Maven or Gradle, or download it directly.

**Maven**
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

**Direct Download**
Download the latest version from [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/).

#### Environment Setup Requirements
- Ensure you have Java Development Kit (JDK) 8 or higher installed.
- Use an IDE like IntelliJ IDEA, Eclipse, or NetBeans.

#### Knowledge Prerequisites
A basic understanding of Java programming and document processing is beneficial.

## Setting Up GroupDocs.Signature for Java
To use GroupDocs.Signature in your project, follow these steps:
1. **Installation**: Choose between Maven, Gradle, or direct download based on your setup.
2. **License Acquisition**:
   - Start with a free trial available on the [GroupDocs website](https://releases.groupdocs.com/signature/java/).
   - Consider obtaining a temporary license for extended testing and development from [here](https://purchase.groupdocs.com/temporary-license/).
3. **Basic Initialization**: 
    Here’s how to initialize GroupDocs.Signature:

    ```java
    Signature signature = new Signature("YOUR_DOCUMENT_PATH");
    ```

This prepares you for implementing QR Code signatures.

## Implementation Guide

### Sign Document with QR-Code Signature
#### Overview
Signing a document using a QR Code involves embedding a unique code that represents your digital signature. This process secures the document and allows easy verification of its authenticity later on.

##### Step 1: Set Up Your Signing Options
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
**Explanation**: `QrCodeSignOptions` is configured to create a QR Code with specific text and alignment. Adjust the width and height as necessary.

##### Step 2: Customize Signature Appearance
```java
import java.awt.Color;

signOptions.setForeColor(Color.RED); // Set QR code color
com.groupdocs.signature.domain.SignatureFont signatureFont = new com.groupdocs.signature.domain.SignatureFont();
signatureFont.setSize(12);
signatureFont.setFamilyName("Comic Sans MS");
signOptions.setFont(signatureFont);
```
**Explanation**: Customizing the font and color enhances visual identification.

##### Step 3: Sign the Document
```java
import java.util.ArrayList;
import java.util.List;

List<String> signatureIds = new ArrayList<>();
List<com.groupdocs.signature.domain.BaseSignature> signedSignatures = signature.sign("YOUR_OUTPUT_PATH", signOptions).getSucceeded();

for (com.groupdocs.signature.domain.BaseSignature temp : signedSignatures) {
    signatureIds.add(temp.getSignatureId());
}
```
**Explanation**: This step signs the document and stores the signature IDs for future reference.

### Verify Document with QR-Code Signature
#### Overview
Verification ensures that a document has been legitimately signed. Here’s how you can verify a QR Code signature in a document.

##### Step 1: Set Up Verification Options
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();

verifyOptions.setEncodeType(QrCodeTypes.QR);
verifyOptions.setText("John Smith"); // Text to verify
verifyOptions.setAllPages(false); 
verifyOptions.setPageNumber(1);
```
**Explanation**: The verification options specify which QR Code type and text to look for, ensuring the signature matches your expectations.

##### Step 2: Perform Verification
```java
boolean isValid = signature2.verify(verifyOptions).isValid();
System.out.println("Is Signature Valid? " + isValid);
```
**Explanation**: This checks if the document contains a valid QR Code matching your criteria.

### Search Document for QR-Code Signature
#### Overview
Locating existing signatures within a document is sometimes necessary. Here’s how you can search for them using GroupDocs.Signature.

##### Step 1: Configure Search Options
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import com.groupdocs.signature.options.search.QrCodeSearchOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeSearchOptions searchOptions = new QrCodeSearchOptions();
searchOptions.setAllPages(true);
```
**Explanation**: This sets up the tool to scan all pages for QR Code signatures.

##### Step 2: Execute Search
```java
List<QrCodeSignature> signatures = signature2.search(QrCodeSignature.class, searchOptions);

for (QrCodeSignature qrSignature : signatures) {
    System.out.println("Found Signature ID: " + qrSignature.getSignatureId());
}
```
**Explanation**: This retrieves all QR Code signatures found in the document.

### Update Document QR-Code Signature
#### Overview
Updating a signature involves changing its properties, like position or size. Here’s how to do it:

##### Step 1: Prepare Signatures for Update
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.io.ByteArrayOutputStream;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
List<QrCodeSignature> signaturesToUpdate = new ArrayList<>();

// Assuming 'signatures' is a list of QrCodeSignature objects obtained from searching
for (QrCodeSignature qrSignature : signatures) {
    qrSignature.setLeft(qrSignature.getLeft() + 100);
    qrSignature.setTop(qrSignature.getTop() + 100);
    qrSignature.setWidth(200);
    qrSignature.setHeight(50);
    signaturesToUpdate.add(qrSignature);
}
```
**Explanation**: This adjusts the position and size of each signature.

##### Step 2: Update the Document
```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature2.update(outputStream, signaturesToUpdate);
```
**Explanation**: The document is updated with the modified QR Code signatures.

### Delete Document QR-Code Signature by ID
#### Overview
Deleting a signature might be necessary if it’s no longer needed or was added in error. Here's how you can remove it using its unique ID.

##### Step 1: Identify Signatures to Delete
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
**Explanation**: This finds and deletes the QR Code signature by its unique ID.

## Conclusion
This guide has walked you through securing documents using QR code signatures in Java with GroupDocs.Signature. By following these steps, you can ensure your documents are signed securely and verify their authenticity easily.
