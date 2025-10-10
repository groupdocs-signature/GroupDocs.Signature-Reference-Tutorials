---
title: "Extract Address from QR Code Java"
linktitle: "Extract QR Code Address Data in Java"
description: "Learn how to extract address data from QR codes in Java using GroupDocs.Signature API. Step-by-step tutorial with code examples, troubleshooting, and best practices for document automation."
date: "2025-01-02"
lastmod: "2025-01-02"
weight: 1
url: "/java/qr-code-signatures/extract-qr-code-address-data-groupdocs-signature-java/"
keywords: "extract address from QR code Java, QR code data extraction Java, GroupDocs Signature Java tutorial, parse QR code address Java, Java QR code scanner PDF"
categories: ["Document Processing"]
tags: ["java", "qr-code", "groupdocs", "address-extraction", "document-automation"]
type: docs
---

# How to Extract Address from QR Code Java Documents

## Introduction

Ever spent hours manually copying address information from scanned documents? If you're building invoice processing systems, document management platforms, or any application that deals with physical-to-digital workflows, you've probably hit this bottleneck. QR codes are everywhere now—on invoices, shipping labels, business cards—but extracting that data programmatically can be tricky if you don't have the right tools.

Here's the good news: the GroupDocs.Signature for Java API makes QR code data extraction straightforward, even if you're working with complex document formats like PDFs or Word files. In this tutorial, I'll walk you through exactly how to extract address from QR code Java applications, handle common pitfalls, and get your document automation running smoothly.

**What you'll learn in this guide:**
- Setting up GroupDocs.Signature for Java in your project (Maven, Gradle, or direct download)
- Implementing QR code scanning and address extraction with working code examples
- Handling different QR code formats and data structures
- Troubleshooting common errors (because they *will* happen)
- Best practices for production environments

Whether you're automating invoice processing or building a document management system, this guide will get you from zero to extracting QR code addresses in about 15 minutes. Let's dive in.

## Prerequisites

Before we start extracting address data from QR codes, make sure you've got these basics covered:

