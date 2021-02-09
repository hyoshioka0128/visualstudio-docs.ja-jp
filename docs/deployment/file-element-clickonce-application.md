---
title: '&lt;file &gt; 要素 (ClickOnce アプリケーション) |Microsoft Docs'
description: File 要素は、アプリケーションによってダウンロードおよび使用されるアセンブリ以外のすべてのファイルを識別します。 File 要素は省略可能です。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://www.w3.org/2000/09/xmldsig#Transform
- urn:schemas-microsoft-com:asm.v2#file
- http://www.w3.org/2000/09/xmldsig#DigestValue
- http://www.w3.org/2000/09/xmldsig#DigestMethod
- http://www.w3.org/2000/09/xmldsig#Transforms
- urn:schemas-microsoft-com:asm.v2#hash
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <file> element [ClickOnce application manifest]
- manifests [ClickOnce], file element
ms.assetid: 56e3490c-eed5-4841-b1bf-eefe778b6ac9
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 8ad19de19176b7c8ee1d2c2872126a19abb93b67
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99895090"
---
# <a name="ltfilegt-element-clickonce-application"></a>&lt;file &gt; 要素 (ClickOnce アプリケーション)
アプリケーションによってダウンロードおよび使用されるアセンブリ以外のすべてのファイルを識別します。

## <a name="syntax"></a>構文

```xml
<file
    name
    size
    group
    optional
    writeableType
>
    <typelib
        tlbid
        version
        helpdir
        resourceid
        flags
    />
    <comClass
        clsid
        description
        threadingModel
        tlbid
        progid
        miscStatus
        miscStatusIcon
        miscStatusContent
        miscStatusDocPrint
        miscStatusThumbnail
    />
    <comInterfaceExternalProxyStub
        iid
        baseInterface
        numMethods
        name
        tlbid
        proxyStubClass32
    />
    <comInterfaceProxyStub
        iid
        baseInterface
        numMethods
        name
        tlbid
        proxyStubClass32
    />
    <windowClass
        versioned
    />
</file>
```

## <a name="elements-and-attributes"></a>要素と属性
 `file` 要素は省略可能です。 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`name`|必須。 ファイルの名前を識別します。|
|`size`|必須。 ファイルのサイズをバイト単位で指定します。|
|`group`|属性が指定されていない場合、またはに設定されている場合は省略可能 `optional` `false` 。がの場合は必須。 `optional` `true` このファイルが属するグループの名前。 名前には、開発者が選択した任意の Unicode 文字列値を使用できます。また、クラスを使用して必要に応じてファイルをダウンロードするために使用され <xref:System.Deployment.Application.ApplicationDeployment> ます。|
|`optional`|任意。 アプリケーションの初回実行時にこのファイルをダウンロードする必要があるかどうか、またはアプリケーションが要求時にファイルをサーバーにのみ配置するかどうかを指定します。 `false`または未定義の場合、アプリケーションを最初に実行またはインストールしたときに、ファイルがダウンロードされます。 の場合 `true` 、 `group` アプリケーションマニフェストが有効であるためにを指定する必要があります。 `optional``writeableType`が値と共に指定されている場合、を true にすることはできません `applicationData` 。|
|`writeableType`|任意。 このファイルがデータファイルであることを指定します。 現在、有効値は `applicationData` のみです。|

## <a name="typelib"></a>typelib
 要素は、 `typelib` file 要素の省略可能な子です。 要素は、COM コンポーネントに属するタイプライブラリを記述します。 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`tlbid`|必須。 タイプライブラリに割り当てられた GUID。|
|`version`|必須。 タイプライブラリのバージョン番号。|
|`helpdir`|必須。 コンポーネントのヘルプファイルが格納されているディレクトリ。 長さをゼロにすることができます。|
|`resourceid`|任意。 ロケール識別子 (LCID) の16進数文字列形式。 これは、0x プレフィックスのない 1 ~ 4 桁の16進数で、先頭に0を付けません。 LCID にニュートラルサブ言語識別子が含まれている場合があります。|
|`flags`|任意。 このタイプライブラリのタイプライブラリフラグの文字列形式。 具体的には、"RESTRICTED"、"CONTROL"、"HIDDEN"、および "HASDISKIMAGE" のいずれかである必要があります。|

## <a name="comclass"></a>comClass
 要素は、 `comClass` 要素の省略可能な子です `file` が、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 登録を必要としない com を使用して配置する com コンポーネントがアプリケーションに含まれている場合は必須です。 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`clsid`|必須。 GUID として表される COM コンポーネントのクラス ID。|
