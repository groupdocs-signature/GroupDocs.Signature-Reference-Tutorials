---
categories:
- Java Development
date: '2026-06-11'
description: Lär dig hur du signerar PDF med Java med hjälp av GroupDocs.Signature,
  lägg till digital signatur och tidsstämpel. Steg-för-steg guide med kodexempel och
  bästa praxis.
keywords:
- how to sign pdf
- add digital signature pdf
- timestamp pdf signature
- java pdf signature library
- groupdocs signature java
lastmod: '2026-06-11'
linktitle: Lägg till digital signatur till PDF Java
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to sign PDF with Java using GroupDocs.Signature, add digital
    signature and timestamp. Step-by-step guide with code examples and best practices.
  headline: 'How to Sign PDF with Java: Add Digital Signature and Timestamp'
  type: TechArticle
- description: Learn how to sign PDF with Java using GroupDocs.Signature, add digital
    signature and timestamp. Step-by-step guide with code examples and best practices.
  name: 'How to Sign PDF with Java: Add Digital Signature and Timestamp'
  steps:
  - name: Import Required Classes
    text: The following imports give you access to signature configuration, positioning,
      and timestamp functionality.
  - name: Define Your File Paths
    text: Set up paths for your input PDF, certificate, and where you want the signed
      PDF saved. Keep the certificate file secure; it contains your private key.
  - name: Initialize the Signature Object
    text: Create a `Signature` instance pointing to the PDF you want to sign. This
      loads the PDF into memory and prepares it for signing.
  - name: Configure Signature Properties and Timestamp
    text: The `DigitalSignature` class represents the cryptographic seal that will
      be embedded in the PDF. You can also attach a timestamp from a trusted authority.
      * **ContactInfo** – e.g., `john.doe@company.com` * **Location** – e.g., `New
      York Office` * **Reason** – e.g., `Contract Approval` We use FreeTSA
  - name: Configure Digital Sign Options
    text: The `SignOptions` class ties together the certificate, signature properties,
      and visual placement. Alignment enums control where the signature appears.
  - name: Sign and Save the Document
    text: Execute the signing process and write the signed PDF to disk. The returned
      `SignResult` object tells you whether the operation succeeded and lists any
      warnings.
  type: HowTo
- questions:
  - answer: A digital signature uses cryptographic algorithms to verify identity and
      detect tampering, while an electronic signature can be as simple as a typed
      name.
    question: What's the difference between a digital signature and an electronic
      signature?
  - answer: Only for the timestamp service; the cryptographic signing itself runs
      locally.
    question: Do I need internet connectivity to sign PDFs?
  - answer: Any modification breaks the signature, and PDF viewers will display a
      warning indicating the document has been altered.
    question: Can signed PDFs be edited later?
  - answer: Most PDF readers verify automatically; programmatically, use GroupDocs.Signature's
      verification API to check status, signer details, and timestamp validity.
    question: How do I verify a signed PDF?
  - answer: The embedded timestamp proves the signature was created while the certificate
      was still valid, preserving legal standing.
    question: What happens if my certificate expires after I've signed documents?
  type: FAQPage
tags:
- pdf-signing
- digital-signatures
- java-security
- groupdocs
title: 'Hur man signerar PDF med Java: Lägg till digital signatur och tidsstämpel'
type: docs
url: /sv/java/digital-signatures/digital-signature-timestamp-pdf-java-groupdocs/
weight: 1
---

# Hur man signerar PDF med Java och tidsstämpel

Ever sent an important document and worried whether someone could tamper with it later? You're not alone. Whether you're building an enterprise document management system, creating a contract signing platform, or just need to secure your PDF files programmatically, **how to sign PDF** with a trusted timestamp is the answer. Adding a digital signature not only proves who signed the file but also creates an immutable record of *exactly* when the signing occurred.

## Snabba svar
- **Vilket bibliotek förenklar PDF‑signering i Java?** GroupDocs.Signature for Java.  
- **Behöver jag en internetanslutning?** Endast för tidsstämpelmyndigheten; själva signeringen sker offline.  
- **Kan jag använda ett självsignerat certifikat för testning?** Ja, generera ett med `keytool`.  
- **Finns det en storleksgräns?** Biblioteket kan signera PDF‑filer upp till 500 MB utan att ladda hela filen i minnet.  
- **Hur många format stödjer GroupDocs?** Över 50 in‑ och utdataformat, inklusive DOCX, XLSX, PPTX, HTML och bilder.

## Varför digitala signaturer är viktiga (och varför du behöver tidsstämplar)

