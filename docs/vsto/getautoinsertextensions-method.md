---
description: デバッグ中に自動的に挿入される Office 用アプリに関する情報を取得します。
title: GetAutoInsertExtensions メソッド
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: c4a49942f50a79db604d2363cf2d85762c5ddce5
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102223434"
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

## <a name="remarks"></a>解説
 挿入される Office 用の各アプリは、Office アプリケーションの拡張子名として返されます。これは **HKEY_CURRENT_USER\Software\Microsoft\Office\WEF\Developer** の下の値に対応します。 ホストはレジストリでこれらの値を検索してから、自動的に拡張機能を挿入する必要があります。
