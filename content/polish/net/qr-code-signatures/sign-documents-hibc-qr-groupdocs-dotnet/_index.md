---
"date": "2025-05-07"
"description": "Dowiedz się, jak podpisywać dokumenty PDF kodami HIBC QR za pomocą GroupDocs.Signature dla platformy .NET. Ten przewodnik obejmuje kody LIC i PAS, w tym kody QR, Aztec i DataMatrix."
"title": "Jak podpisywać dokumenty kodami QR HIBC za pomocą GroupDocs.Signature dla platformy .NET? Kompleksowy przewodnik"
"url": "/pl/net/qr-code-signatures/sign-documents-hibc-qr-groupdocs-dotnet/"
"weight": 1
type: docs
---
# Jak podpisywać dokumenty kodami QR HIBC za pomocą GroupDocs.Signature dla platformy .NET

## Wstęp

W dzisiejszym dynamicznym środowisku biznesowym zapewnienie autentyczności i integralności dokumentów jest kwestią priorytetową. Niezależnie od tego, czy zajmujesz się produktami farmaceutycznymi, produktami medycznymi, czy logistyką, bezpieczna metoda podpisywania i śledzenia dokumentów może zaoszczędzić czas i zapobiec błędom. **GroupDocs.Signature dla .NET**, potężna biblioteka zaprojektowana w celu usprawnienia procesów zarządzania dokumentami poprzez umożliwienie bezproblemowej integracji kodów QR HIBC z dokumentami.

W tym samouczku pokażemy, jak wykorzystać GroupDocs.Signature dla platformy .NET do podpisywania dokumentów PDF różnymi typami kodów QR HIBC – LIC (licencja) i PAS (system uwierzytelniania produktów) – w tym kodami QR, Aztec Code i DataMatrix. Po ukończeniu kursu będziesz mieć solidną wiedzę na temat wdrażania tych rozwiązań w aplikacjach .NET.

**Czego się nauczysz:**
- Jak skonfigurować GroupDocs.Signature dla platformy .NET
- Wdrażanie kodów QR HIBC LIC, kodów Aztec i DataMatrix
- Dodawanie kodów QR HIBC PAS, kodów Aztec i DataMatrix
- Praktyczne przypadki użycia i możliwości integracji

Zanim zaczniemy wdrażać te funkcje, przyjrzyjmy się bliżej wymaganiom wstępnym.

## Wymagania wstępne

Zanim zaczniesz kodować, upewnij się, że masz przygotowane następujące rzeczy:

- **Środowisko .NET**Upewnij się, że na Twoim komputerze jest zainstalowany .NET (najlepiej .NET Core lub .NET 5/6+).
- **GroupDocs.Signature dla .NET**:Ta biblioteka będzie naszym podstawowym narzędziem. Można ją zainstalować za pomocą NuGet.
- **Podstawowa wiedza programistyczna**:Zalecana jest znajomość języka C# i obsługi plików w środowisku .NET.

### Wymagane biblioteki

Aby użyć GroupDocs.Signature dla .NET, należy dodać pakiet, korzystając z jednej z następujących metod:

**Interfejs wiersza poleceń .NET**
```bash
dotnet add package GroupDocs.Signature
```

**Menedżer pakietów**
```powershell
Install-Package GroupDocs.Signature
```

**Interfejs użytkownika Menedżera pakietów NuGet**
Wyszukaj „GroupDocs.Signature” i zainstaluj najnowszą wersję.

### Nabycie licencji

celach testowych możesz uzyskać bezpłatną licencję próbną. Aby korzystać z aplikacji dłużej, rozważ zakup subskrypcji lub złóż wniosek o licencję tymczasową:

