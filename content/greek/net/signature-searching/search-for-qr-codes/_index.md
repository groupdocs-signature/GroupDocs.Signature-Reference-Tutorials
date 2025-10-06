---
"description": "Μάθετε πώς να αναζητάτε αποτελεσματικά κωδικούς QR σε έγγραφα χρησιμοποιώντας το GroupDocs.Signature για .NET με αυτόν τον ολοκληρωμένο οδηγό βήμα προς βήμα και παραδείγματα κώδικα."
"linktitle": "Αναζήτηση κωδικών QR"
"second_title": "API GroupDocs.Signature .NET"
"title": "Αναζήτηση υπογραφών κωδικού QR σε έγγραφα"
"url": "/el/net/signature-searching/search-for-qr-codes/"
"weight": 15
type: docs
---
## Εισαγωγή

Στο σημερινό οικοσύστημα ψηφιακών εγγράφων, οι υπογραφές κωδικών QR έχουν γίνει ένα ανεκτίμητο εργαλείο για την ενσωμάτωση πληροφοριών, την επαλήθευση ταυτότητας και την ενίσχυση της ασφάλειας των εγγράφων. Το GroupDocs.Signature για .NET παρέχει στους προγραμματιστές ένα ισχυρό API για την αναζήτηση και εξαγωγή κωδικών QR από διάφορες μορφές εγγράφων, επιτρέποντας προηγμένες δυνατότητες ανάλυσης και επαλήθευσης εγγράφων σε εφαρμογές .NET.

Αυτό το ολοκληρωμένο σεμινάριο θα σας καθοδηγήσει στη διαδικασία υλοποίησης της λειτουργικότητας αναζήτησης κωδικού QR χρησιμοποιώντας το GroupDocs.Signature για .NET, παρέχοντας σαφείς εξηγήσεις, οδηγίες βήμα προς βήμα και πρακτικά παραδείγματα κώδικα που μπορείτε να ενσωματώσετε στις δικές σας εφαρμογές.

## Προαπαιτούμενα

Πριν ξεκινήσετε την αναζήτηση υπογραφής με κωδικό QR, βεβαιωθείτε ότι έχετε τις ακόλουθες προϋποθέσεις:

