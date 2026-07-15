---
date: '2026-07-15'
description: Μάθετε πώς να προσθέσετε barcode PDF Java χρησιμοποιώντας το GroupDocs.Signature
  – βήμα‑βήμα οδηγός για υπογραφή, επαλήθευση, αναζήτηση, ενημέρωση και διαγραφή υπογραφών
  barcode σε έγγραφα Java.
keywords:
- add barcode pdf java
- groupdocs barcode signature
- java document signing
lastmod: '2026-07-15'
linktitle: Οδηγός Υπογραφής Barcode Java
og_description: Μάθετε πώς να προσθέσετε barcode PDF Java χρησιμοποιώντας το GroupDocs.Signature
  – βήμα‑βήμα οδηγός για υπογραφή, επαλήθευση, αναζήτηση, ενημέρωση και διαγραφή υπογραφών
  barcode σε έγγραφα Java.
og_image_alt: Guide showing how to add barcode PDF Java using GroupDocs.Signature
og_title: Προσθήκη Barcode PDF Java – Υπογραφή & Επαλήθευση με GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-07-15'
  description: Learn how to add barcode PDF Java using GroupDocs.Signature – step‑by‑step
    guide to sign, verify, search, update and delete barcode signatures in Java documents.
  headline: Add Barcode PDF Java – Sign & Verify with GroupDocs
  type: TechArticle
- description: Learn how to add barcode PDF Java using GroupDocs.Signature – step‑by‑step
    guide to sign, verify, search, update and delete barcode signatures in Java documents.
  name: Add Barcode PDF Java – Sign & Verify with GroupDocs
  steps:
  - name: Case mismatch (e.g., “John Smith” vs. “john smith”).
    text: Case mismatch (e.g., “John Smith” vs. “john smith”).
  - name: Extra whitespace in the encoded text.
    text: Extra whitespace in the encoded text.
  - name: Wrong barcode type specified in the verification options.
    text: Wrong barcode type specified in the verification options.
  - name: Searching the wrong page number.
    text: Searching the wrong page number.
  - name: '**Reuse Signature Instances** – Create a single `Signature` object per
      document and reuse it for multiple operations.'
    text: '**Reuse Signature Instances** – Create a single `Signature` object per
      document and reuse it for multiple operations.'
  - name: '**Search Specific Pages Only** – Limit the page range to where barcodes
      are expected.'
    text: '**Search Specific Pages Only** – Limit the page range to where barcodes
      are expected.'
  - name: '**Choose the Simplest Barcode Type** – Simpler barcodes generate faster;
      only use QR or Data Matrix when you truly need the extra capacity.'
    text: '**Choose the Simplest Barcode Type** – Simpler barcodes generate faster;
      only use QR or Data Matrix when you truly need the extra capacity.'
  - name: '**Never Encode Sensitive Personal Data** – Barcodes are easily readable;
      avoid PII such as SSNs or passwords.'
    text: '**Never Encode Sensitive Personal Data** – Barcodes are easily readable;
      avoid PII such as SSNs or passwords.'
  - name: '**Validate Server‑Side** – Never trust client‑side verification alone;
      always re‑verify on a trusted backend.'
    text: '**Validate Server‑Side** – Never trust client‑side verification alone;
      always re‑verify on a trusted backend.'
  - name: '**Add Timestamps** – Include a timestamp in the barcode payload to prevent
      replay attacks.'
    text: '**Add Timestamps** – Include a timestamp in the barcode payload to prevent
      replay attacks.'
  type: HowTo
- questions:
  - answer: Yes – the library is fully compatible with JDK 8, 11, and 17.
    question: Can I use GroupDocs.Signature with Java 17?
  - answer: When you use Code128 or QR with sufficient size and contrast, the barcode
      remains scannable after printing and scanning.
    question: Does the barcode survive a print‑scan cycle?
  - answer: There is no hard limit; however, for optimal performance keep the total
      count below **200** per document.
    question: How many barcodes can a single document contain?
  - answer: A temporary license removes evaluation watermarks; a full license is mandatory
      for any production deployment.
    question: Is a license required for development builds?
  - answer: Yes – provide the password when creating the `Signature` object; the API
      will unlock the file internally.
    question: Can I sign password‑protected PDFs?
  type: FAQPage
tags:
- barcode signature
- groupdocs
- java
- pdf
- document signing
title: Προσθήκη Barcode PDF Java – Υπογραφή & Επαλήθευση με GroupDocs
type: docs
url: /el/java/digital-signatures/java-document-signature-groupdocs-signature-barcode/
weight: 1
---

# Προσθήκη Barcode PDF Java – Υπογραφή & Επαλήθευση με GroupDocs

Αν χρειάζεστε έναν γρήγορο, οπτικό τρόπο σήμανσης εγγράφων για εσωτερικές ροές εργασίας, η προσθήκη barcode σε PDF με Java είναι η ιδανική λύση. Με το **GroupDocs.Signature**, μπορείτε να ενσωματώσετε, επαληθεύσετε, αναζητήσετε, ενημερώσετε και διαγράψετε υπογραφές barcode χωρίς το βάρος των πλήρων ψηφιακών υπογραφών PKI. Αυτό το tutorial σας οδηγεί βήμα‑βήμα, από τη ρύθμιση του περιβάλλοντος μέχρι τις βέλτιστες πρακτικές για παραγωγή.

## Γρήγορες Απαντήσεις
- **Ποια βιβλιοθήκη προσθέτει barcode σε PDF με Java;** GroupDocs.Signature for Java.  
- **Μπορώ να υπογράψω PDF, Word και εικόνες;** Ναι – το API υποστηρίζει πάνω από 30 μορφές.  
- **Χρειάζεται άδεια για ανάπτυξη;** Μία προσωρινή άδεια 30 ημερών είναι δωρεάν· πλήρης άδεια απαιτείται για παραγωγή.  
- **Πόσες γραμμές κώδικα χρειάζονται για υπογραφή PDF;** Μόνο δύο: δημιουργήστε ένα αντικείμενο `Signature` και καλέστε `sign`.  
- **Είναι η επαλήθευση barcode case‑sensitive;** Ναι – το κείμενο πρέπει να ταιριάζει ακριβώς, συμπεριλαμβανομένων κεφαλαίων/μικρών και κενών.

## Τι είναι η προσθήκη barcode pdf java;
`add barcode pdf java` αναφέρεται στη διαδικασία χρήσης κώδικα Java για την ενσωμάτωση ενός barcode (π.χ. Code128, QR ή Data Matrix) σε αρχείο PDF. Αυτή η τεχνική παρέχει μια μηχανικά αναγνώσιμη ετικέτα που μπορεί να σαρωθεί ή να επαληθευθεί προγραμματιστικά, επιτρέποντας γρήγορη παρακολούθηση εγγράφων σε εσωτερικά συστήματα.

