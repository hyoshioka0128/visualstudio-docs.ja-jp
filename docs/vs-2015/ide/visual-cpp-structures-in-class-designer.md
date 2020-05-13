---
title: クラス デザイナーの Visual C++ 構造体 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- Class Designer [Visual Studio], structures
ms.assetid: bad18ab6-d956-47a6-a413-811cc26db5f5
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: fc9c09c5f92c4193d3d3f58c819f4bc0fc9aaebf
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72646763"
---
# <a name="visual-c-structures-in-class-designer"></a>クラス デザイナーの Visual C++ 構造体
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

クラス デザイナーは、C++ の構造体をサポートしています。これは、`struct` キーワードを使用して宣言されます。 例を次に示します。

```
struct MyStructure
{
   char a;
   int i;
   long j;
};
```

 `struct` 型の使用法の詳細については、「[struct](https://msdn.microsoft.com/library/3c6ba273-e248-4ff1-8c69-d2abcf1263c6)」を参照してください。

 クラス ダイアグラムにおける C++ 構造体の図形の形状と動作はクラスの図形に似ていますが、ラベルが **[Struct]** である点と、角が丸くなく直角である点が異なります。

|コード要素|クラス デザイナー ビュー|
|------------------|-------------------------|
|`struct StructureName {};`|**StructureName**<br /><br /> 構造体|

## <a name="see-also"></a>関連項目
 [Visual C++ Code (クラスデザイナー)](../ide/working-with-visual-cpp-code-class-designer.md) [クラスと](https://msdn.microsoft.com/library/516dd496-13fb-4f17-845a-e9ca45437873)struct[構造体](https://msdn.microsoft.com/library/3c6ba273-e248-4ff1-8c69-d2abcf1263c6)の操作
