---
title: "How to Sign Documents with QR Code in Java"
linktitle: "Sign Documents with QR Code Java"
description: "Learn how to sign documents with QR codes in Java using GroupDocs.Signature. Add secure, scannable QR signatures to PDFs with HIBC data encoding in minutes."
keywords: "sign documents with QR code Java, Java QR code document signing, add QR code to PDF Java, digital signature QR code Java, GroupDocs.Signature for Java"
date: "2025-01-02"
lastmod: "2025-01-02"
weight: 1
url: "/java/qr-code-signatures/groupdocs-signature-qr-code-document-signing/"
categories: ["Document Signing"]
tags: ["java", "qr-code", "digital-signatures", "pdf", "groupdocs"]
type: docs
---

# How to Sign Documents with QR Code in Java

## Introduction

Ever needed to add a QR code signature to a document that does more than just look official? You're not alone. Traditional digital signatures are great, but what if your signature could encode rich product data, manufacturing details, or compliance information that anyone can scan and verify instantly?

That's exactly what we'll tackle in this guide. If you're working in healthcare, pharmaceuticals, supply chain management—or really any industry where document traceability matters—you'll learn how to sign documents with QR codes in Java using GroupDocs.Signature. We'll specifically focus on encoding HIBC (Health Industry Bar Code) data, but these techniques work for any structured data you need to embed.

**Here's what you'll walk away with:**
- A working implementation for adding QR code signatures to documents
- Understanding of how to encode complex data structures (like HIBC) within QR codes
- Practical knowledge of when and why to use QR signatures vs traditional digital signatures
- Performance optimization tips for production environments

Whether you're building a pharmaceutical compliance system or just need a better way to embed verification data in your documents, this tutorial has you covered. Let's dive in.

## Why Use QR Codes for Document Signatures?

Before we get into the code, let's talk about why you'd choose QR code signatures in the first place. Traditional digital signatures are excellent for authentication and tamper-detection, but they're essentially black boxes—you can't easily extract information from them without specialized software.

**QR code signatures give you three key advantages:**

1. **Instant Verification**: Anyone with a smartphone can scan the QR code and verify document details on the spot. No special software required—just open the camera app.

2. **Rich Data Embedding**: You can encode product information, manufacturing dates, batch numbers, expiration dates, and more. This is huge for industries like pharmaceuticals where traceability isn't optional.

3. **Dual-Purpose Functionality**: Your signature doesn't just authenticate the document—it also serves as a data carrier. One element doing two jobs means cleaner documents and better user experience.

**Common use cases you'll see in the wild:**
- Pharmaceutical packaging documents with product and compliance data
- Supply chain documentation with tracking and origin information
- Healthcare records with patient safety information
- Quality assurance certificates with inspection details
- Invoices with payment verification data

The HIBC standard we'll use in this tutorial is specifically designed for healthcare and pharmaceutical products, but the principles apply to any scenario where you need verifiable, scannable document signatures.

## Prerequisites

### Required Libraries and Dependencies

To sign documents with QR codes in Java, you'll need:

- **Java Development Kit (JDK)**: Version 8 or higher (though 11+ is recommended for better performance)
- **Maven** or **Gradle**: For dependency management (examples provided for both)
- **GroupDocs.Signature for Java**: The library that makes all this possible

### Environment Setup Requirements

Make sure your IDE (IntelliJ IDEA, Eclipse, or VS Code with Java extensions) is configured properly. If you can compile and run a basic "Hello World" Java application, you're good to go.

You'll also want write permissions to your file system for saving signed documents—sounds obvious, but it's easy to overlook when testing.

### Knowledge Prerequisites

This tutorial assumes you're comfortable with:
- Basic Java syntax and object-oriented programming concepts
- Working with external libraries (if you've added a dependency before, you're fine)
- File I/O operations in Java

You don't need prior experience with digital signatures or QR codes—we'll explain everything as we go.

## Setting Up GroupDocs.Signature for Java

### Installation Information

Getting GroupDocs.Signature into your project is straightforward. Choose the build tool you're using:

**Maven Users** - Add this to your `pom.xml`:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle Users** - Add this to your `build.gradle`:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Direct Download Option**: If you prefer manual JAR management (or your organization requires it), download the latest version from [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) and add it to your classpath.

