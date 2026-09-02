---
categories:
- Document Signing
- Healthcare Integration
date: '2026-05-16'
description: Μάθετε πώς να δημιουργήσετε PDF Data Matrix και να προσθέσετε PDF QR
  code χρησιμοποιώντας το GroupDocs.Signature για Java. Οδηγός βήμα‑βήμα για την υπογραφή
  εγγράφων υγειονομικής περίθαλψης.
keywords:
- create data matrix pdf
- add qr code pdf
- HIBC barcode Java
lastmod: '2026-05-16'
linktitle: Οδηγός Υπογραφής HIBC PDF σε Java
schemas:
- author: GroupDocs
  dateModified: '2026-05-16'
  description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  headline: Create Data Matrix PDF with HIBC Barcode in Java
  type: TechArticle
- description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  name: Create Data Matrix PDF with HIBC Barcode in Java
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
  type: HowTo
- questions:
  - answer: Yes, it also supports DOCX, XLSX, PPTX, PNG, JPEG, and TIFF with the same
      barcode‑signing API.
    question: Can GroupDocs.Signature sign file types other than PDF?
  - answer: Verify that your HIBC string follows the exact HIBCC syntax, use the online
      validator, and ensure you’re using the correct `QrCodeTypes` constant for the
      chosen format.
    question: How do I troubleshoot “Invalid barcode content” errors?
  - answer: QR ≈ 4,296 alphanumeric characters, Aztec ≈ 3,832 numeric / 3,067 alphanumeric,
      Data Matrix ≈ 3,116 numeric / 2,335 alphanumeric. Keep codes under 200 characters
      for optimal scan reliability.
    question: What is the maximum data capacity for each HIBC format?
  - answer: Absolutely. Create separate `QrCodeSignOptions` objects with different
      positions and call `signature.sign()` for each. Just ensure they don’t overlap.
    question: Is it possible to embed multiple barcode types in one PDF?
  - answer: No. After the JAR is on the classpath and the license is activated, all
      operations are performed locally.
    question: Do I need an internet connection for signing at runtime?
  type: FAQPage
tags:
- java
- pdf-signing
- hibc
- healthcare
- barcode
- pharmaceutical
title: Δημιουργία PDF Data Matrix με HIBC Barcode σε Java
type: docs
url: /el/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/
weight: 1
---

# Δημιουργία Data Matrix PDF με HIBC Barcode σε Java

Αν δημιουργείτε λογισμικό φαρμακευτικής ή υγειονομικής εφοδιαστικής αλυσίδας, πιθανότατα έχετε αντιμετωπίσει το πρόβλημα της παρακολούθησης με χαρτί, χαμένων υπογραφών και εφιάλτες ελέγχων. **Δημιουργώντας ένα Data Matrix PDF** που ενσωματώνει έναν κωδικό HIBC LIC λύνει αυτά τα προβλήματα παρέχοντας ένα αδιάβλητο, μηχανικά αναγνώσιμο ίχνος που αντέχει στην εκτύπωση, τη σάρωση και την κανονιστική ανασκόπηση. Σε αυτό το σεμινάριο θα δείτε ακριβώς πώς να **προσθέσετε υποστήριξη QR code PDF**, καθώς και μορφές Aztec και Data Matrix, χρησιμοποιώντας το GroupDocs.Signature for Java.

## Γρήγορες Απαντήσεις
- **Ποια βιβλιοθήκη διαχειρίζεται τους κωδικούς HIBC σε Java;** GroupDocs.Signature for Java.  
- **Ποια μορφή κωδικού είναι η πιο συμπαγής;** Data Matrix – ιδανική για μικρές ετικέτες.  
- **Μπορώ να προσθέσω τόσο QR όσο και Data Matrix στο ίδιο PDF;** Ναι, απλώς δημιουργήστε ξεχωριστά `QrCodeSignOptions`.  
- **Χρειάζεται σύνδεση στο διαδίκτυο κατά την εκτέλεση;** Όχι, η βιβλιοθήκη λειτουργεί πλήρως offline μετά την εγκατάσταση.  
- **Ποια έκδοση Java συνιστάται;** Java 11+ για απόδοση παραγωγικού επιπέδου.

