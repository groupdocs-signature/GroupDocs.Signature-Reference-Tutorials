---
"date": "2025-05-07"
"description": "Μάθετε πώς να υπογράφετε εικόνες DICOM με κωδικούς QR χρησιμοποιώντας το GroupDocs.Signature για .NET. Αυτός ο οδηγός καλύπτει τη ρύθμιση, την εφαρμογή και την επαλήθευση υπογραφών κωδικών QR στην ιατρική απεικόνιση."
"title": "Πώς να υπογράψετε εικόνες DICOM με κωδικούς QR χρησιμοποιώντας το GroupDocs.Signature για .NET™; Ένας πλήρης οδηγός"
"url": "/el/net/qr-code-signatures/groupdocs-signature-net-dicom-images-qr-codes/"
"weight": 1
---

# Πώς να υπογράψετε εικόνες DICOM με κωδικούς QR χρησιμοποιώντας το GroupDocs.Signature για .NET: Ένας πλήρης οδηγός

Ψάχνετε για μια ασφαλή μέθοδο για την επαλήθευση της ταυτότητας των αρχείων DICOM σας; Αυτός ο λεπτομερής οδηγός θα σας δείξει πώς να χρησιμοποιήσετε το GroupDocs.Signature για .NET για την ενσωμάτωση υπογραφών κωδικού QR σε εικόνες DICOM. Ιδανικό για επαγγελματίες υγείας, προγραμματιστές και οποιονδήποτε εργάζεται με ψηφιακά ιατρικά έγγραφα, αυτό το σεμινάριο καλύπτει την εγκατάσταση έως την υλοποίηση.

## Τι θα μάθετε:
- Ρύθμιση του περιβάλλοντος ανάπτυξής σας με το GroupDocs.Signature για .NET.
- Οδηγίες βήμα προς βήμα για την υπογραφή εικόνων DICOM χρησιμοποιώντας κωδικούς QR.
- Μέθοδοι επαλήθευσης και αναζήτησης υπογραφών κωδικού QR σε αρχεία DICOM.
- Τεχνικές για τη δημιουργία προεπισκοπήσεων υπογεγραμμένων εγγράφων για σκοπούς αναθεώρησης.
- Βέλτιστες πρακτικές για τη βελτιστοποίηση της απόδοσης και την αποτελεσματική διαχείριση των πόρων.

Ας ξεκινήσουμε με τις προϋποθέσεις!

## Προαπαιτούμενα

Για να χρησιμοποιήσετε το GroupDocs.Signature για .NET, βεβαιωθείτε ότι το περιβάλλον σας είναι έτοιμο. Δείτε τι θα χρειαστείτε:

### Απαιτούμενες βιβλιοθήκες και εκδόσεις
- **GroupDocs.Signature για .NET**Διασφαλίστε τη συμβατότητα με το .NET framework σας.

### Απαιτήσεις Ρύθμισης Περιβάλλοντος
- Ένα περιβάλλον ανάπτυξης σε Windows ή Linux.
- Εγκατεστημένο Visual Studio ή άλλο .NET-συμβατό IDE.

### Προαπαιτούμενα Γνώσεων
- Βασική κατανόηση προγραμματισμού C#.
- Εξοικείωση με την είσοδο/έξοδο αρχείων σε εφαρμογές .NET.

## Ρύθμιση του GroupDocs.Signature για .NET

Εγκαταστήστε τη βιβλιοθήκη GroupDocs.Signature χρησιμοποιώντας την προτιμώμενη μέθοδο:

**Χρησιμοποιώντας το .NET CLI:**
```bash
dotnet add package GroupDocs.Signature
```

**Διαχειριστής πακέτων:**
```powershell
Install-Package GroupDocs.Signature
```

**Διεπαφή χρήστη του διαχειριστή πακέτων NuGet:**
- Αναζητήστε το "GroupDocs.Signature" και εγκαταστήστε την πιο πρόσφατη έκδοση.

