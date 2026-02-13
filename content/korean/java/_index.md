---
categories:
- Java Development
- Document Security
date: '2025-12-19'
description: Java에서 PDF 디지털 서명, 보안 전자 서명, QR 코드 및 바코드를 추가하는 방법을 배웁니다. 인증서를 사용해 PDF에
  서명하고 Java로 PDF 서명을 검증하는 단계별 가이드를 포함합니다.
is_root: true
keywords: java digital signature, add signature in java, electronic signature java,
  pdf signing java, document verification java, barcode signature, qr code signature
  java
lastmod: '2025-12-19'
linktitle: Java Document Signing Tutorials
tags:
- digital-signatures
- java-tutorials
- document-signing
- pdf-security
title: 'Java PDF 디지털 서명 튜토리얼 - Java에서 서명 추가'
type: docs
url: /ko/java/
weight: 10
---

# Java에서 디지털 서명 추가하기

Java 애플리케이션에서 계약서, 청구서 또는 기타 중요한 문서를 처리하고 있다면 아마도 다음과 같은 질문을 해봤을 것입니다: **"이 문서를 법적으로 구속력 있게 그리고 안전하게 만들려면 어떻게 해야 할까?"** 엔터프라이즈 문서 관리 시스템, 전자상거래 플랫폼, 혹은 정부 애플리케이션을 개발하고 있든, 적절한 문서 서명을 구현하는 것은 선택 사항이 아니라 종종 법적 요구 사항입니다. **java pdf digital signature**을 추가하면 내용이 변경되지 않았으며 서명자가 진본임을 암호학적으로 증명할 수 있습니다.

## 빠른 답변
- **어떤 라이브러리를 사용해야 하나요?** GroupDocs.Signature for Java는 모든 서명 유형을 위한 완전한 API를 제공합니다.  
- **인증서를 사용해 PDF에 서명할 수 있나요?** 예 – “sign pdf with certificate” 워크플로를 사용하세요.  
- **PDF에 비밀번호를 설정해 보호할 수 있나요?** API를 사용하면 서명 전에 암호화와 비밀번호 보호를 적용할 수 있습니다.  
- **Java에서 PDF 서명을 검증할 수 있나요?** 물론입니다; “verify pdf signature java” 메서드가 이를 처리합니다.  
- **Java에서 이미지 워터마크를 추가할 수 있나요?** “add image watermark java” 기능을 사용해 로고나 스탬프를 삽입하세요.

## java pdf digital signature란?
**java pdf digital signature**은 Java 코드를 사용해 PDF 문서에 적용되는 암호화 씰입니다. 인증서(증명서)를 통해 서명자의 신원을 문서 내용에 결합하여 무결성, 인증 및 부인 방지를 보장합니다.

## java pdf digital signature를 사용해야 하는 이유
- **법적 준수:** 많은 관할 구역에서 전자서명 규정을 충족합니다.  
- **변조 방지:** 서명 후 내용이 변경되면 서명 검증이 실패합니다.  
- **자동화 친화:** 배치 처리, 워크플로 및 문서 관리 시스템과의 통합에 이상적입니다.

## Java에서 인증서를 사용해 PDF에 서명하는 방법
PFX/PKCS#12 인증서를 로드하고 PDF에 적용하면 디지털 서명을 만들 수 있습니다. API가 저수준 암호화 작업을 처리하므로 인증서 경로와 비밀번호만 제공하면 됩니다.

## Java를 사용해 PDF에 비밀번호를 설정하는 방법
서명 전이나 후에 PDF를 암호화하고 열기 비밀번호를 설정할 수 있습니다. 이는 특히 문서가 보안이 취약한 채널을 통해 전송될 때 추가 보안 레이어를 제공합니다.

## Java에서 PDF 서명을 검증하는 방법
검증 루틴은 서명을 읽고 인증서 체인을 확인하며 문서가 수정되지 않았는지 확인합니다. 자세한 검증 결과를 반환하여 후속 조치를 취할 수 있습니다.

## Java에서 이미지 워터마크를 추가하는 방법
이미지 서명 기능을 사용해 로고, 스탬프 또는 사용자 정의 그래픽을 오버레이합니다. 불투명도, 회전 및 위치를 제어해 전문적인 워터마크를 만들 수 있습니다.

