---
title: 'IDispatchEx:: InvokeEx |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDispatchEx.InvokeEx
apilocation:
- scrobj.dll
helpviewer_keywords:
- InvokeEx method
ms.assetid: d90783e6-4b89-4423-8a56-a9c8b4b2c813
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 673b3f1e64caa79dc2b21641209423d93fe0f834
ms.sourcegitcommit: d281d2a04a5bc302650eebf369946d8f101e59dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88144416"
---
# <a name="idispatchexinvokeex"></a>IDispatchEx::InvokeEx
オブジェクトによって公開されるプロパティおよびメソッドへのアクセスを提供し `IDispatchEx` ます。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT InvokeEx(  
   DISPID id,  
   LCID lcid,  
   WORD wFlags,  
   DISPARAMS *pdp,  
   VARIANT *pVarRes,   
   EXCEPINFO *pei,   
   IServiceProvider *pspCaller   
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `id`  
 メンバーを識別します。 `GetDispID`は、またはを使用し `GetNextDispID` てディスパッチ識別子を取得します。  
  
 `lcid`  
 引数を解釈する対象のロケール コンテキスト。 は、オブジェクトがロケール固有の引数を解釈できるようにするために、 `lcid` に渡され `InvokeEx` ます。  
  
 `wFlags`  
 の有効な値 `wFlags` は次のとおりです。  
  
 DISPATCH_PROPERTYGET &#124; DISPATCH_METHOD &#124; DISPATCH_PROPERTYPUT &#124; DISPATCH_PROPERTYPUTREF &#124; DISPATCH_CONSTRUCT  
  
 呼び出しのコンテキストを記述するフラグ `InvokeEx` :  
  
|値|意味|  
|-----------|-------------|  
|DISPATCH_METHOD|メンバーは、メソッドとして呼び出されます。 同じ名前のプロパティがある場合は、このと DISPATCH_PROPERTYGET フラグの両方を設定できます (で定義 `IDispatch` )。|  
|DISPATCH_PROPERTYGET|メンバーは、プロパティまたはデータメンバー (で定義) として取得され `IDispatch` ます。|  
|DISPATCH_PROPERTYPUT|メンバーは、プロパティまたはデータメンバー (で定義) として変更され `IDispatch` ます。|  
|DISPATCH_PROPERTYPUTREF|メンバーは、値の割り当てではなく、参照の割り当てによって変更されます。 このフラグは、プロパティが (で定義された) オブジェクトへの参照を受け入れる場合にのみ有効です `IDispatch` 。|  
|DISPATCH_CONSTRUCT|メンバーはコンストラクターとして使用されています。 (これはによって定義される新しい値です `IDispatchEx` )。 の有効な値 `wFlags` は次のとおりです。<br /><br /> DISPATCH_PROPERTYGET DISPATCH_METHOD DISPATCH_PROPERTYPUT DISPATCH_PROPERTYPUTREF DISPATCH_CONSTRUCT|  
  
 `pdp`  
 引数の配列、名前付き引数の DISPID の配列、配列内の要素数のカウントを格納している構造体へのポインター。 `IDispatch`DISPPARAMS 構造体の詳細については、ドキュメントを参照してください。  
  
 `pVarRes`  
 結果が格納される場所へのポインター。呼び出し元が結果を期待しない場合は Null。 DISPATCH_PROPERTYPUT または DISPATCH_PROPERTYPUTREF が指定されている場合、この引数は無視されます。  
  
 `pei`  
 例外情報を格納する構造体へのポインター。 が返される場合は、この構造体を入力する必要があり `DISP_E_EXCEPTION` ます。 Null を指定できます。 構造の詳細については、ドキュメントを参照してください `IDispatch` `EXCEPINFO` 。  
  
 `pspCaller`  
 呼び出し元から提供されるサービスプロバイダーオブジェクトへのポインター。これにより、オブジェクトが呼び出し元からサービスを取得できるようになります。 Null を指定できます。  
  
 `IDispatchEx::InvokeEx`はと同じ機能をすべて提供 `IDispatch::Invoke` し、いくつかの拡張機能を追加します。  
  
|値|意味|
|-|-|  
|DISPATCH_CONSTRUCT|項目がコンストラクターとして使用されていることを示します。|  
|`pspCaller`|を `pspCaller` 使用すると、オブジェクトは、呼び出し元によって提供されるサービスにアクセスできます。 特定のサービスは、呼び出し元自体によって処理されるか、呼び出しチェーンの上位にある呼び出し元に委任されることがあります。 たとえば、ブラウザー内のスクリプトエンジンが外部オブジェクトへの呼び出しを行う場合、その `InvokeEx` オブジェクトはチェーンに従って `pspCaller` スクリプトエンジンまたはブラウザーからサービスを取得できます。 (呼び出しチェーンは、コンテナーチェーンまたはサイトチェーンとも呼ばれる、作成チェーンとは異なることに注意してください。 作成チェーンは、などの他の機構を通じて使用できる場合があり `IObjectWithSite` ます)。|  
|`this` ポインター|で DISPATCH_METHOD が設定されている場合は、" `wFlags` this" 値に "名前付きパラメーター" がある可能性があります。 DISPID は DISPID_THIS され、最初の名前付きパラメーターである必要があります。|  
  
 の使用 `riid` されていないパラメーターは `IDispatch::Invoke` 削除されました。  
  
 `puArgArr`のパラメーター `IDispatch::Invoke` が削除されました。  
  
 次の例については、ドキュメントを参照してください `IDispatch::Invoke` 。  
  
 "引数のないメソッドの呼び出し"  
  
 "プロパティの取得と設定"  
  
 "パラメーターを渡す"  
  
 "インデックス付きプロパティ"  
  
 "呼び出し中の例外の発生"  
  
 "エラーを返す"  
  
## <a name="return-value"></a>戻り値  
 次の値のいずれか。  
  
|値|意味|  
|-|-|  
|`S_OK`|正常終了しました。|  
|DISP_E_BADPARAMCOUNT|DISPPARAMS に指定された要素の数が、メソッドまたはプロパティで許容される引数の数と異なります。|  
|DISP_E_BADVARTYPE|の引数の1つが `rgvarg` 有効なバリアント型ではありません。|  
|DISP_E_EXCEPTION|アプリケーションで例外を発生させる必要がある。 この場合は、渡された構造体を `pei` 入力する必要があります。|  
|DISP_E_MEMBERNOTFOUND|要求されたメンバーが存在しないか、またはの呼び出しが `InvokeEx` 読み取り専用プロパティの値を設定しようとしました。|  
|DISP_E_NONAMEDARGS|のこの実装 `IDispatch` では、名前付き引数はサポートされていません。|  
|DISP_E_OVERFLOW|の引数の1つ `rgvarg` を指定された型に強制変換できませんでした。|  
|DISP_E_PARAMNOTFOUND|パラメーター Dispid の1つがメソッドのパラメーターに対応していません。|  
|DISP_E_TYPEMISMATCH|1つ以上の引数を強制変換できませんでした。|  
|DISP_E_UNKNOWNLCID|呼び出されるメンバーは、LCID に従って文字列の引数を解釈し、LCID は認識されません。 引数を解釈するために LCID が不要な場合、このエラーは返されません。|  
|DISP_E_PARAMNOTOPTIONAL|必須パラメーターが省略されました。|  
  
## <a name="example"></a>例  
  
```cpp
VARIANT var;  
   BSTR bstrName;  
   DISPID dispid;  
   IDispatchEx *pdex;  
   DISPPARAMS dispparamsNoArgs = {NULL, NULL, 0, 0};  
  
   // Assign to pdex and bstrName  
   if (SUCCEEDED(pdex->GetDispID(bstrName, fdexNameCaseSensitive, &dispid)))  
   {  
      pdex->InvokeEx(dispid, LOCALE_USER_DEFAULT,  
         DISPATCH_PROPERTYGET, &dispparamsNoArgs,   
         &var, NULL, NULL);  
   }  
```  
  
## <a name="see-also"></a>関連項目  
 [IDispatchEx インターフェイス](../../winscript/reference/idispatchex-interface.md)   
 [IDispatchEx:: GetDispID](../../winscript/reference/idispatchex-getdispid.md)   
 [IDispatchEx::GetNextDispID](../../winscript/reference/idispatchex-getnextdispid.md)