*Pro tip: Check for newer versions than 23.12—the library receives regular updates with performance improvements and new features.*

### License Acquisition Steps

GroupDocs.Signature isn't free, but you have options:

1. **Free Trial**: Perfect for testing and development. Download from the releases page to try basic functionalities without commitment.

2. **Temporary License**: Need full access for evaluation? Request a temporary license that removes limitations for 30 days. Great for proof-of-concept work.

3. **Full License**: For production deployments. Purchase options are flexible based on your needs (developer licenses, site licenses, etc.).

The trial version will add watermarks to your output—totally fine for development, but you'll want a proper license before going live.

### Basic Initialization and Setup

Here's the simplest possible initialization (we'll build on this throughout the tutorial):

```java
String filePath = "Sample.pdf";
Signature signature = new Signature(filePath);
```

That's it. The `Signature` object is your main entry point for all signing operations. It handles the heavy lifting of document parsing, signature generation, and file output.

**Important resource management note**: Always dispose of the `Signature` object when you're done. We'll use try-finally blocks throughout to ensure cleanup happens even if exceptions occur. Memory leaks are no fun, especially in production environments.

## Understanding HIBC Data Structures

Before we write code to sign documents with QR codes, let's quickly understand what HIBC data actually is. If you're not in healthcare/pharma, don't skip this section—the pattern applies to any complex data you need to encode.

HIBC (Health Industry Bar Code) is a standard for encoding product information in the healthcare industry. It uses a two-tier structure:

**Primary Data** = Core product identification (what it is, who made it)
**Secondary Data** = Lifecycle information (when it expires, batch numbers, quantities)