|`description`|任意。 クラス名。|
|`threadingModel`|任意。 インプロセス COM クラスによって使用されるスレッドモデル。 このプロパティが null の場合、スレッドモデルは使用されません。 コンポーネントはクライアントのメインスレッドで作成され、他のスレッドからの呼び出しはこのスレッドにマーシャリングされます。 有効な値を次の一覧に示します。<br /><br /> `Apartment`、`Free`、`Both`、`Neutral`。|
|`tlbid`|任意。 この COM コンポーネントのタイプライブラリの GUID。|
|`progid`|任意。 COM コンポーネントに関連付けられているバージョン依存のプログラム識別子。 の形式 `ProgID` は `<vendor>.<component>.<version>` です。|
|`miscStatus`|任意。 レジストリキーによって提供される情報をアセンブリマニフェスト内で複製し `MiscStatus` ます。 `miscStatusIcon`、、 `miscStatusContent` 、または属性の値が見つからない場合は、 `miscStatusDocprint` `miscStatusThumbnail` に示されている対応する既定値が、不足している `miscStatus` 属性に使用されます。 値には、次の表に示す属性値のコンマ区切りの一覧を指定できます。 COM クラスがレジストリキー値を必要とする OCX クラスの場合は、この属性を使用でき `MiscStatus` ます。|
|`miscStatusIcon`|任意。 DVASPECT_ICON によって提供される情報をアセンブリマニフェスト内で複製します。 オブジェクトのアイコンが用意されています。 値には、次の表に示す属性値のコンマ区切りの一覧を指定できます。 COM クラスがレジストリキー値を必要とする OCX クラスの場合は、この属性を使用でき `Miscstatus` ます。|
|`miscStatusContent`|任意。 DVASPECT_CONTENT によって提供される情報をアセンブリマニフェスト内で複製します。 画面またはプリンターに表示される複合ドキュメントを提供できます。 値には、次の表に示す属性値のコンマ区切りの一覧を指定できます。 COM クラスがレジストリキー値を必要とする OCX クラスの場合は、この属性を使用でき `MiscStatus` ます。|
|`miscStatusDocPrint`|任意。 DVASPECT_DOCPRINT によって提供される情報をアセンブリマニフェスト内で複製します。 プリンターに印刷されるかのように、画面に表示されるオブジェクト表現を提供できます。 値には、次の表に示す属性値のコンマ区切りの一覧を指定できます。 COM クラスがレジストリキー値を必要とする OCX クラスの場合は、この属性を使用でき `MiscStatus` ます。|
|`miscStatusThumbnail`|任意。 DVASPECT_THUMBNAIL によって提供される情報をアセンブリマニフェスト内で複製します。 参照ツールで表示できるオブジェクトのサムネイルを提供できます。 値には、次の表に示す属性値のコンマ区切りの一覧を指定できます。 COM クラスがレジストリキー値を必要とする OCX クラスの場合は、この属性を使用でき `MiscStatus` ます。|

## <a name="cominterfaceexternalproxystub"></a>comInterfaceExternalProxyStub
 要素は、 `comInterfaceExternalProxyStub` 要素の省略可能な子です `file` が、登録を必要としない [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] com を使用して配置する com コンポーネントがアプリケーションに含まれている場合に必要になることがあります。 要素には、次の属性が含まれています。

|属性|説明|
|---------------|-----------------|
|`iid`|必須。 このプロキシによって提供されるインターフェイス ID (IID)。 IID の周囲には中かっこが必要です。|
|`baseInterface`|任意。 によって参照されるインターフェイスの派生元であるインターフェイスの IID `iid` 。|
|`numMethods`|任意。 インターフェイスによって実装されたメソッドの数。|
|`name`|任意。 コードに表示されるインターフェイスの名前。|
|`tlbid`|任意。 属性によって指定されたインターフェイスの説明を含むタイプライブラリ `iid` 。|
|`proxyStubClass32`|任意。 IID を32ビットプロキシ Dll の CLSID にマップします。|

## <a name="cominterfaceproxystub"></a>comInterfaceProxyStub
 要素は、 `comInterfaceProxyStub` 要素の省略可能な子です `file` が、登録を必要としない [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] com を使用して配置する com コンポーネントがアプリケーションに含まれている場合に必要になることがあります。 要素には、次の属性が含まれています。

