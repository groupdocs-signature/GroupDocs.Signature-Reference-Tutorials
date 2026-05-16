---
title: "Create Data Matrix PDF with HIBC Barcode in Java"
linktitle: "HIBC PDF Signing Java Guide"
description: "Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature for Java. Step‑by‑step guide for healthcare document signing."
keywords:
- create data matrix pdf
- add qr code pdf
- HIBC barcode Java
date: "2026-05-16"
lastmod: "2026-05-16"
weight: 1
url: "/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/"
categories: ["Document Signing", "Healthcare Integration"]
tags: ["java", "pdf-signing", "hibc", "healthcare", "barcode", "pharmaceutical"]
type: docs
schemas:
- type: TechArticle
  headline: Create Data Matrix PDF with HIBC Barcode in Java
  description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  dateModified: '2026-05-16'
  author: GroupDocs
- type: HowTo
  name: Create Data Matrix PDF with HIBC Barcode in Java
  description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  steps:
  - name: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
    text: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
  - name: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
    text: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
  - name: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
    text: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
  - name: '**Apply the signature** to the PDF.'
    text: '**Apply the signature** to the PDF.'
  - name: '**Dispose of resources** to free file handles and avoid memory leaks.'
    text: '**Dispose of resources** to free file handles and avoid memory leaks.'
  - name: '**Import QR‑specific classes**'
    text: '**Import QR‑specific classes**'
  - name: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
    text: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
  - name: '**Sign the document**'
    text: '**Sign the document**'
- type: FAQPage
  questions:
  - question: Can GroupDocs.Signature sign file types other than PDF?
    answer: Yes, it also supports DOCX, XLSX, PPTX, PNG, JPEG, and TIFF with the same
      barcode‑signing API.
  - question: How do I troubleshoot “Invalid barcode content” errors?
    answer: Verify that your HIBC string follows the exact HIBCC syntax, use the online
      validator, and ensure you’re using the correct `QrCodeTypes` constant for the
      chosen format.
  - question: What is the maximum data capacity for each HIBC format?
    answer: QR ≈ 4,296 alphanumeric characters, Aztec ≈ 3,832 numeric / 3,067 alphanumeric,
      Data Matrix ≈ 3,116 numeric / 2,335 alphanumeric. Keep codes under 200 characters
      for optimal scan reliability.
  - question: Is it possible to embed multiple barcode types in one PDF?
    answer: Absolutely. Create separate `QrCodeSignOptions` objects with different
      positions and call `signature.sign()` for each. Just ensure they don’t overlap.
  - question: Do I need an internet connection for signing at runtime?
    answer: No. After the JAR is on the classpath and the license is activated, all
      operations are performed locally.
---
# Create Data Matrix PDF with HIBC Barcode in Java

If you’re building pharmaceutical or healthcare logistics software, you’ve probably hit the wall of paper‑based tracking, lost signatures, and audit nightmares. **Creating a Data Matrix PDF** that embeds a HIBC LIC barcode solves those problems by giving you a tamper‑evident, machine‑readable trail that survives printing, scanning, and regulatory review. In this tutorial you’ll see exactly how to **add QR code PDF** support, as well as Aztec and Data Matrix formats, using GroupDocs.Signature for Java.

## Quick Answers
- **What library handles HIBC barcodes in Java?** GroupDocs.Signature for Java.  
- **Which barcode format is most compact?** Data Matrix – ideal for small labels.  
- **Can I add both QR and Data Matrix to the same PDF?** Yes, just create separate `QrCodeSignOptions`.  
- **Do I need an internet connection at runtime?** No, the library works fully offline after installation.  
- **What Java version is recommended?** Java 11+ for production‑grade performance.

## What is HIBC barcode PDF signing?
The `Signature` class in GroupDocs.Signature for Java represents a PDF document and provides methods to embed HIBC barcodes as digital signatures. By signing a PDF with an HIBC barcode you create a verifiable, tamper‑evident record that can be scanned at any point in the supply chain.

## Why use Data Matrix and QR codes together?
GroupDocs.Signature supports **50+ input and output formats** and can process multi‑hundred‑page PDFs without loading the entire file into memory. Using Data Matrix for dense, small‑area labels and QR for more spacious documents gives you the best balance of readability, data capacity (up to 4,296 characters for QR), and print‑space efficiency.

## Prerequisites
- **JDK 11 or higher** (Java 8 works but Java 11+ is recommended for optimal performance).  
- **IDE** such as IntelliJ IDEA, Eclipse, or VS Code with Java extensions.  
- **Maven or Gradle** for dependency management (examples below).  
- **Sample PDF** (e.g., `sample.pdf`) to test the implementation.  
- **Valid GroupDocs.Signature license** (free trial for development, paid license for production).