## Γιατί να χρησιμοποιήσετε υπογραφές barcode αντί για πλήρεις ψηφιακές υπογραφές;
Οι υπογραφές barcode είναι **30‑50 % πιο γρήγορες** στην παραγωγή και επαλήθευση σε σχέση με τις ψηφιακές υπογραφές PKI, και λειτουργούν αξιόπιστα μετά από κύκλο εκτύπωση‑σάρωση. Δεν απαιτούν διαχείριση πιστοποιητικών, καθιστώντας τες ιδανικές για υψηλού όγκου εσωτερικές ροές εργασίας όπου η κρυπτογραφική απόδειξη δεν είναι υποχρεωτική.

## Προαπαιτούμενα

- **Java Development Kit (JDK) 8+** – Συνιστάται Java 11 ή 17 για καλύτερη απόδοση.  
- **IDE** – IntelliJ IDEA ή Eclipse (τα παραδείγματα χρησιμοποιούν σύνταξη IntelliJ).  
- **Εργαλείο κατασκευής** – Maven ή Gradle για διαχείριση εξαρτήσεων.  

### Προσθήκη GroupDocs.Signature στο Project σας

Ο πιο εύκολος τρόπος είναι η προσθήκη της βιβλιοθήκης μέσω του εργαλείου κατασκευής. Δείτε πώς:

