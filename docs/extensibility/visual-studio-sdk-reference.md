---
title: ビジュアルスタジオ SDK リファレンス |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio SDK, reference
- reference, Visual Studio SDK
ms.assetid: a6930db5-a112-4651-8de3-e520df851f82
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 93c1f6eaa2019e602efc760003c960a9b62f9ebd
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698096"
---
# <a name="visual-studio-sdk-reference"></a>ビジュアル スタジオ SDK リファレンス

このセクションでは、Visual Studio SDK を使用する開発者向けの Visual Studio 名前空間、関連する名前空間、およびその他の関心領域について説明します。

## <a name="in-this-section"></a>このセクションの内容

- <xref:Microsoft.VisualStudio.TextManager.Interop>エディターおよび言語サービスで使用される従来の相互運用機能インターフェイス。

- <xref:Microsoft.VisualStudio.Editor>新しいエディターで使用されるクラス。

- <xref:Microsoft.VisualStudio.Language.Intellisense>IntelliSense の新しいエディターで使用されるクラス。

- <xref:Microsoft.VisualStudio.Language.StandardClassification>新しいエディターで使用されるクラス。

- <xref:Microsoft.VisualStudio.Text>新しいエディターで使用されるクラス。

- <xref:Microsoft.VisualStudio.Text.Adornments>新しいエディターで表示要素として使用されるクラス。

- <xref:Microsoft.VisualStudio.Text.Classification>新しいエディタで分類に使用されるクラス。

- <xref:Microsoft.VisualStudio.Text.Differencing>差分処理のために新しいエディターで使用されるクラス。

- <xref:Microsoft.VisualStudio.Text.Document>ドキュメントの新しいエディターで使用されるクラス。

- <xref:Microsoft.VisualStudio.Text.Editor>新しいエディターで使用されるクラス。

- <xref:Microsoft.VisualStudio.Text.Editor.DragDrop>ドラッグ アンド ドロップに使用する新しいエディターで使用されるクラス。

- <xref:Microsoft.VisualStudio.Text.Editor.OptionsExtensionMethods>新しいエディターで使用されるクラス。

- <xref:Microsoft.VisualStudio.Text.Formatting>新しいエディターで書式設定に使用されるクラス。

- <xref:Microsoft.VisualStudio.Text.IncrementalSearch>インクリメンタル検索用に新しいエディタで使用されるクラス。

- <xref:Microsoft.VisualStudio.Text.Operations>新しいエディターで使用されるクラス。

- <xref:Microsoft.VisualStudio.Text.Outlining>新しいエディタでアウトライン表示に使用されるクラス。

- <xref:Microsoft.VisualStudio.Text.Projection>新しいエディタでプロジェクションに使用するクラス。

- <xref:Microsoft.VisualStudio.Text.Tagging>新しいエディタでタグ付けに使用するクラス。

- <xref:Microsoft.VisualStudio.Utilities>新しいエディターで使用されるクラス。

- <xref:Microsoft.VisualStudio.PlatformUI>

- <xref:Microsoft.VisualStudio.Shell.Interop>

- <xref:Microsoft.VisualStudio>Visual Studio の定数とヘルパーのクラス。

- <xref:Microsoft.VisualStudio.CommandBars>Visual Studio コマンド バーのクラス。

- <xref:Microsoft.VisualStudio.ComponentModelHost>マネージ機能拡張フレームワーク (MEF) で使用されるクラス。

- <xref:Microsoft.VisualStudio.Designer.Interfaces>Visual Studio デザイナーで使用されるインターフェイス。

- <xref:Microsoft.VisualStudio.ManagedInterfaces.ProjectDesigner>Visual Studio プロジェクト デザイナーで使用されるインターフェイス。

- <xref:Microsoft.VisualStudio.ManagedInterfaces.Publish>アプリケーションの発行に使用するクラス。

- <xref:Microsoft.VisualStudio.OLE.Interop>OLE コンポーネント用の Visual Studio で使用される相互運用機能インターフェイス。

- <xref:Microsoft.VisualStudio.Package>Visual Studio マネージ言語サービスに使用されるクラス。

- <xref:Microsoft.VisualStudio.PlatformUI>Visual Studio シェルで使用されるクラス。

- <xref:Microsoft.VisualStudio.PlatformUI.OleComponentSupport>マイクロソフトの内部使用のみ。

- <xref:Microsoft.VisualStudio.ProjectAggregator>Visual Studio プロジェクトで使用されるクラス。

- <xref:Microsoft.VisualStudio.Settings>Visual Studio シェルで使用されるクラス。

- <xref:Microsoft.VisualStudio.Shell>Visual Studio シェルで使用されるクラス。

- <xref:Microsoft.VisualStudio.Shell.Design>Visual Studio シェルで使用されるクラス。

- <xref:Microsoft.VisualStudio.Shell.Design.Serialization>Visual Studio シェルで使用されるクラス。

- <xref:Microsoft.VisualStudio.Shell.Design.Serialization.CodeDom>Visual Studio シェルで使用されるクラス。

- <xref:Microsoft.VisualStudio.Shell.Flavor>Visual Studio プロジェクトで使用されるクラス。

- <xref:Microsoft.VisualStudio.Shell.Interop>Visual Studio シェルで使用される相互運用機能インターフェイス。

- <xref:Microsoft.VisualStudio.Shell.Settings>Visual Studio シェルで使用されるクラス。

- <xref:Microsoft.VisualStudio.VSHelp>ヘルプに使用するクラス。

- <xref:VSLangProj>言語サービス プロジェクトに使用されるクラス。

