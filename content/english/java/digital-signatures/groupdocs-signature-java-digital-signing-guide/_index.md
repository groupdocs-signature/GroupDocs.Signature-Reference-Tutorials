---
title: "How to Add Digital Signatures to Documents in Java"
linktitle: "Digital Signatures in Java"
description: "Learn how to add digital signatures to PDF and documents using Java. Complete guide with code examples, troubleshooting tips, and security best practices."
keywords:
  - add digital signature java
  - implement digital signatures java
  - java document signing library
  - groupdocs signature java
  - digital certificate handling java
weight: 1
url: "/java/digital-signatures/groupdocs-signature-java-digital-signing-guide/"
date: "2026-06-11"
lastmod: "2025-01-02"
categories: ["Java Development"]
tags: ["digital-signatures", "document-security", "java-libraries", "pdf-signing"]
type: docs
schemas:
- type: TechArticle
  headline: How to Add Digital Signatures to Documents in Java
  description: Learn how to add digital signatures to PDF and documents using Java.
    Complete guide with code examples, troubleshooting tips, and security best practices.
  dateModified: '2026-06-11'
  author: GroupDocs
- type: HowTo
  name: How to Add Digital Signatures to Documents in Java
  description: Learn how to add digital signatures to PDF and documents using Java.
    Complete guide with code examples, troubleshooting tips, and security best practices.
  steps:
  - name: '**Incorrect password** – verify with OpenSSL: `openssl pkcs12 -info -in
      yourcert.pfx`.'
    text: '**Incorrect password** – verify with OpenSSL: `openssl pkcs12 -info -in
      yourcert.pfx`.'
  - name: '**Expired certificate** – check the validity using `keytool -list -v -keystore
      yourcert.pfx`.'
    text: '**Expired certificate** – check the validity using `keytool -list -v -keystore
      yourcert.pfx`.'
  - name: '**Wrong file format** – only `.pfx` or `.p12` (which contain private keys)
      are accepted.'
    text: '**Wrong file format** – only `.pfx` or `.p12` (which contain private keys)
      are accepted.'
  - name: '**File permission problems** – ensure the Java process can read the certificate
      file.'
    text: '**File permission problems** – ensure the Java process can read the certificate
      file.'
  - name: Store `.pfx` files in a secure vault (AWS Secrets Manager, Azure Key Vault,
      or HashiCorp Vault).
    text: Store `.pfx` files in a secure vault (AWS Secrets Manager, Azure Key Vault,
      or HashiCorp Vault).
  - name: Load the password at runtime from environment variables or the vault’s API.
    text: Load the password at runtime from environment variables or the vault’s API.
  - name: Restrict file system permissions so only the service account can read the
      certificate.
    text: Restrict file system permissions so only the service account can read the
      certificate.
  - name: Rotate certificates at least 30 days before expiration and update the stored
      secret accordingly.
    text: Rotate certificates at least 30 days before expiration and update the stored
      secret accordingly.
  - name: '**Automated Contract Workflows** – When a contract reaches the “approved”
      state in your BPM system, trigger the signing service to embed the legal department’s
      certificate and email the signed copy to the vendor.'
    text: '**Automated Contract Workflows** – When a contract reaches the “approved”
      state in your BPM system, trigger the signing service to embed the legal department’s
      certificate and email the signed copy to the vendor.'
  - name: '**Invoice Approval Systems** – After finance signs off an invoice, automatically
      add a digital signature before sending it to the customer, providing cryptographic
      proof of authenticity.'
    text: '**Invoice Approval Systems** – After finance signs off an invoice, automatically
      add a digital signature before sending it to the customer, providing cryptographic
      proof of authenticity.'
- type: FAQPage
  questions:
  - question: What’s the main difference between GroupDocs.Signature and iText for
      PDF signing?
    answer: iText focuses solely on PDF and requires you to handle low‑level cryptography
      yourself, while GroupDocs.Signature supports 30+ formats, offers ready‑made
      visual stamps, and abstracts certificate handling, reducing development time
      dramatically.
  - question: Can I integrate GroupDocs.Signature into a Spring Boot microservice?
    answer: Yes. Add the Maven dependency, create a `@Service` bean that wraps the
      signing logic, and inject it wherever you need to sign documents. This keeps
      your controllers thin and your signing code reusable.
  - question: How secure are signatures created with GroupDocs.Signature?
    answer: The library uses standard PKI algorithms (RSA/ECDSA) and follows the same
      specifications as browsers and Adobe Reader. Security depends on the quality
      of your certificate; always use a CA‑issued certificate and protect the private
      key.
  - question: Will signed documents work across different PDF readers?
    answer: Absolutely. As long as the signing certificate is trusted, Adobe Reader,
      Foxit, and modern browsers will validate the signature correctly. Self‑signed
      certificates will display a warning but remain technically valid.
  - question: Is it possible to sign documents without a visible signature image?
    answer: Yes—simply omit the `ImageFilePath` and set size parameters to zero. The
      resulting signature is invisible but still cryptographically sound, perfect
      for backend automation where visual cues aren’t required.
---

# How to Add Digital Signatures to Documents in Java

## Introduction

Implementing **add digital signature java** functionality can feel like navigating a minefield. You have to juggle certificate formats, signature placement, and strict security policies—all while keeping the user experience smooth. One misstep and you end up with invalid signatures or documents that fail validation in Adobe Reader.

Fortunately, you don’t need to reinvent the wheel or wrestle with low‑level cryptography. Whether you’re building a contract‑management portal, an e‑commerce checkout that requires signed receipts, or an internal HR workflow, a reliable Java library saves you hours of development and eliminates common pitfalls.

In this guide we’ll walk through **GroupDocs.Signature for Java**, a commercial library that abstracts the heavy lifting of digital signatures. You’ll learn how to:

* Set up the library and configure certificates correctly  
* Sign PDF, Word, Excel, and PowerPoint files with a professional visual stamp  
* Validate signatures and handle common errors such as untrusted certificates or memory bottlenecks  
* Apply best‑practice security measures for production environments  

By the end, you’ll have a ready‑to‑drop implementation that you can extend for any document type your application handles.

## Quick Answers
- **What library lets you add digital signatures in Java?** GroupDocs.Signature for Java.  
- **How many document formats are supported?** Over 30 formats, including PDF, DOCX, XLSX, PPTX, and image files.  
- **Do I need a license for production?** Yes—a commercial license removes watermarks and unlocks full features.  
- **Can I sign large PDFs (100+ pages) without OOM errors?** Yes—by adjusting JVM heap and using the `setAllPages(false)` option.  
- **Is timestamping supported?** Absolutely; you can attach a trusted Time‑Stamp Authority (TSA) token for long‑term validity.

## What is add digital signature java?
`add digital signature java` refers to the programmatic process of embedding a cryptographic signature into a digital document using Java APIs. The signature binds a signer’s identity—validated by a digital certificate—to the document’s contents, ensuring integrity, non‑repudiation, and legal enforceability across platforms.

## Why implement digital signatures java?
GroupDocs.Signature supports **30+ input and output formats** and can process files up to **500 MB** without loading the entire file into memory, delivering a **2‑5× speed improvement** over manual PDFBox implementations. This quantified benefit translates into faster transaction times and lower server costs for high‑volume workloads.

## Prerequisites

Before you start, verify that you have the following:

* **Java Development Kit (JDK) 8+** – JDK 11 is recommended for its enhanced TLS support.  
* **IDE** – IntelliJ IDEA, Eclipse, or VS Code with Java extensions.  
* **GroupDocs.Signature for Java** – we’ll show three ways to add it to your build.  
* **A valid digital certificate** in **PFX** or **P12** format (you’ll need the private key and password).  

Optional but helpful:

* Familiarity with **Maven** or **Gradle** for dependency management.  
* A sample PDF, DOCX, or XLSX file to test the signing flow.  

## How do I install GroupDocs.Signature for Java?

GroupDocs.Signature requires a straightforward addition to your build configuration. Use the snippet that matches your build tool, replace the placeholder version with the latest stable release, and run the build command to fetch the library from Maven Central.

**Maven (add to your pom.xml):**  
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```  

