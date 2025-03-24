---
title: Υπογραφή PDF με Μεταδεδομένα
linktitle: Υπογραφή PDF με Μεταδεδομένα
second_title: GroupDocs.Signature .NET API
description: Μάθετε πώς να υπογράφετε έγγραφα PDF με μεταδεδομένα χρησιμοποιώντας το GroupDocs.Signature για .NET. Βελτιώστε την ιχνηλασιμότητα και την αυθεντικότητα των εγγράφων εύκολα.
weight: 11
url: /el/net/document-signing/sign-pdf-with-metadata/
---

# Υπογραφή PDF με Μεταδεδομένα

## Εισαγωγή
Σε αυτό το σεμινάριο, θα μάθουμε πώς να υπογράφετε ένα έγγραφο PDF με μεταδεδομένα χρησιμοποιώντας το GroupDocs.Signature για .NET. Η προσθήκη μεταδεδομένων σε ένα PDF μπορεί να παρέχει πρόσθετες πληροφορίες σχετικά με το έγγραφο, όπως συγγραφή, ημερομηνία δημιουργίας, αναγνωριστικό εγγράφου και άλλα.
## Προαπαιτούμενα
Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα εξής:
1.  GroupDocs.Signature για .NET: Μπορείτε να το κατεβάσετε από[εδώ](https://releases.groupdocs.com/signature/net/).
2. Έγγραφο PDF: Έχετε ένα δείγμα αρχείου PDF έτοιμο για υπογραφή.
3. Βασικές γνώσεις προγραμματισμού C#: Απαιτείται εξοικείωση με τη σύνταξη C# για την κατανόηση των παραδειγμάτων κώδικα.
## Εισαγωγή χώρων ονομάτων
Αρχικά, βεβαιωθείτε ότι εισάγετε τους απαραίτητους χώρους ονομάτων για πρόσβαση στις απαιτούμενες κλάσεις και μεθόδους:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Βήμα 1: Φορτώστε το έγγραφο PDF
Φορτώστε το έγγραφο PDF που θέλετε να υπογράψετε:
```csharp
string filePath = "sample.pdf";
```
## Βήμα 2: Καθορίστε τη διαδρομή αρχείου εξόδου
Καθορίστε τη διαδρομή του αρχείου εξόδου όπου θα αποθηκευτεί το υπογεγραμμένο PDF με μεταδεδομένα:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
```
## Βήμα 3: Δημιουργία παρουσίας υπογραφής
Εκκινήστε μια παρουσία υπογραφής παρέχοντας τη διαδρομή προς το έγγραφο PDF:
```csharp
using (Signature signature = new Signature(filePath))
{
    // Ο κωδικός που σχετίζεται με την υπογραφή θα πάει εδώ
}
```
## Βήμα 4: Ορισμός Επιλογών Μεταδεδομένων
Δημιουργήστε MetadataSignOptions και προσθέστε πεδία μεταδεδομένων με τις αντίστοιχες τιμές τους:
```csharp
MetadataSignOptions options = new MetadataSignOptions();
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Τιμή συμβολοσειράς
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Τιμές DateTime
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Ακέραια τιμή
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Διπλή αξία
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Δεκαδική τιμή
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Διακύμανση αξίας
```
## Βήμα 5: Υπογράψτε το Έγγραφο
Υπογράψτε το έγγραφο PDF με τις καθορισμένες επιλογές μεταδεδομένων και αποθηκεύστε το υπογεγραμμένο έγγραφο:
```csharp
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## συμπέρασμα
Σε αυτό το σεμινάριο, έχουμε καλύψει τον τρόπο υπογραφής ενός εγγράφου PDF με μεταδεδομένα χρησιμοποιώντας GroupDocs.Signature για .NET. Ακολουθώντας τον οδηγό βήμα προς βήμα, μπορείτε εύκολα να προσθέσετε πληροφορίες μεταδεδομένων όπως συγγραφή, ημερομηνία δημιουργίας και πολλά άλλα στα αρχεία PDF σας, βελτιώνοντας τη χρησιμότητα και την ιχνηλασιμότητα τους.
## Συχνές ερωτήσεις
### Μπορώ να προσθέσω προσαρμοσμένα πεδία μεταδεδομένων στα έγγραφά μου PDF;
Ναι, μπορείτε να προσθέσετε προσαρμοσμένα πεδία μεταδεδομένων καθορίζοντας το όνομα του πεδίου και την αντίστοιχη τιμή του χρησιμοποιώντας το GroupDocs.Signature για .NET.
### Είναι το GroupDocs.Signature για .NET συμβατό με όλες τις εκδόσεις του .NET Framework;
Το GroupDocs.Signature για .NET είναι συμβατό με διάφορες εκδόσεις του .NET Framework, εξασφαλίζοντας ευελιξία και ευκολία ενσωμάτωσης.
### Το GroupDocs.Signature υποστηρίζει την υπογραφή άλλων μορφών εγγράφων εκτός από το PDF;
Ναι, το GroupDocs.Signature υποστηρίζει ένα ευρύ φάσμα μορφών εγγράφων, συμπεριλαμβανομένων των Word, Excel, PowerPoint και άλλων.
### Μπορώ να υπογράψω πολλά έγγραφα μαζικά χρησιμοποιώντας το GroupDocs.Signature για .NET;
Ναι, μπορείτε να υπογράψετε πολλά έγγραφα μαζικά επαναλαμβάνοντας μια λίστα αρχείων και εφαρμόζοντας τη διαδικασία υπογραφής μέσω προγραμματισμού.
### Είναι διαθέσιμη τεχνική υποστήριξη για τους χρήστες του GroupDocs.Signature;
 Ναι, το GroupDocs παρέχει αποκλειστική τεχνική υποστήριξη μέσω των φόρουμ του. Μπορείτε να αποκτήσετε πρόσβαση στο φόρουμ υποστήριξης[εδώ](https://forum.groupdocs.com/c/signature/13).