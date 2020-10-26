---
title: '方法: ワークフローデザイナーを使用して XAML をデバッグする |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: d9305dbc-af62-4bdd-b03f-c54e3fe9ecc7
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a696123551c24fd0d14fecde67826cf14f88826f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72668645"
---
# <a name="how-to-debug-xaml-with-the-workflow-designer"></a>ワークフロー デザイナーを使用して XAML をデバッグする方法
ワークフローは XAML で定義されます。 ワークフローの UI 表現は、ワークフローを定義する XAML ツリーに基づいて構築されます。 デバッグ作業は、[!INCLUDE[wfd1](../includes/wfd1-md.md)]でのワークフローのデバッグと同様です。 たとえば、XAML のデバッグ中に、ローカル、ウォッチ、およびスレッドの各ウィンドウは、[!INCLUDE[wfd2](../includes/wfd2-md.md)]でのデバッグ時と同様に機能します。 また、XAML のデバッグ中に使用される呼び出し履歴ビューは、ワークフローの実行フローの行ベースの階層ビューです。

> [!NOTE]
> ワークフローの XAML がアクティビティと同じアセンブリ内にある場合、クラス名のアセンブリ部分は含まれません。 クラス (アクティビティ) 名のこの部分がないと、実行時に XAML を読み込むことはできません。 メイン プロジェクトと同じ名前空間でアクティビティを定義することはお勧めしません。定義した場合は、XAML をデザイナーで編集した後に手動で編集する必要があります。

### <a name="to-debug-workflow-xaml"></a>ワークフローの XAML をデバッグするには

1. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] でワークフロー プロジェクトまたはアクティビティ プロジェクトを開きます。

2. 「 [方法: ワークフローにブレークポイントを設定する](../workflow-designer/how-to-set-breakpoints-in-workflows.md)」の説明に従って、デバッグするアクティビティにブレークポイントを設定します。

3. ワークフロー定義が含まれている .xaml ファイルを右クリックし、[ **コードの表示**] を選択します。 デザイン ビューでブレークポイントを設定したアクティビティの XAML 要素宣言と同じ行に、ブレークポイントが表示されます。

4. 「 [方法: ワークフローデバッガーを呼び出す](../workflow-designer/how-to-invoke-the-workflow-debugger.md)」の説明に従って、デバッガーを呼び出します。

5. コードがいずれかのブレークポイントまで実行されると、そのブレークポイントに関連付けられている XAML 要素が強調表示されます。 次のブレークポイントに移動するには、 **F10** キーまたは **F11** キーを使用します。

## <a name="see-also"></a>参照
 [方法: ワークフローにブレークポイントを設定](../workflow-designer/how-to-set-breakpoints-in-workflows.md)[する方法: ワークフローデバッガーを呼び出す](../workflow-designer/how-to-invoke-the-workflow-debugger.md)