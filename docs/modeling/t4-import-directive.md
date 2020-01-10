---
title: T4 インポート ディレクティブ
ms.date: 11/04/2016
ms.topic: reference
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2a28bedd01e3a4f6a7a87b025ac9a9a6184da9b2
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75591867"
---
# <a name="t4-import-directive"></a>T4 インポート ディレクティブ

`import`ディレクティブにより、Visual Studio T4 テキスト テンプレートのコード ブロックにおいて、完全修飾名を指定せずに別の名前空間内の要素を参照を使用することができるようになります。 このディレクティブは、C# の `using` または `imports` の [!INCLUDE[vb_current_short](../debugger/includes/vb_current_short_md.md)] に相当します。

T4 テキスト テンプレートの作成方法の一般的な概要については、次を参照してください。 [T4 テキスト テンプレートの作成](../modeling/writing-a-t4-text-template.md)

## <a name="using-the-import-directive"></a>import ディレクティブの使用

```
<#@ import namespace="namespace" #>
```

 この例では、テンプレート コードで System.IO のメンバーの明示的な名前空間を省略できます。

```
<#@ import namespace="System.IO" #>
<#
   string fileContent = File.ReadAllText("C:\x.txt"); // System.IO.File
#>
The file contains: <#=  fileContent #>
```

## <a name="standard-imports"></a>標準インポート
 次の名前空間は自動的にインポートされるので、この名前空間のインポート ディレクティブを記述する必要はありません。

- `System`

  また、カスタム ディレクティブを使用する場合は、ディレクティブ プロセッサによって一部の名前空間が自動的にインポートされます。

  たとえば、ドメイン固有言語 (DSL) のテンプレートを作成する場合、次の名前空間のインポート ディレクティブを記述する必要はありません。

- `Microsoft.VisualStudio.Modeling`

- DSL の名前空間

## <a name="see-also"></a>関連項目

- [T4 アセンブリ ディレクティブ](../modeling/t4-assembly-directive.md)