1. GroupDocs.Signature για .NET SDK: Λήψη και εγκατάσταση του SDK από το [σελίδα λήψης](https://releases.groupdocs.com/signature/net/).

2. Περιβάλλον Ανάπτυξης: Ρυθμίστε ένα περιβάλλον ανάπτυξης .NET, όπως το Visual Studio, με εγκατεστημένο το .NET Framework ή το .NET Core.

3. Βασικές Γνώσεις: Εξοικείωση με τον προγραμματισμό C# και τις έννοιες ανάπτυξης .NET.

4. Δείγματα εγγράφων: Προετοιμάστε έγγραφα δοκιμών που περιέχουν κωδικούς QR για επαλήθευση και δοκιμή.

## Εισαγωγή χώρων ονομάτων

Ξεκινήστε εισάγοντας τους απαραίτητους χώρους ονομάτων για να αποκτήσετε πρόσβαση στη λειτουργικότητα του GroupDocs.Signature:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;
```

Τώρα, ας αναλύσουμε τη διαδικασία αναζήτησης κωδικών QR σε σαφή και εύκολα βήματα:

## Βήμα 1: Ορίστε τη διαδρομή εγγράφου

Αρχικά, καθορίστε τη διαδρομή προς το έγγραφο που περιέχει τους κωδικούς QR που θέλετε να αναζητήσετε:

```csharp
string filePath = "sample_multiple_signatures.docx";
```

## Βήμα 2: Αρχικοποίηση του αντικειμένου υπογραφής

Δημιουργήστε μια παρουσία του `Signature` κλάση περνώντας τη διαδρομή εγγράφου:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Ο κωδικός αναζήτησης QR θα προστεθεί εδώ
}
```

## Βήμα 3: Αναζήτηση υπογραφών κωδικού QR

Χρησιμοποιήστε το `Search` μέθοδο με τον κατάλληλο τύπο υπογραφής για να βρείτε κωδικούς QR στο έγγραφο:

```csharp
// Αναζήτηση υπογραφών κωδικού QR μέσα στο έγγραφο
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

## Βήμα 4: Επεξεργασία και εμφάνιση αποτελεσμάτων

Επαναλάβετε τις υπογραφές κωδικών QR που βρέθηκαν και αποκτήστε πρόσβαση στις ιδιότητές τους:

```csharp
// Εμφάνιση πληροφοριών σχετικά με τους κωδικούς QR που βρέθηκαν
Console.WriteLine($"\nSource document contains {signatures.Count} QR code signature(s):");

foreach (var qrCodeSignature in signatures)
{
    Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
    Console.WriteLine($"Content: {qrCodeSignature.Text}");
    Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
    Console.WriteLine();
}
```

## Πλήρες παράδειγμα

Ακολουθεί ένα ολοκληρωμένο παράδειγμα εργασίας που δείχνει την πλήρη διαδικασία αναζήτησης κωδικών QR σε ένα έγγραφο:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;

namespace QrCodeSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Διαδρομή εγγράφου - ενημέρωση με τη διαδρομή αρχείου σας
            string filePath = "sample_multiple_signatures.docx";
            
            // Αρχικοποίηση στιγμιότυπου υπογραφής
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Αναζήτηση υπογραφών κωδικού QR στο έγγραφο
                    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
                    
                    // Εμφάνιση αποτελεσμάτων αναζήτησης
                    Console.WriteLine($"\nSource document ['{filePath}'] contains {signatures.Count} QR code signature(s):");
                    
                    foreach (var qrCodeSignature in signatures)
                    {
                        Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
                        Console.WriteLine($"Content: {qrCodeSignature.Text}");
                        Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
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

## Προηγμένες Τεχνικές Αναζήτησης Κωδικών QR

### Αναζήτηση με συγκεκριμένα κριτήρια

Για πιο στοχευμένες αναζητήσεις, μπορείτε να χρησιμοποιήσετε `QrCodeSearchOptions` για να προσαρμόσετε τα κριτήρια αναζήτησής σας:

```csharp
// Δημιουργήστε επιλογές αναζήτησης κωδικού QR με συγκεκριμένα κριτήρια
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    // Αναζήτηση μόνο σε συγκεκριμένες σελίδες
    AllPages = false,
    PageNumber = 1,
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // Φιλτράρισμα κατά περιεχόμενο κωδικού QR
    Text = "Invoice",
    MatchType = TextMatchType.Contains,
    
    // Φιλτράρισμα κατά συγκεκριμένους τύπους κωδικών QR
    EncodeType = QrCodeTypes.QR,
    
    // Ορίστε μια συγκεκριμένη περιοχή για αναζήτηση
    Rectangle = new Rectangle(100, 100, 400, 400)
};

// Αναζήτηση με συγκεκριμένες επιλογές
List<QrCodeSignature> filteredSignatures = signature.Search<QrCodeSignature>(options);
```

### Επεξεργασία δεδομένων κωδικού QR

Μπορείτε να εφαρμόσετε προσαρμοσμένη επεξεργασία για δεδομένα κωδικού QR με βάση τις απαιτήσεις της εφαρμογής σας:

```csharp
foreach (var qrCode in signatures)
{
    // Εξαγωγή και επεξεργασία δεδομένων κωδικού QR με βάση το περιεχόμενο
    string qrContent = qrCode.Text;
    
    if (qrContent.StartsWith("URL:"))
    {
        // Επεξεργασία δεδομένων URL
        string url = qrContent.Substring(4);
        Console.WriteLine($"Found URL in QR code: {url}");
    }
    else if (qrContent.StartsWith("CONTACT:"))
    {
        // Στοιχεία επικοινωνίας επεξεργασίας
        string contact = qrContent.Substring(8);
        Console.WriteLine($"Found contact information in QR code: {contact}");
    }
    else if (qrContent.StartsWith("INVOICE:"))
    {
        // Επεξεργασία πληροφοριών τιμολογίου
        string invoiceData = qrContent.Substring(8);
        Console.WriteLine($"Found invoice information in QR code: {invoiceData}");
        
        // Ανάλυση και επικύρωση δεδομένων τιμολογίου
        if (ValidateInvoiceData(invoiceData))
        {
            Console.WriteLine("Invoice data is valid!");
        }
        else
        {
            Console.WriteLine("Warning: Invalid invoice data detected!");
        }
    }
}

