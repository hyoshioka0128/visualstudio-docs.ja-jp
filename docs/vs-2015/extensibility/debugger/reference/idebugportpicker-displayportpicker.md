---
title: IDebugPortPicker::D isplayPortPicker |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- DisplayPortPicker
- IDebugPortPicker::DisplayPortPicker
ms.assetid: 08511ef5-be64-4069-b169-a569cc94bc64
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3dd9317a73800a3886a5a807e9e28b0c24b2301c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68188375"
---
# <a name="idebugportpickerdisplayportpicker"></a>IDebugPortPicker::DisplayPortPicker
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定されたダイアログボックスを表示し、ユーザーがポートを選択できるようにします。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT DisplayPortPicker(  
   HWND hwndParentDialog,  
   BSTR* pbstrPortId  
);  
```  
  
```csharp  
public int DisplayPortPicker(  
   int hwndParentDialog,  
   out string pbstrPortId  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `hwndParentDialog`  
 から親ダイアログボックスのハンドル。  
  
 `pbstrPortId`  
 入出力ポート識別子文字列。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 戻り値 `S_FALSE` (またはがに設定されたの戻り値) は、 `S_OK` `BSTR` `NULL` ユーザーが **[キャンセル]** をクリックしたことを示します。  
  
## <a name="see-also"></a>参照  
 [IDebugPortPicker](../../../extensibility/debugger/reference/idebugportpicker.md)