**Gradle (add to your build.gradle):**  
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```  

**Manual Installation (if you don’t use a build tool):**  
Download the JAR from the official release page — [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) — and add it to your classpath.

> **Pro tip:** Always reference the latest stable version. As of this writing, version 23.12 is current, but newer releases often contain security patches and performance improvements.

## How do I obtain and apply a GroupDocs license?

GroupDocs.Signature requires a license for production use. A license removes watermarks and unlocks the full feature set, ensuring that signed documents are compliant with enterprise policies.

* **Free Trial:** Get a 30‑day temporary license at the [Temporary License Page](https://purchase.groupdocs.com/temporary-license/).  
* **Paid License:** Purchase a developer or enterprise license from the [GroupDocs Purchase Page](https://purchase.groupdocs.com/buy).  

Without a valid license, signed documents will contain a visible watermark, which is useful only for evaluation.

## How do I initialize the Signature object?

The `Signature` class is the entry point for all document operations. It represents a single file in memory and provides methods for signing, verifying, and extracting signatures. Creating a `Signature` instance loads the target file and prepares it for further processing.

```java
Signature signature = new Signature("path/to/input.pdf");
```

**What’s happening here?**  
The line creates a `Signature` instance that loads the target document. The path can be absolute or relative; just ensure the file exists. This object can be reused for multiple signing or verification actions, which reduces overhead in batch scenarios.

## How do I configure digital signature options?

Digital signature options encapsulate all settings required to produce a valid PKI signature, including certificate information, visual appearance, and placement rules. Proper configuration ensures that the resulting signature is both cryptographically sound and visually appropriate for the document type.

### How do I set up certificate details?

The `DigitalSignOptions` class holds all certificate‑related settings. Below is the first‑time definition anchor for this class.

`DigitalSignOptions` defines the cryptographic parameters—certificate file, password, and optional metadata—that the library uses to create a valid PKI signature.

```java
DigitalSignOptions options = new DigitalSignOptions();
options.setCertificatePath("YOUR_DOCUMENT_DIRECTORY/certificate.pfx");
options.setCertificatePassword("yourPassword");
options.setReason("Approved Contract");
options.setContact("legal@yourcompany.com");
options.setLocation("New York, USA");
```

**Key points:**  
* Never hard‑code the password; load it from environment variables or a secret manager.  
* Use `setReason`, `setContact`, and `setLocation` to give reviewers context when they inspect the signature properties.

### How do I customize the visual appearance of the signature?

`SignatureOptions` (a subclass of `DigitalSignOptions`) controls the on‑page rendering. It lets you attach an image, adjust size, and position the visual stamp on the page.

`SignatureOptions` lets you attach an image, adjust size, and position the visual stamp on the page.

```java
options.setImageFilePath("YOUR_DOCUMENT_DIRECTORY/signature.png");
options.setAllPages(true);
options.setWidth(150);
options.setHeight(0); // Auto‑scale based on image aspect ratio
```

* **ImageFilePath:** Point to a PNG or JPG of your handwritten signature or corporate logo. Transparent PNGs work best.  
* **AllPages:** Set to `true` for contracts that need a proof on every page; otherwise `false` signs only the last page.  
* **Width/Height:** Measured in pixels; a height of **50‑80** pixels looks professional for most business documents.

## How do I control alignment and padding?

Alignment settings determine where the stamp lands on the page, while padding adds a buffer around the visual element to keep it from touching page edges. Proper alignment improves readability and ensures the signature does not interfere with existing content.

`AlignmentOptions` provides vertical and horizontal placement constants such as `Bottom`, `Right`, `Top`, and `Center`.

```java
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
options.setPadding(10);
```

* **Padding:** Adds breathing room around the stamp; a value of **10** pixels prevents the image from touching page edges.  
* **Real‑world example:** In invoice templates, you might use `Top`/`Left` to place the approver’s signature near the header.

## How do I add a signature line for Office documents?

When signing DOCX or XLSX files, a visible signature line improves readability for end users. The library creates a Microsoft‑style signature line that displays the signer’s name, title, and email, mirroring the native Office experience.

`SignatureLineOptions` creates a Microsoft‑style signature line that displays the signer’s name, title, and email.

```java
options.setSignatureLineText("John Doe", "Chief Legal Officer", "j.doe@yourcompany.com");
```

* This feature is ignored for PDFs but is essential for Word and Excel files opened in Microsoft Office.

## How do I actually sign a document?

Load the source file with a `Signature` instance, apply the fully configured `DigitalSignOptions`, and invoke `sign()`. The library writes a new file to the output path, leaving the original untouched. For large PDFs (50+ pages) expect a 2‑5 second processing window; consider asynchronous execution in web services.

```java
Signature signature = new Signature("SAMPLE_WORDPROCESSING/contract.docx");
DigitalSignOptions options = new DigitalSignOptions();
// ...configure options as shown earlier...
signature.sign("OUTPUT_FOLDER/signed_contract.docx", options);
```

**Performance note:** For documents over 100 pages, increase the JVM heap (`-Xmx2g`) or disable `setAllPages(true)` to limit memory consumption.

## How do I troubleshoot common issues?

When signing fails, the most common problems relate to certificate handling, visual placement, or memory constraints. Identify the symptom, then follow the targeted checklist below to resolve the issue quickly.

### Why do I see “Invalid Certificate” or “Cannot Load Certificate” errors?

These exceptions usually stem from one of four causes:

1. **Incorrect password** – verify with OpenSSL: `openssl pkcs12 -info -in yourcert.pfx`.  
2. **Expired certificate** – check the validity using `keytool -list -v -keystore yourcert.pfx`.  
3. **Wrong file format** – only `.pfx` or `.p12` (which contain private keys) are accepted.  
4. **File permission problems** – ensure the Java process can read the certificate file.

### Why doesn’t the signature appear on the page?

* **AllPages flag** may be `false`, so you’re looking at a page without a stamp.  
* **Image path** could be misspelled; print `options.getImageFilePath()` to confirm.  
* **Alignment settings** might push the stamp off‑screen; temporarily switch to `Center` for debugging.

### Why does Adobe Reader report “Signature Invalid”?

* **Certificate not trusted** – self‑signed certificates trigger warnings. Use a CA‑issued certificate for production.  
* **Incomplete certificate chain** – ensure the `.pfx` includes intermediate and root certificates.  
* **Missing timestamp** – without a TSA token, the signature may be considered invalid after the certificate expires. GroupDocs supports timestamping via `setTimeStampOptions()`.

### How do I avoid OutOfMemoryError with huge PDFs?

* Increase JVM heap (`-Xmx4g` or higher).  
* Sign only the required pages (`setAllPages(false)`).  
* Process files in smaller batches or stream them if you’re on a constrained environment.

## How do I manage certificates securely in production?

Never embed certificates or passwords in source code. Follow these steps:

1. Store `.pfx` files in a secure vault (AWS Secrets Manager, Azure Key Vault, or HashiCorp Vault).  
2. Load the password at runtime from environment variables or the vault’s API.  
3. Restrict file system permissions so only the service account can read the certificate.  
4. Rotate certificates at least 30 days before expiration and update the stored secret accordingly.

```java
String certPath = System.getenv("CERT_PATH");
String certPassword = System.getenv("CERT_PASSWORD");
options.setCertificatePath(certPath);
options.setCertificatePassword(certPassword);
```

## How do I log signature operations for audit compliance?

Audit logs provide non‑repudiation evidence. Record the following fields for each signing event:

* Document name and hash before signing  
* Signer identity (certificate subject)  
* Timestamp of the operation (preferably UTC)  
* Result status (success/failure) and error details if any  

```java
logger.info("Signing document {} with certificate {} at {}", docPath, options.getCertificatePath(), Instant.now());
```

## How do I verify a signature after it’s been applied?

Verification ensures the document hasn’t been tampered with post‑signing. Use the `verify()` method, which returns a `VerificationResult` containing validity status, signer details, and any timestamp information. A successful verification confirms both integrity and authenticity.

```java
VerificationResult result = signature.verify("OUTPUT_FOLDER/signed_contract.docx");
if (result.isValid()) {
    logger.info("Signature is valid and trusted.");
} else {
    logger.warn("Signature verification failed: {}", result.getErrorMessage());
}
```

## How can I add multiple signatures to a single document?

You may need an approver and a witness signature. Call `sign()` multiple times with distinct `DigitalSignOptions` instances, each configured with its own certificate and visual settings. The library preserves existing signatures while appending new ones.

```java
// First signature (approver)
signature.sign("output.docx", approverOptions);
// Second signature (witness)
signature.sign("output.docx", witnessOptions);
```

## How do I create a factory method for different document types?

A helper method can return a pre‑configured `DigitalSignOptions` based on the file extension, keeping your code DRY. This centralizes certificate loading, visual defaults, and page‑selection logic for PDFs, Word, Excel, and other supported formats.

```java
public DigitalSignOptions getOptionsFor(String extension) {
    DigitalSignOptions opts = new DigitalSignOptions();
    // common settings
    if (extension.equalsIgnoreCase("pdf")) {
        opts.setImageFilePath("signatures/pdf_stamp.png");
    } else if (extension.equalsIgnoreCase("docx")) {
        opts.setSignatureLineText("Jane Smith", "Finance Manager", "j.smith@company.com");
    }
    return opts;
}
```

## How do I validate that a document isn’t already signed?

Before applying a new signature, check for existing signatures to avoid double‑signing. Use the `getSignatures()` method; if the returned collection is non‑empty, decide whether to append a new signature or abort the operation.

```java
List<SignatureInfo> existing = signature.getSignatures();
if (!existing.isEmpty()) {
    logger.warn("Document already contains {} signatures.", existing.size());
}
```

## Practical Applications (Real‑World Use Cases)

1. **Automated Contract Workflows** – When a contract reaches the “approved” state in your BPM system, trigger the signing service to embed the legal department’s certificate and email the signed copy to the vendor.  
2. **Invoice Approval Systems** – After finance signs off an invoice, automatically add a digital signature before sending it to the customer, providing cryptographic proof of authenticity.  
3. **Document Verification Portals** – Offer a self‑service portal where users upload a PDF, you sign it with a company‑wide certificate, and return a tamper‑evident file for legal compliance.  
4. **Compliance‑Heavy Industries** – In healthcare (HIPAA) or finance (SOX), digital signatures satisfy audit requirements by proving who signed a document and when.  
5. **Internal Policy Distribution** – Replace manual stamping of HR policies with an automated process that signs the final PDF using the CHRO’s certificate, ensuring every employee receives a verified copy.

## Performance Considerations

| Document Size | Avg. Processing Time | Recommended Settings |
|---------------|----------------------|----------------------|
| 1‑5 pages | ~0.5 s | Default options |
| 5‑50 pages | 1‑3 s | Increase heap, `setAllPages(true)` if needed |
| 50‑200 pages | 3‑10 s | `setAllPages(false)`, async execution, larger heap |

**Optimization tips:**  

* Reuse a single `Signature` instance when signing many files in a batch.  
* Cache the loaded `DigitalSignOptions` object; loading the certificate repeatedly adds overhead.  
* For web services, wrap the signing call in a `CompletableFuture` or push it to a message queue to keep the UI responsive.

## Pro Tips (Advanced Usage)

* **Timestamping for long‑term validity** – Attach a TSA token using `setTimeStampOptions()` to ensure signatures remain valid after the certificate expires.  
* **Invisible signatures** – Omit `ImageFilePath` and set `Width`/`Height` to `0` to create a cryptographically valid but invisible signature, useful for backend processes that don’t require a visual stamp.  
* **Custom QR‑code signatures** – GroupDocs can embed a QR code containing signer metadata; ideal for supply‑chain documents that need quick verification via mobile devices.  

## Frequently Asked Questions

**Q: What’s the main difference between GroupDocs.Signature and iText for PDF signing?**  
A: iText focuses solely on PDF and requires you to handle low‑level cryptography yourself, while GroupDocs.Signature supports 30+ formats, offers ready‑made visual stamps, and abstracts certificate handling, reducing development time dramatically.

**Q: Can I integrate GroupDocs.Signature into a Spring Boot microservice?**  
A: Yes. Add the Maven dependency, create a `@Service` bean that wraps the signing logic, and inject it wherever you need to sign documents. This keeps your controllers thin and your signing code reusable.

**Q: How secure are signatures created with GroupDocs.Signature?**  
A: The library uses standard PKI algorithms (RSA/ECDSA) and follows the same specifications as browsers and Adobe Reader. Security depends on the quality of your certificate; always use a CA‑issued certificate and protect the private key.

**Q: Will signed documents work across different PDF readers?**  
A: Absolutely. As long as the signing certificate is trusted, Adobe Reader, Foxit, and modern browsers will validate the signature correctly. Self‑signed certificates will display a warning but remain technically valid.

**Q: Is it possible to sign documents without a visible signature image?**  
A: Yes—simply omit the `ImageFilePath` and set size parameters to zero. The resulting signature is invisible but still cryptographically sound, perfect for backend automation where visual cues aren’t required.

## Conclusion

You now have a complete, production‑ready roadmap for **add digital signature java** using GroupDocs.Signature. We covered everything from environment setup and certificate handling to visual customization, performance tuning, and advanced scenarios like multiple signatures and timestamping.  

**Next steps:**  

1. Test the sample code with your own certificates and document templates.  
2. Harden your deployment by moving certificates to a secret manager and configuring proper JVM memory limits.  
3. Extend the helper methods to support batch processing or integrate with your existing workflow engine.  

For deeper dives, explore the official documentation and community forums linked below.

---

**Last Updated:** 2026-06-11  
**Tested With:** GroupDocs.Signature 23.12 for Java  
**Author:** GroupDocs  

**Resources:**  
- [GroupDocs.Signature Documentation](https://docs.groupdocs.com/signature/java/)  
- [Support Forum](https://forum.groupdocs.com/c/signature/)  

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}
```java
import com.groupdocs.signature.Signature;