**Required Libraries:**
- **GroupDocs.Signature for Java** version 23.12 or later (we'll install this in the next section)
- You'll also need access to documents containing QR codes—PDFs work great, but the library supports Word docs, images, and more

**Development Environment:**
- **Java Development Kit (JDK)** 8 or higher installed and configured
- Your favorite IDE (IntelliJ IDEA and Eclipse are popular choices, but any Java IDE works)
- Maven or Gradle for dependency management (optional but recommended)

**Knowledge Prerequisites:**
- Basic Java programming skills (if you can work with objects and loops, you're golden)
- Familiarity with your IDE's project structure
- Understanding of how APIs work (REST isn't required here—this is a native Java library)

**Why GroupDocs.Signature?** You might be wondering why not just use a generic QR code scanner library. The key difference is that GroupDocs.Signature is built specifically for *document* processing. It handles QR codes embedded in PDFs, Word docs, and other formats without you needing to extract images first. Plus, it's designed to work with structured data objects (like addresses) rather than just raw text strings.

## Setting Up GroupDocs.Signature for Java

Getting the library into your project takes just a few minutes. Pick the method that matches your build tool:

### Maven Setup

If you're using Maven (most common), add this dependency to your `pom.xml` file:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Pro tip:** After adding the dependency, run `mvn clean install` to make sure Maven downloads everything correctly. If you get repository errors, you might need to add the GroupDocs repository to your `pom.xml` (check their documentation for the latest repository URL).

### Gradle Setup

For Gradle projects, include this line in your `build.gradle` file:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

Then sync your Gradle project (usually happens automatically in IntelliJ, or run `gradle build` from the command line).

### Direct Download Method

Not using a build tool? No problem. Download the JAR files directly from [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) and add them to your project's classpath manually.

**License Acquisition:**
You'll need a license to use GroupDocs.Signature beyond the evaluation period. Here are your options:
- **Free trial**: Test all features with watermarked output (perfect for development)
- **Temporary license**: Get a full-featured 30-day license for testing ([request here](https://purchase.groupdocs.com/temporary-license/))
- **Full license**: Purchase for production use at [GroupDocs' licensing page](https://purchase.groupdocs.com/buy)

**Common setup issue:** If you're getting "class not found" errors after adding the dependency, make sure you've refreshed your IDE's project structure. In IntelliJ, that's File → Reload Project. In Eclipse, right-click your project and select Maven → Update Project.

Once your environment is set up, we're ready to write some code.

## Implementation Guide: Extract QR Code Address Data in Java

Now for the fun part—actually extracting address information from QR codes. This implementation covers the most common scenario: scanning a PDF document for QR codes and pulling out structured address data.

### Step 1: Initialize the Signature Object

First, you need to create a `Signature` object that points to your document. Think of this as opening the document in memory so the library can work with it.

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample_qrcode_address_object.pdf";
Signature signature = new Signature(filePath);
```

**What's happening here:**
- `filePath` is the full path to your document—replace `YOUR_DOCUMENT_DIRECTORY` with your actual directory path
- The `Signature` object loads the document and prepares it for signature operations (QR code scanning, in our case)

**When to use this approach:** This initialization method works great for local files. If you're working with cloud storage or streams, GroupDocs also supports loading documents from byte arrays or input streams—check their documentation for those scenarios.

**Common mistake:** Make sure your file path uses the correct separator for your OS (forward slashes work on all platforms in Java, backslashes only on Windows and need escaping: `\\`).

### Step 2: Search for QR Code Signatures

Now we tell the library to scan the entire document and find all QR codes:

```java
List<QrCodeSignature> signatures = signature.search(QrCodeSignature.class, SignatureType.QrCode);
```

**Breaking this down:**
- `search()` method scans the document for specific signature types
- `QrCodeSignature.class` tells it we're looking for QR codes (not barcodes, digital signatures, etc.)
- `SignatureType.QrCode` is a filter ensuring we only get QR code results
- The return value is a `List` of all QR codes found in the document

**Performance note:** This searches the entire document. If you're working with large PDFs (100+ pages), consider searching specific page ranges using the overloaded `search()` method to improve performance. For example:

```java
// Search only pages 1-10
SearchOptions options = new SearchOptions();
options.setAllPages(false);
options.setPagesSetup(new PagesSetup(1, 10));
List<QrCodeSignature> signatures = signature.search(QrCodeSignature.class, options);
```

### Step 3: Extract and Parse Address Data

This is where the magic happens. For each QR code found, we attempt to extract the address information:

```java
for (QrCodeSignature qrSignature : signatures) {
    System.out.println("Found QRCode signature: " + qrSignature.getEncodeType().getTypeName() +
            " with text " + qrSignature.getText());

    Address address = qrSignature.getData(Address.class);
    if (address != null) {
        System.out.println("Found Address: " + address.getCountry() +
                " " + address.getState() + " " + address.getCity() +
                " " + address.getZIP());
    } else {
        System.out.println("Address object was not found. QRCode " +
                qrSignature.getEncodeType().getTypeName() + " with text " + qrSignature.getText());
    }
}
```

**Understanding the code flow:**

1. **Loop through each QR code**: The `for` loop processes every QR code found in the document
2. **Display basic info**: First `println` shows the QR code type (QR, DataMatrix, etc.) and raw text content
3. **Attempt data extraction**: `getData(Address.class)` tries to deserialize the QR code content into an `Address` object
4. **Handle results**: If the QR code contains structured address data, we print it; otherwise, we log that it's not an address QR code

**Important note about data structure:** This code assumes your QR codes contain data in a format that matches the `Address` class structure. GroupDocs.Signature uses JSON deserialization internally, so your QR code data needs to be JSON-formatted with fields like `country`, `state`, `city`, and `ZIP`.

**What if my QR codes use a different format?** You have two options:
1. Create a custom class that matches your QR code's data structure and use `getData(YourCustomClass.class)`
2. Use `qrSignature.getText()` to get the raw string data and parse it yourself

### Step 4: Setting Up a License (Production Environment)

To use GroupDocs.Signature without limitations in production, you'll need to apply your license. Here's how:

```java
String licensePath = "YOUR_DOCUMENT_DIRECTORY/groupdocs.license";
License signatureLicense = new License();
try {
    signatureLicense.setLicense(licensePath);
    System.out.println("GroupDocs Signature license applied successfully.");
} catch (Exception e) {
    System.out.println("Failed to apply GroupDocs Signature license. Ensure the license file is valid and accessible.");
}
```

**License application best practices:**

- **Call this once at application startup**: Don't apply the license every time you process a document—do it once when your app initializes
- **Use absolute paths**: Relative paths can be tricky depending on where your app runs. Absolute paths eliminate confusion
- **Handle exceptions gracefully**: If the license fails to load, your app should either fall back to trial mode or exit gracefully with a clear error message

**Where to put this code:** For Spring Boot applications, put this in a `@PostConstruct` method in a configuration class. For standalone apps, call it at the start of your `main()` method.

## Troubleshooting Common Issues

Here are the problems I've seen developers run into most often when extracting address data from QR codes, plus how to fix them:

### "Address object was not found" Despite QR Code Being Present

**Symptom:** Your code finds the QR code but `getData(Address.class)` returns `null`.

**Common causes:**
1. **Data format mismatch**: The QR code doesn't contain JSON data or the JSON structure doesn't match your `Address` class
2. **Wrong encoding**: The QR code uses a character encoding that's not UTF-8
3. **Corrupted data**: The QR code is damaged or poorly printed in the document

**How to fix it:**
```java
// First, check what the raw data looks like
System.out.println("Raw QR code content: " + qrSignature.getText());

// Try parsing manually to see the actual structure
try {
    // You might need a JSON library like Gson or Jackson
    JsonObject json = JsonParser.parseString(qrSignature.getText()).getAsJsonObject();
    System.out.println("QR code contains these fields: " + json.keySet());
} catch (Exception e) {
    System.out.println("QR code doesn't contain valid JSON: " + e.getMessage());
}
```

### Performance Issues with Large Documents

**Symptom:** Processing takes too long on PDFs with many pages.

**Solutions:**
1. **Search specific pages only** (shown in Step 2 above)
2. **Use multi-threading** for batch processing:

```java
ExecutorService executor = Executors.newFixedThreadPool(4);
List<Future<List<Address>>> futures = new ArrayList<>();

for (String filePath : documentPaths) {
    futures.add(executor.submit(() -> extractAddresses(filePath)));
}

// Collect results
for (Future<List<Address>> future : futures) {
    List<Address> addresses = future.get();
    // Process addresses
}
executor.shutdown();
```

3. **Cache documents** if processing the same files repeatedly

### ClassNotFoundException or NoClassDefFoundError

**Symptom:** App crashes with class-related errors despite dependency being added.

**Fix:**
- Ensure your build tool actually downloaded the JARs (check your local Maven repository)
- Verify you're using compatible Java version (JDK 8+)
- Clean and rebuild your project: `mvn clean install` or `gradle clean build`

### License Validation Errors

**Symptom:** "License not found" or "Invalid license" errors.

**Checklist:**
- [ ] License file exists at the specified path
- [ ] License file is readable (check file permissions)
- [ ] License hasn't expired
- [ ] License matches the product (GroupDocs.Signature, not another GroupDocs product)

## Practical Applications and Real-World Use Cases

Understanding how to extract address from QR code Java applications opens up tons of automation possibilities. Here are scenarios where this capability really shines:

### 1. Automated Invoice Processing

**The problem:** Your accounting department receives hundreds of supplier invoices daily, each with a QR code containing address and payment details.

**The solution:** Build a pipeline that:
- Scans incoming invoice PDFs for QR codes
- Extracts supplier addresses automatically
- Populates your ERP or accounting system without manual data entry
- Flags invoices with missing or invalid QR codes for human review

**Business impact:** A mid-sized company processing 500 invoices daily can save 2-3 hours of manual data entry per day.

### 2. Document Management Systems (DMS)

**The scenario:** Legal or medical documents often have QR codes with metadata about the document origin, department, or handling instructions.

**Implementation:**
- Scan documents on upload
- Extract address data to automatically route documents to the correct department
- Use the extracted location data to determine document retention policies
- Enable geographic-based document searches

**Example code snippet for DMS integration:**

```java
public DocumentMetadata processUploadedDocument(File document) {
    Signature signature = new Signature(document.getAbsolutePath());
    List<QrCodeSignature> qrCodes = signature.search(QrCodeSignature.class, SignatureType.QrCode);
    
    DocumentMetadata metadata = new DocumentMetadata();
    for (QrCodeSignature qr : qrCodes) {
        Address address = qr.getData(Address.class);
        if (address != null) {
            metadata.setOriginLocation(address);
            metadata.setDepartment(determineDepartmentByZip(address.getZIP()));
            break; // Use first address found
        }
    }
    return metadata;
}
```

### 3. Warehouse and Inventory Management

**Use case:** Shipping labels and packing slips with destination address QR codes.

**How it works:**
- Scan package labels as they arrive
- Extract destination addresses to verify correct delivery location
- Update inventory tracking systems with location data
- Generate routing instructions for warehouse staff

**Why it matters:** Reduces mis-shipments by catching address mismatches early in the logistics chain.

### 4. Customer Onboarding Automation

**Application:** Processing customer registration forms or contracts that include address QR codes.

**Benefits:**
- Eliminate typos from manual address entry
- Speed up KYC (Know Your Customer) verification
- Cross-reference extracted addresses with validation services
- Maintain consistent address formatting across systems

## Best Practices for Production Environments

When you're ready to deploy your QR code address extraction to production, keep these guidelines in mind:

### 1. Resource Management

**Always close Signature objects** to prevent memory leaks:

```java
Signature signature = null;
try {
    signature = new Signature(filePath);
    // ... your processing code
} finally {
    if (signature != null) {
        signature.dispose(); // Releases document resources
    }
}
```

Or better yet, use try-with-resources (Java 7+):

```java
try (Signature signature = new Signature(filePath)) {
    // Your processing code here
    // Signature will be automatically disposed
}
```

### 2. Error Handling and Logging

Don't just catch and print exceptions—log them properly for production debugging:

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

private static final Logger logger = LoggerFactory.getLogger(QRCodeExtractor.class);

public List<Address> extractAddresses(String filePath) {
    List<Address> addresses = new ArrayList<>();
    
    try (Signature signature = new Signature(filePath)) {
        List<QrCodeSignature> signatures = signature.search(QrCodeSignature.class, SignatureType.QrCode);
        
        for (QrCodeSignature qr : signatures) {
            try {
                Address address = qr.getData(Address.class);
                if (address != null) {
                    addresses.add(address);
                    logger.info("Successfully extracted address from QR code in {}", filePath);
                } else {
                    logger.warn("QR code in {} does not contain address data: {}", 
                              filePath, qr.getText());
                }
            } catch (Exception e) {
                logger.error("Error parsing QR code data in {}: {}", filePath, e.getMessage());
            }
        }
    } catch (Exception e) {
        logger.error("Failed to process document {}: {}", filePath, e.getMessage(), e);
    }
    
    return addresses;
}
```

### 3. Performance Optimization Tips

**For high-volume processing:**

- **Batch processing**: Group documents and process them in batches rather than one at a time
- **Page-specific scanning**: If you know QR codes are always on page 1, don't scan the entire document
- **Caching**: Cache License objects and reuse Signature objects when possible
- **Parallel processing**: Use ExecutorService for concurrent document processing (shown in troubleshooting section)

**Memory considerations:**

- Large PDFs can consume significant memory—monitor heap usage
- For documents over 50MB, consider processing them on a separate thread or queue
- Implement circuit breakers for documents that consistently cause issues

### 4. Validation and Data Quality

Don't trust extracted data blindly—validate it:

```java
public boolean isValidAddress(Address address) {
    if (address == null) return false;
    
    // Check required fields
    if (address.getCountry() == null || address.getCountry().isEmpty()) {
        logger.warn("Address missing country");
        return false;
    }
    
    // Validate ZIP code format (US example)
    if (address.getZIP() != null && !address.getZIP().matches("\\d{5}(-\\d{4})?")) {
        logger.warn("Invalid ZIP code format: {}", address.getZIP());
        return false;
    }
    
    // Add more validation as needed
    return true;
}
```

### 5. Security Considerations

**Important security notes:**

- **Validate file sources**: Only process documents from trusted sources
- **Scan for malicious content**: Consider integrating antivirus scanning before processing
- **Limit file sizes**: Reject files over a reasonable size (e.g., 100MB) to prevent DoS attacks
- **Sanitize extracted data**: Don't trust QR code data—sanitize before inserting into databases

## Performance Considerations

Understanding the performance characteristics of QR code extraction helps you build scalable applications. Here's what you need to know:

### Processing Speed Benchmarks

Based on typical hardware (Intel i7, 16GB RAM), you can expect:

- **Small PDFs (1-10 pages)**: 100-300ms per document
- **Medium PDFs (10-50 pages)**: 500ms-2 seconds per document
- **Large PDFs (50+ pages)**: 2-10 seconds per document

**Variables that affect speed:**
- Document size and complexity
- Number of QR codes per page
- QR code size and quality (damaged codes take longer to decode)
- Whether you're scanning all pages or specific pages

### Optimization Strategies

**1. Page-Specific Scanning**

If you know QR codes are only on certain pages:

```java
SearchOptions options = new SearchOptions();
options.setAllPages(false);
options.setPagesSetup(new PagesSetup(1, 1)); // Only scan first page
List<QrCodeSignature> signatures = signature.search(QrCodeSignature.class, options);
```

This can improve performance by 5-10x on large documents.

**2. Async Processing for Web Applications**

Don't block HTTP requests waiting for QR code extraction:

```java
@RestController
public class DocumentController {
    @Autowired
    private AsyncQRCodeProcessor processor;
    
    @PostMapping("/upload")
    public ResponseEntity<String> uploadDocument(@RequestParam("file") MultipartFile file) {
        String jobId = UUID.randomUUID().toString();
        processor.processAsync(file, jobId);
        return ResponseEntity.accepted().body("Job ID: " + jobId);
    }
    
    @GetMapping("/status/{jobId}")
    public ResponseEntity<ProcessingStatus> getStatus(@PathVariable String jobId) {
        return ResponseEntity.ok(processor.getStatus(jobId));
    }
}
```

**3. Connection Pooling for Database Operations**

If you're saving extracted addresses to a database, use connection pooling to avoid overhead:

```java
// HikariCP configuration (for Spring Boot, add to application.properties)
spring.datasource.hikari.maximum-pool-size=10
spring.datasource.hikari.minimum-idle=5
```

### Memory Management

**Monitor memory usage**, especially when processing multiple documents:

```java
Runtime runtime = Runtime.getRuntime();
long usedMemory = (runtime.totalMemory() - runtime.freeMemory()) / 1024 / 1024;
logger.info("Memory usage: {} MB", usedMemory);

if (usedMemory > 500) { // 500 MB threshold
    System.gc(); // Suggest garbage collection
    logger.warn("High memory usage detected, suggested GC");
}
```

**Best practice:** Set JVM memory limits based on your expected load:

```bash
java -Xms512m -Xmx2048m -jar your-application.jar
```

## Conclusion

You've now learned how to extract address from QR code Java applications using GroupDocs.Signature—from basic setup to production-ready implementations. Let's recap the key takeaways:

**What we covered:**
- Setting up GroupDocs.Signature for Java with Maven, Gradle, or direct download
- Implementing QR code scanning and address data extraction with complete working code
- Handling different data formats and troubleshooting common issues
- Real-world applications like invoice automation and document management
- Production best practices for performance, security, and reliability

**Your next steps:**

1. **Start experimenting**: Download the free trial and test with your own documents
2. **Explore other features**: GroupDocs.Signature supports more than just QR codes—try extracting barcodes, digital signatures, or text signatures
3. **Build something**: Apply this to a real problem in your workflow (invoice processing is a great starting point)
4. **Scale it up**: Once your proof-of-concept works, implement the production practices we discussed

**Going further:**

- Check out the [GroupDocs.Signature documentation](https://docs.groupdocs.com/signature/java/) for advanced features
- Join the [GroupDocs forum](https://forum.groupdocs.com/c/signature/) to get help from the community
- Explore batch processing capabilities for high-volume scenarios

The beauty of this approach is that it's not limited to addresses—you can extract any structured data from QR codes using the same patterns. Whether you're processing medical records, shipping manifests, or event tickets, the principles remain the same.

Ready to eliminate manual data entry from your workflows? Start with a simple proof-of-concept and scale from there. You'll be amazed how much time you can save.

## FAQ Section

**Q1: What is GroupDocs.Signature for Java?**  
A1: It's a comprehensive document signature API that allows Java developers to add, verify, search, and extract electronic signatures from documents. Unlike generic QR code scanners, it's specifically designed for document processing and handles QR codes embedded in PDFs, Word docs, images, and other formats without requiring image extraction.

**Q2: How do I obtain a temporary license for testing?**  
A2: Visit [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/) and fill out the request form. You'll receive a 30-day full-featured license via email, typically within a few hours. This lets you test all features without evaluation limitations or watermarks.

**Q3: Can I extract other data types from QR codes besides addresses?**  
A3: Absolutely! GroupDocs.Signature supports extracting any custom objects embedded in QR codes. Just create a Java class that matches your QR code's data structure (with matching field names) and use `getData(YourCustomClass.class)`. The library handles JSON deserialization automatically. Common use cases include contact information (vCard), product details, booking confirmations, and authentication tokens.

**Q4: What QR code formats are supported?**  
A4: GroupDocs.Signature supports all standard QR code types including QR Code, Micro QR Code, and DataMatrix. It can also extract data from barcodes like Code128, EAN, UPC, and others. The `getEncodeType()` method tells you exactly which format was found.

**Q5: How do I troubleshoot "Address object was not found" errors?**  
A5: This usually means the QR code doesn't contain data in the expected format. First, print the raw QR code text using `qrSignature.getText()` to see what's actually in there. The data needs to be JSON-formatted with fields matching your `Address` class. If your QR codes use a different structure, create a custom class or parse the text manually. Also verify the QR code isn't damaged or poorly scanned.

**Q6: Is it necessary to have a license for development purposes?**  
A6: You can develop and test using the free trial, which includes all features but adds watermarks to output and has some usage limitations. For serious development work, get a temporary license (30 days, free, no limitations). For production deployment, you'll need to purchase a full license to remove all restrictions.

**Q7: Can I use GroupDocs.Signature in a web application?**  
A7: Yes! GroupDocs.Signature works great in web applications (Spring Boot, Jakarta EE, etc.). Just be sure to process documents asynchronously (don't block HTTP requests) and manage resources properly. Use try-with-resources or explicit `dispose()` calls to prevent memory leaks. Consider implementing a job queue for batch processing.

**Q8: What document formats are supported besides PDF?**  
A8: GroupDocs.Signature supports over 50 document formats including: Microsoft Office (Word, Excel, PowerPoint), images (JPG, PNG, TIFF), OpenDocument formats (ODT, ODS), and various other formats. You can extract QR codes from any of these without converting to PDF first.

**Q9: How do I handle multiple QR codes in one document?**  
A9: The `search()` method returns a `List` of all QR codes found. Just loop through them as shown in Step 3 of the implementation guide. If you need to distinguish between different QR code types (address vs. contact info), check the data type or structure after extraction.

**Q10: What's the performance impact on my application?**  
A10: Processing speed depends on document size and complexity. Small PDFs (1-10 pages) typically process in 100-300ms. For high-volume applications, implement page-specific scanning, use parallel processing for batches, and consider caching frequently accessed documents. See the Performance Considerations section for detailed optimization strategies.

**Q11: Can I extract QR codes from scanned images or photos?**  
A11: Yes, but with some caveats. The QR codes need to be reasonably clear and properly oriented. Poor image quality, skewed angles, or low resolution can affect extraction accuracy. For best results, use documents with clean, well-printed QR codes. If you're working with camera photos, consider implementing image preprocessing (rotation correction, contrast enhancement).

**Q12: Is there a limit to how many documents I can process?**  
A12: With a valid license, there are no artificial limits. Practical limits depend on your hardware resources (CPU, RAM) and how you've architected your solution. For processing thousands of documents, implement proper queuing, batch processing, and resource management as discussed in the Best Practices section.

## Resources

**Documentation and Support:**
- **Full Documentation**: [GroupDocs.Signature for Java Docs](https://docs.groupdocs.com/signature/java/) - comprehensive guides, tutorials, and API references
- **API Reference**: [Java API Documentation](https://reference.groupdocs.com/signature/java/) - detailed class and method documentation
- **Community Forum**: [GroupDocs Support Forum](https://forum.groupdocs.com/c/signature/) - get help from developers and GroupDocs team
- **Downloads**: [Latest Release](https://releases.groupdocs.com/signature/java/) - download JARs and dependencies

**Licensing and Trials:**
- **Free Trial**: [Start Free Trial](https://releases.groupdocs.com/signature/java/) - test with evaluation limitations
- **Temporary License**: [Request 30-Day License](https://purchase.groupdocs.com/temporary-license/) - full features for testing
- **Purchase Options**: [Buy License](https://purchase.groupdocs.com/buy) - production licenses and pricing
