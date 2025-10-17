---
title: "Add Text Signature to PDF Java Complete Tutorial"
linktitle: "Java Text Signature Tutorial"
description: "Learn how to add text signatures to PDF and documents in Java. Step-by-step guide with GroupDocs.Signature covering position, rotation, shadows, and customization."
date: "2025-01-02"
lastmod: "2025-01-02"
weight: 1
url: "/java/text-signatures/configure-text-signatures-java-groupdocs-signature/"
keywords: "add text signature to PDF Java, Java digital signature library tutorial, customize signature appearance Java, programmatic document signing Java, Java signature with rotation, configure signature position size Java"
categories: ["Java Development", "Document Processing"]
tags: ["java-signature", "pdf-signing", "groupdocs", "digital-signatures", "document-automation"]
type: docs
---

# Add Text Signature to PDF Java Complete Tutorial

## Introduction

Need to programmatically add signatures to PDFs, Word documents, or spreadsheets in your Java application? Whether you're building a contract management system, automating invoice approval workflows, or creating digital certificates, adding customizable text signatures is often a critical requirement.

The challenge? Most Java developers start by wrestling with low-level PDF libraries like iText or Apache PDFBox, spending hours figuring out coordinate systems, font rendering, and format-specific quirks. There's a better way.

This tutorial shows you how to **add text signatures to documents in Java** using GroupDocs.Signature—a high-level library that handles the complexity for you. In just a few lines of code, you'll learn to position signatures precisely, customize their appearance with borders and shadows, apply rotation effects, and even add gradient backgrounds (way easier than you'd think).

**What You'll Master:**
- Setting up a Java signature library in under 5 minutes
- Adding basic text signatures to any document format
- Customizing signature position, size, and alignment
- Applying professional visual effects (borders, shadows, rotation)
- Handling multiple file formats (PDF, DOCX, XLSX) with identical code
- Troubleshooting common signature configuration issues

Let's start with what you'll need to follow along.

## Prerequisites

Before diving into code, make sure you've got these basics covered:

### Required Libraries, Versions, and Dependencies

You'll need GroupDocs.Signature for Java added to your project. The library supports Java 8 and above, so if you're on a recent JDK version, you're good to go. Here's how to add it depending on your build tool:

