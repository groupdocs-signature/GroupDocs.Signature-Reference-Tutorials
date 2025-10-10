---
title: "Add Metadata to PDF with Java - Complete GroupDocs Signature Tutorial"
linktitle: "Add PDF Metadata with Java"
description: "Learn how to add author, creation date, and custom metadata to PDFs using Java. Step-by-step guide with code examples for GroupDocs.Signature library."
keywords: "PDF metadata signature Java, add metadata to PDF Java, GroupDocs Signature Java tutorial, embed metadata in PDF Java, PDF document metadata programmatically"
date: "2025-01-02"
lastmod: "2025-01-02"
weight: 1
url: "/java/metadata-signatures/groupdocs-signature-java-add-metadata-to-pdfs/"
categories: ["Java PDF Processing"]
tags: ["pdf-metadata", "java-pdf", "document-security", "groupdocs"]
type: docs
---

# Add Metadata to PDF with Java - Complete GroupDocs Signature Tutorial

## Introduction

Ever received a PDF and wondered who created it, when it was made, or what tool generated it? That's metadata at work—and if you're building document management systems in Java, you'll want to add this information to your own PDFs.

Here's the thing: metadata signatures aren't just about storing information. They're about proving document authenticity, tracking changes, and meeting compliance requirements (think legal documents, medical records, or financial reports). Without proper metadata, your PDFs are basically anonymous files floating in a sea of digital content.

**In this guide, you'll learn how to:**
- Add standard metadata signatures (author, creation date, keywords) to PDFs using Java
- Set up GroupDocs.Signature in your project (Maven or Gradle)
- Implement metadata signing in under 10 lines of code
- Verify that your metadata was added correctly
- Avoid common pitfalls that trip up developers

Whether you're building a contract management system, an e-signature platform, or just need to add document tracking to your app, this tutorial will get you up and running fast. Let's dive in.

## Why Metadata Signatures Matter