### Απόκτηση Άδειας

Ξεκινήστε με μια δωρεάν δοκιμαστική περίοδο για να εξερευνήσετε τις δυνατότητες. Για εκτεταμένη χρήση, σκεφτείτε να αποκτήσετε μια προσωρινή ή πλήρη άδεια χρήσης από [GroupDocs](https://purchase.groupdocs.com/buy).

Μόλις εγκατασταθεί, αρχικοποιήστε τη βιβλιοθήκη:

```csharp
using GroupDocs.Signature;
// Αρχικοποιήστε το αντικείμενο Signature με τη διαδρομή του αρχείου DICOM.
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample.dicom");
```

## Οδηγός Εφαρμογής

### Υπογραφή εικόνας DICOM με κωδικό QR

#### Επισκόπηση
Προσθέστε υπογραφές κωδικού QR για να διασφαλίσετε την αυθεντικότητα και την ιχνηλασιμότητα των ιατρικών εγγράφων.

**Βήμα 1: Αρχικοποίηση αντικειμένου υπογραφής**

```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY\\sample.dicom";
using (Signature signature = new Signature(filePath))
{
    // Συνέχεια με τις λειτουργίες υπογραφής...
}
```

**Βήμα 2: Δημιουργία επιλογών υπογραφής κωδικού QR**

Ρυθμίστε τις παραμέτρους ιδιοτήτων όπως κείμενο, μέγεθος και στοίχιση.

```csharp
QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues")
{
    AllPages = true,
    Width = 100,
    Height = 100,
    VerticalAlignment = VerticalAlignment.Bottom,
    HorizontalAlignment = HorizontalAlignment.Right,
    Margin = new Padding() { Right = 5, Left = 5 }
};
```

**Βήμα 3: Προσθήκη μεταδεδομένων XMP**

Βελτιώστε το έγγραφο με πρόσθετα μεταδεδομένα.

```csharp
DicomSaveOptions dicomSaveOptions = new DicomSaveOptions()
{
    XmpEntries = new List<DicomXmpEntry>() { new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4") }
};
```

**Βήμα 4: Υπογράψτε το έγγραφο**

Εκτελέστε την υπογραφή και αποθηκεύστε.

```csharp
SignResult signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY\\SignedDicom", options, dicomSaveOptions);
```

### Λήψη πληροφοριών εγγράφου

Ανάκτηση μεταδεδομένων από υπογεγραμμένα αρχεία DICOM για διασφάλιση της ακεραιότητας των δεδομένων.

**Επισκόπηση:**
Πρόσβαση σε πληροφορίες εγγράφων και υπογραφές μεταδεδομένων XMP για επαλήθευση.

**Βήμα 1: Ανάκτηση πληροφοριών εγγράφου**

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    IDocumentInfo signedDocumentInfo = signature.GetDocumentInfo();
}
```

**Βήμα 2: Επανάληψη και εκτύπωση δεδομένων XMP**

Εμφάνιση λεπτομερειών μεταδεδομένων.

```csharp
foreach (var item in signedDocumentInfo.MetadataSignatures)
{
    Console.WriteLine(item.ToString());
}
```

### Επαλήθευση υπογραφών DICOM

Επικυρώστε την αυθεντικότητα των υπογραφών κωδικών QR σε εικόνες DICOM.

**Επισκόπηση:**
Βεβαιωθείτε ότι οι υπογραφές είναι σωστές και αυθεντικές.

**Βήμα 1: Δημιουργία επιλογών επαλήθευσης κωδικού QR**

Ορίστε επιλογές που ταιριάζουν με συγκεκριμένο κείμενο στους κωδικούς QR.

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true,
    Text = "Patient #36363393",
    MatchType = TextMatchType.Contains
};
```

**Βήμα 2: Επαλήθευση υπογραφών**

