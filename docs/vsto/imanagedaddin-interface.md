---
title: IManagedAddin インターフェイス
description: マネージ VSTO アドインを読み込むコンポーネントを作成するには、IManagedAddin インターフェイスを実装します。
ms.date: 02/02/2017
ms.topic: interface
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- IManagedAddin interface
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 614cf7e8d0e682d894328fb764c6d64b855d2834
ms.sourcegitcommit: 8590cf6b3351e82827fd21159beefef0c02bf162
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2021
ms.locfileid: "102469789"
---
# <a name="imanagedaddin-interface"></a>IManagedAddin インターフェイス
  マネージ VSTO アドインを読み込むコンポーネントを作成するには、IManagedAddin インターフェイスを実装します。このインターフェイスは、2007 Microsoft Office システムに追加されました。

## <a name="syntax"></a>構文

```csharp
[
    object,
    uuid(B9CEAB65-331C-4713-8410-DDDAF8EC191A),
    pointer_default(unique),
    oleautomation
]
interface IManagedAddin : IUnknown
{
    HRESULT Load(
        [in] BSTR bstrManifestURL,
        [in] IDispatch *pdispApplication);
    HRESULT Unload();
};
```

## <a name="methods"></a>メソッド
 次の表に、IManagedAddin インターフェイスによって定義されるメソッドの一覧を示します。

|名前|説明|
|----------|-----------------|
|[IManagedAddin::Load](../vsto/imanagedaddin-load.md)|Microsoft Office アプリケーションがマネージド VSTO アドインを読み込むときに呼び出されます。|
|[IManagedAddin::Unload](../vsto/imanagedaddin-unload.md)|Microsoft Office アプリケーションがマネージド VSTO アドインをアンロードする直前に呼び出されます。|

## <a name="remarks"></a>解説
 2007 Microsoft Office システムから Microsoft Office アプリケーションでは、IManagedAddin インターフェイスを使用して Office VSTO アドインを読み込むことができます。IManagedAddin インターフェイスを実装して、VSTO アドインローダー (*VSTOLoader.dll*) およびを使用する代わりに、マネージ vsto アドイン用の独自の vsto アドインローダーとランタイムを作成でき [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ます。 詳細については、「 [Architecture of VSTO Add-ins](../vsto/architecture-of-vsto-add-ins.md)」を参照してください。

## <a name="how-managed-add-ins-are-loaded"></a>マネージアドインの読み込み方法
 アプリケーションが起動すると、次の処理が行われます。

1. アプリケーションによって、次のレジストリ キーにあるエントリが検索され、VSTO アドインが検出されます。

    **HKEY_CURRENT_USER\Software\Microsoft\Office\\ *\<application name>* \ Addins\\**

    このレジストリ キーにある各エントリは、VSTO アドインの一意な ID です。 通常、これは VSTO アドイン アセンブリの名前です。

2. アプリケーションによって、各 VSTO アドイン エントリにある `Manifest` エントリが検索されます。

    マネージ VSTO アドインでは、マニフェストの完全なパスを `Manifest` **HKEY_CURRENT_USER\Software\Microsoft\Office\\ _\<application name>_ \\ _\<add-in ID>_** の下のエントリに格納できます。 マニフェストは、VSTO アドインの読み込みに使用される情報を提供するファイル (通常は XML ファイル) です。

3. アプリケーションによって `Manifest` エントリが検出されると、そのアプリケーションはマネージド VSTO アドイン ローダー コンポーネントの読み込みを試みます。 このアプリケーションでは、IManagedAddin インターフェイスを実装する COM オブジェクトを作成しようとします。

    には、 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] VSTO アドインローダーコンポーネント (*VSTOLoader.dll*) が含まれています。または、IManagedAddin インターフェイスを実装して独自のアドインローダーコンポーネントを作成することもできます。

4. アプリケーションによって [IManagedAddin::Load](../vsto/imanagedaddin-load.md) メソッドが呼び出され、 `Manifest` エントリの値に渡されます。

5. [IManagedAddin::Load](../vsto/imanagedaddin-load.md) メソッドによって、読み込む VSTO アドイン用のアプリケーション ドメインやセキュリティ ポリシーの構成など、VSTO アドイン読み込みに必要なタスクが実行されます。

   マネージ VSTO アドインの検出と読み込みに Microsoft Office アプリケーションが使用するレジストリキーの詳細については、「 [Vsto アドインのレジストリエントリ](../vsto/registry-entries-for-vsto-add-ins.md)」を参照してください。

## <a name="guidance-to-implement-imanagedaddin"></a>IManagedAddin を実装するためのガイダンス
 IManagedAddin を実装する場合は、次の CLSID を使用して、実装を含む DLL を登録する必要があります。

 99D651D7-5F7C-470E-8A3B-774D5D9536AC

 Microsoft Office アプリケーションは、この CLSID を使用して、IManagedAddin を実装する COM オブジェクトを作成します。

> [!CAUTION]
> この CLSID は、の *VSTOLoader.dll* によっても使用され [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ます。 そのため、IManagedAddin を使用して独自の VSTO アドインローダーとランタイムコンポーネントを作成する場合、に依存する VSTO アドインを実行しているコンピューターにコンポーネントを配置することはできません [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 。

## <a name="see-also"></a>関連項目
- [Visual Studio での Office 開発 &#40;アンマネージ API リファレンス&#41;](../vsto/unmanaged-api-reference-office-development-in-visual-studio.md)
