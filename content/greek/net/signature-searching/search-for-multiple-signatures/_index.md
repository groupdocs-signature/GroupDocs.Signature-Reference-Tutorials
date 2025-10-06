---
"description": "Μάθετε πώς να αναζητάτε πολλαπλούς τύπους υπογραφών σε έγγραφα χρησιμοποιώντας το GroupDocs.Signature για .NET. Πλήρης οδηγός με παραδείγματα κώδικα για βελτιωμένη ασφάλεια εγγράφων."
"linktitle": "Αναζήτηση για πολλαπλές υπογραφές"
"second_title": "API GroupDocs.Signature .NET"
"title": "Αναζήτηση πολλαπλών τύπων υπογραφών σε έγγραφα"
"url": "/el/net/signature-searching/search-for-multiple-signatures/"
"weight": 14
type: docs
---
## Εισαγωγή

Στα σύγχρονα συστήματα διαχείρισης εγγράφων, η δυνατότητα αναζήτησης και επικύρωσης πολλαπλών τύπων υπογραφών μέσα σε ένα μόνο έγγραφο αποκτά ολοένα και μεγαλύτερη σημασία. Οι οργανισμοί συχνά χρησιμοποιούν διάφορους τύπους υπογραφών — όπως ψηφιακές υπογραφές, υπογραφές κειμένου, γραμμωτούς κώδικες, κωδικούς QR και άλλα — για να βελτιώσουν την ασφάλεια των εγγράφων και να βελτιστοποιήσουν τις διαδικασίες επαλήθευσης. Το GroupDocs.Signature για .NET παρέχει ένα ισχυρό πλαίσιο που επιτρέπει στους προγραμματιστές να εφαρμόσουν ολοκληρωμένη λειτουργικότητα αναζήτησης υπογραφών σε διάφορες μορφές εγγράφων.

Αυτό το σεμινάριο θα σας καθοδηγήσει στη διαδικασία αναζήτησης πολλαπλών τύπων υπογραφών σε έγγραφα χρησιμοποιώντας το GroupDocs.Signature για .NET, προσφέροντας λεπτομερείς εξηγήσεις και πρακτικά παραδείγματα κώδικα.

## Προαπαιτούμενα

Πριν ξεκινήσετε την εφαρμογή της λειτουργίας αναζήτησης πολλαπλών υπογραφών, βεβαιωθείτε ότι έχετε τις ακόλουθες προϋποθέσεις:

1. Περιβάλλον Ανάπτυξης: Visual Studio ή οποιοδήποτε προτιμώμενο περιβάλλον ανάπτυξης .NET που είναι εγκατεστημένο στο σύστημά σας.
  
2. GroupDocs.Signature for .NET: Κατεβάστε και εγκαταστήστε τη βιβλιοθήκη GroupDocs.Signature for .NET από [εδώ](https://releases.groupdocs.com/signature/net/).

3. Βασικές γνώσεις C#: Εξοικείωση με τη γλώσσα προγραμματισμού C# και τις έννοιες του .NET framework.

4. Δείγματα εγγράφων: Προετοιμάστε έγγραφα δοκιμών που περιέχουν διάφορους τύπους υπογραφών για σκοπούς δοκιμών.

## Εισαγωγή χώρων ονομάτων

Ξεκινήστε εισάγοντας τους απαραίτητους χώρους ονομάτων για να αποκτήσετε πρόσβαση στη λειτουργικότητα του GroupDocs.Signature:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Τώρα, ας αναλύσουμε τη διαδικασία αναζήτησης πολλαπλών τύπων υπογραφών σε σαφή και διαχειρίσιμα βήματα:

## Βήμα 1: Φόρτωση του εγγράφου

Αρχικά, φορτώστε το έγγραφο που περιέχει τις υπογραφές που θέλετε να αναζητήσετε:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Ο κώδικας αναζήτησης πολλαπλών υπογραφών θα προστεθεί εδώ
}
```

## Βήμα 2: Ορισμός επιλογών αναζήτησης για διαφορετικούς τύπους υπογραφής

Δημιουργήστε επιλογές αναζήτησης για κάθε τύπο υπογραφής που θέλετε να αναζητήσετε:

```csharp
// Ορισμός επιλογών αναζήτησης για υπογραφές κειμένου
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,  // Αναζήτηση σε όλες τις σελίδες
    Text = "Signature",  // Προαιρετικά: κείμενο προς εύρεση
    MatchType = TextMatchType.Contains  // Κριτήρια αντιστοίχισης
};

