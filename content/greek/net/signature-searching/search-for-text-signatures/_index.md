---
"description": "Μάθετε πώς να αναζητάτε αποτελεσματικά υπογραφές κειμένου σε έγγραφα χρησιμοποιώντας το GroupDocs.Signature για .NET με τον ολοκληρωμένο οδηγό βήμα προς βήμα και παραδείγματα κώδικα."
"linktitle": "Αναζήτηση για υπογραφές κειμένου"
"second_title": "API GroupDocs.Signature .NET"
"title": "Αναζήτηση υπογραφών κειμένου σε έγγραφα"
"url": "/el/net/signature-searching/search-for-text-signatures/"
"weight": 16
type: docs
---
## Εισαγωγή

Οι υπογραφές κειμένου είναι μια κοινή μέθοδος για την ένδειξη της συγγραφής, της έγκρισης ή της επαλήθευσης εγγράφων. Στη διαχείριση ψηφιακών εγγράφων, η δυνατότητα προγραμματιστικής αναζήτησης και εξαγωγής υπογραφών κειμένου είναι ζωτικής σημασίας για την επικύρωση εγγράφων, την αυτοματοποίηση της ροής εργασίας και την επαλήθευση συμμόρφωσης. Το GroupDocs.Signature για .NET προσφέρει μια ολοκληρωμένη λύση για την εφαρμογή λειτουργικότητας αναζήτησης υπογραφών κειμένου στις εφαρμογές .NET, υποστηρίζοντας διάφορες μορφές εγγράφων και δυνατότητες προηγμένης αναζήτησης.

Αυτό το σεμινάριο θα σας καθοδηγήσει στη διαδικασία αναζήτησης υπογραφών κειμένου σε έγγραφα χρησιμοποιώντας το GroupDocs.Signature για .NET, παρέχοντας λεπτομερείς εξηγήσεις, οδηγίες βήμα προς βήμα και πρακτικά παραδείγματα κώδικα.

## Προαπαιτούμενα

Πριν ξεκινήσετε την αναζήτηση υπογραφών κειμένου, βεβαιωθείτε ότι έχετε τις ακόλουθες προϋποθέσεις:

1. GroupDocs.Signature για τη βιβλιοθήκη .NET: Λήψη και εγκατάσταση της βιβλιοθήκης από το [σελίδα κυκλοφοριών](https://releases.groupdocs.com/signature/net/).

2. Περιβάλλον Ανάπτυξης: Δημιουργήστε ένα κατάλληλο περιβάλλον ανάπτυξης, όπως το Visual Studio ή οποιοδήποτε συμβατό IDE με υποστήριξη .NET.

3. Δείγματα εγγράφων: Προετοιμάστε έγγραφα δοκιμών που περιέχουν υπογραφές κειμένου για επαλήθευση και δοκιμή.

4. Βασικές γνώσεις C#: Εξοικείωση με τη γλώσσα προγραμματισμού C# και τις έννοιες του .NET framework.

## Εισαγωγή χώρων ονομάτων

Ξεκινήστε εισάγοντας τους απαραίτητους χώρους ονομάτων για να αποκτήσετε πρόσβαση στη λειτουργικότητα του GroupDocs.Signature:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Τώρα, ας αναλύσουμε τη διαδικασία αναζήτησης υπογραφών κειμένου σε σαφή και διαχειρίσιμα βήματα:

## Βήμα 1: Φόρτωση του εγγράφου

Αρχικά, ορίστε τη διαδρομή του εγγράφου και αρχικοποιήστε ένα `Signature` αντικείμενο:

```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);

using (Signature signature = new Signature(filePath))
{
    // Ο κώδικας αναζήτησης υπογραφής κειμένου θα προστεθεί εδώ
}
```

## Βήμα 2: Ρύθμιση παραμέτρων επιλογών αναζήτησης

Δημιουργία και διαμόρφωση `TextSearchOptions` για να καθορίσετε τον τρόπο αναζήτησης στις υπογραφές κειμένου:

```csharp
// Ρύθμιση παραμέτρων επιλογών αναζήτησης κειμένου
TextSearchOptions options = new TextSearchOptions
{
    // Αναζήτηση σε όλες τις σελίδες
    AllPages = true,
    
    // Προαιρετικά: καθορίστε κείμενο που να ταιριάζει
    // Κείμενο = "Εγκρίθηκε",
    
    // Προαιρετικά: καθορίστε τον τύπο αντιστοίχισης
    // Τύπος αντιστοίχισης = Τύπος αντιστοίχισης κειμένου.Περιέχει
};
```

## Βήμα 3: Εκτελέστε αναζήτηση υπογραφής κειμένου

Εκτελέστε την αναζήτηση χρησιμοποιώντας τις διαμορφωμένες επιλογές:

```csharp
// Αναζήτηση για υπογραφές κειμένου
List<TextSignature> signatures = signature.Search<TextSignature>(options);
```

## Βήμα 4: Επεξεργασία και εμφάνιση αποτελεσμάτων

Επαναλάβετε τις υπογραφές κειμένου που βρέθηκαν και εμφανίστε τις λεπτομέρειες τους:

```csharp
// Εμφάνιση αποτελεσμάτων αναζήτησης
Console.WriteLine($"\nSource document '{fileName}' contains {signatures.Count} text signature(s):");

foreach (TextSignature textSignature in signatures)
{
    Console.WriteLine($"Text signature found at page {textSignature.PageNumber} with text '{textSignature.Text}'");
    Console.WriteLine($"Location: X={textSignature.Left}, Y={textSignature.Top}, Width={textSignature.Width}, Height={textSignature.Height}");
    Console.WriteLine($"Signature type: {textSignature.SignatureImplementation}");
    Console.WriteLine();
}
```

## Πλήρες παράδειγμα

Ακολουθεί ένα πλήρες παράδειγμα λειτουργίας που δείχνει πώς να αναζητήσετε υπογραφές κειμένου σε ένα έγγραφο:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace TextSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Διαδρομή εγγράφου - ενημέρωση με τη διαδρομή αρχείου σας
            string filePath = "sample_multiple_signatures.docx";
            string fileName = Path.GetFileName(filePath);
            
            // Αρχικοποίηση στιγμιότυπου υπογραφής
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Ρύθμιση παραμέτρων επιλογών αναζήτησης κειμένου
                    TextSearchOptions options = new TextSearchOptions
                    {
                        // Αναζήτηση σε όλες τις σελίδες
                        AllPages = true
                    };
                    
                    // Αναζήτηση για υπογραφές κειμένου
                    List<TextSignature> signatures = signature.Search<TextSignature>(options);
                    
                    // Εμφάνιση αποτελεσμάτων αναζήτησης
                    Console.WriteLine($"\nSource document '{fileName}' contains {signatures.Count} text signature(s):");
                    
                    foreach (TextSignature textSignature in signatures)
                    {
                        Console.WriteLine($"Text signature found at page {textSignature.PageNumber} with text '{textSignature.Text}'");
                        Console.WriteLine($"Location: X={textSignature.Left}, Y={textSignature.Top}, Width={textSignature.Width}, Height={textSignature.Height}");
                        Console.WriteLine($"Signature type: {textSignature.SignatureImplementation}");
                        Console.WriteLine();
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"Error occurred: {ex.Message}");
                }
            }
            
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## Προηγμένες Τεχνικές Αναζήτησης Υπογραφής Κειμένου

### Αναζήτηση με συγκεκριμένα κριτήρια κειμένου

Για πιο στοχευμένες αναζητήσεις, μπορείτε να προσαρμόσετε το `TextSearchOptions` για φιλτράρισμα με βάση συγκεκριμένο περιεχόμενο κειμένου:

```csharp
// Δημιουργήστε επιλογές αναζήτησης με συγκεκριμένα κριτήρια κειμένου
TextSearchOptions options = new TextSearchOptions
{
    // Αναζήτηση σε όλες τις σελίδες
    AllPages = true,
    
    // Αναζήτηση συγκεκριμένου κειμένου
    Text = "Approved",
    
    // Καθορίστε τον τύπο αντιστοίχισης (Περιέχει, Ακριβές, Ξεκινά με, Λήγει με)
    MatchType = TextMatchType.Contains,
    
    // Αναζήτηση με διάκριση πεζών-κεφαλαίων
    MatchCase = true
};
```