Java 애플리케이션에서 계약서, 청구서 또는 기타 중요한 문서를 처리하고 있다면 아마도 다음과 같은 질문을 해봤을 것입니다: **"이 문서를 법적으로 구속력 있게 그리고 안전하게 만들려면 어떻게 해야 할까?"** 엔터프라이즈 문서 관리 시스템, 전자상거래 플랫폼, 혹은 정부 애플리케이션을 개발하고 있든, 적절한 문서 서명을 구현하는 것은 선택 사항이 아니라 종종 법적 요구 사항입니다.

좋은 소식은? 암호학 전문가가 되거나 모든 것을 처음부터 구축할 필요가 없다는 것입니다. 이 포괄적인 튜토리얼 모음은 Java에서 보안 문서 서명 솔루션을 구현하는 방법을 단계별로 안내합니다. 기본 디지털 서명부터 고급 다중 서명 워크플로까지 모두 다룹니다. 문서를 보호하고, 진위를 검증하며, 규정 준수를 충족하는 데 필요한 모든 내용을 제공할 것입니다.

## Java 개발자를 위한 문서 서명의 중요성

사실, 이메일 첨부 파일과 공유 문서는 쉽게 변조될 수 있습니다. 적절한 서명이 없으면 다음을 증명할 수 없습니다:
- **누가 실제로 서명했는지** (인증)  
- **언제 서명했는지** (부인 방지)  
- **서명 후에 아무도 변경하지 않았는지** (무결성)

이것이 전자 서명의 역할입니다. 단순 이미지 스탬프(누구나 복사 가능)와 달리, 적절한 디지털 서명은 암호화 기술을 사용해 문서를 변조 방지하고 대부분의 관할 구역에서 법적 효력을 갖게 합니다.

## 배우게 될 내용

이 튜토리얼은 GroupDocs.Signature for Java를 사용해 전체 문서 서명 수명 주기를 다룹니다—첫 번째 “Hello World” 서명부터 다중 서명 유형, 검증 워크플로, 보안 기능을 포함한 복잡한 엔터프라이즈 시나리오까지. 초보자든 고급 기능을 구현해야 하든, 모든 시나리오에 맞는 실용적인 복사‑붙여넣기 예제를 찾을 수 있습니다.

## 올바른 서명 유형 선택하기

모든 서명이 동일하게 만들어진 것은 아닙니다. 아래는 각 유형을 언제 사용해야 하는지에 대한 가이드이며, 모든 유형에 대한 튜토리얼이 준비되어 있습니다:

**Digital Signatures** – 법적 문서에 대한 금본위 표준. 문서가 변경되지 않았음을 암호학적으로 증명해야 할 때 사용합니다. 계약서, 법적 합의서, 규정 준수 문서에 적합합니다. 실제로 인증서 기반 PKI 인프라를 사용합니다.

**Barcode Signatures** – 내부 문서 추적 및 재고 관리에 적합합니다. 구조화된 데이터를 삽입해 스캔 및 프로그래밍 방식으로 처리하기 쉽습니다. 창고 문서, 배송 라벨, 내부 양식에 활용됩니다.

**QR Code Signatures** – 바코드보다 더 많은 정보를 작은 공간에 담아야 할 때 사용합니다. 모바일 환경에서 사용자가 휴대폰으로 스캔하기에 최적입니다. 이벤트 티켓, 인증 워크플로, 물리 문서를 디지털 레코드와 연결할 때 활용됩니다.

**Image Signatures** – 브랜드 로고, 워터마크 또는 스캔한 손글씨 서명이 필요할 때 사용합니다. 자체적으로는 암호학적으로 안전하지 않지만, 고객용 문서에서 시각적 인식이 중요한 경우에 유용합니다.

**Text Signatures** – 주석, 승인 또는 텍스트 기반 증명이 필요할 때 간단하고 효과적입니다. 내부 워크플로, 코멘트, “Approved by [Name]”와 같은 표시가 필요할 때 사용합니다.

**Form Field Signatures** – PDF 양식에서 사용자가 특정 필드를 채우고 서명해야 할 때 이상적입니다. 정부 양식, 신청서, 구조화된 데이터 수집 시나리오에 흔히 사용됩니다.

**Metadata Signatures** – 눈에 보이지 않는 옵션. 서명 데이터를 문서 내부에 숨겨 시각적 레이아웃을 변경하지 않습니다. 내부 추적이 필요하지만 시각적 혼란을 피하고 싶을 때 적합합니다.

