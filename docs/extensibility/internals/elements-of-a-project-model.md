---
title: プロジェクトモデル | の要素Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], implementation considerations
- project models
- projects [Visual Studio SDK], elements
ms.assetid: a1dbe0dc-68da-45d7-8704-5b43ff7e4fc4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cf847e35878dc84bb32fe81053c01c23e565fc4c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80708522"
---
# <a name="elements-of-a-project-model"></a>プロジェクトモデルの要素
のすべてのプロジェクトのインターフェイスと実装は、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 基本構造を共有します。プロジェクトの種類のプロジェクトモデルです。 開発中の VSPackage であるプロジェクトモデルでは、設計上の決定に準拠したオブジェクトを作成し、IDE によって提供されるグローバル機能と連携します。 たとえば、プロジェクト項目を永続化する方法を制御しますが、ファイルを永続化する必要があるという通知は制御しません。 開いているプロジェクト項目にフォーカスを移動し、メニューバーの [**ファイル**] メニューの [**保存**] を選択した場合 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 、プロジェクトの種類のコードは ide からコマンドをインターセプトし、ファイルを永続化して、ファイルが変更されていないことを ide に通知を送信する必要があります。

 VSPackage は、IDE インターフェイスへのアクセスを提供するサービスを介して IDE と対話します。 たとえば、特定のサービスを使用して、コマンドを監視およびルーティングし、プロジェクトで行われた選択に関するコンテキスト情報を提供します。 VSPackage に必要なすべてのグローバル IDE 機能は、サービスによって提供されます。 サービスの詳細については、「 [方法: サービスを取得](../../extensibility/how-to-get-a-service.md)する」を参照してください。

 その他の実装に関する考慮事項:

- 1つのプロジェクトモデルには、複数のプロジェクトの種類を含めることができます。

- プロジェクトの種類とアテンダントプロジェクトファクトリは、Guid とは別に登録されます。

- ユーザーが UI を使用して新しいプロジェクトを作成するときに、新しいプロジェクトファイルを初期化するには、各プロジェクトにテンプレートファイルまたはウィザードが必要です [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 たとえば、テンプレートは [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 最終的に .vcproj ファイルとなるものを初期化します。

  次の図は、一般的なプロジェクトの実装を構成する主要なインターフェイス、サービス、およびオブジェクトを示しています。 アプリケーションヘルパー () を使用して、 `HierUtil7` 基になるオブジェクトやその他のプログラミング定型を作成できます。 アプリケーションヘルパーの詳細につい `HierUtil7` ては、「 [HierUtil7 プロジェクトクラスを使用してプロジェクトの種類を実装する (C++)](https://msdn.microsoft.com/library/a5c16a09-94a2-46ef-87b5-35b815e2f346)」を参照してください。

  ![Visual Studio プロジェクトモデルグラフィック](../../extensibility/internals/media/vsprojectmodel.gif "vsProjectModel") プロジェクトモデル

  上の図に示されているインターフェイスとサービスの詳細、および図に含まれていないその他のオプションのインターフェイスについては、「 [プロジェクトモデルのコアコンポーネント](../../extensibility/internals/project-model-core-components.md)」を参照してください。

  プロジェクトはコマンドをサポートできます。したがって、コマンド <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> コンテキスト guid を使用してコマンドルーティングに参加するには、インターフェイスを実装する必要があります。

## <a name="see-also"></a>関連項目
- [チェックリスト: 新しいプロジェクトの種類を作成する](../../extensibility/internals/checklist-creating-new-project-types.md)
- [HierUtil7 プロジェクトクラスを使用してプロジェクトの種類を実装する (C++)](https://msdn.microsoft.com/library/a5c16a09-94a2-46ef-87b5-35b815e2f346)
- [プロジェクトモデルコアコンポーネント](../../extensibility/internals/project-model-core-components.md)
- [プロジェクトファクトリを使用したプロジェクトインスタンスの作成](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)
- [方法: サービスを取得する](../../extensibility/how-to-get-a-service.md)
- [プロジェクトの種類の作成](../../extensibility/internals/creating-project-types.md)
