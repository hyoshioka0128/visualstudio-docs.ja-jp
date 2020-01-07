---
title: GenerateDeploymentManifest タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#GenerateDeploymentManifest
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, GenerateDeploymentManifest task
- GenerateDeploymentManifest task [MSBuild]
ms.assetid: 0734ebda-734d-49c4-9642-8d9d919d45fd
caps.latest.revision: 32
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6f0c13e5ea8778ca91c30383287aaad6e965bb65
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68149591"
---
# <a name="generatedeploymentmanifest-task"></a>GenerateDeploymentManifest タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 配置マニフェストを生成します。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 配置マニフェストでは、アプリケーションの配置方法について記述します。記述する内容は、配置するための一意の ID の定義、インストールするのかオンライン モードで使用するのかなど配置の特徴の指定、アプリケーションの更新設定および更新プログラムの場所の指定、対応する [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーション マニフェストの指定などです。  
  
## <a name="parameters"></a>パラメーター  
 `GenerateDeploymentManifest` タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`AssemblyName`|省略可能な `String` 型のパラメーターです。<br /><br /> 生成されるマニフェストのアセンブリ ID の `Name` フィールドを指定します。 このパラメーターを指定しない場合、名前は `EntryPoint` パラメーターまたは `InputManifest` パラメーターから推測されます。 名前が推測できない場合、タスクはエラーをスローします。|  
