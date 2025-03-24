---
title: Διαγραφή υπογραφής με ταυτότητα
linktitle: Διαγραφή υπογραφής με ταυτότητα
second_title: GroupDocs.Signature .NET API
description: Μάθετε πώς μπορείτε να διαγράψετε μια υπογραφή κατά αναγνωριστικό σε έγγραφα .NET χρησιμοποιώντας τη βιβλιοθήκη GroupDocs.Signature. Εύκολος οδηγός βήμα προς βήμα.
weight: 11
url: /el/net/delete-operations/delete-signature-by-id/
---
## Εισαγωγή
Σε αυτό το σεμινάριο, θα διερευνήσουμε πώς να διαγράψετε μια υπογραφή με βάση το αναγνωριστικό της χρησιμοποιώντας το GroupDocs.Signature για .NET. Το GroupDocs.Signature για .NET είναι μια ισχυρή βιβλιοθήκη που επιτρέπει στους προγραμματιστές να προσθέτουν, να αφαιρούν ή να επαληθεύουν ψηφιακές υπογραφές σε διάφορες μορφές εγγράφων χρησιμοποιώντας εφαρμογές .NET.
## Προαπαιτούμενα
Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τις ακόλουθες προϋποθέσεις:
1.  GroupDocs.Signature for .NET Library: Κάντε λήψη και εγκατάσταση της βιβλιοθήκης από[εδώ](https://releases.groupdocs.com/signature/net/).
2. .NET Framework: Βεβαιωθείτε ότι έχετε εγκαταστήσει το .NET Framework στο σύστημά σας.
3. Έγγραφο με υπογραφή: Προετοιμάστε ένα έγγραφο (π.χ. DOCX, PDF) με υπογραφή που θέλετε να διαγράψετε.

## Εισαγωγή χώρων ονομάτων
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Βήμα 1: Καθορισμός Διαδρομών Αρχείων
Αρχικά, καθορίστε τη διαδρομή αρχείου για το έγγραφο που περιέχει την υπογραφή και τη διαδρομή αρχείου εξόδου όπου θα αποθηκευτεί το τροποποιημένο έγγραφο.
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteById", fileName);
```
## Βήμα 2: Αντιγράψτε το Έγγραφο
 Δεδομένου ότι το`Delete` μέθοδος τροποποιεί το έγγραφο στη θέση του, είναι καλύτερο να δημιουργήσετε ένα αντίγραφο του αρχικού εγγράφου.
```csharp
File.Copy(filePath, outputFilePath, true);
```
## Βήμα 3: Διαγραφή υπογραφής με αναγνωριστικό
 Αρχικοποιήστε το`Signature` αντικείμενο με τη διαδρομή αρχείου εγγράφου και χρησιμοποιήστε το`Delete` μέθοδο αφαίρεσης της υπογραφής με το αναγνωριστικό του.
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    string id = @"eff64a14-dad9-47b0-88e5-2ee4e3604e71";
    bool result = signature.Delete(id);
    if (result)
    {
        Console.WriteLine($"Signature with Id# '{id}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with id# '{id}' was not found!");
    }
}
```

## συμπέρασμα
Σε αυτό το σεμινάριο, μάθαμε πώς να διαγράψουμε μια υπογραφή με βάση το αναγνωριστικό της χρησιμοποιώντας το GroupDocs.Signature για .NET. Αυτή η βιβλιοθήκη παρέχει έναν βολικό τρόπο διαχείρισης ψηφιακών υπογραφών σε διάφορες μορφές εγγράφων μέσω προγραμματισμού.
## Συχνές ερωτήσεις
### Μπορώ να διαγράψω πολλές υπογραφές ταυτόχρονα;
 Ναι, μπορείτε να διαγράψετε πολλές υπογραφές επαναλαμβάνοντας τα αναγνωριστικά τους και καλώντας το`Delete` μέθοδος για κάθε ID.
### Είναι το GroupDocs.Signature για .NET συμβατό με όλες τις μορφές εγγράφων;
Το GroupDocs.Signature για .NET υποστηρίζει ένα ευρύ φάσμα μορφών εγγράφων, συμπεριλαμβανομένων των PDF, DOCX, XLSX και άλλων.
### Μπορώ να προσαρμόσω την εμφάνιση της υπογραφής;
Ναι, μπορείτε να προσαρμόσετε την εμφάνιση της υπογραφής, συμπεριλαμβανομένης της θέσης, του μεγέθους, της γραμματοσειράς και του χρώματός της.
### Υπάρχει διαθέσιμη δοκιμαστική έκδοση;
 Ναι, μπορείτε να κάνετε λήψη μιας δωρεάν δοκιμαστικής έκδοσης από[εδώ](https://releases.groupdocs.com/).
### Πού μπορώ να βρω βοήθεια ή υποστήριξη για το GroupDocs.Signature για .NET;
 Μπορείτε να επισκεφτείτε το φόρουμ υποστήριξης[εδώ](https://forum.groupdocs.com/c/signature/13) για βοήθεια.