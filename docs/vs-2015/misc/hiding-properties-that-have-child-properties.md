---
title: 子プロパティを持つプロパティの非表示 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- properties [Visual Studio SDK], hiding
- Properties window, hiding properties that have child properties
ms.assetid: 6003607e-fc19-4bf9-a299-9f6adf8e92eb
caps.latest.revision: 13
manager: jillfra
ms.openlocfilehash: 1d20b865c6f07d76320a7df8402810c82869ddfb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62822387"
---
# <a name="hiding-properties-that-have-child-properties"></a>子プロパティを持つ非表示のプロパティ
子プロパティを持つプロパティを非表示にするには、次のようにします。  
  
- 入れ子になったプロジェクトがある場合、親プロジェクトはプログラムによって子プロジェクトの一部の側面を制御します。  
  
- 特殊なデザイナーでコントロールを使用し、そのコントロールのすべてのプロパティへのフルアクセスを開発者に付与しない場合。  
  
- オブジェクトのスコープの所有権があり、プロパティの表示を制限する場合。  
  
### <a name="to-hide-properties-that-have-child-properties"></a>子プロパティを持つプロパティを非表示にするには  
  
1. パラメーターを `pfDisplay` に設定 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.DisplayChildProperties%2A> `FALSE` します。  
  
2. パラメーターを `pfHide` に設定 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HideProperty%2A> `TRUE` します。  
  
## <a name="see-also"></a>参照  
 [プロパティ表示グリッド](../extensibility/internals/properties-display-grid.md)