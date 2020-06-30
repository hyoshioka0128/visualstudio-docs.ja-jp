---
title: Office ソリューションの配置マニフェスト
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office applications [Office development in Visual Studio], deployment manifests
- deployment manifests [Office development in Visual Studio]
- manifests [Office development in Visual Studio], deployment
- Office development in Visual Studio, deployment manifests
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 3540420d07bd158b19f0b078f01cfdb37ce18beb
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547551"
---
# <a name="deployment-manifests-for-office-solutions"></a>Office ソリューションの配置マニフェスト
  配置マニフェストは、Office ソリューションの配置設定を記述する XML ファイルであり、現在のアプリケーションのバージョンを識別します。

 Visual Studio での Office 開発では、 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)リファレンスで定義されている配置マニフェストスキーマを使用します。

## <a name="remarks"></a>Remarks
 Office ソリューションの配置マニフェストファイルは、現在のバージョンとその他の配置設定を識別します。 アプリケーションマニフェストを参照し、ソリューションの現在のバージョンとソリューション内のすべてのファイルについて説明します。

## <a name="file-name-syntax"></a>ファイル名の構文
 配置マニフェストファイルの名前は、拡張子が *.vsto*である必要があります。 これは標準の配置マニフェストですが、 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 拡張機能は、Visual Studio Tools for Office ランタイムがファイルを処理できるようにすることとは異なります。

## <a name="example"></a>例
 次のコード例は、Visual Studio Tools for Office ソリューションの配置マニフェストを示しています。

```xml
<?xml version="1.0" encoding="utf-8"?>
<asmv1:assembly
  xsi:schemaLocation=
    "urn:schemas-microsoft-com:asm.v1 assembly.adaptive.xsd"
  manifestVersion="1.0"
  xmlns:asmv3="urn:schemas-microsoft-com:asm.v3"
  xmlns:dsig="http://www.w3.org/2000/09/xmldsig#"
  xmlns:co.v1="urn:schemas-microsoft-com:clickonce.v1"
  xmlns:co.v2="urn:schemas-microsoft-com:clickonce.v2"
  xmlns="urn:schemas-microsoft-com:asm.v2"
  xmlns:asmv1="urn:schemas-microsoft-com:asm.v1"
  xmlns:asmv2="urn:schemas-microsoft-com:asm.v2"
  xmlns:xrml="urn:mpeg:mpeg21:2003:01-REL-R-NS"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <assemblyIdentity
    name="ContosoOfficeSolutions.vsto"
    version="1.0.0.0"
    publicKeyToken="25d0f3ca94156f1f"
    language="neutral"
    processorArchitecture="msil"
    xmlns="urn:schemas-microsoft-com:asm.v1" />
  <description
    asmv2:publisher="Microsoft"
    asmv2:product="ContosoOfficeSolutions"
    xmlns="urn:schemas-microsoft-com:asm.v1" />
  <deployment install="false" mapFileExtensions="true" />
  <dependency>
    <dependentAssembly
      dependencyType="install"
      codebase="ContosoOfficeSolutions.dll.manifest"
      size="13545">
      <assemblyIdentity
        name="ContosoOfficeSolutions.dll"
        version="1.0.0.0"
        publicKeyToken="25d0f3ca94156f1f"
        language="neutral"
        processorArchitecture="msil"
        type="win32" />
      <hash>
        <dsig:Transforms>
          <dsig:Transform Algorithm=
            "urn:schemas-microsoft-com:HashTransforms.Identity" />
        </dsig:Transforms>
        <dsig:DigestMethod Algorithm=
          "http://www.w3.org/2000/09/xmldsig#sha1" />
        <dsig:DigestValue>PoY</dsig:DigestValue>
      </hash>
    </dependentAssembly>
  </dependency>
  <publisherIdentity name="name" issuerKeyHash="003" />
<Signature
  Id="StrongNameSignature"
  xmlns="http://www.w3.org/2000/09/xmldsig#">
  <SignedInfo>
    <CanonicalizationMethod Algorithm=
      "http://www.w3.org/2001/10/xml-exc-c14n#" />
  <SignatureMethod Algorithm=
    "http://www.w3.org/2000/09/xmldsig#rsa-sha1" />
    <Reference URI="">
      <Transforms>
        <Transform Algorithm=
          "http://www.w3.org/2000/09/xmldsig#enveloped-signature" />
        <Transform Algorithm=
          "http://www.w3.org/2001/10/xml-exc-c14n#" />
      </Transforms>
      <DigestMethod Algorithm=
        "http://www.w3.org/2000/09/xmldsig#sha1" />
      <DigestValue>5oz</DigestValue>
    </Reference>
  </SignedInfo>
  <SignatureValue>nNG</SignatureValue>
  <KeyInfo Id="StrongNameKeyInfo">
    <KeyValue>
      <RSAKeyValue>
        <Modulus>ufI</Modulus>
        <Exponent>AQAB</Exponent>
      </RSAKeyValue>
    </KeyValue>
    <msrel:RelData
      xmlns:msrel=
        "http://schemas.microsoft.com/windows/rel/2005/reldata">
      <r:license
        xmlns:r="urn:mpeg:mpeg21:2003:01-REL-R-NS"
        xmlns:as=
          "http://schemas.microsoft.com/windows/pki/2005/Authenticode">
        <r:grant>
          <as:ManifestInformation
            Hash="099"
            Description=""
            Url="">
            <as:assemblyIdentity
              name="ContosoOfficeSolutions.vsto"
              version="1.0.0.0"
              publicKeyToken="25d0f3ca94156f1f"
              language="neutral"
              processorArchitecture="msil"
              xmlns="urn:schemas-microsoft-com:asm.v1" />
          </as:ManifestInformation>
          <as:SignedBy />
          <as:AuthenticodePublisher>
            <as:X509SubjectName>CN=DDNET\BAAdmin</as:X509SubjectName>
          </as:AuthenticodePublisher>
        </r:grant>
        <r:issuer>
          <Signature
            Id="AuthenticodeSignature"
            xmlns="http://www.w3.org/2000/09/xmldsig#">
            <SignedInfo>
              <CanonicalizationMethod
                Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
              <SignatureMethod
                Algorithm=
                  "http://www.w3.org/2000/09/xmldsig#rsa-sha1" />
              <Reference URI="">
                <Transforms>
                  <Transform Algorithm=
                    "http://www.w3.org/2000/09/xmldsig#enveloped-signature" />
                  <Transform Algorithm=
                    "http://www.w3.org/2001/10/xml-exc-c14n#" />
                </Transforms>
                <DigestMethod
                  Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
                <DigestValue>iAd</DigestValue>
              </Reference>
            </SignedInfo>
            <SignatureValue>HL9</SignatureValue>
            <KeyInfo>
              <KeyValue>
                <RSAKeyValue>
                  <Modulus>ufI</Modulus>
                  <Exponent>AQAB</Exponent>
                </RSAKeyValue>
              </KeyValue>
              <X509Data>
                <X509Certificate>MII</X509Certificate>
              </X509Data>
            </KeyInfo>
          </Signature>
        </r:issuer>
      </r:license>
    </msrel:RelData>
  </KeyInfo>
</Signature>
</asmv1:assembly>
```

## <a name="see-also"></a>関連項目

- [Office ソリューション用アプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)