---
title: CvIsEnabled 関数 | Microsoft Docs
description: コンカレンシー ビジュアライザー SDK 関数 CvIsEnabled (C ライブラリ) のリファレンス情報を参照してください。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkers/CvIsEnabledEx
- cvmarkers/CvIsEnabled
helpviewer_keywords:
- CvIsEnabled method
- CvIsEnabledEx method
ms.assetid: 2e4fea6d-758d-4150-8744-6102a1d58c1c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0be750f62e248b3d9f837c5baa561765e14bfba5
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99940944"
---
# <a name="cvisenabled-function"></a>CvIsEnabled 関数
セッションにより ETW プロバイダーが有効になっているか判断します。

## <a name="syntax"></a>構文

```C
HRESULT CvIsEnabled(
   _In_ PCV_PROVIDER pProvider
);
HRESULT CvIsEnabledEx(
   _In_ PCV_PROVIDER pProvider,
   _In_ CV_IMPORTANCE level,
   _In_ int category
);
```

#### <a name="parameters"></a>パラメーター
 `category` カテゴリ。

 `level` 重要度レベル。

 `pProvider`有効なプロバイダー オブジェクト。 Nll は指定できません。

## <a name="return-value"></a>戻り値
 プロバイダーが現在有効になっている場合は S_OK を返します。 プロバイダーが現在無効になっている場合は S_FALSE を返します。 エラーが発生した場合はエラー コードを返します。 FAILED マクロを使用し、エラーの状態を確認し、それから S_OK/S_FALSE を確認します。

## <a name="requirements"></a>必要条件
 **ヘッダー:** *cvmarkers.h*

## <a name="see-also"></a>関連項目
- [C++ ライブラリ リファレンス](../profiling/cpp-library-reference.md)