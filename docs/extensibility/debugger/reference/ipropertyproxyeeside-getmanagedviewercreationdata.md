---
title: を指定します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide::GetManagedViewerCreationData
helpviewer_keywords:
- IPropertyProxyEESide::GetManagedViewerCreationData
ms.assetid: c4eb4d60-8816-4d52-bc8d-dffd4f066499
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2e72922b348c8744f10037e199e93f735ff4be8e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714960"
---
# <a name="ipropertyproxyeesidegetmanagedviewercreationdata"></a>IPropertyProxyEESide::GetManagedViewerCreationData
このビューワーをインスタンス化するために、このプロパティの種類のビューアーに関する情報を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetManagedViewerCreationData(
   BSTR*                  assemName,
   IEEDataStorage**       assemBytes,
   IEEDataStorage**       assemPdb,
   BSTR*                  className,
   ASSEMBLYLOCRESOLUTION* alr,
   BOOL*                  replacementOk
);
```

```csharp
int GetManagedViewerCreationData(
   out string                     assemName,
   out IEEDataStorage             assemBytes,
   out IEEDataStorage             assemPdb,
   out string                     className,
   out enum_ASSEMBLYLOCRESOLUTION alr,
   out int                        replacementOk
);
```

## <a name="parameters"></a>パラメーター
`assemName`\
[アウト]このオブジェクトを保持しているアセンブリの名前を返します。

`assemBytes`\
[アウト]このオブジェクトのアセンブリ バイトを含む[IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)オブジェクトを返します (使用できるバイトがない場合は null 値です)。

`assemPdb`\
[アウト]このオブジェクト`IEEDataStorage`のシンボル ストア情報を含むオブジェクトを返します (シンボル ストアが使用できない場合は null 値)。

`className`\
[アウト]このオブジェクトを含むクラス名を返します。

`alr`\
[アウト]アセンブリの場所を示す[値をアセンブリの LOCRESOLUTION](../../../extensibility/debugger/reference/assemblylocresolution.md)列挙体から返します。

`replacementOk`\
[アウト]このオブジェクトの値`TRUE`を変更できる場合は、ゼロ以外の値 ( ) を返します。オブジェクトが`FALSE`読み取り専用の場合は、0 ( ) を返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドは、マネージ ビューアーをインスタンス化するために型ビジュアライザーによって使用されます。

## <a name="see-also"></a>関連項目
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [ASSEMBLYLOCRESOLUTION](../../../extensibility/debugger/reference/assemblylocresolution.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
