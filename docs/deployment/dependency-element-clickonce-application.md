---
title: '&lt;dependency &gt; 要素 (ClickOnce アプリケーション) |Microsoft Docs'
description: Dependency 要素は、アプリケーションに必要なプラットフォームまたはアセンブリの依存関係を識別します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#osVersionInfo
- urn:schemas-microsoft-com:asm.v2#os
- http://www.w3.org/2000/09/xmldsig#Transform
- urn:schemas-microsoft-com:asm.v2#dependency
- http://www.w3.org/2000/09/xmldsig#DigestValue
- urn:schemas-microsoft-com:asm.v2#assemblyIdentity
- http://www.w3.org/2000/09/xmldsig#DigestMethod
- http://www.w3.org/2000/09/xmldsig#Transforms
- urn:schemas-microsoft-com:asm.v2#hash
- urn:schemas-microsoft-com:asm.v2#dependentAssembly
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- manifests [ClickOnce], dependency element
- <dependency> element [ClickOnce application manifest]
ms.assetid: 09d6a1e0-60f8-4fbd-843b-8e49ee3115a3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e7896fa2d39bafc793c5fd74f66f4991cf5e8461
ms.sourcegitcommit: 0893244403aae9187c9375ecf0e5c221c32c225b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2020
ms.locfileid: "94382950"
---
# <a name="ltdependencygt-element-clickonce-application"></a>&lt;dependency &gt; 要素 (ClickOnce アプリケーション)
アプリケーションに必要なプラットフォームまたはアセンブリの依存関係を識別します。

## <a name="syntax"></a>構文

```xml

      <dependency>
   <dependentOS
      supportURL
      description
   >
      <osVersionInfo>
         <os
            majorVersion
            minorVersion
            buildNumber
            servicePackMajor
            servicePackMinor
            productType
            suiteType
         />
      </osVersionInfo>
   </dependentOS>
   <dependentAssembly
      dependencyType
      allowDelayedBinding
      group
      codeBase
      size
   >
      <assemblyIdentity
         name
         version
         processorArchitecture
         language
      >
         <hash>
            <dsig:Transforms>
               <dsig:Transform
                  Algorithm
            />
            </dsig:Transforms>
            <dsig:DigestMethod />
            <dsig:DigestValue>
            </dsig:DigestValue>
    </hash>

      </assemblyIdentity>
   </dependentAssembly>
</dependency>
```

## <a name="elements-and-attributes"></a>要素と属性
 `dependency` 要素は必須です。 同じアプリケーションマニフェストにの複数のインスタンスが存在する場合があり `dependency` ます。

 `dependency`要素には属性がなく、には次の子要素が含まれています。

### <a name="dependentos"></a>依存関係 Entos
 省略可能。 要素が含まれてい `osVersionInfo` ます。 要素 `dependentOS` と `dependentAssembly` 要素は相互に排他的です。一方またはもう一方は要素に対して存在する必要があり `dependency` ますが、両方を指定することはできません。

 `dependentOS` では、次の属性がサポートされています。

|属性|説明|
|---------------|-----------------|
|`supportUrl`|省略可能。 依存プラットフォームのサポート URL を指定します。 この URL は、必要なプラットフォームが見つかった場合にユーザーに表示されます。|
|`description`|省略可能。 人間が判読できる形式で、要素によって記述されるオペレーティングシステムについて説明し `dependentOS` ます。|

### <a name="osversioninfo"></a>osVersionInfo
 必須。 この要素は `dependentOS` 要素の子であり、 `os` 要素を含んでいます。 この要素には属性はありません。

### <a name="os"></a>os
 必須。 この要素は `osVersionInfo` 要素の子です。 この要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`majorVersion`|必須。 OS のメジャーバージョン番号を指定します。|
|`minorVersion`|必須。 OS のマイナーバージョン番号を指定します。|
|`buildNumber`|必須。 OS のビルド番号を指定します。|
|`servicePackMajor`|必須。 OS の Service Pack メジャー番号を指定します。|
|`servicePackMinor`|省略可能。 OS の Service Pack マイナー番号を指定します。|
|`productType`|省略可能。 製品の種類の値を識別します。 有効な値は `server`、`workstation`、`domainController` です。 たとえば、Windows 2000 Professional の場合、この属性値はに `workstation` なります。|
|`suiteType`|省略可能。 システムで使用可能な製品スイート、またはシステムの構成の種類を識別します。 有効な値は、`backoffice`、`blade`、`datacenter`、`enterprise`、`home`、`professional`、`smallbusiness`、`smallbusinessRestricted`、および `terminal` です。 たとえば、Windows 2000 Professional の場合、この属性値はに `professional` なります。|

### <a name="dependentassembly"></a>dependentAssembly
 省略可能。 要素が含まれてい `assemblyIdentity` ます。 要素 `dependentOS` と `dependentAssembly` 要素は相互に排他的です。一方またはもう一方は要素に対して存在する必要があり `dependency` ますが、両方を指定することはできません。

 `dependentAssembly` には次の属性があります。

