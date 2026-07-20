---
categories:
- Java PDF Processing
date: '2026-07-20'
description: Learn how to create barcode signature in PDF documents using Java and
  GroupDocs.Signature. Step-by-step tutorial with code examples and best practices.
images:
- /java/barcode-signatures/java-pdf-signing-barcode-groupdocs/og-image.png
keywords:
- create barcode signature
- how to add barcode
- generate code128 barcode
- add barcode pdf
- tamper evident barcode
lastmod: '2026-07-20'
linktitle: Create Barcode Signature Java
og_description: Create barcode signature in PDF using Java with GroupDocs.Signature.
  Learn step-by-step how to add Code128 barcodes, position them, and secure documents.
og_image_alt: 'Developer guide: Create barcode signature in PDF using Java and GroupDocs'
og_title: Create Barcode Signature in PDF using Java – Full Guide
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to create barcode signature in PDF documents using Java and
    GroupDocs.Signature. Step-by-step tutorial with code examples and best practices.
  headline: How to Create Barcode Signature in PDF using Java
  type: TechArticle
- description: Learn how to create barcode signature in PDF documents using Java and
    GroupDocs.Signature. Step-by-step tutorial with code examples and best practices.
  name: How to Create Barcode Signature in PDF using Java
  steps:
  - name: Initialize the Signature object
    text: '**Definition anchor:** The `Signature` class is GroupDocs.Signature''s
      entry point for loading, modifying, and saving PDF documents. First, you need
      to tell GroupDocs which PDF you''re working with: **What''s happening here:**
      The `Signature` object loads your PDF into memory and prepares it for modifi'
  - name: Configure your barcode options (How to add barcode)
    text: '**Definition anchor:** `BarcodeSignOptions` encapsulates all settings required
      to render a barcode inside a PDF. Now let''s create the barcode signature with
      your data: - `"12345678"` is your barcode data — this could be an order ID,
      certificate number, or any identifier you need. - `Code128` is the '
  - name: Position your barcode (How to sign PDF with barcode)
    text: '**Definition anchor:** `SignatureOptions` provides layout properties such
      as page number, size, and alignment. Here''s where GroupDocs really shines —
      percentage‑based positioning means your barcode looks good on any PDF size:
      **Why percentages matter:** Imagine you''re signing both A4 documents and l'
  - name: Sign and save your document (How to add barcode pdf)
    text: 'Time to actually apply the signature and save your work: **Important note:**
      The output directory must exist before you run this code. GroupDocs won''t create
      nested directories for you, so create them first or handle that in your code:
      **What if something goes wrong?** Wrap this in a try‑catch block'
  type: HowTo
- questions:
  - answer: Yes! Call `signature.sign()` multiple times with different `BarcodeSignOptions`
      for each barcode type. Just ensure they don’t overlap.
    question: Can I use different barcode types in the same PDF?
  - answer: Code128 handles most ASCII characters fine. For Unicode or complex data,
      switch to QR codes—they support UTF‑8 encoding.
    question: How do I handle barcodes that contain special characters?
  - answer: Technically up to 128 characters, but readability drops significantly
      above 30‑40 characters. For larger payloads, use QR codes.
    question: What's the maximum data I can store in a Code128 barcode?
  - answer: Not noticeably—barcodes are vector graphics, typically adding only 5‑20
      KB per barcode depending on size and complexity.
    question: Will adding barcodes significantly increase my PDF file size?
  - answer: Yes! Use `options.setRotationAngle(90)` to rotate your barcode, which
      is handy for margin placement.
    question: Can I rotate barcodes or place them vertically?
  type: FAQPage
tags:
- pdf-signing
- barcode-signature
- document-security
- groupdocs
- java
- pdf
title: How to Create Barcode Signature in PDF using Java
type: docs
url: /java/barcode-signatures/java-pdf-signing-barcode-groupdocs/
weight: 1
---

# How to Create Barcode Signature in PDF using Java

