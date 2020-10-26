---
title: カスタムプロジェクトのバージョン認識 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
ms.assetid: 5233d3ff-6e89-4401-b449-51b4686becca
caps.latest.revision: 33
manager: jillfra
ms.openlocfilehash: 0b29728cffc962b5d09a5adc45f8cac2093b020a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "67825681"
---
# <a name="making-custom-projects-version-aware"></a>カスタム プロジェクトでのバージョンの認識
カスタム プロジェクト システムでは、カスタム プロジェクトを Visual Studio の複数のバージョンに読み込むことができます。 また、そのタイプのプロジェクトが、以前のバージョンの Visual Studio に読み込まれないようにすることもできます。 そのプロジェクトの修復や変換や廃止が必要になった場合に備えて、今後のバージョンでそのプロジェクト自体が識別されるようにすることもできます。  
  
## <a name="allowing-projects-to-load-in-multiple-versions"></a>複数のバージョンでのプロジェクトの読み込みの許可  
 SP1 以降の [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] で作成されたほとんどのプロジェクトを、複数のバージョンで動作するように変更できます。  
  
 プロジェクトを読み込む前に、Visual Studio は <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory4.UpgradeProject_CheckOnly%2A> メソッドを呼び出してプロジェクトをアップグレードできるかどうかを判別します。 プロジェクトをアップグレードできる場合、`UpgradeProject_CheckOnly` メソッドは後で <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> メソッドを呼び出してプロジェクトをアップグレードできるようにするためのフラグを設定します。 互換性のないプロジェクトはアップグレードできないため、前のセクションで説明したように、 `UpgradeProject_CheckOnly` ではまずプロジェクトの互換性を確認する必要があります。  
  
 プロジェクト システムの作成者として、プロジェクト システムのユーザーがアップグレードをチェックできるように `UpgradeProject_CheckOnly` を ( `IVsProjectUpgradeViaFactory4` インターフェイスから) 実装します。 ユーザーがプロジェクトを開くと、プロジェクトを読み込む前に、このメソッドが呼び出されて、プロジェクトを修復する必要があるかどうかが判別されます。 アップグレード要件の候補が `VSPUVF_REPAIRFLAGS`に列挙され、その中には次のようなものがあります。  
  
1. `SPUVF_PROJECT_NOREPAIR`: 修復は不要です。  
  
2. `VSPUVF_PROJECT_SAFEREPAIR`: プロジェクトと以前のバージョンとの互換性を確保します。以前のバージョンの製品で見られたような問題は発生しません。  
  
3. `VSPUVF_PROJECT_UNSAFEREPAIR`: プロジェクトと以前のバージョンとの互換性を確保しますが、以前のバージョンの製品で見られたような問題が発生するリスクがあります。 たとえば、プロジェクトが別の SDK バージョンに依存している場合、プロジェクトには互換性がありません。  
  
4. `VSPUVF_PROJECT_ONEWAYUPGRADE`: プロジェクトと以前のバージョンとの互換性を確保しません。  
  
5. `VSPUVF_PROJECT_INCOMPATIBLE`: 現在のバージョンがこのプロジェクトをサポートしないことを示します。  
  
6. `VSPUVF_PROJECT_DEPRECATED`: このプロジェクトがサポートされなくなったことを示します。  
  
