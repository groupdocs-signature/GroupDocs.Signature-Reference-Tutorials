---
title: Υπογραφή εικόνας με μεταδεδομένα
linktitle: Υπογραφή εικόνας με μεταδεδομένα
second_title: GroupDocs.Signature .NET API
description: Μάθετε πώς να υπογράφετε εικόνες με μεταδεδομένα στο .NET χρησιμοποιώντας GroupDocs.Signature. Εύκολη, αποτελεσματική και προσαρμόσιμη λύση υπογραφής μεταδεδομένων.
weight: 10
url: /el/net/document-signing/sign-image-with-metadata/
---
## Εισαγωγή
Το GroupDocs.Signature για .NET επιτρέπει στους προγραμματιστές να υπογράφουν εικόνες με μεταδεδομένα αποτελεσματικά. Αυτό το σεμινάριο σας καθοδηγεί στη διαδικασία βήμα προς βήμα.
## Προαπαιτούμενα
Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε τα ακόλουθα:
1. GroupDocs.Signature για .NET: Εγκαταστήστε το πακέτο GroupDocs.Signature στο έργο σας .NET. Μπορείτε να το κατεβάσετε από[εδώ](https://releases.groupdocs.com/signature/net/).   
2. Αρχείο εικόνας: Προετοιμάστε το αρχείο εικόνας που θέλετε να υπογράψετε με μεταδεδομένα.

## Εισαγωγή χώρων ονομάτων
Βεβαιωθείτε ότι έχετε εισαγάγει τους απαραίτητους χώρους ονομάτων στον κώδικα C#:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Βήμα 1: Φόρτωση αρχείου εικόνας
Αρχικά, καθορίστε τη διαδρομή προς το αρχείο εικόνας και τον κατάλογο εξόδου για την υπογεγραμμένη εικόνα με μεταδεδομένα:
```csharp
string filePath = "sample.png";            
string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
```
## Βήμα 2: Δημιουργήστε υπογραφές μεταδεδομένων
Στη συνέχεια, δημιουργήστε διαφορετικές υπογραφές μεταδεδομένων και προσθέστε τις στη συλλογή υπογραφών επιλογών:
```csharp
using (Signature signature = new Signature(filePath))
{
    ushort imgsMetadataId = 41996;
    MetadataSignOptions options = new MetadataSignOptions();
    options
        .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Scherlock Holmes")) // Τιμή συμβολοσειράς
        .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Ημερομηνία Ώρα τιμή
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Ακέραια τιμή
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Διπλή αξία
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Δεκαδική τιμή
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Διακύμανση αξίας
    
    // υπογράψτε έγγραφο σε αρχείο
    SignResult result = signature.Sign(outputFilePath, options);
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## συμπέρασμα
Σε αυτό το σεμινάριο, μάθατε πώς να υπογράφετε μια εικόνα με μεταδεδομένα χρησιμοποιώντας το GroupDocs.Signature για .NET. Ακολουθώντας αυτά τα βήματα, μπορείτε εύκολα να ενσωματώσετε υπογραφές μεταδεδομένων στις εφαρμογές σας .NET.

## Συχνές ερωτήσεις
### Μπορώ να υπογράψω πολλές εικόνες με μεταδεδομένα χρησιμοποιώντας το GroupDocs.Signature για .NET;
Ναι, μπορείτε να υπογράψετε πολλές εικόνες με μεταδεδομένα επαναλαμβάνοντας κάθε αρχείο εικόνας και εφαρμόζοντας τις υπογραφές μεταδεδομένων.
### Υπάρχει διαθέσιμη δοκιμαστική έκδοση για το GroupDocs.Signature για .NET;
 Ναι, μπορείτε να κάνετε λήψη της δοκιμαστικής έκδοσης από[εδώ](https://releases.groupdocs.com/).
### Το GroupDocs.Signature για .NET υποστηρίζει άλλες μορφές αρχείων εκτός από εικόνες;
Ναι, το GroupDocs.Signature υποστηρίζει διάφορες μορφές αρχείων, συμπεριλαμβανομένων των PDF, Word, Excel και άλλων.
### Μπορώ να προσαρμόσω την εμφάνιση της υπογραφής μεταδεδομένων;
Ναι, μπορείτε να προσαρμόσετε την εμφάνιση της υπογραφής μεταδεδομένων, όπως μέγεθος γραμματοσειράς, χρώμα και θέση.
### Πού μπορώ να λάβω υποστήριξη για το GroupDocs.Signature για .NET;
 Μπορείτε να λάβετε υποστήριξη από το φόρουμ GroupDocs.Signature[εδώ](https://forum.groupdocs.com/c/signature/13).