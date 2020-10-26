---
title: Visual Studio SDK リファレンス |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- Visual Studio SDK, reference
- reference, Visual Studio SDK
ms.assetid: a6930db5-a112-4651-8de3-e520df851f82
caps.latest.revision: 32
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3a2450aee436b15dfa7154ce96885456eb15a885
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68870033"
---
# <a name="visual-studio-sdk-reference"></a>Visual Studio SDK のリファレンス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このセクションでは、visual studio の名前空間、関連する名前空間、Visual Studio SDK を使用する開発者にとって関心のあるその他の領域について説明します。

## <a name="in-this-section"></a>このセクションの内容

 [セットアップの構成](https://msdn.microsoft.com/library/faa4ed55-66ce-4792-939f-a5b093f13a2e) Visual Studio 2017 のインスタンスを検出するための構成 API を設定します。

 [フォルダー拡張機能を開く](https://msdn.microsoft.com/library/0897ae3d-6a09-4d26-90c9-7f3d0b8e5c5d) Visual Studio 2017 の開いているフォルダーのワークスペース API。

 <xref:Microsoft.VisualStudio.TextManager.Interop> エディターと言語サービスに使用される従来の相互運用インターフェイス。

 <xref:Microsoft.VisualStudio.Editor> 新しいエディターで使用されるクラス。

 <xref:Microsoft.VisualStudio.Language.Intellisense> IntelliSense 用の新しいエディターで使用されるクラス。

 <xref:Microsoft.VisualStudio.Language.StandardClassification> 新しいエディターで使用されるクラス。

 <xref:Microsoft.VisualStudio.Text> 新しいエディターで使用されるクラス。

 <xref:Microsoft.VisualStudio.Text.Adornments> 修飾のために新しいエディターで使用されるクラス。

 <xref:Microsoft.VisualStudio.Text.Classification> 新しいエディターで分類に使用されるクラス。

 <xref:Microsoft.VisualStudio.Text.Differencing> 新しいエディターで差分に使用されるクラス。

 <xref:Microsoft.VisualStudio.Text.Document> ドキュメント用の新しいエディターで使用されるクラス。

 <xref:Microsoft.VisualStudio.Text.Editor> 新しいエディターで使用されるクラス。

 <xref:Microsoft.VisualStudio.Text.Editor.DragDrop> ドラッグアンドドロップ用の新しいエディターで使用されるクラス。

 <xref:Microsoft.VisualStudio.Text.Editor.OptionsExtensionMethods> 新しいエディターで使用されるクラス。

 <xref:Microsoft.VisualStudio.Text.Formatting> 新しいエディターで書式設定のために使用されるクラス。

 <xref:Microsoft.VisualStudio.Text.IncrementalSearch> インクリメンタル検索のために新しいエディターで使用されるクラス。

 <xref:Microsoft.VisualStudio.Text.Operations> 新しいエディターで使用されるクラス。

 <xref:Microsoft.VisualStudio.Text.Outlining> 新しいエディターでアウトラインに使用されるクラス。

 <xref:Microsoft.VisualStudio.Text.Projection> プロジェクションのために新しいエディターで使用されるクラス。

 <xref:Microsoft.VisualStudio.Text.Tagging> タグ付けのために新しいエディターで使用されるクラス。

 <xref:Microsoft.VisualStudio.Utilities> 新しいエディターで使用されるクラス。

 <xref:Microsoft.VisualStudio.PlatformUI>

 <xref:Microsoft.VisualStudio.Shell.Interop>

 <xref:Microsoft.VisualStudio> Visual Studio の定数とヘルパーのクラス。

 <xref:Microsoft.VisualStudio.CommandBars> Visual Studio のコマンドバーのクラス。

 <xref:Microsoft.VisualStudio.ComponentModelHost> Visual Studio の Managed Extensibility Framework (MEF) に使用されるクラス。

 <xref:Microsoft.VisualStudio.Designer.Interfaces> Visual Studio デザイナーで使用されるインターフェイス。

 <xref:Microsoft.VisualStudio.ManagedInterfaces.ProjectDesigner> Visual Studio プロジェクトデザイナーで使用されるインターフェイス。

 <xref:Microsoft.VisualStudio.ManagedInterfaces.Publish> アプリケーションの発行に使用されるクラス。

 <xref:Microsoft.VisualStudio.OLE.Interop> Visual Studio for OLE コンポーネントで使用される相互運用インターフェイス。

 <xref:Microsoft.VisualStudio.Package> Visual Studio マネージ言語サービスに使用されるクラス。

 <xref:Microsoft.VisualStudio.PlatformUI> Visual Studio シェルで使用されるクラス。

 <xref:Microsoft.VisualStudio.PlatformUI.OleComponentSupport> Microsoft 内部でのみ使用します。

 <xref:Microsoft.VisualStudio.ProjectAggregator> Visual Studio プロジェクトに使用されるクラス。

 <xref:Microsoft.VisualStudio.Settings> Visual Studio シェルで使用されるクラス。

 <xref:Microsoft.VisualStudio.Shell> Visual Studio シェルで使用されるクラス。

 <xref:Microsoft.VisualStudio.Shell.Design> Visual Studio シェルで使用されるクラス。

 <xref:Microsoft.VisualStudio.Shell.Design.Serialization> Visual Studio シェルで使用されるクラス。

 <xref:Microsoft.VisualStudio.Shell.Design.Serialization.CodeDom> Visual Studio シェルで使用されるクラス。

 <xref:Microsoft.VisualStudio.Shell.Flavor> Visual Studio プロジェクトに使用されるクラス。

 <xref:Microsoft.VisualStudio.Shell.Interop> Visual Studio シェルに使用される相互運用インターフェイス。

 <xref:Microsoft.VisualStudio.Shell.Settings> Visual Studio シェルで使用されるクラス。

 <xref:Microsoft.VisualStudio.VSHelp> ヘルプに使用されるクラス。

 <xref:VSLangProj> 言語サービスプロジェクトに使用されるクラス。

 <xref:XamlGeneratedNamespace> Microsoft 内部でのみ使用します。

 <xref:Microsoft.VisualStudio.ManagedInterfaces9> Visual Studio に使用されるインターフェイス。

 <xref:Microsoft.VisualStudio.WCFReference.Interop> Windows Communication Framework に使用されるクラス。

 テストツールで使用される[VisualStudio](/previous-versions/aa993343(v=vs.120))クラス。

 <xref:EnvDTE> Visual Studio オートメーションに使用されます。

 <xref:Extensibility> Visual Studio オートメーションに使用されます。

 <xref:EnvDTE80> Visual Studio オートメーションに使用されます。

 <xref:EnvDTE90> Visual Studio オートメーションに使用されます。

 <xref:EnvDTE90a> Visual Studio オートメーションに使用されます。

 <xref:EnvDTE100> Visual Studio オートメーションに使用されます。

 <xref:Microsoft.VisualStudio.VCCodeModel> プロジェクトの自動化の Visual C++ に使用されます。

 <xref:Microsoft.VisualStudio.VCProject> プロジェクトオートメーションの Visual C++ に使用されるクラス。

 <xref:Microsoft.VisualStudio.VCProjectEngine> プロジェクトの自動化の Visual C++ に使用されます。

 <xref:Microsoft.VisualStudio.VsWizard> Visual Studio ウィザードで使用されます。

 <xref:VSLangProj> C# および Visual Basic プロジェクトオートメーションに使用されます。

 <xref:VSLangProj2> C# および Visual Basic プロジェクトオートメーションに使用されます。

 <xref:VSLangProj80> C# および Visual Basic プロジェクトオートメーションに使用されます。

 <xref:VslangProj90> C# および Visual Basic プロジェクトオートメーションに使用されます。

 <xref:VslangProj100> C# および Visual Basic プロジェクトオートメーションに使用されます。

 <xref:VSLangProj110> C# および Visual Basic プロジェクトオートメーションに使用されます。

 <xref:VSLangProj140> C# および Visual Basic プロジェクトオートメーションに使用されます。

 <xref:Microsoft.VisualStudio.Language.CallHierarchy> C# および Visual Basic オートメーションに使用されます。

 <xref:Microsoft.VisualStudio.Language.NavigateTo.Interfaces> C# および Visual Basic オートメーションに使用されます。

 <xref:Microsoft.VisualStudio.Threading> Visual Studio のスレッド処理に使用されます。

 <xref:Microsoft.VisualStudio.ConnectedServices?qualifyHint=False&autoUpgrade=True> Visual Studio 接続済みサービスに使用されます。

 [IntelliSenseHostFlags](../extensibility/intellisensehostflags.md) 列挙は、IntelliSense ホストフラグを指定します。

 [Vsct XML スキーマリファレンス](../extensibility/vsct-xml-schema-reference.md) 各に許可されている子要素と属性を持つ Visual Studio コマンドテーブルスキーマ要素のテーブルを提供します。

 [Guid と定数](../extensibility/guids-and-constants-in-the-visual-studio-sdk.md) SDK 全体で使用される Guid の一覧を示します。

 [マネージコードの COM 定数](../extensibility/com-constants-in-managed-code.md) 環境 SDK 全体で使用されるユーザーインターフェイス要素の識別子の一覧を示します。

 [ソース管理プラグイン](../extensibility/source-control-plug-ins.md) ソース管理プラグイン API に関するトピックへのリンク。

 [コマンドラインスイッチ](../extensibility/command-line-switches-visual-studio-sdk.md) 開発者がコマンドラインからいくつかのタスクを自動化する方法について説明するトピックへのリンクを示します。

 [エラー処理と戻り値](../extensibility/error-handling-and-return-values.md) Vspackage のエラーアーキテクチャについて説明します。これは、他の Windows プログラミングで採用されているものと同じです。

 [オブジェクト](../extensibility/objects.md) 環境で使用されるオブジェクトの一覧を示します。

 [用語集](../extensibility/visual-studio-sdk-glossary.md) Visual Studio SDK のドキュメントを読むときに使用する便利な用語とその定義の一覧を示します。

 <xref:Microsoft.Build.BuildEngine> MSBuild に使用されます。

 <xref:Microsoft.Build.Construction> MSBuild に使用されます。

 <xref:Microsoft.Build.Conversion> MSBuild に使用されます。

 <xref:Microsoft.Build.Debugging> MSBuild に使用されます。

 <xref:Microsoft.Build.Evaluation> MSBuild に使用されます。

 <xref:Microsoft.Build.Exceptions> MSBuild に使用されます。

 <xref:Microsoft.Build.Execution> MSBuild に使用されます。

 <xref:Microsoft.Build.Framework> MSBuild に使用されます。

 <xref:Microsoft.Build.Framework.XamlTypes> MSBuild に使用されます。

 <xref:Microsoft.Build.Logging> MSBuild に使用されます。

 <xref:Microsoft.Build.Tasks> MSBuild に使用されます。

 <xref:Microsoft.Build.Tasks.Deployment.Bootstrapper> MSBuild に使用されます。

 <xref:Microsoft.Build.Tasks.Deployment.ManifestUtilities> MSBuild に使用されます。

 <xref:Microsoft.Build.Tasks.Hosting> MSBuild に使用されます。

 <xref:Microsoft.Build.Tasks.Xaml> MSBuild に使用されます。

 <xref:Microsoft.Build.Utilities> MSBuild に使用されます。

## <a name="related-sections"></a>関連項目
 [Visual STUDIO SDK](../extensibility/visual-studio-sdk.md) Visual Studio と統合する製品の開発に役立つドキュメント、サンプル、コードが含まれています。
