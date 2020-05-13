---
title: プロジェクトシステムを拡張するための IDE 定義コマンド |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, project systems
- project systems, environment-defined commands
ms.assetid: 0e33b8e9-16fa-4400-a941-e92d56120e7e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 61c0b2924548f50ad650389e3ad81759be1986a4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707731"
---
# <a name="ide-defined-commands-for-extending-project-systems"></a>プロジェクト システムを拡張するための IDE 定義コマンド
プロジェクトシステムを拡張する場合は、IDE で提供されるコマンドとコマンドグループを[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]使用できます。

 次のセクションでは、プロジェクト システムの拡張に特に役立つコマンド項目を示します。

## <a name="command-menus"></a>コマンド メニュー
 次の表は、プロジェクト エクステンダーを呼び出す高レベルのコマンドを配置するのに役立つコマンド メニューを示しています。

|コマンドメニュー|説明|
|------------------|-----------------|
|IDM_VS_MENU_PROJECT|**プロジェクト**のトップレベルメニュー。|
|IDM_VS_TOOL_PROJWIN|**ソリューション エクスプローラー**のツール バー。|

## <a name="shortcut-menus"></a>ショートカット メニュー
 次の表は、**ソリューション エクスプローラ**で 1 つのノードが選択されている場合、または選択したすべてのノードが同じ種類の場合に、**ソリューション エクスプローラ**で複数の同種の選択が行われた場合に適用されるショートカット メニューを示しています。

|ショートカット メニュー|説明|
|-------------------|-----------------|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_PROJNODE>|プロジェクト ノードが選択されている場合に適用されます。|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_ITEMNODE>|ファイルが選択されている場合に適用されます。|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_FOLDERNODE>|フォルダが選択されている場合に適用されます。|
|IDM_VS_CTXT_WEBREFFOLDER|Web 参照フォルダが選択されている場合に適用されます。|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_REFERENCEROOT>|"参照" という名前の参照ルート ノードが選択されている場合に適用されます。|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_REFERENCE>|参照ノードが選択されている場合に適用されます。アセンブリ、COM、およびプロジェクト参照のみが含まれます。 Web 参照は含まれません。|

 次の表は、**ソリューション エクスプローラー**で選択した項目が複数の階層にまたがる場合に適用されるショートカット メニューを示しています。

|ショートカット メニュー|説明|
|-------------------|-----------------|
|IDM_VS_CTXT_XPROJ_SLNPROJ|現在の選択項目にソリューション ノードとルート プロジェクト ノードが含まれている場合に適用されます。|
|IDM_VS_CTXT_XPROJ_SLNITEM|現在の選択項目にソリューション ノードとプロジェクト項目が含まれている場合に適用されます。|
|IDM_VS_CTXT_XPROJ_MULTIPROJ|現在の選択が複数のルート プロジェクト ノードのみで構成されている場合に適用されます。|
|IDM_VS_CTXT_XPROJ_PROJITEM|現在の選択項目に、ルート プロジェクト ノードとプロジェクト項目が混在している場合に適用されます。 さらに、選択にはソリューション ノードを含めることができます。|
|IDM_VS_CTXT_XPROJ_MULTIITEM|現在の選択項目に、ソリューション内の複数のプロジェクトのプロジェクト項目が含まれている場合、または同じプロジェクトで異なる種類の項目が選択されている場合に適用されます。|

## <a name="command-groups"></a>コマンド グループ
 次の表は、プロジェクトを拡張するときに使用できるコマンド グループと、ショートカット メニューからアクセスできるコマンド<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_PROJNODE>グループを示しています。

|コマンド グループ|説明|
|-------------------|-----------------|
|IDG_VS_CTXT_PROJECT_BUILD|プロジェクトをビルド、再構築、および配置するためのコマンド。|
|IDG_VS_CTXT_COMPILELINK|プロジェクトをコンパイルおよびリンクするためのコマンド。|
|IDG_VS_CTXT_PROJECT_CONFIG|プロジェクトの構成とビルドの順序を設定するコマンド。|
|IDG_VS_CTXT_PROJECT_ADD|プロジェクトに項目を追加するコマンド。|
|IDG_VS_CTXT_PROJECT_START|F5 キーに関連付けられたスタートアップ プロジェクトを設定するコマンド。|
|IDG_VS_CTXT_PROJECT_SAVE|プロジェクト項目を保存するためのコマンド。|
|IDG_VS_CTXT_PROJECT_DEBUG|デバッグ用のコマンド。|
|IDG_VS_CTXT_PROJECT_SCC|ソース管理のコマンド。|
|IDG_VS_CTXT_PROJECT_TRANSFER|切り取り、コピー、貼り付け操作のコマンド。|
|IDG_VS_CTXT_PROJECT_PROPERTIES|**[プロジェクトのプロパティ]** ダイアログ ボックスへのアクセスを提供するコマンド。|

## <a name="see-also"></a>関連項目

- [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [再利用可能なボタンのグループの作成](../../extensibility/creating-reusable-groups-of-buttons.md)
