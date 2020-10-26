---
title: コード メトリックに関する問題のトラブルシューティング | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: troubleshooting
ms.assetid: f2fdb995-4888-4246-85dc-7bacadd45968
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b4d374a2737e2ce8892304b615bebcf99d9c60ad
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72672452"
---
# <a name="troubleshooting-code-metrics-issues"></a>コード メトリックに関する問題のトラブルシューティング
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コード メトリックを収集するときに、次に示す問題が発生する場合があります。

- [Visual Studio 2010 のコードの複雑度の計算における変更点](#Changes_in_Visual_Studio_2010_code_complexity_calculations)

## <a name="changes-in-visual-studio-2010-code-complexity-calculations"></a><a name="Changes_in_Visual_Studio_2010_code_complexity_calculations"></a> Visual Studio 2010 の変更点コードの複雑度の計算
 次のような状況では、同じ関数について [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] で計算したコードの複雑度のメトリックと旧バージョンの [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] で計算したメトリックとが異なる場合があります。

- 関数に 1 つ以上の catch ブロックが含まれている。 以前のバージョンの [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] では、catch ブロックが計算に含まれていませんでした。 [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] では、各 catch ブロックの複雑度が関数の複雑度に加算されます。

- 関数に switch (VB の場合は Select Case) ステートメントが含まれている。 [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] と旧バージョンの間のコンパイラの相違点により、case のフォールスルーを含んでいる一部の switch ステートメントに対して、異なる MSIL コードが生成される場合があります。

## <a name="see-also"></a>参照
 [マネージド コードの複雑さと保守性の測定](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)
