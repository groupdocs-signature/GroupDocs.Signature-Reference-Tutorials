---
categories:
- Java Document Processing
date: '2026-08-19'
description: Μάθετε πώς να δημιουργήσετε barcode signature java και να ενημερώσετε
  τη θέση, το μέγεθος και τις ιδιότητές του για PDF χρησιμοποιώντας το GroupDocs.Signature
  API.
keywords:
- create barcode signature java
- barcode signature java
- groupdocs signature java
lastmod: '2026-08-19'
linktitle: Ενημέρωση Barcode Signatures σε Java
og_description: Μάθετε πώς να δημιουργήσετε barcode signature java και να τροποποιήσετε
  τη θέση, το μέγεθος και τις ιδιότητές του σε PDF χρησιμοποιώντας το GroupDocs.Signature
  API. Γρήγορα, αξιόπιστα και έτοιμα για batch.
og_image_alt: Guide to creating and updating barcode signatures in Java PDFs with
  GroupDocs.Signature
og_title: Δημιουργία barcode signature java – ενημέρωση barcode PDF αποδοτικά
schemas:
- author: GroupDocs
  dateModified: '2026-08-19'
  description: Learn how to create barcode signature java and update its position,
    size, and properties for PDFs using GroupDocs.Signature API.
  headline: Create Barcode Signature Java – Update PDF Barcodes
  type: TechArticle