In this tutorial, you'll learn how to **create barcode signature** in PDF files using Java and GroupDocs.Signature. Barcode signatures embed machine‑readable identifiers that are both tamper‑evident and easy to scan—perfect for contracts, certificates, invoices, and any document that needs reliable verification.

## Quick Answers
- **What is a barcode signature?** A barcode embedded in a PDF that stores structured data and can be read by scanners or software.  
- **Which barcode type is recommended?** Code128, because it handles alphanumeric data compactly.  
- **Do I need a license?** A free trial works for testing; a full license is required for production.  
- **Can I position the barcode on any page size?** Yes—use percentage‑based positioning for automatic scaling.  
- **Is the barcode vector‑based?** Yes, it adds only a few kilobytes to the PDF and remains crisp at any resolution.  

## What is a barcode signature?
A barcode signature is a vector‑based barcode embedded directly into a PDF page, acting both as a visual element and as a cryptographic signature that can be validated later. It stores structured data, such as IDs or timestamps, and ensures the document’s integrity while providing a machine‑readable reference.

## Why barcode signatures matter for your PDFs
Barcode signatures give PDFs a compact, machine‑readable identifier that can be scanned instantly, eliminating manual data entry and reducing errors. Because they are embedded as vector graphics, they remain sharp at any resolution and add only a few kilobytes to the file. This combination of readability, tamper‑evidence, and minimal size makes them ideal for contracts, invoices, certificates, and any document that requires reliable verification.

Here's a challenge you've probably faced: you need to add unique identifiers to PDFs that are both machine‑readable and tamper‑evident. Maybe you're working on a document management system, processing certificates, or handling contracts that need verification down the line.

That's where barcode signatures come in handy. Unlike simple text stamps, barcodes let you embed structured data that scanners (and your software) can read instantly. Plus, when you combine them with PDF signing through GroupDocs.Signature for Java, you get a powerful way to track and verify documents without adding complex database lookups.

In this guide, you'll learn exactly how to implement barcode signatures in your Java PDFs — from basic setup to production‑ready code with flexible positioning. Whether you're building an invoice system, certificate generator, or contract management platform, you'll have everything you need by the end.