| 属性 | 説明 |
|-----------------------| - |
| `dependencyType` | 必須。 依存関係の種類を指定します。 有効な値は `preprequisite` と `install` です。 `install`アセンブリは、アプリケーションの一部としてインストールされ [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。 `prerequisite`アプリケーションをインストールする前に、アセンブリがグローバルアセンブリキャッシュ (GAC) に存在している必要があり [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。 |
| `allowDelayedBinding` | 必須。 実行時にアセンブリをプログラムによって読み込むことができるかどうかを指定します。 |
| `group` | 省略可能。 `dependencyType`属性がに設定されている場合 `install` 、は、要求時にのみインストールされるアセンブリの名前付きグループを指定します。 詳細については、「[チュートリアル:デザイナーを使用し、ClickOnce 配置 API で必要に応じてアセンブリをダウンロードする](../deployment/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer.md)」を参照してください。<br /><br /> に設定 `framework` され、 `dependencyType` 属性がに設定されている場合 `prerequisite` 、は、アセンブリを .NET Framework の一部として指定します。 .NET Framework 4 以降のバージョンにインストールする場合、このアセンブリのグローバル assemby キャッシュ (GAC) はチェックされません。 |
| `codeBase` | `dependencyType`属性がに設定されている場合に必要です `install` 。 依存アセンブリへのパス。 絶対パス、またはマニフェストのコードベースを基準とした相対パスのいずれかを指定できます。 このパスは、アセンブリマニフェストが有効であるために有効な URI である必要があります。 |
| `size` | `dependencyType`属性がに設定されている場合に必要です `install` 。 依存アセンブリのサイズ (バイト単位)。 |

### <a name="assemblyidentity"></a>assemblyIdentity
 必須。 この要素は `dependentAssembly` 要素の子であり、以下の属性があります。

|属性|説明|
|---------------|-----------------|
|`name`|必須。 アプリケーションの名前を識別します。|
|`version`|必須。 アプリケーションのバージョン番号を次の形式で指定します。 `major.minor.build.revision`|
|`publicKeyToken`|省略可能。 `SHA-1`アプリケーションまたはアセンブリに署名するときに使用する公開キーのハッシュ値の最後の8バイトを表す16文字の16進数文字列を指定します。 カタログの署名に使用される公開キーは、2048ビット以上である必要があります。|
|`processorArchitecture`|省略可能。 プロセッサを指定します。 有効な値は、 `x86` 32 ビット windows の場合は、 `I64` 64 ビット版の場合はです。|
|`language`|省略可能。 アセンブリの2つの部分言語コード (EN-US など) を識別します。|

### <a name="hash"></a>hash
 要素は、 `hash` 要素の省略可能な子です `assemblyIdentity` 。 `hash` 要素に属性はありません。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] は、アプリケーション内のすべてのファイルのアルゴリズムハッシュをセキュリティチェックとして使用して、展開後にファイルが変更されていないことを確認します。 `hash`要素が含まれていない場合、このチェックは実行されません。 そのため、要素を省略する `hash` ことは推奨されません。

### <a name="dsigtransforms"></a>dsig:Transforms
 要素は、 `dsig:Transforms` 要素の必須の子です `hash` 。 `dsig:Transforms` 要素に属性はありません。

### <a name="dsigtransform"></a>dsig:Transform
 要素は、 `dsig:Transform` 要素の必須の子です `dsig:Transforms` 。 `dsig:Transform` 要素には、次の属性があります。

| 属性 | [説明] |
|-------------| - |
| `Algorithm` | このファイルのダイジェストの計算に使用されるアルゴリズム。 現在、で使用されている値 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] はのみ `urn:schemas-microsoft-com:HashTransforms.Identity` です。 |

### <a name="dsigdigestmethod"></a>dsig: DigestMethod
 要素は、 `dsig:DigestMethod` 要素の必須の子です `hash` 。 `dsig:DigestMethod` 要素には、次の属性があります。

| 属性 | [説明] |
|-------------| - |
| `Algorithm` | このファイルのダイジェストの計算に使用されるアルゴリズム。 現在、で使用されている値 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] はのみ `http://www.w3.org/2000/09/xmldsig#sha1` です。 |

### <a name="dsigdigestvalue"></a>dsig:DigestValue
 要素は、 `dsig:DigestValue` 要素の必須の子です `hash` 。 `dsig:DigestValue` 要素に属性はありません。 テキスト値は、指定されたファイルの計算済みハッシュです。

## <a name="remarks"></a>Remarks
 アプリケーションで使用されるすべてのアセンブリには、対応する要素が必要 `dependency` です。 依存アセンブリには、プラットフォームアセンブリとしてグローバルアセンブリキャッシュにプレインストールする必要があるアセンブリは含まれません。

## <a name="example"></a>例
 次のコード例は、 `dependency` アプリケーションマニフェストの要素を示してい [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。 このコード例は、 [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md) トピック用に用意されている、より大きな例の一部です。

```xml
<dependency>
  <dependentOS>
    <osVersionInfo>
      <os
        majorVersion="4"
        minorVersion="10"
        buildNumber="0"
        servicePackMajor="0" />
    </osVersionInfo>
  </dependentOS>
</dependency>
<dependency>
  <dependentAssembly
    dependencyType="preRequisite"
    allowDelayedBinding="true">
    <assemblyIdentity
      name="Microsoft.Windows.CommonLanguageRuntime"
      version="4.0.20506.0" />
  </dependentAssembly>
</dependency>

<dependency>
  <dependentAssembly
    dependencyType="install"
    allowDelayedBinding="true"
    codebase="MyApplication.exe"
    size="4096">
    <assemblyIdentity
      name="MyApplication"
      version="1.0.0.0"
      language="neutral"
      processorArchitecture="x86" />
    <hash>
      <dsig:Transforms>
        <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />
      </dsig:Transforms>
      <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
      <dsig:DigestValue>DpTW7RzS9IeT/RBSLj54vfTEzNg=</dsig:DigestValue>
    </hash>
  </dependentAssembly>
</dependency>
```

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md)
- [\<dependency> element](../deployment/dependency-element-clickonce-deployment.md)