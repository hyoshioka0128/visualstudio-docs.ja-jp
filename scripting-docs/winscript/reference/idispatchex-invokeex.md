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
ms.openlocfilehash: 8a15acb3211c0d3dd19c0d262efb6cbd3327ab9a
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575312"
---
# <a name="idispatchexinvokeex"></a>IDispatchEx::InvokeEx
`IDispatchEx` オブジェクトによって公開されるプロパティおよびメソッドへのアクセスを提供します。  
  
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
 メンバーを識別します。 `GetDispID` または `GetNextDispID` を使用してディスパッチ識別子を取得します。  
  
 `lcid`  
 引数を解釈する対象のロケール コンテキスト。 オブジェクトがロケール固有の引数を解釈できるようにするために、`lcid` が `InvokeEx` に渡されます。  
  
 `wFlags`  
 `wFlags` の有効な値は次のとおりです。  
  
 DISPATCH_PROPERTYGET &#124; DISPATCH_METHOD &#124; DISPATCH_PROPERTYPUT &#124; DISPATCH_PROPERTYPUTREF &#124; DISPATCH_CONSTRUCT  
  
 `InvokeEx` 呼び出しのコンテキストを記述するフラグ:  
  
|値|意味|  
|-----------|-------------|  
|DISPATCH_METHOD|メンバーは、メソッドとして呼び出されます。 プロパティの名前が同じである場合は、このフラグと DISPATCH_PROPERTYGET フラグの両方を設定できます (`IDispatch`によって定義されます)。|  
|DISPATCH_PROPERTYGET|メンバーは、プロパティまたはデータメンバー (`IDispatch`によって定義) として取得されます。|  
|DISPATCH_PROPERTYPUT|メンバーは、プロパティまたはデータメンバー (`IDispatch`によって定義) として変更されます。|  
|DISPATCH_PROPERTYPUTREF|メンバーは、値の割り当てではなく、参照の割り当てによって変更されます。 このフラグは、プロパティが (`IDispatch`によって定義された) オブジェクトへの参照を受け入れる場合にのみ有効です。|  
|DISPATCH_CONSTRUCT|メンバーはコンストラクターとして使用されています。 (これは `IDispatchEx`によって定義される新しい値です)。 `wFlags` の有効な値は次のとおりです。<br /><br /> DISPATCH_PROPERTYGET DISPATCH_METHOD DISPATCH_PROPERTYPUT DISPATCH_PROPERTYPUTREF DISPATCH_CONSTRUCT|  
  
 `pdp`  
 引数の配列、名前付き引数の DISPID の配列、配列内の要素数のカウントを格納している構造体へのポインター。 DISPPARAMS 構造の詳細については、`IDispatch` のドキュメントを参照してください。  
  
 `pVarRes`  
 結果が格納される場所へのポインター。呼び出し元が結果を期待しない場合は Null。 DISPATCH_PROPERTYPUT または DISPATCH_PROPERTYPUTREF が指定されている場合、この引数は無視されます。  
  
 `pei`  
 例外情報を格納する構造体へのポインター。 `DISP_E_EXCEPTION` が返される場合は、この構造体を入力する必要があります。 Null を指定できます。 `EXCEPINFO` 構造の詳細については、`IDispatch` のドキュメントを参照してください。  
  
 `pspCaller`  
 呼び出し元から提供されるサービスプロバイダーオブジェクトへのポインター。これにより、オブジェクトが呼び出し元からサービスを取得できるようになります。 Null を指定できます。  
  
 `IDispatchEx::InvokeEx` は `IDispatch::Invoke` と同じ機能をすべて提供し、いくつかの拡張機能を追加します。  
  
|||  
|-|-|  
|DISPATCH_CONSTRUCT|項目がコンストラクターとして使用されていることを示します。|  
|`pspCaller`|`pspCaller` を使用すると、呼び出し元によって提供されるサービスにオブジェクトがアクセスできるようになります。 特定のサービスは、呼び出し元自体によって処理されるか、呼び出しチェーンの上位にある呼び出し元に委任されることがあります。 たとえば、ブラウザー内のスクリプトエンジンが外部オブジェクトへの `InvokeEx` 呼び出しを行う場合、オブジェクトは `pspCaller` チェーンに従ってスクリプトエンジンまたはブラウザーからサービスを取得できます。 (呼び出しチェーンは、コンテナーチェーンまたはサイトチェーンとも呼ばれる、作成チェーンとは異なることに注意してください。 作成チェーンは、`IObjectWithSite`などの他のメカニズムを通じて使用できる場合があります)。|  
|`this` ポインター|`wFlags`で DISPATCH_METHOD が設定されている場合は、"this" 値に "名前付きパラメーター" がある可能性があります。 DISPID は DISPID_THIS され、最初の名前付きパラメーターである必要があります。|  
  
 `IDispatch::Invoke` の未使用の `riid` パラメーターが削除されました。  
  
 `IDispatch::Invoke` の `puArgArr` パラメーターが削除されました。  
  
 次の例については、`IDispatch::Invoke` のドキュメントを参照してください。  
  
 "引数のないメソッドの呼び出し"  
  
 "プロパティの取得と設定"  
  
 "パラメーターを渡す"  
  
 "インデックス付きプロパティ"  
  
 "呼び出し中の例外の発生"  
  
 "エラーを返す"  
  
## <a name="return-value"></a>戻り値  
 次のいずれかの値を返します。  
  
|||  
|-|-|  
|`S_OK`|成功。|  
|DISP_E_BADPARAMCOUNT|DISPPARAMS に指定された要素の数が、メソッドまたはプロパティで許容される引数の数と異なります。|  
|DISP_E_BADVARTYPE|`rgvarg` の引数の1つが有効なバリアント型ではありません。|  
|DISP_E_EXCEPTION|アプリケーションで例外を発生させる必要がある。 この場合、`pei` 渡された構造体を入力する必要があります。|  
|DISP_E_MEMBERNOTFOUND|要求されたメンバーが存在しないか、またはの呼び出しが読み取り専用プロパティの値を設定しようとしました `InvokeEx`。|  
|DISP_E_NONAMEDARGS|この `IDispatch` の実装では、名前付き引数はサポートされていません。|  
|DISP_E_OVERFLOW|`rgvarg` の引数の1つは、指定された型に強制変換できませんでした。|  
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
  
## <a name="see-also"></a>参照  
 [IDispatchEx インターフェイス](../../winscript/reference/idispatchex-interface.md)   
 [IDispatchEx::GetDispID](../../winscript/reference/idispatchex-getdispid.md)   
 [IDispatchEx::GetNextDispID](../../winscript/reference/idispatchex-getnextdispid.md)