**What You'll Master:**
- Setting up GroupDocs.Signature for Java in minutes  
- Creating Code128 barcode signatures (and why they're often your best choice)  
- Positioning barcodes using percentage‑based layouts that work across any PDF size  
- Avoiding common pitfalls that trip up developers  
- Testing your implementation properly  

## How to create barcode signature in Java
Creating a barcode signature in Java involves loading the target PDF, configuring the barcode options such as data, type, size, and position, and then applying the signature to generate a new document. GroupDocs.Signature handles the rendering and cryptographic binding, so you only need to supply the desired parameters and manage file paths.

## Prerequisites and environment checklist

Before you dive in, verify that you have the following items ready:

- **Java Development Kit (JDK) 8 or newer** – required for all GroupDocs Java libraries.  
- **Maven or Gradle** – to manage the GroupDocs.Signature dependency.  
- **An IDE** such as IntelliJ IDEA, Eclipse, or VS Code with Java extensions.  
- **GroupDocs.Signature for Java** (version 23.12 or newer is recommended).  
- **Basic Java knowledge** – you should be comfortable creating classes, handling exceptions, and working with file I/O.

## Setting up GroupDocs.Signature in your project

Getting the library into your project is straightforward. Pick your build tool:

**For Maven users**, add this dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Using Gradle?** Add this line to your `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Prefer manual setup?** Download the JAR directly from [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) and add it to your classpath.

### Getting your license sorted

Before you go full production, you'll want to handle licensing:

- **Free Trial:** Perfect for testing — get it from the GroupDocs website to explore core features.  
- **Temporary License:** Need more time to evaluate? Apply for a 30‑day temporary license.  
- **Full License:** Ready for production? Purchase a license for unlimited usage.  

Here's a quick sanity check to make sure everything's working:

```java
Signature signature = new Signature("sample.pdf");
System.out.println("Signature object created successfully.");
```

If that runs without errors, you're all set!

## How to create barcode signature in Java

Now for the fun part — let's sign a PDF with a barcode. We'll break this down into bite‑sized steps so you understand exactly what's happening at each stage.

### Step 1: Initialize the Signature object

**Definition anchor:** The `Signature` class is GroupDocs.Signature's entry point for loading, modifying, and saving PDF documents.

First, you need to tell GroupDocs which PDF you're working with:

```java
Signature signature = new Signature("input.pdf");
```

**What's happening here:** The `Signature` object loads your PDF into memory and prepares it for modifications. Make sure your file path is correct — a common gotcha is using backslashes on Windows without escaping them (use `\\` or just use forward slashes, which work cross‑platform).

### Step 2: Configure your barcode options (How to add barcode)

**Definition anchor:** `BarcodeSignOptions` encapsulates all settings required to render a barcode inside a PDF.

Now let's create the barcode signature with your data:

```java
BarcodeSignOptions options = new BarcodeSignOptions("12345678");
options.setEncodeType(BarcodeEncodeType.Code128);
```

- `"12345678"` is your barcode data — this could be an order ID, certificate number, or any identifier you need.  
- `Code128` is the encoding type (more on choosing the right type below).  

**Pro tip:** Code128 can handle both numbers and letters, making it versatile for most use cases. If you only need numbers, `Code39` might be simpler, but Code128 gives you more flexibility.

### Step 3: Position your barcode (How to sign PDF with barcode)

**Definition anchor:** `SignatureOptions` provides layout properties such as page number, size, and alignment.

Here's where GroupDocs really shines — percentage‑based positioning means your barcode looks good on any PDF size:

```java
options.setLeft(10);   // 10% from the left edge
options.setTop(90);    // 90% from the bottom edge (near the footer)
options.setWidth(30);  // 30% of page width
options.setHeight(10); // 10% of page height
options.setPageNumber(1);
```

**Why percentages matter:** Imagine you're signing both A4 documents and legal‑sized forms. With percentage positioning, your barcode automatically scales to look consistent on both. Using fixed pixel values would make your barcode too small on large documents or too large on small ones.

**Real‑world example:** On an A4 page (595 × 842 points), a 30% width barcode will be ~180 points wide. On a legal page (612 × 1008 points), it will be ~184 points wide — automatically proportional.

### Step 4: Sign and save your document (How to add barcode pdf)

Time to actually apply the signature and save your work:

```java
signature.sign(outputPath, options);
```

**Important note:** The output directory must exist before you run this code. GroupDocs won't create nested directories for you, so create them first or handle that in your code:

```java
new File("output").mkdirs();
```

**What if something goes wrong?** Wrap this in a try‑catch block:

```java
try {
    signature.sign("signed.pdf", options);
} catch (Exception e) {
    e.printStackTrace();
}
```

## Choosing the right barcode type for your needs (generate code128 barcode)

GroupDocs supports multiple barcode formats, and picking the right one matters. Here's a practical comparison:

**Code128 (Our Default Choice):**
- **Best for:** Mixed alphanumeric data (IDs like "INV2024-001")  
- **Capacity:** Up to 128 ASCII characters  
- **Why it wins:** Compact, widely supported, handles both letters and numbers  
- **Use when:** You need flexibility and don't know what kind of data you'll encode  

**Code39:**
- **Best for:** Simple alphanumeric codes  
- **Capacity:** 43 characters (A‑Z, 0‑9, and some symbols)  
- **Why consider it:** Older scanners often support it better  
- **Use when:** Working with legacy systems or when simplicity matters more than data density  

**QR Code:**
- **Best for:** Large amounts of data (URLs, JSON payloads)  
- **Capacity:** Up to 3 KB of data  
- **Why it's powerful:** Can store complex data structures, error correction built‑in  
- **Use when:** You need to embed structured data or URLs  

**EAN/UPC:**
- **Best for:** Product identification  
- **Capacity:** Fixed‑length numeric codes (8‑13 digits)  
- **Use when:** You're working with retail or inventory systems  

**Quick decision guide:**  
- Need letters and numbers? → Code128  
- Only numbers, keep it simple? → Code39  
- Lots of data or URLs? → QR Code  
- Retail/product codes? → EAN/UPC  

## Common pitfalls and how to avoid them (tamper evident barcode)

Here are the issues developers run into most often (so you don't have to):

### Problem 1: Barcode positioning looks wrong

**Symptom:** Your barcode appears in unexpected locations or gets cut off.

**Common causes:**  
- Using pixel values on different page sizes  
- Forgetting that PDF coordinates start from bottom‑left, not top‑left  
- Margins pushing content outside visible area  

**Solution:** Always use percentage‑based positioning for consistency:

```java
options.setLeft(5);
options.setTop(95);
options.setWidth(40);
options.setHeight(12);
```

### Problem 2: Barcode text is unreadable

**Symptom:** The encoded text displays but scanners can't read it.

**Causes:**  
- Barcode too small for the amount of data  
- Wrong encoding type for your data  
- Low contrast between bars and background  

**Solution:** Match your barcode size to your data length. For Code128 with 10‑15 characters, aim for at least 8‑10% page width.

### Problem 3: File path exceptions

**Symptom:** `FileNotFoundException` or similar errors.

**Causes:**  
- Hardcoded Windows paths with single backslashes  
- Output directory doesn't exist  
- File permissions issues  

**Solution:** Use forward slashes (they work everywhere) and create directories first:

```java
Path output = Paths.get("output/signed.pdf");
Files.createDirectories(output.getParent());
```

### Problem 4: Memory issues with large PDFs

**Symptom:** Out of memory errors when processing big documents.

**Solution:** Close the `Signature` object when you're done to free resources:

```java
signature.close();
```

## Testing your barcode implementation

Before you deploy, make sure your barcodes actually work. Here's a practical testing checklist:

### 1. Visual inspection test
Open your signed PDF and check:
- Is the barcode visible and properly positioned?  
- Does it look crisp (not blurry or pixelated)?  
- Is there adequate white space around it?

### 2. Scanning test
Use a barcode scanner app on your phone (like “Barcode Scanner” or “QR & Barcode Reader”) to verify:
- The scanner can read your barcode  
- The decoded data matches what you encoded  
- It works from different angles and distances

### 3. Cross‑platform test
Open your PDF on different devices:
- Windows (Adobe Reader, Chrome)  
- Mac (Preview, Chrome)  
- Mobile devices (iOS, Android)  

Make sure the barcode renders correctly everywhere.

### 4. Automated testing code
Here's a simple test you can run:

```java
Signature testSignature = new Signature("signed.pdf");
List<BarcodeSignature> signatures = testSignature.search(BarcodeSignature.class);
if (signatures.size() > 0) {
    System.out.println("Barcode found: " + signatures.get(0).getText());
}
```

## Real‑world use cases for barcode signatures

Let's look at where this technique really shines in production systems:

### 1. Certificate generation and verification
**Scenario:** You're building a training platform that issues completion certificates.  
**Implementation:** Generate a unique certificate ID (e.g., “CERT‑2024‑00123”) and embed it as a Code128 barcode in the bottom‑right corner. Scanning the barcode lets your API retrieve the certificate details instantly, eliminating manual data entry.  

### 2. Invoice tracking systems
**Scenario:** Your company processes thousands of invoices monthly.  
**Implementation:** Add invoice number and due date as a QR code positioned where scanning equipment can easily read it. Automated sorting systems can route invoices without human intervention, cutting processing time from hours to minutes.  

### 3. Legal contract management
**Scenario:** A law firm needs to track contract versions and amendments.  
**Implementation:** Each contract version gets a unique barcode identifier that includes contract ID, version number, and signature date. Scanning during audits pulls up the full version history automatically.  

### 4. Medical records security
**Scenario:** A hospital wants to prevent unauthorized record access.  
**Implementation:** Embed patient ID and record creation timestamp in a barcode. Only authenticated devices can decode and access the full record, and every scan creates an audit log for compliance.  

## Performance optimization tips (java document security)

When you're signing lots of PDFs, performance matters. Here are some tips to keep things running smoothly:

### Batch processing strategy
Instead of signing one document at a time, batch them:

```java
for (String filePath : pdfList) {
    Signature batchSignature = new Signature(filePath);
    batchSignature.sign(outputPath, options);
    batchSignature.close();
}
```

**Why this helps:** Reusing the options object and properly closing resources prevents memory leaks.

### Memory management for large PDFs
For PDFs larger than 50 MB:
- Process them sequentially rather than loading multiple at once.  
- Use try‑with‑resources to ensure cleanup.  
- Monitor heap size and adjust JVM parameters if needed: `-Xmx2g`.

### Caching frequently used barcodes
If you sign many documents with the same barcode, cache the `BarcodeSignOptions` instance:

```java
BarcodeSignOptions cachedOptions = new BarcodeSignOptions("STATIC_ID");
cachedOptions.setEncodeType(BarcodeEncodeType.Code128);
```

## When to use barcode signatures (and when not to)

**Perfect scenarios:**
- You need machine‑readable document identifiers.  
- Documents will be scanned or processed automatically.  
- You want tamper‑evident tracking without digital certificates.  
- Integration with existing barcode infrastructure is required.  

**Not ideal when:**
- You need legally binding digital signatures (use digital certificates instead).  
- Documents will only be viewed by humans (a simple text watermark may suffice).  
- You're working with extremely small documents where a barcode would dominate the page.  
- Security requirements mandate encryption—barcodes are visible and scannable by anyone.  

**Can you combine approaches?** Absolutely! Many systems use both barcode signatures for tracking and digital signatures for legal validity.

## Frequently Asked Questions

**Q: Can I use different barcode types in the same PDF?**  
A: Yes! Call `signature.sign()` multiple times with different `BarcodeSignOptions` for each barcode type. Just ensure they don’t overlap.

**Q: How do I handle barcodes that contain special characters?**  
A: Code128 handles most ASCII characters fine. For Unicode or complex data, switch to QR codes—they support UTF‑8 encoding.

**Q: What's the maximum data I can store in a Code128 barcode?**  
A: Technically up to 128 characters, but readability drops significantly above 30‑40 characters. For larger payloads, use QR codes.

**Q: Will adding barcodes significantly increase my PDF file size?**  
A: Not noticeably—barcodes are vector graphics, typically adding only 5‑20 KB per barcode depending on size and complexity.

**Q: Can I rotate barcodes or place them vertically?**  
A: Yes! Use `options.setRotationAngle(90)` to rotate your barcode, which is handy for margin placement.

**Q: How do I make barcodes appear on every page of a multi‑page PDF?**  
A: Iterate through pages and apply the signature to each one. Check the `PagesSetup` class in the GroupDocs documentation to control which pages get signed.

**Q: What if my barcode scanner can't read the generated barcode?**  
A: First, verify the scanner supports the chosen barcode type. Then increase the barcode size—most scanning issues stem from bars that are too small. Aim for at least 1 inch (2.54 cm) width for reliable reads.

## Additional Resources

**Documentation:**  
- [GroupDocs.Signature for Java Docs](https://docs.groupdocs.com/signature/java/)  
- [API Reference Guide](https://reference.groupdocs.com/signature/java/)  

**Downloads and Licensing:**  
- [Download Latest Version](https://releases.groupdocs.com/signature/java/)  
- [Free Trial Access](https://releases.groupdocs.com/signature/java/)  
- [Get Temporary License](https://purchase.groupdocs.com/temporary-license/)  
- [Purchase Full License](https://purchase.groupdocs.com/buy)  

**Community and Support:**  
- [Support Forum](https://forum.groupdocs.com/c/signature/) - Active community with GroupDocs engineers  

---

**Last Updated:** 2026-07-20  
**Tested With:** GroupDocs.Signature 23.12 (Java)  
**Author:** GroupDocs

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

```java
import com.groupdocs.signature.Signature;

public class QuickTest {
    public static void main(String[] args) {
        try {
            Signature signature = new Signature("test-document.pdf");
            System.out.println("GroupDocs.Signature is ready to go!");
        } catch (Exception e) {
            System.err.println("Setup issue: " + e.getMessage());
        }
    }
}
```

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
Signature signature = new Signature(filePath);
```

```java
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

BarcodeSignOptions options = new BarcodeSignOptions("12345678");
options.setEncodeType(BarcodeTypes.Code128);
```

```java
import com.groupdocs.signature.domain.enums.MeasureType;
import com.groupdocs.signature.domain.Padding;

// Use percentages instead of fixed pixels
options.setLocationMeasureType(MeasureType.Percents);
options.setLeft(5);  // 5% from the left edge
options.setTop(5);   // 5% from the top

// Size it proportionally too
options.setSizeMeasureType(MeasureType.Percents);
options.setWidth(10);  // 10% of page width
options.setHeight(5);  // 5% of page height

// Add some breathing room with margins
Padding margins = new Padding();
margins.setLeft(1);
margins.setTop(1);
margins.setRight(1);
options.setMargin(margins);
```

```java
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithPercents/sample_signed.pdf";
signature.sign(outputFilePath, options);
```

```java
Path outputPath = Paths.get(outputFilePath);
Files.createDirectories(outputPath.getParent());
signature.sign(outputFilePath, options);
```

```java
try {
    signature.sign(outputFilePath, options);
    System.out.println("PDF signed successfully at: " + outputFilePath);
} catch (Exception e) {
    System.err.println("Signing failed: " + e.getMessage());
    e.printStackTrace();
}
```

```java
options.setLocationMeasureType(MeasureType.Percents);
options.setLeft(5);  // 5% from left works on any page width
```

```java
options.setWidth(10);  // Give it room to breathe
options.setHeight(5);  // Maintain proper aspect ratio
```

```java
String filePath = "documents/sample.pdf";  // Works on Windows, Mac, Linux
Files.createDirectories(Paths.get("output/signed"));
```

```java
try (Signature signature = new Signature(filePath)) {
    signature.sign(outputFilePath, options);
} // Automatically closes and releases memory
```

```java
import org.junit.Test;
import static org.junit.Assert.*;

public class BarcodeSignatureTest {
    
    @Test
    public void testBarcodeSigning() {
        String testPdf = "test-data/sample.pdf";
        String output = "test-output/signed.pdf";
        
        try (Signature signature = new Signature(testPdf)) {
            BarcodeSignOptions options = new BarcodeSignOptions("TEST123");
            options.setEncodeType(BarcodeTypes.Code128);
            
            signature.sign(output, options);
            
            // Verify output file exists
            assertTrue(new File(output).exists());
            
            // Verify file size increased (signature was added)
            long originalSize = new File(testPdf).length();
            long signedSize = new File(output).length();
            assertTrue(signedSize > originalSize);
            
        } catch (Exception e) {
            fail("Signing should not throw exception: " + e.getMessage());
        }
    }
}
```

```java
List<String> pdfFiles = Arrays.asList("doc1.pdf", "doc2.pdf", "doc3.pdf");

for (String pdfFile : pdfFiles) {
    try (Signature signature = new Signature(pdfFile)) {
        BarcodeSignOptions options = createBarcodeOptions(); // Reuse options
        signature.sign(getOutputPath(pdfFile), options);
    }
}
```

```java
// Create options once, reuse many times
BarcodeSignOptions templateOptions = createStandardBarcodeOptions();

// For each document, clone and customize
BarcodeSignOptions documentOptions = templateOptions.clone();
documentOptions.setText(uniqueDocumentId);
```

## Related Tutorials

- [Java Barcode Signature Tutorial - Add, Verify & Manage Barcodes in PDFs](/signature/java/barcode-signatures/)
- [Create Barcode Signature in Java – Update PDF Barcodes](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [How to read QR code PDF using Java and GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)