## 튜토리얼 카테고리

### [Getting Started](./getting-started/)
Java에서 문서 서명을 처음 접하나요? 여기서 시작하세요. 설치, 라이선스, 기본 설정 및 10분 이내에 첫 서명을 만드는 과정을 단계별로 안내합니다. GroupDocs.Signature 설정 방법, 핵심 개념 이해, 첫 문서 서명을 배울 수 있습니다.

**구축 예제**: 디지털 서명을 사용해 PDF에 서명하는 간단한 Java 애플리케이션.

### [Document Loading & Saving](./document-loading-saving/)
문서에 서명하려면 먼저 로드하고, 서명 후에는 올바르게 저장해야 합니다. 로컬 스토리지, 스트림, 클라우드 스토리지, 인‑메모리 문서 등 다양한 소스에서 파일을 다루는 방법을 배웁니다. 다양한 시나리오에 맞는 저장 옵션도 소개합니다(특정 포맷이나 압축 저장 등).

**일반 사용 사례**: AWS S3에서 문서를 로드하고 서명한 뒤 클라우드에 다시 저장하기.

### [Digital Signatures](./digital-signatures/)
가장 안전한 서명 유형. 인증서 기반 디지털 서명을 구현하는 방법을 배웁니다. 디지털 서명 추가, 검증, 인증서 저장소 사용, 만료된 인증서 처리 등 실무에 필요한 모든 내용을 다룹니다.

**마스터 목표**: PFX 인증서를 사용해 법적 구속력이 있는 디지털 서명 생성, 서명 체인 검증, 인증서 유효성 검사 처리.

### [Barcode Signatures](./barcode-signatures/)
스캔하기 쉬운 구조화 데이터를 삽입하고 싶나요? 다양한 바코드 유형(Code128, DataMatrix 등) 추가, 기존 문서에서 바코드 검색, 바코드 진위 검증 방법을 배웁니다.

**적합 분야**: 재고 관리 시스템, 배송 문서, 내부 추적 워크플로.

### [QR Code Signatures](./qr-code-signatures/)
QR 코드는 바코드보다 더 많은 데이터를 담을 수 있으며 모바일 기기와 잘 어울립니다. 맞춤형 포맷, 민감 데이터 암호화, 복합 시나리오용 특수 QR 객체 등을 구현하는 방법을 배웁니다. 기본 QR 코드부터 고급 암호화 구현까지 모두 다룹니다.

**실제 예제**: 암호화된 참석자 데이터를 포함한 이벤트 티켓 QR 코드 만들기.

### [Image Signatures](./image-signatures/)
시각적 증명이 필요할 때—회사 로고, 워터마크, 스캔한 손글씨 서명 등—이미지 서명을 추가하고, 맞춤형 워터마크를 만들고, 스탬프 서명을 구현하는 방법을 배웁니다. 위치 지정, 투명도, 크기 조정, 전문적인 이미지 처리 기술을 다룹니다.

**일반 시나리오**: 민감한 문서에 “CONFIDENTIAL” 워터마크 추가 또는 공식 서한에 회사 로고 삽입.

### [Text Signatures](./text-signatures/)
가장 단순하지만 강력한 서명 유형. 주석, 승인, 문서 표시 등에 텍스트 서명을 활용합니다. 서식 있는 텍스트 추가, 사용자 정의 폰트·색상, 정확한 위치 지정, 대각선 워터마크용 텍스트 회전 등을 배웁니다.

**빠른 성과**: “Approved by John Smith – Jan 15, 2025”와 같은 텍스트를 워크플로에 자동 삽입.

### [Form Field Signatures](./form-field-signatures/)
PDF 양식 작업 중인가요? 체크박스, 텍스트 입력, 서명 필드 등 양식 필드를 프로그래밍 방식으로 채우고 서명하는 방법을 배웁니다. 정부 양식, 신청서 등 구조화된 데이터 수집이 필요한 모든 경우에 필수적입니다.

**사용 사례**: 세금 양식이나 비자 신청서를 자동으로 채우고 서명하기.

### [Metadata Signatures](./metadata-signatures/)
보이지 않는 서명이 필요할 때. 메타데이터 서명은 문서 외관을 바꾸지 않으면서 추적 정보, 타임스탬프, 인증 데이터를 삽입합니다. 내부 문서 관리와 추적에 최적입니다.

