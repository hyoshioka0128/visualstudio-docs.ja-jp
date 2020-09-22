---
title: POPLISTFUNC |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- POPDIRLISTFUNC
helpviewer_keywords:
- POPLISTFUNC callback function
ms.assetid: b2199fd5-d707-4628-92dd-e2a01e2f507a
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8c3ae2ce451f076c33ea5613b71c6d262c1d7a0e
ms.sourcegitcommit: fb8babf5cd72f1fc2f97ffe4ad7b62d91f325f61
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2020
ms.locfileid: "90841880"
---
# <a name="poplistfunc"></a>POPLISTFUNC
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このコールバックは、IDE によって [SccPopulateList](../extensibility/sccpopulatelist-function.md) に提供され、ソース管理プラグインがファイルまたはディレクトリの一覧を更新するために使用します (関数にも指定されてい `SccPopulateList` ます)。  
  
 ユーザーが IDE で **get** コマンドを選択すると、ide には、ユーザーが取得できるすべてのファイルのリストボックスが表示されます。 残念ながら、IDE では、ユーザーが取得する可能性のあるすべてのファイルの正確な一覧がわかりません。このリストはプラグインのみに含まれています。 他のユーザーがソースコード管理プロジェクトにファイルを追加している場合、これらのファイルは一覧に表示されますが、IDE では認識されません。 IDE によって、ユーザーが取得できると思われるファイルの一覧が作成されます。 このリストをユーザーに表示する前に、 [SccPopulateList](../extensibility/sccpopulatelist-function.md)を呼び出して、 `,` リストからファイルを追加および削除するためのソース管理プラグインを提供します。  
  
## <a name="signature"></a>署名  
 ソース管理プラグインは、次のプロトタイプで IDE によって実装された関数を呼び出すことによって、リストを変更します。  
  
```cpp#  
typedef BOOL (*POPLISTFUNC) (  
   LPVOID pvCallerData,  
   BOOL fAddRemove,  
   LONG nStatus,  
   LPSTR lpFileName  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 pvCallerData  
 `pvCallerData`呼び出し元 (IDE) によって[SccPopulateList](../extensibility/sccpopulatelist-function.md)に渡されるパラメーター。 ソース管理プラグインは、このパラメーターの内容について何も想定していません。  
  
 fAddRemove リスト  
 の場合 `TRUE` 、 `lpFileName` はファイルリストに追加する必要があるファイルです。 の場合 `FALSE` 、 `lpFileName` はファイルリストから削除する必要があるファイルです。  
  
 nStatus  
 の状態 `lpFileName` (ビットの組み合わせ `SCC_STATUS` )。詳細については、「 [ファイルの状態コード](../extensibility/file-status-code-enumerator.md) 」を参照してください。  
  
 lpFileName  
 一覧から追加または削除するファイル名の完全なディレクトリパス。  
  
## <a name="return-value"></a>戻り値  
  
|値|説明|  
|-----------|-----------------|  
|`TRUE`|プラグインは、この関数の呼び出しを続行できます。|  
|`FALSE`|IDE 側で問題が発生しました (メモリ不足など)。 プラグインが動作を停止する必要があります。|  
  
## <a name="remarks"></a>注釈  
 ソース管理プラグインがファイルリストに追加または削除しようとしているファイルごとに、この関数を呼び出してを渡し `lpFileName` ます。 フラグは、 `fAddRemove` 一覧に追加する新しいファイルまたは削除する古いファイルを示します。 パラメーターは、 `nStatus` ファイルの状態を示します。 SCC プラグインがファイルの追加と削除を完了すると、 [SccPopulateList](../extensibility/sccpopulatelist-function.md) 呼び出しから制御が戻ります。  
  
> [!NOTE]
> `SCC_CAP_POPULATELIST`Visual Studio では、機能ビットが必要です。  
  
## <a name="see-also"></a>参照  
 [IDE によって実装されるコールバック関数](../extensibility/callback-functions-implemented-by-the-ide.md)   
 [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)   
 [SccPopulateList](../extensibility/sccpopulatelist-function.md)   
 [ファイルの状態コード](../extensibility/file-status-code-enumerator.md)