|`AssemblyVersion`|省略可能な `String` 型のパラメーターです。<br /><br /> 生成されるマニフェストのアセンブリ ID の `Version` フィールドを指定します。 このパラメーターを指定しなかった場合、タスクは "1.0.0.0" という値を使用します。|  
|`CreateDesktopShortcut`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> true の場合、ClickOnce アプリケーションのインストール時にデスクトップにアイコンが作成されます。|  
|`DeploymentUrl`|省略可能な `String` 型のパラメーターです。<br /><br /> アプリケーションの更新プログラムの場所を指定します。 このパラメーターを指定しなかった場合、アプリケーションの更新プログラムの場所は定義されません。 ただし、`UpdateEnabled` パラメーターが `true` である場合、更新プログラムの場所を指定する必要があります。 値には、完全修飾 URL または UNC パスを指定します。|  
|`Description`|省略可能な `String` 型のパラメーターです。<br /><br /> アプリケーションの説明を指定します。|  
|`DisallowUrlActivation`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> URL 経由で開かれたときに、アプリケーションを自動的に実行するかどうかを指定します。 このパラメーターを `true` にすると、アプリケーションの実行は [スタート] メニューからのみ行えるようになります。 このパラメーターの既定値は、`false` です。 この値は、`Install` パラメーターが `true` である場合のみ適用されます。|  
|`EntryPoint`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 生成されるマニフェスト アセンブリのエントリ ポイントを指定します。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 配置マニフェストの場合には、[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーション マニフェストを指定します。<br /><br /> [!INCLUDE[vsprvslong](../includes/vsprvslong-md.md)] では、[GenerateApplicationManifest タスク](../msbuild/generateapplicationmanifest-task.md)でアプリケーション マニフェストを生成するためには、`EntryPoint` が必要でした (アセンブリ マニフェストまたはネイティブ マニフェストの場合、`EntryPoint` は不要)。ビルド エラーでこの要件が適用されます。"MSB 3185。EntryPoint マニフェストに指定されていません。"<br /><br /> [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] では、`EntryPoint` タスク パラメーターが指定されていなくても、このエラーは発生しません。 代わりに、たとえば \<customHostSpecified> タグが \<entryPoint> タグの子として挿入されます。<br /><br /> `<entryPoint xmlns="urn:schemas-`<br /><br /> `microsoft-com:asm.v2">`<br /><br /> `<co.v1:customHostSpecified />`<br /><br /> `</entryPoint>`<br /><br /> 次の手順を使用して、アプリケーション マニフェストに DLL 依存関係を追加できます。<br /><br /> 1. <xref:Microsoft.Build.Tasks.ResolveAssemblyReference> への呼び出しでアセンブリの参照を解決します。<br />2.前のタスクの出力とアセンブリ自体を <xref:Microsoft.Build.Tasks.ResolveManifestFiles> に渡します。<br />3.`Dependencies` パラメーターを使用して <xref:Microsoft.Build.Tasks.GenerateApplicationManifest> に依存関係を渡します。|  
|`ErrorReportUrl`|省略可能な [String](<!-- TODO: review code entity reference <xref:assetId:///String?qualifyHint=False&amp;autoUpgrade=True>  -->) のパラメーターです。<br /><br /> ClickOnce のインストール時にダイアログ ボックスに表示される Web ページの URL を指定します。|  
|`InputManifest`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです。<br /><br /> マニフェスト ジェネレーターのベースとして使用する、入力 XML ドキュメントを指定します。 これによって、カスタム マニフェスト定義など、構造化されたデータが出力マニフェストに反映されます。 XML ドキュメントのルート要素は、asmv1 名前空間内のアセンブリ ノードである必要があります。|  
|`Install`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> アプリケーションがインストールされているアプリケーションであるか、オンライン専用アプリケーションであるかを指定します。 このパラメーターを `true` にすると、アプリケーションはユーザーの [スタート] メニューにインストールされ、[プログラムの追加と削除] ダイアログ ボックスから削除できるようになります。 このパラメーターを `false` にすると、アプリケーションは Web ページからオンラインで使用するためのものになります。 このパラメーターの既定値は、`true` です。|  
|`MapFileExtensions`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> .deploy ファイル名拡張子の割り当てを使用するかどうかを指定します。 このパラメーターを `true` にすると、各プログラム ファイルは、.deploy のファイル名拡張子で発行されます。 このオプションを使用すると、ブロックを解除して [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーション配置を有効にする必要があるファイル名拡張子の数を制限できるので、Web サーバーのセキュリティに役立ちます。 このパラメーターの既定値は、`false` です。|  
|`MaxTargetPath`|省略可能な `String` 型のパラメーターです。<br /><br /> [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーション配置におけるファイル パスの最大許容長を指定します。 このパラメーターを指定した場合、アプリケーションで指定されている各ファイル パスの長さが、この制限に照らしてチェックされます。 この制限を超える項目に対しては、ビルド警告が出力されます。 入力を指定しないか、ゼロを指定した場合、チェック処理は行われません。|  
|`MinimumRequiredVersion`|省略可能な `String` 型のパラメーターです。<br /><br /> ユーザーが更新をスキップできるかどうかを指定します。 最低限必要なバージョンよりも前のバージョンをユーザーが所有している場合、ユーザーは更新をスキップできません。 この入力は、`Install` パラメーターの値が `true` である場合のみ適用されます。|  
|`OutputManifest`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです。<br /><br /> 生成される出力マニフェスト ファイルの名前を指定します。 このパラメーターが指定されていない場合、出力ファイルの名前は、生成されるマニフェストの ID から推測されます。|  
|`Platform`|省略可能な `String` 型のパラメーターです。<br /><br /> アプリケーションの対象プラットフォームを指定します。 このパラメーターには、次の値を指定できます。<br /><br /> -   `AnyCPU`<br />-   `x86`<br />-   `x64`<br />-   `Itanium`<br /><br /> 既定値は `AnyCPU` です。|  
|`Product`|省略可能な `String` 型のパラメーターです。<br /><br /> アプリケーション名を示します。 このパラメーターが指定されていない場合、名前は、生成されるマニフェストの ID から推測されます。 この名前は、[スタート] メニューに表示する名前として使用され、[プログラムの追加と削除] ダイアログ ボックスに表示される名前の一部としても使用されます。|  
|`Publisher`|省略可能な `String` 型のパラメーターです。<br /><br /> アプリケーションの発行者を指定します。 このパラメーターが指定されていない場合、名前は、登録されているユーザー名または生成されるマニフェストの ID から推測されます。 この名前は、[スタート] メニューに表示するフォルダー名として使用され、[プログラムの追加と削除] ダイアログ ボックスに表示される名前の一部としても使用されます。|  
|`SuiteNamel`|省略可能な `String` 型のパラメーターです。<br /><br /> ClickOnce の配置後にアプリケーションが存在する、[スタート] メニューのフォルダーの名前を指定します。|  
|`SupportUrl`|省略可能な `String` 型のパラメーターです。<br /><br /> [プログラムの追加と削除] ダイアログ ボックスで、このアプリケーションのエントリに表示されるリンクを指定します。 値には、完全修飾 URL または UNC パスを指定します。|  
|`TargetCulture`|省略可能な `String` 型のパラメーターです。<br /><br /> アプリケーションのカルチャを指定し、生成されるマニフェストのアセンブリ ID の `Language` フィールドを指定します。 このパラメーターを指定しなかった場合、アプリケーションは、カルチャに依存しないと仮定されます。|  
|`TrustUrlParameters`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> アプリケーションで、URL クエリ文字列パラメーターが使用できるかどうかを指定します。 このパラメーターの既定値は、アプリケーションでパラメーターが使用できないことを示す `false` です。|  
|`UpdateEnabled`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> アプリケーションが更新プログラムに対して有効であるかどうかを指定します。 このパラメーターの既定値は、`false` です。 このパラメーターは、`Install` パラメーターが `true` である場合のみ適用されます。|  
|`UpdateInterval`|省略可能な `Int32` 型のパラメーターです。<br /><br /> アプリケーションの更新間隔を指定します。 このパラメーターの既定値は、ゼロです。 このパラメーターは、`Install` パラメーターおよび `UpdateEnabled` パラメーターの両方が `true` である場合にのみ適用されます。|  
|`UpdateMode`|省略可能な `String` 型のパラメーターです。<br /><br /> 更新プログラムの確認を、アプリケーションを起動する前にフォアグラウンドで行うのか、アプリケーションの実行中にバックグラウンドで行うのかを指定します。 このパラメーターには、次の値を指定できます。<br /><br /> -   `Foreground`<br />-   `Background`<br /><br /> このパラメーターの既定値は、`Background` です。 このパラメーターは、`Install` パラメーターおよび `UpdateEnabled` パラメーターの両方が `true` である場合にのみ適用されます。|  
|`UpdateUnit`|省略可能な `String` 型のパラメーターです。<br /><br /> `UpdateInterval` パラメーターの単位を指定します。 このパラメーターには、次の値を指定できます。<br /><br /> -   `Hours`<br />-   `Days`<br />-   `Weeks`<br /><br /> このパラメーターは、`Install` パラメーターおよび `UpdateEnabled` パラメーターの両方が `true` である場合にのみ適用されます。|  
  
## <a name="remarks"></a>Remarks  
 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.GenerateManifestBase> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 Task クラスのパラメーターの一覧については、[「Task Base Class」](../msbuild/task-base-class.md) を参照してください。  
  
## <a name="see-also"></a>関連項目
 [タスク](../msbuild/msbuild-tasks.md)   
 [GenerateApplicationManifest タスク](../msbuild/generateapplicationmanifest-task.md)   
 [SignFile タスク](../msbuild/signfile-task.md)   
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)
