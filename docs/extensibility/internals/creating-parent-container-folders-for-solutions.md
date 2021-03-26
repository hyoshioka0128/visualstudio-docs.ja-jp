---
title: ソリューションの親コンテナーフォルダーを作成する |Microsoft Docs
description: ソース管理プラグイン API バージョン1.2 を使用して、ソリューション内のすべての web プロジェクトに対して単一のルートソース管理ターゲットを指定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions, creating parent containers
- source control plug-ins, creating parent containers
ms.assetid: 961e68ed-2603-4479-a306-330eda2b2efa
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2c9b3b5c01e9c1ad5de9fbb0a44398d3f7963295
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056841"
---
# <a name="create-parent-container-folders-for-solutions"></a>ソリューションの親コンテナーフォルダーを作成する
ソース管理プラグイン API バージョン1.2 では、ユーザーは、ソリューション内のすべての web プロジェクトに対して単一のルートソース管理のターゲットを指定できます。 この1つのルートは、スーパー統合ルート (.SUR) と呼ばれます。

 ソース管理プラグイン API バージョン1.1 では、ユーザーがマルチプロジェクトソリューションをソース管理に追加した場合、ユーザーは各 web プロジェクトに対して1つのソース管理の宛先を指定するように求められました。

## <a name="new-capability-flags"></a>新しい機能フラグ
 `SCC_CAP_CREATESUBPROJECT`

 `SCC_CAP_GETPARENTPROJECT`

## <a name="new-functions"></a>新しい関数
- [SccCreateSubProject](../../extensibility/scccreatesubproject-function.md)

- [SccGetParentProjectPath](../../extensibility/sccgetparentprojectpath-function.md)

 IDE では、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ソース管理にソリューションを追加するときに、ほとんどの場合、.sur フォルダーが作成されます。 具体的には、次のような場合に実行されます。

- プロジェクトはファイル共有 web プロジェクトです。

- プロジェクトとソリューションファイルには異なるドライブがあります。

- プロジェクトとソリューションファイルには異なる共有があります。

- プロジェクトは、(ソース管理ソリューションで) 個別に追加されました。

で [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] は、.sur フォルダーの名前は、拡張子のないソリューション名と同じにすることをお勧めします。 次の表は、2つのバージョンの動作をまとめたものです。

|特徴量|ソース管理プラグイン API バージョン1.1|ソース管理プラグイン API バージョン1.2|
|-------------| - | - |
|SCC へのソリューションの追加|SccInitialize ()<br /><br /> SccGetProjPath ()<br /><br /> SccGetProjPath ()<br /><br /> SccOpenProject ()|SccInitialize ()<br /><br /> SccGetProjPath ()<br /><br /> SccCreateSubProject()<br /><br /> SccCreateSubProject()<br /><br /> SccOpenProject ()|
|ソース管理ソリューションへのプロジェクトの追加|SccGetProjPath ()<br /><br /> OpenProject ()|SccGetParentProjectPath()<br /><br /> SccOpenProject ()<br /><br />  **注:**  Visual Studio では、ソリューションが .SUR の直接の子であることを前提としています。|

## <a name="examples"></a>例
 次の表は、2つの例を示しています。 どちらの場合も、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]  *user_choice* が変換先として指定されるまで、ユーザーにはソース管理下のソリューションの宛先の場所を入力するように求められます。 User_choice が指定されている場合、ソリューションと2つのプロジェクトは、ユーザーにソース管理の変換先の入力を求めずに追加されます。

|ソリューションに含まれるもの|ディスクの場所|データベースの既定の構造|
|-----------------------|-----------------------|--------------------------------|
|*sln1*<br /><br /> Web1<br /><br /> Web2|*C:\ ソリューション \ n1*<br /><br /> *C:\Inetpub\wwwroot\Web1*<br /><br /> \\\ \ _ wwwroot $ \ web2|$/<user_choice>/sln1<br /><br /> $/<user_choice>/C/Web1<br /><br /> $/<user_choice>/web2|
|*sln1*<br /><br /> Web1<br /><br /> Win1|*C:\ ソリューション \ n1*<br /><br /> *D:\Inetpub\wwwroot\Web1*<br /><br /> *C:\solutions\sln1\Win1*|$/<user_choice>/sln1<br /><br /> $/<user_choice>/D/web1<br /><br /> $/<user_choice>/sln1/win1|

 .SUR フォルダーとサブフォルダーは、操作が取り消されたか、エラーが原因で失敗したかに関係なく作成されます。 これらは、キャンセルまたはエラー条件で自動的に削除されることはありません。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ソース管理プラグインによってとの機能フラグが返されない場合、バージョン1.1 の動作が既定値に `SCC_CAP_CREATESUBPROJECT` `SCC_CAP_GETPARENTPROJECT` なります。 さらに、のユーザー [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] は、次のキーの値を *dword: 00000001* に設定することにより、バージョン1.1 の動作に戻すことができます。

 **[HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl] DoNotCreateSolutionRootFolderInSourceControl**  = *dword: 00000001*

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理プラグイン API バージョン1.2 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
