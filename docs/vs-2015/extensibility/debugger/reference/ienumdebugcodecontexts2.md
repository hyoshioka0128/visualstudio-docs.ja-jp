---
title: IEnumDebugCodeContexts2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugCodeContexts2
helpviewer_keywords:
- IEnumDebugCodeContexts2
ms.assetid: 72915146-215f-4c99-a034-131b2b474e0e
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f36da19e6bc47d70010dd96a26256537803ccb29
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62551619"
---
# <a name="ienumdebugcodecontexts2"></a>IEnumDebugCodeContexts2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、デバッグセッション、または特定のプログラムまたはドキュメントに関連付けられたコードコンテキストを列挙します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IEnumDebugCodeContexts2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 デバッグエンジン (DE) は、プログラム内の特定のテキスト位置のコードコンテキストの一覧、または特定のドキュメントコンテキストのコードコンテキストのリストを表すために、このインターフェイスを実装します。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 [EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)を呼び出して、プログラムのソースドキュメント内の特定のテキスト位置のコードコンテキストの一覧を表すこのインターフェイスを取得します。  
  
 [EnumCodeContexts](../../../extensibility/debugger/reference/idebugdocumentcontext2-enumcodecontexts.md)を呼び出して、特定のソースドキュメント内のすべてのコードコンテキストのリストを表すこのインターフェイスを取得します。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表に、のメソッドを示し `IEnumDebugCodeContexts2` ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|[次へ](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-next.md)|列挙シーケンス内の指定された数のコードコンテキストを取得します。|  
|[Skip](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-skip.md)|列挙シーケンス内の指定された数のコードコンテキストをスキップします。|  
|[リセット](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-reset.md)|列挙シーケンスを先頭にリセットします。|  
|[複製](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|  
|[GetCount](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-getcount.md)|列挙子内のコードコンテキストの数を取得します。|  
  
## <a name="remarks"></a>注釈  
 Visual Studio は、 [EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md) を呼び出して、次のステートメントを設定するとき、またはソースファイルの逆アセンブリを表示するときに、ユーザーが選択できるコードコンテキストの一覧を設定します。 複数のコードコンテキストが発生する可能性があります。たとえば、C++ スタイルのテンプレートの複数のインスタンスがある場合です。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)   
 [EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)   
 [EnumCodeContexts](../../../extensibility/debugger/reference/idebugdocumentcontext2-enumcodecontexts.md)