public class SignatureSetup {
    public static void main(String[] args) {
        Signature signature = new Signature("path/to/your/document");
        // Your signing logic goes here
    }
}
```
```java
import com.groupdocs.signature.options.sign.DigitalSignOptions;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.exception.GroupDocsSignatureException;

DigitalSignOptions options = new DigitalSignOptions("YOUR_DOCUMENT_DIRECTORY/CertificatePfx");
options.setPassword("1234567890"); // Ensure your certificate password is secure
options.setReason("Sign"); // Reason for signing, e.g., "Contract Approval"
options.setContact("JohnSmith"); // Contact information of the signer
options.setLocation("Office1"); // Location where document is signed
```
```java
options.setImageFilePath("YOUR_DOCUMENT_DIRECTORY/ImageHandwrite");
options.setAllPages(true); // Apply signature to all pages of the document
options.setWidth(0); // Auto-width based on content
options.setHeight(60); // Height in pixels
```
```java
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
Padding padding = new Padding();
padding.setBottom(10); // Bottom padding for aesthetic spacing
padding.setRight(10); // Right padding to prevent clipping at edges
options.setMargin(padding);
```
```java
import com.groupdocs.signature.domain.signatures.DigitalSignatureAppearance;

options.setAppearance(new DigitalSignatureAppearance("John Smith", "Title", "jonny@test.com"));
```
```java
try {
    Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/SAMPLE_WORDPROCESSING");
    String outputFilePath = "YOUR_OUTPUT_DIRECTORY/DigitalAppearance.docx";
    signature.sign(outputFilePath, options);
} catch (GroupDocsSignatureException e) {
    throw new RuntimeException(e.getMessage());
}
```
```java
// BAD - Don't do this
options.setPassword("1234567890");