Ελέγξτε αν οι υπογραφές πληρούν τα κριτήρια.

```csharp
VerificationResult result = signature.Verify(options);

if (result.IsValid)
{
    Console.WriteLine($"DICOM {filePath} has {result.Succeeded.Count} successfully verified signatures!");
}
```

### Αναζήτηση υπογραφών στο DICOM

Εντοπίστε υπογραφές κωδικών QR μέσα σε υπογεγραμμένες εικόνες DICOM.

**Επισκόπηση:**
Βρείτε αποτελεσματικά όλες τις υπογραφές κωδικών QR για να διαχειριστείτε την αυθεντικότητα των εγγράφων.

**Βήμα 1: Αναζήτηση υπογραφών κωδικού QR**

```csharp
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

**Βήμα 2: Επαναλάβετε και εκτυπώστε λεπτομέρειες υπογραφής**

Ελέγξτε τις λεπτομέρειες κάθε υπογραφής που βρέθηκε.

```csharp
foreach (var QrCodeSignature in signatures)
{
    Console.WriteLine($"QRCode signature found at page {QrCodeSignature.PageNumber} with type {QrCodeSignature.EncodeType.TypeName} and text {QrCodeSignature.Text}");
}
```

### Δημιουργία προεπισκόπησης υπογεγραμμένου DICOM

Δημιουργήστε οπτικές προεπισκοπήσεις για επαλήθευση.

**Επισκόπηση:**
Δημιουργήστε προεπισκοπήσεις εικόνων για να επαληθεύσετε το περιεχόμενο χωρίς εξειδικευμένο λογισμικό.

**Βήμα 1: Ορισμός μεθόδων ροής**

Ορίστε μεθόδους για τη διαχείριση ροής αρχείων κατά τη δημιουργία προεπισκόπησης.

```csharp
Stream CreatePageStream(PreviewPageData pageData)
{
    string imageFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignDicomImageAdvanced", $"preview-{pageData.PageNumber}.jpg");
    var folder = Path.GetDirectoryName(imageFilePath);
    if (!Directory.Exists(folder))
    {
        Directory.CreateDirectory(folder);
    }
    return new FileStream(imageFilePath, FileMode.Create);
}

void ReleasePageStream(PreviewPageData pageData, Stream pageStream)
{
    pageStream.Dispose();
}
```

**Βήμα 2: Δημιουργία προεπισκοπήσεων**

Εκτελέστε τη διαδικασία δημιουργίας προεπισκόπησης.

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    PreviewOptions previewOption = new PreviewOptions(CreatePageStream, ReleasePageStream)
    {
        PreviewFormat = PreviewOptions.PreviewFormats.PNG,
    };

    signature.GeneratePreview(previewOption);
}
```

## Πρακτικές Εφαρμογές

1. **Διαχείριση Ιατρικών Αρχείων**: Επαληθεύστε τα αρχεία ασθενών χρησιμοποιώντας υπογραφές κωδικού QR για συμμόρφωση.
2. **Διαδρομές Ελέγχου σε Συστήματα Υγειονομικής Περίθαλψης**Παρακολουθήστε τις αλλαγές στα έγγραφα και επαληθεύστε την αυθεντικότητά τους με κωδικούς QR.
3. **Ασφαλής κοινή χρήση δεδομένων**Διασφάλιση ασφαλούς κοινής χρήσης ιατρικών εικόνων με την ενσωμάτωση ψηφιακών υπογραφών.
4. **Επαλήθευση συμμόρφωσης**Ελέγχετε τακτικά την ακεραιότητα του αρχείου DICOM για να πληροίτε τις νομικές απαιτήσεις.
5. **Ενσωμάτωση με συστήματα ΗΜΥ**: Ομαλή ενσωμάτωση υπογεγραμμένων αρχείων DICOM σε συστήματα Ηλεκτρονικών Αρχείων Υγείας (EHR) για βελτιστοποιημένες λειτουργίες.