---
title: .NET Framework 4、4.5 に移行された Office プロジェクトに必要な変更
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
ms.openlocfilehash: 82ae3f8a43b65e6ff617192dc38149691d229455
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "66836059"
---
# <a name="required-changes-to-run-office-projects-that-you-migrate-to-the-net-framework-4-or-the-net-framework-45"></a>.NET Framework 4 または .NET Framework 4.5 に移行する Office プロジェクトの実行に必要な変更
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

 エンドユーザーのコンピューターへの展開の前提条件の更新の詳細については、「 [方法: Office ソリューションを実行するための必須コンポーネントをエンドユーザーのコンピューターにインストールする](https://msdn.microsoft.com/74dd2c52-838f-4abf-b2b4-4d7b0c2a0a98)」を参照してください。

## <a name="reinstall-solutions-on-end-user-computers"></a>エンドユーザーのコンピューターにソリューションを再インストールする
 ClickOnce を使用して .NET Framework 3.5 を対象とする Office ソリューションを配置してから、プロジェクトの対象を [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降に変更した場合、エンド ユーザーはソリューションをアンインストールし、再発行後のソリューションを再インストールする必要があります。 ターゲットソリューションを再発行し、エンドユーザーのコンピューターでソリューションが更新された場合、エンドユーザーは更新された <xref:System.Runtime.InteropServices.COMException> ソリューションを実行すると、を受け取ります。

## <a name="see-also"></a>関連項目
- [Office ソリューションを .NET Framework 4 以降に移行する](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)
