---
title: Getvalid互換フレームワーク関数
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
ms.openlocfilehash: 2219417fe8ddae3d11d0e624ad12d3de80e290dd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85520225"
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

|パラメーター|[説明]|
|---------------|-----------------|
|*lpwszCompatibleFrameworksXML*|使用しないでください。|
|*pbstrValidFrameworkTag*|使用しないでください。|

## <a name="return-value"></a>戻り値
 関数が成功した場合は、 **S_OK**を返します。 関数が失敗した場合は、エラーコードを返します。
