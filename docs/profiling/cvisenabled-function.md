---
title: CvIsEnabled 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- cvmarkers/CvIsEnabledEx
- cvmarkers/CvIsEnabled
helpviewer_keywords:
- CvIsEnabled method
- CvIsEnabledEx method
ms.assetid: 2e4fea6d-758d-4150-8744-6102a1d58c1c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 92763e352d04d5aa3e88a68bad7adfcd05897027
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "62945415"
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