## Τι είναι η υπογραφή PDF με κωδικό HIBC;
Η κλάση `Signature` στο GroupDocs.Signature for Java αντιπροσωπεύει ένα έγγραφο PDF και παρέχει μεθόδους για ενσωμάτωση κωδικών HIBC ως ψηφιακές υπογραφές. Με την υπογραφή ενός PDF με κωδικό HIBC δημιουργείτε ένα επαληθεύσιμο, αδιάβλητο αρχείο που μπορεί να σαρωθεί σε οποιοδήποτε σημείο της εφοδιαστικής αλυσίδας.

## Γιατί να χρησιμοποιήσετε Data Matrix και QR codes μαζί;
Το GroupDocs.Signature υποστηρίζει **50+ μορφές εισόδου και εξόδου** και μπορεί να επεξεργαστεί PDF πολλών εκατοντάδων σελίδων χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη. Η χρήση Data Matrix για πυκνές, μικρής περιοχής ετικέτες και QR για πιο ευρύχωρα έγγραφα προσφέρει την καλύτερη ισορροπία μεταξύ αναγνωσιμότητας, χωρητικότητας δεδομένων (έως 4.296 χαρακτήρες για QR) και αποδοτικότητας χώρου εκτύπωσης.

## Προαπαιτούμενα
- **JDK 11 ή νεότερο** (Java 8 λειτουργεί αλλά συνιστάται Java 11+ για βέλτιστη απόδοση).  
- **IDE** όπως IntelliJ IDEA, Eclipse ή VS Code με επεκτάσεις Java.  
- **Maven ή Gradle** για διαχείριση εξαρτήσεων (παραδείγματα παρακάτω).  
- **Δείγμα PDF** (π.χ., `sample.pdf`) για δοκιμή της υλοποίησης.  
- **Έγκυρη άδεια GroupDocs.Signature** (δωρεάν δοκιμή για ανάπτυξη, επί πληρωμή για παραγωγή).

## Ρύθμιση GroupDocs.Signature για Java

### Διαμόρφωση Maven
Προσθέστε την εξάρτηση στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Διαμόρφωση Gradle
Για έργα Gradle, προσθέστε αυτό στο `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Επιλογή Άμεσης Λήψης
Μπορείτε επίσης να κατεβάσετε το αρχείο JAR απευθείας από [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) και να το προσθέσετε στο classpath του έργου σας χειροκίνητα. Αυτή η προσέγγιση λειτουργεί καλά σε περιβάλλοντα με περιορισμένο δίκτυο.

### Απόκτηση Άδειας
Ζητήστε δωρεάν δοκιμή ή προσωρινή άδεια από το GroupDocs για να αφαιρέσετε τα υδατογραφήματα και να ξεκλειδώσετε όλες τις λειτουργίες. Οι παραγωγικές εγκαταστάσεις απαιτούν αγορασμένη άδεια.

### Βασική Αρχικοποίηση
Η κλάση `Signature` είναι το σημείο εισόδου για όλες τις λειτουργίες υπογραφής. Φορτώνει το PDF, εφαρμόζει τον κωδικό και γράφει το υπογεγραμμένο αρχείο.

```java
import com.groupdocs.signature.Signature;

class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("sample.pdf");
        // Proceed with signing operations...
    }
}
```

## Πώς να δημιουργήσετε Data Matrix PDF με κωδικό HIBC;
Φορτώστε το πηγαίο PDF, διαμορφώστε ένα αντικείμενο `QrCodeSignOptions` για τη μορφή Data Matrix και καλέστε `sign()` – αυτό είναι ό,τι χρειάζεστε για την ενσωμάτωση ενός συμβατού κωδικού HIBC Data Matrix. Τα παρακάτω βήματα σας καθοδηγούν μέσα από τον ακριβή κώδικα που απαιτείται. Το `QrCodeSignOptions` ορίζει τις ρυθμίσεις για μια υπογραφή κωδικού, όπως τύπο, περιεχόμενο, μέγεθος και θέση.

1. **Εισαγωγή των απαιτούμενων κλάσεων** – αυτές σας δίνουν πρόσβαση στη μηχανή υπογραφής και στις επιλογές Data Matrix.  

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
```