## Setting Up GroupDocs.Signature for Java

### Maven Configuration
Add the dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle Configuration
For Gradle projects, add this to your `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Direct Download Option
You can also download the JAR file directly from [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) and add it to your project’s classpath manually. This approach works well in restricted‑network environments.

### Getting a License
Request a free trial or temporary license from GroupDocs to remove watermarks and unlock all features. Production deployments require a purchased license.

### Basic Initialization
The `Signature` class is the entry point for all signing operations. It loads the PDF, applies the barcode, and writes the signed file.

```java
import com.groupdocs.signature.Signature;

class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("sample.pdf");
        // Proceed with signing operations...
    }
}
```

## How to create a Data Matrix PDF with HIBC barcode?
Load your source PDF, configure a `QrCodeSignOptions` object for the Data Matrix format, and call `sign()` – that’s all you need to embed a compliant HIBC Data Matrix barcode. The following steps walk you through the exact code required. `QrCodeSignOptions` defines the settings for a barcode signature, such as type, content, size, and position.

1. **Import the required classes** – these give you access to the signature engine and Data Matrix options.  

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
```

2. **Instantiate the `Signature` object** with absolute paths for source and destination files.  

```java
String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY";
String destinFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithHIBCLICQR.pdf";

final Signature signature = new Signature(sourceFilePath);
```

3. **Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`, and define placement coordinates. `QrCodeTypes` enumerates the supported barcode formats for HIBC signatures.  

```java
QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR);
hibcLic_QR.setLeft(1); // Set the position from left
hibcLic_QR.setTop(1);   // Set the position from top
hibcLic_QR.setReturnContent(true); // Return content after signing
hibcLic_QR.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

4. **Apply the signature** to the PDF.  

```java
signature.sign(destinFilePath, hibcLic_QR);
```

5. **Dispose of resources** to free file handles and avoid memory leaks.  

```java
finally {
    if (signature != null) signature.dispose();
}
```

### Complete working example
Here’s the full flow in a single block (the placeholders represent the exact code you’ll paste from the earlier snippets):

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;

public class HibcQrSigning {
    public static void main(String[] args) {
        String sourceFilePath = "sample.pdf";
        String destinFilePath = "output/SignWithHIBCLICQR.pdf";
        
        Signature signature = null;
        try {
            signature = new Signature(sourceFilePath);
            
            QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions(
                "A123PROD30917/75#422011907#GP293", 
                QrCodeTypes.HIBCLICQR
            );
            hibcLic_QR.setLeft(1);
            hibcLic_QR.setTop(1);
            hibcLic_QR.setReturnContent(true);
            hibcLic_QR.setReturnContentType(FileType.PNG);
            
            signature.sign(destinFilePath, hibcLic_QR);
            System.out.println("PDF signed successfully with HIBC QR code");
            
        } catch (Exception e) {
            System.err.println("Error signing PDF: " + e.getMessage());
            e.printStackTrace();
        } finally {
            if (signature != null) signature.dispose();
        }
    }
}
```

#### Direct answer (40–70 words)
To **create a Data Matrix PDF**, instantiate `Signature` with your source PDF, set `QrCodeSignOptions` to `QrCodeTypes.HIBCLICDataMatrix` and provide a correctly formatted HIBC string, then call `signature.sign(outputPath, options)`. The library writes the signed PDF to the destination, preserving layout and embedding the barcode as a tamper‑evident signature.

## How to add QR code PDF using GroupDocs.Signature?
Load the PDF, configure `QrCodeSignOptions` for the QR format, and invoke `sign()`. This two‑line pattern works for any PDF size and automatically scales the QR image for optimal readability. `QrCodeSignOptions` configures the QR barcode signature, including its content and visual properties. It positions the code based on the coordinates you set, ensuring it does not overlap existing content and remains scannable after printing.

1. **Import QR‑specific classes**  

```java
QrCodeSignOptions hibcLic_AZ = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec);
hibcLic_AZ.setLeft(1); // Set the position from left
hibcLic_AZ.setTop(200); // Set the position from top
hibcLic_AZ.setReturnContent(true); // Return content after signing
hibcLic_AZ.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

2. **Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.  

```java
signature.sign(destinFilePath, hibcLic_AZ);
```

3. **Sign the document**  

```java
QrCodeSignOptions hibcLic_DM = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix);
hibcLic_DM.setLeft(1); // Set the position from left
hibcLic_DM.setTop(400); // Set the position from top
hibcLic_DM.setReturnContent(true); // Return content after signing
hibcLic_DM.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

> **Direct answer:** Use `QrCodeTypes.HIBCLICQR` in `QrCodeSignOptions`, set the HIBC content string, position the code with `setLeft()` and `setTop()`, then call `signature.sign(outputPath, options)`. The QR barcode is embedded instantly, ready for smartphone or scanner capture.

## Common Mistakes to Avoid

### 1. Forgetting Resource Disposal
**Wrong:**  
```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  