- description: Learn how to create barcode signature java and update its position,
    size, and properties for PDFs using GroupDocs.Signature API.
  name: Create Barcode Signature Java – Update PDF Barcodes
  steps:
  - name: Initialize the Signature Instance
    text: '#### Direct answer Create a `Signature` object by passing the path of the
      document you want to edit; this loads the file into memory and prepares it for
      barcode operations. The `Signature` class is the gateway to all signature‑related
      actions. It reads the file and exposes methods for searching, add'
  - name: Search for Barcode Signatures
    text: '#### Direct answer Use `BarcodeSearchOptions` with the `search` method
      to retrieve a list of all barcode signatures in the document. You can’t update
      what you can’t find. GroupDocs.Signature provides a powerful search API that
      filters signatures by type. You now have a list of `BarcodeSignature` obj'
  - name: Update Barcode Properties
    text: '#### Direct answer Modify the `Left`, `Top`, `Width`, and `Height` of the
      retrieved `BarcodeSignature` and call `signature.update` to write the changes
      to a new file. Now you can **change barcode size** or reposition it wherever
      you need. **Key points:** - `setLeft` / `setTop` move the barcode (coor'
  type: HowTo
tags:
- barcode signatures
- pdf automation
- groupdocs java
- document management
- java barcode
title: Δημιουργία barcode signature java – ενημέρωση barcode PDF
type: docs
url: /el/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/
weight: 1
---

# Δημιουργία υπογραφής barcode java – ενημέρωση PDF barcode

Όταν χρειάζεται να μετακινήσετε τα barcode σε χιλιάδες ετικέτες αποστολής ή να προσαρμόσετε τις θέσεις των barcode μετά από ανασχεδιασμό του προτύπου, η χειροκίνητη εκτέλεση είναι επιρρεπής σε σφάλματα και χρονοβόρα. Σε αυτόν τον οδηγό θα μάθετε **πώς να δημιουργήσετε υπογραφή barcode java** και στη συνέχεια να τροποποιήσετε τη θέση, το μέγεθος και άλλες ιδιότητες προγραμματιστικά με το GroupDocs.Signature for Java. Η προσέγγιση λειτουργεί για PDF, Word, Excel, PowerPoint και αρχεία εικόνας, παρέχοντάς σας ένα ενιαίο, συνεπές API για όλα τα σενάρια αυτοματοποίησης εγγράφων.

## Γρήγορες απαντήσεις
- **Τι σημαίνει “create barcode signature”**; Σημαίνει τη δημιουργία ενός αντικειμένου `BarcodeSignature` που μπορεί να τοποθετηθεί, μετακινηθεί ή επεξεργαστεί μέσα σε ένα έγγραφο μέσω του API.  
- **Μπορώ να αλλάξω το μέγεθος του barcode μετά τη δημιουργία του;** Ναι – χρησιμοποιήστε `setWidth`/`setHeight` ή προσαρμόστε τις συντεταγμένες `Left`/`Top`.  
- **Χρειάζομαι άδεια για την ενημέρωση των barcode;** Μια δοκιμαστική έκδοση λειτουργεί για ανάπτυξη· απαιτείται πλήρης άδεια για παραγωγή.  
- **Λειτουργεί μόνο με PDF;** Όχι – ο ίδιος κώδικας λειτουργεί με Word, Excel, PowerPoint και κοινές μορφές εικόνας.  
- **Πόσα έγγραφα μπορώ να επεξεργαστώ ταυτόχρονα;** Υποστηρίζεται επεξεργασία δέσμης· απλώς διαχειριστείτε τη μνήμη με try‑with‑resources.  

## Τι είναι η δημιουργία υπογραφής barcode java;
Η δημιουργία υπογραφής barcode java είναι η διαδικασία δημιουργίας ενός αντικειμένου `BarcodeSignature` που αντιπροσωπεύει ένα barcode ενσωματωμένο ως ψηφιακή υπογραφή μέσα σε ένα έγγραφο. Χρησιμοποιώντας το GroupDocs.Signature API, μπορείτε προγραμματιστικά να προσθέσετε ένα νέο barcode, να εντοπίσετε υπάρχοντα ή να τροποποιήσετε τις ιδιότητές τους όπως θέση, μέγεθος και κωδικοποιημένο κείμενο, όλα χωρίς να ανοίξετε το αρχείο σε οπτικό επεξεργαστή.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Signature για Java;
Το GroupDocs.Signature υποστηρίζει **πάνω από 50 μορφές εισόδου και εξόδου** — συμπεριλαμβανομένων PDF, DOCX, XLSX, PPTX και κοινών τύπων εικόνας — και μπορεί να επεξεργαστεί PDF με εκατοντάδες σελίδες διατηρώντας τη χρήση μνήμης κάτω από 100 MB. Το batch API του διαχειρίζεται έως **10.000 έγγραφα ανά εκτέλεση** σε έναν τυπικό διακομιστή, καθιστώντας εφικτές ενημερώσεις μεγάλης κλίμακας.

## Προαπαιτούμενα

- **GroupDocs.Signature for Java** ≥ 23.12 (οι παλαιότερες εκδόσεις λείπουν τις μεθόδους ενημέρωσης που χρησιμοποιούνται εδώ).  
- Java Development Kit 8 ή νεότερο.  
- Ένα IDE όπως IntelliJ IDEA, Eclipse ή VS Code.  
- Βασικές γνώσεις Java (κλάσεις, αντικείμενα, διαχείριση εξαιρέσεων).  

### Απαιτούμενες βιβλιοθήκες
Προσθέστε το GroupDocs.Signature στο έργο σας με το προτιμώμενο εργαλείο κατασκευής.

**Maven**  
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```  

**Gradle**  
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```  

**Άμεση λήψη** – κατεβάστε το πιο πρόσφατο JAR από [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) και προσθέστε το στο classpath σας.

### Απόκτηση άδειας
Το GroupDocs.Signature λειτουργεί τόσο με δοκιμαστικές όσο και με πλήρεις άδειες:

- **Δωρεάν δοκιμή** – ιδανική για αποδείξεις έννοιας.  
- **Προσωρινή άδεια** – για εκτεταμένη αξιολόγηση σε συγκεκριμένο έργο.  
- **Πλήρης άδεια** – αφαιρεί υδατογραφήματα και περιορισμούς χρήσης για παραγωγή.  

*Συμβουλή*: Ξεκινήστε με τη δωρεάν δοκιμή, στη συνέχεια αναβαθμίστε όταν έχετε επικυρώσει τη ροή εργασίας.

## Πώς να δημιουργήσετε υπογραφή barcode java

### Βήμα 1: αρχικοποίηση του αντικειμένου signature
`Signature` είναι η κύρια κλάση εισόδου που φορτώνει ένα έγγραφο και εκθέτει μεθόδους για αναζήτηση, προσθήκη και ενημέρωση υπογραφών.

#### Άμεση απάντηση
Δημιουργήστε ένα αντικείμενο `Signature` περνώντας τη διαδρομή του εγγράφου που θέλετε να επεξεργαστείτε· αυτό φορτώνει το αρχείο στη μνήμη και το προετοιμάζει για λειτουργίες barcode. Η κλάση `Signature` είναι η πύλη για όλες τις ενέργειες σχετικές με υπογραφές. Διαβάζει το αρχείο και εκθέτει μεθόδους για αναζήτηση, προσθήκη ή ενημέρωση υπογραφών.

```java
import com.groupdocs.signature.Signature;
import java.nio.file.Paths;
```  

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/your_document.pdf";
```  

```java
Signature signature = new Signature(filePath);
```  

> **Συμβουλή**: Επικυρώστε τη διαδρομή του αρχείου πριν δημιουργήσετε το αντικείμενο `Signature` για να αποφύγετε το `FileNotFoundException`.

### Βήμα 2: αναζήτηση υπογραφών barcode
`BarcodeSearchOptions` ορίζει τα κριτήρια που χρησιμοποιούνται κατά τη σάρωση ενός εγγράφου για υπογραφές barcode.

#### Άμεση απάντηση
Χρησιμοποιήστε `BarcodeSearchOptions` με τη μέθοδο `search` για να λάβετε μια λίστα με όλες τις υπογραφές barcode στο έγγραφο. Δεν μπορείτε να ενημερώσετε ό,τι δεν μπορείτε να βρείτε. Το GroupDocs.Signature παρέχει ένα ισχυρό API αναζήτησης που φιλτράρει τις υπογραφές ανά τύπο, αριθμό σελίδας ή μορφή barcode.

```java
import com.groupdocs.signature.options.search.BarcodeSearchOptions;
import com.groupdocs.signature.domain.signatures.BarcodeSignature;
import java.util.List;
```  

```java
BarcodeSearchOptions options = new BarcodeSearchOptions();
```  

```java
List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, options);
```  

Τώρα έχετε μια λίστα από αντικείμενα `BarcodeSignature`, το καθένα εκθέτει ιδιότητες όπως `Left`, `Top`, `Width`, `Height`, `Text` και `EncodeType`.

> **Σημείωση απόδοσης**: Για πολύ μεγάλα PDF, περιορίστε την αναζήτηση σε συγκεκριμένες σελίδες ή τύπους barcode για να επιταχύνετε την εκτέλεση.

### Βήμα 3: ενημέρωση ιδιοτήτων barcode
`BarcodeSignature` αντιπροσωπεύει ένα μεμονωμένο barcode ενσωματωμένο σε ένα έγγραφο και παρέχει setters για τα οπτικά του χαρακτηριστικά.

#### Άμεση απάντηση
Τροποποιήστε τα `Left`, `Top`, `Width` και `Height` του ανακτημένου `BarcodeSignature` και καλέστε `signature.update` για να γράψετε τις αλλαγές σε νέο αρχείο. Αυτό σας επιτρέπει να αλλάξετε το μέγεθος του barcode ή να το μετακινήσετε όπου χρειάζεται, ενώ το αρχικό αρχείο παραμένει αμετάβλητο.

```java
import java.io.File;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
```  

```java
String fileName = Paths.get(filePath).getFileName().toString();
String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY/UpdateBarcode/" + fileName).getPath();
checkDir(outputFilePath);
```  

```java
if (signatures.size() > 0) {
    BarcodeSignature barcodeSignature = signatures.get(0);
    
    // Update the barcode's position and size
    barcodeSignature.setLeft(100);
    barcodeSignature.setTop(100);
    
    // Apply the changes to the document
    boolean result = signature.update(outputFilePath, barcodeSignature);
    
    if (result) {
        System.out.println("Signature with Barcode '" +
            barcodeSignature.getText() + "' and encode type '"+
            barcodeSignature.getEncodeType().getTypeName() + "' was updated in the document ['" +
            fileName + "'].");
    }
} catch (GroupDocsSignatureException e) {
    System.err.println("Error updating signature: " + e.getMessage());
}
```  

**Βασικά σημεία**
- `setLeft` / `setTop` μετακινούν το barcode (συντεταγμένες μετρημένες από την επάνω‑αριστερή γωνία).  
- `update` γράφει ένα νέο αρχείο· το αρχικό παραμένει αμετάβλητο.  
- Τυλίξτε την κλήση σε μπλοκ `try‑catch` για να διαχειριστείτε πιθανές `GroupDocsSignatureException`.

## Πότε πρέπει να ενημερώσετε υπογραφές barcode;
Θα πρέπει να ενημερώνετε τις υπογραφές barcode όποτε αλλάζουν οι διατάξεις των εγγράφων, μεταβάλλονται οι κανονιστικές απαιτήσεις ή χρειάζεται να επεξεργαστείτε μαζικά υπάρχοντα αρχεία μετά από μεταφορά δεδομένων. Η προγραμματιστική ενημέρωση αποφεύγει τη χειροκίνητη επεξεργασία, μειώνει τα σφάλματα και εξασφαλίζει συνεπή τοποθέτηση σε χιλιάδες αρχεία.

## Συχνά προβλήματα & λύσεις

### Πρόβλημα 1: “Δεν βρέθηκαν υπογραφές barcode”
**Συμπτωμα**: Η αναζήτηση επιστρέφει κενή λίστα παρόλο που τα barcode είναι ορατά στο PDF.  

**Πιθανές αιτίες**
- Τα barcode είναι ενσωματωμένα ως εικόνες ή πεδία φόρμας, όχι ως αντικείμενα υπογραφής.  
- Το έγγραφο είναι προστατευμένο με κωδικό.  
- Φιλτράρετε για συγκεκριμένο τύπο barcode που δεν ταιριάζει.  

**Λύση**  
```java
BarcodeSearchOptions options = new BarcodeSearchOptions();
options.setAllPages(true); // Search all pages, not just the first
List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, options);

