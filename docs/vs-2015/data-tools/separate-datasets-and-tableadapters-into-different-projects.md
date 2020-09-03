---
title: データセットと Tableadapter を別々のプロジェクトに分離する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- TableAdapters, n-tier applications
- n-tier applications, separating Datasets and TableAdapters
ms.assetid: f66a3940-6227-46af-a930-9177f425f4fd
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6f6ec76e79cc1c4759cbe05d8bdcacc1297b655b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72655430"
---
# <a name="separate-datasets-and-tableadapters-into-different-projects"></a>データセットと TableAdapters を別々のプロジェクトに分離する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

型指定されたデータセットが拡張され、 [tableadapter](https://msdn.microsoft.com/library/09416de9-134c-4dc7-8262-6c8d81e3f364) とデータセットクラスを別々のプロジェクトに生成できるようになりました。 これにより、アプリケーション層を分離して、n 層データ アプリケーションをすばやく生成できるようになります。

 次の手順では、データセットデザイナーを使用して、生成されたコードを含むプロジェクトとは別のプロジェクトにデータセットコードを生成するプロセスについて説明し `TableAdapter` ます。

## <a name="separatedatasets-and-tableadapters"></a>Separatedatasets と Tableadapter
 データセットコードをコードから分離する場合は、 `TableAdapter` データセットコードを含むプロジェクトを現在のソリューションに配置する必要があります。 このプロジェクトが現在のソリューションに配置されていない場合、[**プロパティ**] ウィンドウの [**データセットプロジェクト**] の一覧では使用できません。

 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

#### <a name="to-separate-the-dataset-into-a-different-project"></a>データセットを別のプロジェクトに分離するには

1. データセット (.xsd ファイル) を含むソリューションを開きます。

   > [!NOTE]
   > データセットコードを分離するプロジェクトがソリューションに含まれていない場合は、プロジェクトを作成するか、既存のプロジェクトをソリューションに追加します。

2. **ソリューション エクスプローラー**で型指定されたデータセット ファイル (.xsd ファイル) をダブルクリックして、**データセット デザイナー**でデータセットを開きます。

3. **データセットデザイナー**の空の領域を選択します。

4. [ **プロパティ** ] ウィンドウで、[ **データセットプロジェクト** ] ノードを見つけます。

5. [ **データセットプロジェクト** ] ボックスの一覧で、データセットコードを生成するプロジェクトの名前を選択します。

    データセットコードを生成するプロジェクトを選択すると、既定のファイル名が **データセットファイル** のプロパティに設定されます。 必要に応じて、この名前を変更できます。 さらに、データセット コードを特定のディレクトリに生成する場合は、**[プロジェクト フォルダー]** プロパティをフォルダーの名前に設定できます。

   > [!NOTE]
   > データセットと Tableadapter を分離すると ( **DataSet プロジェクト** プロパティを設定することによって)、プロジェクト内の既存の部分データセットクラスは自動的には移動されません。 既存のデータセット部分クラスは、データセットプロジェクトに手動で移動する必要があります。

6. データセットを保存します。

    データセットコードは、 **データセットプロジェクト** のプロパティで選択されたプロジェクトに生成され、 **TableAdapter** コードは現在のプロジェクトに生成されます。

   既定では、データセットと `TableAdapter` コードを分離すると、結果としてプロジェクトごとに別個のクラス ファイルが生成されます。 元のプロジェクトには、コードを含む DatasetName (または DatasetName.Designer.cs) という名前のファイルがあり `TableAdapter` ます。 " **Dataset プロジェクト** " プロパティで指定されているプロジェクトには、データセットコードを含む DatasetName (または DatasetName.DataSet.Designer.cs) という名前のファイルがあります。

> [!NOTE]
> 生成されたクラスファイルを表示するには、データセットまたはプロジェクトを選択し `TableAdapter` ます。 次に、  **ソリューションエクスプローラー**で [ **すべてのファイルを表示** ] を選択します。

## <a name="see-also"></a>参照
 [N 層データアプリケーションの概要](../data-tools/n-tier-data-applications-overview.md)[チュートリアル: n 層データアプリケーション](../data-tools/walkthrough-creating-an-n-tier-data-application.md)[の作成 Visual Studio でのデータへのアクセスの](../data-tools/accessing-data-in-visual-studio.md)[階層更新](../data-tools/hierarchical-update.md) [ADO.NET](https://msdn.microsoft.com/library/5b96ed06-9759-4966-a797-a1d5f6ee50ca)
