---
title: ユーザー設定のサポート |Microsoft Docs
description: Visual Studio SDK の設定 Api を使用して、設定カテゴリの永続化を有効にする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Custom Settings Points
- user settings [Visual Studio SDK], registering persistence support
- persistence, registering settings
ms.assetid: ad9beac3-4f8d-4093-ad0e-6fb00444a709
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e0128ce1f27674010d1b624457815ddb1016e016
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080646"
---
# <a name="support-for-user-settings"></a>ユーザー設定のサポート
VSPackage は、1つまたは複数の設定カテゴリを定義できます。これは、ユーザーが [**ツール**] メニューの [**設定のインポート/エクスポート**] コマンドを選択したときに保持される状態変数のグループです。 この永続化を有効にするには、の設定 Api を使用し [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] ます。

 レジストリエントリはカスタム設定ポイントとして参照され、GUID は VSPackage の設定カテゴリを定義します。 VSPackage は、カスタム設定ポイントで定義されている複数の設定カテゴリをサポートできます。

- (インターフェイスを使用して) 相互運用機能アセンブリに基づく設定を実装 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserSettings> するには、レジストリを編集するか、レジストラースクリプト (.rgs ファイル) を使用して、カスタム設定ポイントを作成する必要があります。 詳細については、「 [Creating Registrar Scripts](/cpp/atl/creating-registrar-scripts)」を参照してください。

- Managed Package Framework (MPF) を使用するコードでは、カスタム設定ポイントごとにを VSPackage にアタッチすることによって、カスタム設定ポイントを作成する必要があり <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> ます。

     1つの VSPackage が複数のカスタム設定ポイントをサポートしている場合、各カスタム設定ポイントは個別のクラスによって実装され、クラスの一意のインスタンスによって登録され <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> ます。 その結果、クラスを実装する設定では、複数の設定カテゴリをサポートできます。

## <a name="custom-settings-point-registry-entry-details"></a>カスタム設定ポイントのレジストリエントリの詳細
 カスタム設定ポイントは、次の場所にあるレジストリエントリに作成されます: HKLM\Software\Microsoft\VisualStudio \\ *\<Version>* \UserSettings \\ `<CSPName>` 。ここで、は、VSPackage が `<CSPName>` サポートするカスタム設定ポイントの名前です *\<Version>* [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。は、8.0 などのバージョンです。

> [!NOTE]
> \\ *\<Version>* [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE: integrated development environment) が初期化されると、HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudioのルートパスを代替ルートでオーバーライドできます。 詳細については、「 [コマンドラインスイッチ](../../extensibility/command-line-switches-visual-studio-sdk.md)」を参照してください。

 レジストリエントリの構造を次に示します。

 HKLM\Software\Microsoft\VisualStudio \\ *\<Version>* \ Usersettings\

 `<CSPName`>= s ' #12345 '

 Package = ' {XXXXXX XXXX XXXX xxxx XXXXXXXXX} '

 Category = ' {YYYYYY YYYY yyyy yyyy YYYYYYYYY} '

 ResourcePackage = ' {ZZZZZZ ZZZZ ZZZZ ZZZZ ZZZZZZZZZ} '

 AlternateParent = 区分名

| Name | 種類 | Data | 説明 |
|-----------------|--------| - | - |
| (既定値)。 | REG_SZ | カスタム設定ポイントの名前 | キーの名前 ( `<CSPName`>) は、カスタム設定ポイントの unlocalized 名です。<br /><br /> MPF に基づく実装では、 `categoryName` コンストラクターの引数と引数をに組み合わせてキーの名前を取得し `objectName` <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> `categoryName_objectName` ます。<br /><br /> キーは空にすることも、サテライト DLL 内のローカライズされた文字列への参照 ID を含めることもできます。 この値は、コンストラクターの引数から取得され `objectNameResourceID` <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> ます。 |
| パッケージ | REG_SZ | GUID | カスタム設定ポイントを実装する VSPackage の GUID。<br /><br /> MPF に基づく実装クラスを使用して <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> 、VSPackage のおよびリフレクションを含むコンストラクターの引数を使用して、 `objectType` <xref:System.Type> この値を取得します。 |
| カテゴリ | REG_SZ | GUID | 設定カテゴリを識別する GUID。<br /><br /> 相互運用機能アセンブリに基づく実装では、この値を任意に選択した GUID にすることができます。この GUID は [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE が <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserSettings.ExportSettings%2A> メソッドとメソッドに渡し <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserSettings.ImportSettings%2A> ます。 これらの2つのメソッドのすべての実装は、GUID 引数を検証する必要があります。<br /><br /> MPF に基づく実装の場合、この GUID は、設定メカニズムを実装するクラスのによって取得され <xref:System.Type> [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 |
| ResourcePackage | REG_SZ | GUID | 省略可能。<br /><br /> 実装している VSPackage が指定していない場合に、ローカライズされた文字列を含むサテライト DLL へのパス。<br /><br /> MPF は、リフレクションを使用して適切なリソース VSPackage を取得するため、 <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> クラスはこの引数を設定しません。 |
| AlternateParent | REG_SZ | このカスタム設定ポイントを含む [ツールオプション] ページの下にあるフォルダーの名前。 | 省略可能。<br /><br /> この値は、設定の実装で、状態を保存するオートメーションモデルのメカニズムではなく、の永続化メカニズムを使用する **ツールオプション** ページがサポートされている場合にのみ設定する必要があり [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] ます。<br /><br /> このような場合、AlternateParent キーの値は、 `topic` `topic.sub-topic` 特定の **ToolsOptions** ページを識別するために使用される文字列のセクションです。 たとえば、 **ToolsOptions** ページの場合、 `"TextEditor.Basic"` alternateparent の値はになり `"TextEditor"` ます。<br /><br /> <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>でカスタム設定ポイントが生成されると、カテゴリ名と同じになります。 |
