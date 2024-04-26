---
title: Tìm kiếm nhiều chữ ký
linktitle: Tìm kiếm nhiều chữ ký
second_title: API GroupDocs.Signature .NET
description: Tìm hiểu cách tìm kiếm nhiều chữ ký trong tài liệu .NET bằng GroupDocs.Signature để bảo mật và toàn vẹn tài liệu hiệu quả.
type: docs
weight: 14
url: /vi/net/signature-searching/search-for-multiple-signatures/
---
## Giới thiệu
GroupDocs.Signature for .NET là một thư viện mạnh mẽ cho phép các nhà phát triển thêm, tìm kiếm và xóa nhiều loại chữ ký khác nhau ở các định dạng tài liệu phổ biến bằng ứng dụng .NET. Trong hướng dẫn này, chúng tôi sẽ tập trung vào việc tìm kiếm nhiều chữ ký trong tài liệu bằng GroupDocs.Signature cho .NET.
## Điều kiện tiên quyết
Trước khi chúng tôi bắt đầu, hãy đảm bảo bạn có các điều kiện tiên quyết sau:
- Visual Studio được cài đặt trên hệ thống của bạn.
- Hiểu biết cơ bản về ngôn ngữ lập trình C#.
- Thư viện GroupDocs.Signature cho .NET được cài đặt trong dự án của bạn. Bạn có thể tải nó xuống từ[đây](https://releases.groupdocs.com/signature/net/).

## Nhập không gian tên
Trước tiên, bạn cần nhập các không gian tên cần thiết để truy cập các lớp và phương thức do GroupDocs.Signature cung cấp cho .NET.
```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Bước 1: Tải tài liệu
Tải tài liệu nơi bạn muốn tìm kiếm nhiều chữ ký. Đảm bảo rằng bạn cung cấp đường dẫn tệp chính xác.
```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Mã của bạn ở đây
}
```
## Bước 2: Xác định tùy chọn tìm kiếm
Xác định các tùy chọn tìm kiếm cho nhiều loại chữ ký khác nhau như văn bản, kỹ thuật số, mã vạch, mã QR và siêu dữ liệu. Bạn có thể chỉ định tiêu chí tìm kiếm như văn bản phù hợp, loại đối sánh và tìm kiếm trên tất cả các trang.
```csharp
// Xác định các tùy chọn tìm kiếm
TextSearchOptions textOptions = new TextSearchOptions()
{
    AllPages = true
};
DigitalSearchOptions digitalOptions = new DigitalSearchOptions()
{
    AllPages = true
};
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions()
{
    AllPages = true,
    Text = "123456",
    MatchType = TextMatchType.Exact
};
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions()
{
    AllPages = true,
    Text = "John",
    MatchType = TextMatchType.Contains
};
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```
## Bước 3: Thêm tùy chọn tìm kiếm vào danh sách
Thêm các tùy chọn tìm kiếm đã xác định vào danh sách.
```csharp
// Thêm tùy chọn vào danh sách
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
listOptions.Add(metadataOptions);
listOptions.Add(digitalOptions);
```
## Bước 4: Tìm kiếm chữ ký
Tìm kiếm chữ ký trong tài liệu bằng các tùy chọn tìm kiếm đã xác định.
```csharp
// Tìm kiếm chữ ký trong tài liệu
SearchResult result = signature.Search(listOptions);
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains following signatures.");
    foreach (var resSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found at page {resSignature.PageNumber} with type {resSignature.SignatureType} and Id#: {resSignature.SignatureId}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## Phần kết luận
Trong hướng dẫn này, chúng ta đã học cách tìm kiếm nhiều chữ ký trong một tài liệu bằng GroupDocs.Signature cho .NET. Bằng cách làm theo các bước được cung cấp, bạn có thể xác định hiệu quả các loại chữ ký khác nhau trong tài liệu của mình, tăng cường tính bảo mật và tính toàn vẹn của tài liệu.
## Câu hỏi thường gặp
### Tôi có thể tìm kiếm chữ ký ở các định dạng tài liệu khác nhau không?
Có, GroupDocs.Signature for .NET hỗ trợ nhiều định dạng tài liệu bao gồm Word, PDF, Excel, v.v.
### Có thể tùy chỉnh tiêu chí tìm kiếm chữ ký không?
Hoàn toàn có thể, bạn có thể điều chỉnh tiêu chí tìm kiếm theo yêu cầu của mình, chẳng hạn như chỉ định kết quả khớp văn bản chính xác hoặc tìm kiếm trên tất cả các trang.
### GroupDocs.Signature cho .NET có hỗ trợ chữ ký số không?
Có, bạn có thể tìm kiếm chữ ký số cũng như các loại khác như chữ ký văn bản, mã vạch và mã QR.
### Tôi có thể tích hợp chức năng tìm kiếm chữ ký vào các ứng dụng .NET của mình một cách dễ dàng không?
Có, GroupDocs.Signature dành cho .NET cung cấp một API đơn giản giúp đơn giản hóa quá trình tích hợp.
### Tôi có thể tìm thêm hỗ trợ hoặc trợ giúp ở đâu?
 Bạn có thể truy cập diễn đàn GroupDocs.Signature[đây](https://forum.groupdocs.com/c/signature/13) cho bất kỳ thắc mắc hoặc hỗ trợ.