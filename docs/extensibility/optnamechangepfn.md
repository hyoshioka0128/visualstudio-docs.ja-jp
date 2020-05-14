---
title: オプトネームチェンジプフン |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- OPTNAMECHANGEPFN
helpviewer_keywords:
- OPTNAMECHANGEPFN callback function
ms.assetid: 147303f3-c7f1-438a-81b7-db891ea3d076
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 603bd08c1ec3832bf732e0b33101076738d009e3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702247"
---
# <a name="optnamechangepfn"></a>OPTNAMECHANGEPFN
これは[、SccSetOption](../extensibility/sccsetoption-function.md) (オプション`SCC_OPT_NAMECHANGEPFN`を使用) の呼び出しで指定されたコールバック関数で、ソース管理プラグインによって行われた名前の変更を IDE に伝えるために使用されます。

## <a name="signature"></a>署名

```cpp
typedef void (*OPTNAMECHANGEPFN)(
   LPVOID pvCallerData,
   LPCSTR pszOldName,
   LPCSTR pszNewName
);
```

## <a name="parameters"></a>パラメーター
 呼び出し元データ

[in][SccSetOption](../extensibility/sccsetoption-function.md) (オプション`SCC_OPT_USERDATA`を使用して) の前の呼び出しで指定されたユーザー値。

 名前

[in]ファイルの元の名前。

 名前を変更します。

[in]ファイルの名前が変更されました。

## <a name="return-value"></a>戻り値
 [なし] :

## <a name="remarks"></a>Remarks
 ソース管理操作中にファイルの名前が変更された場合、ソース管理プラグインはこのコールバックを通じて名前の変更を IDE に通知できます。

 IDE がこのコールバックをサポートしていない場合、それを指定するために[SccSetOption を](../extensibility/sccsetoption-function.md)呼び出しません。 プラグインがこのコールバックをサポートしていない場合、IDE がコールバックを`SCC_E_OPNOTSUPPORTED``SccSetOption`設定しようとすると、関数から返されます。

## <a name="see-also"></a>関連項目
- [IDE によって実装されるコールバック関数](../extensibility/callback-functions-implemented-by-the-ide.md)
- [SccSetOption](../extensibility/sccsetoption-function.md)
