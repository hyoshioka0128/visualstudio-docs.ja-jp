---
title: 'IDebugProcessSecurity:: GetUserName |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugProcessSecurity::GetUserName
ms.assetid: c73c60ac-da6e-45ae-8f04-95353a24ca3e
caps.latest.revision: 5
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 17a6ef52d7df1c60b0cb6581a7e15eeaf67e7875
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68202786"
---
# <a name="idebugprocesssecuritygetusername"></a>IDebugProcessSecurity::GetUserName
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

ポートサプライヤーからユーザー名を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetUserName(  
    BSTR *pbstrUserName  
);  
```  
  
```csharp  
int GetUserName (  
    string pbstrUserName  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pbstrUserName`  
 入出力ユーザー名を表す文字列です。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は `S_OK` を返します。 それ以外の場合は、エラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 `GetUserName`[**プロセスにアタッチ**] ダイアログボックスの [**ユーザー名**] 列に表示されるユーザー名を返します。 [**プロセスにアタッチ**] ダイアログボックスを表示するには、統合開発環境 (IDE) の [**ツール**] メニューの [**プロセスにアタッチ**] をクリックし [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] ます。  
  
## <a name="see-also"></a>参照  
 [IDebugProcessSecurity](../../../extensibility/debugger/reference/idebugprocesssecurity.md)