**활용 이유**: 문서 버전 추적, 작성자 정보 삽입, 숨겨진 승인 워크플로 구현.

### [Multiple Signatures](./multiple-signatures/)
실제 문서는 종종 여러 서명 유형을 동시에 필요로 합니다—법적 효력을 위한 디지털 서명, 브랜드 로고를 위한 이미지 서명, 감사용 타임스탬프 등. 다양한 서명 유형을 결합하고 복잡한 서명 워크플로를 관리하며 순차 서명을 처리하는 방법을 배웁니다.

**엔터프라이즈 시나리오**: 법무팀의 디지털 서명, 회사 로고 이미지 서명, 검증용 QR 코드가 모두 포함된 계약서.

### [Search & Verification](./search-verification/)
문서에 서명했으면 이제 무엇을 해야 할까요? 기존 서명을 검색하고, 진위를 검증하며, 인증서 유효성을 확인하고, 서명 체인을 검증하는 방법을 배웁니다. 신뢰할 수 있는 문서 워크플로를 구축하는 데 필수적인 기술입니다.

**핵심 스킬**: 디지털 서명된 계약서를 실행하기 전에 검증하거나, 문서가 변조되었는지 확인하기.

### [Signature Management](./signature-management/)
문서는 시간이 지나면서 변경될 수 있고, 서명을 업데이트하거나 삭제해야 할 때도 있습니다. 기존 서명을 업데이트(예: 유효 기간 연장), 필요 시 삭제, 장기 문서의 서명 수명 주기 관리 방법을 다룹니다.

**실용 예제**: 계약서 수정 전 오래된 서명을 제거하고 재서명하기.

### [Preview & Info](./preview-info/)
사용자에게 서명 전에 문서 미리보기를 보여주거나, 기존 서명에 대한 정보를 추출하고 싶나요? 썸네일 생성, 문서 메타데이터 조회, 문서 내 모든 서명 목록 가져오기 등을 배웁니다.

**사용자 경험 향상**: 웹 애플리케이션에서 사용자가 서명하기 전에 미리보기를 제공하기.

### [Advanced Options](./advanced-options/)
고급 기술을 배우고 싶나요? 서명 암호화, 사용자 정의 직렬화, 특수 서명 옵션, 외관 커스터마이징, 성능 최적화 등을 다룹니다. 엔터프라이즈 애플리케이션에서 마주칠 수 있는 엣지 케이스와 고급 시나리오를 포함합니다.

**고급 시나리오**: 사용자 정의 키로 서명 데이터 암호화하거나 타임스탬프 기관 구현하기.

### [Event Handling](./event-handling/)
서명 프로세스를 모니터링하고, 작업을 취소하거나, 서명 중에 사용자 정의 로직을 추가하고 싶나요? 이벤트 핸들러 구현, 진행 상황 추적, 취소 처리, 반응형 서명 워크플로 구축 방법을 배웁니다.

**실제 사용 사례**: 대량 문서 서명 시 진행 바 표시하거나 장시간 작업을 취소하기.

### [Document Protection](./document-protection/)
보안은 서명에만 국한되지 않습니다. 비밀번호 보호, 문서 암호화, 인쇄·편집 방지 권한 설정, 다중 보호 방법 결합 등을 배워 최대 보안을 구현합니다.

**보안 레이어**: 문서를 비밀번호로 보호한 뒤 디지털 서명을 추가하고, 다시 암호화하는 방어 깊이 전략.

## 일반적인 문제와 해결책

**문제**: “내 디지털 서명이 무효로 표시됩니다”  
- **해결책**: 인증서 만료일 확인, 인증서 체인 완전성 점검, 올바른 인증서 저장소 사용 여부 확인. 자세한 내용은 [Digital Signatures](./digital-signatures/) 튜토리얼에서 인증서 문제 해결을 다룹니다.

**문제**: “문서를 저장하면 서명이 사라집니다”  
- **해결책**: 사용 중인 서명 유형을 지원하는 포맷으로 저장하고 있는지 확인하세요. 모든 포맷이 모든 서명 유형을 지원하는 것은 아니므로 [Document Loading & Saving](./document-loading-saving/) 섹션에서 포맷 호환성을 확인하십시오.