**Fix:** Wrap the `Signature` usage in a try‑with‑resources block or explicitly call `close()` in a finally clause.

### 2. Using Incorrect HIBC Format Strings
**Wrong:** Using generic strings like “12345”.  
**Fix:** Follow the HIBCC standard (e.g., `A123PROD30917/75#422011907#GP293`). Validate with the [HIBCC online validator](https://www.hibcc.org/).

### 3. Hard‑coding File Paths
**Wrong:**  
```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  

**Fix:** Store paths in a configuration file or environment variable and read them at runtime.

### 4. Ignoring Barcode Position Conflicts
Place barcodes away from existing text or signatures. Use PDF coordinates (origin is bottom‑left) and test with a printed sample.

### 5. Not Testing with Real Scanners
Print the signed PDF and scan it with the exact hardware used in your workflow. Verify readability at different print qualities.

## Practical Applications in Healthcare

| Scenario | Recommended Barcode | Why it fits |
|----------|--------------------|--------------|
| **Pharmaceutical distribution** | QR Code | High data capacity, widely scanned by smartphones. |
| **Inventory management** | Data Matrix | Small footprint, ideal for dense shelf labels. |
| **Regulatory compliance (FDA 21 CFR Part 11)** | QR + Data Matrix | Dual‑format provides redundancy and auditability. |
| **Medical device tracking** | Aztec Code | Compact size works on limited‑space packaging. |

## Performance Considerations and Best Practices

### Batch Processing Pattern
```java
List<String> filesToSign = getFileList();
for (String filePath : filesToSign) {
    Signature signature = null;
    try {
        signature = new Signature(filePath);
        // Sign and save
    } finally {
        if (signature != null) signature.dispose();
    }
}
```

- Create a new `Signature` instance per file to keep memory usage low.  
- Use a fixed thread pool (`Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() - 1)`) for parallel processing, but monitor heap size because each `Signature` holds the full PDF in memory.  

### Keep Libraries Updated
GroupDocs releases improve processing speed by up to **20 %** and add new HIBC compliance features. Schedule quarterly dependency checks.

### Caching Templates
Load a PDF template once, clone it for each barcode variant, and sign the clones. This reduces I/O and speeds up high‑volume workflows.

## Frequently Asked Questions

**Q: Can GroupDocs.Signature sign file types other than PDF?**  
A: Yes, it also supports DOCX, XLSX, PPTX, PNG, JPEG, and TIFF with the same barcode‑signing API.

**Q: How do I troubleshoot “Invalid barcode content” errors?**  
A: Verify that your HIBC string follows the exact HIBCC syntax, use the online validator, and ensure you’re using the correct `QrCodeTypes` constant for the chosen format.

**Q: What is the maximum data capacity for each HIBC format?**  
A: QR ≈ 4,296 alphanumeric characters, Aztec ≈ 3,832 numeric / 3,067 alphanumeric, Data Matrix ≈ 3,116 numeric / 2,335 alphanumeric. Keep codes under 200 characters for optimal scan reliability.

**Q: Is it possible to embed multiple barcode types in one PDF?**  
A: Absolutely. Create separate `QrCodeSignOptions` objects with different positions and call `signature.sign()` for each. Just ensure they don’t overlap.

**Q: Do I need an internet connection for signing at runtime?**  
A: No. After the JAR is on the classpath and the license is activated, all operations are performed locally.

## Additional Resources

- [GroupDocs.Signature for Java Documentation](https://docs.groupdocs.com/signature/java/)  
- [API Reference Guide](https://reference.groupdocs.com/signature/java/)  
- [Latest Release Downloads](https://releases.groupdocs.com/signature/java/)  
- [Purchase License](https://purchase.groupdocs.com/buy)  
- [Get Free Trial](https://releases.groupdocs.com/signature/java/)  
- [Request Temporary License](https://purchase.groupdocs.com/temporary-license/)  
- [GroupDocs Forum](https://forum.groupdocs.com/c/signature/)

---

**Last Updated:** 2026-05-16  
**Tested With:** GroupDocs.Signature 23.12 for Java  
**Author:** GroupDocs  

---

```java
signature.sign(destinFilePath, hibcLic_DM);
```

## Related Tutorials

- [Create Barcode Signature PDF in Java – GroupDocs Guide](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)
- [Create Barcode Signature in Java – Update PDF Barcodes](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [How to read QR code PDF using Java and GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)
