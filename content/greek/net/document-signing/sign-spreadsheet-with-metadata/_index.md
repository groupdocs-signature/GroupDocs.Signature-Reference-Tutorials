---
"description": "Προστατέψτε και βελτιώστε τα υπολογιστικά φύλλα του Excel ενσωματώνοντας υπογραφές μεταδεδομένων χρησιμοποιώντας το GroupDocs.Signature για .NET. Προσθέστε πληροφορίες συντάκτη, χρονικές σημάνσεις και προσαρμοσμένα δεδομένα για να βελτιώσετε την ιχνηλασιμότητα και την αυθεντικότητα των εγγράφων."
"linktitle": "Υπογραφή υπολογιστικού φύλλου με μεταδεδομένα"
"second_title": "API GroupDocs.Signature .NET"
"title": "Προσθήκη υπογραφών μεταδεδομένων σε υπολογιστικά φύλλα Excel σε C# .NET"
"url": "/el/net/document-signing/sign-spreadsheet-with-metadata/"
"weight": 13
type: docs
---
## Εισαγωγή

Τα υπολογιστικά φύλλα Excel συχνά περιέχουν κρίσιμα επιχειρηματικά δεδομένα, οικονομικές πληροφορίες και σημαντικούς υπολογισμούς. Η διασφάλιση της αυθεντικότητάς τους, η παρακολούθηση της προέλευσής τους και η προστασία της ακεραιότητάς τους είναι ζωτικής σημασίας σε πολλά επαγγελματικά περιβάλλοντα. Μια αποτελεσματική προσέγγιση για την ενίσχυση της ασφάλειας και της ιχνηλασιμότητας των υπολογιστικών φύλλων είναι η ενσωμάτωση υπογραφών μεταδεδομένων.

Αυτό το ολοκληρωμένο σεμινάριο θα σας καθοδηγήσει στη διαδικασία υπογραφής υπολογιστικών φύλλων Excel με μεταδεδομένα χρησιμοποιώντας το GroupDocs.Signature για .NET. Προσθέτοντας υπογραφές μεταδεδομένων, μπορείτε να ενσωματώσετε πολύτιμες πληροφορίες, όπως στοιχεία συντάκτη, χρονικές σημάνσεις δημιουργίας, αναγνωριστικά εγγράφων και άλλες προσαρμοσμένες ιδιότητες, απευθείας στη δομή αρχείου υπολογιστικού φύλλου.

## Προαπαιτούμενα

Πριν προχωρήσετε σε αυτό το σεμινάριο, βεβαιωθείτε ότι έχετε τα εξής:

1. [GroupDocs.Signature για .NET](https://releases.groupdocs.com/signature/net/) - Λήψη και εγκατάσταση της βιβλιοθήκης
2. Περιβάλλον Ανάπτυξης - Visual Studio ή οποιοδήποτε άλλο IDE συμβατό με .NET
3. Υπολογιστικό φύλλο Excel - Ένα δείγμα αρχείου υπολογιστικού φύλλου (XLSX, XLS, κ.λπ.)
4. Βασικές γνώσεις C# - Εξοικείωση με τη γλώσσα προγραμματισμού C#

## Εισαγωγή χώρων ονομάτων

Ξεκινήστε εισάγοντας τους απαραίτητους χώρους ονομάτων για να αποκτήσετε πρόσβαση στη λειτουργικότητα του GroupDocs.Signature:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Βήμα 1: Ρύθμιση διαδρομών αρχείων

Ορίστε τις διαδρομές για το υπολογιστικό φύλλο προέλευσης και πού θα πρέπει να αποθηκευτεί η υπογεγραμμένη έξοδος:

```csharp
// Καθορίστε τη διαδρομή προς το αρχείο Excel σας
string filePath = "sample.xlsx";

// Ορίστε τον κατάλογο εξόδου και το όνομα αρχείου για το υπογεγραμμένο υπολογιστικό φύλλο
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");

// Βεβαιωθείτε ότι ο κατάλογος εξόδου υπάρχει
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Βήμα 2: Αρχικοποίηση του αντικειμένου υπογραφής

Δημιουργήστε μια παρουσία της κλάσης Signature με το αρχείο υπολογιστικού φύλλου προέλευσης:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Ο υπόλοιπος κώδικας θα μπει εδώ
}
```

## Βήμα 3: Δημιουργία και ρύθμιση παραμέτρων υπογραφών μεταδεδομένων

Στη συνέχεια, ορίστε τις επιλογές μεταδεδομένων και δημιουργήστε έναν πίνακα υπογραφών μεταδεδομένων υπολογιστικού φύλλου:

```csharp
// Δημιουργία αντικειμένου επιλογών μεταδεδομένων
MetadataSignOptions options = new MetadataSignOptions();

// Δημιουργήστε μια σειρά από υπογραφές μεταδεδομένων υπολογιστικών φύλλων με διαφορετικούς τύπους δεδομένων
SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // Τιμή συμβολοσειράς
    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // Τιμή ημερομηνίας/ώρας
    new SpreadsheetMetadataSignature("DocumentId", 123456),           // Ακέραιη τιμή
    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // Διπλή αξία
    new SpreadsheetMetadataSignature("Amount", 123.456M),             // Δεκαδική τιμή
    new SpreadsheetMetadataSignature("Total", 123.456F)               // Αριθ. κινητής μεταβλητής
};

// Προσθήκη συλλογής υπογραφών στις επιλογές
options.Signatures.AddRange(signatures);
```

## Βήμα 4: Υπογραφή του υπολογιστικού φύλλου με μεταδεδομένα

Εφαρμόστε τις υπογραφές μεταδεδομένων στο υπολογιστικό φύλλο και αποθηκεύστε το αποτέλεσμα:

```csharp
// Υπογράψτε το έγγραφο και αποθηκεύστε το στη διαδρομή αρχείου εξόδου
SignResult result = signature.Sign(outputFilePath, options);

// Εμφάνιση μηνύματος επιτυχίας
Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed spreadsheet saved at: {outputFilePath}");
```

## Πλήρες παράδειγμα

Ακολουθεί το πλήρες παράδειγμα κώδικα που συνδυάζει όλα τα βήματα:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignSpreadsheetWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Καθορίστε διαδρομές αρχείων
            string filePath = "sample.xlsx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");
            
            // Βεβαιωθείτε ότι ο κατάλογος εξόδου υπάρχει
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Υπογραφή του υπολογιστικού φύλλου με μεταδεδομένα
            using (Signature signature = new Signature(filePath))
            {
                // Δημιουργία αντικειμένου επιλογών μεταδεδομένων
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Δημιουργήστε μια σειρά από υπογραφές μεταδεδομένων υπολογιστικών φύλλων με διαφορετικούς τύπους δεδομένων
                SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
                {
                    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // Τιμή συμβολοσειράς
                    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // Τιμή ημερομηνίας/ώρας
                    new SpreadsheetMetadataSignature("DocumentId", 123456),           // Ακέραιη τιμή
                    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // Διπλή αξία
                    new SpreadsheetMetadataSignature("Amount", 123.456M),             // Δεκαδική τιμή
                    new SpreadsheetMetadataSignature("Total", 123.456F)               // Αριθ. κινητής μεταβλητής
                };
                
                // Προσθήκη συλλογής υπογραφών στις επιλογές
                options.Signatures.AddRange(signatures);
                
                // Υπογραφή εγγράφου και αποθήκευση σε αρχείο
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Εμφάνιση αποτελεσμάτων
                Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Προηγμένες Τεχνικές Μεταδεδομένων Υπολογιστικών Φύλλων

### Εργασία με προσαρμοσμένες και ενσωματωμένες ιδιότητες υπολογιστικού φύλλου

Τα υπολογιστικά φύλλα του Excel διαθέτουν ενσωματωμένες και προσαρμοσμένες ιδιότητες, στις οποίες μπορείτε να αποκτήσετε πρόσβαση μέσω του παραθύρου διαλόγου ιδιοτήτων αρχείου. Το GroupDocs.Signature σάς επιτρέπει να εργαστείτε και με τα δύο:

```csharp
// Προσθήκη ενσωματωμένων ιδιοτήτων
signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Company", "Sherlock Holmes Consulting"),
    new SpreadsheetMetadataSignature("Category", "Financial"),
    new SpreadsheetMetadataSignature("Keywords", "budget,forecast,analysis"),
    new SpreadsheetMetadataSignature("Comments", "This spreadsheet contains confidential information"),
    new SpreadsheetMetadataSignature("Manager", "John Watson")
};
options.Signatures.AddRange(signatures);

// Προσθήκη προσαρμοσμένων ιδιοτήτων
options.Signatures.Add(new SpreadsheetMetadataSignature("Department", "Finance"));
options.Signatures.Add(new SpreadsheetMetadataSignature("SecurityLevel", "Confidential"));
```

### Αναζήτηση μεταδεδομένων σε υπογεγραμμένα υπολογιστικά φύλλα

Μετά την υπογραφή, ίσως θελήσετε να επαληθεύσετε ή να εξαγάγετε τα μεταδεδομένα:

```csharp
// Δημιουργία επιλογών αναζήτησης για μεταδεδομένα
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Αναζήτηση για υπογραφές μεταδεδομένων
SearchResult searchResult = signature.Search(searchOptions);

// Εμφάνιση υπογραφών που βρέθηκαν
Console.WriteLine($"Found {searchResult.Signatures.Count} metadata signatures:");
foreach (var foundSignature in searchResult.Signatures)
{
    MetadataSignature metadataSignature = foundSignature as MetadataSignature;
    if (metadataSignature != null)
    {
        Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value} ({metadataSignature.Value.GetType().Name})");
    }
}
```

### Ενημέρωση υπαρχόντων μεταδεδομένων

Μπορείτε να ενημερώσετε τα υπάρχοντα μεταδεδομένα σε υπολογιστικά φύλλα χρησιμοποιώντας τα ίδια ονόματα ιδιοτήτων:

```csharp
// Ενημέρωση υπαρχόντων μεταδεδομένων
options.Signatures.Add(new SpreadsheetMetadataSignature("Author", "Updated Author Name"));
```

## Σύναψη

Σε αυτό το ολοκληρωμένο σεμινάριο, μάθατε πώς να υπογράφετε υπολογιστικά φύλλα Excel με μεταδεδομένα χρησιμοποιώντας το GroupDocs.Signature για .NET. Η ενσωμάτωση μεταδεδομένων σε αρχεία υπολογιστικών φύλλων βελτιώνει την ιχνηλασιμότητα των εγγράφων, παρέχει πολύτιμο περιεχόμενο και βοηθά στην επαλήθευση της αυθεντικότητας.

Οι υπογραφές μεταδεδομένων σε υπολογιστικά φύλλα είναι ιδιαίτερα χρήσιμες σε επιχειρηματικά περιβάλλοντα όπου η προέλευση, η συγγραφή και η παρακολούθηση έκδοσης του εγγράφου είναι σημαντικές. Τα ενσωματωμένα μεταδεδομένα μπορούν να περιλαμβάνουν πληροφορίες σχετικά με τον δημιουργό, την ώρα δημιουργίας, τα αναγνωριστικά εγγράφων και τις προσαρμοσμένες ιδιότητες που σχετίζονται με τις ανάγκες του οργανισμού σας.

Υλοποιώντας υπογραφές μεταδεδομένων με το GroupDocs.Signature, μπορείτε να διασφαλίσετε ότι τα υπολογιστικά φύλλα του Excel διατηρούν την ακεραιότητά τους και παρέχουν επαληθεύσιμες πληροφορίες καθ' όλη τη διάρκεια του κύκλου ζωής τους.

## Συχνές ερωτήσεις

### Μπορώ να προσθέσω μεταδεδομένα σε υπολογιστικά φύλλα που έχουν ήδη ορίσει ορισμένες ιδιότητες;

Ναι, μπορείτε να προσθέσετε νέα μεταδεδομένα ή να ενημερώσετε υπάρχοντα μεταδεδομένα σε υπολογιστικά φύλλα. Το GroupDocs.Signature θα χειριστεί την ενσωμάτωση, είτε προσθέτοντας νέες ιδιότητες είτε ενημερώνοντας υπάρχουσες με τα ίδια ονόματα.

### Ποιες μορφές υπολογιστικών φύλλων υποστηρίζονται για την υπογραφή μεταδεδομένων;

Το GroupDocs.Signature για .NET υποστηρίζει την υπογραφή μεταδεδομένων για διάφορες μορφές υπολογιστικών φύλλων, συμπεριλαμβανομένων των XLSX, XLS, XLSM, ODS και άλλων. Για μια πλήρη λίστα, ανατρέξτε στο [επίσημη τεκμηρίωση](https://docs.groupdocs.com/signature/net/).

### Είναι οι υπογραφές μεταδεδομένων στα υπολογιστικά φύλλα ορατές στους χρήστες;

Οι υπογραφές μεταδεδομένων δεν είναι ορατές στο ίδιο το περιεχόμενο του υπολογιστικού φύλλου. Ωστόσο, μπορούν να προβληθούν μέσω του πίνακα ιδιοτήτων του εγγράφου στο Excel ή σε άλλες συμβατές εφαρμογές.

### Μπορώ να επικυρώσω μέσω προγραμματισμού εάν ένα υπολογιστικό φύλλο έχει παραβιαστεί μετά την προσθήκη μεταδεδομένων;

Ναι, το GroupDocs.Signature παρέχει δυνατότητες επαλήθευσης που μπορούν να βοηθήσουν στην ανίχνευση τροποποιήσεων ενός εγγράφου μετά την υπογραφή, συμπεριλαμβανομένων των αλλαγών στα μεταδεδομένα.

### Η προσθήκη μεταδεδομένων επηρεάζει τη λειτουργικότητα του υπολογιστικού φύλλου;

Η προσθήκη μεταδεδομένων έχει ελάχιστη επίδραση στο μέγεθος του αρχείου και καμία επίδραση στη λειτουργικότητα του υπολογιστικού φύλλου. Είναι ένας ελαφρύς τρόπος για να βελτιώσετε τις ιδιότητες του εγγράφου χωρίς να επηρεάσετε τους υπολογισμούς, τους τύπους ή άλλες λειτουργίες του Excel.

### Πού μπορώ να βρω περισσότερους πόρους και υποστήριξη;

- [Αναφορά API](https://reference.groupdocs.com/signature/net/)
- [Λήψεις](https://releases.groupdocs.com/signature/net/)
- [Παραδείγματα](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Απόδειξη με έγγραφα](https://docs.groupdocs.com/signature/net/)
- [Σελίδα προϊόντος](https://products.groupdocs.com/signature/net/)
- [Ιστολόγιο](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Φόρουμ Υποστήριξης](https://forum.groupdocs.com/c/signature/13)
- [Προσωρινή Άδεια](https://purchase.groupdocs.com/temporary-license/)