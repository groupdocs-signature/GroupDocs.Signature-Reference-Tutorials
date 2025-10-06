---
"description": "Εξασκηθείτε στην αναζήτηση ψηφιακών υπογραφών σε έγγραφα με το GroupDocs.Signature για .NET. Βελτιώστε την ασφάλεια και την επαλήθευση εγγράφων με τον λεπτομερή οδηγό μας βήμα προς βήμα."
"linktitle": "Αναζήτηση για Ψηφιακές Υπογραφές"
"second_title": "API GroupDocs.Signature .NET"
"title": "Αναζήτηση ψηφιακών υπογραφών σε έγγραφα"
"url": "/el/net/signature-searching/search-for-digital-signatures/"
"weight": 11
type: docs
---
## Εισαγωγή

Στο σημερινό ψηφιακό τοπίο, η διασφάλιση της αυθεντικότητας και της ακεραιότητας των εγγράφων είναι κρίσιμη για τις επιχειρήσεις και τους οργανισμούς. Οι ψηφιακές υπογραφές παρέχουν έναν ισχυρό μηχανισμό για την επαλήθευση της αυθεντικότητας των εγγράφων και την ανίχνευση μη εξουσιοδοτημένων τροποποιήσεων. Το GroupDocs.Signature για .NET προσφέρει μια ολοκληρωμένη λύση για την εργασία με ψηφιακές υπογραφές σε διάφορες μορφές εγγράφων, επιτρέποντας στους προγραμματιστές να ενσωματώνουν απρόσκοπτα τη λειτουργικότητα υπογραφών στις εφαρμογές .NET τους.

Αυτό το σεμινάριο θα σας καθοδηγήσει στη διαδικασία αναζήτησης ψηφιακών υπογραφών σε έγγραφα χρησιμοποιώντας το GroupDocs.Signature για .NET, παρέχοντας λεπτομερείς εξηγήσεις και πρακτικά παραδείγματα κώδικα.

## Προαπαιτούμενα

Πριν προχωρήσετε στις λεπτομέρειες της υλοποίησης, βεβαιωθείτε ότι έχετε τις ακόλουθες προϋποθέσεις:

1. GroupDocs.Signature για .NET: Λήψη και εγκατάσταση της βιβλιοθήκης από [εδώ](https://releases.groupdocs.com/signature/net/).
   
2. Περιβάλλον Ανάπτυξης: Ρυθμίστε ένα περιβάλλον ανάπτυξης .NET με το Visual Studio ή το IDE της προτίμησής σας.
   
3. Δείγματα εγγράφων: Προετοιμάστε δείγματα εγγράφων που περιέχουν ψηφιακές υπογραφές για σκοπούς δοκιμών.

4. Βασικές Γνώσεις: Εξοικείωση με τη γλώσσα προγραμματισμού C# και τα βασικά στοιχεία του .NET framework.

## Εισαγωγή χώρων ονομάτων

Ξεκινήστε εισάγοντας τους απαιτούμενους χώρους ονομάτων για να αποκτήσετε πρόσβαση στη λειτουργικότητα που παρέχεται από το GroupDocs.Signature για .NET:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Τώρα, ας αναλύσουμε τη διαδικασία αναζήτησης ψηφιακών υπογραφών σε σαφή και διαχειρίσιμα βήματα:

## Βήμα 1: Αρχικοποίηση αντικειμένου υπογραφής

Ξεκινήστε δημιουργώντας μια παρουσία του `Signature` κλάση, περνώντας τη διαδρομή προς το έγγραφό σας:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Ο κώδικας για την αναζήτηση ψηφιακών υπογραφών θα προστεθεί εδώ
}
```

## Βήμα 2: Αναζήτηση ψηφιακών υπογραφών

Στη συνέχεια, χρησιμοποιήστε το `Search` μέθοδος με το `SignatureType.Digital` παράμετρος για αναζήτηση ψηφιακών υπογραφών στο έγγραφο:

```csharp
// Αναζήτηση ψηφιακών υπογραφών στο έγγραφο
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```

## Βήμα 3: Επεξεργασία και εμφάνιση αποτελεσμάτων

Τέλος, επεξεργαστείτε τα αποτελέσματα αναζήτησης και εμφανίστε σχετικές πληροφορίες σχετικά με τις ψηφιακές υπογραφές που βρέθηκαν:

```csharp
Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
foreach (var digitalSignature in signatures)
{
    Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
    Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
    Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
    Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
    Console.WriteLine();
}
```

## Πλήρες παράδειγμα

Ακολουθεί ένα πλήρες, λειτουργικό παράδειγμα που δείχνει πώς να αναζητήσετε ψηφιακές υπογραφές σε ένα έγγραφο:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SearchDigitalSignatures
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
                // Αναζήτηση ψηφιακών υπογραφών στο έγγραφο
                List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
                
                // Εμφάνιση αποτελεσμάτων αναζήτησης
                Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
                
                if (signatures.Count > 0)
                {
                    foreach (var digitalSignature in signatures)
                    {
                        Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
                        Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
                        Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
                        Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
                        Console.WriteLine();
                    }
                }
                else
                {
                    Console.WriteLine("No digital signatures found in the document.");
                }
            }
        }
    }
}
```

