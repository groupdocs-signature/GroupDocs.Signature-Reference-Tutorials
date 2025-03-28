---
title: Διαγραφή πολλαπλών υπογραφών από το έγγραφο
linktitle: Διαγραφή πολλαπλών υπογραφών από το έγγραφο
second_title: GroupDocs.Signature .NET API
description: Διαγράψτε χωρίς κόπο πολλές υπογραφές από έγγραφα χρησιμοποιώντας το GroupDocs.Signature για .NET. Βελτιώστε τη ροή εργασιών διαχείρισης εγγράφων.
weight: 15
url: /el/net/delete-operations/delete-multiple-signatures/
---

# Διαγραφή πολλαπλών υπογραφών από το έγγραφο

## Εισαγωγή
Στον ψηφιακό κόσμο, η διαχείριση εγγράφων συχνά περιλαμβάνει το χειρισμό διαφόρων υπογραφών. Η διαγραφή πολλαπλών υπογραφών από ένα έγγραφο μέσω προγραμματισμού μπορεί να απλοποιήσει τις ροές εργασίας και να βελτιώσει την αποτελεσματικότητα. Με το GroupDocs.Signature για .NET, αυτή η εργασία γίνεται απρόσκοπτη και απλή. Αυτό το σεμινάριο θα σας καθοδηγήσει στη διαδικασία διαγραφής πολλαπλών υπογραφών από ένα έγγραφο βήμα προς βήμα.
## Προαπαιτούμενα
Πριν βουτήξετε στο σεμινάριο, βεβαιωθείτε ότι έχετε τις ακόλουθες προϋποθέσεις:
- Βασική κατανόηση της γλώσσας προγραμματισμού C#.
- Εγκατεστημένο GroupDocs.Signature για τη βιβλιοθήκη .NET.
- Δείγμα εγγράφου με πολλαπλές υπογραφές για δοκιμή.