// Ορισμός επιλογών αναζήτησης για ψηφιακές υπογραφές
DigitalSearchOptions digitalOptions = new DigitalSearchOptions
{
    AllPages = true
};

// Ορισμός επιλογών αναζήτησης για υπογραφές γραμμωτού κώδικα
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
{
    AllPages = true,
    Text = "123456",  // Προαιρετικά: κείμενο γραμμωτού κώδικα που ταιριάζει με το κείμενο του γραμμωτού κώδικα.
    MatchType = TextMatchType.Exact  // Κριτήρια αντιστοίχισης
};

// Ορισμός επιλογών αναζήτησης για υπογραφές κωδικού QR
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
{
    AllPages = true,
    Text = "John",  // Προαιρετικά: Κείμενο κωδικού QR που ταιριάζει
    MatchType = TextMatchType.Contains  // Κριτήρια αντιστοίχισης
};

// Ορισμός επιλογών αναζήτησης για υπογραφές μεταδεδομένων
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```

## Βήμα 3: Προσθήκη επιλογών σε μια συλλογή

Προσθήκη όλων των επιλογών αναζήτησης σε μια συλλογή:

```csharp
// Δημιουργήστε μια λίστα που να περιέχει όλες τις επιλογές αναζήτησης
List<SearchOptions> searchOptions = new List<SearchOptions>
{
    textOptions,
    digitalOptions,
    barcodeOptions,
    qrCodeOptions,
    metadataOptions
};
```

## Βήμα 4: Εκτελέστε την αναζήτηση και επεξεργαστείτε τα αποτελέσματα

Εκτελέστε την αναζήτηση χρησιμοποιώντας τις συνδυασμένες επιλογές αναζήτησης και επεξεργαστείτε τα αποτελέσματα:

```csharp
// Αναζήτηση όλων των τύπων υπογραφής χρησιμοποιώντας τις καθορισμένες επιλογές
SearchResult result = signature.Search(searchOptions);

// Ελέγξτε αν βρέθηκαν υπογραφές
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
    
    // Επαναλάβετε τις υπογραφές που βρέθηκαν
    foreach (var foundSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}, ID: {foundSignature.SignatureId}");
        
        // Τύποι υπογραφών για συγκεκριμένες διεργασίες
        if (foundSignature is TextSignature textSignature)
        {
            Console.WriteLine($"Text: '{textSignature.Text}'");
        }
        else if (foundSignature is BarcodeSignature barcodeSignature)
        {
            Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
        }
        else if (foundSignature is QrCodeSignature qrCodeSignature)
        {
            Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
        }
        else if (foundSignature is DigitalSignature digitalSignature)
        {
            Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
        }
        else if (foundSignature is MetadataSignature metadataSignature)
        {
            Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
        }
    }
}
else
{
    Console.WriteLine("No signatures were found in the document.");
}
```

## Πλήρες παράδειγμα

Ακολουθεί ένα πλήρες, λειτουργικό παράδειγμα που δείχνει την αναζήτηση πολλαπλών τύπων υπογραφής σε ένα έγγραφο:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace MultiSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Διαδρομή εγγράφου
            string filePath = "sample_multiple_signatures.docx";
            
            // Αρχικοποίηση στιγμιότυπου υπογραφής
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Ορισμός επιλογών αναζήτησης για υπογραφές κειμένου
                    TextSearchOptions textOptions = new TextSearchOptions
                    {
                        AllPages = true,
                        MatchType = TextMatchType.Contains
                    };

                    // Ορισμός επιλογών αναζήτησης για ψηφιακές υπογραφές
                    DigitalSearchOptions digitalOptions = new DigitalSearchOptions
                    {
                        AllPages = true
                    };

                    // Ορισμός επιλογών αναζήτησης για υπογραφές γραμμωτού κώδικα
                    BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Ορισμός επιλογών αναζήτησης για υπογραφές κωδικού QR
                    QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Ορισμός επιλογών αναζήτησης για υπογραφές μεταδεδομένων
                    MetadataSearchOptions metadataOptions = new MetadataSearchOptions();

                    // Δημιουργήστε μια λίστα που να περιέχει όλες τις επιλογές αναζήτησης
                    List<SearchOptions> searchOptions = new List<SearchOptions>
                    {
                        textOptions,
                        digitalOptions,
                        barcodeOptions,
                        qrCodeOptions,
                        metadataOptions
                    };

                    // Αναζήτηση για όλους τους τύπους υπογραφών
                    SearchResult result = signature.Search(searchOptions);

                    // Ελέγξτε αν βρέθηκαν υπογραφές
                    if (result.Signatures.Count > 0)
                    {
                        Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
                        
                        // Αποτελέσματα επεξεργασίας ανά τύπο υπογραφής
                        foreach (var foundSignature in result.Signatures)
                        {
                            Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}");
                            
                            // Τύποι υπογραφών για συγκεκριμένες διεργασίες
                            switch (foundSignature.SignatureType)
                            {
                                case SignatureType.Text:
                                    var textSignature = foundSignature as TextSignature;
                                    Console.WriteLine($"Text: '{textSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Barcode:
                                    var barcodeSignature = foundSignature as BarcodeSignature;
                                    Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.QrCode:
                                    var qrCodeSignature = foundSignature as QrCodeSignature;
                                    Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Digital:
                                    var digitalSignature = foundSignature as DigitalSignature;
                                    Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
                                    break;
                                    
                                case SignatureType.Metadata:
                                    var metadataSignature = foundSignature as MetadataSignature;
                                    Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
                                    break;
                            }
                            
                            Console.WriteLine(); // Προσθήκη αλλαγής γραμμής μεταξύ υπογραφών
                        }
                    }
                    else
                    {
                        Console.WriteLine("No signatures were found in the document.");
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

## Προηγμένες Τεχνικές Αναζήτησης Πολλαπλών Υπογραφών

### Φιλτράρισμα αποτελεσμάτων αναζήτησης

Μπορείτε να εφαρμόσετε προηγμένο φιλτράρισμα για να περιορίσετε τα αποτελέσματα αναζήτησης:

```csharp
// Φιλτράρισμα αποτελεσμάτων κατά αριθμό σελίδας
var signaturesOnFirstPage = result.Signatures.FindAll(s => s.PageNumber == 1);