- **Bezpłatny okres próbny**: Dostęp [Tutaj](https://releases.groupdocs.com/signature/net/)
- **Licencja tymczasowa**: Zapytaj na [ten link](https://purchase.groupdocs.com/temporary-license/)

### Konfiguracja środowiska

Skonfiguruj środowisko, upewniając się, że projekt jest skierowany na odpowiednią wersję platformy .NET i ma dostęp do GroupDocs.Signature. Zainicjuj go w swojej aplikacji, jak pokazano poniżej:

```csharp
using GroupDocs.Signature;
```

## Konfigurowanie GroupDocs.Signature dla platformy .NET

Aby rozpocząć korzystanie z GroupDocs.Signature dla .NET, należy zainstalować bibliotekę i skonfigurować podstawowe ustawienia w ramach projektu.

### Instalacja

Aby dodać GroupDocs.Signature do swojego projektu, zastosuj jedną z powyższych metod. Po zainstalowaniu upewnij się, że projekt jest skonfigurowany do korzystania z niego, odwołując się do niego w plikach kodu.

### Inicjalizacja licencji

Po nabyciu licencji zainicjuj ją w następujący sposób:

```csharp
SignatureConfig signConfig = new SignatureConfig();
signConfig.LicensePath = "path/to/your/license.lic";
Signature signature = new Signature("Sample.pdf", signConfig);
```

Ta konfiguracja umożliwi Ci dostęp do wszystkich funkcji GroupDocs.Signature bez ograniczeń.

## Przewodnik wdrażania

Teraz przyjrzyjmy się implementacji każdej funkcji przy użyciu kodów QR HIBC z GroupDocs.Signature dla .NET.

### Podpisz dokument kodem QR HIBC LIC

#### Przegląd

Podpisanie dokumentu kodem QR HIBC LIC zapewnia zgodność i identyfikowalność w scenariuszach licencjonowania. Ta sekcja przeprowadzi Cię przez proces tworzenia i osadzania kodu QR w dokumentach PDF.

#### Kroki wdrożenia

##### Krok 1: Skonfiguruj ścieżki źródłowe i wyjściowe

Zdefiniuj lokalizację dokumentu źródłowego i miejsce, w którym ma zostać zapisany podpisany dokument wyjściowy:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICQR.pdf");
```

##### Krok 2: Utwórz opcje podpisu kodem QR

Skonfiguruj swój kod QR, wprowadzając określony tekst i ustawienia:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_QR_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR)
    {
        Left = 1,
        Top = 1,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    // Podpisz dokument, korzystając z tych opcji.
    signature.Sign(destinFilePath, hibcLic_QR_Options);
}
```

**Wyjaśnienie**: 
- `QrCodeSignOptions` Ustawia wygląd i zawartość kodu QR. W tym miejscu określamy typ kodu QR HIBC LIC i umieszczamy go w dokumencie.
- `ReturnContent` ustawienie wartości true umożliwia pobranie renderowanego obrazu podpisanego dokumentu.

#### Wskazówki dotyczące rozwiązywania problemów

- Sprawdź, czy ścieżka dostępu do dokumentu jest poprawnie określona.
- Sprawdź, czy GroupDocs.Signature posiada odpowiednią licencję zapewniającą pełną funkcjonalność.

### Podpisz dokument kodem HIBC LIC Aztec

#### Przegląd

Kod Aztec oferuje inną formę kodowania, odpowiednią do przechowywania informacji o dużej gęstości. Ta sekcja koncentruje się na osadzaniu kodu Aztec w dokumentach za pomocą GroupDocs.Signature.

#### Kroki wdrożenia

##### Krok 1: Skonfiguruj ścieżki

Podobnie jak w poprzedniej funkcji, zdefiniuj ścieżki do plików:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICAztec");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICAztec.pdf");
```

##### Krok 2: Skonfiguruj opcje kodu Aztec

Skonfiguruj kod Aztec przy użyciu GroupDocs.Signature:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_AZ_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec)
    {
        Left = 1,
        Top = 200,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    signature.Sign(destinFilePath, hibcLic_AZ_Options);
}
```

**Wyjaśnienie**: 
- Ten `QrCodeSignOptions` jest tu użyty ponownie, ale z kodem typu Aztec.
- Pozycjonowanie (`Top`, `Left`) i ustawienia pobierania treści są podobne do kodów QR.

#### Wskazówki dotyczące rozwiązywania problemów

- Sprawdź, czy ścieżki do plików są prawidłowe.
- Upewnij się, że wersja GroupDocs.Signature obsługuje typy kodu Aztec.

### Podpisz dokument za pomocą HIBC LIC DataMatrix

#### Przegląd

Kod DataMatrix zapewnia kolejną niezawodną metodę przechowywania danych. W tej sekcji pokażemy, jak zintegrować kod DataMatrix z dokumentami PDF.

#### Kroki wdrożenia

##### Krok 1: Ustaw ścieżki plików

Podobnie jak poprzednio, ustal, gdzie znajdują się Twoje pliki:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICDataMatrix");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICDataMatrix.pdf");
```

##### Krok 2: Utwórz opcje podpisu DataMatrix

Skonfiguruj i zastosuj kod DataMatrix:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_DM_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix)
    {
        Left = 1,
        Top = 400,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    signature.Sign(destinFilePath, hibcLic_DM_Options);
}
```

