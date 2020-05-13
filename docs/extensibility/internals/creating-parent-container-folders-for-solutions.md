---
title: ソリューションの親コンテナフォルダを作成する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions, creating parent containers
- source control plug-ins, creating parent containers
ms.assetid: 961e68ed-2603-4479-a306-330eda2b2efa
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3e5481e20a12fc05ccba97eef55173e5ce9b30d6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709097"
---
# <a name="create-parent-container-folders-for-solutions"></a>ソリューションの親コンテナフォルダを作成する
ソース管理プラグイン API バージョン 1.2 では、ユーザーはソリューション内のすべての Web プロジェクトに対して単一のルート ソース コントロールの宛先を指定できます。 この単一のルートは、スーパー統合ルート(SUR)と呼ばれます。

 ソース管理プラグイン API バージョン 1.1 では、ユーザーがソース管理にマルチプロジェクト ソリューションを追加した場合、ユーザーは、各 Web プロジェクトに対して 1 つのソース管理の宛先を指定するように求められます。

## <a name="new-capability-flags"></a>新しい機能フラグ
 `SCC_CAP_CREATESUBPROJECT`

 `SCC_CAP_GETPARENTPROJECT`

## <a name="new-functions"></a>新しい関数
- [SccCreateSubProject](../../extensibility/scccreatesubproject-function.md)

- [SccGetParentProjectPath](../../extensibility/sccgetparentprojectpath-function.md)

 IDE[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]は、ソース管理にソリューションを追加するときに、ほとんど常に SUR フォルダを作成します。 具体的には、次の場合に行われます。

- プロジェクトはファイル共有 Web プロジェクトです。

- プロジェクトとソリューション ファイルには、異なるドライブがあります。

- プロジェクトとソリューション ファイルに対しては、異なる共有があります。

- プロジェクトは個別に (ソース管理されたソリューションで) 追加されました。

では[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]、SUR フォルダの名前は、拡張子を除いたソリューション名と同じであることが推奨されます。 次の表は、2 つのバージョンの動作をまとめたものです。

|機能|ソース管理プラグイン API バージョン 1.1|ソース管理プラグイン API バージョン 1.2|
|-------------| - | - |
|SCC にソリューションを追加する|を実行します。<br /><br /> パスパス()<br /><br /> パスパス()<br /><br /> プロジェクトを開く()|を実行します。<br /><br /> パスパス()<br /><br /> サブプロジェクト()<br /><br /> サブプロジェクト()<br /><br /> プロジェクトを開く()|
|ソース管理ソリューションへのプロジェクトの追加|パスパス()<br /><br /> プロジェクトを開く()|プロジェクトパス()<br /><br /> プロジェクトを開く()<br /><br />  **注:** ソリューションは SUR の直接の子であると想定します。|

## <a name="examples"></a>使用例
 次の表は、2 つの例を示しています。 どちらの場合も[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]*、user_choice*が宛先として指定されるまで、ソース管理下にあるソリューションの宛先の場所を指定するようユーザーに求められます。 user_choiceを指定すると、ソリューションと 2 つのプロジェクトが追加され、ユーザーにソース コントロールの出力先を確認するメッセージが表示されません。

|ソリューションには次の項目が含まれています|ディスク上の場所|データベースの既定の構造|
|-----------------------|-----------------------|--------------------------------|
|*sln1.sln*<br /><br /> Web1<br /><br /> ウェブ2|*C:\ソリューション\sln1*<br /><br /> *C:\イネットパブ\wwwroot\ウェブ1*<br /><br /> \\\サーバー\wwwroot$\Web2|$/<user_choice>/sln1<br /><br /> $/<user_choice>/C/Web1<br /><br /> $/<user_choice>/Web2|
|*sln1.sln*<br /><br /> Web1<br /><br /> ウィン1|*C:\ソリューション\sln1*<br /><br /> *D:\イネットパブ\wwwroot\ウェブ1*<br /><br /> *C:\ソリューション\sln1\Win1*|$/<user_choice>/sln1<br /><br /> user_choice>/D/ウェブ1user_choice $/<<br /><br /> $/<user_choice>/sln1/win1|

 エラーが発生したために操作がキャンセルされたか失敗するかに関係なく、SUR フォルダとサブフォルダが作成されます。 キャンセルまたはエラーの条件では、自動的に削除されません。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ソース管理プラグインが機能フラグと`SCC_CAP_CREATESUBPROJECT``SCC_CAP_GETPARENTPROJECT`機能フラグを返さない場合は、デフォルトでバージョン 1.1 の動作になります。 さらに、ユーザーは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]次のキーの値を*dword:0000001*に設定することで、バージョン 1.1 の動作に戻すことができます。

 **[HKEY_CURRENT_USER\ソフトウェア\マイクロソフト\VisualStudio\8.0\ソースコントロール]ド・ソース・ソリューション・ルートフォルダーインソースコントロール** = *・ドワード:00000001*

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API バージョン 1.2 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