> [!NOTE]
> 混乱を避けるため、これらを設定するときにアップグレード フラグを組み合わせないでください。 たとえば、 `VSPUVF_PROJECT_SAFEREPAIR | VSPUVF_PROJECT_DEPRECATED`のようなあいまいなアップグレード状態を作成しないでください。  
  
 プロジェクト フレーバーによっては、 `UpgradeProjectFlavor_CheckOnly` インターフェイスから関数 `IVsProjectFlavorUpgradeViaFactory2` を実装することがあります。 この関数が機能するには、前述した `IVsProjectUpgradeViaFactory4.UpgradeProject_CheckOnly` 実装で呼び出す必要があります。 この呼び出しは、Visual Basic または C# 基本プロジェクト システムに既に実装されています。 この関数の機能により、プロジェクト フレーバーで、基本プロジェクト システムによって判別されることに加え、プロジェクトのアップグレード要件も判別できるようになります。 互換性のダイアログ ボックスには、2 つの要件のうち最も深刻なものが示されます。  
  
 Visual Studio は、アップグレード チェックを実行するとき、以前のバージョンのような NULL 値ではなく、ロガーを提供します。 ロガーを使用すると、プロジェクト システムおよびフレーバーでは、古いプロジェクトを正しく読み込むにはどのような性質の変更が必要になるかを理解するために役立つ追加情報を提供できます。 ダイアログ ボックスを使用するのではなく、ロガーを使用して、より多くの情報を提供することをお勧めします。 詳細については、後述の「 [The Upgrade Logger](../misc/making-custom-projects-version-aware.md#BKMK_UpgradeLogger) 」を参照してください。  
  
 マネージド実装の場合、Microsoft.VisualStudio.Shell.Interop.11.0.dll 相互運用機能アセンブリでプロジェクト アップグレード インターフェイスを使用できます。  
  
 `UpgradeProject` メソッドでは、それが加える変更により、プロジェクトが以前のバージョンの Visual Studio に読み込まれないようになるかどうかを判別できます。 該当する場合、メソッドはプロジェクトを互換性なしとしてマークします。 プロジェクトが互換性なしとしてマークされる方法を理解するには、このトピックで前述した「 [Marking a Project as Incompatible](../misc/making-custom-projects-version-aware.md#BKMK_Incompat) 」を参照してください。 このダイアログ ボックスが表示されたら、最初にメソッド `IVsAppCompat.BreakAssetCompatibility` を呼び出すのではなく、メソッド `IVsAppCompat.AskForUserConsentToBreakAssetCompat` を直接呼び出して、プロジェクトを互換性なしとしてマークすることをお勧めします。このダイアログ ボックスを 2 回表示する必要はないためです。  
  
 次に、互換性ユーザー エクスペリエンスの概要の理解に役立つ例を示します。 以前のバージョンで作成されプロジェクトについて、アップグレードが必要であると現在のバージョンが判断した場合は、変更を許可するかどうかを確認するダイアログ ボックスが表示されます。 ユーザーが同意した場合は、プロジェクトが変更され、読み込まれます。 その後、このソリューションを閉じて以前のバージョンで再び開いた場合、この一方向のアップグレード プロジェクトは互換性がなくなり、読み込まれなくなります。 プロジェクトの (アップグレードではなく) 修復のみが必要な場合は、修復したプロジェクトが引き続き両方のバージョンで開きます。  
  
## <a name="marking-a-project-as-incompatible"></a><a name="BKMK_Incompat"></a> プロジェクトを互換性なしとしてマークする  
 プロジェクトを以前のバージョンの Visual Studio との互換性なしとしてマークできます。  たとえば、.NET Framework 4.5 の機能を使用するプロジェクトを作成するとします。 このプロジェクトは [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)]に組み込むことができないため、そのバージョンによって読み込まれないように、このプロジェクトを互換性なしとしてマークすることができます。  
  
 互換性のない機能を追加するコンポーネントには、プロジェクトを互換性なしとしてマークする責任があります。 コンポーネントは、対象となるプロジェクトを表す <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> インターフェイスにアクセスできる必要があります。  
  
#### <a name="to-mark-a-project-as-incompatible"></a>プロジェクトを互換性なしとしてマークするには  
  
1. コンポーネントで、グローバル サービス SVsSolution から `IVsAppCompat` インターフェイスを取得します。  
  
     詳細については、「<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>」を参照してください。  
  
2. コンポーネントで、 `IVsAppCompat.AskForUserConsentToBreakAssetCompat`を呼び出して、対象のプロジェクトを表す `IVsHierarchy` インターフェイスの配列を渡します。  
  
     このメソッドのシグネチャは次のとおりです。  
  
    ```  
    HRESULT AskForUserConsentToBreakAssetCompat([in] SAFEARRAY(IVsHierarchy*) sarrProjectHierarchies)  
  
    ```  
  
     このコードを実装すると、プロジェクト互換性のダイアログ ボックスが表示されます。 指定したすべてのプロジェクトを互換性なしとしてマークしてよいかどうかを確認するように求められます。 ユーザーが同意した場合、 `AskForUserConsentToBreakAssetCompat` は `S_OK`を返します。それ以外の場合、 `AskForUserConsentToBreakAssetCompat` は `OLE_E_PROMPTSAVECANCELLED`を返します。  
  
    > [!WARNING]
    > 最も一般的なシナリオの場合、 `IVsHierarchy` 配列には 1 つの項目のみが含まれます。  
  
3. `AskForUserConsentToBreakAssetCompat` が `S_OK`を返した場合、コンポーネントは互換性を破棄する変更を加えるか、受け入れます。  
  
4. コンポーネントで、互換性なしとしてマークするプロジェクトごとに `IVsAppCompat.BreakAssetCompatibility` メソッドを呼び出します。 コンポーネントでは、Visual Studio がレジストリ内の現在のバージョン文字列を検索するようにするのではなく、パラメーター `lpszMinimumVersion` の値を特定の最小バージョンに設定できます。 この方法は、コンポーネントが今後値を設定するとき、その時点でのレジストリの内容に基づいて誤って値を大きく設定するリスクを最小化します。 そのように高い値を設定した場合、Visual Studio ではプロジェクトを開くことができません。  
  
     このメソッドのシグネチャは次のとおりです。  
  
    ```  
    HRESULT BreakAssetCompatibility([in] IVsHierarchy * pProjHier), [in] LPCOLESTR lpszMinimumVersion);  
  
    ```  
  
     コンポーネントが `lpszMinimumVersion` を NULL に設定した場合は、 `BreakAssetCompatibility` メソッドが `IVsAppCompat.GetCurrentDesignTimeCompatVersion` メソッドを呼び出して、Visual Studio の現在のバージョンを表す文字列を取得します。  
  
     このメソッドのシグネチャは次のとおりです。  
  
    ```  
    HRESULT GetCurrentDesignTimeCompatVersion([out] BSTR * pbstrCurrentDesignTimeCompatVersion)  
    ```  
  
     BreakAssetCompatibility メソッドは、その後 `IVsHierarchy.SetProperty` メソッドを呼び出して、ルート `VSHPROPID_MinimumDesignTimeCompatVersion` プロパティを前の手順で取得したバージョン文字列の値に設定します。  
  
     詳細については、「<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetProperty%2A>」を参照してください。  
  
> [!IMPORTANT]
> プロジェクトを互換性ありまたは互換性なしとしてマークするには、 `VSHPROPID_MinimumDesignTimeCompatVersion` プロパティを実装する必要があります。 たとえば、プロジェクト システムが MSBuild プロジェクト ファイルを使用している場合は、対応する `<MinimumVisualStudioVersion>` プロパティ値と等しい値を持つ `VSHPROPID_MinimumDesignTimeCompatVersion` ビルド プロパティをプロジェクト ファイルに追加します。  
  
## <a name="detecting-whether-a-project-is-incompatible"></a>プロジェクトに互換性があるかどうかの検出  
 Visual Studio の現在のバージョンと互換性がないプロジェクトは、読み込まれないようにする必要があります。 さらに、互換性のないプロジェクトは、アップグレードしたり修復したりすることができません。 このため、プロジェクトの互換性は 2 回確認する必要があります。1 回目はプロジェクトのアップグレードや修復を検討するときで、2 回目はプロジェクトを読み込む前です。  
  
 プロジェクトに互換性がないことを検出できるようにするには、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory4.UpgradeProject_CheckOnly%2A> メソッドと <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A> メソッドを実装する必要があります。 プロジェクトに互換性がない場合は、 `UpgradeProject_CheckOnly` が成功コード `VS_S_INCOMPATIBLEPROJECT`を返し、 `CreateProject` がエラー コード `VS_E_INCOMPATIBLEPROJECT`を返す必要があります。 フレーバー プロジェクトの場合は、 `IVsProjectFlavorUpgradeViaFactory2.UpgradeProjectFlavor_CheckOnly` ではなく `IVsProjectUpgradeViaFactory4.UpgradeProject_CheckOnly`を実装する必要があります。  
  
 プロジェクト システムの上に Web、Office (VSTO)、Silverlight などのプロジェクト タイプが構築されている場合、そのプロジェクト システムはフレーバーと呼ばれます。 `IVsProjectUpgradeViaFactory.UpgradeProject_CheckOnly` を既に実装している以前のプロジェクト システムも、 `IVsProjectFlavorUpgradeViaFactory.UpgradeProjectFlavor_CheckOnly` を既に実装しているフレーバー プロジェクト システムも引き続きサポートされます。 古いバージョンの `IVsProjectUpgradeViaFactory.UpgradeProject_CheckOnly` の実装シグネチャは次のとおりです。  
  
```  
IVsProjectUpgradeViaFactory::UpgradeProject_CheckOnly(  
  
/* [in] */ BSTR bstrFileName,  
/* [in] */ IVsUpgradeLogger *pLogger,  
/* [out] */ BOOL *pUpgradeRequired,  
/* [out] */ GUID *pguidNewProjectFactory,  
/* [out] */ VSPUVF_FLAGS *pUpgradeProjectCapabilityFlags  
)  
```  
  
 このメソッドが `pUpgradeRequired` を TRUE に設定し、 `S_OK`を返した場合、その結果は "アップグレード" として扱われ、メソッドが値 `VSPUVF_PROJECT_ONEWAYUPGRADE`にアップグレード フラグを設定した場合と同様になります。このことについては、このトピックで後述します。 この古いメソッドを使用することで、次の戻り値がサポートされます。ただし、 `pUpgradeRequired` を TRUE に設定しているときに限られます。  
  
1. `VS_S_PROJECT_SAFEREPAIRREQUIRED`. この戻り値は、 `pUpgradeRequired` (このトピックで後述) と同様、 `VSPUVF_PROJECT_SAFEREPAIR`値を TRUE に変換します。  
  
2. `VS_S_PROJECT_UNSAFEREPAIRREQUIRED`. この戻り値は、 `pUpgradeRequired` (このトピックで後述) と同様、 `VSPUVF_PROJECT_UNSAFEREPAIR`値を TRUE に変換します。  
  
3. `VS_S_PROJECT_ONEWAYUPGRADEREQUIRED`. この戻り値は、 `pUpgradeRequired` (このトピックで後述) と同様、 `VSPUVF_PROJECT_ONEWAYUPGRADE`値を TRUE に変換します。  
  
   `IVsProjectUpgradeViaFactory4` と `IVsProjectFlavorUpgradeViaFactory2` の新しい実装により、移行の種類をより正確に指定できます。  
  
> [!NOTE]
> `UpgradeProject_CheckOnly` メソッドで互換性チェックの結果をキャッシュして、後で `CreateProject`を呼び出すことでもその結果を使用できるようにすることができます。  
  
 たとえば、SP1 プロジェクト システムの `UpgradeProject_CheckOnly` 用に記述した `CreateProject` メソッドと [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] メソッドがプロジェクト ファイルを調べて、 `<MinimumVisualStudioVersion>` ビルド プロパティが "11.0" であることを検出した場合、Visual Studio 2010 SP1 はプロジェクトを読み込みません。 さらに、 **ソリューション ナビゲーター** は、プロジェクトに "互換性がなく"、読み込まれないことを示します。  
  
## <a name="the-upgrade-logger"></a><a name="BKMK_UpgradeLogger"></a> アップグレード Logger  
 `IVsProjectUpgradeViaFactory::UpgradeProject` の呼び出しには `IVsUpgradeLogger` ロガーが含まれており、プロジェクト システムとフレーバーはそのロガーを使用してトラブルシューティング用に詳細なアップグレード トレースを提供します。 警告またはエラーが記録された場合は、アップグレード レポートが表示されます。  
  
 アップグレード ロガーを記述するときは、次のガイドラインを考慮してください。  
  
- すべてのプロジェクトのアップグレードが完了した後で、Visual Studio が Flush を呼び出します。 プロジェクト システムでは呼び出さないでください。  
  
- LogMessage 関数には、次のエラー レベルがあります。  
  
  - 0 は、トレースする情報用です。  

  - 1 は警告用です。  

  - 2 はエラー用です。  

  - 3 はレポート フォーマッタ用です。 プロジェクトをアップグレードすると、"Converted" という単語が 1 回記録されます。この単語はローカライズしないでください。  
  
- プロジェクトの修復やアップグレードが必要ない場合は、UpgradeProject_CheckOnly メソッドまたは UpgradeProjectFlavor_CheckOnly メソッドの実行時にプロジェクト システムが警告またはエラーを記録したときにのみ、ログ ファイルが生成されます。
