---
title: '&lt;dependency &gt; 要素 (ClickOnce 配置) |Microsoft Docs'
description: Dependency 要素は、インストールするアプリケーションのバージョンと、アプリケーションマニフェストの場所を指定します。
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
- <dependency> element [ClickOnce deployment manifest]
ms.assetid: 9b4d2082-0347-4922-ac70-85f11b913039
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 09e5973b39bae2fbf923cf97ac1bd9cf15e10874
ms.sourcegitcommit: 023f52f10fb91850824558478cbfd2ec965054f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94407680"
---
# <a name="ltdependencygt-element-clickonce-deployment"></a>&lt;dependency &gt; 要素 (ClickOnce 配置)
インストールするアプリケーションのバージョンと、アプリケーションマニフェストの場所を指定します。

## <a name="syntax"></a>構文

```xml

      <dependency>
   <dependentAssembly
      preRequisite
      visible
      dependencyType
      codeBase
      size
   >
      <assemblyIdentity
         name
         version
         publicKeyToken
         processorArchitecture
         language
         type
      />
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

   </dependentAssembly>
</dependency>
```

## <a name="elements-and-attributes"></a>要素と属性
 `dependency` 要素は必須です。 属性はありません。 配置マニフェストには、複数の要素を含めることができ `dependency` ます。

 要素は、 `dependency` 通常、アプリケーション内に含まれるアセンブリのメインアプリケーションの依存関係を表し [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。 Main.exe アプリケーションが DotNetAssembly.dll というアセンブリを使用する場合は、そのアセンブリを依存関係セクションに一覧表示する必要があります。 ただし、依存関係は、特定のバージョンの共通言語ランタイムの依存関係、グローバルアセンブリキャッシュ (GAC) 内のアセンブリ、COM オブジェクトなど、他の種類の依存関係を表現することもできます。 このような [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 種類の依存関係のダウンロードとインストールを開始することはできませんが、指定された依存関係のうち1つ以上が存在しない場合は、アプリケーションが実行されません。

## <a name="dependentassembly"></a>dependentAssembly
 必須。 この要素には要素が含まれてい `assemblyIdentity` ます。 次の表は、がサポートする属性を示して `dependentAssembly` います。

| 属性 | 説明 |
|------------------| - |
| `preRequisite` | 省略可能。 このアセンブリが既に GAC に存在する必要があることを指定します。 有効な値は `true` と `false` です。 `true`、および指定されたアセンブリが GAC に存在しない場合、アプリケーションの実行は失敗します。 |
| `visible` | 省略可能。 最上位レベルのアプリケーション id (依存関係を含む) を識別します。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]アプリケーションのストレージとアクティブ化を管理するために、によって内部的に使用されます。 |
| `dependencyType` | 必須。 この依存関係とアプリケーションの関係。 有効な値は次のとおりです。<br /><br /> -   `install`. コンポーネントは、現在のアプリケーションとは別のインストールを表します。<br />-   `preRequisite`. 現在のアプリケーションではコンポーネントが必要です。 |
| `codebase` | 省略可能。 アプリケーションマニフェストへの完全パス。 |
| `size` | 省略可能。 アプリケーションマニフェストのサイズ (バイト単位)。 |

## <a name="assemblyidentity"></a>assemblyIdentity
 必須。 この要素は `dependentAssembly` 要素の子です。 の内容は、 `assemblyIdentity` アプリケーションマニフェストに記述されているものと同じである必要があり [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。 要素の属性を次の表に示し `assemblyIdentity` ます。

|属性|説明|
|---------------|-----------------|
|`Name`|必須。 アプリケーションの名前を識別します。|
|`Version`|必須。 アプリケーションのバージョン番号を次の形式で指定します。 `major.minor.build.revision`|
|`publicKeyToken`|必須。 アプリケーションまたはアセンブリに署名するときに使用する公開キーの SHA-1 ハッシュの最後の8バイトを表す16文字の16進数文字列を指定します。 署名に使用する公開キーは、2048ビット以上である必要があります。|
|`processorArchitecture`|必須。 マイクロプロセッサを指定します。 有効な値は、 `x86` 32 ビット windows の場合は、 `IA64` 64 ビット版の場合はです。|
|`Language`|省略可能。 アセンブリの2つの部分言語コードを識別します。 たとえば、EN-US は英語 (U.S.) を表します。 既定値は、`neutral` です。 この要素は `asmv2` 名前空間にあります。|
|`type`|省略可能。 Windows サイドバイサイドインストールテクノロジとの下位互換性のために使用します。 使用できる値はのみ `win32` です。|

## <a name="hash"></a>hash
 要素は、 `hash` 要素の省略可能な子です `file` 。 `hash` 要素に属性はありません。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] は、アプリケーション内のすべてのファイルのアルゴリズムハッシュをセキュリティチェックとして使用して、展開後にファイルが変更されていないことを確認します。 `hash`要素が含まれていない場合、このチェックは実行されません。 そのため、要素を省略する `hash` ことは推奨されません。

## <a name="dsigtransforms"></a>dsig:Transforms
 要素は、 `dsig:Transforms` 要素の必須の子です `hash` 。 `dsig:Transforms` 要素に属性はありません。

## <a name="dsigtransform"></a>dsig:Transform
 要素は、 `dsig:Transform` 要素の必須の子です `dsig:Transforms` 。 要素の属性を次の表に示し `dsig:Transform` ます。

| 属性 | [説明] |
|-------------| - |
| `Algorithm` | このファイルのダイジェストの計算に使用されるアルゴリズム。 現在、で使用されている値 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] はのみ `urn:schemas-microsoft-com:HashTransforms.Identity` です。 |