// Παράδειγμα μεθόδου επικύρωσης
static bool ValidateInvoiceData(string data)
{
    // Εφαρμόστε τη λογική επικύρωσης
    return !string.IsNullOrEmpty(data) && data.Contains("ID") && data.Contains("Amount");
}
```

### Εφαρμογή επαλήθευσης ασφαλείας

Οι κωδικοί QR χρησιμοποιούνται συχνά για σκοπούς ελέγχου ταυτότητας. Δείτε πώς μπορείτε να εφαρμόσετε βασική επαλήθευση ασφαλείας:

```csharp
// Ελέγξτε εάν το έγγραφο περιέχει έγκυρο κωδικό QR ελέγχου ταυτότητας
bool hasValidAuthQrCode = false;

foreach (var qrCode in signatures)
{
    if (qrCode.Text.StartsWith("AUTH:"))
    {
        string authCode = qrCode.Text.Substring(5);
        
        // Επαλήθευση κωδικού ελέγχου ταυτότητας (π.χ., σε σχέση με μια βάση δεδομένων ή μια προκαθορισμένη λίστα)
        if (VerifyAuthCode(authCode))
        {
            hasValidAuthQrCode = true;
            Console.WriteLine("Document contains valid authentication QR code!");
            break;
        }
    }
}

if (!hasValidAuthQrCode)
{
    Console.WriteLine("Warning: Document does not contain a valid authentication QR code!");
}

