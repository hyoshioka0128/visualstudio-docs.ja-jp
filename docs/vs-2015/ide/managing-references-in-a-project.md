---
title: プロジェクト内の参照の管理 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.ProjectPropertiesReferencePaths
- cs.ProjectPropertiesReferencePaths
helpviewer_keywords:
- Visual C# projects, references
- referencing objects, project references
- external component references
- referencing namespaces
- Visual Basic projects, references
- referencing components, external components
- Web references, types of project references
- namespaces [Visual Studio], referencing
- COM components, referencing
- objects [Visual Studio], referencing
ms.assetid: 05d1c51b-44f3-4973-8a11-6c919b08ad62
caps.latest.revision: 55
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a1f2f3c26d89616f083c218c6b11610fe5e329a9
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72651313"
---
# <a name="managing-references-in-a-project"></a>プロジェクト内の参照の管理
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

外部コンポーネントまたは接続しているサービスを使用するためにコードを記述する前に、あらかじめプロジェクトにそのコンポーネントへの参照を追加しておく必要があります。 参照は、本質的には、Visual Studio がコンポーネントまたはサービスを検索するために必要な情報を含むプロジェクト ファイル内のエントリです。

 参照を追加するには、ソリューション エクスプローラーで参照ノードを右クリックして **[参照の追加]** を選択します。 詳細については、「 [方法: 参照マネージャーを使用して参照を追加または削除する](../ide/how-to-add-or-remove-references-by-using-the-reference-manager.md)」を参照してください。

 ![Visual C&#43;&#43; での参照の追加](../ide/media/vs2015-cpp-add-reference.png "|::ref1::|")

 参照は、次の種類のコンポーネント/サービスに対して行うことができます。

- Windows ストア アプリケーションの参照

- .NET Framework クラス ライブラリまたはアセンブリ

- COM コンポーネント

- 同じソリューション内のプロジェクトにあるその他のアセンブリまたはクラス ライブラリ

- XML Web サービス

## <a name="windows-store-app-references"></a>Windows ストア アプリケーションの参照

### <a name="project-references"></a>プロジェクト参照
 Windows の 10 を対象とするユニバーサル Windows プラットフォーム (UWP: Universal Windows Platform) プロジェクトでは、ソリューション内の他の UWP プロジェクトへの参照、または [!INCLUDE[win81](../includes/win81-md.md)] を対象とする Windows ストア プロジェクトまたはバイナリ (ただし、それらのプロジェクトが、Windows 10 で非推奨とされた API を使用していない場合) への参照を作成できます。 詳細については、「 [Windows Runtime 8 から UWP への移行](https://msdn.microsoft.com/library/windows/apps/dn954974.aspx)」を参照してください。

 [!INCLUDE[win81](../includes/win81-md.md)] プロジェクトの Windows 10 への再ターゲットを選択した場合は、「[Visual Studio プロジェクトの移植、移行、およびアップグレード](../porting/porting-migrating-and-upgrading-visual-studio-projects.md)」を参照してください。

### <a name="extension-sdk-references"></a>拡張 SDK の参照
 ユニバーサル Windows プラットフォーム (UWP) を対象とする Visual Basic、C#、C++、JavaScript の各 Windows ストア プロジェクトは、[!INCLUDE[win81](../includes/win81-md.md)] を対象とする拡張 SDK を参照できます (ただし、Windows 10 で非推奨とされた API をそれらの拡張 SDK が使用していない場合のみ)。 UWP を対象としている Windows ストア プロジェクトから拡張 SDK を参照できるかどうかを確認するには、その拡張 SDK の販売元のサイトを調べてください。

 アプリで参照している拡張 SDK がサポートされていないことがわかった場合、次の手順を実行する必要があります。

1. エラーの原因となっているプロジェクトの名前を確認します。 プロジェクトのターゲット プラットフォームはプロジェクト名の横にあるかっこ内に表示されます。 たとえば、**MyProjectName (Windows 8.1)** は、プロジェクト **MyProjectName** がプラットフォーム バージョン [!INCLUDE[win81](../includes/win81-md.md)] を対象としていることを意味します。

2. サポートされていない拡張 SDK の販売元のサイトにアクセスして、プロジェクトのターゲット プラットフォームのバージョンと互換性のある依存関係を持つ拡張 SDK のバージョンをインストールします。

    > [!NOTE]
    > ある拡張 SDK が他の拡張 SDK に依存しているかどうかを調べる 1 つの方法は、Visual Studio を再起動し、新しい C# Windows ストア プロジェクトを作成することです。そのプロジェクトを右クリックし、 **[参照の追加]** をクリックして、 **[Windows]** タブに移動します。次に **[Extensions] (拡張機能)** サブタブで拡張 SDK を選択し、 **[参照マネージャー]** の右ペインを確認します。 依存関係がある場合は、そのウィンドウに表示されます。

    > [!IMPORTANT]
    > プロジェクトが Windows 10 を対象としており、前の手順でインストールした拡張 SDK が Microsoft Visual C++ ランタイム パッケージに依存している場合は、Windows 10 と互換性のある Microsoft Visual C++ ランタイム パッケージのバージョンは v14.0 になります。このバージョンは Visual Studio 2015 と共にインストールされます。

3. 前の手順インストールした拡張 SDK が他の拡張 SDK に依存している場合、その依存関係に関連する販売元のサイトにアクセスして、プロジェクトの対象であるプラットフォームのバージョンと互換性のある依存先バージョンをインストールします。

4. Visual Studio を再起動し、アプリを開きます。

5. エラーの原因となったプロジェクト内の **[参照]** ノードを右クリックして **[参照の追加]** を選択します。

6. **[Windows]** タブをクリックし、 **[Extensions] (拡張機能)** サブタブをクリックしてから、古い拡張 SDK に対応するチェック ボックスをオフにし、新しい拡張 SDK に対応するチェック ボックスをオンにします。 **[OK]** をクリックします。

## <a name="adding-a-reference-at-design-time"></a>デザイン時の参照の追加
 プロジェクトでアセンブリを参照すると、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] は次の場所でアセンブリを検索します。

- 現在のプロジェクト ディレクトリ。 ここにあるアセンブリは、 **[参照]** タブに表示されます。

- 同じソリューション内のその他のプロジェクト ディレクトリ。 ここにあるアセンブリは、 **[プロジェクト]** タブに表示されます。

> [!NOTE]
> すべてのプロジェクトには、mscorlib への暗黙的な参照が含まれます。 Visual Basic プロジェクトには、 `Microsoft.VisualBasic`への暗黙的な参照が含まれます。
>
> Visual Studio 内のすべてのプロジェクトでは、 `System.Core`が参照のリストから削除された場合でも、すべてのプロジェクトに `System.Core` への暗黙的な参照が含まれます。

## <a name="references-to-shared-components-at-run-time"></a>実行時の共有コンポーネントへの参照
 実行時には、コンポーネントがプロジェクトの出力パスまたは GAC ( [Global Assembly Cache](https://msdn.microsoft.com/library/cf5eacd0-d3ec-4879-b6da-5fd5e4372202) ) のどちらかにある必要があります。 どちらの場所にも存在しないオブジェクトへの参照がプロジェクトに含まれている場合は、プロジェクトをビルドするときに、その参照をプロジェクトの出力パスにコピーする必要があります。 <xref:Microsoft.VisualStudio.VCProjectEngine.VCProjectReference.CopyLocal%2A> プロパティは、コピーを作成する必要があるかどうかを示します。 値が **True**の場合は、プロジェクトをビルドするときに参照がプロジェクト ディレクトリにコピーされます。 値が **False**の場合は、参照はコピーされません。

 GAC に登録されているカスタム コンポーネントへの参照を含むアプリケーションを配置した場合、 <xref:Microsoft.VisualStudio.VCProjectEngine.VCProjectReference.CopyLocal%2A> の設定に関係なく、そのコンポーネントはアプリケーションと共に配置されません。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]の旧バージョンでは、参照に <xref:Microsoft.VisualStudio.VCProjectEngine.VCProjectReference.CopyLocal%2A> プロパティを設定して、アセンブリを確実に配置することができました。 現バージョンでは、アセンブリを \Bin フォルダーに手動で追加する必要があります。 これにより、すべてのカスタム コードを監視下に置いて、見覚えのないカスタム コードを公開するリスクを軽減します。

 アセンブリまたはコンポーネントがグローバル アセンブリ キャッシュまたはフレームワーク コンポーネントである場合、既定では、 <xref:Microsoft.VisualStudio.VCProjectEngine.VCProjectReference.CopyLocal%2A> プロパティは **False** に設定されます。 それ以外の場合、値は **True**に設定されます。 プロジェクト間参照は、常に **True**に設定されます。

## <a name="referencing-a-project-or-assembly-that-targets-a-different-version-of-the-net-framework"></a>異なるバージョンの .NET Framework を対象とするプロジェクトまたはアセンブリへの参照
 異なるバージョンの .NET Framework を対象にしたプロジェクトまたはアセンブリを参照するアプリケーションを作成できます。 たとえば、[!INCLUDE[net_client_v40_long](../includes/net-client-v40-long-md.md)] を対象とするアプリケーションを作成し、そのアプリケーションで [!INCLUDE[dnprdnext](../includes/dnprdnext-md.md)] を対象とするアセンブリを参照できます。 以前のバージョンの [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] を対象とするプロジェクトを作成した場合、そのプロジェクトでは、[!INCLUDE[net_client_v40_long](../includes/net-client-v40-long-md.md)] または .NET Framework Version 4 を対象とするプロジェクトまたはアセンブリを参照することはできません。

 詳細については、「[対象となる特定の .NET Framework のバージョンの指定](../ide/targeting-a-specific-dotnet-framework-version.md)」を参照してください。

## <a name="project-to-project-references"></a>プロジェクト間参照
 プロジェクト間参照とは、アセンブリを格納するプロジェクトへの参照です。これは **[プロジェクト]** タブを使用して作成します。Visual Studio は、プロジェクトへのパスが指定されると、アセンブリを見つけることができます。

 アセンブリを生成するプロジェクトがある場合は、ファイル参照 (下記参照) を使用せず、プロジェクトを参照してください。 プロジェクト間参照の利点は、ビルド システム内のプロジェクト間に依存関係が作成されることです。 参照元のプロジェクトの前回のビルド以降に依存プロジェクトが変更されていると、依存プロジェクトのビルドが行われます。 ファイル参照ではビルド依存関係が作成されないため、依存プロジェクトをビルドせずに参照元のプロジェクトをビルドできます。したがって、参照が古くなる可能性があります。 つまり、プロジェクトから、同じプロジェクトの以前にビルドされたバージョンが参照される場合があります。その結果、bin ディレクトリ内に 1 つの DLL の複数のバージョンが求められる場合がありますが、これを実現するのは不可能です。 この矛盾が生じた場合は、"[警告: プロジェクト 'project' の依存関係 'file' は、参照 'file' を上書きするため、実行ディレクトリにコピーできません](../misc/warning-the-dependency-file-in-project-project-cannot-be-copied.md)" などのメッセージが表示されます。 詳細については、「[壊れた参照のトラブルシューティング](../ide/troubleshooting-broken-references.md)」および「[方法: プロジェクトの依存関係を作成および削除する](../ide/how-to-create-and-remove-project-dependencies.md)」を参照してください。

> [!NOTE]
> あるプロジェクトが対象とする .NET Framework のバージョンが Version 4.5 であり、他のプロジェクトが対象とする .NET Framework が Version 2、3.0、3.5、または 4.0 である場合は、プロジェクト間参照ではなくファイル参照が作成されます。

## <a name="file-references"></a>ファイル参照
 ファイル参照とは、Visual Studio プロジェクトのコンテキスト外にあるアセンブリへの直接参照です。これは、 **[参照マネージャー]** の **[参照]** タブを使用して作成します。 アセンブリまたはコンポーネントだけが手元にあり、それを出力として作成したプロジェクトがない場合は、ファイル参照を使用します。

## <a name="see-also"></a>関連項目
 [壊れた参照のトラブルシューティング](../ide/troubleshooting-broken-references.md)[アセンブリを使用したプログラミング](https://msdn.microsoft.com/library/25918b15-701d-42c7-95fc-c290d08648d6)[方法: 参照マネージャーを使用して参照を追加または削除](../ide/how-to-add-or-remove-references-by-using-the-reference-manager.md)する