## <a name="dsigdigestmethod"></a>dsig: DigestMethod
 要素は、 `dsig:DigestMethod` 要素の必須の子です `hash` 。 要素の属性を次の表に示し `dsig:DigestMethod` ます。

| 属性 | [説明] |
|-------------| - |
| `Algorithm` | このファイルのダイジェストの計算に使用されるアルゴリズム。 現在、で使用されている値 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] はのみ `http://www.w3.org/2000/09/xmldsig#sha1` です。 |

## <a name="dsigdigestvalue"></a>dsig:DigestValue
 要素は、 `dsig:DigestValue` 要素の必須の子です `hash` 。 `dsig:DigestValue` 要素に属性はありません。 テキスト値は、指定されたファイルの計算済みハッシュです。

## <a name="remarks"></a>Remarks
 配置マニフェストには、通常、 `assemblyIdentity` アプリケーションマニフェストの名前とバージョンを識別する1つの要素があります。

## <a name="example-1"></a>例 1
 次のコード例は、 `dependency` 配置マニフェストの要素を示して [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] います。

```xml
<!-- Identify the assembly dependencies -->
<dependency>
  <dependentAssembly dependencyType="install" allowDelayedBinding="true" codebase="MyApplication.exe" size="16384">
    <assemblyIdentity name="MyApplication" version="0.0.0.0" cultural="neutral" processorArchitecture="msil" />
    <hash>
      <dsig:Transforms>
        <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />
      </dsig:Transforms>
      <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
       <dsig:DigestValue>YzXYZJAvj9pgAG3y8jXUjC7AtHg=</dsig:DigestValue>
    </hash>
  </dependentAssembly>
</dependency>
```

## <a name="example-2"></a>例 2
 GAC に既にインストールされているアセンブリに対する依存関係を指定するコード例を次に示します。

```xml
<dependency>
  <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true">
    <assemblyIdentity name="GACAssembly" version="1.0.0.0" language="neutral" processorArchitecture="msil" />
  </dependentAssembly>
</dependency>
```

## <a name="example-3"></a>例 3
 共通言語ランタイムの特定のバージョンに対する依存関係を指定するコード例を次に示します。

```xml
<dependency>
  <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true">
    <assemblyIdentity name="Microsoft.Windows.CommonLanguageRuntime" version="2.0.50215.0" />
  </dependentAssembly>
</dependency>
```

## <a name="example-4"></a>例 4
 オペレーティングシステムの依存関係を指定するコード例を次に示します。

```xml
<dependency>
   <dependentOS supportUrl="http://www.microsoft.com" description="Microsoft Windows Operating System">
      <osVersionInfo>
         <os majorVersion="4" minorVersion="10" />
      </osVersionInfo>
   </dependentOS>
</dependency>
```

## <a name="see-also"></a>関連項目
- [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)
- [\<dependency> element](../deployment/dependency-element-clickonce-application.md)