|属性|説明|
|---------------|-----------------|
|`iid`|必須。 このプロキシによって提供されるインターフェイス ID (IID)。 IID の周囲には中かっこが必要です。|
|`baseInterface`|任意。 によって参照されるインターフェイスの派生元であるインターフェイスの IID `iid` 。|
|`numMethods`|任意。 インターフェイスによって実装されたメソッドの数。|
|`Name`|任意。 コードに表示されるインターフェイスの名前。|
|`Tlbid`|任意。 属性によって指定されたインターフェイスの説明を含むタイプライブラリ `iid` 。|
|`proxyStubClass32`|任意。 IID を32ビットプロキシ Dll の CLSID にマップします。|
|`threadingModel`|任意。 任意。 インプロセス COM クラスによって使用されるスレッドモデル。 このプロパティが null の場合、スレッドモデルは使用されません。 コンポーネントはクライアントのメインスレッドで作成され、他のスレッドからの呼び出しはこのスレッドにマーシャリングされます。 有効な値を次の一覧に示します。<br /><br /> `Apartment`、`Free`、`Both`、`Neutral`。|

## <a name="windowclass"></a>windowClass
 要素は、 `windowClass` 要素の省略可能な子です `file` が、登録を必要としない [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] com を使用して配置する com コンポーネントがアプリケーションに含まれている場合に必要になることがあります。 要素は、バージョンが適用されている必要のある COM コンポーネントによって定義されたウィンドウクラスを参照します。 要素には、次の属性が含まれています。

|属性|説明|
|---------------|-----------------|
|`versioned`|任意。 登録に使用される内部ウィンドウクラスの名前に、ウィンドウクラスを含むアセンブリのバージョンが含まれているかどうかを制御します。 この属性の値には、 `yes` またはを指定でき `no` ます。 既定値は、`yes` です。 値を `no` 使用できるのは、同じウィンドウクラスがサイドバイサイドコンポーネントと同等ではないコンポーネントによって定義されていて、それらを同じウィンドウクラスとして扱う場合だけです。 ウィンドウクラスの登録に関する通常の規則が適用されることに注意してください。ウィンドウクラスを登録する最初のコンポーネントのみが、バージョンが適用されていないため、登録できます。|

## <a name="hash"></a>hash
 要素は、 `hash` 要素の省略可能な子です `file` 。 `hash` 要素に属性はありません。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] は、アプリケーション内のすべてのファイルのアルゴリズムハッシュをセキュリティチェックとして使用して、展開後にファイルが変更されていないことを確認します。 `hash`要素が含まれていない場合、このチェックは実行されません。 そのため、要素を省略する `hash` ことは推奨されません。

 ハッシュされていないファイルがマニフェストに含まれている場合、ユーザーはハッシュされていないファイルの内容を確認できないため、そのマニフェストにデジタル署名することはできません。

## <a name="dsigtransforms"></a>dsig:Transforms
 要素は、 `dsig:Transforms` 要素の必須の子です `hash` 。 `dsig:Transforms` 要素に属性はありません。

## <a name="dsigtransform"></a>dsig:Transform
 要素は、 `dsig:Transform` 要素の必須の子です `dsig:Transforms` 。 `dsig:Transform` 要素には、次の属性があります。

| 属性 | 説明 |
|-------------| - |
| `Algorithm` | このファイルのダイジェストの計算に使用されるアルゴリズム。 現在、で使用されている値 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] はのみ `urn:schemas-microsoft-com:HashTransforms.Identity` です。 |

## <a name="dsigdigestmethod"></a>dsig: DigestMethod
 要素は、 `dsig:DigestMethod` 要素の必須の子です `hash` 。 `dsig:DigestMethod` 要素には、次の属性があります。

| 属性 | 説明 |
|-------------| - |
| `Algorithm` | このファイルのダイジェストの計算に使用されるアルゴリズム。 現在、で使用されている値 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] はのみ `http://www.w3.org/2000/09/xmldsig#sha1` です。 |

## <a name="dsigdigestvalue"></a>dsig:DigestValue
 要素は、 `dsig:DigestValue` 要素の必須の子です `hash` 。 `dsig:DigestValue` 要素に属性はありません。 テキスト値は、指定されたファイルの計算済みハッシュです。

## <a name="remarks"></a>解説
 この要素は、アプリケーションを構成するすべての非アセンブリファイルと、特にファイル検証のハッシュ値を識別します。 この要素には、ファイルに関連付けられているコンポーネントオブジェクトモデル (COM) 分離データを含めることもできます。 ファイルが変更された場合は、アプリケーションマニフェストファイルを更新して変更を反映する必要もあります。

## <a name="example"></a>例
 次のコード例は、 `file` を使用して配置されたアプリケーションのアプリケーションマニフェストの要素を示してい [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。

```xml
<file name="Icon.ico" size="9216">
  <hash>
    <dsig:Transforms>
      <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />
    </dsig:Transforms>
    <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
    <dsig:DigestValue>lVoj+Rh6RQ/HPNLOdayQah5McrI=</dsig:DigestValue>
  </hash>
</file>
```

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md)