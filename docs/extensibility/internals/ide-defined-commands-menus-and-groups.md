---
title: IDE で定義されたコマンド、メニュー、およびグループ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, environment-defined
- .vsct files, environment-defined constants
- command groups, environment-defined
ms.assetid: 86b3af13-7163-48c6-986b-7beeedbc26cc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6557f49b019a6793698dabe852919ec2e9f28cfd
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707718"
---
# <a name="ide-defined-commands-menus-and-groups"></a>IDE 定義コマンド、メニュー、およびグループ
多くのメニュー、コマンド、およびコマンドグループは、IDE で[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]使用するために既に定義されています。 これらのコマンドは、 を拡張[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]するときにも使用できます。

## <a name="finding-environment-defined-commands"></a>環境定義コマンドの検索
 環境コマンドは、次の 4 つの .vsct ファイルのセットで定義されます。

- を使用します。

- 共有の場所を配置します。

- を使用します。

- を見る

  これらのファイルは*\<、Visual Studio SDK のインストール パス>* \VisualStudioIntegration\Common\Inc.\\にあります。 これらのファイルは、独自のメニュー、グループ、およびコマンドのコンテナーとして VSPackage のコマンド テーブル構成 (.vsct) ファイルで使用できるメニューとグループの定義と GUID を提供します。

## <a name="in-this-section"></a>このセクションの内容
- [Visual Studio メニューの GUID および ID](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)

 Visual Studio のメニュー バーのメニュー、およびメニューに含まれるグループの GUID と ID の値を指定します。

- [Visual Studio ツール バーの GUID および ID](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)

 Visual Studio IDE のツール バー、およびツール バーに含まれるグループの GUID と ID の値を指定します。

- [Visual Studio コマンドの GUID および ID](../../extensibility/internals/guids-and-ids-of-visual-studio-commands.md)

 VISUAL Studio IDE によって定義されたコマンドの GUID と ID の値を提供します。

## <a name="see-also"></a>関連項目
- [Visual Studio Command Table (.Vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [プロジェクト システムを拡張するための IDE 定義コマンド](../../extensibility/internals/ide-defined-commands-for-extending-project-systems.md)
- [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