Load your PDF, apply a cryptographic seal, and embed a trusted timestamp—this two‑step process guarantees authentication, integrity, and non‑repudiation. The timestamp proves the signature existed at a specific moment, even if the signing certificate later expires or is revoked.

## Hur man signerar PDF med Java?

Load your PDF with `new Signature("input.pdf")`, configure a `DigitalSignature` object, attach a timestamp from a trusted authority, and call `sign()`—the entire operation completes in a few lines of code. GroupDocs.Signature handles certificate parsing, hash calculation, and timestamp retrieval automatically, so you can focus on business logic rather than cryptography.

## Konfigurera GroupDocs.Signature för Java

### Integrationsmetoder

Pick whichever build tool you're using:

**För Maven‑användare:**  
Add this dependency to your `pom.xml`:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**För Gradle‑användare:**  
Add this to your `build.gradle`:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Direkt nedladdning (om du föredrar):**  
Head over to [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) and download the JAR file. Add it to your project's classpath manually. See the [GroupDocs.Signature Documentation](https://docs.groupdocs.com/signature/java/) for detailed API reference. For the most recent build, see the [Latest Version & Releases](https://releases.groupdocs.com/signature/java/).

Proffstips: Använd Maven eller Gradle om möjligt – det gör beroendehantering och uppdateringar mycket enklare i framtiden.

### Skaffa din licens

GroupDocs offers a few options here, depending on where you're at in your project:

