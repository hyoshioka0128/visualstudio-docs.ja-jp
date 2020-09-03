---
title: '方法: Windows Communication Foundation コントラクト操作を実装する (レガシ) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: d6aeb20e-fac8-4a9d-bd26-ae78bef96b41
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 1f6f54e781dfae15b4b1c1159d73ac3495b35c21
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72603863"
---
# <a name="how-to-implement-a-windows-communication-foundation-contract-operation-legacy"></a>方法: Windows Communication Foundation コントラクト操作を実装する (レガシ)
このトピックでは、[!INCLUDE[indigo1](../includes/indigo1-md.md)] または [!INCLUDE[wfd1](../includes/wfd1-md.md)] を対象とする従来の [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)]を使用して [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] コントラクト操作を実装する方法について説明します。

 **ReceiveActivity**アクティビティをツールボックスからワークフローデザインサーフェイスにドラッグすると、新しいコントラクトを作成するか、 [!INCLUDE[indigo2](../includes/indigo2-md.md)] 既存のコントラクトをインポートして操作を実装することになります。 コントラクトとその操作を選択または作成するには、[ [操作の選択] ダイアログボックス (レガシ)](../workflow-designer/choose-operation-dialog-box-legacy.md)を使用します。

### <a name="to-implement-a-wcf-contract-operation"></a>WCF コントラクト操作を実装するには

1. デザイナーで**ReceiveActivity**アクティビティをダブルクリックするか、[**プロパティ**] ペインの**serviceoperationinfo**プロパティの横にある省略記号をクリックします。

2. 次のいずれかの操作を行います。

   - ダイアログボックスの右上隅にある [ **コントラクトの追加** ] をクリックします。 新しい [!INCLUDE[indigo2](../includes/indigo2-md.md)] コントラクトおよび操作が作成されます。

      \- または -

   - ダイアログボックスの右上隅にある [ **インポート** ] をクリックします。 [ [.Net 型の参照と選択] ダイアログボックス (レガシ)](../workflow-designer/browse-and-select-a-dotnet-type-dialog-box-legacy.md) が開きます。 必要なコントラクトを含んでいるアセンブリまたはプロジェクトを検索します。 コントラクトを選択し、[ **OK]** をクリックします。

     コントラクトを作成またはインポートしたら、そのコントラクトに新しい操作を追加できます。 新しい操作を追加するには、コントラクトを選択し、ダイアログボックスの右上隅にある [ **操作の追加** ] をクリックします。 操作の追加が終了したら、手順 3. に進みます。

3. **ReceiveActivity**アクティビティに関連付ける操作を選択します。 操作の定義は、操作の名前、パラメータ、プロパティ、アクセス許可の設定を変更することにより、操作できます。

    名前を変更するには、[ **操作名** ] テキストボックスに新しい名前を入力します。

    操作のパラメーターにアクセスするには、[ **パラメーター** ] タブをクリックします。 パラメータの名前、型、方向の変更のほか、操作のパラメータの追加または削除を行うことができます。

    操作の保護レベルとサポートされているメッセージ交換機能にアクセスするには、[ **プロパティ** ] タブをクリックします。

    操作を実装できるグループを指定するには、[ **アクセス許可** ] タブをクリックします。

4. [ **OK]** をクリックすると、 **ReceiveActivity** アクティビティに実装している操作の操作名が表示されます。

5. **ReceiveActivity**アクティビティ内のその操作の実装に使用するワークフローアクティビティを配置します。

## <a name="see-also"></a>参照
 [[操作の選択] ダイアログボックス (レガシ)](../workflow-designer/choose-operation-dialog-box-legacy.md) [方法: WCF コントラクト操作を呼び出す (レガシ)](../workflow-designer/how-to-invoke-a-windows-communication-foundation-contract-operation-legacy.md) [レガシワークフローアクティビティ](../workflow-designer/legacy-workflow-activities.md)