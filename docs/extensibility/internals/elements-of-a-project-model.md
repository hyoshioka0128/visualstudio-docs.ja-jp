---
title: プロジェクト モデルの要素 |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708522"
---
# <a name="elements-of-a-project-model"></a>プロジェクト モデルの要素
すべてのプロジェクトのインターフェイスと実装は、プロジェクト[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]の種類のプロジェクト モデルという基本的な構造を共有します。 開発中の VSPackage であるプロジェクト モデルでは、設計上の決定に従い、IDE によって提供されるグローバルな機能と連携するオブジェクトを作成します。 たとえば、プロジェクト項目の永続化方法を制御しますが、ファイルを永続化する必要があるという通知は制御しません。 ユーザーが開いているプロジェクト項目にフォーカスを置き、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]メニュー バーの **[ファイル]** メニューの **[保存]** を選択すると、プロジェクトの種類コードは、IDE からコマンドを途中で受信し、ファイルを永続化し、ファイルが変更されなくなったことを示す通知を IDE に送信する必要があります。

 VSPackage は、IDE インターフェイスへのアクセスを提供するサービスを通じて IDE と対話します。 たとえば、特定のサービスを通じて、コマンドを監視およびルーティングし、プロジェクトで行われた選択に関するコンテキスト情報を提供します。 VSPackage に必要なすべてのグローバル IDE 機能は、サービスによって提供されます。 サービスの詳細については、「方法[: サービスを取得する 」を参照](../../extensibility/how-to-get-a-service.md)してください。

 その他の実装に関する考慮事項:

- 1 つのプロジェクト モデルに複数のプロジェクト タイプを含めることができます。

- プロジェクトの種類とアテンダント プロジェクト ファクトリは、GUID に個別に登録されます。

- ユーザーが UI を使用して新しいプロジェクトを作成するときに、新しいプロジェクト ファイルを初期化するには、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]各プロジェクトにテンプレート ファイルまたはウィザードが必要です。 たとえば、テンプレートは[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]最終的に .vcproj ファイルになるものを初期化します。

  次の図は、一般的なプロジェクト実装を構成する主要なインターフェイス、サービス、およびオブジェクトを示しています。 アプリケーション ヘルパー を使用して`HierUtil7`、基になるオブジェクトやその他のプログラミング の定型句を作成できます。 アプリケーション ヘルパーの`HierUtil7`詳細については、「 [HierUtil7 プロジェクト クラスを使用してプロジェクトの種類を実装する (C++)」](https://msdn.microsoft.com/library/a5c16a09-94a2-46ef-87b5-35b815e2f346)を参照してください。

  ![プロジェクト モデル グラフィック](../../extensibility/internals/media/vsprojectmodel.gif "プロジェクトモデル")プロジェクト モデル

  前の図に示したインターフェイスとサービス、および図に含まれていないその他のオプション のインターフェイスの詳細については、「[プロジェクト モデルのコア コンポーネント](../../extensibility/internals/project-model-core-components.md)」を参照してください。

  プロジェクトはコマンドをサポートできるため、コマンド<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>コンテキスト GUID を介したコマンド ルーティングに参加するインターフェイスを実装する必要があります。

## <a name="see-also"></a>関連項目
- [チェックリスト: 新しいプロジェクトの種類を作成する](../../extensibility/internals/checklist-creating-new-project-types.md)
- [HierUtil7 プロジェクト クラスを使用してプロジェクトの種類を実装する (C++)](https://msdn.microsoft.com/library/a5c16a09-94a2-46ef-87b5-35b815e2f346)
- [プロジェクト モデルのコア コンポーネント](../../extensibility/internals/project-model-core-components.md)
- [プロジェクト ファクトリを使用してプロジェクト インスタンスを作成する](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)
- [方法: サービスを取得する](../../extensibility/how-to-get-a-service.md)
- [プロジェクト タイプの作成](../../extensibility/internals/creating-project-types.md)
