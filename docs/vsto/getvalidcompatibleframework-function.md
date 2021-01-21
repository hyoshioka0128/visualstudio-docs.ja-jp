---
title: Getvalid互換フレームワーク関数
description: Getvalid互換フレームワーク API が Office インフラストラクチャをサポートする方法について説明します。コードから直接使用するためのものではありません。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 96f536b3ab8e28b87a59a637fcf6dbaadeb21bf7
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96845077"
---
# <a name="getvalidcompatibleframework-function"></a>Getvalid互換フレームワーク関数
  この API は Office インフラストラクチャをサポートします。独自に作成したコードから直接使用するためのものではありません。

## <a name="syntax"></a>構文

```csharp
HRESULT WINAPI GetValidCompatibleFramework(
    LPCWSTR lpwszCompatibleFrameworksXML,
    BSTR* pbstrValidFrameworkTag
);
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------------|-----------------|
|*lpwszCompatibleFrameworksXML*|使用しないでください。|
|*pbstrValidFrameworkTag*|使用しないでください。|

## <a name="return-value"></a>戻り値
 関数が成功した場合は、 **S_OK** を返します。 関数が失敗した場合は、エラーコードを返します。
