---
title: '[参照設定] ページ (プロジェクト デザイナー) (Visual Basic)'
description: '[プロジェクト デザイナー] の [参照] ページを利用して、プロジェクトの参照、Web 参照、インポートした名前空間を管理する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 06/21/2017
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesReference
- vb.ProjectPropertiesUnusedReference
- vb.ProjectPropertiesReferencePaths
helpviewer_keywords:
- References page in Project Designer
- Project Designer, References page
ms.assetid: 5a47c595-e084-401c-86e1-74e0bf74fd86
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 30e3847c87559fd7a916af8ad3be48343d649671
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99958142"
---
# <a name="references-page-project-designer-visual-basic"></a>[参照設定] ページ (プロジェクト デザイナー) (Visual Basic)

**[プロジェクト デザイナー]** の **[参照]** ページを利用し、プロジェクトの参照、Web 参照、インポートした名前空間を管理します。 プロジェクトには、COM コンポーネント、XML Web サービス、.NET ライブラリまたはアセンブリ、その他のクラス ライブラリの参照を含めることができます。 参照の使用方法については、「[プロジェクト内の参照の管理](../../ide/managing-references-in-a-project.md)」を参照してください。

**[参照]** ページにアクセスするには、**ソリューション エクスプローラー** のプロジェクト ノード (**[ソリューション]** ノードではありません) を選択します。 その後、メニュー バーで **[プロジェクト]**、**[プロパティ]** の順に選択します。 プロジェクト デザイナーが表示されたら、**[参照]** タブをクリックします。

## <a name="uielement-list"></a>UIElement の一覧

次のオプションを使用すると、プロジェクトの参照やインポートした名前空間を選択または削除できます。

**参照パス**

このボタンをクリックすると、**[参照パス]** ダイアログ ボックスにアクセスします。

> [!NOTE]
> プロジェクト システムでは、検出されたアセンブリ参照が解決されます。解決するとき、次の場所で次の順序で検索されます。
>
> 1. プロジェクト フォルダー。 **[すべてのファイルを表示]** が有効になっていないとき、**ソリューション エクスプローラー** にプロジェクト フォルダー ファイルが表示されます。
> 2. **[参照パス]** ダイアログ ボックスに指定されているフォルダー。
> 3. **[参照の追加]** ダイアログ ボックスでファイルを表示するフォルダー。
> 4. プロジェクトの obj フォルダー。 (プロジェクトに COM 参照を追加するとき、1 つまたは複数のアセンブリをプロジェクトの obj フォルダーに追加できることがあります。)

 **参照**

この一覧には、使用か未使用かを問わず、プロジェクトのすべての参照が表示されます。

 **[追加]**

このボタンをクリックすると、参照または Web 参照が **[参照]** 一覧に追加されます。

[参照の追加] ダイアログ ボックスを利用してプロジェクトに参照を追加するには、**[参照]** を選択します。

**[Web 参照の追加]** ダイアログ ボックスを利用してプロジェクトに Web 参照を追加するには、**[Web 参照]** を選択します。

 **削除**

**[参照]** 一覧で 1 つまたは複数の参照を選択し、このボタンをクリックして削除します。

 **[Web 参照の更新]**

**[参照]** 一覧の Web 参照を選択し、このボタンをクリックして更新します。

 **[インポートされた名前空間]**

このボックスに独自の名前空間を入力し、**[ユーザー インポートの追加]** をクリックし、名前空間一覧に追加します。

ユーザーがインポートした名前空間にエイリアスを作成できます。 これを行うには、*エイリアス*=*名前空間* の形式でエイリアスと名前空間を入力します。 これは、`Http= MyOrg.ObjectLib.Internet.WebRequestMethods.Http` のような、長い名前空間を使用する場合に便利です。

 **[ユーザー インポートの追加]**

このボタンをクリックし、**[インポートされた名前空間]** ボックスに指定されている名前空間をインポートした名前空間の一覧に追加します。 このボタンは、指定の名前空間が一覧にまだない場合にのみ有効になります。

 **[名前空間の一覧]**

この一覧には、利用可能なすべての名前空間が表示されます。 プロジェクトに含まれている名前空間のチェック ボックスが選択されます。

 **[ユーザー インポートの更新]**

名前空間の一覧でユーザー指定の名前空間を選択し、**[インポートされた名前空間]** ボックスにその新しい名前を入力し、このボタンをクリックして新しい名前空間に変更します。 このボタンは、選択した名前空間が **[ユーザー インポートの追加]** ボタンを利用して一覧に追加した名前空間の場合にのみ表示されます。 以下を追加できます。

- <xref:System.Math?displayProperty=fullName> など、クラスまたは名前空間。

- `VB=Microsoft.VisualBasic` など、エイリアスが付けられたインポート。

- `<xmlns:xsl="http://www.w3.org/1999/XSL/Transform">` など、XML 名前空間。

## <a name="see-also"></a>関連項目

- [プロジェクト内の参照の管理](../../ide/managing-references-in-a-project.md)
- [方法: インポートした名前空間を追加または削除する (Visual Basic)](../../ide/how-to-add-or-remove-imported-namespaces-visual-basic.md)
- [Imports ステートメント (XML 名前空間)](/dotnet/visual-basic/language-reference/statements/imports-statement-xml-namespace)
