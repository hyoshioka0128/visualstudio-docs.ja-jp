---
title: 'IActiveScriptProperty:: SetProperty |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptProperty.SetProperty
apilocation:
- scrobj.dll
helpviewer_keywords:
- SetProperty method, IActiveScriptProperty interface
ms.assetid: 0ba429c5-04a3-4505-bc5f-69c505dfca91
caps.latest.revision: 21
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0f8307a82f181be20205c7bfcc47e881b0fa1e90
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571309"
---
# <a name="iactivescriptpropertysetproperty"></a>IActiveScriptProperty::SetProperty
パラメーターによって指定されたプロパティを設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT SetProperty(  
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
 設定するプロパティ値。  
  
 `pvarIndex`  
 使用しません。  
  
 `pvarValue`  
 プロパティの値。  
  
 `dwProperty` に使用できる値を次の表に示します。  
  
|定数|値|意味|  
|--------------|-----------|-------------|  
|SCRIPTPROP_INTEGERMODE|0x00003000|スクリプトエンジンを強制的に浮動小数点モードではなく整数モードで除算します。 既定値は `False` です。|  
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
 整数除算を有効または無効にするには、`SetProperty` を呼び出し、`Boolean` を `Object`に変換します。 既定では、プロパティの値は `False`です。 `True`に設定した場合、除算演算では整数のみが返されます。  
  
 カスタム文字列比較を有効または無効にするには、`SetProperty` を呼び出し、`Object` の値を渡します。 渡すオブジェクトは、インターフェイス[IActiveScriptStringCompare インターフェイス](../../winscript/reference/iactivescriptstringcompare-interface.md)を実装する必要があります。 [IActiveScriptStringCompare インターフェイス](../../winscript/reference/iactivescriptstringcompare-interface.md)インターフェイスの[StrComp](../../winscript/reference/iactivescriptstringcompare-strcomp.md)メソッドは、文字列比較関数が実行されるたびに呼び出されます。  
  
 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] スクリプトエンジンが初期化されるときにサポートされる言語機能のセットを選択するには、`SetProperty` を呼び出し、SCRIPTPROP_INVOKEVERSIONING に対して有効になる言語機能セットに対応する値を渡します。 このプロパティが 1 (SCRIPTLANGUAGEVERSION_5_7) に設定されている場合、使用可能な言語機能は、[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] スクリプトエンジンのバージョン5.7 で表示されていた機能と同じです。 2 (SCRIPTLANGUAGEVERSION_5_8) に設定されている場合、使用可能な言語機能はバージョン5.8 で追加された新機能に加えて、バージョン5.7 で表示されていた機能です。 既定では、このプロパティは 0 (SCRIPTLANGUAGEVERSION_DEFAULT) に設定されています。これは、ホストが異なる既定の動作をサポートしている場合を除き、バージョン5.7 で表示された言語機能セットと同じです。 たとえば、internet explorer 8 の既定のドキュメントモードが "Internet Explorer 8 標準" モードの場合、既定では、バージョン 5.8 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] スクリプトエンジンでサポートされている [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 言語機能を使用できます。 Internet Explorer 8 ドキュメントモードを Internet Explorer 7 標準モードまたは互換モードに切り替えると、[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] スクリプトエンジンがリセットされ、バージョン 5.7 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] スクリプトエンジンに存在していた言語機能セットのみがサポートされます。  
  
> [!NOTE]
> SCRIPTPROP_INVOKEVERSIONING は、[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] スクリプトエンジンが初期化されている場合にのみ設定する必要があります。  
  
## <a name="example"></a>例  
 次の例では、スクリプトエンジンで整数除算を使用するように強制する方法と、compare 関数のオーバーロードを許可する方法を示します。  
  
```c#  
BMLScriptEngine bmlScriptEngine = new BMLScriptEngine();  
IActiveScriptProperty scriptProperties = bmlScriptEngine as   
    IActiveScriptProperty;  
  
// Force the scripting engine to use integer division.  
Boolean enableIntegerDivision = true;  
Object vtIntegerDivInstance = (Object)enableIntegerDivision;  
                scriptProperties.SetProperty(SCRIPTPROP_INTEGERDIVISION,   
    System.IntPtr.Zero, ref vtIntegerDivInstance);  
  
// Allow overloading of the compare function.  
BMLScriptStringCompare bmlScriptStringCompareInstance = new   
    BMLScriptStringCompare();  
Object vtStrCmpInstance = (Object)bmlScriptStringCompareInstance;  
scriptProperties.SetProperty(SCRIPTPROP_STRCOMPINST,   
    System.IntPtr.Zero, ref vtStrCmpInstance);  
```  
  
## <a name="see-also"></a>参照  
 [ドキュメント互換性](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/compatibility/cc288325(v=vs.85))  の定義  
 [IActiveScriptProperty](../../winscript/reference/iactivescriptproperty.md)   
 [バージョン情報](../../javascript/reference/javascript-version-information.md)