// GOOD - Load from environment variable
String certPassword = System.getenv("CERT_PASSWORD");
if (certPassword == null) {
    throw new RuntimeException("CERT_PASSWORD environment variable not set");
}
options.setPassword(certPassword);
```
```java
logger.info("Document signed: {}, SignedBy: {}, Timestamp: {}", 
    documentName, signerEmail, LocalDateTime.now());
```
```java
// Verify the signature immediately after signing
List<DigitalSignature> signatures = signature.verify();
if (signatures.isEmpty()) {
    throw new RuntimeException("Signature verification failed");
}
```
```java
signature.sign(outputPath, approverOptions);
signature = new Signature(outputPath); // Reload the signed document
signature.sign(finalOutputPath, witnessOptions);
```
```java
public DigitalSignOptions getOptionsForDocType(String docType) {
    DigitalSignOptions options = new DigitalSignOptions(certPath);
    if (docType.equals("contract")) {
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        // Contract-specific settings
    } else if (docType.equals("invoice")) {
        options.setVerticalAlignment(VerticalAlignment.Top);
        // Invoice-specific settings
    }
    return options;
}
```
```java
List<DigitalSignature> existingSignatures = signature.search(DigitalSignature.class);
if (!existingSignatures.isEmpty()) {
    System.out.println("Document already signed by: " + 
        existingSignatures.get(0).getContactInfo());
}
```

## Related Tutorials

- [Digital Signature in Java - Complete Guide to Certificate Loading and Document Signing](/signature/java/digital-signatures/digital-signature-loading-signing-groupdocs-java/)
- [How to Verify Digital Certificates in Java - Complete Guide with Code Examples](/signature/java/digital-signatures/java-certificate-verification-groupdocs-signature/)
- [Java Document Signing Tutorial - Add Text Signatures with Event Handling](/signature/java/event-handling/java-text-signing-groupdocs-signature-event-handling/)