- <xref:XamlGeneratedNamespace>マイクロソフトの内部使用のみ。

- <xref:Microsoft.VisualStudio.ManagedInterfaces9>Visual Studio で使用されるインターフェイス。

- <xref:Microsoft.VisualStudio.WCFReference.Interop>Windows 通信フレームワークで使用されるクラス。

- [テスト](/previous-versions/aa993343(v=vs.120))ツールに使用されるクラス。

- <xref:EnvDTE>ビジュアル スタジオのオートメーションに使用されます。

- <xref:Extensibility>ビジュアル スタジオのオートメーションに使用されます。

- <xref:EnvDTE80>ビジュアル スタジオのオートメーションに使用されます。

- <xref:EnvDTE90>ビジュアル スタジオのオートメーションに使用されます。

- <xref:EnvDTE90a>ビジュアル スタジオのオートメーションに使用されます。

- <xref:EnvDTE100>ビジュアル スタジオのオートメーションに使用されます。

- <xref:Microsoft.VisualStudio.VCCodeModel>Visual C++ プロジェクトオートメーションに使用されます。

- <xref:Microsoft.VisualStudio.VCProject>Visual C++ プロジェクトオートメーションで使用されるクラス。

- <xref:Microsoft.VisualStudio.VCProjectEngine>Visual C++ プロジェクトオートメーションに使用されます。

- <xref:Microsoft.VisualStudio.VsWizard>Visual Studio ウィザードで使用されます。

- <xref:VSLangProj>C# および Visual Basic プロジェクトオートメーションに使用されます。

- <xref:VSLangProj2>C# および Visual Basic プロジェクトオートメーションに使用されます。

- <xref:VSLangProj80>C# および Visual Basic プロジェクトオートメーションに使用されます。

- <xref:VslangProj90>C# および Visual Basic プロジェクトオートメーションに使用されます。

- <xref:VslangProj100>C# および Visual Basic プロジェクトオートメーションに使用されます。

- <xref:VSLangProj110>C# および Visual Basic プロジェクトオートメーションに使用されます。

- <xref:VSLangProj140>C# および Visual Basic プロジェクトオートメーションに使用されます。

- <xref:Microsoft.VisualStudio.Language.CallHierarchy>C# および Visual Basic オートメーションで使用されます。

- <xref:Microsoft.VisualStudio.Language.NavigateTo.Interfaces>C# および Visual Basic オートメーションで使用されます。

- <xref:Microsoft.VisualStudio.Threading>Visual Studio のスレッド処理に使用されます。

- [名前空間を接続します。](/dotnet/api/microsoft.visualstudio.connectedservices)Visual Studio 接続されたサービスに使用されます。

- [列挙体は](../extensibility/intellisensehostflags.md)、IntelliSense ホスト フラグを指定します。

- [VSCT XML スキーマ リファレンス](../extensibility/vsct-xml-schema-reference.md)Visual Studio コマンド テーブル スキーマ要素のテーブルを提供し、それぞれに対して許可された子要素と属性を示します。

- [GUID と定数](../extensibility/guids-and-constants-in-the-visual-studio-sdk.md)SDK 全体で使用される GUID の一覧を示します。

- [マネージ コード内の COM 定数](../extensibility/com-constants-in-managed-code.md)環境 SDK 全体で使用されるユーザー インターフェイス要素の識別子の一覧を提供します。

- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)ソース管理プラグイン API のトピックへのリンクを示します。

- [コマンド ライン スイッチ](../extensibility/command-line-switches-visual-studio-sdk.md)開発者がコマンド ラインからいくつかのタスクを自動化する方法について説明するトピックへのリンクを示します。

- [エラー処理と戻り値](../extensibility/error-handling-and-return-values.md)VSPackages のエラー アーキテクチャについて説明します。

- [オブジェクト](../extensibility/objects.md)環境で使用されるオブジェクトの一覧を示します。

- [用語集](../extensibility/visual-studio-sdk-glossary.md)Visual Studio SDK ドキュメントを読むときに使用する、役立つ用語とその定義の一覧を示します。

- <xref:Microsoft.Build.BuildEngine>MSBuild に使用されます。

- <xref:Microsoft.Build.Construction>MSBuild に使用されます。

- <xref:Microsoft.Build.Conversion>MSBuild に使用されます。

- <xref:Microsoft.Build.Debugging>MSBuild に使用されます。

- <xref:Microsoft.Build.Evaluation>MSBuild に使用されます。

- <xref:Microsoft.Build.Exceptions>MSBuild に使用されます。

- <xref:Microsoft.Build.Execution>MSBuild に使用されます。

- <xref:Microsoft.Build.Framework>MSBuild に使用されます。

- <xref:Microsoft.Build.Framework.XamlTypes>MSBuild に使用されます。

- <xref:Microsoft.Build.Logging>MSBuild に使用されます。

- <xref:Microsoft.Build.Tasks>MSBuild に使用されます。

- <xref:Microsoft.Build.Tasks.Deployment.Bootstrapper>MSBuild に使用されます。

- <xref:Microsoft.Build.Tasks.Deployment.ManifestUtilities>MSBuild に使用されます。

- <xref:Microsoft.Build.Tasks.Hosting>MSBuild に使用されます。

- <xref:Microsoft.Build.Tasks.Xaml>MSBuild に使用されます。

- <xref:Microsoft.Build.Utilities>MSBuild に使用されます。

## <a name="related-sections"></a>関連項目

[Visual Studio SDK](../extensibility/visual-studio-sdk.md)には、Visual Studio と統合する製品の開発に役立つドキュメント、サンプル、およびコードが含まれています。