Before we jump into code, let's talk about why you'd want to add metadata signatures in the first place (because it's more than just "nice to have").

**1. Legal and Compliance Requirements**
Many industries require documents to have verifiable creation dates, author information, and audit trails. Try submitting a legal contract without proper metadata in some jurisdictions—it might not hold up in court.

**2. Document Authenticity**
Metadata signatures help prove a document hasn't been tampered with. When you embed creator information and timestamps, you're creating a digital paper trail that's harder to forge than file properties alone.

**3. Workflow Automation**
Your document management system can automatically route files based on metadata. For example, contracts created by specific authors could trigger approval workflows, or documents older than X days could be archived automatically.

**4. Better Organization**
Ever tried finding a document in a folder with 500+ PDFs? Searchable metadata (like keywords, subjects, and categories) makes this infinitely easier—especially when integrated with enterprise search tools.

## Prerequisites

Before we get our hands dirty, make sure you've got these basics covered:

**Development Environment:**
- **JDK 8 or later** - GroupDocs.Signature works with Java 8+, but we recommend Java 11 or 17 for better performance
- **IDE** - IntelliJ IDEA, Eclipse, or VS Code with Java extensions (whatever you're comfortable with)
- **Build Tool** - Maven or Gradle (we'll show both configurations)

**Knowledge Prerequisites:**
- Basic Java programming (you should know classes, objects, and file I/O)
- Familiarity with Maven or Gradle (just enough to add dependencies)
- Understanding of PDF structure is helpful but not required

**What You'll Need:**
- A sample PDF file to work with (any PDF will do—we'll modify a copy)
- About 15 minutes to follow along with the code examples

## Setting Up GroupDocs.Signature for Java

### Installation Information

First things first: let's get GroupDocs.Signature into your project. The library is available through standard Java repositories, so adding it is straightforward.

**For Maven Projects:**

Add this dependency to your `pom.xml` file (inside the `<dependencies>` section):

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**For Gradle Projects:**

Add this line to your `build.gradle` file (in the dependencies block):

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Note on Versions:** We're using version 23.12 here, but check [GroupDocs releases](https://releases.groupdocs.com/signature/java/) for the latest version. Newer versions often include performance improvements and bug fixes.

**Direct Download Option:**

If you're not using Maven or Gradle (or you prefer manual dependency management), you can download the JAR files directly from the [releases page](https://releases.groupdocs.com/signature/java/) and add them to your project's classpath.

### License Acquisition

GroupDocs.Signature isn't free, but they offer flexible options depending on your needs:

**1. Free Trial**
Start with a free trial to evaluate the library. No credit card required—just download and test all features with some limitations (usually a watermark on output documents).

**2. Temporary License**
Need more time to evaluate? Grab a [temporary license](https://purchase.groupdocs.com/temporary-license/) that removes limitations for 30 days. Perfect for development and testing before going live.

**3. Full License**
When you're ready for production, [purchase a license](https://purchase.groupdocs.com/buy) based on your deployment needs (single application, multiple applications, or OEM licensing).

**Pro Tip:** If you're working on an open-source project or educational use, reach out to GroupDocs—they sometimes offer special licensing arrangements.

### Basic Initialization and Setup

Once you've got the dependency added, initialization is super simple. Here's the basic pattern you'll use throughout your code:

```java
Signature signature = new Signature("path/to/your/document.pdf");
```

That's it! The `Signature` class is your main entry point for all operations. It handles loading the PDF, applying signatures, and saving the result.

**Important:** Make sure the path to your PDF is correct. Use absolute paths during development to avoid file-not-found headaches, then switch to relative paths or configuration-based paths in production.

## Implementation Guide

Alright, now for the fun part—let's actually add some metadata to a PDF.

### Adding Metadata Signatures

#### Overview

Adding metadata signatures involves three main steps:
1. Load your PDF document
2. Configure which metadata fields you want to add
3. Sign the document and save it

The beauty of GroupDocs.Signature is that it provides pre-defined metadata fields for PDFs (like Author, Subject, Keywords), so you don't have to worry about PDF specification details.

**What metadata can you add?**
- Author name
- Title and subject
- Keywords (for search)
- Creation and modification dates
- Producer (the software that created it)
- Creator (the original application)
- Custom metadata fields

Let's walk through it step by step.

#### Step-by-Step Implementation

##### Step 1: Define Output File Path

First, decide where your signed PDF will be saved. Don't overwrite your original file—always create a new copy:

```java
String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", "SignedDocument.pdf").getPath();
```

**Why this matters:** In production systems, you'll typically save signed documents to a different location or versioning system. This keeps your original files safe and maintains an audit trail.

**Pro Tip:** Use a timestamped filename pattern like `document_signed_20250102.pdf` to avoid overwriting previous versions.

##### Step 2: Initialize Signature Object

Create a `Signature` instance pointing to your source PDF:

```java
String filePath = "path/to/your/original.pdf"; // Your input PDF
Signature signature = new Signature(filePath);
```

**What's happening here:** The `Signature` object loads your PDF into memory and prepares it for modification. It doesn't change the original file—yet.

**Memory consideration:** For large PDFs (50MB+), be aware that this loads the entire file. If you're processing many files, consider doing this in batches or using streaming approaches.

##### Step 3: Configure Metadata Signatures

This is where the magic happens. We'll create a `MetadataSignOptions` object and populate it with the metadata fields we want to add:

```java
MetadataSignOptions options = new MetadataSignOptions();

// Create an array of metadata signatures
MetadataSignature[] signatures = new MetadataSignature[]{
    PdfMetadataSignatures.getAuthor().deepClone("Mr. Scherlock Holmes"),
    PdfMetadataSignatures.getCreateDate().deepClone(DateUtils.addDays(new Date(), -1)),
    PdfMetadataSignatures.getMetadataDate().deepClone(new Date()),
    PdfMetadataSignatures.getCreatorTool().deepClone("GroupDocs.Signature App"),
    PdfMetadataSignatures.getProducerTool().deepClone("GroupDocs.Signature for Java"),
};

// Add signatures to options
options.setSignatures(signatures);
```

**Let's break this down:**

- **PdfMetadataSignatures.getAuthor()** - Pre-defined field for document author. The `deepClone()` method creates a copy with your value ("Mr. Scherlock Holmes" in this case).

- **PdfMetadataSignatures.getCreateDate()** - When the document was created. Here we're using `DateUtils.addDays(new Date(), -1)` to set it to yesterday (just an example—normally you'd use the actual creation date).

- **PdfMetadataSignatures.getMetadataDate()** - When the metadata was added. Using `new Date()` stamps it with the current date/time.

- **PdfMetadataSignatures.getCreatorTool()** - The application that created the document. This could be your app's name.

- **PdfMetadataSignatures.getProducerTool()** - The library or tool that generated the PDF. We're crediting GroupDocs here.

**Why deepClone()?** This creates a new instance with your custom value while preserving the field's type and structure. It's a pattern specific to GroupDocs.Signature.

**Adding more metadata:**
You can also add fields like:
- `PdfMetadataSignatures.getTitle()` - Document title
- `PdfMetadataSignatures.getSubject()` - Document subject/description  
- `PdfMetadataSignatures.getKeywords()` - Searchable keywords (comma-separated)

##### Step 4: Sign the Document

Now we apply the metadata signatures to the PDF and save the result:

```java
SignResult result = signature.sign(outputFilePath, options);

// Optionally, check the result
System.out.println("Document signed successfully. Signatures added: " + result.getSucceeded().size());
```

**What happens during signing:**
1. GroupDocs loads your PDF structure
2. It adds the metadata fields to the PDF's internal metadata dictionary
3. The modified PDF is written to your output path
4. A `SignResult` object is returned with details about the operation

**Error handling tip:** Wrap this in a try-catch block to handle issues like file permissions, disk space, or invalid paths:

```java
try {
    SignResult result = signature.sign(outputFilePath, options);
    System.out.println("Success! Signatures added: " + result.getSucceeded().size());
} catch (Exception ex) {
    System.err.println("Signing failed: " + ex.getMessage());
    ex.printStackTrace();
}
```

#### Complete Code Example

Here's the full implementation in one place so you can see how it all fits together:

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.signatures.metadata.MetadataSignature;
import com.groupdocs.signature.domain.signatures.metadata.PdfMetadataSignatures;
import com.groupdocs.signature.options.sign.MetadataSignOptions;
import org.apache.commons.lang3.time.DateUtils;
import java.io.File;
import java.util.Date;

public class PdfMetadataExample {
    public static void main(String[] args) {
        try {
            // Define paths
            String inputFile = "path/to/your/document.pdf";
            String outputFile = "path/to/output/SignedDocument.pdf";
            
            // Initialize signature object
            Signature signature = new Signature(inputFile);
            
            // Configure metadata options
            MetadataSignOptions options = new MetadataSignOptions();
            MetadataSignature[] signatures = new MetadataSignature[]{
                PdfMetadataSignatures.getAuthor().deepClone("John Doe"),
                PdfMetadataSignatures.getCreateDate().deepClone(new Date()),
                PdfMetadataSignatures.getMetadataDate().deepClone(new Date()),
                PdfMetadataSignatures.getKeywords().deepClone("contract, legal, signed"),
                PdfMetadataSignatures.getCreatorTool().deepClone("MyDocumentApp v1.0")
            };
            options.setSignatures(signatures);
            
            // Sign the document
            SignResult result = signature.sign(outputFile, options);
            
            System.out.println("Successfully added " + result.getSucceeded().size() + " metadata signatures!");
            
        } catch (Exception ex) {
            System.err.println("Error: " + ex.getMessage());
        }
    }
}
```

## Common Pitfalls and How to Avoid Them

Even with straightforward APIs like GroupDocs.Signature, developers run into predictable issues. Here's what to watch out for:

**1. File Path Mistakes**

**Problem:** "File not found" errors are the #1 issue beginners face.

**Solution:** 
- Use absolute paths during development: `/Users/yourname/Documents/test.pdf`
- Double-check that your file actually exists at that location
- On Windows, escape backslashes: `"C:\\Documents\\file.pdf"` or use forward slashes: `"C:/Documents/file.pdf"`

**2. Overwriting Original Files**

**Problem:** Accidentally overwriting source documents (especially bad if you don't have backups).

**Solution:**
- Always use different input and output paths
- In production, write to a staging directory first, then move files after validation

**3. Date Format Issues**

**Problem:** Metadata dates showing up as weird values or causing exceptions.

**Solution:**
- Use Java's `Date` or `LocalDateTime` objects—don't pass strings
- If you need a specific date, use `SimpleDateFormat` or `DateTimeFormatter` to parse it first
- Remember that dates are stored in UTC in PDFs

**4. Permission Errors**

**Problem:** "Access denied" when trying to save the signed PDF.

**Solution:**
- Check write permissions on your output directory
- Make sure the output file isn't open in another program (like Adobe Reader)
- On Linux/Mac, verify file ownership and permissions

**5. Missing Dependencies**

**Problem:** `ClassNotFoundException` or `NoClassDefFoundError` at runtime.

**Solution:**
- If using Maven/Gradle, run `mvn clean install` or `gradle build` to ensure dependencies are downloaded
- For manual JAR management, make sure all GroupDocs JARs are in your classpath

## Verifying Your Metadata Signatures

After adding metadata, you probably want to verify it actually worked. Here's how to read the metadata back from your signed PDF:

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.signatures.metadata.MetadataSignature;
import com.groupdocs.signature.options.search.MetadataSearchOptions;

public class VerifyMetadata {
    public static void main(String[] args) {
        try {
            Signature signature = new Signature("path/to/SignedDocument.pdf");
            
            // Search for metadata signatures
            MetadataSearchOptions searchOptions = new MetadataSearchOptions();
            List<MetadataSignature> signatures = signature.search(MetadataSignature.class, searchOptions);
            
            // Print all metadata
            System.out.println("Found " + signatures.size() + " metadata fields:");
            for (MetadataSignature sig : signatures) {
                System.out.println(sig.getName() + ": " + sig.getValue());
            }
            
        } catch (Exception ex) {
            System.err.println("Error reading metadata: " + ex.getMessage());
        }
    }
}
```

**What you'll see:** This prints all metadata fields in the PDF, including the ones you just added. It's a great way to debug and confirm your metadata is stored correctly.

## Practical Applications

Let's look at real-world scenarios where this functionality shines:

**1. Legal Contract Management**

**Scenario:** A law firm needs to track who created each contract, when it was generated, and which version of their software was used.

**Implementation:**
```java
PdfMetadataSignatures.getAuthor().deepClone(lawyerName);
PdfMetadataSignatures.getCreateDate().deepClone(new Date());
PdfMetadataSignatures.getCreatorTool().deepClone("LegalDocGen v2.3");
PdfMetadataSignatures.getKeywords().deepClone("contract, " + clientName + ", " + caseNumber);
```

**Benefits:** Automated audit trails, easy case file searches, compliance with document retention policies.

**2. Publishing Workflow**

**Scenario:** A publishing company needs to track manuscript versions, authors, and editorial dates through their review process.

**Implementation:**
```java
PdfMetadataSignatures.getAuthor().deepClone(authorName);
PdfMetadataSignatures.getTitle().deepClone(manuscriptTitle);
PdfMetadataSignatures.getSubject().deepClone("Review Draft - " + versionNumber);
PdfMetadataSignatures.getKeywords().deepClone(String.join(", ", tags));
PdfMetadataSignatures.getMetadataDate().deepClone(new Date()); // Editorial review date
```

**Benefits:** Clear version control, searchable by author or topic, integration with content management systems.

**3. Financial Document Archiving**

**Scenario:** A bank needs to archive statements and reports with verifiable creation dates and processing information for regulatory compliance.

**Implementation:**
```java
PdfMetadataSignatures.getCreateDate().deepClone(statementDate);
PdfMetadataSignatures.getProducerTool().deepClone("FinanceSystem v5.2.1");
PdfMetadataSignatures.getKeywords().deepClone(accountNumber + ", " + statementType + ", " + year);
// Add custom metadata for account type, branch, etc.
```

**Benefits:** Meets SOX and banking regulations, tamper-evident records, faster retrieval during audits.

**4. Medical Records Management**

**Scenario:** A healthcare provider needs HIPAA-compliant document tracking with patient identifiers, creation dates, and system information.

**Implementation:**
```java
PdfMetadataSignatures.getAuthor().deepClone("Dr. " + physicianName);
PdfMetadataSignatures.getCreateDate().deepClone(visitDate);
PdfMetadataSignatures.getSubject().deepClone("Medical Record - " + recordType);
// Note: Never put PHI like patient names in keywords—use internal IDs
PdfMetadataSignatures.getKeywords().deepClone("record-" + internalRecordID);
```

**Benefits:** Audit trail for compliance, secure identification without exposing PHI in file properties, integration with EHR systems.

## Best Practices for Production Use

When you're ready to move from proof-of-concept to production, follow these guidelines:

**1. Input Validation**

Always validate metadata values before signing:

```java
if (authorName == null || authorName.trim().isEmpty()) {
    throw new IllegalArgumentException("Author name cannot be empty");
}

if (authorName.length() > 100) {
    throw new IllegalArgumentException("Author name too long (max 100 characters)");
}
```

**2. Centralized Configuration**

Don't hardcode metadata values. Use configuration files or environment variables:

```java
Properties config = new Properties();
config.load(new FileInputStream("app.properties"));

String producerTool = config.getProperty("pdf.producer.name", "DefaultProducer");
```

**3. Batch Processing**

Processing multiple PDFs? Use a thread-safe approach:

```java
ExecutorService executor = Executors.newFixedThreadPool(4);

for (File pdfFile : pdfFiles) {
    executor.submit(() -> {
        try {
            Signature signature = new Signature(pdfFile.getPath());
            // ... configure and sign
            signature.sign(outputPath, options);
        } catch (Exception ex) {
            // Log error but continue processing other files
            logger.error("Failed to sign " + pdfFile.getName(), ex);
        }
    });
}

executor.shutdown();
executor.awaitTermination(1, TimeUnit.HOURS);
```

**4. Logging and Monitoring**

Track signing operations for debugging and auditing:

```java
logger.info("Starting metadata signing for: " + inputFile);
long startTime = System.currentTimeMillis();

SignResult result = signature.sign(outputFilePath, options);

long duration = System.currentTimeMillis() - startTime;
logger.info("Completed signing in " + duration + "ms. Signatures added: " + result.getSucceeded().size());
```

**5. Resource Cleanup**

The `Signature` object holds resources—clean it up when done:

```java
Signature signature = null;
try {
    signature = new Signature(filePath);
    // ... do your work
} finally {
    if (signature != null) {
        signature.dispose(); // Releases resources
    }
}
```

Or use try-with-resources if available in your GroupDocs version:

```java
try (Signature signature = new Signature(filePath)) {
    // ... do your work
} // Automatically disposed
```

## Performance Considerations

**File Size Impact**

Adding metadata has minimal impact on file size (typically less than 1KB per document). However, if you're signing thousands of files, consider:

- **Disk I/O:** Use SSDs for temporary processing directories
- **Memory:** Each `Signature` object loads the PDF into memory—limit concurrent operations based on available RAM
- **Network:** If reading/writing to network storage, bandwidth becomes the bottleneck

**Optimization Tips**

1. **Reuse Signature Options:** If you're processing multiple PDFs with the same metadata structure, create the `MetadataSignOptions` once and reuse it:

```java
MetadataSignOptions options = createStandardMetadataOptions();

for (File pdf : pdfs) {
    Signature signature = new Signature(pdf.getPath());
    signature.sign(getOutputPath(pdf), options); // Reuse options
    signature.dispose();
}
```

2. **Parallel Processing:** For bulk operations, process files in parallel (as shown in Best Practices above)

3. **Streaming:** For very large PDFs (100MB+), check GroupDocs documentation for streaming options that don't load entire files into memory

**Benchmarks (Approximate)**

Based on typical hardware (Intel i7, 16GB RAM, SSD):
- **Small PDF (1-5 pages):** 200-500ms per document
- **Medium PDF (10-50 pages):** 500ms-2s per document  
- **Large PDF (100+ pages):** 2-10s per document

Your mileage will vary based on PDF complexity, metadata fields added, and system specs.

## Troubleshooting

**Issue: "Document is corrupted" error after signing**

**Cause:** Usually happens when the original PDF is already corrupted or uses unsupported PDF features.

**Solution:**
- Verify your source PDF opens correctly in Adobe Reader
- Try with a different PDF to isolate the issue
- Check GroupDocs.Signature version—newer versions support more PDF types

**Issue: Metadata not showing up in Adobe Reader properties**

**Cause:** Some metadata fields are internal to the PDF specification and don't appear in Reader's File > Properties dialog.

**Solution:**
- Use a PDF metadata tool like ExifTool to view all metadata
- Or use the verification code shown earlier to programmatically read metadata

**Issue: "Access denied" when saving signed PDF**

**Cause:** File permissions or file is locked by another process.

**Solution:**
- Close the PDF if it's open in a viewer
- Check write permissions on the output directory
- Try writing to a different location (like your user's temp directory)

**Issue: OutOfMemoryError with large PDFs**

**Cause:** Loading huge PDFs into memory exceeds JVM heap size.

**Solution:**
- Increase JVM heap: `java -Xmx2g -jar yourapp.jar`
- Process large files sequentially instead of in parallel
- Consider using streaming APIs if available in newer GroupDocs versions

## Conclusion

You've now got everything you need to add metadata signatures to PDFs using GroupDocs.Signature for Java. Here's what we covered:

✅ Why metadata signatures matter (compliance, authenticity, organization)  
✅ Setting up GroupDocs.Signature in Maven or Gradle projects  
✅ Adding standard metadata fields (author, dates, keywords) with working code  
✅ Verifying metadata after signing  
✅ Real-world applications across industries  
✅ Production best practices and performance tips  
✅ Troubleshooting common issues

**Next Steps:**

1. **Try it yourself** - Download a trial license and add metadata to one of your PDFs
2. **Explore more signature types** - GroupDocs.Signature supports digital signatures, QR codes, barcodes, and stamps
3. **Integrate with your workflow** - Connect this to your document management system or workflow automation
4. **Read the full API docs** - Check out custom metadata fields and advanced options

The great thing about metadata signatures? They're invisible to end users but incredibly powerful for document management. Whether you're building a compliance system, an e-signature platform, or just want better document tracking, this foundation will serve you well.

Got stuck somewhere? Drop your questions in the GroupDocs forum (link below)—the community is pretty responsive.

## FAQ Section

**1. Can I add custom metadata fields beyond the standard ones?**

Yes! While we focused on standard fields (Author, Date, Keywords), GroupDocs.Signature supports custom metadata. You can create your own `MetadataSignature` objects with custom names and values. Check the API reference for the `PdfMetadataSignature` constructor.

**2. What if my PDF is already password-protected?**

You'll need to provide the password when creating the `Signature` object. GroupDocs.Signature has overloaded constructors that accept LoadOptions with password parameters. Without the correct password, the library can't modify the PDF.

**3. Does adding metadata invalidate existing digital signatures?**

Yes, modifying a PDF in any way (including adding metadata) will invalidate existing digital signatures. If you need both, add metadata first, then apply digital signatures last in your workflow.

**4. How much does signing a document typically take?**

For average PDFs (10-20 pages), expect 500ms to 2 seconds on modern hardware. Very large PDFs or those with complex structures might take 5-10 seconds. File I/O is usually the bottleneck, not the signing itself.

**5. Is GroupDocs.Signature compatible with Spring Boot?**

Absolutely! It's just a standard Java library, so it works seamlessly with Spring Boot, Jakarta EE, and other frameworks. You can inject dependencies, use configuration properties, and integrate with Spring's transaction management.

**6. Can I remove or modify metadata after it's been added?**

Yes. Load the signed PDF, search for existing metadata signatures, remove them, then add new ones and re-sign. Keep in mind this creates a new version of the document.

**7. What's the difference between metadata signatures and PDF form fields?**

Metadata signatures are invisible document properties stored in the PDF structure—they don't appear visually on pages. PDF form fields are visible elements users can interact with. Use metadata for background information and tracking, not user-facing content.

**8. Does this work with PDF/A (archival format)?**

Yes, GroupDocs.Signature supports PDF/A formats. However, be aware that PDF/A has strict rules about what modifications are allowed. Test thoroughly if you're working with archival documents.

## Resources

- [Documentation](https://docs.groupdocs.com/signature/java/) - Comprehensive guides and tutorials
- [API Reference](https://reference.groupdocs.com/signature/java/) - Detailed API documentation  
- [Download Library](https://releases.groupdocs.com/signature/java/) - Latest releases and versions
- [Purchase License](https://purchase.groupdocs.com/buy) - Production licensing options
- [Free Trial](https://releases.groupdocs.com/signature/java/) - Evaluate before buying
- [Temporary License](https://purchase.groupdocs.com/temporary-license/) - Extended testing license
- [Support Forum](https://forum.groupdocs.com/c/signature/) - Community help and support
