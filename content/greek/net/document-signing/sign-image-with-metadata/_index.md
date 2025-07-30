---
"description": "Μάθετε πώς να υπογράφετε και να ενσωματώνετε μεταδεδομένα σε εικόνες χρησιμοποιώντας το GroupDocs.Signature για .NET. Προσθέστε πληροφορίες δημιουργού, χρονικές σημάνσεις και προσαρμοσμένα δεδομένα για να βελτιώσετε την αυθεντικότητα και την ιχνηλασιμότητα της εικόνας."
"linktitle": "Υπογραφή εικόνας με μεταδεδομένα"
"second_title": "API GroupDocs.Signature .NET"
"title": "Υπογραφή εικόνων με μεταδεδομένα σε C# .NET"
"url": "/el/net/document-signing/sign-image-with-metadata/"
"weight": 10
---

## Εισαγωγή

Η ψηφιακή υπογραφή εικόνων με μεταδεδομένα αποκτά ολοένα και μεγαλύτερη σημασία για την εδραίωση της αυθεντικότητας, της ιδιοκτησίας και της ιχνηλασιμότητας. Το GroupDocs.Signature για .NET παρέχει μια ισχυρή, αλλά και εύχρηστη λύση για την προσθήκη υπογραφών μεταδεδομένων σε διάφορες μορφές εικόνας. Αυτό το σεμινάριο σας καθοδηγεί σε ολόκληρη τη διαδικασία υπογραφής εικόνων με μεταδεδομένα χρησιμοποιώντας C#.

Οι υπογραφές μεταδεδομένων σάς επιτρέπουν να ενσωματώνετε πολύτιμες πληροφορίες απευθείας σε αρχεία εικόνας, όπως πληροφορίες δημιουργού, χρονικές σημάνσεις δημιουργίας, μοναδικά αναγνωριστικά και άλλα. Αυτές οι πληροφορίες γίνονται μέρος του ίδιου του αρχείου εικόνας, παρέχοντας μια αξιόπιστη μέθοδο για την παρακολούθηση και την επαλήθευση της αυθεντικότητας της εικόνας.

## Προαπαιτούμενα

Πριν προχωρήσετε σε αυτό το σεμινάριο, βεβαιωθείτε ότι έχετε τα εξής:

1. [GroupDocs.Signature για .NET](https://releases.groupdocs.com/signature/net/) - Λήψη και εγκατάσταση της βιβλιοθήκης
2. Περιβάλλον Ανάπτυξης - Visual Studio ή οποιοδήποτε συμβατό IDE με υποστήριξη .NET
3. Αρχείο εικόνας - Ένα δείγμα αρχείου εικόνας σε υποστηριζόμενη μορφή (PNG, JPG, TIFF, κ.λπ.)
4. Βασικές γνώσεις προγραμματισμού C# - Εξοικείωση με τις έννοιες προγραμματισμού C#

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

Ορίστε τις διαδρομές για την εικόνα πηγής σας και πού θα πρέπει να αποθηκευτεί η υπογεγραμμένη έξοδος:

```csharp
// Καθορίστε τη διαδρομή προς το αρχείο εικόνας πηγής
string filePath = "sample.png";

// Ορίστε τον κατάλογο εξόδου και το όνομα αρχείου για την υπογεγραμμένη εικόνα
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignImageWithMetadata", "SignedWithMetadata.png");

// Βεβαιωθείτε ότι ο κατάλογος εξόδου υπάρχει
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Βήμα 2: Αρχικοποίηση του αντικειμένου υπογραφής

Δημιουργήστε μια παρουσία της κλάσης Signature με το αρχείο εικόνας πηγής σας:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Ο υπόλοιπος κώδικας θα μπει εδώ
}
```

## Βήμα 3: Δημιουργία και ρύθμιση παραμέτρων υπογραφών μεταδεδομένων

Στη συνέχεια, ορίστε τα μεταδεδομένα που θέλετε να ενσωματώσετε στην εικόνα. Το GroupDocs.Signature υποστηρίζει διάφορους τύπους δεδομένων για μεταδεδομένα:

```csharp
// Αρχικοποίηση αναγνωριστικού μεταδεδομένων (συγκεκριμένα για τη μορφή εικόνας)
ushort imgsMetadataId = 41996;

// Δημιουργία αντικειμένου επιλογών μεταδεδομένων
MetadataSignOptions options = new MetadataSignOptions();

// Προσθήκη διαφόρων τύπων υπογραφών μεταδεδομένων
options
    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes"))  // Τιμή συμβολοσειράς
    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Τιμή ημερομηνίας/ώρας
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Ακέραιη τιμή
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Διπλή αξία
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Δεκαδική τιμή
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Αριθ. κινητής μεταβλητής
```

## Βήμα 4: Υπογραφή της εικόνας με μεταδεδομένα

Εφαρμόστε τις υπογραφές μεταδεδομένων στην εικόνα και αποθηκεύστε το αποτέλεσμα:

```csharp
// Υπογράψτε το έγγραφο και αποθηκεύστε το στη διαδρομή αρχείου εξόδου
SignResult result = signature.Sign(outputFilePath, options);

// Εμφάνιση μηνύματος επιτυχίας
Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed image saved at: {outputFilePath}");
```

## Πλήρες παράδειγμα

Ακολουθεί το πλήρες παράδειγμα κώδικα που συνδυάζει όλα τα βήματα:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignImageWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Καθορίστε διαδρομές αρχείων
            string filePath = "sample.png";            
            string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
            
            // Βεβαιωθείτε ότι ο κατάλογος εξόδου υπάρχει
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Υπογραφή της εικόνας με μεταδεδομένα
            using (Signature signature = new Signature(filePath))
            {
                // Αρχικοποίηση αναγνωριστικού μεταδεδομένων (συγκεκριμένα για τη μορφή εικόνας)
                ushort imgsMetadataId = 41996;
                
                // Δημιουργία επιλογών μεταδεδομένων
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Προσθήκη διαφορετικών τύπων υπογραφών μεταδεδομένων
                options
                    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes")) // Τιμή συμβολοσειράς
                    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Τιμή ημερομηνίας/ώρας
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Ακέραιη τιμή
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Διπλή αξία
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Δεκαδική τιμή
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Αριθ. κινητής μεταβλητής
                
                // Υπογραφή εγγράφου και αποθήκευση σε αρχείο
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Εμφάνιση αποτελεσμάτων
                Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Προηγμένες Τεχνικές Υπογραφής Μεταδεδομένων

### Εργασία με προσαρμοσμένα μεταδεδομένα

Μπορείτε επίσης να δημιουργήσετε προσαρμοσμένα πεδία μεταδεδομένων με συγκεκριμένα αναγνωριστικά:

```csharp
// Δημιουργήστε προσαρμοσμένα μεταδεδομένα με συγκεκριμένο αναγνωριστικό
options.Add(new ImageMetadataSignature(42000, "CustomValue"));
```

### Επαλήθευση υπογραφών μεταδεδομένων

Μετά την υπογραφή, ίσως θελήσετε να επαληθεύσετε τις υπογραφές μεταδεδομένων:

```csharp
// Δημιουργία επιλογών επαλήθευσης
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Αναζήτηση για υπογραφές μεταδεδομένων
SearchResult result = signature.Search(searchOptions);

// Εμφάνιση υπογραφών που βρέθηκαν
Console.WriteLine($"Found {result.Signatures.Count} metadata signatures:");
foreach(var metadataSignature in result.Signatures)
{
    Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value}");
}
```

## Σύναψη

Σε αυτό το σεμινάριο, μάθατε πώς να υπογράφετε εικόνες με μεταδεδομένα χρησιμοποιώντας το GroupDocs.Signature για .NET. Η ενσωμάτωση μεταδεδομένων σε εικόνες παρέχει έναν εξαιρετικό τρόπο για να βελτιώσετε την αυθεντικότητα των εικόνων, να προσθέσετε κρίσιμες πληροφορίες και να βελτιώσετε τις ροές εργασίας διαχείρισης εγγράφων. Η διαδικασία είναι απλή αλλά ισχυρή, επιτρέποντας την προσαρμογή με βάση τις συγκεκριμένες απαιτήσεις σας.

Τα μεταδεδομένα που είναι ενσωματωμένα στο αρχείο εικόνας μπορούν να χρησιμοποιηθούν για διάφορους σκοπούς, όπως προστασία πνευματικών δικαιωμάτων, παρακολούθηση προέλευσης εικόνας, προσθήκη περιγραφικών πληροφοριών και δημιουργία ψηφιακής αλυσίδας επιμέλειας. Εφαρμόζοντας υπογραφές μεταδεδομένων, μπορείτε να διασφαλίσετε ότι οι εικόνες σας διατηρούν την ακεραιότητα και την αυθεντικότητά τους καθ' όλη τη διάρκεια του κύκλου ζωής τους.

## Συχνές ερωτήσεις

### Μπορώ να προσθέσω μεταδεδομένα σε υπάρχουσες υπογεγραμμένες εικόνες;

Ναι, μπορείτε να προσθέσετε επιπλέον μεταδεδομένα σε εικόνες που περιέχουν ήδη υπογραφές μεταδεδομένων. Τα υπάρχοντα μεταδεδομένα θα διατηρηθούν και θα προστεθούν νέα μεταδεδομένα ανάλογα.

### Ποιες μορφές εικόνας υποστηρίζονται για την υπογραφή μεταδεδομένων;

Το GroupDocs.Signature για .NET υποστηρίζει την υπογραφή μεταδεδομένων για διάφορες μορφές εικόνας, όπως PNG, JPEG, TIFF, BMP, GIF και άλλες. Για μια πλήρη λίστα, ανατρέξτε στο [επίσημη τεκμηρίωση](https://docs.groupdocs.com/signature/net/).

### Είναι δυνατή η κρυπτογράφηση των μεταδεδομένων σε εικόνες;

Ναι, το GroupDocs.Signature παρέχει επιλογές κρυπτογράφησης μεταδεδομένων για βελτιωμένη ασφάλεια. Μπορείτε να χρησιμοποιήσετε τις επιλογές κρυπτογράφησης που παρέχονται από τη βιβλιοθήκη για να προστατεύσετε ευαίσθητες πληροφορίες μεταδεδομένων.

### Μπορώ να επικυρώσω μέσω προγραμματισμού την αυθεντικότητα υπογεγραμμένων εικόνων;

Απολύτως. Μπορείτε να χρησιμοποιήσετε τις μεθόδους επαλήθευσης στο GroupDocs.Signature για να επικυρώσετε τις υπογραφές μεταδεδομένων και να επιβεβαιώσετε την αυθεντικότητα των υπογεγραμμένων εικόνων.

### Υπάρχει περιορισμός στο μέγεθος του αρχείου κατά την υπογραφή εικόνων με μεταδεδομένα;

Δεν υπάρχει συγκεκριμένος περιορισμός στο μέγεθος των αρχείων από την ίδια τη βιβλιοθήκη, αλλά τα πολύ μεγάλα αρχεία ενδέχεται να απαιτούν περισσότερο χρόνο επεξεργασίας και μνήμη. Συνιστάται να λαμβάνετε υπόψη τους πόρους του συστήματος όταν εργάζεστε με εξαιρετικά μεγάλες εικόνες.

### Πώς μπορώ να αποκτήσω προσωρινή άδεια για δοκιμαστικούς σκοπούς;

Μπορείτε να αποκτήσετε ένα [προσωρινή άδεια](https://purchase.groupdocs.com/temporary-license/) για τον έλεγχο του GroupDocs.Signature πριν από την πραγματοποίηση μιας αγοράς.

### Πού μπορώ να βρω περισσότερους πόρους και υποστήριξη;

- [Αναφορά API](https://reference.groupdocs.com/signature/net/)
- [Λήψεις](https://releases.groupdocs.com/signature/net/)
- [Παραδείγματα](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Απόδειξη με έγγραφα](https://docs.groupdocs.com/signature/net/)
- [Σελίδα προϊόντος](https://products.groupdocs.com/signature/net/)
- [Ιστολόγιο](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Φόρουμ Υποστήριξης](https://forum.groupdocs.com/c/signature/13)