### Αναζήτηση σε συγκεκριμένες περιοχές εγγράφων

Μπορείτε να περιορίσετε την αναζήτηση σε συγκεκριμένες περιοχές του εγγράφου:

```csharp
// Δημιουργία επιλογών αναζήτησης για μια συγκεκριμένη περιοχή εγγράφου
TextSearchOptions options = new TextSearchOptions
{
    // Αναζήτηση μόνο σε συγκεκριμένες σελίδες
    AllPages = false,
    PageNumber = 1,
    
    // Ή καθορίστε πολλές σελίδες
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // Ορίστε μια συγκεκριμένη περιοχή για αναζήτηση
    Rectangle = new Rectangle(100, 100, 400, 200)
};
```

### Προηγμένο φιλτράρισμα κειμένου

Υλοποίηση προσαρμοσμένης λογικής φιλτραρίσματος για πιο σύνθετες απαιτήσεις αναζήτησης:

```csharp
// Δημιουργήστε επιλογές αναζήτησης με προσαρμοσμένη επεξεργασία
TextSearchOptions options = new TextSearchOptions
{
    AllPages = true,
    
    // Ορισμός προσαρμοσμένης επεξεργασίας χρησιμοποιώντας έναν εκπρόσωπο
    ProcessCompleted = (TextSignature signature) =>
    {
        // Προσαρμοσμένη λογική επικύρωσης
        bool isValid = signature.Text.Length > 5 && 
                      (signature.Text.Contains("Approved") || signature.Text.Contains("Verified"));
        
        return isValid;
    }
};
```

### Αναζήτηση διαφορετικών στυλ κειμένου

Χρησιμοποιήστε τις ιδιότητες γραμματοσειράς και στυλ για να φιλτράρετε τις υπογραφές κειμένου:

```csharp
// Δημιουργήστε επιλογές αναζήτησης που στοχεύουν σε συγκεκριμένη εμφάνιση κειμένου
TextSearchOptions options = new TextSearchOptions
{
    // Φιλτράρισμα κατά όνομα γραμματοσειράς
    FontName = "Arial",
    
    // Φιλτράρισμα κατά εύρος μεγέθους γραμματοσειράς
    MinFontSize = 10,
    MaxFontSize = 14,
    
    // Φιλτράρισμα κατά χρώμα γραμματοσειράς
    ForeColor = System.Drawing.Color.Blue
};
```

### Εξαγωγή μεταδεδομένων υπογραφής

Εξαγωγή και επεξεργασία μεταδεδομένων που σχετίζονται με υπογραφές κειμένου:

```csharp
foreach (TextSignature signature in signatures)
{
    // Πρόσβαση σε μεταδεδομένα υπογραφής
    if (signature.Metadata != null && signature.Metadata.Count > 0)
    {
        Console.WriteLine("Signature Metadata:");
        
        foreach (var item in signature.Metadata)
        {
            Console.WriteLine($"  {item.Key}: {item.Value}");
        }
    }
    
    // Ελέγξτε για ημερομηνίες δημιουργίας και τροποποίησης υπογραφής
    if (signature.CreatedOn.HasValue)
    {
        Console.WriteLine($"Created on: {signature.CreatedOn.Value}");
    }
    
    if (signature.ModifiedOn.HasValue)
    {
        Console.WriteLine($"Modified on: {signature.ModifiedOn.Value}");
    }
}
```

## Σύναψη

Σε αυτόν τον ολοκληρωμένο οδηγό, έχουμε εξερευνήσει τον τρόπο αναζήτησης υπογραφών κειμένου σε έγγραφα χρησιμοποιώντας το GroupDocs.Signature για .NET. Από βασικές λειτουργίες αναζήτησης έως προηγμένες τεχνικές, τώρα έχετε τις γνώσεις για να εφαρμόσετε ισχυρή λειτουργικότητα υπογραφής κειμένου στις εφαρμογές .NET που διαθέτετε.