2. **Δημιουργία του αντικειμένου `Signature`** με απόλυτες διαδρομές για τα αρχεία προέλευσης και προορισμού.  

```java
String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY";
String destinFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithHIBCLICQR.pdf";

final Signature signature = new Signature(sourceFilePath);
```

3. **Διαμόρφωση των επιλογών Data Matrix** – ορίστε τη συμβολοσειρά HIBC, επιλέξτε `QrCodeTypes.HIBCLICDataMatrix` και καθορίστε τις συντεταγμένες τοποθέτησης. Το `QrCodeTypes` απαριθμεί τις υποστηριζόμενες μορφές κωδικού για υπογραφές HIBC.  

```java
QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR);
hibcLic_QR.setLeft(1); // Set the position from left
hibcLic_QR.setTop(1);   // Set the position from top
hibcLic_QR.setReturnContent(true); // Return content after signing
hibcLic_QR.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

4. **Εφαρμογή της υπογραφής** στο PDF.  

```java
signature.sign(destinFilePath, hibcLic_QR);
```

5. **Απελευθέρωση πόρων** για να κλείσετε τα αρχεία και να αποφύγετε διαρροές μνήμης.  

```java
finally {
    if (signature != null) signature.dispose();
}
```

### Πλήρες λειτουργικό παράδειγμα
Ακολουθεί η πλήρης ροή σε ένα ενιαίο μπλοκ (οι θέσεις κράτησης αντιπροσωπεύουν τον ακριβή κώδικα που θα επικολλήσετε από τα προηγούμενα αποσπάσματα):

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

#### Άμεση απάντηση (40–70 λέξεις)
Για **δημιουργία Data Matrix PDF**, δημιουργήστε ένα `Signature` με το πηγαίο PDF, ορίστε `QrCodeSignOptions` σε `QrCodeTypes.HIBCLICDataMatrix` και παρέχετε μια σωστά μορφοποιημένη συμβολοσειρά HIBC, στη συνέχεια καλέστε `signature.sign(outputPath, options)`. Η βιβλιοθήκη γράφει το υπογεγραμμένο PDF στον προορισμό, διατηρώντας τη διάταξη και ενσωματώνοντας τον κωδικό ως αδιάβλητη υπογραφή.

## Πώς να προσθέσετε QR code PDF χρησιμοποιώντας το GroupDocs.Signature;
Φορτώστε το PDF, διαμορφώστε `QrCodeSignOptions` για τη μορφή QR και καλέστε `sign()`. Αυτό το μοτίβο δύο γραμμών λειτουργεί για οποιοδήποτε μέγεθος PDF και κλιμακώνει αυτόματα την εικόνα QR για βέλτιστη αναγνωσιμότητα. Το `QrCodeSignOptions` διαμορφώνει την υπογραφή κωδικού QR, συμπεριλαμβανομένου του περιεχομένου και των οπτικών ιδιοτήτων του. Τοποθετεί τον κωδικό βάσει των συντεταγμένων που ορίζετε, εξασφαλίζοντας ότι δεν επικαλύπτεται με υπάρχον περιεχόμενο και παραμένει σαρώσιμο μετά την εκτύπωση.

1. **Εισαγωγή κλάσεων ειδικών για QR**  

```java
QrCodeSignOptions hibcLic_AZ = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec);
hibcLic_AZ.setLeft(1); // Set the position from left
hibcLic_AZ.setTop(200); // Set the position from top
hibcLic_AZ.setReturnContent(true); // Return content after signing
hibcLic_AZ.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

2. **Δημιουργία και διαμόρφωση επιλογών QR** – σημειώστε τη χρήση του `QrCodeTypes.HIBCLICQR`.  