## Εισαγωγή χώρων ονομάτων
Ξεκινήστε εισάγοντας τους απαραίτητους χώρους ονομάτων για πρόσβαση στη λειτουργικότητα του GroupDocs.Signature για .NET:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Βήμα 1: Καθορίστε τη διαδρομή εγγράφου και το όνομα αρχείου
Ορίστε τη διαδρομή αρχείου του εγγράφου που περιέχει πολλές υπογραφές. Βεβαιωθείτε ότι έχετε την κατάλληλη διαδρομή αρχείου και όνομα αρχείου:
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
```
## Βήμα 2: Αντιγράψτε το έγγραφο για επεξεργασία
Για να αποφύγετε την τροποποίηση του αρχικού εγγράφου, δημιουργήστε ένα αντίγραφο για επεξεργασία:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "DeleteMultiple", fileName);
File.Copy(filePath, outputFilePath, true);
```
## Βήμα 3: Αρχικοποίηση αντικειμένου υπογραφής
Δημιουργήστε ένα αντικείμενο Signature χρησιμοποιώντας τη διαδρομή αρχείου εξόδου:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Ο κωδικός επεξεργασίας υπογραφής πηγαίνει εδώ
}
```
## Βήμα 4: Ορίστε τις επιλογές αναζήτησης
Ορίστε διάφορες επιλογές αναζήτησης για την αναγνώριση υπογραφών μέσα στο έγγραφο. Οι επιλογές περιλαμβάνουν αναζήτηση κειμένου, αναζήτηση εικόνων, αναζήτηση γραμμωτού κώδικα και αναζήτηση κωδικού QR:
```csharp
TextSearchOptions textSearchOptions = new TextSearchOptions();
ImageSearchOptions imageSearchOptions = new ImageSearchOptions();
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions();
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions();
// Προσθήκη επιλογών στη λίστα
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textSearchOptions);
listOptions.Add(imageSearchOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
```
## Βήμα 5: Αναζήτηση για υπογραφές
Εκτελέστε μια λειτουργία αναζήτησης για να βρείτε όλες τις υπογραφές μέσα στο έγγραφο με βάση τις καθορισμένες επιλογές αναζήτησης:
```csharp
SearchResult result = signature.Search(listOptions);
```
## Βήμα 6: Διαγραφή υπογραφών
Εάν βρεθούν υπογραφές, προχωρήστε στη διαγραφή τους:
```csharp
if (result.Signatures.Count > 0)
{
    // Προσπαθήστε να διαγράψετε όλες τις υπογραφές
    DeleteResult deleteResult = signature.Delete(result.Signatures);
    //Ελέγξτε εάν η διαγραφή ήταν επιτυχής
    if(deleteResult.Succeeded.Count == result.Signatures.Count)
    {
        Console.WriteLine("\nAll signatures were successfully deleted!");                        
    }
    else
    {
        Console.WriteLine($"Successfully deleted signatures : {deleteResult.Succeeded.Count}");
        Helper.WriteError($"Not deleted signatures : {deleteResult.Failed.Count}");
    }
    // Εμφάνιση πληροφοριών σχετικά με τις διαγραμμένες υπογραφές
    Console.WriteLine("\nList of deleted signatures:");
    int number = 1;
    foreach(BaseSignature temp in deleteResult.Succeeded)
    {
        Console.WriteLine($"Signature #{number++}: Type: {temp.SignatureType} Id:{temp.SignatureId}, Location: {temp.Left}x{temp.Top}. Size: {temp.Width}x{temp.Height}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## συμπέρασμα
Η διαγραφή πολλαπλών υπογραφών από ένα έγγραφο μέσω προγραμματισμού είναι μια κρίσιμη εργασία στη διαχείριση εγγράφων. Με το GroupDocs.Signature για .NET, αυτή η διαδικασία γίνεται αποτελεσματική και αξιόπιστη. Ακολουθώντας τα βήματα που περιγράφονται σε αυτό το σεμινάριο, μπορείτε εύκολα να ενσωματώσετε τη λειτουργία διαγραφής υπογραφής στις εφαρμογές σας .NET.
## Συχνές ερωτήσεις
### Μπορεί το GroupDocs.Signature για .NET να χειριστεί διάφορες μορφές εγγράφων;
Ναι, το GroupDocs.Signature για .NET υποστηρίζει ένα ευρύ φάσμα μορφών εγγράφων, συμπεριλαμβανομένων των DOCX, PDF, PPTX, XLSX και άλλων.
### Είναι δυνατή η προσαρμογή των επιλογών αναζήτησης για τον εντοπισμό υπογραφών;
Αναμφίβολα, μπορείτε να προσαρμόσετε τις επιλογές αναζήτησης όπως αναζήτηση κειμένου, αναζήτηση εικόνων, αναζήτηση γραμμωτού κώδικα και αναζήτηση κωδικού QR για να ικανοποιήσετε τις συγκεκριμένες απαιτήσεις σας.
### Το GroupDocs.Signature για .NET παρέχει μηχανισμούς διαχείρισης σφαλμάτων;
Ναι, η βιβλιοθήκη προσφέρει ισχυρές δυνατότητες χειρισμού σφαλμάτων για να διασφαλιστεί η ομαλή εκτέλεση των εργασιών επεξεργασίας εγγράφων.
### Μπορώ να ενσωματώσω το GroupDocs.Signature για .NET με άλλες βιβλιοθήκες τρίτων;
Σίγουρα, το GroupDocs.Signature για .NET έχει σχεδιαστεί για να ενσωματώνεται απρόσκοπτα με άλλες βιβλιοθήκες .NET, παρέχοντας ευελιξία και επεκτασιμότητα.
### Πού μπορώ να βρω πρόσθετη υποστήριξη και πόρους για το GroupDocs.Signature για .NET;
 Μπορείτε να επισκεφτείτε τα GroupDocs[δικαστήριο](https://forum.groupdocs.com/c/signature/13) αφιερώνονται σε συζητήσεις που σχετίζονται με τις υπογραφές και ζητούν βοήθεια από την κοινότητα και τους ειδικούς.