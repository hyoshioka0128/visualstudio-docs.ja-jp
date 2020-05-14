---
title: クラス デザイナーの C++ 構造体
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Class Designer [Visual Studio], structures
ms.assetid: bad18ab6-d956-47a6-a413-811cc26db5f5
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 2aa8014835df2b5b2bd3dc68e2aaf0b079e001e8
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75590685"
---
# <a name="c-structures-in-class-designer"></a>クラス デザイナーの C++ 構造体

**クラス デザイナー**は、C++ の構造体をサポートしています。これは、`struct` キーワードを使用して宣言されます。 たとえば次のようになります。

```cpp
struct MyStructure
{
   char a;
   int i;
   long j;
};
```

`struct` 型の使用法の詳細については、「[struct](/cpp/cpp/struct-cpp)」を参照してください。

クラス ダイアグラムにおける C++ 構造体の図形の形状と動作はクラスの図形に似ていますが、ラベルが **[Struct]** である点と、角が丸くなく直角である点が異なります。

|コード要素|クラス デザイナー ビュー|
|------------------| - |
|`struct StructureName {};`|**StructureName**<br /><br /> 構造体|

## <a name="see-also"></a>参照

- [C++ のコードを操作する](working-with-visual-cpp-code.md)
- [クラスと構造体](/cpp/cpp/classes-and-structs-cpp)
- [struct](/cpp/cpp/struct-cpp)
