---
title: GetAutoInsertExtensions メソッド
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f5d88af6f24306b7b243359c9797a2cb7e7449bc
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543508"
---
# <a name="getautoinsertextensions-method"></a>GetAutoInsertExtensions メソッド
  デバッグ中に自動的に挿入される Office 用アプリに関する情報を取得します。

 このメソッドは将来使用するために予約されています。

## <a name="syntax"></a>構文

```csharp
HRESULT GetAutoInsertExtensions(
    [out, retval] SAFEARRAY(BSTR)* psaExtensionNames
);
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------------|-----------------|
|*psaExtensionNames*|Office 用アプリの拡張機能名。|

## <a name="return-value"></a>戻り値
 メソッドが正常に完了したかどうかを示す HRESULT 値。

## <a name="remarks"></a>Remarks
 挿入される Office 用の各アプリは、Office アプリケーションの拡張子名として返されます。これは**HKEY_CURRENT_USER \software\microsoft\office\wef\developer**の下の値に対応します。 ホストはレジストリでこれらの値を検索してから、自動的に拡張機能を挿入する必要があります。