```java
signature.sign(destinFilePath, hibcLic_AZ);
```

3. **Υπογραφή του εγγράφου**  

```java
QrCodeSignOptions hibcLic_DM = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix);
hibcLic_DM.setLeft(1); // Set the position from left
hibcLic_DM.setTop(400); // Set the position from top
hibcLic_DM.setReturnContent(true); // Return content after signing
hibcLic_DM.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

> **Άμεση απάντηση:** Χρησιμοποιήστε `QrCodeTypes.HIBCLICQR` στο `QrCodeSignOptions`, ορίστε τη συμβολοσειρά περιεχομένου HIBC, τοποθετήστε τον κωδικό με `setLeft()` και `setTop()`, στη συνέχεια καλέστε `signature.sign(outputPath, options)`. Ο κωδικός QR ενσωματώνεται άμεσα, έτοιμος για λήψη από smartphone ή σαρωτή.

## Συνηθισμένα Λάθη που Πρέπει να Αποφύγετε

### 1. Παράλειψη Απελευθέρωσης Πόρων
**Λάθος:**  
```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  

**Διόρθωση:** Τυλίξτε τη χρήση του `Signature` σε μπλοκ try‑with‑resources ή καλέστε ρητά `close()` σε τελικό τμήμα.

### 2. Χρήση Λανθασμένων Συμβολοσειρών HIBC
**Λάθος:** Χρήση γενικών συμβολοσειρών όπως “12345”.  
**Διόρθωση:** Ακολουθήστε το πρότυπο HIBCC (π.χ., `A123PROD30917/75#422011907#GP293`). Επαληθεύστε με τον [HIBCC online validator](https://www.hibcc.org/).

### 3. Σκληρή Κωδικοποίηση Διαδρομών Αρχείων
**Λάθος:**  
```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  

**Διόρθωση:** Αποθηκεύστε τις διαδρομές σε αρχείο ρυθμίσεων ή μεταβλητή περιβάλλοντος και διαβάστε τις κατά την εκτέλεση.

### 4. Παράβλεψη Συγκρούσεων Θέσης Κωδικού
Τοποθετήστε τους κωδικούς μακριά από υπάρχον κείμενο ή υπογραφές. Χρησιμοποιήστε συντεταγμένες PDF (η αρχή είναι κάτω‑αριστερά) και δοκιμάστε με τυπωμένο δείγμα.

### 5. Μη Δοκιμή με Πραγματικούς Σαρωτές
Τυπώστε το υπογεγραμμένο PDF και σαρώστε το με το ακριβές υλικό που χρησιμοποιείται στη ροή εργασίας σας. Επαληθεύστε την αναγνωσιμότητα σε διαφορετικές ποιότητες εκτύπωσης.

## Πρακτικές Εφαρμογές στην Υγεία

| Σενάριο | Προτεινόμενος Κωδικός | Γιατί ταιριάζει |
|----------|--------------------|--------------|
| **Διανομή φαρμακευτικών προϊόντων** | QR Code | Υψηλή χωρητικότητα δεδομένων, ευρέως σαρωμένο από smartphones. |
| **Διαχείριση αποθεμάτων** | Data Matrix | Μικρό αποτύπωμα, ιδανικό για πυκνές ετικέτες ραφιών. |
| **Κανονιστική συμμόρφωση (FDA 21 CFR Part 11)** | QR + Data Matrix | Διπλή μορφή παρέχει εφεδρεία και δυνατότητα ελέγχου. |
| **Παρακολούθηση ιατρικών συσκευών** | Aztec Code | Συμπαγές μέγεθος λειτουργεί σε περιορισμένο χώρο συσκευασίας. |

## Σκέψεις Απόδοσης και Καλές Πρακτικές

### Μοτίβο Μαζικής Επεξεργασίας
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

- Δημιουργήστε νέο αντικείμενο `Signature` ανά αρχείο για να κρατήσετε τη χρήση μνήμης χαμηλή.  
- Χρησιμοποιήστε σταθερό thread pool (`Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() - 1)`) για παράλληλη επεξεργασία, αλλά παρακολουθείτε το μέγεθος heap επειδή κάθε `Signature` κρατά ολόκληρο το PDF στη μνήμη.  

### Διατήρηση Ενημερωμένων Βιβλιοθηκών
Οι εκδόσεις του GroupDocs βελτιώνουν την ταχύτητα επεξεργασίας έως **20 %** και προσθέτουν νέες λειτουργίες συμμόρφωσης HIBC. Προγραμματίστε τριμηνιαίους ελέγχους εξαρτήσεων.

### Caching Προτύπων
Φορτώστε ένα πρότυπο PDF μία φορά, κλωνοποιήστε το για κάθε παραλλαγή κωδικού και υπογράψτε τα κλώνα. Αυτό μειώνει το I/O και επιταχύνει τις εργασίες υψηλού όγκου.

## Συχνές Ερωτήσεις

**Ε: Μπορεί το GroupDocs.Signature να υπογράψει τύπους αρχείων εκτός του PDF;**  
Α: Ναι, υποστηρίζει επίσης DOCX, XLSX, PPTX, PNG, JPEG και TIFF με το ίδιο API υπογραφής κωδικού.

**Ε: Πώς αντιμετωπίζω σφάλματα “Invalid barcode content”;**  
Α: Επαληθεύστε ότι η συμβολοσειρά HIBC ακολουθεί ακριβώς τη σύνταξη HIBCC, χρησιμοποιήστε τον online validator και βεβαιωθείτε ότι χρησιμοποιείτε τη σωστή σταθερά `QrCodeTypes` για τη μορφή που επιλέξατε.

**Ε: Ποια είναι η μέγιστη χωρητικότητα δεδομένων για κάθε μορφή HIBC;**  
Α: QR ≈ 4.296 αλφαριθμητικούς χαρακτήρες, Aztec ≈ 3.832 αριθμητικούς / 3.067 αλφαριθμητικούς, Data Matrix ≈ 3.116 αριθμητικούς / 2.335 αλφαριθμητικούς. Κρατήστε τους κωδικούς κάτω από 200 χαρακτήρες για βέλτιστη αξιοπιστία σάρωσης.

**Ε: Είναι δυνατόν να ενσωματώσω πολλαπλούς τύπους κωδικού σε ένα PDF;**  
Α: Απόλυτα. Δημιουργήστε ξεχωριστά αντικείμενα `QrCodeSignOptions` με διαφορετικές θέσεις και καλέστε `signature.sign()` για το καθένα. Απλώς βεβαιωθείτε ότι δεν επικαλύπτονται.

**Ε: Χρειάζεται σύνδεση στο διαδίκτυο για υπογραφή κατά την εκτέλεση;**  
Α: Όχι. Μόλις το JAR είναι στο classpath και η άδεια ενεργοποιηθεί, όλες οι λειτουργίες εκτελούνται τοπικά.

## Πρόσθετοι Πόροι

- [GroupDocs.Signature for Java Documentation](https://docs.groupdocs.com/signature/java/)  
- [API Reference Guide](https://reference.groupdocs.com/signature/java/)  
- [Latest Release Downloads](https://releases.groupdocs.com/signature/java/)  
- [Purchase License](https://purchase.groupdocs.com/buy)  
- [Get Free Trial](https://releases.groupdocs.com/signature/java/)  
- [Request Temporary License](https://purchase.groupdocs.com/temporary-license/)  
- [GroupDocs Forum](https://forum.groupdocs.com/c/signature/)

---

**Τελευταία ενημέρωση:** 2026-05-16  
**Δοκιμασμένο με:** GroupDocs.Signature 23.12 for Java  
**Συγγραφέας:** GroupDocs  

---

```java
signature.sign(destinFilePath, hibcLic_DM);
```

## Σχετικά Μαθήματα

- [Create Barcode Signature PDF in Java – GroupDocs Guide](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)
- [Create Barcode Signature in Java – Update PDF Barcodes](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [How to read QR code PDF using Java and GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)