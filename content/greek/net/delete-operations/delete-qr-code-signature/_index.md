---
title: Διαγράψτε την υπογραφή κωδικού QR από το έγγραφο
linktitle: Διαγράψτε την υπογραφή κωδικού QR από το έγγραφο
second_title: GroupDocs.Signature .NET API
description: Μάθετε πώς να διαγράφετε υπογραφές κώδικα QR από έγγραφα χρησιμοποιώντας το GroupDocs.Signature για .NET. Ακολουθήστε τον βήμα προς βήμα οδηγό μας για αποτελεσματική διαχείριση υπογραφών.
weight: 16
url: /el/net/delete-operations/delete-qr-code-signature/
---

# Διαγράψτε την υπογραφή κωδικού QR από το έγγραφο

## Εισαγωγή
Σε αυτό το σεμινάριο, θα σας καθοδηγήσουμε στη διαδικασία αφαίρεσης μιας υπογραφής κώδικα QR από ένα έγγραφο χρησιμοποιώντας το GroupDocs.Signature για .NET. Ακολουθήστε αυτές τις οδηγίες βήμα προς βήμα για να διαγράψετε αποτελεσματικά τις υπογραφές κώδικα QR.
## Προαπαιτούμενα
Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε τις ακόλουθες προϋποθέσεις:
-  GroupDocs.Signature για .NET: Βεβαιωθείτε ότι έχετε εγκαταστήσει τη βιβλιοθήκη GroupDocs.Signature στο έργο σας .NET. Μπορείτε να το κατεβάσετε από[εδώ](https://releases.groupdocs.com/signature/net/).
- Έγγραφο με υπογραφή κώδικα QR: Προετοιμάστε ένα έγγραφο που περιέχει υπογραφές κώδικα QR που θέλετε να διαγράψετε.
- Βασικές γνώσεις C#: Εξοικειωθείτε με τα βασικά της γλώσσας προγραμματισμού C#.

## Εισαγωγή χώρων ονομάτων
Πριν βουτήξετε στον κώδικα, εισαγάγετε τους απαραίτητους χώρους ονομάτων στο αρχείο C#:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Βήμα 1: Καθορισμός Διαδρομών Αρχείων
```csharp
// Η διαδρομή προς τον κατάλογο εγγράφων.
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
// Καθορίστε τη διαδρομή αρχείου εξόδου για το τροποποιημένο έγγραφο.
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);
// Αντιγράψτε το αρχείο προέλευσης καθώς η μέθοδος Διαγραφή λειτουργεί με το ίδιο Έγγραφο.
File.Copy(filePath, outputFilePath, true);
```
## Βήμα 2: Αρχικοποίηση αντικειμένου υπογραφής
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Δημιουργήστε επιλογές για την αναζήτηση υπογραφών κωδικών QR.
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    // Αναζητήστε υπογραφές κωδικών QR στο έγγραφο.
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```
## Βήμα 3: Ελέγξτε για ύπαρξη υπογραφής κωδικού QR
```csharp
    if (signatures.Count > 0)
    {
        // Αποκτήστε την πρώτη υπογραφή κωδικού QR που βρέθηκε στο έγγραφο.
        QrCodeSignature qrCodeSignature = signatures[0];
```
## Βήμα 4: Διαγράψτε την υπογραφή κωδικού QR
```csharp
        // Διαγράψτε την υπογραφή του κωδικού QR από το έγγραφο.
        bool result = signature.Delete(qrCodeSignature);
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```
Συγχαρητήρια! Καταργήσατε με επιτυχία την υπογραφή κώδικα QR από το έγγραφο χρησιμοποιώντας το GroupDocs.Signature για .NET.

## συμπέρασμα
Σε αυτό το σεμινάριο, μάθαμε πώς να διαγράψουμε μια υπογραφή κώδικα QR από ένα έγγραφο χρησιμοποιώντας το GroupDocs.Signature για .NET. Ακολουθώντας τα παρεχόμενα βήματα, μπορείτε να διαχειριστείτε και να χειριστείτε αποτελεσματικά τις υπογραφές στις εφαρμογές σας .NET.
## Συχνές ερωτήσεις
### Μπορώ να διαγράψω πολλές υπογραφές κώδικα QR από ένα έγγραφο;
Ναι, μπορείτε να τροποποιήσετε τον κωδικό ώστε να επαναλαμβάνεται σε όλες τις υπογραφές κώδικα QR και να τις διαγράψετε ανάλογα.
### Το GroupDocs.Signature υποστηρίζει άλλους τύπους υπογραφών εκτός από κωδικούς QR;
Ναι, το GroupDocs.Signature υποστηρίζει διάφορους τύπους υπογραφών, όπως κείμενο, εικόνα, γραμμωτό κώδικα και άλλα.
### Είναι το GroupDocs.Signature συμβατό με όλες τις μορφές εγγράφων;
Το GroupDocs.Signature υποστηρίζει ένα ευρύ φάσμα μορφών εγγράφων, όπως PDF, Microsoft Word, Excel, PowerPoint και άλλα.
### Μπορώ να προσαρμόσω τις επιλογές αναζήτησης για υπογραφές;
Ναι, μπορείτε να προσαρμόσετε τις επιλογές αναζήτησης σύμφωνα με τις απαιτήσεις σας για να εντοπίσετε συγκεκριμένες υπογραφές μέσα στο έγγραφο.
### Υπάρχει διαθέσιμη δοκιμαστική έκδοση για το GroupDocs.Signature;
 Ναι, μπορείτε να αποκτήσετε πρόσβαση σε μια δωρεάν δοκιμαστική έκδοση του GroupDocs.Signature από[εδώ](https://releases.groupdocs.com/).