## Επιλογές σύνθετης αναζήτησης

Για πιο στοχευμένες αναζητήσεις, μπορείτε να χρησιμοποιήσετε `DigitalSearchOptions` για να προσαρμόσετε τα κριτήρια αναζήτησης:

```csharp
// Δημιουργήστε επιλογές ψηφιακής αναζήτησης
DigitalSearchOptions options = new DigitalSearchOptions()
{
    // Αναζήτηση μόνο σε συγκεκριμένες σελίδες (π.χ., σελίδες 1 και 2)
    PageNumber = 1,
    PagesSetup = new PagesSetup() { Pages = new List<int> { 1, 2 } },
    
    // Φιλτράρισμα με βάση τα σχόλια στις ψηφιακές υπογραφές
    Comments = "Approved",
    
    // Ορισμός εύρους ημερομηνίας και ώρας για αναζήτηση
    SignDateTimeFrom = new DateTime(2022, 1, 1),
    SignDateTimeTo = DateTime.Now
};

// Αναζήτηση με συγκεκριμένες επιλογές
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(options);
```

## Εργασία με πληροφορίες πιστοποιητικού

Οι ψηφιακές υπογραφές περιέχουν πολύτιμες πληροφορίες πιστοποιητικών στις οποίες μπορείτε να αποκτήσετε πρόσβαση και να τις επικυρώσετε:

```csharp
foreach (var digitalSignature in signatures)
{
    if (digitalSignature.Certificate != null)
    {
        // Ιδιότητες πιστοποιητικού πρόσβασης
        Console.WriteLine($"Certificate Valid From: {digitalSignature.Certificate.NotBefore}");
        Console.WriteLine($"Certificate Valid To: {digitalSignature.Certificate.NotAfter}");
        
        // Ελέγξτε εάν το πιστοποιητικό βρίσκεται σε έγκυρο εύρος ημερομηνιών
        bool isDateValid = DateTime.Now >= digitalSignature.Certificate.NotBefore && 
                          DateTime.Now <= digitalSignature.Certificate.NotAfter;
        
        Console.WriteLine($"Certificate Date Validity: {isDateValid}");
        
        // Στοιχεία εκδότη πιστοποιητικού πρόσβασης
        Console.WriteLine($"Certificate Issuer: {digitalSignature.Certificate.IssuerName}");
    }
}
```

## Σύναψη

