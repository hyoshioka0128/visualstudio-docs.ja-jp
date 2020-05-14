---
title: 検索式の論理演算子 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- Help Viewer 2.0, logical operators in search
- logical operators in search [Help Viewer 2.0]
ms.assetid: 0c38ae7d-3e20-4d47-a020-9677cd285916
caps.latest.revision: 11
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3d56f2dfc2924008a6be293fe1498f0ffe32abaf
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72651441"
---
# <a name="logical-operators-in-search-expressions"></a>検索式の論理演算子
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

論理演算子を使用すると、より単純な検索式からより複雑な検索式を作成して、コンテンツの検索を絞り込むことができます。 次の表に示すように、論理演算子では、複数の検索用語を検索クエリでどのように組み合わせる必要があるかを指定します。

> [!IMPORTANT]
> 検索エンジンが認識できるように、論理演算子をすべて大文字で入力する必要があります。

|検索対象|使用|例|結果|
|-------------------|---------|-------------|------------|
|同じトピック内の両方の用語|AND|dib AND palette|"dib" と "palette" の両方を含むトピック。|
|トピック内のいずれかの用語|OR|raster OR vector|"raster" または "vector" を含むトピック。|
|同じトピック内の最初の用語 (2 番目の用語を含まない)|NOT|"operating system" NOT DOS|"operating system" を含むが、"DOS" を含まないトピック。|
|トピック内で近接する両方の用語|NEAR|user NEAR kernel|"kernel" にきわめて近い "user" を含むトピック。|

## <a name="see-also"></a>関連項目
 [フルテキスト検索のヒント](../ide/full-text-search-tips.md)[情報](../ide/locate-information.md)の検索
