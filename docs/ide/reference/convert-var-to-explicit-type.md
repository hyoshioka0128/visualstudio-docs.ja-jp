---
title: var を明示的な型に置き換えるコードのリファクタリング
ms.date: 05/15/2018
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 4ec388564e1851402f085f6bbaefba08dbea212c
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75595775"
---
# <a name="refactoring-to-replace-var-with-an-explicit-type"></a>var を明示的な型に置き換えるリファクタリング

このリファクタリングは、ローカル変数宣言内の [var](/dotnet/csharp/language-reference/keywords/var) を明示的な型に置き換えるために使います。

このリファクタリングは以下に適用されます。

- C#

## <a name="why-to-use-an-explicit-type"></a>明示的な型を使用する理由

明示的な型で変数を宣言するには次のような理由があります。

- コードの読みやすさを向上させる。

- 宣言内で変数を初期化したくない。

ただし、変数を匿名型で初期化し、後でオブジェクトのプロパティへのアクセスが必要になる場合は、[var](/dotnet/csharp/language-reference/keywords/var) を使う必要があります。 詳細については、「[暗黙的に型指定されるローカル変数 (C#)](/dotnet/csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables)」を参照してください。

## <a name="how-to-use-it"></a>使用方法

1. キャレットを `var` キーワードに配置します。

1. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 またはコード ファイルの余白でねじ回し ![ねじ回しアイコン](../media/screwdriver-icon.png) アイコンをクリックします。

   ![明示的な型の使用クイック アクション メニュー](media/use-explicit-type.png)

1. **[明示的な型の使用]** を選びます。 または、 **[変更のプレビュー]** を選択して [[変更のプレビュー]](../../ide/preview-changes.md) ダイアログを開いて **[適用]** を選択します。

## <a name="see-also"></a>関連項目

- [暗黙的に型指定された変数 (C#)](/dotnet/csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables)
- [リファクタリング](../refactoring-in-visual-studio.md)
- [変更のプレビュー](../../ide/preview-changes.md)
