---
title: 'IActiveScriptProperty:: GetProperty |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptProperty.GetProperty
apilocation:
- scrobj.dll
helpviewer_keywords:
- GetProperty method, IActiveScriptProperty interface
ms.assetid: a43383db-b148-4d76-83bd-4f0e899b7cb1
caps.latest.revision: 24
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f1eeec6472a067d18a8b8962cfac70c25c0ff971
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571415"
---
# <a name="iactivescriptpropertygetproperty"></a>IActiveScriptProperty::GetProperty
パラメーターによって指定されたプロパティを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetProperty(  
// The property value:  
    uint dwProperty,    
// Not used:  
    IntPtr pvarIndex,    
// The value of the property:   
    out object pvarValue,    
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `dwProperty`  
 取得するプロパティ値。  
  
 `pvarIndex`  
 使用しません。  
  
 `pvarValue`  
 プロパティの値。  
  
 `dwProperty` に使用できる値を次の表に示します。  
  
|定数|値|意味|  
|--------------|-----------|-------------|  
|SCRIPTPROP_INTEGERMODE|0x00003000|スクリプトエンジンを強制的に浮動小数点モードではなく整数モードで除算します。|  
|SCRIPTPROP_STRINGCOMPAREINSTANCE|0x00003001|スクリプトエンジンの文字列比較関数を置き換えることができるようにします。|  
|SCRIPTPROP_ABBREVIATE_GLOBALNAME_RESOLUTION|0x70000002|他のスクリプトエンジンがグローバルオブジェクトに関与していないことをスクリプトエンジンに通知します。|  
|SCRIPTPROP_INVOKEVERSIONING|0x00004000|[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] スクリプトエンジンに対して、サポートされる言語機能のセットを強制的に選択させます。 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] スクリプトエンジンでサポートされている言語機能の既定のセットは、[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] スクリプトエンジンのバージョン5.7 にある言語機能セットと同じです。|  
  
## <a name="return-value"></a>戻り値  
 次のいずれかの値を返します。  
  
|戻り値|意味|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_INVALIDARG`|引数が有効ではありません。|  
|`E_UNEXPECTED`|この呼び出しは想定されていませんでした (たとえば、スクリプトエンジンがまだ読み込まれていないか、初期化されていません)。|  
  
## <a name="remarks"></a>コメント  
 ホストは、SCRIPTPROP_ABBREVIATE_GLOBALNAME_RESOLUTION プロパティを使用して、グローバルオブジェクトに寄与する他のスクリプトエンジンが存在しないことをスクリプトエンジンに通知できます。 たとえば、Internet Explorer では、表示されているページに [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] スクリプトだけが含まれていることを [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] エンジンに通知できます。 したがって、グローバルオブジェクトウィンドウに新しいプロパティを追加できるのは [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] エンジンだけであり、同じ操作を実行する Visual Basic Scripting Edition (VBScript) エンジンは存在しません。 エンジンは、このフラグを無視することも、グローバルオブジェクトに追加される新しいメンバーの管理を最適化するために使用することもできます。  
  
 ホストは、SCRIPTPROP_INVOKEVERSIONING プロパティを使用して、[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] スクリプトエンジンが開始されるときにサポートされる言語機能のセットを選択できます。 このプロパティが 1 (SCRIPTLANGUAGEVERSION_5_7) に設定されている場合、使用可能な言語機能は、[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] スクリプトエンジンのバージョン5.7 で表示されていた機能と同じです。 2 (SCRIPTLANGUAGEVERSION_5_8) に設定されている場合、使用可能な言語機能はバージョン5.8 で追加された機能に加えて、バージョン5.7 で表示されていた機能です。 既定では、このプロパティは 0 (SCRIPTLANGUAGEVERSION_DEFAULT) に設定されています。これは、ホストが異なる既定の動作をサポートしている場合を除き、バージョン5.7 で表示された言語機能セットと同じです。 たとえば、internet explorer 8 のドキュメントモードが "Internet Explorer 8 標準" モードの場合、既定では、バージョン 5.8 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] スクリプトエンジンによってサポートされる [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 言語機能が internet Explorer 8 で使用されます。  
  
## <a name="see-also"></a>参照  
 [ドキュメント互換性](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/compatibility/cc288325(v=vs.85))  の定義  
 [IActiveScriptProperty](../../winscript/reference/iactivescriptproperty.md)   
 [バージョン情報](../../javascript/reference/javascript-version-information.md)