**문제**: “어떤 서명 유형을 사용해야 할지 모르겠어요”  
-해결책**: 법적 문서는 디지털 서명, 추적은 QR/바코드, 브랜드는 이미지, 보이지 않는 추적은 메타데이터를 사용하세요. 위 “Choosing the Right Signature Type” 섹션을 참고하십시오.

**문제**: “대량 배치 서명 시 성능이 느립니다”  
- **해결책**: [Advanced Options](./advanced-options/)에서 배치 처리 기법을 사용하고, 비동기 처리와 인증서 로딩 최적화를 적용하세요. 인증서를 매 문서마다 다시 로드하지 마십시오!

## 모범 사례

1. 서명을 추가한 후 **항상 검증**하세요—성공을 가정하지 마세요.  
2. 법적 구속력이나 부인 방지가 필요하면 **디지털 서명**을 사용하세요.  
3. **인증서를 안전하게 보관**하세요—비밀번호를 코드에 하드코딩하거나 인증서를 코드에 포함하지 마십시오.  
4. 인증서 만료 시 **친절한 오류 메시지**로 처리하세요.  
5. 여러 PDF 리더에서 **테스트**하세요—서명 외관이 다르게 표시될 수 있습니다.  
6. 시각적 혼란을 피하려면 **메타데이터 서명**을 활용하세요.  
7. **예외 처리**를 철저히 구현하세요—서명 작업은 다양한 이유로 실패할 수 있습니다.  
8. 모바일 기기를 고려해 서명 유형을 선택하세요(QR 코드가 특히 유용).  
9. 서명 전에 **입력 검증**을 수행하세요—잘못된 입력은 무효 서명으로 이어집니다.  
10. 인증서를 **제때 갱신**하고, 갱신 계획을 미리 세우세요.

## 빠른 시작 경로

어디서 시작해야 할지 모르겠나요? 아래 학습 경로를 따라가세요:

1. **1주차**: [Getting Started](./getting-started/)를 완료하고 첫 문서에 서명하기.  
2. **2주차**: 보안 서명을 위해 [Digital Signatures](./digital-signatures/) 학습.  
3. **3주차**: 서명 검증을 위해 [Search & Verification](./search-verification/) 탐색.  
4. **4주차**: 자신에게 맞는 서명 유형 심화([QR Code](./qr-code-signatures/), [Barcode](./barcode-signatures/) 등).  
5. **5주차 이후**: [Multiple Signatures](./multiple-signatures/)와 [Advanced Options](./advanced-options/) 구현.

## 추가 리소스