Το GroupDocs.Signature παρέχει ένα ισχυρό και ευέλικτο πλαίσιο για την εργασία με υπογραφές κειμένου, επιτρέποντάς σας να δημιουργήσετε εξελιγμένα συστήματα επαλήθευσης εγγράφων, αυτοματοποιημένες λύσεις ροής εργασίας και εργαλεία επικύρωσης συμμόρφωσης.

## Συχνές ερωτήσεις

### Μπορώ να αναζητήσω υπογραφές κειμένου σε έγγραφα που προστατεύονται με κωδικό πρόσβασης;

Ναι, το GroupDocs.Signature υποστηρίζει την αναζήτηση υπογραφών κειμένου σε έγγραφα που προστατεύονται με κωδικό πρόσβασης. Μπορείτε να δώσετε τον κωδικό πρόσβασης κατά την αρχικοποίηση του `Signature` αντικείμενο:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Αναζήτηση για υπογραφές κειμένου
}
```

### Ποιες μορφές εγγράφων υποστηρίζονται για αναζήτηση υπογραφής κειμένου;

Το GroupDocs.Signature υποστηρίζει ένα ευρύ φάσμα μορφών εγγράφων, όπως PDF, έγγραφα του Microsoft Office (Word, Excel, PowerPoint), μορφές OpenOffice, εικόνες και άλλα.

### Μπορώ να αναζητήσω υπογραφές κειμένου με συγκεκριμένη μορφοποίηση, όπως έντονη ή πλάγια γραφή;

Ναι, μπορείτε να αναζητήσετε υπογραφές κειμένου με συγκεκριμένη μορφοποίηση χρησιμοποιώντας το `FontBold` και `FontItalic` ακίνητα σε `TextSearchOptions`:

```csharp
TextSearchOptions options = new TextSearchOptions
{
    FontBold = true,
    FontItalic = true
};
```

### Πώς μπορώ να βελτιώσω την απόδοση αναζήτησης για μεγάλα έγγραφα;

Για μεγάλα έγγραφα, μπορείτε να βελτιστοποιήσετε την απόδοση αναζήτησης ως εξής:

1. Περιορισμός της αναζήτησης σε συγκεκριμένες σελίδες αντί για αναζήτηση σε ολόκληρο το έγγραφο
2. Χρήση πιο συγκεκριμένων κριτηρίων αναζήτησης για μείωση του αριθμού των αντιστοιχίσεων
3. Καθορισμός περιοχής αναζήτησης χρησιμοποιώντας το `Rectangle` ιδιοκτησίας εάν γνωρίζετε πού βρίσκονται συνήθως οι υπογραφές
4. Εφαρμογή σελιδοποίησης στην εφαρμογή σας για την επεξεργασία αποτελεσμάτων αναζήτησης σε παρτίδες

### Μπορώ να εντοπίσω εάν μια υπογραφή κειμένου προστέθηκε ηλεκτρονικά ή αποτελεί μέρος του αρχικού περιεχομένου του εγγράφου;

Το GroupDocs.Signature μπορεί να διακρίνει μεταξύ διαφορετικών τύπων στοιχείων κειμένου σε έγγραφα. `SignatureImplementation` ιδιοκτησία του `TextSignature` υποδεικνύει εάν το κείμενο είναι επίσημη υπογραφή ή κανονικό περιεχόμενο εγγράφου. Ωστόσο, η οριστική απόφαση μπορεί να εξαρτάται από τον τρόπο με τον οποίο το κείμενο προστέθηκε αρχικά στο έγγραφο.

## Δείτε επίσης

* [Αναφορά API](https://reference.groupdocs.com/signature/net/)
* [Παραδείγματα κώδικα στο GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Τεκμηρίωση προϊόντος](https://docs.groupdocs.com/signature/net/)
* [Σελίδα προϊόντος](https://products.groupdocs.com/signature/net/)
* [Λήψη τελευταίας έκδοσης](https://releases.groupdocs.com/signature/net/)
* [Άρθρα ιστολογίου](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Δωρεάν Φόρουμ Υποστήριξης](https://forum.groupdocs.com/c/signature/13)
* [Προσωρινή Άδεια](https://purchase.groupdocs.com/temporary-license/)