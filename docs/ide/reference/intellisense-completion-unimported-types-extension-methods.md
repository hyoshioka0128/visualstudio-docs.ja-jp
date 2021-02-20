---
title: 型と拡張メソッドに対する IntelliSense 入力候補
description: '`using` ディレクティブでまだインポートしていない型と拡張メソッドに対して IntelliSense 入力候補を使用する方法です。'
ms.custom: SEO-VS-2020
ms.date: 07/27/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 2b73b4d73c36215b70b7551298492e39b69e179f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99852337"
---
# <a name="intellisense-completion-for-unimported-types-and-extension-methods"></a>インポートされていない型と拡張メソッドに対する IntelliSense 入力候補

このリファクタリングは以下に適用されます。

- C#

- Visual Basic

**概要:** IntelliSense からは、インポートされていない型と拡張メソッドに対して入力候補が提示されます。

**条件:** プロジェクト内に既に依存関係があるが、using ステートメントがファイルにまだ追加されていない型または拡張メソッドを使用する必要があります。

**理由:** using ステートメントをファイルに手動で追加する必要はありません。

## <a name="how-to"></a>方法

1. プロジェクト内に依存関係のある型または拡張メソッドの名前の入力を始めると、IntelliSense から入力候補が提示されます。 インポートされていない名前空間からの項目には、それが含まれている名前空間がサフィックスとして表示されることがあります。

   > [!TIP]
   > インポートされていない名前空間は、入力候補一覧の左下に表示される **展開ボタン (Alt + A)** を使用することで、必要に応じて表示したり、非表示にしたりできます。 既定の動作を変更するには、 **[ツール]** 、 **[オプション]** 、 **[テキスト エディター]**  > 、 **[C#]** 、 **[Basic]** 、 **[IntelliSense]** の順に進み、 **[インポートされていない名前空間の項目を表示する]** を探します。

2. インポートされていない項目を選択し、コミットします。

   using ステートメントがファイルに自動的に追加されます。

   ![インポートされていない型に対する IntelliSense 入力候補](media/intellisense-completion-unimported-types.png)

## <a name="see-also"></a>関連項目

- [IntelliSense](../using-intellisense.md)
- [リファクタリング](../refactoring-in-visual-studio.md)
