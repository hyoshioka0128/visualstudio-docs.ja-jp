---
title: IManagedAddin::Load
ms.date: 02/02/2017
ms.topic: interface
dev_langs:
- VB
- CSharp
helpviewer_keywords: ''
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 1307d720e005855770ee68659374dbbfae247d65
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85541038"
---
# <a name="imanagedaddinload"></a>IManagedAddin::Load
  管理対象の VSTO アドインが読み込まれるときに呼び出されます。

## <a name="syntax"></a>構文

```csharp
HRESULT Load([in] BSTR bstrManifestURL,
             [in] IDispatch *pdispApplication);
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------------|-----------------|
|*bstrManifestURL*|VSTO アドインのマニフェストの完全なパス。|
|*pdispApplication*|VSTO アドインを読み込んでいるホストアプリケーションを表す IDispatch へのポインター。|

## <a name="return-value"></a>戻り値
 メソッドが正常に完了したかどうかを示す HRESULT 値。

## <a name="remarks"></a>Remarks
 マニフェストは、VSTO アドインの読み込みに使用される情報を提供するファイル (通常は XML ファイル) です。 たとえば、マニフェストには、VSTO アドイン アセンブリの場所や、VSTO アドインが読み込まれるときにインスタンス化するエントリ ポイント クラスを指定できます。

 *Bstrmanifesturl*パラメーターには、 `Manifest` VSTO アドインの**HKEY_CURRENT_USER \software\microsoft\office \\ _\<application name>_ \ Addins \\ _\<add-in ID>_ **レジストリキーの下にあるエントリの値が含まれます。 詳細については、「 [IManagedAddin インターフェイス](../vsto/imanagedaddin-interface.md)」を参照してください。

 読み込まれる VSTO アドインのアプリケーション ドメインやセキュリティ ポリシーの構成などのタスクを実行するように、 [IManagedAddIn::Load](../vsto/imanagedaddin-load.md) メソッドを実装します。

## <a name="see-also"></a>関連項目
- [IManagedAddin Interface](../vsto/imanagedaddin-interface.md)
- [IManagedAddin::Unload](../vsto/imanagedaddin-unload.md)
