---
title: "Sign DICOM Images with QR Codes and Metadata Using GroupDocs.Signature for Java"
description: "Learn how to securely sign DICOM images using GroupDocs.Signature for Java. Enhance document security by embedding QR codes and metadata."
date: "2025-05-08"
weight: 1
url: "/java/image-signatures/sign-dicom-images-groupdocs-signature-java/"
keywords:
- sign DICOM images
- GroupDocs.Signature for Java
- QR code signature
type: docs
---
# How to Sign DICOM Images with QR Codes and Metadata Using GroupDocs.Signature for Java

## Introduction

In the rapidly evolving digital healthcare landscape, managing patient data securely is paramount. This tutorial guides you through implementing a robust solution using GroupDocs.Signature for Java to sign Digital Imaging and Communications in Medicine (DICOM) images with QR codes and metadata. These features ensure authenticity, enhance traceability, and maintain compliance by embedding vital information directly into medical images.

### What You'll Learn:
- How to integrate GroupDocs.Signature for Java into your project.
- The process of signing DICOM images with QR codes.
- Adding XMP metadata to enhance document security.
- Retrieving, verifying, and searching for signatures within DICOM files.
- Generating previews of signed DICOM images.

Let's dive in! Before we begin, let’s ensure you have everything needed to follow along seamlessly.

## Prerequisites

To implement the GroupDocs.Signature features effectively, make sure you meet the following prerequisites:

### Required Libraries and Dependencies
- **GroupDocs.Signature for Java**: You'll need version 23.12 or later of this library.

### Environment Setup Requirements
- **Java Development Kit (JDK)**: Ensure JDK is installed on your system.
- **IDE**: Use an Integrated Development Environment like IntelliJ IDEA or Eclipse.

### Knowledge Prerequisites
A basic understanding of:
- Java programming and object-oriented principles.
- Maven or Gradle build tools for dependency management.

## Setting Up GroupDocs.Signature for Java

To get started with GroupDocs.Signature, you need to add it as a dependency in your project. Here’s how you can do this using different build tools:

### Maven
Add the following snippet to your `pom.xml` file:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle
Include this in your `build.gradle` file:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Direct Download
Alternatively, you can download the latest version from [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/).

#### License Acquisition Steps
1. **Free Trial**: Test out the features with a limited-time free trial.
2. **Temporary License**: Obtain a temporary license to explore full capabilities.
3. **Purchase**: Buy a subscription if you need long-term access.

#### Basic Initialization and Setup

To initialize GroupDocs.Signature, create an instance of the `Signature` class:
```java
import com.groupdocs.signature.Signature;

// Initialize signature object with the path to your DICOM file
Signature signature = new Signature(filePath);
```

## Implementation Guide

### Signing a DICOM Image with QR Code and Metadata

#### Overview
This feature allows you to sign DICOM images with a QR code and add XMP metadata, enhancing document security.

#### Step 1: Set Up QR Code Sign Options
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
Here, we configure the QR code's appearance and position on the DICOM image.

#### Step 2: Add XMP Metadata
```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomSaveOptions;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpEntry;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpType;

DicomSaveOptions dicomSaveOptions = new DicomSaveOptions();
List<DicomXmpEntry> xmpEntries = new ArrayList<>();
xmpEntries.add(new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4"));
dicomSaveOptions.setXmpEntries(xmpEntries);
```
This snippet adds metadata to the DICOM file, embedding additional patient information.

#### Step 3: Sign the Document
```java
String outputFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/" + fileName;
signature.sign(outputFilePath, options, dicomSaveOptions);
```
The `sign` method writes the QR code and metadata into your DICOM file, saving it to the specified location.

### Retrieving Signed DICOM Image Info

#### Overview
Extract XMP metadata from a signed DICOM image for verification or audit purposes.
```java
import com.groupdocs.signature.domain.IDocumentInfo;
import com.groupdocs.signature.domain.signatures.MetadataSignature;

IDocumentInfo documentInfo = signature.getDocumentInfo();
for (MetadataSignature item : documentInfo.getMetadataSignatures()) {
    System.out.println(item.toString());
}
```
This code retrieves and prints all metadata signatures associated with the DICOM file.

### Verifying Signed DICOM

#### Overview
Verify that a QR code signature is present in the signed DICOM image to confirm its authenticity.
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
This verification step ensures that the QR code matches expected criteria, confirming document integrity.

### Searching for Signatures in Signed DICOM

#### Overview
Locate all QR code signatures within a signed DICOM image to review or audit them.
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
This feature is useful for scanning all QR code signatures within the document, providing comprehensive visibility.

### Generating Preview of Signed DICOM

#### Overview
Create previews for each page of a signed DICOM image, allowing quick visual inspection without opening the entire file.
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
This snippet generates image previews for each page, which can be useful for quick verification or sharing.

## Practical Applications

GroupDocs.Signature for Java offers several real-world applications:
- **Medical Imaging**: Securely sign and manage patient DICOM images with QR codes and metadata.
- **Legal Document Management**: Enhance document authenticity and compliance in legal proceedings.
- **Financial Services**: Implement secure electronic signatures on sensitive financial documents.
