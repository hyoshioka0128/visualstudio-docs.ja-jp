---
title: プロジェクト ファクトリを使用したプロジェクト インスタンスの作成 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project factories
- projects [Visual Studio SDK], project factories
ms.assetid: 94c90012-8669-459c-af8e-307ac242c8c4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 31ba5dd11af18f8a723b2271544eff2bd292e2e8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709058"
---
# <a name="create-project-instances-by-using-project-factories"></a>プロジェクト ファクトリを使用してプロジェクト インスタンスを作成する
プロジェクトの種類[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]では *、プロジェクト ファクトリ*を使用してプロジェクト オブジェクトのインスタンスを作成します。 プロジェクト ファクトリは、コクリー可能な COM オブジェクトの標準クラス ファクトリに似ています。 ただし、プロジェクト オブジェクトはコクリー可能ではありません。プロジェクト ファクトリを使用して作成することしかできません。

 ユーザー[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]が既存のプロジェクトを読み込むか、新しいプロジェクトを作成するときに、VSPackage に実装されている[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]プロジェクト ファクトリが IDE によって呼び出されます。 新しいプロジェクト オブジェクトは、**ソリューション エクスプローラ**を読み込むのに十分な情報を IDE に提供します。 新しいプロジェクトオブジェクトには、IDE によって開始されたすべての関連 UI アクションをサポートするために必要なインタフェースも用意されています。

 プロジェクトの<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>クラスにインターフェイスを実装できます。 通常、それは独自のモジュールに存在します。

 所有者による集計をサポートするプロジェクトは、プロジェクト ファイルに所有者キーを保持する必要があります。 オーナー<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>キーを持つプロジェクトでメソッドが呼び出されると、所有プロジェクトは、その所有者キーをプロジェクト ファクトリ GUID`CreateProject`に変換し、プロジェクト ファクトリのメソッドを呼び出して実際の作成を行います。

## <a name="create-an-owned-project"></a>所有プロジェクトの作成
 所有者は、次の 2 つのフェーズで所有プロジェクトを作成します。

1. メソッドを呼<xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.PreCreateForOwner%2A>び出します。 これにより、所有プロジェクトは、入力制御に基づいて集約されたプロジェクトオブジェクトを作成する機会を`IUnknown`与えます。 所有プロジェクトは、内部`IUnknown`オブジェクトと集約オブジェクトを所有者プロジェクトに返します。 これにより、所有するプロジェクトに内部を格納する機会`IUnknown`が与えます。

2. メソッドを呼<xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.InitializeForOwner%2A>び出します。 所有プロジェクトは、このメソッドが呼び出される代わりに呼び出`IVsProjectFactory::CreateProject`されたときに、所有されていないプロジェクトの場合と同様に、すべてのインスタンス化を行います。 入力`VSOWNEDPROJECTOBJECT`列挙体は、通常、集計済み所有プロジェクトです。 所有プロジェクトは、この変数を使用して、プロジェクト オブジェクトが既に作成されているか (cookie が NULL と等しくない) または作成する必要があるかどうかを判断できます (cookie は NULL に等しい)。

   プロジェクトの種類は、コクリー可能な COM オブジェクトの CLSID と同様に、一意のプロジェクト GUID によって識別されます。 通常、1 つのプロジェクト ファクトリは 1 つのプロジェクトの種類のインスタンスの作成を処理しますが、1 つのプロジェクト ファクトリが複数のプロジェクトの種類の GUID を処理できます。

   プロジェクトの種類は、特定のファイル名拡張子に関連付けられます。 ユーザーが既存のプロジェクト ファイルを開こうとしたり、テンプレートを複製して新しいプロジェクトを作成しようとすると、IDE はファイルの拡張子を使用して対応するプロジェクト GUID を決定します。

   IDE は、新しいプロジェクトを作成するか、特定の種類の既存のプロジェクトを開く必要があるかを決定するとすぐに、システム レジストリの **[HKEY_LOCAL_MACHINE\ソフトウェア\Microsoft\VisualStudio\8.0\Projects]** の下の情報を使用して、必要なプロジェクト ファクトリを実装する VSPackage を見つけます。 IDE はこの VS パッケージを読み込みます。 メソッドでは<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>、VSPackage メソッドを呼び出すことによって、IDE にプロジェクト<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectTypes.RegisterProjectType%2A>ファクトリを登録する必要があります。

   インターフェイスの`IVsProjectFactory`主な方法は<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>、 の 2 つのシナリオを処理する必要があります: 既存のプロジェクトを開くと新しいプロジェクトを作成します。 ほとんどのプロジェクトは、プロジェクト ファイルにプロジェクトの状態を格納します。 通常、`CreateProject`新しいプロジェクトは、メソッドに渡されたテンプレート ファイルのコピーを作成し、そのコピーを開くことによって作成されます。 既存のプロジェクトは、`CreateProject`メソッドに渡されたプロジェクト ファイルを直接開くことによってインスタンス化されます。 メソッド`CreateProject`は、必要に応じて、ユーザーに追加の UI 機能を表示できます。

   プロジェクトはファイルを使用せず、代わりに、データベースや Web サーバーなどのファイル システム以外のストレージ 機構にプロジェクトの状態を格納することもできます。 この場合、`CreateProject`メソッドに渡されるファイル名パラメーターは、実際にはファイル システム パスではなく、プロジェクト データを識別するための一意の文字列 (URL) です。 適切な構築シーケンスを実行するために`CreateProject`渡されるテンプレートファイルをコピーする必要はありません。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectTypes>
- [チェックリスト: 新しいプロジェクトの種類を作成する](../../extensibility/internals/checklist-creating-new-project-types.md)
