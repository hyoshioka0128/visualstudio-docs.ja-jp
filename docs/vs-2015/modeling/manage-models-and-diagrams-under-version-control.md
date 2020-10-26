---
title: バージョン管理の下でモデルと図を管理する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- models, version control
ms.assetid: ca6443e3-6d11-4da8-aae7-ca7dcc410076
caps.latest.revision: 32
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b30b13610cc59b8a0225e52abf47f9a4f2cc97d1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72657576"
---
# <a name="manage-models-and-diagrams-under-version-control"></a>モデルおよび図のバージョン管理
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

オンプレミスの Team Foundation Server やクラウド内の Visual Studio Team Services のいずれかで、 [Team Foundation バージョン管理や Git を使用](https://msdn.microsoft.com/library/33267cee-fe5f-4aa3-b2cd-6d22ceace314)して、コード マップ (.dgml ファイル) などのモデリング プロジェクトとダイアグラムの異なるバージョンを管理します。

 この機能をサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

> [!IMPORTANT]
> 同一のモデリング プロジェクトで複数のユーザーが作業している場合は注意してください。 [中規模や大規模のプロジェクトでモデルを整理](../modeling/structure-your-modeling-solution.md)する方法をご確認ください。

## <a name="files-in-a-modeling-project"></a><a name="ModelingProjects"></a> モデリングプロジェクト内のファイル
 作業対象のファイルが異なっている限り、複数のユーザーが同時にモデリング プロジェクトに対して作業できます。

 異なるユーザーによって加えられた変更間の競合を回避または解決するには、モデルがどのようにファイルに格納されるかを理解することが重要です。

- 各パッケージは、 **.uml** プロジェクト フォルダー内の別個の **ModelDefinition** ファイルに格納されます。 モデルには、 **.uml** ファイルも含まれています。 これらのファイルのいずれかが削除されたり破損したりした場合、対応するパッケージまたはモデルは失われます。

- それぞれの図は、2 つのファイルに保存されます。 たとえば、クラス図は、次の 2 つのファイルから構成されます。

  - **DiagramName.classdiagram** : このファイルが削除されたり破損したりした場合は、図が失われます。ただし、表示されていたクラスおよび関連はモデル内に残っているため、UML モデル エクスプローラーに表示できます。

  - **DiagramName.classdiagram.layout** : このファイルが削除された場合、シェイプは図に表示されますが、そのサイズと位置は失われます。 それぞれのレイアウト ファイルは、図ファイルに関連付けられています。 レイアウト ファイルを表示するには、ソリューション エクスプローラーで図ファイルの横の [+] をクリックします。

> [!NOTE]
> ファイル間の一貫性を維持することが重要です。 たとえば、ソース管理を使用して .uml ファイルの変更をロールバックしたら、それに対応する変更を *diagram ファイルと .layout ファイルでも同時にロールバックする必要があります。 で表される要素。 \*uml ファイルにも表示されていない場合、ダイアグラムファイルは失われます。

## <a name="working-on-shared-modeling-projects"></a><a name="Shared"></a> 共有モデリングプロジェクトでの作業
 プロジェクトの異なる部分に対して同時に実行された作業間の競合を最小限に抑えるには、次の点に注意します。

- モデリング プロジェクトを異なる作業領域を表す複数のパッケージに分割します。 ルート モデル内にモデルを残さずに、モデル全体をパッケージに移動します。 詳細については、「 [Define packages and namespace](../modeling/define-packages-and-namespaces.md)」を参照してください。

- 異なるユーザーが同時に同じパッケージまたは図を操作しないようにしてください。

- プロファイルを使用している場合は、全員が同じプロファイルをインストールしていることを確認します。 「 [プロファイルとステレオタイプを使用してモデルをカスタマイズする](../modeling/customize-your-model-with-profiles-and-stereotypes.md)」を参照してください。

- 作業しているパッケージのみを変更していることを確実にするために、次の操作を行います。

  - UML クラス、コンポーネント、またはユース ケース図の **LinkedPackage** プロパティを設定する。

  - アクティビティまたは相互作用を生成した後、UML モデル エクスプローラーで即座にこれらをパッケージにドラッグする。 この要素は、アクティビティ図またはシーケンス図に最初のノードを生成したときに UML モデル エクスプローラーに表示されます。

- パッケージを追跡しやすくするために、実際のパッケージ名に合わせてパッケージ ファイルの名前を変更します。

- [!INCLUDE[esprscc](../includes/esprscc-md.md)]で、個々のファイルではなく、完全なモデリング プロジェクトに対して、 **[チェックイン]** と **[最新バージョンの取得]** の操作を実行します。

- **[取得]** 操作は、必ずモデリング プロジェクトをチェックインする直前に実行します。

- **[取得]** 操作を実行する前に、必ずすべての図を閉じます。

    > [!NOTE]
    > ファイルが開かれている状態で **[取得]** を実行し、その操作でローカルな変更が発生した場合は、ファイルの再読み込みが求められます。 その場合は、 **[いいえ]** をクリックし、完全なプロジェクトを再度読み込みます。 **ソリューション エクスプローラー**で、モデリング プロジェクト ノードを右クリックし、 **[プロジェクトのアンロード]** をクリックします。次に、 **[プロジェクトの再読み込み]** をクリックします。

### <a name="changes-requiring-exclusive-access-to-the-model"></a><a name="Exclusive"></a> モデルへの排他アクセスが必要な変更
 次の種類の変更を行う前に、必ずプロジェクト全体に対してチェックアウト ロックを設定してください。

- 他のパッケージから参照される要素の名前の変更または削除。

- パッケージ境界をまたぐ関係のプロパティの変更。

- チェックアウト ロックについて詳しくは、「 [ファイルのチェックアウトと編集](https://msdn.microsoft.com/library/eb404d63-c448-4994-9416-3e6d50ec554a)」をご覧ください。

##### <a name="to-move-a-diagram-file-in-or-out-of-a-project-folder"></a>プロジェクト フォルダーの図ファイルの移動

1. **Visual Studio の開発者コマンド プロンプト**を開始します。

2. **tf rename** を使用して、図ファイルとその **.layout** ファイルを移動します。

     `tf rename sourcePath targetPath`

3. ソリューション エクスプローラーで、ファイルを右クリックし、 **[プロジェクトから除外]** をクリックします。

4. ファイルを追加先のフォルダーに追加します。

     ソリューション エクスプローラーで、追加先のフォルダーまたはプロジェクトを右クリックします。次に、 **[追加]** をポイントし、 **[既存の項目]** をクリックします。 ダイアログ ボックスで、図ファイルを選択します。次に、 **[追加]** をクリックします。 レイアウト ファイルは自動的に追加されます。

    > [!NOTE]
    > ファイルを別のプロジェクトに移動することはできません。

## <a name="merging-changes-in-model-files-and-diagrams"></a><a name="Merging"></a> モデルファイルとダイアグラムの変更のマージ
 1 つのモデルが複数のユーザーによって同時に操作された場合、モデル ファイルに加えられた変更をマージするよう [!INCLUDE[esprscc](../includes/esprscc-md.md)] から求められます。 前のセクションに説明したように別個のプロジェクトで作業することで、マージ操作のほとんどを回避できます。 通常、残りの競合は、自動的に安全にマージできます。 次の種類の変更の場合は、問題は発生しません。

- 生存線の種類。 生存線を相互作用 (シーケンス図) に追加する場合、既存の型から生存線を生成した場合を除き、その種類はルート モデルに保存されます。

- 新しいアクティビティおよび相互作用。最初にルート モデルに保存されます。

- 要素および関係の追加。

- パッケージ内でのみ参照される要素の名前の変更または削除。

## <a name="see-also"></a>参照
 アーキテクチャ共有モデルの[分析とモデリング](../modeling/analyze-and-model-your-architecture.md)[とダイアグラムのエクスポート](../modeling/share-models-and-exporting-diagrams.md)
