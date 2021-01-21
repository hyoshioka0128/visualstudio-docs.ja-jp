---
title: GetVstoSolutionMetadata 関数
description: GetVstoSolutionMetadata API が Office インフラストラクチャをサポートする方法について説明します。コードから直接使用するためのものではありません。
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
ms.openlocfilehash: 205bde9352e2a037b4a08108d8cfce3460034e66
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96845038"
---
# <a name="getvstosolutionmetadata-function"></a>GetVstoSolutionMetadata 関数
  この API は Office インフラストラクチャをサポートします。独自に作成したコードから直接使用するためのものではありません。

## <a name="syntax"></a>構文

```csharp
HRESULT WINAPI GetVstoSolutionMetadata(
    LPCWSTR lpwszSolutionMetadataKey,
    ISolutionMetadata** ppSolutionInfo
);
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------------|-----------------|
|*lpwszSolutionMetadataKey*|使用しないでください。|
|*ppSolutionInfo*|使用しないでください。|

## <a name="return-value"></a>戻り値
 関数が成功した場合は、 **S_OK** を返します。 関数が失敗した場合は、エラーコードを返します。
