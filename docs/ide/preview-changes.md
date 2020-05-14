---
title: コード変更のプレビュー
ms.date: 12/16/2016
ms.topic: conceptual
author: TerryGLee
ms.author: tglee
manager: jillfra
f1_keywords:
- vs.codefix.previewchanges
ms.workload:
- multiple
ms.openlocfilehash: f45b186153b4cc046d35fd941f6a80e108476fc0
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75585770"
---
# <a name="preview-changes-window"></a>[変更のプレビュー] ウィンドウ

Visual Studio でさまざまな*クイック アクション* ツールまたは*リファクタリング* ツールを使用すると、実施される変更を受け入れる前にプレビューできることがよくあります。 プレビューは、 **[変更のプレビュー]** で行います。  たとえば、ここでは、C# プロジェクトにおける名前の変更リファクタリング中に変更される内容が **[変更のプレビュー]** に表示されています。

![変更のプレビュー](media/previewchanges.png)

ウィンドウの上半分には、変更される特定の行が表示され、それぞれの行にチェックボックスが配置されています。 特定の行にのみ選択的にリファクタリングを適用する場合は、各チェック ボックスをオフまたはオフにします。

ウィンドウの下半分には、変更されるプロジェクトからの書式設定されたコードが表示され、影響を受ける部分が強調表示されています。 ウィンドウの上半分で特定の行を選択すると、ウィンドウの下半分で対応する行が強調表示されます。 これにより、該当する行にすばやくスキップして、前後のコードを確認することができます。

変更内容を確認したら、 **[適用]** ボタンをクリックして該当する変更をコミットするか、 **[キャンセル]** をクリックして元のままにしておきます。

## <a name="see-also"></a>参照

- [Visual Studio でのリファクタリング](../ide/refactoring-in-visual-studio.md)
- [クイック アクション](../ide/quick-actions.md)