// Φιλτράρισμα αποτελεσμάτων κατά τύπο υπογραφής
var digitalSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.Digital);
var qrCodeSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.QrCode);

// Φιλτράρισμα υπογραφών κειμένου που περιέχουν συγκεκριμένο περιεχόμενο
var approvalSignatures = result.Signatures
    .FindAll(s => s is TextSignature && ((TextSignature)s).Text.Contains("Approved"));
```

### Επικύρωση πολλαπλών υπογραφών

Υλοποίηση λογικής επικύρωσης για διαφορετικούς τύπους υπογραφών:

```csharp
bool ValidateAllSignatures(SearchResult result)
{
    bool isDocumentValid = true;
    
    // Ελέγξτε εάν το έγγραφο διαθέτει έγκυρη ψηφιακή υπογραφή
    bool hasValidDigitalSignature = result.Signatures
        .Any(s => s is DigitalSignature && ((DigitalSignature)s).IsValid);
    
    if (!hasValidDigitalSignature)
    {
        Console.WriteLine("Warning: Document does not contain a valid digital signature");
        isDocumentValid = false;
    }
    
    // Ελέγξτε εάν το έγγραφο απαιτεί κωδικό QR
    bool hasRequiredQRCode = result.Signatures
        .Any(s => s is QrCodeSignature && ((QrCodeSignature)s).Text.Contains("Auth-Code"));
    
    if (!hasRequiredQRCode)
    {
        Console.WriteLine("Warning: Document does not contain the required authentication QR code");
        isDocumentValid = false;
    }
    
    return isDocumentValid;
}
```

### Αναζήτηση με προσαρμοσμένη επεξεργασία

Μπορείτε να ορίσετε προσαρμοσμένη λογική επεξεργασίας για λειτουργίες αναζήτησης:

```csharp
// Δημιουργήστε επιλογές αναζήτησης με προσαρμοσμένη επεξεργασία
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,
    
    // Ορισμός προσαρμοσμένης επεξεργασίας χρησιμοποιώντας έναν εκπρόσωπο
    ProcessCompleted = (signature) =>
    {
        // Προσαρμοσμένη λογική επικύρωσης - αποδοχή μόνο υπογραφών σε συγκεκριμένες σελίδες
        TextSignature textSignature = signature as TextSignature;
        return textSignature != null && (textSignature.PageNumber == 1 || textSignature.PageNumber == 2);
    }
};
```

## Σύναψη

Σε αυτόν τον ολοκληρωμένο οδηγό, έχουμε εξερευνήσει τον τρόπο αναζήτησης για πολλαπλούς τύπους υπογραφών σε έγγραφα χρησιμοποιώντας το GroupDocs.Signature για .NET. Από τη ρύθμιση επιλογών αναζήτησης για διαφορετικούς τύπους υπογραφών έως την επεξεργασία και την επικύρωση των αποτελεσμάτων, πλέον έχετε τις γνώσεις για να εφαρμόσετε ισχυρή λειτουργικότητα αναζήτησης υπογραφών στις εφαρμογές .NET σας.

Η δυνατότητα ταυτόχρονης αναζήτησης πολλαπλών τύπων υπογραφών βελτιώνει τις διαδικασίες επαλήθευσης εγγράφων, ενισχύει τα μέτρα ασφαλείας και βελτιστοποιεί τις ροές εργασίας επικύρωσης εγγράφων. Το GroupDocs.Signature παρέχει ένα ισχυρό, ευέλικτο πλαίσιο για την εργασία με διάφορους τύπους υπογραφών σε διαφορετικές μορφές εγγράφων, καθιστώντας το μια εξαιρετική επιλογή για εφαρμογές επεξεργασίας εγγράφων.

## Συχνές ερωτήσεις

### Μπορώ να αναζητήσω υπογραφές σε έγγραφα που προστατεύονται με κωδικό πρόσβασης;

Ναι, το GroupDocs.Signature υποστηρίζει την αναζήτηση υπογραφών σε έγγραφα που προστατεύονται με κωδικό πρόσβασης. Μπορείτε να δώσετε τον κωδικό πρόσβασης κατά την αρχικοποίηση του `Signature` αντικείμενο:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Αναζήτηση υπογραφών
}
```