Think of it like a passport: primary data is your name and nationality (doesn't change), secondary data is your entry stamps and visa details (specific to use).

Why split it up? Because you might need to encode just primary data in some contexts (like product catalogs) and combined data in others (like batch-specific shipping documents). The flexibility is built into the standard.

For QR code signatures, we'll typically use the combined format because it gives us complete traceability. But understanding the structure helps you adapt this to your specific needs.

## Implementation Guide: Creating and Signing Documents

### Create HIBC LIC Primary Data

**What you're doing here**: Setting up the core product identification that never changes for a specific product. This is like the product's DNA.

#### Step 1: Initialize Primary Data Object

```java
HIBCLICPrimaryData primaryData = new HIBCLICPrimaryData();
```

Simple start. This creates an empty container for your primary product data.

#### Step 2: Set Essential Properties

Now here's where it gets interesting. You need three key pieces of information:

```java
primaryData.setProductOrCatalogNumber("12345");
primaryData.setLabelerIdentificationCode("A999");
primaryData.setUnitOfMeasureID(1);
```

**Let's break down what each property actually means:**

- **Product or Catalog Number**: This is your unique identifier for the product. Could be an internal SKU, a manufacturer part number, whatever makes sense for your system. Keep it alphanumeric and under 18 characters for HIBC compliance.

- **Labeler Identification Code (LIC)**: This identifies who manufactured or distributed the product. In the US, this is typically assigned by HIBCC (Health Industry Business Communications Council). If you're testing, any 4-character alphanumeric code works—but use real codes in production.

- **Unit of Measure ID**: Tells you what unit the product quantity refers to. The code `1` typically means "single unit," but HIBC has specific codes for boxes, cases, doses, etc. Check the HIBC standard documentation for the complete list.

**Common mistake to avoid**: Don't use special characters in the product number. HIBC is designed for barcode scanners, which can choke on symbols like `@`, `#`, or `%`. Stick to letters and numbers.

### Create HIBC LIC Secondary Additional Data

**What you're doing here**: Adding the time-sensitive, batch-specific information that changes with each production run.

#### Step 1: Initialize Secondary Data Object

```java
HIBCLICSecondaryAdditionalData secondaryData = new HIBCLICSecondaryAdditionalData();
```

Again, starting with an empty container. This will hold all the lifecycle data.

#### Step 2: Set Additional Properties

Here's where you encode the details that matter for tracking and compliance:

```java
secondaryData.setExpiryDate(new Date());
secondaryData.setExpiryDateFormat(HIBCLICDateFormat.MMDDYY);
secondaryData.setQuantity(30);
secondaryData.setLotNumber("LOT123");
secondaryData.setSerialNumber("SERIAL123");
secondaryData.setDateOfManufacture(new Date());
secondaryData.setLinkCharacter('S');
```

**What each property does in the real world:**

- **Expiry Date**: Critical for pharmaceuticals. Use `new Date()` here for demo purposes, but in production you'd calculate this based on manufacturing date plus shelf life. The library handles the date encoding for you.

- **Expiry Date Format**: HIBC supports several date formats. `MMDDYY` is common in the US, but there's also `YYMMDD`, `YYMMDDHH`, and others. Choose based on your regional requirements and precision needs.

- **Quantity**: How many units in this batch? Seems simple, but this is crucial for inventory reconciliation. If your QR code says 30 units but only 28 arrive, you know something went wrong.

- **Lot Number**: Your internal batch tracking ID. This is how you trace back to specific production runs if there's a quality issue. Make it meaningful—include dates or facility codes if that helps your tracking.

- **Serial Number**: Unit-level tracking. Not always necessary (depends on your product type), but invaluable for high-value items or when you need to track individual units through their lifecycle.

- **Date of Manufacture**: When this batch was produced. Combined with lot numbers, this gives you complete production traceability.

- **Link Character**: This is a technical HIBC requirement that tells scanners how primary and secondary data connect. `'S'` means "supplemental data follows." You typically won't change this unless you're doing advanced HIBC implementations.

**Real-world tip**: In production, you'd pull most of these values from a database or manufacturing execution system (MES). The pattern would look like:

```java
// Pseudo-code showing real-world usage
Product product = productService.getById(productId);
Batch batch = batchService.getCurrentBatch(productId);

secondaryData.setExpiryDate(batch.getManufactureDate().plusMonths(product.getShelfLifeMonths()));
secondaryData.setLotNumber(batch.getLotNumber());
// etc...
```

### Combine HIBC LIC Primary and Secondary Data

**Why combine them**: QR codes have size limits. By using the HIBC combined format, you get optimized encoding that includes both primary and secondary data while staying within QR code capacity constraints.

#### Step 1: Initialize Combined Data Object

```java
HIBCLICCombinedData combinedData = new HIBCLICCombinedData();
```

This is your final container that merges everything together.

#### Step 2: Link Primary and Secondary Data

```java
combinedData.setPrimaryData(primaryData);
combinedData.setSecondaryAdditionalData(secondaryData);
```

This might look simple, but there's magic happening under the hood. The library validates that your primary and secondary data structures are compatible, then encodes them using the HIBC combined format specification. This ensures any HIBC-compliant scanner can read your QR code correctly.

**Performance note**: The encoding happens when you actually generate the QR code (next section), not here. These setter calls just reference your data objects, so there's no performance penalty for setting up complex data structures.

### Sign Document with QR Code Containing HIBC LIC Combined Data

**The payoff**: Everything we've built up to now comes together here. You're about to create a signed document with a scannable QR code containing all your product and compliance data.

#### Step 1: Define File Paths

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/Sample.pdf";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithQRCodeHIBCLICCombinedData/" + fileName;
```

**What to actually put here**: Replace `YOUR_DOCUMENT_DIRECTORY` and `YOUR_OUTPUT_DIRECTORY` with real paths. The library doesn't create directories for you, so make sure the output path exists before running this code.

In production, you'd typically have these paths in configuration files or environment variables rather than hardcoded. Something like:

```java
String filePath = config.getDocumentPath() + "/" + documentId + ".pdf";
String outputPath = config.getOutputPath() + "/signed/" + generateUniqueFileName();
```

#### Step 2: Configure and Apply QR Code Signature

Here's where the actual signing happens:

```java
Signature signature = new Signature(filePath);
try {
    QrCodeSignOptions options = new QrCodeSignOptions();
    options.setEncodeType(QrCodeTypes.HIBCLICQR);
    options.setData(combinedData);

    // Sign and save document
    signature.sign(outputFilePath, options);
} finally {
    if (signature != null) signature.dispose();
}
```

**Let's unpack what's happening here:**

- **QrCodeSignOptions**: This object configures how your QR code looks and behaves. We're using defaults for positioning and size (centered on the page), but you can customize these with methods like `setLeft()`, `setTop()`, `setWidth()`, and `setHeight()`.

- **setEncodeType**: This tells the library to use HIBC LIC QR encoding. There are dozens of other QR types available (Aztec, DataMatrix, etc.), but `HIBCLICQR` is specifically optimized for healthcare data.

- **setData**: Here's where you pass in your combined data object. The library handles all the HIBC encoding complexity—checksums, data formatting, structure validation—automatically.

- **signature.sign()**: This is the money line. It reads your input document, generates the QR code with your encoded data, applies it as a signature, and writes the result to your output path. All in one call.

**The try-finally pattern**: This ensures `signature.dispose()` always runs, even if an exception occurs. GroupDocs.Signature holds file handles and memory buffers that need proper cleanup. Skipping disposal can cause file locks and memory leaks that'll haunt you in production.

**What if you need multiple QR codes?** Just call `sign()` with different options:

```java
QrCodeSignOptions options1 = new QrCodeSignOptions();
options1.setEncodeType(QrCodeTypes.HIBCLICQR);
options1.setData(productData);
options1.setLeft(50);
options1.setTop(50);

QrCodeSignOptions options2 = new QrCodeSignOptions();
options2.setEncodeType(QrCodeTypes.HIBCLICQR);
options2.setData(batchData);
options2.setLeft(50);
options2.setTop(200);

signature.sign(outputFilePath, options1, options2);
```

Each QR code gets positioned independently, and they're all applied in a single operation.

## Practical Applications Beyond Pharmaceuticals

While we've focused on HIBC and pharmaceutical use cases, signing documents with QR codes in Java has applications across many industries:

**Supply Chain and Logistics**:
- Encode shipping manifests with origin, destination, and tracking data
- Add packing list details directly to bills of lading
- Include customs information in export documentation

**Manufacturing Quality Assurance**:
- Embed inspection results and quality metrics in certificates
- Link to online calibration data for measurement equipment
- Include tester identification and timestamp data

**Legal and Compliance**:
- Encode audit trail information in compliance certificates
- Add verification URLs to contracts for authenticity checking
- Include witness information in notarized documents

**Education and Certification**:
- Add verification data to diplomas and certificates
- Encode course completion details in training records
- Link to online credential verification systems

The beauty of this approach is flexibility. You're not limited to HIBC—you can encode any structured data (JSON, XML, custom formats) by adjusting the encode type. The same signing workflow applies regardless of your data structure.

## QR Code Signatures vs Traditional Digital Signatures

**When to use QR code signatures:**
- You need human-readable verification (anyone with a phone can check)
- Your signature must carry additional data beyond authentication
- You're working in industries requiring specific data encoding (healthcare, food safety, etc.)
- You want dual-purpose elements (signature + data carrier)
- Offline verification is important (no internet connection needed to scan)

**When to stick with traditional digital signatures:**
- Legal non-repudiation is critical (QR codes don't provide cryptographic proof)
- You need PKI infrastructure integration
- Document size is a major concern (traditional signatures are smaller)
- Your workflow requires signature timestamps and certificate chains
- You're signing sensitive documents where data exposure is a risk

**Can you use both?** Absolutely. Many production systems apply a traditional digital signature for legal validity, then add a QR code signature for convenience and data sharing. GroupDocs.Signature supports multiple signature types on the same document:

```java
// Apply traditional digital signature first
DigitalSignOptions digitalOptions = new DigitalSignOptions("certificate.pfx");
digitalOptions.setPassword("password");

// Then add QR code signature
QrCodeSignOptions qrOptions = new QrCodeSignOptions();
qrOptions.setData(combinedData);
qrOptions.setEncodeType(QrCodeTypes.HIBCLICQR);

// Apply both in one operation
signature.sign(outputPath, digitalOptions, qrOptions);
```

This gives you the best of both worlds—cryptographic security plus user-friendly verification.

## Common Pitfalls and How to Avoid Them

**Issue #1: File locks and "file in use" errors**

**Symptom**: You get exceptions about files being locked or in use, especially when running your code multiple times quickly.

**Cause**: Not properly disposing of `Signature` objects. Each instance holds a file handle to your input document.

**Solution**: Always use try-finally blocks (as shown in our examples) or try-with-resources if you're on Java 7+:

```java
try (Signature signature = new Signature(filePath)) {
    signature.sign(outputPath, options);
}
// Automatic disposal happens here
```

**Issue #2: QR codes too small to scan**

**Symptom**: Your QR code is technically correct but can't be scanned reliably with smartphone cameras.

**Cause**: Default size may be too small, especially for dense HIBC data.

**Solution**: Increase the QR code size explicitly:

```java
options.setWidth(200);  // Width in pixels
options.setHeight(200); // Height in pixels
```

Aim for at least 150x150 pixels for reliable smartphone scanning. Test with your actual devices—what works on a newer iPhone might fail on older Android phones.

**Issue #3: Date formatting issues**

**Symptom**: Scanned QR codes show garbled dates or dates don't match what you encoded.

**Cause**: HIBC date format doesn't match your input date format.

**Solution**: Be explicit about date formats and handle time zones:

```java
// If you're parsing dates from strings
SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
Date mfgDate = sdf.parse("2025-01-15");
secondaryData.setDateOfManufacture(mfgDate);

// Always set the HIBC date format explicitly
secondaryData.setExpiryDateFormat(HIBCLICDateFormat.MMDDYY);
```

**Issue #4: QR code data truncation**

**Symptom**: Only partial data appears when scanning your QR code.

**Cause**: Exceeding QR code data capacity. Even though QR codes can hold a lot, HIBC combined format has specific limits.

**Solution**: Keep your strings concise. Product numbers, lot numbers, and serial numbers should all be under 18 characters. If you're hitting limits, consider encoding just a reference ID and store detailed data in a database:

```java
// Instead of encoding all data
primaryData.setProductOrCatalogNumber("VERY-LONG-PRODUCT-DESCRIPTION-THAT-WONT-FIT");

// Use a reference
primaryData.setProductOrCatalogNumber("P123456");
// Full details accessible via P123456 lookup
```

**Issue #5: Output directory doesn't exist**

**Symptom**: IOException when trying to save signed document.

**Cause**: The library doesn't create output directories automatically.

**Solution**: Create directories before signing:

```java
File outputDir = new File(outputFilePath).getParentFile();
if (!outputDir.exists()) {
    outputDir.mkdirs();
}
```

## Performance Considerations

**Memory management**: Each `Signature` object loads the entire input document into memory. For large PDFs (100+ MB), this can be significant. Process documents sequentially rather than loading many at once:

```java
// Good - processes one at a time
for (String docPath : documentPaths) {
    try (Signature sig = new Signature(docPath)) {
        sig.sign(getOutputPath(docPath), options);
    }
}

// Bad - loads all documents simultaneously
List<Signature> signatures = documentPaths.stream()
    .map(Signature::new)
    .collect(Collectors.toList());
```

**QR code generation overhead**: Creating QR codes is CPU-intensive. If you're signing thousands of documents, consider:
- Batch processing during off-peak hours
- Multi-threading with a thread pool (but watch memory usage)
- Caching QR codes for identical data (reuse the same options object)

**File I/O optimization**: When signing multiple documents, write to fast storage (SSD over HDD). Network drives add significant latency—consider downloading to local temp storage, signing, then uploading results.

**Best practice for production**: Monitor your application's resource usage. Set up alerts for memory spikes, track average processing time per document, and establish baseline performance metrics. This helps you catch issues before they impact users.

## Conclusion

You've now got a complete toolkit for signing documents with QR codes in Java. We've covered everything from basic setup to advanced HIBC data encoding, with practical examples you can adapt to your specific needs.

**Here's what you've learned:**
- How to structure and encode HIBC data (applicable to any complex data encoding)
- The complete workflow for adding QR code signatures to documents
- When to use QR codes versus traditional digital signatures
- How to avoid common pitfalls that trip up most developers
- Performance optimization techniques for production environments

**Your next steps**:
1. Try the basic example with a sample PDF to verify your setup
2. Adapt the HIBC data structure to match your actual data needs
3. Test QR code scanning with various smartphone cameras
4. Integrate this into your existing document workflow
5. Consider adding traditional digital signatures alongside QR codes for maximum security

The real power of this approach isn't just the technology—it's how it bridges the gap between digital security and real-world usability. Anyone with a smartphone can verify your documents instantly, no special apps required.

Ready to take it further? Explore GroupDocs.Signature's other features like barcode signatures, text signatures, and image signatures. They all follow similar patterns, so you've already got the foundation.

## FAQ Section

**Q: Can I customize the QR code appearance (colors, logo)?**

Yes, GroupDocs.Signature lets you customize QR code appearance:
```java
options.setForeColor(Color.BLUE);      // QR code color
options.setBackgroundColor(Color.WHITE); // Background color
```
However, avoid extreme customization—scanners need sufficient contrast to read the code reliably. Stick to dark QR codes on light backgrounds.

**Q: What's the maximum data size I can encode in a HIBC QR code?**

HIBC combined format typically supports up to about 100 characters of encoded data. The library handles the encoding optimization automatically, but keep your product numbers and lot numbers concise (under 18 characters each) for best results.

**Q: Can I sign documents other than PDFs?**

Absolutely. GroupDocs.Signature supports Word documents (DOCX), Excel spreadsheets (XLSX), PowerPoint presentations (PPTX), and image formats (PNG, JPG). The signing code is identical—just change the input file path:
```java
String filePath = "document.docx";  // Works exactly the same
```

**Q: How do I verify the QR code after signing?**

For basic verification, any QR code scanner app works—just scan and view the decoded data. For programmatic verification, use GroupDocs.Signature's search functionality:
```java
List<QrCodeSignature> signatures = signature.search(QrCodeSignature.class, SignatureType.QrCode);
for (QrCodeSignature sig : signatures) {
    System.out.println(sig.getText());  // Decoded data
}
```

**Q: What happens if my HIBC data is invalid?**

The library validates HIBC format when encoding. If your data doesn't conform to HIBC standards (wrong character types, invalid dates, etc.), you'll get an exception during signing. Always validate your data before encoding:
```java
try {
    signature.sign(outputPath, options);
} catch (Exception e) {
    System.err.println("Invalid HIBC data: " + e.getMessage());
    // Log the error and handle appropriately
}
```

**Q: Is there a performance difference between QR codes and barcodes?**

QR codes are slightly more CPU-intensive to generate than linear barcodes (like Code 128), but the difference is negligible for most use cases (milliseconds per signature). The real benefit of QR codes is data capacity—they can hold 100x more data than traditional barcodes while remaining scannable.

**Q: Can I batch-sign multiple documents with the same QR code?**

Yes. Create your `QrCodeSignOptions` once, then reuse it across multiple documents:
```java
QrCodeSignOptions options = new QrCodeSignOptions();
options.setData(combinedData);
options.setEncodeType(QrCodeTypes.HIBCLICQR);

for (String docPath : documentPaths) {
    try (Signature sig = new Signature(docPath)) {
        sig.sign(getOutputPath(docPath), options);
    }
}
```
This is much more efficient than recreating the options for each document.

**Q: Does this work on mobile/Android Java?**

GroupDocs.Signature for Java is designed for server-side and desktop Java applications. For Android, you'd need to use mobile-specific libraries for QR code generation. However, documents signed with GroupDocs.Signature can be viewed and scanned on any mobile device.

**Q: How do I handle exceptions during signing?**

Always wrap signing operations in try-catch blocks and implement proper error handling:
```java
try (Signature signature = new Signature(filePath)) {
    signature.sign(outputPath, options);
    System.out.println("Document signed successfully");
} catch (Exception e) {
    System.err.println("Signing failed: " + e.getMessage());
    e.printStackTrace();
    // Log to your logging system
    // Alert administrators if appropriate
    // Return error to user
}
```

## Resources

- **Documentation**: [GroupDocs.Signature for Java Docs](https://docs.groupdocs.com/signature/java/)
- **API Reference**: [Complete API Reference](https://reference.groupdocs.com/signature/java/)
- **Download**: [Latest GroupDocs Releases](https://releases.groupdocs.com/signature/java/)
- **Purchase Options**: [Buy a License](https://purchase.groupdocs.com/buy)
- **Free Trial**: [Try Before You Buy](https://releases.groupdocs.com/signature/java/)
- **Temporary License**: [Request Evaluation License](https://purchase.groupdocs.com/temporary-license/)
- **Support Forum**: [Get Help from the Community](https://forum.groupdocs.com/c/signature)