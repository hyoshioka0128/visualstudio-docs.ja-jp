---
title: 'IActiveScriptAuthor:: AddNamedItem |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthor.AddNamedItem
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthor::AddNamedItem
ms.assetid: 951003b6-1c4a-4086-b7ce-2f128e007280
caps.latest.revision: 19
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f0d2f08a49fdc768e87152bf486ce48687c79e68
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577254"
---
# <a name="iactivescriptauthoraddnameditem"></a>IActiveScriptAuthor::AddNamedItem
ルートレベルの項目の名前をスクリプト作成エンジンの名前空間に追加します。 *ルートレベルの項目*は、プロパティとメソッドを含むことができ、イベントソースも含むことができるオブジェクトです。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT AddNamedItem(  
   LPCOLESTR          pszName,  
   DWORD              dwFlags,  
   IDispatch          *pdisp  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pszName`  
 からスクリプトから表示される項目の名前。 名前は一意であり、持続可能でなければなりません。  
  
 `dwFlags`  
 から名前付き項目に関連付けられているフラグ。 は、次の値の組み合わせにすることができます。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|SCRIPTITEM_ISVISIBLE|0x00000002|項目の名前がスクリプトの名前空間で使用できることを示します。 これにより、項目のプロパティ、メソッド、およびイベントにアクセスできるようになります。<br /><br /> 規則により、項目のプロパティには項目の子メンバーが含まれます。 そのため、すべての子オブジェクトのプロパティとメソッド (およびその子メンバー) にアクセスできます。|  
|SCRIPTITEM_ISSOURCE|0x00000004|スクリプトがスクリプトイベントハンドラーを持つことができるアイテムソースのイベントを示します。|  
|SCRIPTITEM_GLOBALMEMBERS|0x00000008|項目が、スクリプトに関連付けられているグローバルプロパティとメソッドのコレクションであることを示します。 そのメンバーは、グローバル変数およびメソッドとして作成されます。|  
|SCRIPTITEM_ISPERSISTENT|0x00000040|スクリプト作成エンジンが保存されている場合に、アイテムを保存することを示します。|  
|SCRIPTITEM_CODEONLY|0x00000200|名前付き項目がコードのみのオブジェクトを表し、作成するメンバーを持たないことを示します。|  
|SCRIPTITEM_NOCODE|0x00000400|名前付き項目が追加されるのは名前だけであり、作成するものがないことを示します。|  
  
 `pdisp`  
 からメソッド、プロパティ、またはイベントソースの収集に使用される `NamedItem` オブジェクトの `IDispatch`。  
  
## <a name="return-value"></a>戻り値  
 `HRESULT`。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|値|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>コメント  
  
## <a name="see-also"></a>参照  
 [IActiveScriptAuthor インターフェイス](../../winscript/reference/iactivescriptauthor-interface.md)   
 [IActiveScriptAuthor::RemoveNamedItem](../../winscript/reference/iactivescriptauthor-removenameditem.md)