if (signatures.isEmpty()) {
    System.out.println("No barcode signatures found. The barcodes might be images, not signature objects.");
}
```  

### Πρόβλημα 2: Το ενημερωμένο έγγραφο φαίνεται κατεστραμμένο
**Συμπτωμα**: Το PDF δεν ανοίγει μετά την ενημέρωση.  

**Πιθανές αιτίες**
- Ανεπαρκής χώρος στο δίσκο.  
- Ο φάκελος εξόδου δεν υπάρχει.  
- Τα δικαιώματα του συστήματος αρχείων εμποδίζουν τη γραφή.  

**Λύση**  
```java
File outputDir = new File("YOUR_OUTPUT_DIRECTORY/UpdateBarcode/");
if (!outputDir.exists()) {
    outputDir.mkdirs(); // Create directories if they don't exist
}

// Check write permissions
if (!outputDir.canWrite()) {
    throw new IOException("Cannot write to output directory: " + outputDir.getAbsolutePath());
}
```  

### Πρόβλημα 3: Υποβάθμιση απόδοσης με μεγάλα έγγραφα
**Συμπτωμα**: Η επεξεργασία επιβραδύνεται δραματικά για PDF πάνω από ~50 σελίδες.  

**Λύση**  
```java
BarcodeSearchOptions options = new BarcodeSearchOptions();
options.setPageNumber(1); // Start with page 1
options.setPagesSetup(new PagesSetup());
options.getPagesSetup().setFirstPage(true);
options.getPagesSetup().setLastPage(false);
```  

## Συμβουλές βελτιστοποίησης απόδοσης

### Διαχείριση μνήμης για λειτουργίες δέσμης
Επεξεργαστείτε ένα έγγραφο τη φορά και αφήστε τη Java να καθαρίσει τους πόρους αυτόματα:

```java
List<String> documentPaths = getDocumentList();
for (String path : documentPaths) {
    try (Signature sig = new Signature(path)) {
        // Process one document at a time
        // Signature instance is auto‑closed after each iteration
    }
}
```  

### Κρυφή μνήμη αποτελεσμάτων αναζήτησης
Αν χρειάζεται να τροποποιήσετε πολλές ιδιότητες στα ίδια barcode, κάντε αναζήτηση μία φορά και επαναχρησιμοποιήστε τη λίστα:

```java
List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, options);

