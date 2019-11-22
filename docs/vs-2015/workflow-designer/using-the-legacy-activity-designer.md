---
title: Using the Legacy Activity Designer | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- activities, configuring
- custom activities
- Activity Designer
- child activities, adding
- activities, adding child
- activities, creating custom
ms.assetid: 2fea8a05-6e58-423d-94bf-a822b15ffb80
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a13aeeb3394ee6b8896376c0e7d520b90fb56fa6
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74302824"
---
# <a name="using-the-legacy-activity-designer"></a>従来のアクティビティ デザイナーの使用
このトピックでは、従来の [!INCLUDE[wfd1](../includes/wfd1-md.md)]でアクティビティ デザイナーを使用する方法について説明します。 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] または [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] を対象とする場合は、従来のデザイナーを使用します。

 アクティビティ デザイナーを使用すると、独自のカスタム アクティビティを作成できます。

## <a name="creating-a-custom-activity"></a>カスタム アクティビティの作成
 アクティビティ デザイナを使ってカスタム アクティビティを作成するには、次の手順に従います。

1. On the **Project** menu, click **Add Activity**.

2. Select the **Activity** or **Activity (with code separation)** template.

   1. Use the **Activity** template to create an activity with the activity definition and the user code in same code file.

   2. Use the **Activity (with code separation)** template to create an activity with the activity definition expressed as workflow markup and the user code in a separate code file.

3. Type an activity name or keep the default name, and then click **Add**.

   You can also create a set of custom activities by creating a new project of type **Workflow Activity Library**. For more information about this project type, see [How to: Create a Workflow Activity Library (Legacy)](../workflow-designer/how-to-create-a-workflow-activity-library-legacy.md).

## <a name="configuring-an-activity"></a>アクティビティの構成
 アクティビティ デザイナがアクティブであるときに、プロパティ ブラウザを使用すると、次の表にリストされているプロパティを構成できます。

|property|コメント|
|--------------|--------------|
|**Name**|アクティビティの名前。|
|**Base Class**|アクティビティの派生元の基本クラス。 The default base class is [SequenceActivity](https://go.microsoft.com/fwlink?LinkID=65020). In the **Properties** window, click the **Base Class** ellipses **[…]** to select another base class in the [Browse and Select a .NET Type Dialog Box (Legacy)](../workflow-designer/browse-and-select-a-dotnet-type-dialog-box-legacy.md).|
|**説明**|アクティビティに関するユーザー定義の説明。|
|**Enabled**|Set to **True** by default to enable activity execution and validation. Set to **False** to disable activity execution and validation. For information about activity execution and validation, see [Developing Workflow Activities](https://go.microsoft.com/fwlink?LinkID=65024).|

## <a name="adding-child-activities"></a>子アクティビティの追加
 子アクティビティを、ツールボックスから設計中のアクティビティまでドラッグすることができます。 その後、プロパティ ブラウザを使ってそれぞれの子アクティビティを構成できます。

## <a name="see-also"></a>参照
 [Developing Workflow Activities](https://go.microsoft.com/fwlink?LinkID=65024) [Creating Custom Activities](https://go.microsoft.com/fwlink?LinkID=65021) [Legacy Workflow Activities](../workflow-designer/legacy-workflow-activities.md) [Custom Activities Samples](https://go.microsoft.com/fwlink?LinkID=65022) [How to: Create a Workflow Activity Library (Legacy)](../workflow-designer/how-to-create-a-workflow-activity-library-legacy.md) [Using the Legacy Workflow Designer](../workflow-designer/using-the-legacy-workflow-designer.md)