Το GroupDocs.Signature για .NET παρέχει μια ισχυρή και ευέλικτη λύση για την αναζήτηση και την επικύρωση ψηφιακών υπογραφών σε έγγραφα. Σε αυτό το σεμινάριο, εξερευνήσαμε τη βήμα προς βήμα διαδικασία εφαρμογής της λειτουργικότητας αναζήτησης ψηφιακών υπογραφών σε εφαρμογές .NET, εξοπλίζοντάς σας με τις γνώσεις για την ενίσχυση της ασφάλειας και της επαλήθευσης ακεραιότητας των εγγράφων.

Αξιοποιώντας το GroupDocs.Signature, μπορείτε να δημιουργήσετε ισχυρά συστήματα διαχείρισης εγγράφων που διασφαλίζουν την αυθεντικότητα και την ακεραιότητα των ψηφιακών σας εγγράφων, ενισχύοντας την εμπιστοσύνη και τη συμμόρφωση στις επιχειρηματικές σας διαδικασίες.

## Συχνές ερωτήσεις

### Μπορεί το GroupDocs.Signature να επαληθεύσει την εγκυρότητα των ψηφιακών υπογραφών;

Ναι, το GroupDocs.Signature επικυρώνει αυτόματα τις ψηφιακές υπογραφές κατά τη διάρκεια της διαδικασίας αναζήτησης και παρέχει κατάσταση επικύρωσης μέσω του `IsValid` ιδιοκτησία του `DigitalSignature` τάξη.

### Ποιες μορφές εγγράφων υποστηρίζουν αναζήτηση με ψηφιακή υπογραφή;

Το GroupDocs.Signature υποστηρίζει αναζήτηση ψηφιακής υπογραφής σε διάφορες μορφές, όπως PDF, έγγραφα του Microsoft Office (Word, Excel, PowerPoint), μορφές OpenOffice και άλλα.

### Μπορώ να αναζητήσω ψηφιακές υπογραφές σε έγγραφα που προστατεύονται με κωδικό πρόσβασης;

Ναι, μπορείτε να αναζητήσετε ψηφιακές υπογραφές σε έγγραφα που προστατεύονται με κωδικό πρόσβασης, παρέχοντας τον κωδικό πρόσβασης κατά την αρχικοποίηση του `Signature` αντικείμενο:

```csharp
LoadOptions loadOptions = new LoadOptions() { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Αναζήτηση ψηφιακών υπογραφών
}
```

### Πώς μπορώ να επαληθεύσω εάν μια ψηφιακή υπογραφή δημιουργήθηκε από ένα συγκεκριμένο άτομο;

Μπορείτε να εξετάσετε το όνομα θέματος του πιστοποιητικού και άλλες ιδιότητες για να επαληθεύσετε την ταυτότητα του υπογράφοντος:

```csharp
foreach (var signature in signatures)
{
    if (signature.Certificate?.SubjectName?.Contains("John Doe") == true)
    {
        Console.WriteLine("Found signature by John Doe");
    }
}
```

### Μπορώ να εξαγάγω το δημόσιο κλειδί από ένα πιστοποιητικό ψηφιακής υπογραφής;

Ναι, μπορείτε να αποκτήσετε πρόσβαση στις πληροφορίες δημόσιου κλειδιού μέσω των ιδιοτήτων πιστοποιητικού:

```csharp
if (signature.Certificate != null)
{
    // Πρόσβαση σε πληροφορίες δημόσιου κλειδιού
    Console.WriteLine($"Public Key: {signature.Certificate.GetPublicKeyString()}");
}
```

## Δείτε επίσης

* [Αναφορά API](https://reference.groupdocs.com/signature/net/)
* [Παραδείγματα κώδικα](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Τεκμηρίωση προϊόντος](https://docs.groupdocs.com/signature/net/)
* [Σελίδα προϊόντος](https://products.groupdocs.com/signature/net/)
* [Λήψη τελευταίας έκδοσης](https://releases.groupdocs.com/signature/net/)
* [Άρθρα ιστολογίου](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Φόρουμ Υποστήριξης](https://forum.groupdocs.com/c/signature/13)
* [Προσωρινή Άδεια](https://purchase.groupdocs.com/temporary-license/)