### Ποιες μορφές εγγράφων υποστηρίζονται για αναζήτηση υπογραφών;

Το GroupDocs.Signature υποστηρίζει ένα ευρύ φάσμα μορφών εγγράφων, όπως PDF, έγγραφα του Microsoft Office (Word, Excel, PowerPoint), μορφές OpenOffice, εικόνες και άλλα.

### Μπορώ να περιορίσω την αναζήτηση σε συγκεκριμένες σελίδες ενός εγγράφου;

Ναι, κάθε τύπος επιλογής αναζήτησης έχει ιδιότητες που σας επιτρέπουν να καθορίσετε σε ποιες σελίδες θα γίνει αναζήτηση:

```csharp
TextSearchOptions options = new TextSearchOptions
{
    AllPages = false,  // Μην κάνετε αναζήτηση σε όλες τις σελίδες
    PageNumber = 1,    // Αναζήτηση μόνο στη σελίδα 1
    
    // Ή καθορίστε πολλές σελίδες
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } }
};
```

### Πώς μπορώ να βελτιστοποιήσω την απόδοση κατά την αναζήτηση σε μεγάλα έγγραφα;

Για μεγάλα έγγραφα, μπορείτε να βελτιστοποιήσετε την απόδοση ως εξής:

1. Περιορισμός της αναζήτησης σε συγκεκριμένες σελίδες ή εύρη σελίδων
2. Χρήση πιο συγκεκριμένων κριτηρίων αναζήτησης για τη μείωση του αριθμού των πιθανών αντιστοιχίσεων
3. Εφαρμογή σελιδοποίησης στην εμφάνιση αποτελεσμάτων
4. Αναζήτηση για έναν τύπο υπογραφής κάθε φορά, εάν δεν χρειάζεστε ταυτόχρονα αποτελέσματα

### Μπορώ να επεκτείνω το GroupDocs.Signature για να υποστηρίξω προσαρμοσμένους τύπους υπογραφής;

Ενώ το GroupDocs.Signature παρέχει ενσωματωμένη υποστήριξη για κοινούς τύπους υπογραφών, μπορείτε να επεκτείνετε τη λειτουργικότητά του ως εξής:

1. Δημιουργία προσαρμοσμένων κλάσεων επιλογών αναζήτησης που προέρχονται από `SearchOptions`
2. Υλοποίηση προσαρμοσμένης λογικής επεξεργασίας χρησιμοποιώντας το `ProcessCompleted` αντιπρόσωπος
3. Ανάπτυξη κλάσεων περιτυλίγματος που συνδυάζουν πολλαπλές αναζητήσεις υπογραφών με προηγμένη επιχειρηματική λογική

## Δείτε επίσης

* [Αναφορά API](https://reference.groupdocs.com/signature/net/)
* [Παραδείγματα κώδικα στο GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Τεκμηρίωση προϊόντος](https://docs.groupdocs.com/signature/net/)
* [Σελίδα προϊόντος](https://products.groupdocs.com/signature/net/)
* [Λήψη τελευταίας έκδοσης](https://releases.groupdocs.com/signature/net/)
* [Άρθρα ιστολογίου](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Δωρεάν Φόρουμ Υποστήριξης](https://forum.groupdocs.com/c/signature/13)
* [Προσωρινή Άδεια](https://purchase.groupdocs.com/temporary-license/)