// Παράδειγμα μεθόδου επαλήθευσης
static bool VerifyAuthCode(string code)
{
    // Εφαρμόστε τη λογική επαλήθευσης
    // Αυτό θα μπορούσε να είναι μια αναζήτηση βάσης δεδομένων, μια κλήση API ή μια σύγκριση με προκαθορισμένες τιμές
    return code == "A7B82C3D" || code == "X9Y8Z7W6";
}
```

### Εξαγωγή εικόνων κωδικού QR

Μπορείτε να εξαγάγετε εικόνες κωδικού QR από έγγραφα για περαιτέρω επεξεργασία ή προβολή:

```csharp
// Αποθήκευση εικόνων κωδικού QR στο δίσκο
foreach (var qrCode in signatures)
{
    if (qrCode.Content != null)
    {
        // Δημιουργήστε ένα μοναδικό όνομα αρχείου με βάση τον αριθμό σελίδας και τη θέση
        string outputPath = $"QrCode_P{qrCode.PageNumber}_X{qrCode.Left}_Y{qrCode.Top}.png";
        
        // Αποθήκευση δεδομένων εικόνας
        File.WriteAllBytes(outputPath, qrCode.Content);
        Console.WriteLine($"Saved QR code image to {outputPath}");
    }
}
```

## Σύναψη

Σε αυτόν τον ολοκληρωμένο οδηγό, εξερευνήσαμε τον τρόπο αναζήτησης υπογραφών κωδικών QR σε έγγραφα χρησιμοποιώντας το GroupDocs.Signature για .NET. Από βασική αναζήτηση έως προηγμένες τεχνικές, τώρα έχετε τις γνώσεις για να εφαρμόσετε ισχυρό χειρισμό κωδικών QR στις εφαρμογές .NET σας. Το GroupDocs.Signature API παρέχει ένα ισχυρό, ευέλικτο πλαίσιο για την εργασία με διάφορους τύπους υπογραφών, συμπεριλαμβανομένων κωδικών QR, σε διαφορετικές μορφές εγγράφων.

Αξιοποιώντας αυτές τις δυνατότητες, μπορείτε να βελτιώσετε τις διαδικασίες επαλήθευσης εγγράφων, να εφαρμόσετε συστήματα ελέγχου ταυτότητας και να εξαγάγετε πολύτιμες πληροφορίες ενσωματωμένες σε κωδικούς QR, όλα μέσα στις εφαρμογές .NET σας.

## Συχνές ερωτήσεις

### Ποιες μορφές κωδικού QR υποστηρίζονται από το GroupDocs.Signature;

Το GroupDocs.Signature υποστηρίζει διάφορες μορφές κωδικών QR, συμπεριλαμβανομένων των τυπικών κωδικών QR, των κωδικών Micro QR και άλλων κοινών προτύπων κωδικών QR. Η συγκεκριμένη μορφή είναι προσβάσιμη μέσω του `EncodeType` ιδιοκτησία του `QrCodeSignature` αντικείμενο.

### Μπορώ να αναζητήσω κωδικούς QR σε έγγραφα που προστατεύονται με κωδικό πρόσβασης;

Ναι, το GroupDocs.Signature υποστηρίζει την αναζήτηση κωδικών QR σε έγγραφα που προστατεύονται με κωδικό πρόσβασης, παρέχοντας τον κωδικό πρόσβασης κατά την αρχικοποίηση του `Signature` αντικείμενο:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Αναζήτηση κωδικών QR
}
```

### Πώς μπορώ να φιλτράρω τους κωδικούς QR με βάση το περιεχόμενό τους;

Μπορείτε να φιλτράρετε τους κωδικούς QR με βάση το περιεχόμενό τους χρησιμοποιώντας το `Text` και `MatchType` ιδιότητες του `QrCodeSearchOptions`:

```csharp
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    Text = "Invoice",
    MatchType = TextMatchType.Contains // Άλλες επιλογές: Ακριβής, Αρχίζει με, Λήγει με
};
```

### Μπορεί το GroupDocs.Signature να εντοπίσει κατεστραμμένους ή μερικώς ορατούς κωδικούς QR;

Το GroupDocs.Signature έχει κάποια δυνατότητα ανίχνευσης μερικώς ορατών κωδικών QR, αλλά οι κωδικοί QR που είναι πολύ κατεστραμμένοι ενδέχεται να μην αναγνωρίζονται. Η ακρίβεια ανίχνευσης εξαρτάται από την ποιότητα και την ορατότητα του κωδικού QR στο έγγραφο.

### Ποιες μορφές εγγράφων υποστηρίζονται για αναζήτηση με κωδικό QR;

Το GroupDocs.Signature υποστηρίζει αναζήτηση κωδικών QR σε διάφορες μορφές εγγράφων, όπως PDF, έγγραφα του Microsoft Office (Word, Excel, PowerPoint), εικόνες (JPEG, PNG, TIFF) και πολλά άλλα.

## Δείτε επίσης

* [Αναφορά API](https://reference.groupdocs.com/signature/net/)
* [Παραδείγματα κώδικα στο GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Τεκμηρίωση προϊόντος](https://docs.groupdocs.com/signature/net/)
* [Σελίδα προϊόντος](https://products.groupdocs.com/signature/net/)
* [Λήψη τελευταίας έκδοσης](https://releases.groupdocs.com/signature/net/)
* [Άρθρα ιστολογίου](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Δωρεάν Φόρουμ Υποστήριξης](https://forum.groupdocs.com/c/signature/13)
* [Προσωρινή Άδεια](https://purchase.groupdocs.com/temporary-license/)