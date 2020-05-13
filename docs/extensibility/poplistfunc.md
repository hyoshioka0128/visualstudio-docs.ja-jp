---
title: ポップリストファンク |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- POPDIRLISTFUNC
helpviewer_keywords:
- POPLISTFUNC callback function
ms.assetid: b2199fd5-d707-4628-92dd-e2a01e2f507a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6c5f8c1683a993915476ff23f1f5d5f2c2aba462
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702063"
---
# <a name="poplistfunc"></a>POPLISTFUNC
このコールバックは、IDE によって[SccPopulateList](../extensibility/sccpopulatelist-function.md)に提供され、ソース管理プラグインがファイルまたはディレクトリのリストを更新するために使用されます (`SccPopulateList`関数にも提供されます)。

 IDE でユーザーが **[取得**] コマンドを選択すると、IDE にユーザーが取得できるすべてのファイルのリスト ボックスが表示されます。 残念ながら、IDE は、ユーザーが取得する可能性のあるすべてのファイルの正確なリストを認識していません。このリストはプラグインのみに含まれます。 他のユーザーがソース コード管理プロジェクトにファイルを追加した場合、これらのファイルは一覧に表示されますが、IDE はファイルを認識しません。 IDE は、ユーザーが取得できると思うファイルのリストを作成します。 このリストをユーザーに表示する前に、ソース管理プラグインがリストに対してファイルを追加および削除する機会を与える[SccPopulateList](../extensibility/sccpopulatelist-function.md)`,`を呼び出します。

## <a name="signature"></a>署名
 ソース管理プラグインは、IDE 実装関数を呼び出して、次のプロトタイプを使用してリストを変更します。

```cpp
typedef BOOL (*POPLISTFUNC) (
   LPVOID pvCallerData,
   BOOL fAddRemove,
   LONG nStatus,
   LPSTR lpFileName
);
```

## <a name="parameters"></a>パラメーター
 呼び出し`pvCallerData`元 (IDE) から[SccPopulateList](../extensibility/sccpopulatelist-function.md)に渡されたパラメーター。 ソース管理プラグインは、このパラメーターの内容について何も想定しません。

 fAddRemoveIf `TRUE``lpFileName`はファイルリストに追加する必要があるファイルです。 の`FALSE`場合`lpFileName`は、ファイルリストから削除する必要があるファイルです。

 nステータスの状態`lpFileName`(`SCC_STATUS`ビットの組み合わせ;詳細は[ファイルステータスコード](../extensibility/file-status-code-enumerator.md)を参照)。

 lpFileName リストに追加または削除するファイル名の完全なディレクトリ パス。

## <a name="return-value"></a>戻り値

|[値]|説明|
|-----------|-----------------|
|`TRUE`|プラグインは、この関数を引き続き呼び出すことができます。|
|`FALSE`|IDE 側で問題が発生しました (メモリ不足などの状況)。 プラグインは操作を停止する必要があります。|

## <a name="remarks"></a>Remarks
 ソース管理プラグインがファイルリストに追加または削除するファイルごとに、この関数を呼び出して、 を渡します`lpFileName`。 フラグ`fAddRemove`は、リストに追加する新しいファイル、または削除する古いファイルを示します。 この`nStatus`パラメーターは、ファイルの状況を示します。 SCC プラグインがファイルの追加と削除を完了すると[、SccPopulateList](../extensibility/sccpopulatelist-function.md)呼び出しから戻ります。

> [!NOTE]
> `SCC_CAP_POPULATELIST`機能ビットは、Visual Studio に必要です。

## <a name="see-also"></a>関連項目
- [IDE によって実装されるコールバック関数](../extensibility/callback-functions-implemented-by-the-ide.md)
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
- [SccPopulateList](../extensibility/sccpopulatelist-function.md)
- [ファイルステータスコード](../extensibility/file-status-code-enumerator.md)
