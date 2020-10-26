---
title: '方法: インポートデザイナーを使用する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Presentation.View.ImportDesigner.UI
ms.assetid: 61328ab6-9b66-4e12-8630-22e30ee8c9d1
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 47b5055cca0b00e7fdec49947df13b473a090aaf
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72659081"
---
# <a name="how-to-use-the-imports-designer"></a>インポート デザイナーを使用する方法
インポート デザイナーを使用すると、式で使用する型の名前空間を入力できます。 Visual Basic .NET と C# での **imports** または **using** キーワードと同様に、imports デザイナーで名前空間を指定すると、完全修飾バージョンの型名ではなく、式に型名を入力するだけで済みます。

 インポート デザイナーでは、UI での変更とワークフローの保存時に行われる変更の両方に応じて処理を行います。 ワークフローの保存時に、インポート デザイナーに名前空間を自動的に追加できます。 コーディネートは次のとおりです。

- 変数および引数の宣言で使用されている型の名前空間。

- 式で使用されている型の名前空間。

- ワークフローをシリアル化するために必要な、上記以外の名前空間 (ワークフロー内で削除されたカスタム アクティビティで使用した名前空間など)。

  ワークフローを保存すると、手動で削除したいくつかの名前空間がインポート デザイナーに自動的に再度追加されることがあります。これは、上記の一覧で説明したロジックによるものです。

### <a name="to-add-a-namespace-to-the-list-of-imported-namespaces"></a>名前空間をインポートされた名前空間の一覧に追加するには

1. WCF ワークフロー サービス アプリケーション、ワークフロー コンソール アプリケーション、[!INCLUDE[vs2010](../includes/vs2010-md.md)] のアクティビティ ライブラリ プロジェクト、または再ホストされたワークフロー アプリケーションのアクティビティ ライブラリ プロジェクトを開きます。

2. メインキャンバスの下部にある [ **インポート** ] をクリックします。 インポート デザイナーが表示されます。

3. 名前空間を入力するか、インポート デザイナーの上部にあるドロップダウン リスト コントロールから名前空間を選択します。

     入力すると、入力した文字に一致する有効な名前空間の一覧が表示されます。

4. 名前空間を一覧に追加するには、 **enter** キーを押します。

5. 一覧から名前空間を削除する場合は、名前空間を選択し、キーボードの **del** キーを押します。 名前空間が削除できるのは、たとえば、名前空間を含むアセンブリがプロジェクトによって参照されなくなる場合など、名前空間がなんらかの理由で無効である場合のみであることに注意してください。