**Maven** (most common)
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle** (if that's your preference)
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Direct Download** (for manual setup):  
Grab the latest JAR from [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) and add it to your classpath.

### Environment Setup Requirements

Make sure you have:
- **JDK 8 or higher** installed (verify with `java -version`)
- Your favorite IDE (IntelliJ IDEA, Eclipse, or VS Code work great)
- Write permissions to the directory where you'll save signed documents

### Knowledge Prerequisites

This guide assumes you're comfortable with:
- Basic Java syntax (classes, methods, imports)
- File I/O operations in Java
- Working with dependencies in Maven or Gradle (just adding them, nothing fancy)

Don't worry if you haven't worked with document processing before—I'll explain everything as we go.

## Setting Up GroupDocs.Signature for Java

GroupDocs.Signature is built to make document signing painless. Unlike low-level PDF libraries where you're calculating coordinates and managing fonts manually, this library abstracts away the complexity. You work with high-level concepts (signature position, appearance, effects) and it handles the format-specific implementation.

Here's why it's popular for Java signature projects:
- **Multi-format support**: Same code works for PDF, Word, Excel, PowerPoint, and images
- **Rich customization**: Position, styling, rotation, shadows—all configurable
- **Production-ready**: Battle-tested in enterprise applications
- **Good documentation**: Plenty of examples to reference

### Getting Your License

Start by grabbing a license from [GroupDocs](https://purchase.groupdocs.com/buy). They offer:
- **Free trial**: Perfect for testing and development
- **Temporary license**: Get a 30-day full-access license for evaluation
- **Commercial license**: For production deployments

For this tutorial, the free trial works fine. You'll just see a watermark on output documents until you add a license (easy to remove later when you're ready to deploy).

### Basic Initialization

Every signature operation starts by initializing a `Signature` object that points to your document. Think of it as opening a file—you're telling the library "this is the document I want to work with."

```java
import com.groupdocs.signature.Signature;
import java.io.File;
import java.nio.file.Paths;

public class InitializeSignature {
    public static void main(String[] args) throws Exception {
        String filePath = "YOUR_DOCUMENT_DIRECTORY";
        Signature signature = new Signature(filePath);
        // Now you're ready to configure and apply signatures!
    }
}
```

**What's happening here:**
- We're importing the `Signature` class from GroupDocs
- Creating a new `Signature` instance with the path to our document
- The library automatically detects the file format (PDF, DOCX, etc.)

**Pro tip**: Use `Paths.get()` for cross-platform file paths, and always use try-with-resources to ensure proper cleanup:

```java
String docPath = Paths.get("documents", "contract.pdf").toString();
try (Signature signature = new Signature(docPath)) {
    // Your signature code here
} // Automatically closes and releases resources
```

Now that initialization is out of the way, let's actually add some signatures.

## Implementation Guide: Adding and Customizing Text Signatures

Let's build up from a basic signature to fully customized ones. Each section adds a new layer of customization you'd typically need in real applications.

### FEATURE: Initialize Signature Object

**When you need this**: Every signature operation starts here—it's like opening a document before you can modify it.

**Real-world scenario**: You're building an invoice approval system. Users upload PDFs, and approved invoices need a "Approved by [Name]" signature stamped on them.

```java
import com.groupdocs.signature.Signature;
import java.io.File;
import java.nio.file.Paths;

public class FeatureInitializeSignature {
    public static void main(String[] args) throws Exception {
        String filePath = "YOUR_DOCUMENT_DIRECTORY";
        Signature signature = new Signature(filePath);
        // The signature object is now initialized and ready.
    }
}
```

**What's happening:**
- `filePath` should point to your actual document (e.g., `"./documents/invoice.pdf"`)
- The `Signature` constructor loads the document into memory
- The library validates the file format and prepares it for signing
- If the file doesn't exist or is corrupted, you'll get an exception here (we'll cover error handling later)

**Common mistake to avoid**: Don't create a new `Signature` object for each signature you want to add. Initialize once, then add multiple signatures if needed. Creating multiple instances wastes memory.

### FEATURE: Configure Text Signature Position and Appearance

**When you need this**: You want control over where your signature appears and how it looks. This is your bread-and-butter configuration for most use cases.

**Real-world scenario**: Legal documents need signatures in the bottom-right corner, invoices need them top-right, and certificates need centered signatures. Position matters.

```java
import com.groupdocs.signature.options.sign.TextSignOptions;
import java.awt.Color;
import java.awt.Font;

public class FeatureConfigureTextSignOptions {
    public static void main(String[] args) {
        TextSignOptions options = new TextSignOptions("John Smith");
        
        // Position the signature precisely
        options.setLeft(100);   // 100 pixels from the left edge
        options.setTop(100);    // 100 pixels from the top
        options.setWidth(100);  // Signature box width
        options.setHeight(30);  // Signature box height

        // Use alignment for responsive positioning (better than hardcoding coordinates)
        options.setVerticalAlignment(com.groupdocs.signature.domain.enums.VerticalAlignment.Top);
        options.setHorizontalAlignment(com.groupdocs.signature.domain.enums.HorizontalAlignment.Right);

        // Add a professional border
        com.groupdocs.signature.domain.Border border = new com.groupdocs.signature.domain.Border();
        border.setColor(Color.GREEN);
        border.setDashStyle(com.groupdocs.signature.domain.enums.DashStyle.DashLongDashDot);
        border.setTransparency(0.5);  // Semi-transparent for subtle effect
        border.setVisible(true);
        border.setWeight(2);          // Border thickness in pixels
        options.setBorder(border);

        // Customize text appearance
        options.setForeColor(Color.RED);
        com.groupdocs.signature.domain.SignatureFont signatureFont = new com.groupdocs.signature.domain.SignatureFont();
        signatureFont.setSize(12);
        signatureFont.setFamilyName("Comic Sans MS");  // Use a professional font in production!
        options.setFont(signatureFont);
    }
}
```

**Breaking down the configuration:**

1. **Position vs. Alignment**: 
   - `setLeft()/setTop()` give you pixel-perfect control
   - `setVerticalAlignment()/setHorizontalAlignment()` are better for responsive placement (signatures stay in the corner regardless of page size)
   - You can combine both: alignment for general position, then use margins to fine-tune

2. **Border styling**: 
   - `DashStyle` options include Solid, Dash, Dot, DashDot, and more
   - `setTransparency()` accepts values from 0 (opaque) to 1 (invisible)
   - Use subtle borders (gray, thin, semi-transparent) for professional documents

3. **Font selection**:
   - Stick to common fonts (Arial, Times New Roman, Helvetica) for compatibility
   - Size 10-14 is typically readable without being obnoxious
   - Bold weight can help signatures stand out: `signatureFont.setBold(true)`

**Pro tip for dynamic positioning**: If you're signing multiple documents with different page sizes, use alignment instead of hardcoded coordinates:

```java
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
options.setMargin(new Padding(10)); // 10px margin from edges
```

This ensures your signature always appears in the bottom-right corner, regardless of whether you're signing A4, Letter, or custom-sized documents.

### FEATURE: Apply Background and Rotation Effects

**When you need this**: You want signatures that stand out visually or need angled signatures (common for watermarks or diagonal "APPROVED" stamps).

**Real-world scenario**: You're creating a certificate generator. Each certificate needs a semi-transparent background with a subtle gradient behind the signature text, rotated 15 degrees for a dynamic look.

```java
import com.groupdocs.signature.domain.Background;
import com.groupdocs.signature.domain.extensions.LinearGradientBrush;

public class FeatureApplyBackgroundAndRotation {
    public static void main(String[] args) {
        TextSignOptions options = new TextSignOptions("");
        
        // Create an eye-catching background
        Background background = new Background();
        background.setColor(Color.LIGHT_GRAY);    // Base color
        background.setTransparency(0.5);           // 50% transparent (subtle)
        background.setBrush(new LinearGradientBrush(Color.GREEN, Color.DARK_GRAY, 0));
        options.setBackground(background);

        // Rotate for visual interest (or to prevent easy removal)
        options.setRotationAngle(45);  // 45-degree angle
    }
}
```

**Understanding the background settings:**

1. **Solid color vs. gradient**:
   - Solid: Just set `background.setColor()` with no brush
   - Gradient: Use `LinearGradientBrush` for smooth color transitions
   - The third parameter (0 in the example) controls gradient angle in degrees

2. **Transparency guidelines**:
   - 0.0 = completely opaque (blocks content behind it)
   - 0.5 = semi-transparent (ideal for backgrounds)
   - 0.9 = barely visible (good for subtle watermarks)

3. **Rotation angles**:
   - 0° = horizontal (default)
   - 45° = diagonal (common for "CONFIDENTIAL" or "DRAFT" stamps)
   - 90° = vertical (rarely used but possible)
   - Negative values rotate counter-clockwise

**Common use cases by rotation angle:**
- **0°**: Standard signatures, approval stamps
- **15-30°**: Certificate signatures (adds elegance)
- **45°**: Watermarks, status stamps (DRAFT, CONFIDENTIAL)
- **-5° to -10°**: Handwritten effect (mimics slight tilt)

**Performance note**: Gradients add minimal overhead, but avoid complex multi-stop gradients if you're signing hundreds of documents in batch operations.

### FEATURE: Add Professional Shadow Effects

**When you need this**: Shadows add depth and make signatures look more "printed" and official rather than flatly overlaid on the document.

**Real-world scenario**: You're creating executive-level contracts where visual polish matters. A subtle shadow makes signatures look professionally printed rather than digitally pasted.

```java
import com.groupdocs.signature.domain.extensions.signoptions.TextShadow;

public class FeatureAddTextShadow {
    public static void main(String[] args) {
        TextSignOptions options = new TextSignOptions("");
        
        // Configure shadow for depth and professionalism
        TextShadow shadow = new TextShadow();
        shadow.setColor(Color.ORANGE);  // Shadow color (usually dark gray or black)
        shadow.setAngle(135);           // Light source angle (135° = top-left)
        shadow.setBlur(5);              // Blur radius (higher = softer shadow)
        shadow.setDistance(4);          // Offset from text (in pixels)
        shadow.setTransparency(0.2);    // Shadow opacity

        // Add the shadow effect to signature extensions
        options.getExtensions().add(shadow);
    }
}
```

**Shadow configuration explained:**

1. **Color selection**:
   - Black (`Color.BLACK`) with transparency is most realistic
   - Dark gray for softer, professional look
   - Avoid bright colors unless you want a stylized effect

2. **Angle guide** (imagine a clock):
   - 135° (default) = light from top-left, shadow bottom-right
   - 45° = light from top-right, shadow bottom-left
   - 180° = light directly above, shadow directly below
   - Stick to 120-150° for natural-looking shadows

3. **Blur amount**:
   - 0-2: Sharp shadow (harsh, rarely looks good)
   - 3-6: Standard shadow (professional)
   - 7+: Very soft shadow (subtle, elegant)

4. **Distance**:
   - 2-3px: Subtle depth
   - 4-6px: Noticeable but not excessive
   - 7+px: Dramatic, can look unrealistic

**Recommended settings for different document types:**

```java
// Legal documents (subtle and professional)
shadow.setColor(new Color(0, 0, 0, 50));  // Semi-transparent black
shadow.setBlur(4);
shadow.setDistance(3);
shadow.setAngle(135);

// Certificates (bold and clear)
shadow.setColor(new Color(0, 0, 0, 80));
shadow.setBlur(6);
shadow.setDistance(5);
shadow.setAngle(135);

// Invoices (minimal distraction)
shadow.setColor(new Color(0, 0, 0, 30));
shadow.setBlur(3);
shadow.setDistance(2);
shadow.setAngle(135);
```

**Pro tip**: Test shadow settings on both light and dark backgrounds. A shadow that looks great on white paper might be invisible on a light gray background.

## Common Pitfalls and How to Avoid Them

Even experienced developers hit these snags when implementing signature functionality. Here's what to watch out for:

### 1. File Path Issues

**Problem**: Your code throws `FileNotFoundException` even though the file exists.

**Why it happens**: Relative paths behave differently depending on where you run the code (IDE vs. command line vs. deployed JAR).

**Solution**:
```java
// ❌ Risky: Might work in IDE but fail in production
String filePath = "documents/contract.pdf";

// ✅ Better: Use absolute paths or workspace-relative paths
String filePath = Paths.get(System.getProperty("user.dir"), "documents", "contract.pdf").toString();

// ✅ Best: Load from resources for embedded files
InputStream stream = getClass().getResourceAsStream("/templates/contract.pdf");
Signature signature = new Signature(stream);
```

### 2. Signature Position Goes Off-Page

**Problem**: Your signature appears cut off or not at all because coordinates exceed page dimensions.

**Why it happens**: You hardcoded coordinates without checking page size, or forgot that coordinates are in pixels, not percentages.

**Solution**:
```java
// ✅ Use alignment instead of hardcoded positions
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
options.setMargin(new Padding(20)); // 20px from edges

// If you must use coordinates, calculate them dynamically:
// (This is advanced—most apps can just use alignment)
```

### 3. Memory Leaks from Unclosed Signatures

**Problem**: Your application slows down or crashes after processing multiple documents.

**Why it happens**: `Signature` objects hold file handles and memory. Forgetting to close them causes resource leaks.

**Solution**:
```java
// ❌ Risky: Must remember to call signature.dispose()
Signature signature = new Signature(filePath);
// ... your code ...
signature.dispose();

// ✅ Better: Use try-with-resources (automatic cleanup)
try (Signature signature = new Signature(filePath)) {
    // Your signature code here
} // Automatically calls dispose() even if exceptions occur
```

### 4. Font Not Rendering Correctly

**Problem**: Your chosen font doesn't appear in the signed document—it defaults to a generic font.

**Why it happens**: The font you specified isn't installed on the server where your code runs, or isn't embedded in the output.

**Solution**:
```java
// ✅ Stick to universally available fonts
signatureFont.setFamilyName("Arial");        // Safe
signatureFont.setFamilyName("Times New Roman"); // Safe
signatureFont.setFamilyName("Helvetica");    // Safe

// ❌ Avoid custom or OS-specific fonts unless you embed them
signatureFont.setFamilyName("My Custom Font"); // Will fail on most servers
```

### 5. Transparency Not Working as Expected

**Problem**: Your semi-transparent signature or background appears fully opaque.

**Why it happens**: Some PDF viewers don't properly render transparency, or you're using RGB colors instead of RGBA.

**Solution**:
```java
// ✅ Use RGBA colors with alpha channel
Color transparentBlack = new Color(0, 0, 0, 128); // 128 = 50% transparency
options.setForeColor(transparentBlack);

// Also set transparency on the component itself
options.getBackground().setTransparency(0.5);

// Test on multiple PDF viewers (Adobe Reader, Chrome, Firefox)
```

## Troubleshooting Guide

### Issue: "Could not load file or assembly" Error

**Symptoms**: Exception when initializing `Signature` object.

**Causes**:
1. GroupDocs.Signature JAR not in classpath
2. Version mismatch between dependencies
3. Corrupted download

**Fix**:
1. Verify dependency is in your `pom.xml` or `build.gradle`
2. Run `mvn clean install` or `gradle clean build`
3. Check for duplicate versions in dependency tree
4. Re-download the library if necessary

### Issue: Signature Appears But Text Is Invisible

**Symptoms**: A box or border appears where signature should be, but text is missing.

**Causes**:
1. Font color matches background color
2. Font size set to 0 or negative value
3. Text is empty string

**Fix**:
```java
// Verify text content
TextSignOptions options = new TextSignOptions("John Smith"); // ✅ Not empty

// Check color contrast
options.setForeColor(Color.BLACK);
options.getBackground().setColor(Color.WHITE);

// Verify font size
signatureFont.setSize(12); // ✅ Reasonable size
```

### Issue: Signed Document Is Corrupted or Won't Open

**Symptoms**: After signing, the output file can't be opened or displays errors.

**Causes**:
1. Writing to same file you're reading from
2. File stream not properly closed
3. Disk space full
4. Process interrupted mid-write

**Fix**:
```java
// ✅ Always write to a different file
String inputPath = "original.pdf";
String outputPath = "original_signed.pdf";

try (Signature signature = new Signature(inputPath)) {
    TextSignOptions options = new TextSignOptions("Signed");
    SignResult result = signature.sign(outputPath, options);
    
    // Verify the operation succeeded
    if (result.getSucceeded().size() > 0) {
        System.out.println("Signature applied successfully");
    }
}
```

### Issue: Performance Is Slow for Large PDFs

**Symptoms**: Signing a 50-page PDF takes 10+ seconds.

**Causes**:
1. Loading entire document into memory
2. Re-scanning document for each signature
3. Not using page-specific signing

**Fix**:
```java
// ✅ Sign specific pages only
TextSignOptions options = new TextSignOptions("Signature");
options.setPageNumber(1);        // Sign only page 1
options.setAllPages(false);      // Don't apply to all pages

// Or sign specific page range
options.setPagesSetup(new PagesSetup());
options.getPagesSetup().setFirstPage(1);
options.getPagesSetup().setLastPage(1);
```

## Best Practices for Production Applications

### 1. Centralize Signature Configuration

**Why**: Maintain consistent signature appearance across your application and make updates easier.

```java
public class SignatureConfig {
    public static TextSignOptions getDefaultOptions(String signerName) {
        TextSignOptions options = new TextSignOptions(signerName);
        
        // Standard position
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        options.setHorizontalAlignment(HorizontalAlignment.Right);
        options.setMargin(new Padding(20));
        
        // Company standard font
        SignatureFont font = new SignatureFont();
        font.setFamilyName("Arial");
        font.setSize(10);
        font.setBold(true);
        options.setFont(font);
        
        // Subtle professional styling
        options.setForeColor(new Color(30, 30, 30));
        Border border = new Border();
        border.setColor(Color.GRAY);
        border.setWeight(1);
        options.setBorder(border);
        
        return options;
    }
}

// Usage in your application
TextSignOptions options = SignatureConfig.getDefaultOptions("John Smith");
```

### 2. Validate Input Files Before Processing

**Why**: Fail fast with clear error messages instead of cryptic exceptions during signing.

```java
public boolean isValidDocument(String filePath) {
    File file = new File(filePath);
    
    // Check existence and readability
    if (!file.exists() || !file.canRead()) {
        System.err.println("File not accessible: " + filePath);
        return false;
    }
    
    // Check file size (e.g., max 50MB)
    if (file.length() > 50 * 1024 * 1024) {
        System.err.println("File too large: " + file.length() + " bytes");
        return false;
    }
    
    // Check file extension
    String ext = filePath.substring(filePath.lastIndexOf(".") + 1).toLowerCase();
    if (!Arrays.asList("pdf", "docx", "xlsx").contains(ext)) {
        System.err.println("Unsupported format: " + ext);
        return false;
    }
    
    return true;
}
```

### 3. Handle Exceptions Gracefully

**Why**: Signature failures shouldn't crash your application—provide meaningful feedback to users.

```java
public boolean signDocument(String inputPath, String outputPath, String signerName) {
    try (Signature signature = new Signature(inputPath)) {
        TextSignOptions options = SignatureConfig.getDefaultOptions(signerName);
        SignResult result = signature.sign(outputPath, options);
        
        if (result.getSucceeded().size() > 0) {
            System.out.println("Document signed successfully");
            return true;
        } else {
            System.err.println("Signature failed: " + result.getFailed().get(0).getError());
            return false;
        }
        
    } catch (Exception e) {
        System.err.println("Error signing document: " + e.getMessage());
        e.printStackTrace();
        
        // Optionally: Log to monitoring system, notify admin, etc.
        return false;
    }
}
```

### 4. Optimize for Batch Processing

**Why**: If you're signing multiple documents, reusing resources saves time and memory.

```java
public void signMultipleDocuments(List<String> filePaths, String signerName) {
    TextSignOptions options = SignatureConfig.getDefaultOptions(signerName);
    
    for (String inputPath : filePaths) {
        String outputPath = inputPath.replace(".pdf", "_signed.pdf");
        
        try (Signature signature = new Signature(inputPath)) {
            signature.sign(outputPath, options);
        } catch (Exception e) {
            System.err.println("Failed to sign " + inputPath + ": " + e.getMessage());
            // Continue with next document instead of failing entire batch
        }
    }
}
```

### 5. Test with Real-World Documents

**Why**: Sample PDFs from the internet might work perfectly while your production documents fail due to unusual formatting, encryption, or form fields.

**Testing checklist**:
- ✅ Scanned documents (image-based PDFs)
- ✅ Text-based PDFs from different tools (Word export, Google Docs, LibreOffice)
- ✅ PDFs with existing form fields
- ✅ Password-protected PDFs
- ✅ Multi-page documents (1, 5, 50, 500 pages)
- ✅ Documents with unusual page sizes (A5, Legal, custom dimensions)
- ✅ PDFs with embedded fonts vs. system fonts

## Practical Use Cases and Examples

### 1. Automated Invoice Approval System

**Scenario**: Finance team uploads invoices for approval. Once approved, the system adds an "Approved by [Name] - [Date]" signature.

```java
public void approveInvoice(String invoicePath, String approverName) {
    String outputPath = invoicePath.replace(".pdf", "_approved.pdf");
    
    try (Signature signature = new Signature(invoicePath)) {
        String signatureText = String.format("Approved by %s\n%s", 
            approverName, 
            LocalDate.now().format(DateTimeFormatter.ofPattern("MMM dd, yyyy")));
        
        TextSignOptions options = new TextSignOptions(signatureText);
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        options.setHorizontalAlignment(HorizontalAlignment.Left);
        options.setMargin(new Padding(30));
        
        SignatureFont font = new SignatureFont();
        font.setFamilyName("Arial");
        font.setSize(9);
        options.setFont(font);
        options.setForeColor(new Color(0, 100, 0)); // Dark green
        
        signature.sign(outputPath, options);
    }
}
```

### 2. Certificate Generation with Centered Signature

**Scenario**: Educational platform generates completion certificates with student names.

```java
public void generateCertificate(String templatePath, String studentName) {
    String outputPath = "certificates/" + studentName.replace(" ", "_") + ".pdf";
    
    try (Signature signature = new Signature(templatePath)) {
        TextSignOptions options = new TextSignOptions(studentName);
        
        // Center the name on the page
        options.setVerticalAlignment(VerticalAlignment.Center);
        options.setHorizontalAlignment(HorizontalAlignment.Center);
        options.setTop(-50); // Slightly above center
        
        // Elegant, certificate-appropriate font
        SignatureFont font = new SignatureFont();
        font.setFamilyName("Times New Roman");
        font.setSize(24);
        font.setBold(true);
        options.setFont(font);
        options.setForeColor(new Color(0, 0, 128)); // Navy blue
        
        signature.sign(outputPath, options);
    }
}
```

### 3. Confidential Watermark on Reports

**Scenario**: Add a diagonal "CONFIDENTIAL" watermark across every page of sensitive reports.

```java
public void addConfidentialWatermark(String reportPath) {
    String outputPath = reportPath.replace(".pdf", "_confidential.pdf");
    
    try (Signature signature = new Signature(reportPath)) {
        TextSignOptions options = new TextSignOptions("CONFIDENTIAL");
        
        // Center and rotate for diagonal watermark
        options.setVerticalAlignment(VerticalAlignment.Center);
        options.setHorizontalAlignment(HorizontalAlignment.Center);
        options.setRotationAngle(45);
        options.setAllPages(true); // Apply to every page
        
        // Large, semi-transparent text
        SignatureFont font = new SignatureFont();
        font.setFamilyName("Arial");
        font.setSize(72);
        font.setBold(true);
        options.setFont(font);
        options.setForeColor(new Color(255, 0, 0, 50)); // Semi-transparent red
        
        signature.sign(outputPath, options);
    }
}
```

### 4. Multi-Signature Workflow (Sign in Multiple Locations)

**Scenario**: Contracts need signatures from multiple parties in designated areas.

```java
public void addMultipleSignatures(String contractPath, Map<String, String> signers) {
    String outputPath = contractPath.replace(".pdf", "_signed.pdf");
    
    try (Signature signature = new Signature(contractPath)) {
        List<SignOptions> allOptions = new ArrayList<>();
        
        int verticalOffset = 0;
        for (Map.Entry<String, String> signer : signers.entrySet()) {
            String role = signer.getKey();   // e.g., "Buyer", "Seller", "Witness"
            String name = signer.getValue(); // e.g., "John Smith"
            
            TextSignOptions options = new TextSignOptions(role + ": " + name);
            options.setLeft(50);
            options.setTop(700 + verticalOffset); // Stack signatures vertically
            options.setWidth(200);
            options.setHeight(30);
            
            SignatureFont font = new SignatureFont();
            font.setFamilyName("Arial");
            font.setSize(11);
            options.setFont(font);
            
            allOptions.add(options);
            verticalOffset += 40; // Space between signatures
        }
        
        signature.sign(outputPath, allOptions);
    }
}
```

### 5. Dynamic Timestamp Signatures

**Scenario**: Add current date and time to documents for audit trails.

```java
public void addTimestampSignature(String documentPath, String userName) {
    String outputPath = documentPath.replace(".pdf", "_timestamped.pdf");
    
    try (Signature signature = new Signature(documentPath)) {
        // Format: "Signed by John Smith on Oct 17, 2025 at 2:30 PM"
        String timestamp = String.format("Signed by %s\n%s", 
            userName,
            LocalDateTime.now().format(DateTimeFormatter.ofPattern("MMM dd, yyyy 'at' h:mm a")));
        
        TextSignOptions options = new TextSignOptions(timestamp);
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        options.setHorizontalAlignment(HorizontalAlignment.Right);
        options.setMargin(new Padding(20));
        
        SignatureFont font = new SignatureFont();
        font.setFamilyName("Courier New"); // Monospace for timestamp feel
        font.setSize(8);
        options.setFont(font);
        options.setForeColor(Color.DARK_GRAY);
        
        signature.sign(outputPath, options);
    }
}
```

## Frequently Asked Questions

### Can I sign documents other than PDFs?

Yes! GroupDocs.Signature supports **20+ formats** including:
- **Office documents**: DOCX, XLSX, PPTX
- **Images**: PNG, JPG, BMP, TIFF
- **Other**: ODT, ODS, HTML, and more

The code remains identical regardless of format—just change the file extension. The library handles format-specific implementation automatically.

```java
// Same code works for Word documents
try (Signature signature = new Signature("contract.docx")) {
    // ... your signature code ...
    signature.sign("contract_signed.docx", options);
}
```

### How do I sign specific pages instead of all pages?

Use `setPageNumber()` or `setPagesSetup()` for precise control:

```java
// Sign only page 1
options.setPageNumber(1);
options.setAllPages(false);

// Or sign a range (pages 1-3)
PagesSetup pagesSetup = new PagesSetup();
pagesSetup.setFirstPage(1);
pagesSetup.setLastPage(3);
options.setPagesSetup(pagesSetup);

// Or sign specific pages (e.g., pages 1, 3, and 5)
options.setAllPages(false);
options.setPagesSetup(new PagesSetup());
options.getPagesSetup().setEvenPages(false);
options.getPagesSetup().setOddPages(false);
// Then set specific page numbers as needed
```

### Can I use custom fonts that aren't installed system-wide?

Yes, but with caveats. You can specify any font name, but:
1. The font must be **installed on the server** running your Java code
2. Or, use **embedded fonts** in your documents (more complex)
3. For maximum compatibility, **stick to standard fonts**: Arial, Times New Roman, Helvetica, Courier

For custom fonts, you'd need to ensure they're available:
```java
// This requires the font to be installed
signatureFont.setFamilyName("MyCustomFont");

// Safer approach: Use web-safe fonts
signatureFont.setFamilyName("Arial"); // Works everywhere
```

### How can I verify if a signature was successfully applied?

Check the `SignResult` object returned by the `sign()` method:

```java
SignResult result = signature.sign(outputPath, options);

if (result.getSucceeded().size() > 0) {
    System.out.println("✓ Signature applied successfully");
    System.out.println("Total signatures: " + result.getSucceeded().size());
} else if (result.getFailed().size() > 0) {
    System.err.println("✗ Signature failed");
    System.err.println("Error: " + result.getFailed().get(0).getError());
}
```

### What's the difference between digital signatures and text signatures?

Great question—they serve different purposes:

**Text signatures** (what this tutorial covers):
- Visual representation only
- Can be added, modified, or removed easily
- Used for labels, stamps, watermarks, approval marks
- No cryptographic verification
- Think: "Approved by John Smith" stamp

**Digital signatures** (different feature):
- Cryptographically secure
- Uses certificates (PKI)
- Cannot be modified without invalidating signature
- Used for legal documents, contracts requiring non-repudiation
- Think: DocuSign-style signatures

GroupDocs.Signature supports both. For legal binding signatures, use digital signatures with certificates. For internal workflows and visual indicators, text signatures (this tutorial) work great.

### Can I combine multiple signature styles in one document?

Absolutely! Just create multiple `SignOptions` objects and pass them as a list:

```java
try (Signature signature = new Signature("document.pdf")) {
    // First signature: Approval stamp
    TextSignOptions approval = new TextSignOptions("APPROVED");
    approval.setVerticalAlignment(VerticalAlignment.Top);
    approval.setHorizontalAlignment(HorizontalAlignment.Right);
    
    // Second signature: Timestamp
    TextSignOptions timestamp = new TextSignOptions("Signed: " + LocalDate.now());
    timestamp.setVerticalAlignment(VerticalAlignment.Bottom);
    timestamp.setHorizontalAlignment(HorizontalAlignment.Left);
    
    // Apply both
    List<SignOptions> allSignatures = Arrays.asList(approval, timestamp);
    signature.sign("output.pdf", allSignatures);
}
```

### How much memory does this use for large PDFs?

GroupDocs.Signature is designed to be memory-efficient, but here are typical usage patterns:

- **Small PDFs** (< 5MB, < 50 pages): 20-50MB RAM
- **Medium PDFs** (5-20MB, 50-200 pages): 50-150MB RAM
- **Large PDFs** (20MB+, 200+ pages): 150-500MB RAM

**Tips to reduce memory usage**:
1. Sign specific pages instead of all pages
2. Process documents sequentially instead of loading multiple at once
3. Use try-with-resources to ensure immediate cleanup
4. Avoid keeping `Signature` objects open longer than necessary

### Can I extract existing signatures from documents?

Yes, GroupDocs.Signature can search for and extract existing signatures:

```java
try (Signature signature = new Signature("signed_document.pdf")) {
    List<TextSignature> signatures = signature.search(TextSignature.class);
    
    for (TextSignature sig : signatures) {
        System.out.println("Found signature: " + sig.getText());
        System.out.println("Position: " + sig.getLeft() + ", " + sig.getTop());
    }
}
```

This is useful for:
- Verifying documents are signed
- Extracting signer information
- Audit trails and compliance checks

## Performance Considerations

### Memory Management

When signing multiple documents in production:

```java
// ✅ Good: Process sequentially with proper cleanup
public void signBatch(List<String> files) {
    for (String file : files) {
        try (Signature signature = new Signature(file)) {
            // Sign document
            signature.sign(file.replace(".pdf", "_signed.pdf"), options);
        } // Auto-cleanup after each document
    }
}

// ❌ Bad: Loading all documents at once
public void signBatchBad(List<String> files) {
    List<Signature> signatures = new ArrayList<>();
    for (String file : files) {
        signatures.add(new Signature(file)); // Memory leak!
    }
    // ... signing code ...
}
```

### Optimize for Speed

If you're signing hundreds of documents:

1. **Reuse configuration objects**:
```java
TextSignOptions options = getStandardOptions(); // Create once

for (String file : files) {
    try (Signature sig = new Signature(file)) {
        sig.sign(file + "_signed", options); // Reuse options
    }
}
```

2. **Sign only necessary pages**:
```java
// Instead of all pages
options.setAllPages(false);
options.setPageNumber(1); // Just page 1
```

3. **Use multi-threading for independent documents**:
```java
ExecutorService executor = Executors.newFixedThreadPool(4);
files.forEach(file -> executor.submit(() -> signDocument(file)));
executor.shutdown();
```

### File I/O Optimization

- **Use SSDs** for document storage when possible
- **Avoid network drives** for high-volume signing (copy locally first)
- **Monitor disk space**—signed documents can be 5-10% larger

## Conclusion

You've now mastered the essentials of adding text signatures to documents in Java using GroupDocs.Signature. Let's recap what you've learned:

**Core Skills You've Gained:**
- Setting up and initializing GroupDocs.Signature in any Java project
- Configuring text signatures with precise positioning and styling
- Applying professional visual effects (borders, shadows, rotation, gradients)
- Handling multiple document formats with identical code
- Troubleshooting common signature implementation issues
- Following production-ready best practices

**Key Takeaways:**
1. **Use alignment over hardcoded positions** for responsive signature placement across different page sizes
2. **Always use try-with-resources** to prevent memory leaks
3. **Test with real production documents**, not just sample PDFs
4. **Centralize configuration** for consistent branding and easier maintenance
5. **Handle exceptions gracefully** to provide meaningful feedback

**Next Steps to Level Up:**
- Explore **digital signatures with certificates** for legally binding documents
- Implement **QR code signatures** for document verification
- Add **image-based signatures** (scanned signatures, company logos)
- Build **signature workflows** with approval chains
- Integrate with **cloud storage** (AWS S3, Azure Blob, Google Drive)

**Need More Help?**
- [GroupDocs.Signature Documentation](https://docs.groupdocs.com/signature/java/) - Comprehensive API reference
- [Support Forum](https://forum.groupdocs.com/c/signature) - Community help and official support
