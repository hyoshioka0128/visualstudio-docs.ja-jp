---
title: 'ワークフローデザイナー: XAML のデバッグ'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: d9305dbc-af62-4bdd-b03f-c54e3fe9ecc7
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- uwp
ms.openlocfilehash: 81c3e20e858fb8501c1c1a564a91270af6a4aaa3
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75593942"
---
# <a name="how-to-debug-xaml-with-the-workflow-designer"></a>ワークフロー デザイナーを使用して XAML をデバッグする方法

ワークフローは XAML で定義されます。 ワークフローの UI 表現は、ワークフローを定義する XAML ツリーに基づいて構築されます。 デバッグエクスペリエンスは、ワークフローデザイナーでのワークフローのデバッグに似ています。 たとえば、XAML のデバッグ中に、[ローカル]、[ウォッチ]、および [スレッド] の各ウィンドウは、ワークフローデザイナーデバッグと同じように動作します。 また、XAML のデバッグ中に使用される呼び出し履歴ビューは、ワークフローの実行フローの行ベースの階層ビューです。

> [!NOTE]
> ワークフローの XAML がアクティビティと同じアセンブリ内にある場合、クラス名のアセンブリ部分は含まれません。 クラス (アクティビティ) 名のこの部分がないと、XAML を実行時に読み込むことができません。 メイン プロジェクトと同じ名前空間でアクティビティを定義することはお勧めしません。定義した場合は、XAML をデザイナーで編集した後に手動で編集する必要があります。

## <a name="to-debug-workflow-xaml"></a>ワークフローの XAML をデバッグするには

1. Visual Studio でワークフローまたはアクティビティプロジェクトを開きます。

2. 「[方法: ワークフローにブレークポイントを設定する](../workflow-designer/how-to-set-breakpoints-in-workflows.md)」の説明に従って、デバッグするアクティビティにブレークポイントを設定します。

3. ワークフロー定義が含まれている .xaml ファイルを右クリックし、 **[コードの表示]** を選択します。 デザイン ビューでブレークポイントを設定したアクティビティの XAML 要素宣言と同じ行に、ブレークポイントが表示されます。

4. 「[デバッグワークフロー](debugging-workflows-with-the-workflow-designer.md)」で説明されているように、デバッガーを起動します。

5. コードがいずれかのブレークポイントまで実行されると、そのブレークポイントに関連付けられている XAML 要素が強調表示されます。 次のブレークポイントに移動するには、 **F10**キーまたは**F11**キーを使用します。

## <a name="see-also"></a>関連項目

- [方法 : ワークフロー内のブレークポイントを設定する](../workflow-designer/how-to-set-breakpoints-in-workflows.md)
- [ワークフローのデバッグ](debugging-workflows-with-the-workflow-designer.md)
