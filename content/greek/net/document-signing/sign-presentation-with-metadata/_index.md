---
title: Υπογραφή Παρουσίαση με Μεταδεδομένα
linktitle: Υπογραφή Παρουσίαση με Μεταδεδομένα
second_title: GroupDocs.Signature .NET API
description: Μάθετε πώς να υπογράφετε αρχεία παρουσίασης με μεταδεδομένα χρησιμοποιώντας το GroupDocs.Signature για .NET. Βελτιώστε την ακεραιότητα του εγγράφου και προσθέστε πολύτιμες πληροφορίες.
weight: 12
url: /el/net/document-signing/sign-presentation-with-metadata/
---

# Υπογραφή Παρουσίαση με Μεταδεδομένα

## Εισαγωγή
Σε αυτό το σεμινάριο, θα μάθουμε πώς να υπογράψουμε ένα αρχείο παρουσίασης (PPTX) με μεταδεδομένα χρησιμοποιώντας τη βιβλιοθήκη GroupDocs.Signature για .NET. Η υπογραφή παρουσιάσεων με μεταδεδομένα προσθέτει πολύτιμες πληροφορίες στο έγγραφο, όπως το όνομα του συγγραφέα, την ημερομηνία δημιουργίας, το αναγνωριστικό εγγράφου, το αναγνωριστικό υπογραφής και διάφορες αριθμητικές τιμές.
## Προαπαιτούμενα
Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα εξής:
1.  GroupDocs.Signature for .NET Library: Κάντε λήψη και εγκατάσταση της βιβλιοθήκης από[εδώ](https://releases.groupdocs.com/signature/net/).
2. Περιβάλλον ανάπτυξης: Βεβαιωθείτε ότι έχετε ρυθμίσει ένα περιβάλλον ανάπτυξης .NET.
3. Αρχείο παρουσίασης: Έχετε ένα δείγμα αρχείου παρουσίασης (μορφή PPTX) έτοιμο για υπογραφή.
4. Βασική κατανόηση της C#: Η εξοικείωση με τη γλώσσα προγραμματισμού C# θα είναι επωφελής.

## Εισαγωγή χώρων ονομάτων
Πριν βουτήξουμε στον κώδικα, ας εισαγάγουμε τους απαραίτητους χώρους ονομάτων:
```csharp
using System;
using System.IO;
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;
    using GroupDocs.Signature.Options;
```
## Βήμα 1: Φόρτωση αρχείου παρουσίασης
```csharp
string filePath = "sample.pptx";
```
 Αντικαθιστώ`"sample.pptx"` με τη διαδρομή προς το αρχείο παρουσίασής σας.
## Βήμα 2: Καθορίστε τη διαδρομή αρχείου εξόδου
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPresentationWithMetadata", "SignedWithMetadata.pptx");
```
Καθορίστε τον κατάλογο στον οποίο θέλετε να αποθηκεύσετε το υπογεγραμμένο αρχείο παρουσίασης μαζί με το όνομα του αρχείου.
## Βήμα 3: Αρχικοποίηση αντικειμένου υπογραφής
```csharp
using (Signature signature = new Signature(filePath))
```
Αρχικοποιήστε ένα αντικείμενο Signature παρέχοντας τη διαδρομή προς το αρχείο παρουσίασης.
## Βήμα 4: Καθορίστε τις επιλογές υπογραφής μεταδεδομένων
```csharp
MetadataSignOptions options = new MetadataSignOptions();
```
Δημιουργήστε μια παρουσία του MetadataSignOptions για να ορίσετε επιλογές υπογραφής μεταδεδομένων.
## Βήμα 5: Δημιουργήστε υπογραφές μεταδεδομένων
```csharp
PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Author", "Mr.Scherlock Holmes"),
    new PresentationMetadataSignature("CreatedOn", DateTime.Now),
    new PresentationMetadataSignature("DocumentId", 123456),
    new PresentationMetadataSignature("SignatureId", 123.456D),
    new PresentationMetadataSignature("Amount", 123.456M),
    new PresentationMetadataSignature("Total", 123.456F)
};
```
Δημιουργήστε έναν πίνακα αντικειμένων PresentationMetadataSignature, καθένα από τα οποία αντιπροσωπεύει μια υπογραφή μεταδεδομένων. Μπορείτε να προσθέσετε διάφορους τύπους μεταδεδομένων, συμπεριλαμβανομένων συμβολοσειράς, ημερομηνίας ώρας, ακέραιου, διπλού, δεκαδικού και float.
## Βήμα 6: Προσθήκη υπογραφών στις Επιλογές
```csharp
options.Signatures.AddRange(signatures);
```
Προσθέστε τις δημιουργημένες υπογραφές μεταδεδομένων στο αντικείμενο MetadataSignOptions.
## Βήμα 7: Υπογραφή εγγράφου
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
Υπογράψτε το αρχείο παρουσίασης με μεταδεδομένα χρησιμοποιώντας τις καθορισμένες επιλογές και αποθηκεύστε το υπογεγραμμένο αρχείο στη διαδρομή εξόδου.
## Βήμα 8: Εμφάνιση αποτελεσμάτων
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
Εμφανίστε ένα μήνυμα επιτυχίας μαζί με τον αριθμό των υπογραφών που εφαρμόστηκαν και τη διαδρομή όπου αποθηκεύεται το υπογεγραμμένο αρχείο.

## συμπέρασμα
Σε αυτό το σεμινάριο, μάθαμε πώς να υπογράψουμε ένα αρχείο παρουσίασης με μεταδεδομένα χρησιμοποιώντας τη βιβλιοθήκη GroupDocs.Signature για .NET. Η προσθήκη υπογραφών μεταδεδομένων ενισχύει την ακεραιότητα του εγγράφου και παρέχει πολύτιμες πληροφορίες για το περιεχόμενό του.

## Συχνές ερωτήσεις
### Μπορώ να υπογράψω άλλες μορφές εγγράφων εκτός από το PPTX με μεταδεδομένα χρησιμοποιώντας το GroupDocs.Signature για .NET;
Ναι, το GroupDocs.Signature υποστηρίζει διάφορες μορφές εγγράφων, συμπεριλαμβανομένων των Word, Excel, PDF και άλλων, για υπογραφή με μεταδεδομένα.
### Είναι το GroupDocs.Signature για .NET συμβατό με .NET Core;
Ναι, η βιβλιοθήκη είναι συμβατή τόσο με .NET Framework όσο και με .NET Core.
### Μπορώ να προσαρμόσω την εμφάνιση των υπογραφών μεταδεδομένων;
Ναι, μπορείτε να προσαρμόσετε την εμφάνιση, τη θέση και άλλες ιδιότητες των υπογραφών μεταδεδομένων σύμφωνα με τις απαιτήσεις σας.
### Το GroupDocs.Signature για .NET παρέχει κρυπτογράφηση για υπογεγραμμένα έγγραφα;
Ναι, το GroupDocs.Signature προσφέρει επιλογές κρυπτογράφησης για την προστασία των υπογεγραμμένων εγγράφων από μη εξουσιοδοτημένη πρόσβαση.
### Υπάρχει διαθέσιμη δοκιμαστική έκδοση για δοκιμή πριν την αγορά;
 Ναι, μπορείτε να επωφεληθείτε από μια δωρεάν δοκιμή του GroupDocs.Signature για .NET από[εδώ](https://releases.groupdocs.com/).