1. **Free Trial** – Perfect for evaluation. [Download Trial Version](https://releases.groupdocs.com/signature/java/) and test drive all features.  
2. **Temporary License** – Need full access for development without the trial watermark? Get a 30‑day temporary license.  
3. **Commercial License** – For production use, [Buy License](https://purchase.groupdocs.com/buy). Pricing varies based on deployment type.

Need help? Visit the [GroupDocs Forum](https://forum.groupdocs.com/c/signature/).

### Grundläggande initiering

The `Signature` class is GroupDocs.Signature's top‑level object that represents a single PDF file in memory. After instantiation, all read and write operations flow through this object.

```java
import com.groupdocs.signature.Signature;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
final Signature signature = new Signature(filePath);
```

Simple, right? You just point it at your PDF file, and you're ready to go. The `Signature` object is your main interface for all signing operations.

## Så lägger du till digital signatur till PDF i Java: Steg‑för‑steg

Load your PDF, configure signature details, attach a timestamp, and save the signed document—all in a clear, linear flow.

### Steg 1: Importera nödvändiga klasser

The following imports give you access to signature configuration, positioning, and timestamp functionality.

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.PdfDigitalSignature;
import com.groupdocs.signature.domain.structs.TimeStamp;
import com.groupdocs.signature.options.sign.DigitalSignOptions;
```

### Steg 2: Definiera dina filsökvägar

Set up paths for your input PDF, certificate, and where you want the signed PDF saved. Keep the certificate file secure; it contains your private key.

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
String certificatePath = "YOUR_DOCUMENT_DIRECTORY/certificate.pfx";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/digitallySignedTimeStamp.pdf";
```

### Steg 3: Initiera Signature‑objektet

Create a `Signature` instance pointing to the PDF you want to sign. This loads the PDF into memory and prepares it for signing.

```java
final Signature signature = new Signature(filePath);
```

### Steg 4: Konfigurera signaturens egenskaper och tidsstämpel

The `DigitalSignature` class represents the cryptographic seal that will be embedded in the PDF. You can also attach a timestamp from a trusted authority.

```java
PdfDigitalSignature pdfDigitalSignature = new PdfDigitalSignature();
pdfDigitalSignature.setContactInfo("Contact Information");
pdfDigitalSignature.setLocation("Location Info");
pdfDigitalSignature.setReason("Signing Reason");

// Configure the TimeStamp with URL, User Id, and Password
TimeStamp timeStamp = new TimeStamp("https://freetsa.org/tsr", "User Id", "Password");
pdfDigitalSignature.setTimeStamp(timeStamp);
```

* **ContactInfo** – e.g., `john.doe@company.com`  
* **Location** – e.g., `New York Office`  
* **Reason** – e.g., `Contract Approval`  

We use FreeTSA (a free timestamp authority) for demonstration. In production, choose a commercial TSA for guaranteed uptime and legal standing.

### Steg 5: Konfigurera digital signeringsalternativ

The `SignOptions` class ties together the certificate, signature properties, and visual placement. Alignment enums control where the signature appears.

```java
DigitalSignOptions options = new DigitalSignOptions(certificatePath);
options.setPassword("YourCertificatePassword"); // Certificate password
options.setSignature(pdfDigitalSignature); // Attach the PdfDigitalSignature object

// Specify signature alignment (where it appears on the page)
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
```

### Steg 6: Signera och spara dokumentet

Execute the signing process and write the signed PDF to disk. The returned `SignResult` object tells you whether the operation succeeded and lists any warnings.

```java
try {
    SignResult signResult = signature.sign(outputFilePath, options);
    System.out.println("Document signed successfully!");
    System.out.println("Output: " + outputFilePath);
} catch (Exception e) {
    throw new RuntimeException("Error during signing process: " + e.getMessage());
}
```

## Vanliga fallgropar att undvika

### 1. Certifikatproblem
**Problem:** “Invalid certificate” errors.  
**Fix:** Verify the password with `keytool -list -v -keystore your.pfx`.

```bash
keytool -list -v -keystore certificate.pfx -storetype PKCS12
```

### 2. Tidsstämpel‑tjänstens tidsgränser
**Problem:** Network timeouts when contacting the TSA.  
**Fix:** Test connectivity (`curl -I https://freetsa.org/tsr`), add retry logic, or configure a fallback TSA.

```java
new File(outputFilePath).getParentFile().mkdirs();
```

### 3. Filbehörighetsproblem
**Problem:** “Access denied” while saving.  
**Fix:** Ensure the output directory exists and the application has write permissions.

```bash
keytool -genkeypair -alias mykey -keyalg RSA -keysize 2048 -storetype PKCS12 -keystore certificate.pfx -validity 365
```

### 4. Minnesproblem med stora PDF‑filer
**Problem:** `OutOfMemoryError` for big files.  
**Fix:** Increase JVM heap (`-Xmx4g`) or process files in batches.

### 5. Fel signaturplacering
**Problem:** Signature overlaps existing content.  
**Fix:** Test alignment settings first; for pixel‑perfect placement, use coordinate‑based options.

## Tips för certifikathantering

### Skaffa ett certifikat för utveckling

Generate a self‑signed certificate with Java’s `keytool` for testing purposes.

```java
   String certPassword = System.getenv("CERT_PASSWORD");
   ```

### Bästa praxis för certifikat

1. **Never hard‑code passwords** – use environment variables.  
2. **Rotate certificates** before they expire.  
3. **Store private keys** in secure hardware (HSM) for high‑security apps.  
4. **Back up certificates** in a protected location.  
5. **Validate certificates** before signing to catch expired or revoked ones.

## Säkerhetsbästa praxis

### 1. Skydda privata nycklar
Store certificates outside the project directory, use environment‑specific configs, and consider HSMs for enterprise deployments.

### 2. Validera inmatade PDF‑filer
Check for corruption, existing signatures, size limits, and content compliance before signing.

### 3. Implementera revisionsloggning
Log every signing operation with timestamp, user, document name, and status.

```java
try {
    SignResult result = signature.sign(outputFilePath, options);
    logger.info("Document signed: " + filePath + " by " + signerEmail);
} catch (Exception e) {
    logger.error("Signing failed: " + filePath + " - " + e.getMessage());
    // Handle appropriately
}
```

### 4. Använd betrodda tidsstämpelmyndigheter
Never rely on local system time; always request a timestamp from an RFC 3161‑compliant TSA.

### 5. Implementera felhantering
Catch exceptions without exposing sensitive details.

```java
try {
    signature.sign(outputFilePath, options);
} catch (Exception e) {
    // Log detailed error internally
    logger.error("Signing error: " + e.getMessage(), e);
    // Return generic error to client
    throw new ApplicationException("Unable to sign document. Please try again.");
}
```

## Verkliga användningsfall och tillämpningar

### 1. System för kontraktshantering
Employees sign NDAs and agreements electronically; timestamps prove exactly when each contract was accepted.

### 2. Finansiell dokumentbehandling
Batch‑sign invoices and purchase orders, providing an immutable audit trail for regulators.

### 3. Verifiering av utbildningsdiplom
Universities issue tamper‑proof transcripts that can be instantly validated via a QR‑code link.

### 4. Hantering av programvarulicenser
Generate license certificates with a digital signature and timestamp to prevent forgery.

### 5. Regulatorisk efterlevnad (FDA 21 CFR Part 11, etc.)
Medical device firms sign SOPs and validation reports; timestamps satisfy non‑repudiation requirements.

## Prestandaöverväganden och optimering

### Minneshantering
Process large PDFs in batches, close `Signature` objects promptly, and increase heap size when needed.

### Nätverksoptimering för tidsstämplar
Pool HTTP connections, implement exponential backoff retries, and cache timestamps for rapid successive signings.

### Bästa praxis för batch‑behandling
```java
// Pseudo‑code: process a list of PDFs in parallel, limiting to 5 concurrent TSA calls
```
*Undvik att starta för många trådar; 5‑10 samtidiga signeringar balanserar genomströmning och TSA‑belastning.*

### Disk‑I/O‑optimering
Use SSDs for temporary files, minimize read/write cycles, and clean up temporary artifacts after each signing run.

## Felsökningsguide

### Fel: “Invalid Certificate Password”
**Solution:** Verify the password with `keytool -list -keystore your.pfx`.

```java
ExecutorService executor = Executors.newFixedThreadPool(5);
List<Future<SignResult>> futures = new ArrayList<>();

for (String pdfPath : pdfPaths) {
    futures.add(executor.submit(() -> {
        try (Signature sig = new Signature(pdfPath)) {
            return sig.sign(outputPath, options);
        }
    }));
}

// Wait for all to complete
for (Future<SignResult> future : futures) {
    SignResult result = future.get();
    // Process result
}

executor.shutdown();
```

### Fel: “Timestamp Authority Not Responding”
**Solution:** Test TSA URL, check firewall rules, and add fallback TSA logic.

```bash
keytool -list -v -keystore certificate.pfx -storetype PKCS12
```

### Fel: “PDF is Already Signed”
**Solution:** Detect existing signatures first; either add a counter‑signature or sign a fresh copy.

### Fel: “Access Denied” vid sparande
**Solution:** Ensure the output directory exists, the app has write rights, and no other process locks the file.

```java
TimeStamp timeStamp;
try {
    timeStamp = new TimeStamp("https://freetsa.org/tsr", "", "");
} catch (Exception e) {
    // Fallback to alternative TSA
    timeStamp = new TimeStamp("https://alternate-tsa.com/tsr", "", "");
}
```

### Fel: OutOfMemoryError
**Solution:** Increase JVM heap, process PDFs in smaller batches, or switch to streaming APIs for very large files.

## Slutsats och nästa steg

You've learned **how to sign PDF** files with Java, add a trusted timestamp, and handle common pitfalls. Next, explore:

1. Adding multiple signature fields for multi‑party agreements.  
2. Verifying signatures programmatically with GroupDocs.Signature.  
3. Customizing signature appearance (images, text, positioning).  
4. Building a robust batch‑signing service with queuing and monitoring.

## Vanliga frågor

**Q: What's the difference between a digital signature and an electronic signature?**  
A: A digital signature uses cryptographic algorithms to verify identity and detect tampering, while an electronic signature can be as simple as a typed name.

**Q: Do I need internet connectivity to sign PDFs?**  
A: Only for the timestamp service; the cryptographic signing itself runs locally.

**Q: Can signed PDFs be edited later?**  
A: Any modification breaks the signature, and PDF viewers will display a warning indicating the document has been altered.

**Q: How do I verify a signed PDF?**  
A: Most PDF readers verify automatically; programmatically, use GroupDocs.Signature's verification API to check status, signer details, and timestamp validity.

**Q: What happens if my certificate expires after I've signed documents?**  
A: The embedded timestamp proves the signature was created while the certificate was still valid, preserving legal standing.

**Q: Can I use this with cloud storage (S3, Azure Blob, etc.)?**  
A: Yes—download the PDF to a temporary location, sign it, then upload the signed version back to the cloud.

**Q: Are there file size limits?**  
A: The library handles PDFs up to 500 MB without loading the whole file into memory; larger files may require streaming.

**Q: How much does GroupDocs.Signature cost for commercial use?**  
A: Pricing varies by deployment type; contact GroupDocs sales for the latest rates. Free trials and temporary licenses are available for evaluation.

**Q: Does this work on Linux servers?**  
A: Absolutely. GroupDocs.Signature for Java is platform‑independent and runs on any OS with a JRE.

**Senast uppdaterad:** 2026-06-11  
**Testad med:** GroupDocs.Signature 23.9 for Java  
**Författare:** GroupDocs

```java
File outputFile = new File(outputFilePath);
outputFile.getParentFile().mkdirs(); // Create directories if needed

if (!outputFile.canWrite() && outputFile.exists()) {
    throw new IOException("Cannot write to " + outputFilePath);
}
```

## Relaterade handledningar

- [How to Verify Digital Certificates in Java - Complete Guide with Code Examples](/signature/java/digital-signatures/java-certificate-verification-groupdocs-signature/)
- [How to Sign PDF Programmatically in Java with GroupDocs.Signature](/signature/java/digital-signatures/sign-pdfs-groupdocs-signature-java/)
- [Add Image Signature to PDF Java with GroupDocs](/signature/java/image-signatures/sign-pdf-image-signature-groupdocs-java/)