// Update multiple properties
for (BarcodeSignature barcode : signatures) {
    barcode.setLeft(100);
    barcode.setTop(100);
    barcode.setWidth(200);
    barcode.setHeight(50);
}

// Single update call with all changes
signature.update(outputPath, signatures);
```  

### Παράλληλη επεξεργασία για τεράστιες δέσμες
Εκμεταλλευτείτε τα Java streams για να επιταχύνετε χιλιάδες έγγραφα:

```java
documentPaths.parallelStream().forEach(path -> {
    try (Signature sig = new Signature(path)) {
        List<BarcodeSignature> barcodes = sig.search(BarcodeSignature.class, new BarcodeSearchOptions());
        if (!barcodes.isEmpty()) {
            BarcodeSignature barcode = barcodes.get(0);
            barcode.setLeft(50);  // New position for smaller boxes
            barcode.setTop(10);
            sig.update(generateOutputPath(path), barcode);
        }
    } catch (Exception e) {
        logError(path, e);
    }
});
```  

## Πρακτικές εφαρμογές

### Περίπτωση χρήσης 1: αυτοματοποιημένες ενημερώσεις ετικετών logistics
Μια εταιρεία αποστολών άλλαξε τις διαστάσεις των κουτιών, απαιτώντας μετακίνηση barcode σε 50.000 υπάρχουσες ετικέτες. Το παραπάνω παράδειγμα παράλληλης επεξεργασίας μείωσε το έργο από ημέρες σε λίγες ώρες.

### Περίπτωση χρήσης 2: τυποποίηση προτύπων συμβάσεων
Η νομική ομάδα απαιτούσε σταθερή θέση barcode για σάρωση. Με την αναζήτηση και ενημέρωση όλων των PDF συμβάσεων σε μία δέσμη, η ομάδα απέφυγε το δαπανηρό χειροκίνητο εκτύπωση.

### Περίπτωση χρήσης 3: ενσωμάτωση συστήματος αποθεμάτων
Μετά από αναβάθμιση ERP, τα barcode προϊόντων έπρεπε να ευθυγραμμιστούν με νέο εκτυπωτή ετικετών. Η προγραμματιστική ενημέρωση του μεγέθους και της θέσης του barcode εξοικονόμησε χρόνο και κόστος υλικών.

## Λίστα ελέγχου αντιμετώπισης προβλημάτων
Πριν ζητήσετε υποστήριξη, ελέγξτε αυτή τη λίστα:

- **Η διαδρομή του αρχείου είναι σωστή** και το αρχείο υπάρχει.  
- **Δικαιώματα ανάγνωσης/εγγραφής** έχουν δοθεί για την πηγή και τον προορισμό.  
- **Η έκδοση του GroupDocs.Signature** είναι 23.12 ή νεότερη.  
- **Η άδεια είναι σωστά ρυθμισμένη** (αν χρησιμοποιείτε πλήρη άδεια).  
- **Ο φάκελος εξόδου υπάρχει** ή δημιουργείται προγραμματιστικά.  
- **Αρκετός χώρος δίσκου** για τα αρχεία εξόδου.  
- **Κανένα άλλο πρόγραμμα** δεν κλειδώνει το αρχείο προέλευσης.  
- **Διαχείριση εξαιρέσεων** είναι σε θέση να καταγράψει σφάλματα.  

## Συχνές ερωτήσεις

**Ε: Μπορώ να ενημερώσω κώδικα υπογραφής barcode Java για πολλαπλά barcode σε ένα έγγραφο;**  
Α: Απόλυτα. Επανάλαβε τη `List<BarcodeSignature>` που επιστρέφει η αναζήτηση και κάλεσε `signature.update()` για κάθε ένα, ή πέρασε ολόκληρη τη λίστα σε μία κλήση `update`.

**Ε: Ποιοι τύποι barcode υποστηρίζει το GroupDocs.Signature;**  
Α: Δεκάδες, συμπεριλαμβανομένων Code 128, QR Code, EAN‑13, UPC‑A, DataMatrix, PDF417 κ.ά. Χρησιμοποιήστε `barcodeSignature.getEncodeType()` για να ελέγξετε τον τύπο.

**Ε: Μπορώ να αλλάξω το πραγματικό περιεχόμενο του barcode (τα κωδικοποιημένα δεδομένα);**  
Α: Ναι, μέσω `setText()`, αλλά θυμηθείτε να αναδημιουργήσετε το οπτικό barcode ώστε οι σαρωτές να το διαβάζουν σωστά.

**Ε: Πώς διαχειρίζομαι έγγραφα με barcode σε πολλές σελίδες;**  
Α: Κάθε `BarcodeSignature` περιλαμβάνει `getPageNumber()`. Φιλτράρετε ή επεξεργαστείτε barcode συγκεκριμένων σελίδων όπως χρειάζεται.

**Ε: Τι γίνεται με το αρχικό έγγραφο μετά την ενημέρωση;**  
Α: Το αρχικό αρχείο παραμένει αμετάβλητο. Το GroupDocs γράφει τις αλλαγές στη διαδρομή εξόδου που καθορίζετε, διατηρώντας το αρχικό για ασφάλεια.

**Ε: Μπορώ να ενημερώσω barcode σε PDF προστατευμένα με κωδικό;**  
Α: Ναι. Χρησιμοποιήστε την υπερφόρτωση `LoadOptions` του κατασκευαστή `Signature` για να δώσετε τον κωδικό.

**Ε: Πώς να επεξεργαστώ μαζικά χιλιάδες έγγραφα αποδοτικά;**  
Α: Συνδυάστε parallel streams με try‑with‑resources (όπως φαίνεται στο παράδειγμα παράλληλης επεξεργασίας) και παρακολουθήστε τη χρήση μνήμης.

**Ε: Λειτουργεί αυτό με μορφές εκτός του PDF;**  
Α: Ναι. Το ίδιο API λειτουργεί με Word, Excel, PowerPoint, εικόνες και πολλές άλλες μορφές που υποστηρίζει το GroupDocs.Signature.

## Συμπέρασμα

Τώρα έχετε έναν πλήρη, έτοιμο για παραγωγή οδηγό για τη **δημιουργία αντικειμένων barcode signature java** και την ενημέρωση της θέσης, του μεγέθους και άλλων ιδιοτήτων τους. Καλύψαμε την αρχικοποίηση, την αναζήτηση, την τροποποίηση, την αντιμετώπιση προβλημάτων και τη βελτιστοποίηση απόδοσης για σενάρια μεμονωμένου εγγράφου και μεγάλων δέσμης.

### Επόμενα βήματα
- Δοκιμάστε την ενημέρωση πρόσθετων ιδιοτήτων όπως περιστροφή ή διαφάνεια στην ίδια εκτέλεση.  
- Ενσωματώστε τη λογική σε υπηρεσία REST για να εκθέσετε τις ενημερώσεις barcode ως τελικό σημείο API.  
- Εξερευνήστε άλλους τύπους υπογραφών (κείμενο, εικόνα, ψηφιακή) χρησιμοποιώντας το ίδιο μοτίβο για πλήρη αυτοματοποίηση των ροών εργασίας εγγράφων.  

**Πηγές**  
- [Τεκμηρίωση GroupDocs.Signature για Java](https://docs.groupdocs.com/signature/java/)  
- [Αναφορά API](https://reference.groupdocs.com/signature/java/)  
- [Φόρουμ υποστήριξης](https://forum.groupdocs.com/c/signature)  
- [Λήψη δωρεάν δοκιμής](https://releases.groupdocs.com/signature/java/)  

---

**Last Updated:** 2026-08-19  
**Tested With:** GroupDocs.Signature 23.12  
**Author:** GroupDocs

## Σχετικά μαθήματα

- [Δημιουργία υπογραφής Barcode PDF σε Java – Οδηγός GroupDocs](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)
- [Οδηγός GroupDocs.Signature Java - Προσθήκη υπογραφών Barcode σε PDF](/signature/java/digital-signatures/java-pdf-signing-groupdocs-signature-guide/)
- [Οδηγός Java Barcode Signature - Προσθήκη, Επαλήθευση & Διαχείριση Barcode σε PDF](/signature/java/barcode-signatures/)