- [Documentation](https://docs.groupdocs.com./) – API 세부 사항 및 고급 기능 심층 탐색  
- [API Reference](https://reference.groupdocs.com./) – 전체 메서드·클래스 문서  
- [Download Library](https://releases.groupdocs.com./) – 최신 GroupDocs.Signature for Java 다운로드  
- [Free Support Forum](https://forum.groupdocs.com/) – 커뮤니티에 질문하고 도움 받기  
- [Temporary License](https://purchase.groupdocs.com/temporary-license/) – 제한 없이 모든 기능 테스트 가능

---

# GroupDocs.Signature for Java 튜토리얼 및 예제

GroupDocs.Signature for Java에 대한 포괄적인 튜토리얼 모음에 오신 것을 환영합니다. 단계별 가이드를 통해 Java 애플리케이션에 보안 문서 서명 솔루션을 구현할 수 있습니다. 기본 설정부터 고급 서명 관리까지, 다양한 서명 유형으로 문서를 보호하는 데 필요한 모든 정보를 제공합니다.

### [Getting Started](./getting-started/)
GroupDocs.Signature 설치, 라이선스, 설정 및 Java 애플리케이션에서 첫 서명 프로젝트를 만드는 단계별 튜토리얼.

### [Document Loading & Saving](./document-loading-saving/)
다양한 소스에서 문서를 로드하고, GroupDocs.Signature for Java를 사용해 서명된 문서를 다양한 옵션으로 저장하는 방법을 배웁니다.

### [Digital Signatures](./digital-signatures/)
GroupDocs.Signature for Java를 사용해 문서에 디지털 서명을 추가, 검증 및 관리하는 완전한 튜토리얼.

### [Barcode Signatures](./barcode-signatures/)
GroupDocs.Signature for Java를 사용해 문서에 바코드 서명을 추가, 검색, 검증 및 관리하는 단계별 튜토리얼.

### [QR Code Signatures](./qr-code-signatures/)
GroupDocs.Signature Java 튜토리얼을 통해 QR 코드 서명 구현, 특수 QR 객체, 암호화 및 맞춤 포맷을 배웁니다.

### [Image Signatures](./image-signatures/)
GroupDocs.Signature for Java를 사용해 이미지 서명, 워터마크 및 스탬프를 문서에 추가하는 완전한 튜토리얼.

### [Text Signatures](./text-signatures/)
GroupDocs.Signature for Java를 사용해 텍스트 서명, 주석, 워터마크 및 텍스트 기반 문서 표시를 구현하는 단계별 튜토리얼.

### [Form Field Signatures](./form-field-signatures/)
GroupDocs.Signature Java 튜토리얼을 통해 PDF 양식 필드와 작업하고 서명 및 데이터 수집을 수행하는 방법을 배웁니다.

### [Metadata Signatures](./metadata-signatures/)
GroupDocs.Signature for Java를 사용해 다양한 문서 형식에 숨겨진 메타데이터 서명을 구현하는 완전한 튜토리얼.

### [Multiple Signatures](./multiple-signatures/)
GroupDocs.Signature for Java를 사용해 여러 서명 유형을 함께 구현하고 복잡한 서명 시나리오를 관리하는 단계별 튜토리얼.

### [Search & Verification](./search-verification/)
GroupDocs.Signature Java 튜토리얼을 통해 다양한 서명 유형을 검색하고 문서 서명을 검증하는 방법을 배웁니다.

### [Signature Management](./signature-management/)
GroupDocs.Signature for Java를 사용해 문서 내 기존 서명을 업데이트, 삭제 및 관리하는 완전한 튜토리얼.

### [Preview & Info](./preview-info/)
GroupDocs.Signature for Java를 사용해 문서 미리보기 생성 및 문서·서명 정보를 검색하는 단계별 튜토리얼.

### [Advanced Options](./advanced-options/)
GroupDocs.Signature Java 튜토리얼을 통해 서명 맞춤화, 암호화, 직렬화 및 특수 서명 기능을 배우세요.

### [Event Handling](./event-handling/)
GroupDocs.Signature for Java를 사용해 이벤트 처리, 취소 및 프로세스 모니터링을 구현하는 완전한 튜토리얼.

### [Document Protection](./document-protection/)
GroupDocs.Signature for Java를 사용해 비밀번호 보호, 암호화 및 보안 기능을 구현하는 단계별 튜토리얼.

## 자주 묻는 질문

**Q: GroupDocs.Signature for Java를 상용 제품에 사용할 수 있나요?**  
A: 예, 프로덕션 사용을 위해서는 유효한 GroupDocs 라이선스가 필요합니다. 평가용 임시 라이선스를 제공하고 있습니다.

**Q: 라이브러리가 비밀번호로 보호된 PDF를 지원하나요?**  
A: 물론입니다. 비밀번호로 보호된 PDF를 열고, 서명하고, 다시 저장할 수 있습니다.

**Q: Java에서 PDF 서명을 어떻게 검증하나요?**  
A: `Signature` 클래스에서 제공하는 검증 API를 사용하면 인증서 체인과 문서 무결성을 확인할 수 있습니다.

**Q: 서명하면서 눈에 보이는 워터마크를 추가할 수 있나요?**  
A: 예, 이미지 서명 기능을 사용하면 서명 과정에서 워터마크나 로고를 오버레이할 수 있습니다.

**Q: PDF 외에 지원되는 포맷은 무엇인가요?**  
A: DOCX, XLSX, PPTX, 이미지 등 다양한 일반 문서 형식을 지원합니다.

## 추가 리소스

- [GroupDocs.Signature for Java Documentation](https://docs.groupdocs.com./)  
- [GroupDocs.Signature for Java API Reference](https://reference.groupdocs.com./)  
- [Download GroupDocs.Signature for Java](https://releases.groupdocs.com./)  
- [Free Support](https://forum.groupdocs.com/)  
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

---


**마지막 업데이트:** 2025-12-19  
**테스트 환경:** GroupDocs.Signature for Java 23.12 (최신 릴리스)  
**작성자:** GroupDocs