**Maven Users** – Προσθέστε το παρακάτω στο `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle Users** – Προσθέστε το παρακάτω στο `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Άμεση λήψη JAR** – Αν προτιμάτε χειροκίνητη εγκατάσταση, κατεβάστε το JAR από [GroupDocs.Signature releases](https://releases.groupdocs.com/signature/java/) και προσθέστε το στο classpath.

### Απόκτηση Άδειας

Το GroupDocs.Signature δεν είναι δωρεάν για παραγωγική χρήση, αλλά προσφέρει ευέλικτες επιλογές:

- **Δωρεάν Δοκιμή** – Κατεβάστε από τη [GroupDocs download page](https://releases.groupdocs.com/signature/java/) για δοκιμή (προστίθενται υδατογραφήματα αξιολόγησης).  
- **Προσωρινή Άδεια** – Λάβετε 30 ημέρες πλήρους πρόσβασης μέσω της [temporary license page του GroupDocs](https://purchase.groupdocs.com/temporary-license/) – ιδανική για proof‑of‑concept.  
- **Πλήρης Άδεια** – Για παραγωγικές εγκαταστάσεις, δείτε τις [επιλογές αγοράς του GroupDocs](https://purchase.groupdocs.com/buy).  

**Συμβουλή:** Ξεκινήστε με την προσωρινή άδεια για ανάπτυξη· αφαιρεί τα υδατογραφήματα όταν μεταβείτε σε μόνιμο κλειδί.

### Γρήγορος Έλεγχος Περιβάλλοντος

Αφού προσθέσετε την εξάρτηση, εκτελέστε ένα απλό smoke test:

```java
import com.groupdocs.signature.Signature;

public class SignatureTest {
    public static void main(String[] args) {
        try {
            Signature signature = new Signature("test.pdf");
            System.out.println("GroupDocs.Signature initialized successfully!");
            signature.dispose();
        } catch (Exception e) {
            System.err.println("Setup issue: " + e.getMessage());
        }
    }
}
```

Αν το πρόγραμμα τρέξει χωρίς σφάλματα, το περιβάλλον είναι έτοιμο. Σε περίπτωση προβλημάτων, ελέγξτε την έκδοση του JDK και την ακριβή έκδοση της βιβλιοθήκης που προσθέσατε.

## Πότε να Χρησιμοποιήσετε Υπογραφές Barcode

Οι υπογραφές barcode ξεχωρίζουν σε συγκεκριμένα σενάρια:

- **Εσωτερικές Ροές Εγγράφων** – Παρακολούθηση τιμολογίων, παραγγελιών ή σημειώσεων μέσω αλυσίδων έγκρισης.  
- **Υψηλού Όγκου Επεξεργασία** – Υπογραφή χιλιάδων εγγράφων γρήγορα· η δημιουργία barcode είναι έως **2× πιο γρήγορη** από την πλήρη ψηφιακή υπογραφή.  
- **Γέφυρες Εκτύπωση‑Σάρωση** – Τα barcode επιβιώνουν τον κύκλο εκτύπωσης‑σάρωσης, καθιστώντας τα ιδανικά για υβριδικές διαδικασίες.  
- **Ενσωμάτωση με Παλαιά Συστήματα** – Υπάρχοντες scanners μπορούν να διαβάσουν τις ετικέτες χωρίς πρόσθετο λογισμικό.  
- **Αλυσίδες Ελέγχου** – Ενσωματώστε IDs συναλλαγών ή χρονικές σφραγίδες που οι ελεγκτές μπορούν να επαληθεύσουν άμεσα.

Αποφύγετε τις υπογραφές barcode για νομικά συμβόλαια, έγγραφα υψηλής ασφάλειας ή εξωτερικές ανταλλαγές όπου απαιτούνται ψηφιακές υπογραφές PKI.

## Ρύθμιση GroupDocs.Signature για Java

### Ορισμός Κύριας Κλάσης

Η κλάση `Signature` είναι το σημείο εισόδου για όλες τις λειτουργίες υπογραφής, επαλήθευσης, αναζήτησης, ενημέρωσης και διαγραφής στο GroupDocs.Signature.

```java
import com.groupdocs.signature.Signature;
```

### Βασική Αρχικοποίηση

Δημιουργήστε ένα αντικείμενο `Signature` που δείχνει στο αρχείο στόχο:

```java
Signature signature = new Signature("path/to/your/document.pdf");
```

**Σημαντικές σημειώσεις**

- Οι διαδρομές μπορούν να είναι απόλυτες ή σχετικές· χρησιμοποιήστε `System.getProperty("user.home")` για συμβατότητα μεταξύ πλατφορμών.  
- Το GroupDocs υποστηρίζει **30+ μορφές εισόδου/εξόδου**, όπως PDF, DOCX, XLSX, PPTX και PNG.  
- Πάντα απελευθερώστε τους πόρους με `signature.dispose()` ή με μπλοκ try‑with‑resources:

```java
try (Signature signature = new Signature("path/to/your/document.pdf")) {
    // Your signing operations here
} catch (Exception e) {
    System.err.println("Error working with document: " + e.getMessage());
}
```

Τώρα είστε έτοιμοι να προσθέσετε barcodes.

## Πώς να προσθέσετε barcode σε PDF με Java;

Φορτώστε το πηγαίο PDF με `new Signature("input.pdf")`, διαμορφώστε ένα αντικείμενο `BarcodeSignature` (π.χ. Code128 με το κείμενο “John Smith”) και καλέστε `sign` για να δημιουργήσετε το υπογεγραμμένο αρχείο – όλα σε τρεις σύντομες γραμμές κώδικα. Η προσέγγιση αυτή ενσωματώνει μια μηχανικά αναγνώσιμη ετικέτα διατηρώντας το αρχικό layout, και λειτουργεί για οποιαδήποτε υποστηριζόμενη μορφή, όχι μόνο PDF.

### Υλοποίηση Βήμα‑βήμα

#### 1. Ορισμός Διαδρομών Αρχείων

Καθορίστε τις θέσεις των αρχείων εισόδου και εξόδου:

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/signed_sample.docx";
```

#### 2. Δημιουργία Handler Υπογραφής

Αρχικοποιήστε τον handler με το πηγαίο έγγραφο:

```java
Signature signature = new Signature(filePath);
```

#### 3. Διαμόρφωση Επιλογών Barcode

Ένα αντικείμενο `BarcodeSignature` ορίζει τις οπτικές και δεδομενικές ιδιότητες του barcode που θα ενσωματωθεί. Ορίστε τύπο barcode, κείμενο, θέση, μέγεθος, χρώμα και προαιρετική γραμματοσειρά για ανθρώπινη ανάγνωση:

```java
BarcodeSignOptions signOptions = new BarcodeSignOptions("John Smith", BarcodeTypes.Code128);
signOptions.setVerticalAlignment(VerticalAlignment.Top);
signOptions.setHorizontalAlignment(HorizontalAlignment.Center);
signOptions.setWidth(100);
signOptions.setHeight(40);
signOptions.setMargin(new java.awt.Rectangle(20, 20, 0, 0));
signOptions.setForeColor(Color.RED);

SignatureFont signatureFont = new SignatureFont();
signatureFont.setSize(12);
signatureFont.setFamilyName("Comic Sans MS");
signOptions.setFont(signatureFont);
```

> **Συμβουλή:** Αν το κείμενο υπερβαίνει τους 20 χαρακτήρες, αυξήστε το πλάτος του barcode για να αποφύγετε σφάλματα σάρωσης.

#### 4. Εφαρμογή Υπογραφής

Εκτελέστε τη λειτουργία υπογραφής και δημιουργήστε το αρχείο εξόδου:

```java
signature.sign(outputFilePath, signOptions);
```

#### 5. Παράδειγμα Πραγματικού Κόσμου

Σε σύστημα έγκρισης τιμολογίων, μπορείτε να ενσωματώσετε το ID του υπαλλήλου που εγκρίνει και μια χρονική σφραγίδα:

```java
String invoiceId = "INV-2025-0042";
String approver = "john.smith@company.com";
String timestamp = LocalDateTime.now().toString();

// Combine into barcode data
String barcodeData = invoiceId + "|" + approver + "|" + timestamp;

BarcodeSignOptions signOptions = new BarcodeSignOptions(barcodeData, BarcodeTypes.QR);
signOptions.setVerticalAlignment(VerticalAlignment.Bottom);
signOptions.setHorizontalAlignment(HorizontalAlignment.Right);

signature.sign(outputFilePath, signOptions);
```

Το παραγόμενο PDF περιέχει πλέον ένα σαρώνσιμο barcode που κωδικοποιεί όλα τα απαραίτητα μεταδεδομένα έγκρισης.

## Πώς να επαληθεύσετε μια υπογραφή barcode σε έγγραφο Java;

Η μέθοδος `Signature.verify` ελέγχει ένα έγγραφο για αντιστοιχίες barcode βάσει των παρεχόμενων επιλογών, επιστρέφοντας boolean που υποδεικνύει αν το αναμενόμενο barcode υπάρχει. Η επαλήθευση είναι χρήσιμη για αυτοματοποιημένες ροές εργασίας όπου πρέπει να επιβεβαιωθεί ότι το έγγραφο έχει επεξεργαστεί από το σωστό πρόσωπο πριν προχωρήσει.

### Βήματα Επαλήθευσης

#### 1. Φόρτωση Υπογεγραμμένου Εγγράφου

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");
```

#### 2. Ορισμός Κριτηρίων Επαλήθευσης

Καθορίστε το ακριβές κείμενο, τύπο barcode και αριθμό σελίδας που αναμένετε:

```java
BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
verifyOptions.setAllPages(false); // Only check the first page
verifyOptions.setPageNumber(1);
verifyOptions.setEncodeType(BarcodeTypes.Code128);
verifyOptions.setText("John Smith");
```

#### 3. Εκτέλεση Επαλήθευσης

Τρέξτε τον έλεγχο και διαχειριστείτε το αποτέλεσμα:

```java
boolean isValid = signature.verify(verifyOptions) != null;

if (isValid) {
    System.out.println("Document signature verified successfully!");
} else {
    System.out.println("Warning: Signature verification failed!");
}
```

**Κοινό μοτίβο:** Για απλή επιβεβαίωση ότι *οποιοδήποτε* barcode του συγκεκριμένου τύπου υπάρχει, παραλείψτε το φίλτρο `setText`:

```java
BarcodeVerifyOptions flexibleOptions = new BarcodeVerifyOptions();
flexibleOptions.setAllPages(true);
flexibleOptions.setEncodeType(BarcodeTypes.Code128);
// No setText() call = accept any text with this barcode type

boolean hasAnySignature = signature.verify(flexibleOptions) != null;
```

Ή επαληθεύστε μόνο τον τύπο barcode χωρίς να σας ενδιαφέρει το περιεχόμενο:

```java
BarcodeVerifyOptions formatOnly = new BarcodeVerifyOptions();
formatOnly.setEncodeType(BarcodeTypes.QR);
// Confirms a QR code exists, regardless of content
```

> **Προειδοποίηση:** Η επαλήθευση είναι case‑sensitive και whitespace‑sensitive· πάντα κάντε trim και κανονικοποίηση των δεδομένων πριν την υπογραφή.

## Πώς να αναζητήσετε υπογραφές barcode μέσα σε έγγραφο;

Η μέθοδος `Signature.search` σαρώει ένα έγγραφο για barcode που ταιριάζουν με τις `BarcodeSearchOptions`, επιστρέφοντας μια συλλογή που περιλαμβάνει τη θέση, τον αριθμό σελίδας και την κωδικοποιημένη τιμή κάθε barcode. Αυτή η δυνατότητα επιτρέπει εξαγωγή μεταδεδομένων μαζικά χωρίς να ανοίγετε κάθε αρχείο ξεχωριστά.

### Ροή Αναζήτησης

#### 1. Αρχικοποίηση Αναζήτησης

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");
```

#### 2. Διαμόρφωση Παραμέτρων Αναζήτησης

Καθορίστε εύρος σελίδων, τύπο barcode ή φίλτρα κειμένου:

```java
BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true); // Search the entire document
```

Προαιρετικά περιορίστε την αναζήτηση για καλύτερη απόδοση:

```java
BarcodeSearchOptions narrowSearch = new BarcodeSearchOptions();
narrowSearch.setAllPages(false);
narrowSearch.setPageNumber(1); // Only search page 1
narrowSearch.setEncodeType(BarcodeTypes.Code128); // Only find Code128 barcodes
```

#### 3. Εκτέλεση Αναζήτησης

```java
java.util.List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);

System.out.println("Found " + signatures.size() + " barcode signature(s)");

for (BarcodeSignature bcSignature : signatures) {
    System.out.println("Barcode Type: " + bcSignature.getEncodeType().getTypeName());
    System.out.println("Text: " + bcSignature.getText());
    System.out.println("Position: (" + bcSignature.getLeft() + ", " + bcSignature.getTop() + ")");
    System.out.println("Size: " + bcSignature.getWidth() + "x" + bcSignature.getHeight());
    System.out.println("---");
}
```

#### 4. Παράδειγμα Εξαγωγής Δεδομένων

Αποκτήστε δεδομένα έγκρισης από κάθε barcode σε παρτίδα τιμολογίων:

```java
List<BarcodeSignature> foundSignatures = signature.search(BarcodeSignature.class, searchOptions);

for (BarcodeSignature sig : foundSignatures) {
    String barcodeData = sig.getText();
    
    // Parse your custom format (remember our invoice example?)
    String[] parts = barcodeData.split("\\|");
    if (parts.length == 3) {
        String invoiceId = parts[0];
        String approver = parts[1];
        String timestamp = parts[2];
        
        System.out.println("Invoice " + invoiceId + " approved by " + approver + " at " + timestamp);
    }
}
```

> **Συμβουλή απόδοσης:** Για έγγραφα άνω των 100 σελίδων, περιορίστε πάντα την αναζήτηση στις σελίδες που περιέχουν barcode· αυτό μπορεί να μειώσει το χρόνο εκτέλεσης έως **70 %**.

## Πώς να ενημερώσετε υπάρχουσα υπογραφή barcode;

Η μέθοδος `Signature.update` τροποποιεί οπτικά χαρακτηριστικά μιας υπάρχουσας υπογραφής barcode—όπως θέση, μέγεθος ή χρώμα—διατηρώντας τα αρχικά κωδικοποιημένα δεδομένα. Χρήσιμη όταν απαιτούνται αλλαγές layout μετά την αρχική υπογραφή.

### Διαδικασία Ενημέρωσης

#### 1. Εύρεση Υπογραφών προς Ενημέρωση

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");

BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true);

List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
```

#### 2. Τροποποίηση Επιθυμητών Ιδιοτήτων

```java
List<BarcodeSignature> signaturesToUpdate = new ArrayList<>();

if (!signatures.isEmpty()) {
    BarcodeSignature bcSignature = signatures.get(0); // Update the first found signature
    
    // Move it 100px right and 100px down
    bcSignature.setLeft(bcSignature.getLeft() + 100);
    bcSignature.setTop(bcSignature.getTop() + 100);
    
    // Make it bigger
    bcSignature.setWidth(200);
    bcSignature.setHeight(50);
    
    signaturesToUpdate.add(bcSignature);
}
```

Μπορείτε να αλλάξετε πολλαπλές ιδιότητες ταυτόχρονα:

```java
bcSignature.setLeft(50);
bcSignature.setTop(50);
bcSignature.setWidth(150);
bcSignature.setHeight(45);
// Note: You can't change the encoded text or barcode type with update
// For that, you'd need to delete and re-sign
```

#### 3. Αποθήκευση Αλλαγών

```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature.update(outputStream, signaturesToUpdate);

// If you want to save to a file instead:
// signature.update("path/to/updated_document.docx", signaturesToUpdate);
```

#### 4. Παράδειγμα Πραγματικού Σεναρίου

Ανατοποθετήστε όλες τις υπογραφές ώστε να μην επικαλύπτονται με νέο λογότυπο εταιρείας:

```java
List<BarcodeSignature> allSignatures = signature.search(BarcodeSignature.class, searchOptions);
List<BarcodeSignature> toUpdate = new ArrayList<>();

for (BarcodeSignature sig : allSignatures) {
    // Move all signatures down by 50px to clear space for new logo
    if (sig.getTop() < 100) {
        sig.setTop(sig.getTop() + 50);
        toUpdate.add(sig);
    }
}

if (!toUpdate.isEmpty()) {
    signature.update(outputStream, toUpdate);
    System.out.println("Repositioned " + toUpdate.size() + " signature(s)");
}
```

> **Περιορισμός:** Η αλλαγή του κωδικοποιημένου κειμένου απαιτεί διαγραφή και νέα εισαγωγή υπογραφής.

## Πώς να διαγράψετε υπογραφές barcode από έγγραφο;

Η μέθοδος `Signature.delete` αφαιρεί μόνιμα επιλεγμένες υπογραφές barcode από ένα έγγραφο, διαγράφοντας τόσο το οπτικό στοιχείο όσο και τα κωδικοποιημένα δεδομένα. Χρησιμοποιήστε αυτή τη λειτουργία για καθαρισμό δοκιμαστικών υπογραφών ή όταν ένα barcode δεν είναι πλέον απαραίτητο.

### Βήματα Διαγραφής

#### 1. Εντοπισμός Υπογραφών

```java
Signature signature = new Signature("YOUR_OUTPUT_DIRECTORY/signed_sample.docx");

BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(true);

List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
```

#### 2. Διαγραφή Επιλεγμένων Υπογραφών

```java
List<BarcodeSignature> signaturesToDelete = new ArrayList<>();

// Delete all Code128 signatures (for example)
for (BarcodeSignature sig : signatures) {
    if (sig.getEncodeType().equals(BarcodeTypes.Code128)) {
        signaturesToDelete.add(sig);
    }
}

if (!signaturesToDelete.isEmpty()) {
    boolean result = signature.delete(signaturesToDelete);
    
    if (result) {
        System.out.println("Successfully deleted " + signaturesToDelete.size() + " signature(s)");
    } else {
        System.err.println("Failed to delete signatures");
    }
}
```

#### 3. Παράδειγμα Υποβολής Συνθηκών

Διαγράψτε μόνο τα barcode παλαιότερα από συγκεκριμένη χρονική σφραγίδα (υποθέτοντας ότι η σφραγίδα είναι μέρος του κειμένου):

```java
LocalDateTime cutoffDate = LocalDateTime.now().minusDays(30);
List<BarcodeSignature> outdatedSignatures = new ArrayList<>();

for (BarcodeSignature sig : signatures) {
    try {
        String text = sig.getText();
        // Assuming format like "data|timestamp"
        String[] parts = text.split("\\|");
        if (parts.length > 1) {
            LocalDateTime sigDate = LocalDateTime.parse(parts[1]);
            if (sigDate.isBefore(cutoffDate)) {
                outdatedSignatures.add(sig);
            }
        }
    } catch (Exception e) {
        // Skip signatures that don't match our format
        continue;
    }
}

if (!outdatedSignatures.isEmpty()) {
    signature.delete(outdatedSignatures);
    System.out.println("Removed " + outdatedSignatures.size() + " outdated signature(s)");
}
```

> **Προειδοποίηση:** Η διαγραφή δεν μπορεί να αναιρεθεί· πάντα εργάζεστε σε αντίγραφο των παραγωγικών αρχείων κατά τη δοκιμή.

#### 4. Μοτίβο Μαζικής Διαγραφής

Καθαρίστε τις δοκιμαστικές υπογραφές πριν από μια έκδοση:

```java
// Remove all signatures containing "TEST" in their text
List<BarcodeSignature> testSignatures = signatures.stream()
    .filter(sig -> sig.getText().toUpperCase().contains("TEST"))
    .collect(Collectors.toList());

if (!testSignatures.isEmpty()) {
    signature.delete(testSignatures);
    System.out.println("Cleaned up " + testSignatures.size() + " test signature(s)");
}
```

## Τύποι Barcode: Πρακτικός Οδηγός

Η επιλογή του κατάλληλου barcode επηρεάζει την αξιοπιστία σάρωσης, τη χωρητικότητα δεδομένων και τη συμβατότητα εκτυπωτών.

### Code128 (Η πιο Συνηθισμένη Επιλογή)

- **Πότε να το χρησιμοποιήσετε:** Αλφαριθμητικά δεδομένα, υψηλή πυκνότητα, έντυπα έγγραφα.  
- **Πλεονεκτήματα:** Συμπαγές, λειτουργεί με τυπικούς scanners, εκτυπώνεται καθαρά σε μικρά μεγέθη.  
- **Μειονεκτήματα:** Περιορισμένο σε ASCII, λιγότερο ανθεκτικό σε σφάλματα από 2‑D κώδικες.  

Παράδειγμα:

```java
BarcodeSignOptions code128 = new BarcodeSignOptions("INV-2025-042", BarcodeTypes.Code128);
```

### QR Code (Καλύτερο για Κινητά)

- **Πότε να το χρησιμοποιήσετε:** Σάρωση από κινητά, μεγάλα φορτία δεδομένων (URLs, JSON κ.λπ.), έγγραφα που μπορεί να υποστούν ζημιά.  
- **Πλεονεκτήματα:** Έως 4 000 χαρακτήρες, ενσωματωμένη διόρθωση σφαλμάτων, φιλικό προς smartphones.  
- **Μειονεκτήματα:** Μεγαλύτερο οπτικό αποτύπωμα, απαιτεί υψηλότερη ανάλυση για μικρά μεγέθη.  

Παράδειγμα:

```java
String jsonData = "{\"invoice\":\"INV-042\",\"amount\":1500.00,\"approver\":\"john@company.com\"}";
BarcodeSignOptions qrCode = new BarcodeSignOptions(jsonData, BarcodeTypes.QR);
```

### Code39 (Παραδοσιακός)

- **Πότε να το χρησιμοποιήσετε:** Περιβάλλοντα με παλαιούς scanners, ανάγκη για ανθρώπινη ανάγνωση κειμένου.  
- **Πλεονεκτήματα:** Ευρεία υποστήριξη legacy, απλή μορφή, δεν απαιτεί checksum.  
- **Μειονεκτήματα:** Χαμηλή πυκνότητα δεδομένων, περιορισμένο σύνολο χαρακτήρων, καταλαμβάνει περισσότερο χώρο.  

### Data Matrix (Συμπαγής Δύναμη)

- **Πότε να το χρησιμοποιήσετε:** Εξαιρετικά περιορισμένος χώρος, σήμανση μικροσκοπικών αντικειμένων, υψηλή πυκνότητα δεδομένων.  
- **Πλεονεκτήματα:** Πολύ συμπαγές, ισχυρή διόρθωση σφαλμάτων, λειτουργεί σε κυρτές επιφάνειες.  
- **Μειονεκτήματα:** Απαιτεί υψηλής ποιότητας εκτύπωση, λιγότερη υποστήριξη από scanners.  

#### Γρήγορη Σύγκριση

| Τύπος Barcode | Χωρητικότητα Δεδομένων | Κατάλληλο για | Τυπικό Μέγεθος |
|---------------|------------------------|----------------|-----------------|
| Code128       | ~100 χαρακτήρες        | Γενική σήμανση | Μικρό |
| QR Code       | ~4 000 χαρακτήρες      | Σάρωση από κινητά, πλούσια δεδομένα | Μεσαίο |
| Code39        | ~43 χαρακτήρες         | Παλαιά υλικά | Μεγάλο |
| Data Matrix   | ~3 000 χαρακτήρες      | Μικροί χώροι, βιομηχανικά tags | Πολύ μικρό |

**Σύσταση:** Ξεκινήστε με **Code128** για απλά IDs. Μεταβείτε σε **QR** όταν χρειάζεστε URLs ή μεγαλύτερα payloads. Χρησιμοποιήστε **Code39** μόνο για legacy ενσωματώσεις.

## Συχνά Προβλήματα & Λύσεις

### Πρόβλημα: “Barcode Not Found During Verification”

**Συμπτώματα:** Η επαλήθευση επιστρέφει `false` παρόλο που το barcode είναι ορατό.

**Τυπικές αιτίες**

1. Μη αντιστοίχιση κεφαλαίων/μικρών (π.χ. “John Smith” vs. “john smith”).  
2. Επιπλέον κενά στο κωδικοποιημένο κείμενο.  
3. Λάθος τύπος barcode στα options επαλήθευσης.  
4. Αναζήτηση σε λάθος αριθμό σελίδας.

**Λύση:** Κανονικοποιήστε το κείμενο πριν την υπογραφή και επαλήθευση, και βεβαιωθείτε ότι το `setEncodeType` ταιριάζει με τον αρχικό τύπο.

```java
// Always normalize your data
String signatureText = originalText.trim().toLowerCase();

// When signing:
BarcodeSignOptions signOptions = new BarcodeSignOptions(signatureText, BarcodeTypes.Code128);

// When verifying:
BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
verifyOptions.setText(signatureText); // Use the same normalized text
verifyOptions.setEncodeType(BarcodeTypes.Code128);
```

### Πρόβλημα: “Barcode Appears Blurry or Unreadable”

**Συμπτώματα:** Τα εκτυπωμένα barcodes δεν μπορούν να σαρωθούν.

**Αιτίες**

- Διαστάσεις barcode πολύ μικρές για το κείμενο.  
- Ρυθμίσεις εκτυπωτή χαμηλής ανάλυσης.  
- Ανεπαρκής αντίθεση χρώματος barcode‑προσκηνίου.

**Λύση:** Αυξήστε το πλάτος/ύψος του barcode, χρησιμοποιήστε υψηλής αντίθεσης χρώματα (μαύρο σε λευκό) και ορίστε DPI εκτυπωτή τουλάχιστον 300 dpi.

```java
// Increase size for longer strings
int dataLength = barcodeText.length();
int minWidth = Math.max(100, dataLength * 10); // 10px per character minimum

BarcodeSignOptions signOptions = new BarcodeSignOptions(barcodeText, BarcodeTypes.Code128);
signOptions.setWidth(minWidth);
signOptions.setHeight(60); // Taller = easier to scan

// Use high-contrast colors
signOptions.setForeColor(Color.BLACK); // Black on white is most reliable
signOptions.setBackColor(Color.WHITE);
```

### Πρόβλημα: “OutOfMemoryError with Large Documents”

**Συμπτώματα:** Η εφαρμογή καταρρέει όταν επεξεργάζεται PDF με εκατοντάδες σελίδες.

**Αιτία:** Η βιβλιοθήκη φορτώνει ολόκληρο το έγγραφο στη μνήμη.

**Λύση:** Ενεργοποιήστε λειτουργία streaming και επεξεργαστείτε τις σελίδες διαδοχικά.

```java
// Process pages in batches instead of all at once
BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
searchOptions.setAllPages(false);

List<BarcodeSignature> allSignatures = new ArrayList<>();

for (int page = 1; page <= totalPages; page++) {
    searchOptions.setPageNumber(page);
    List<BarcodeSignature> pageSignatures = signature.search(BarcodeSignature.class, searchOptions);
    allSignatures.addAll(pageSignatures);
    
    // Process and clear as you go
    if (page % 10 == 0) {
        System.gc(); // Suggest garbage collection every 10 pages
    }
}
```

### Πρόβλημα: “Signature Position Inconsistent Across Document Types”

**Συμπτώματα:** Τα barcodes εμφανίζονται σε διαφορετικές θέσεις όταν υπογράφετε PDF vs. Word.

**Αιτία:** Το PDF χρησιμοποιεί προέλευση κάτω‑αριστερά, ενώ το Word χρησιμοποιεί πάνω‑αριστερά.

**Λύση:** Ανιχνεύστε τον τύπο εγγράφου και εφαρμόστε την κατάλληλη μετασχηματιστική συντεταγμένη.

```java
// Use relative positioning instead of absolute
signOptions.setVerticalAlignment(VerticalAlignment.Bottom);
signOptions.setHorizontalAlignment(HorizontalAlignment.Right);

// Then use margins for fine-tuning
Padding margin = new Padding();
margin.setRight(50); // 50px from right edge
margin.setBottom(50); // 50px from bottom
signOptions.setMargin(margin);

// This works consistently across PDF, DOCX, XLSX, etc.
```

### Πρόβλημα: “Updated Signatures Lose Formatting”

**Συμπτώματα:** Μετά το `update`, το χρώμα ή η γραμματοσειρά του barcode αλλάζουν απροσδόκητα.

**Αιτία:** Δεν αποθηκεύονται όλες οι οπτικές ιδιότητες κατά την ενημέρωση.

**Λύση:** Εφαρμόστε ξανά τις οπτικές ρυθμίσεις μετά την κλήση `update`.

```java
// When updating, explicitly set all visual properties
bcSignature.setLeft(newLeft);
bcSignature.setTop(newTop);
bcSignature.setWidth(originalWidth); // Don't forget these!
bcSignature.setHeight(originalHeight);
// Note: Color and font can't be updated - you'd need to delete and re-sign
```

## Καλές Πρακτικές για Παραγωγή

### Βελτιστοποίηση Απόδοσης

1. **Επαναχρησιμοποίηση Αντικειμένων Signature** – Δημιουργήστε ένα αντικείμενο `Signature` ανά έγγραφο και επαναχρησιμοποιήστε το για πολλαπλές λειτουργίες.

```java
// Bad - Creates new instance each time
public void processDocument(String path) {
    Signature sig1 = new Signature(path);
    sig1.search(/* ... */);
    
    Signature sig2 = new Signature(path); // Unnecessary reload
    sig2.verify(/* ... */);
}

// Good - Reuse the same instance
public void processDocument(String path) {
    try (Signature signature = new Signature(path)) {
        signature.search(/* ... */);
        signature.verify(/* ... */);
        signature.update(/* ... */);
    }
}
```

2. **Αναζήτηση Μόνο σε Σχετικές Σελίδες** – Περιορίστε το εύρος σελίδων στα σημεία όπου αναμένεται barcode.

```java
// Slow for 100+ page documents
BarcodeSearchOptions slowSearch = new BarcodeSearchOptions();
slowSearch.setAllPages(true);

// Fast - only check where signatures actually are
BarcodeSearchOptions fastSearch = new BarcodeSearchOptions();
fastSearch.setAllPages(false);
fastSearch.setPageNumber(1); // Only check cover page
```

3. **Επιλογή Απλούστερου Τύπου Barcode** – Τα απλούστερα barcodes παράγουν πιο γρήγορα· χρησιμοποιήστε QR ή Data Matrix μόνο όταν χρειάζεστε επιπλέον χωρητικότητα.

```java
// Overkill for simple IDs
BarcodeSignOptions slow = new BarcodeSignOptions("12345", BarcodeTypes.QR);

// Faster and more appropriate
BarcodeSignOptions fast = new BarcodeSignOptions("12345", BarcodeTypes.Code128);
```

### Θεωρήσεις Ασφάλειας

1. **Μην Κωδικοποιείτε Ευαίσθητα Προσωπικά Δεδομένα** – Τα barcodes διαβάζονται εύκολα· αποφύγετε SSN ή κωδικούς πρόσβασης.

```java
// Bad - exposes sensitive data
String barcodeData = "SSN:123-45-6789|Password:hunter2";

// Good - use reference IDs
String barcodeData = "USER-REF-7721X"; // Look up sensitive data server-side
```

2. **Επαλήθευση στην Πλευρά του Server** – Μην εμπιστεύεστε μόνο την επαλήθευση στην πλευρά του client· επαληθεύστε πάντα και στο αξιόπιστο backend.

```java
// Client scans barcode and extracts "APPROVED-BY-ADMIN"
// Always verify server-side:
public boolean verifyApproval(String documentId, String scannedData) {
    // Load document from secure storage
    Signature signature = new Signature(getSecureDocument(documentId));
    
    BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
    verifyOptions.setText(scannedData);
    
    boolean isValid = signature.verify(verifyOptions) != null;
    
    // Also check against your database
    boolean isInDatabase = checkApprovalDatabase(documentId, scannedData);
    
    return isValid && isInDatabase;
}
```

3. **Προσθήκη Χρονικής Σφραγίδας** – Συμπεριλάβετε timestamp στο payload του barcode για αποφυγή replay attacks.

```java
import java.time.LocalDateTime;
import java.time.temporal.ChronoUnit;

String timestamp = LocalDateTime.now().truncatedTo(ChronoUnit.SECONDS).toString();
String barcodeData = "APPROVAL|" + userId + "|" + timestamp;

// When verifying, check the timestamp isn't too old
public boolean isSignatureRecent(String barcodeData, int maxAgeHours) {
    String[] parts = barcodeData.split("\\|");
    if (parts.length < 3) return false;
    
    LocalDateTime signatureTime = LocalDateTime.parse(parts[2]);
    LocalDateTime now = LocalDateTime.now();
    
    long hoursSince = ChronoUnit.HOURS.between(signatureTime, now);
    return hoursSince <= maxAgeHours;
}
```

### Μοτίβα Διαχείρισης Σφαλμάτων

- **Χρησιμοποιείτε πάντα Try‑With‑Resources** για να διασφαλίσετε την απελευθέρωση των αντικειμένων `Signature`.

```java
try (Signature signature = new Signature(documentPath)) {
    // Your operations here
    signature.sign(outputPath, signOptions);
} catch (Exception e) {
    logger.error("Failed to sign document: " + documentPath, e);
    throw new DocumentSigningException("Could not process document", e);
}
```

- **Επικυρώστε την Πρόσβαση στα Αρχεία** πριν προσπαθήσετε να υπογράψετε.

```java
public void signDocument(String inputPath, String outputPath) {
    File inputFile = new File(inputPath);
    
    if (!inputFile.exists()) {
        throw new IllegalArgumentException("Input file not found: " + inputPath);
    }
    
    if (!inputFile.canRead()) {
        throw new SecurityException("Cannot read input file: " + inputPath);
    }
    
    File outputDir = new File(outputPath).getParentFile();
    if (outputDir != null && !outputDir.exists()) {
        outputDir.mkdirs();
    }
    
    try (Signature signature = new Signature(inputPath)) {
        signature.sign(outputPath, signOptions);
    }
}
```

- **Συγχρονίστε την Πρόσβαση** εάν πολλαπλά νήματα ενδέχεται να εργάζονται στο ίδιο αρχείο.

```java
import java.util.concurrent.locks.ReentrantLock;
import java.util.concurrent.ConcurrentHashMap;

public class SignatureManager {
    private final ConcurrentHashMap<String, ReentrantLock> documentLocks = new ConcurrentHashMap<>();
    
    public void signDocument(String documentPath, BarcodeSignOptions options) {
        ReentrantLock lock = documentLocks.computeIfAbsent(documentPath, k -> new ReentrantLock());
        
        lock.lock();
        try (Signature signature = new Signature(documentPath)) {
            signature.sign(documentPath + ".signed", options);
        } finally {
            lock.unlock();
        }
    }
}
```

### Δοκιμή Υλοποίησης

**Πρότυπο Μονάδας Δοκιμής**

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.io.TempDir;
import static org.junit.jupiter.api.Assertions.*;

public class BarcodeSignatureTest {
    
    @TempDir
    Path tempDir;
    
    @Test
    public void testSignAndVerify() throws Exception {
        // Setup
        String testDoc = "test-document.pdf";
        String outputDoc = tempDir.resolve("signed-test.pdf").toString();
        String testData = "TEST-USER-12345";
        
        // Sign
        try (Signature signature = new Signature(testDoc)) {
            BarcodeSignOptions signOptions = new BarcodeSignOptions(testData, BarcodeTypes.Code128);
            signature.sign(outputDoc, signOptions);
        }
        
        // Verify
        try (Signature signature = new Signature(outputDoc)) {
            BarcodeVerifyOptions verifyOptions = new BarcodeVerifyOptions();
            verifyOptions.setText(testData);
            verifyOptions.setEncodeType(BarcodeTypes.Code128);
            
            boolean isValid = signature.verify(verifyOptions) != null;
            assertTrue(isValid, "Signature should be valid");
        }
    }
    
    @Test
    public void testSearchFindsSignature() throws Exception {
        String signedDoc = "signed-document.pdf";
        
        try (Signature signature = new Signature(signedDoc)) {
            BarcodeSearchOptions searchOptions = new BarcodeSearchOptions();
            searchOptions.setAllPages(true);
            
            List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, searchOptions);
            
            assertFalse(signatures.isEmpty(), "Should find at least one signature");
            assertEquals("TEST-USER-12345", signatures.get(0).getText());
        }
    }
}
```

**Λίστα Ελέγχου Ενσωμάτωσης**

- ✅ Δοκιμή όλων των υποστηριζόμενων μορφών (PDF, DOCX, XLSX, PPTX, PNG).  
- ✅ Επαλήθευση ότι τα barcodes επιβιώνουν κύκλο εκτύπωση‑σάρωση.  
- ✅ Δοκιμή με μέγιστα μήκη δεδομένων.  
- ✅ Επιβεβαίωση θέσης σε A4, Letter και προσαρμοσμένα μεγέθη σελίδας.  
- ✅ Ταυτόχρονη υπογραφή πολλαπλών εγγράφων.  
- ✅ Παρακολούθηση χρήσης μνήμης για έγγραφα > 500 σελίδες.  
- ✅ Διασφάλιση ότι οι barcode scanners διαβάζουν αξιόπιστα το αποτέλεσμα.

### Καταγραφή και Παρακολούθηση

Προσθέστε κατανοητά logs γύρω από κάθε λειτουργία:

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class DocumentSigningService {
    private static final Logger logger = LoggerFactory.getLogger(DocumentSigningService.class);
    
    public void signDocument(String docPath, String barcodeData) {
        logger.info("Starting signature process for document: {}", docPath);
        logger.debug("Barcode data length: {} characters", barcodeData.length());
        
        try (Signature signature = new Signature(docPath)) {
            BarcodeSignOptions options = new BarcodeSignOptions(barcodeData, BarcodeTypes.Code128);
            
            long startTime = System.currentTimeMillis();
            signature.sign(docPath + ".signed", options);
            long duration = System.currentTimeMillis() - startTime;
            
            logger.info("Successfully signed document in {}ms", duration);
        } catch (Exception e) {
            logger.error("Failed to sign document: {}", docPath, e);
            throw new RuntimeException("Signature operation failed", e);
        }
    }
}
```

Παρακολουθήστε βασικές μετρήσεις όπως χρόνος επεξεργασίας, χρήση μνήμης και ποσοστά σφαλμάτων:

```java
// Track success/failure rates
metricsService.incrementCounter("signature.sign.success");
metricsService.incrementCounter("signature.verify.failure");

// Track performance
metricsService.recordTimer("signature.sign.duration", duration);

// Track document sizes
metricsService.recordHistogram("signature.document.pages", pageCount);
```

## Συμβουλές από Πραγματική Χρήση

**Στρατηγική Μαζικής Επεξεργασίας**

Όταν διαχειρίζεστε εκατοντάδες αρχεία, επεξεργαστείτε τα σε παρτίδες και αναφέρετε πρόοδο:

```java
public void signBatch(List<String> documents, String barcodePrefix) {
    int total = documents.size();
    int completed = 0;
    int failed = 0;
    
    for (String docPath : documents) {
        try {
            String barcodeData = barcodePrefix + "-" + UUID.randomUUID().toString();
            signDocument(docPath, barcodeData);
            completed++;
            
            if (completed % 10 == 0) {
                logger.info("Progress: {}/{} documents signed", completed, total);
            }
        } catch (Exception e) {
            failed++;
            logger.warn("Failed to sign: {}", docPath, e);
        }
    }
    
    logger.info("Batch complete: {} succeeded, {} failed", completed, failed);
}
```

**Εξωτερική Διαμόρφωση**

Αποθηκεύστε τις ρυθμίσεις barcode (τύπος, μέγεθος, χρώμα) σε αρχείο properties για εύκολη ρύθμιση χωρίς επαναμεταγλώττιση:

```java
public class BarcodeConfig {
    private int defaultWidth = 100;
    private int defaultHeight = 40;
    private String defaultBarcodeType = "Code128";
    private String defaultColor = "BLACK";
    
    // Load from properties file or environment variables
    public BarcodeConfig() {
        this.defaultWidth = Integer.parseInt(
            System.getProperty("barcode.width", "100")
        );
        // ... load other properties
    }
    
    public BarcodeSignOptions createDefaultOptions(String text) {
        BarcodeSignOptions options = new BarcodeSignOptions(text, getBarcodeType());
        options.setWidth(defaultWidth);
        options.setHeight(defaultHeight);
        options.setForeColor(getColor());
        return options;
    }
}
```

**Τυποποίηση Payload Barcode**

Χρησιμοποιήστε διαχωριστικό μορφότυπο όπως `EMPID|TIMESTAMP|DOCID` για απλή και συνεπή ανάλυση:

```java
public class BarcodeDataBuilder {
    private String userId;
    private String action;
    private LocalDateTime timestamp;
    private String documentId;
    
    public BarcodeDataBuilder setUserId(String userId) {
        this.userId = userId;
        return this;
    }
    
    public BarcodeDataBuilder setAction(String action) {
        this.action = action;
        return this;
    }
    
    public BarcodeDataBuilder setDocumentId(String documentId) {
        this.documentId = documentId;
        return this;
    }
    
    public String build() {
        this.timestamp = LocalDateTime.now();
        
        // Format: VERSION|USER|ACTION|DOC_ID|TIMESTAMP|CHECKSUM
        String data = String.join("|",
            "v1",
            userId,
            action,
            documentId,
            timestamp.toString()
        );
        
        // Add simple checksum
        int checksum = data.hashCode();
        return data + "|" + checksum;
    }
    
    public static ParsedBarcodeData parse(String barcodeData) {
        String[] parts = barcodeData.split("\\|");
        if (parts.length != 6 || !parts[0].equals("v1")) {
            throw new IllegalArgumentException("Invalid barcode format");
        }
        
        return new ParsedBarcodeData(parts[1], parts[2], parts[3], 
                                     LocalDateTime.parse(parts[4]));
    }
}

// Usage:
String barcodeData = new BarcodeDataBuilder()
    .setUserId("john.smith")
    .setAction("APPROVED")
    .setDocumentId("INV-2025-042")
    .build();
```

**Αυτόματη Ανίχνευση Τύπου Εγγράφου**

Προσαρμόστε τις διαστάσεις barcode ανάλογα με το αν το στόχο είναι PDF, Word ή εικόνα:

```java
public BarcodeSignOptions getOptimalOptions(String documentPath, String text) {
    String extension = documentPath.substring(documentPath.lastIndexOf(".") + 1).toLowerCase();
    
    BarcodeSignOptions options = new BarcodeSignOptions(text, BarcodeTypes.Code128);
    
    switch (extension) {
        case "pdf":
            // PDFs can handle larger, detailed barcodes
            options.setWidth(150);
            options.setHeight(50);
            break;
        case "docx":
        case "doc":
            // Word docs need compact signatures that don't disrupt flow
            options.setWidth(100);
            options.setHeight(35);
            options.setVerticalAlignment(VerticalAlignment.Bottom);
            break;
        case "xlsx":
        case "xls":
            // Excel needs signatures that don't obscure data
            options.setWidth(80);
            options.setHeight(30);
            options.setHorizontalAlignment(HorizontalAlignment.Right);
            break;
        default:
            // Safe defaults
            options.setWidth(100);
            options.setHeight(40);
    }
    
    return options;
}
```

## Πρόσθετοι Πόροι

- [GroupDocs.Signature documentation](https://docs.groupdocs.com/signature/java/) – Πλήρης οδηγός API και παραδείγματα.  
- [GroupDocs support forum](https://forum.groupdocs.com/c/signature/13) – Κοινότητα και βοήθεια.  
- [API reference](https://apireference.groupdocs.com/signature/java) – Λεπτομερείς περιγραφές μεθόδων και παραμέτρων.

## Συχνές Ερωτήσεις

**Ε: Μπορώ να χρησιμοποιήσω το GroupDocs.Signature με Java 17;**  
Α: Ναι – η βιβλιοθήκη είναι πλήρως συμβατή με JDK 8, 11 και 17.

**Ε: Επιβιώνει το barcode μετά από κύκλο εκτύπωση‑σάρωση;**  
Α: Όταν χρησιμοποιείτε Code128 ή QR με επαρκές μέγεθος και αντίθεση, το barcode παραμένει αναγνώσιμο μετά την εκτύπωση και τη σάρωση.

**Ε: Πόσα barcodes μπορεί να περιέχει ένα έγγραφο;**  
Α: Δεν υπάρχει σκληρό όριο· ωστόσο, για βέλτιστη απόδοση, κρατήστε τον συνολικό αριθμό κάτω από **200** ανά έγγραφο.

**Ε: Απαιτείται άδεια για builds ανάπτυξης;**  
Α: Μία προσωρινή άδεια αφαιρεί τα υδατογραφήματα αξιολόγησης· πλήρης άδεια είναι υποχρεωτική για οποιαδήποτε παραγωγική ανάπτυξη.

**Ε: Μπορώ να υπογράψω PDF με κωδικό πρόσβασης;**  
Α: Ναι – παρέχετε τον κωδικό όταν δημιουργείτε το αντικείμενο `Signature`; το API θα ξεκλειδώσει το αρχείο εσωτερικά.

---

**Τελευταία ενημέρωση:** 2026-07-15  
**Δοκιμασμένο με:** GroupDocs.Signature 23.9 for Java  
**Συγγραφέας:** GroupDocs  

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

## Σχετικά Tutorials

- [How to Verify Barcode Signatures in Java with GroupDocs.Signature](/signature/java/search-verification/groupdocs-signature-java-document-verification/)
- [How to Search Digital Signatures in Java Documents with GroupDocs](/signature/java/search-verification/groupdocs-signature-java-digital-search-tutorial/)
- [Java Barcode Signature Tutorial - Add, Verify & Manage Barcodes in PDFs](/signature/java/barcode-signatures/)