**Wyjaśnienie**: 
- `QrCodeSignOptions` służy do ustawiania wyglądu i zawartości kodu DataMatrix.
- Pozycjonowanie (`Top`, `Left`) i ustawienia pobierania podążają za tym samym schematem, co poprzednie kody.

#### Wskazówki dotyczące rozwiązywania problemów

- Sprawdź, czy wszystkie ścieżki plików są poprawnie określone.
- Sprawdź, czy GroupDocs.Signature obsługuje typy kodu DataMatrix w Twojej wersji.

### Podpisz dokument kodem QR HIBC PAS

#### Przegląd

Podpisywanie dokumentów kodem QR HIBC PAS usprawnia śledzenie i identyfikowalność produktów. Ta sekcja przeprowadzi Cię przez proces osadzania kodu QR PAS w plikach PDF za pomocą GroupDocs.Signature.

#### Kroki wdrożenia

##### Krok 1: Skonfiguruj ścieżki źródłowe i wyjściowe

Zdefiniuj lokalizację dokumentu źródłowego i miejsce, w którym ma zostać zapisany podpisany dokument wyjściowy:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCPASQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCPASQR.pdf");
```

##### Krok 2: Utwórz opcje podpisu kodem QR

Skonfiguruj swój kod QR PAS, podając konkretny tekst i ustawienia:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcPas_QR_Options = new QrCodeSignOptions("PAS123456789012", QrCodeTypes.HIBCPASQR)
    {
        Left = 1,
        Top = 500,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    // Podpisz dokument, korzystając z tych opcji.
    signature.Sign(destinFilePath, hibcPas_QR_Options);
}
```

**Wyjaśnienie**: 
- `QrCodeSignOptions` jest skonfigurowany dla kodu QR typu HIBC PAS i umieszczony w dokumencie.
- `ReturnContent` ustawienie wartości true powoduje pobranie wyrenderowanego obrazu podpisanego dokumentu.

#### Wskazówki dotyczące rozwiązywania problemów

- Sprawdź, czy wszystkie ścieżki są poprawnie określone.
- Sprawdź, czy GroupDocs.Signature obsługuje typy kodów QR PAS w Twojej wersji.

### Wniosek

Postępując zgodnie z tym przewodnikiem, możesz skutecznie zintegrować kody QR HIBC LIC i PAS z dokumentami PDF za pomocą GroupDocs.Signature dla .NET. Ten proces zwiększa bezpieczeństwo dokumentów, ich identyfikowalność i zgodność z przepisami w różnych branżach. Aby uzyskać więcej informacji na temat dostosowywania i zaawansowanych funkcji, zapoznaj się z [Dokumentacja GroupDocs](https://docs.groupdocs.com/signature/net/).