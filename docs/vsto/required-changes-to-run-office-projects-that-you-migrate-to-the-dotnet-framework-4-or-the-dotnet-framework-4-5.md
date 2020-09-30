---
title: .NET 4.5 に移行された Office プロジェクトに必要な変更
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office projects [Office development in Visual Studio], migrating to .NET Framework 4
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 40db3cd629f2c3a2ced37a781dea3244a3f19957
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91584465"
---
# <a name="changes-required-for-office-projects-migrated-to-net-45"></a>.NET 4.5 に移行された Office プロジェクトに必要な変更

  Office プロジェクトのターゲットフレームワークを以前のバージョンの .NET Framework から以降に変更する場合は、 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 次のタスクを実行して、ソリューションを開発用コンピューターとエンドユーザーのコンピューターで確実に実行できるようにする必要があります。

- Visual Studio 2008 からアップグレードした場合は、プロジェクトから <xref:System.Security.SecurityTransparentAttribute> を削除します。

- Visual Studio で **クリーン** コマンドを実行して、開発用コンピューターでプロジェクトを実行またはデバッグできるようにします。

- プロジェクトの .NET Framework の必須コンポーネントを更新します。

- ターゲット フレームワークを変更する前に ClickOnce を使用してソリューションを配置した場合は、さらにエンド ユーザーがソリューションを再インストールする必要があります。

  これらの各タスクの詳細については、以下の対応するセクションを参照してください。

## <a name="remove-the-securitytransparent-attribute-from-projects-that-you-upgrade-from-visual-studio-2008"></a>Visual Studio 2008 からアップグレードするプロジェクトから SecurityTransparent 属性を削除します。
 Visual Studio 2008 から Office プロジェクトをアップグレードした後で、プロジェクトのターゲット フレームワークが [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降に変更された場合は、プロジェクトから <xref:System.Security.SecurityTransparentAttribute> を削除する必要があります。 この属性は Visual Studio によって自動的に削除されません。 この属性を削除しないと、プロジェクトをコンパイルしたときにエラー メッセージが表示されます。

 Visual Studio でアップグレードされたプロジェクトのターゲットフレームワークをまたはに変更するための条件の詳細について [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] は [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] 、「 [Office ソリューションのアップグレードと移行](../vsto/upgrading-and-migrating-office-solutions.md)」を参照してください。

#### <a name="to-remove-the-securitytransparentattribute"></a>SecurityTransparentAttribute を削除するには

1. Visual Studio でプロジェクトを開き、 **ソリューション エクスプローラー**を開きます。

2. **[プロパティ]** ノード (C# の場合) または **[マイ プロジェクト]** ノード (Visual Basic の場合) の下で、AssemblyInfo コード ファイルをダブルクリックしてコード エディターで開きます。

    > [!NOTE]
    > Visual Basic プロジェクトで AssemblyInfo コード ファイルを表示するには、 **ソリューション エクスプローラー** の **[すべてのファイルの表示]** ボタンをクリックする必要があります。

3. <xref:System.Security.SecurityTransparentAttribute> を探し、ファイルから削除するか、コメント アウトします。

    ```vb
    <Assembly: SecurityTransparent()>
    ```

    ```csharp
    [assembly: SecurityTransparent()]
    ```

## <a name="perform-the-clean-command-to-debug-or-run-a-project-on-the-development-computer"></a>開発用コンピューターでプロジェクトをデバッグまたは実行するには、clean コマンドを実行します。
 プロジェクトのターゲットフレームワークが以降に変更される前に Office プロジェクトがビルドされている場合は、 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ターゲットフレームワークを変更した後で、 **クリーン** コマンドを実行し、プロジェクトをリビルドする必要があります。 [ **クリーン** ] コマンドを実行しない場合は、 <xref:System.Runtime.InteropServices.COMException> ターゲットプロジェクトをデバッグまたは実行しようとすると、が表示されます。

 **Clean**コマンドの詳細については、「 [Office ソリューションのビルド](../vsto/building-office-solutions.md)」を参照してください。

## <a name="update-the-prerequisites-for-deployment"></a>展開の前提条件を更新する
 Office プロジェクトのターゲットを以降に変更する場合は、 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] [ **必須コンポーネント** ] ダイアログボックスで、対応する .NET Framework の前提条件も更新する必要があります。 そうしない場合は、ClickOnce 配置または InstallShield Limited Edition プロジェクトが以前のバージョンの .NET Framework をチェックし、インストールします。

 エンドユーザーのコンピューターへの展開の前提条件の更新の詳細については、「 [方法: Office ソリューションを実行するための必須コンポーネントをエンドユーザーのコンピューターにインストールする](/previous-versions/bb608608(v=vs.110))」を参照してください。

## <a name="reinstall-solutions-on-end-user-computers"></a>エンドユーザーのコンピューターにソリューションを再インストールする
 ClickOnce を使用して .NET Framework 3.5 を対象とする Office ソリューションを配置してから、プロジェクトの対象を [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降に変更した場合、エンド ユーザーはソリューションをアンインストールし、再発行後のソリューションを再インストールする必要があります。 ターゲットソリューションを再発行し、エンドユーザーのコンピューターでソリューションが更新された場合、エンドユーザーは更新された <xref:System.Runtime.InteropServices.COMException> ソリューションを実行すると、を受け取ります。

## <a name="see-also"></a>関連項目
- [Office ソリューションを .NET Framework 4 以降に移行する](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)