---
"date": "2025-05-08"
"description": "Μάθετε πώς να υπογράφετε με ασφάλεια εικόνες DICOM χρησιμοποιώντας το GroupDocs.Signature για Java. Βελτιώστε την ασφάλεια των εγγράφων ενσωματώνοντας κωδικούς QR και μεταδεδομένα."
"title": "Υπογραφή εικόνων DICOM με κωδικούς QR και μεταδεδομένα χρησιμοποιώντας το GroupDocs.Signature για Java"
"url": "/el/java/image-signatures/sign-dicom-images-groupdocs-signature-java/"
"weight": 1
type: docs
---
# Πώς να υπογράψετε εικόνες DICOM με κωδικούς QR και μεταδεδομένα χρησιμοποιώντας το GroupDocs.Signature για Java

## Εισαγωγή

Στο ταχέως εξελισσόμενο τοπίο της ψηφιακής υγειονομικής περίθαλψης, η ασφαλής διαχείριση των δεδομένων των ασθενών είναι ύψιστης σημασίας. Αυτό το σεμινάριο σας καθοδηγεί στην εφαρμογή μιας ισχυρής λύσης χρησιμοποιώντας το GroupDocs.Signature για Java για την υπογραφή εικόνων Ψηφιακής Απεικόνισης και Επικοινωνιών στην Ιατρική (DICOM) με κωδικούς QR και μεταδεδομένα. Αυτές οι λειτουργίες διασφαλίζουν την αυθεντικότητα, ενισχύουν την ιχνηλασιμότητα και διατηρούν τη συμμόρφωση ενσωματώνοντας ζωτικές πληροφορίες απευθείας σε ιατρικές εικόνες.

### Τι θα μάθετε:
- Πώς να ενσωματώσετε το GroupDocs.Signature για Java στο έργο σας.
- Η διαδικασία υπογραφής εικόνων DICOM με κωδικούς QR.
- Προσθήκη μεταδεδομένων XMP για βελτίωση της ασφάλειας των εγγράφων.
- Ανάκτηση, επαλήθευση και αναζήτηση υπογραφών μέσα σε αρχεία DICOM.
- Δημιουργία προεπισκοπήσεων υπογεγραμμένων εικόνων DICOM.

Ας ξεκινήσουμε! Πριν ξεκινήσουμε, ας βεβαιωθούμε ότι έχετε όλα όσα χρειάζεστε για να παρακολουθήσετε απρόσκοπτα.

## Προαπαιτούμενα

Για να εφαρμόσετε αποτελεσματικά τις λειτουργίες του GroupDocs.Signature, βεβαιωθείτε ότι πληροίτε τις ακόλουθες προϋποθέσεις:

### Απαιτούμενες βιβλιοθήκες και εξαρτήσεις
- **GroupDocs.Signature για Java**Θα χρειαστείτε την έκδοση 23.12 ή νεότερη αυτής της βιβλιοθήκης.

### Απαιτήσεις Ρύθμισης Περιβάλλοντος
- **Κιτ ανάπτυξης Java (JDK)**Βεβαιωθείτε ότι το JDK είναι εγκατεστημένο στο σύστημά σας.
- **IDE**Χρησιμοποιήστε ένα Ολοκληρωμένο Περιβάλλον Ανάπτυξης όπως το IntelliJ IDEA ή το Eclipse.

### Προαπαιτούμενα Γνώσεων
Μια βασική κατανόηση:
- Προγραμματισμός Java και αντικειμενοστρεφείς αρχές.
- Εργαλεία δημιουργίας Maven ή Gradle για διαχείριση εξαρτήσεων.

## Ρύθμιση του GroupDocs.Signature για Java

Για να ξεκινήσετε με το GroupDocs.Signature, πρέπει να το προσθέσετε ως εξάρτηση στο έργο σας. Δείτε πώς μπορείτε να το κάνετε αυτό χρησιμοποιώντας διαφορετικά εργαλεία δημιουργίας:

### Maven
Προσθέστε το ακόλουθο απόσπασμα στο δικό σας `pom.xml` αρχείο:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Γκράντλ
Συμπεριλάβετε αυτό στο δικό σας `build.gradle` αρχείο:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Άμεση Λήψη
Εναλλακτικά, μπορείτε να κατεβάσετε την τελευταία έκδοση από το [GroupDocs.Signature για εκδόσεις Java](https://releases.groupdocs.com/signature/java/).

#### Βήματα απόκτησης άδειας χρήσης
1. **Δωρεάν δοκιμή**Δοκιμάστε τις λειτουργίες με μια δωρεάν δοκιμαστική περίοδο περιορισμένου χρόνου.
2. **Προσωρινή Άδεια**Αποκτήστε μια προσωρινή άδεια χρήσης για να εξερευνήσετε όλες τις δυνατότητες.
3. **Αγορά**Αγοράστε μια συνδρομή εάν χρειάζεστε μακροπρόθεσμη πρόσβαση.

#### Βασική Αρχικοποίηση και Ρύθμιση

Για να αρχικοποιήσετε το GroupDocs.Signature, δημιουργήστε μια παρουσία του `Signature` τάξη:
```java
import com.groupdocs.signature.Signature;

// Αρχικοποίηση αντικειμένου υπογραφής με τη διαδρομή προς το αρχείο DICOM
Signature signature = new Signature(filePath);
```

## Οδηγός Εφαρμογής

### Υπογραφή εικόνας DICOM με κωδικό QR και μεταδεδομένα

#### Επισκόπηση
Αυτή η λειτουργία σάς επιτρέπει να υπογράφετε εικόνες DICOM με κωδικό QR και να προσθέτετε μεταδεδομένα XMP, ενισχύοντας την ασφάλεια των εγγράφων.

#### Βήμα 1: Ρύθμιση επιλογών υπογραφής κωδικού QR
```java
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.QrCodeSignOptions;

Padding padding = new Padding();
padding.setRight(5);
padding.setLeft(5);

QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues");
options.setAllPages(true);
options.setWidth(100);
options.setHeight(100);
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
options.setMargin(padding);
```
Εδώ, διαμορφώνουμε την εμφάνιση και τη θέση του κωδικού QR στην εικόνα DICOM.

#### Βήμα 2: Προσθήκη μεταδεδομένων XMP
```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomSaveOptions;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpEntry;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpType;

DicomSaveOptions dicomSaveOptions = new DicomSaveOptions();
List<DicomXmpEntry> xmpEntries = new ArrayList<>();
xmpEntries.add(new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4"));
dicomSaveOptions.setXmpEntries(xmpEntries);
```
Αυτό το απόσπασμα προσθέτει μεταδεδομένα στο αρχείο DICOM, ενσωματώνοντας πρόσθετες πληροφορίες ασθενούς.

#### Βήμα 3: Υπογράψτε το έγγραφο
```java
String outputFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/" + fileName;
signature.sign(outputFilePath, options, dicomSaveOptions);
```
Ο `sign` Η μέθοδος γράφει τον κώδικα QR και τα μεταδεδομένα στο αρχείο DICOM, αποθηκεύοντάς το στην καθορισμένη τοποθεσία.

### Ανάκτηση πληροφοριών υπογεγραμμένης εικόνας DICOM

#### Επισκόπηση
Εξαγωγή μεταδεδομένων XMP από μια υπογεγραμμένη εικόνα DICOM για σκοπούς επαλήθευσης ή ελέγχου.
```java
import com.groupdocs.signature.domain.IDocumentInfo;
import com.groupdocs.signature.domain.signatures.MetadataSignature;

IDocumentInfo documentInfo = signature.getDocumentInfo();
for (MetadataSignature item : documentInfo.getMetadataSignatures()) {
    System.out.println(item.toString());
}
```
Αυτός ο κώδικας ανακτά και εκτυπώνει όλες τις υπογραφές μεταδεδομένων που σχετίζονται με το αρχείο DICOM.

### Επαλήθευση υπογεγραμμένου DICOM

#### Επισκόπηση
Επαληθεύστε ότι υπάρχει υπογραφή κωδικού QR στην υπογεγραμμένη εικόνα DICOM για να επιβεβαιώσετε την αυθεντικότητά της.
```java
import com.groupdocs.signature.domain.VerificationResult;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;
import com.groupdocs.signature.domain.enums.TextMatchType;

QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();
verifyOptions.setAllPages(true);
verifyOptions.setText("Patient #36363393");
verifyOptions.setMatchType(TextMatchType.Contains);

VerificationResult result = signature.verify(verifyOptions);
if (result.isValid()) {
    System.out.println(filePath + " has successfully verified signatures!");
} else {
    System.out.println(filePath + " failed verification process.");
}
```
Αυτό το βήμα επαλήθευσης διασφαλίζει ότι ο κωδικός QR πληροί τα αναμενόμενα κριτήρια, επιβεβαιώνοντας την ακεραιότητα του εγγράφου.

### Αναζήτηση υπογραφών σε υπογεγραμμένο DICOM

#### Επισκόπηση
Εντοπίστε όλες τις υπογραφές κωδικών QR μέσα σε μια υπογεγραμμένη εικόνα DICOM για να τις ελέγξετε ή να τις ελέγξετε.
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.util.List;

List<QrCodeSignature> signatures = signature.search(QrCodeSignature.class);
for (QrCodeSignature qrCodeSignature : signatures) {
    System.out.println("QRCode signature found at page " +
        qrCodeSignature.getPageNumber() + ": " +
        qrCodeSignature.getEncodeType().getTypeName() + ": " +
        qrCodeSignature.getText());
}
```
Αυτή η λειτουργία είναι χρήσιμη για τη σάρωση όλων των υπογραφών κωδικού QR μέσα στο έγγραφο, παρέχοντας ολοκληρωμένη ορατότητα.

### Δημιουργία προεπισκόπησης υπογεγραμμένου DICOM

#### Επισκόπηση
Δημιουργήστε προεπισκοπήσεις για κάθε σελίδα μιας υπογεγραμμένης εικόνας DICOM, επιτρέποντας γρήγορη οπτική επιθεώρηση χωρίς να ανοίξετε ολόκληρο το αρχείο.
```java
import com.groupdocs.signature.options.PreviewOptions;
import java.io.File;
import java.io.FileOutputStream;
import java.nio.file.Paths;

PreviewOptions previewOption = new PreviewOptions(pageNumber -> {
    try {
        String pageFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/image-" + pageNumber + ".jpg";
        return new FileOutputStream(Paths.get(pageFilePath).toFile());
    } catch (Exception e) {
        throw new RuntimeException(e.getMessage());
    }
});

signature.generatePreview(previewOption);
```
Αυτό το απόσπασμα δημιουργεί προεπισκοπήσεις εικόνων για κάθε σελίδα, κάτι που μπορεί να είναι χρήσιμο για γρήγορη επαλήθευση ή κοινή χρήση.

## Πρακτικές Εφαρμογές

Το GroupDocs.Signature για Java προσφέρει αρκετές εφαρμογές πραγματικού κόσμου:
- **Ιατρική Απεικόνιση**Υπογράψτε και διαχειριστείτε με ασφάλεια εικόνες DICOM ασθενών με κωδικούς QR και μεταδεδομένα.
- **Διαχείριση Νομικών Εγγράφων**Βελτίωση της αυθεντικότητας και της συμμόρφωσης των εγγράφων σε νομικές διαδικασίες.
- **Χρηματοοικονομικές Υπηρεσίες**Εφαρμογή ασφαλών ηλεκτρονικών υπογραφών σε ευαίσθητα οικονομικά έγγραφα.