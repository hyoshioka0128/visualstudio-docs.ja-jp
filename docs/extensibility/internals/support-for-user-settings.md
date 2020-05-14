---
title: ユーザー設定のサポート |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Custom Settings Points
- user settings [Visual Studio SDK], registering persistence support
- persistence, registering settings
ms.assetid: ad9beac3-4f8d-4093-ad0e-6fb00444a709
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 02bb2450196de76917e9cffc2f5f5acc6c8ee7b7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704790"
---
# <a name="support-for-user-settings"></a>ユーザー設定のサポート
VSPackage は、1 つ以上の設定カテゴリを定義できます。 **Import/Export Settings** **Tools** この永続性を有効にするには、 の設定 API[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]を使用します。

 カスタム設定ポイントと参照されるレジストリ エントリと GUID は、VSPackage の設定カテゴリを定義します。 VSPackage は、カスタム設定ポイントで定義された複数の設定カテゴリをサポートできます。

- 相互運用機能アセンブリに基づく設定の実装 (インターフェイスを<xref:Microsoft.VisualStudio.Shell.Interop.IVsUserSettings>使用) では、レジストリを編集するか、レジストラー スクリプト (.rgs ファイル) を使用してカスタム設定ポイントを作成する必要があります。 詳細については、「 [Creating Registrar Scripts](/cpp/atl/creating-registrar-scripts)」を参照してください。

- マネージ パッケージ フレームワーク (MPF) を使用するコードでは、各カスタム設定<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>ポイントの VSPackage にをアタッチしてカスタム設定ポイントを作成する必要があります。

     1 つの VSPackage が複数のカスタム設定ポイントをサポートしている場合、各カスタム設定ポイントは個別のクラスによって実装され、それぞれが<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>クラスの一意のインスタンスによって登録されます。 したがって、クラスを実装する設定は、複数の設定カテゴリをサポートできます。

## <a name="custom-settings-point-registry-entry-details"></a>カスタム設定ポイントレジストリエントリの詳細
 カスタム設定ポイントは、次の場所のレジストリ エントリに作成されます: HKLM\ソフトウェア\マイクロソフト\\*\<* \VisualStudio バージョン\\`<CSPName>`>`<CSPName>` \UserSettings、VSPackage がサポートするカスタム設定ポイントの名前と*\<バージョン* [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]>は、たとえば 8.0 のバージョンです。

> [!NOTE]
> 統合開発環境 (IDE) が初期化されるときに、HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\*\<バージョン>* の[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ルート パスを代替ルートでオーバーライドできます。 詳細については、「コマンド[ライン スイッチ](../../extensibility/command-line-switches-visual-studio-sdk.md)」を参照してください。

 レジストリ エントリの構造を次に示します。

 HKLM\ソフトウェア\マイクロソフト\ビジュアルスタジオ\\*\<バージョン>* \ユーザー設定\

 `<CSPName`>= '#12345'

 パッケージ = '{XXXXXX XXXX XXXX XXXX XXX XXXXXXXXXXXXXXX}'

 カテゴリ = '{YYYYYYY YYYYYYYYYYYYYYYYYYYYy}'

 リソースパッケージ = '{ZZZZZZ ZZZZ ZZZZ ZZZZZZZZZZZZ}'

 代替親 = カテゴリ名

| 名前 | Type | Data | 説明 |
|-----------------|--------| - | - |
| (既定値)。 | REG_SZ | カスタム設定ポイントの名前 | キーの名前`<CSPName`は>、カスタム設定ポイントのローカライズされていない名前です。<br /><br /> MPF に基づく実装`categoryName`の場合、`objectName`<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>キーの名前は、 コンストラクターの と の引数を`categoryName_objectName`に結合することによって取得されます。<br /><br /> キーは空にすることも、サテライト DLL のローカライズされた文字列への参照 ID を含めることもできます。 この値は、コンストラクタの`objectNameResourceID`引数から取得<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>されます。 |
| Package | REG_SZ | GUID | カスタム設定ポイントを実装する VSPackage の GUID。<br /><br /> <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>クラスを使用する MPF に基づく実装では、VSPackage とリフレクションを含むコンストラクターの`objectType`<xref:System.Type>引数を使用してこの値を取得します。 |
| カテゴリ | REG_SZ | GUID | 設定カテゴリを識別する GUID です。<br /><br /> 相互運用機能アセンブリに基づく実装の場合、この値は、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]任意<xref:Microsoft.VisualStudio.Shell.Interop.IVsUserSettings.ExportSettings%2A><xref:Microsoft.VisualStudio.Shell.Interop.IVsUserSettings.ImportSettings%2A>に選択された GUID を指定できます。 これら 2 つのメソッドのすべての実装では、GUID 引数を確認する必要があります。<br /><br /> MPF に基づく実装の場合、この GUID<xref:System.Type>は、設定機構を[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]実装するクラスの によって取得されます。 |
| リソースパッケージ | REG_SZ | GUID | 省略可能。<br /><br /> 実装 VSPackage がそれらを提供しない場合、ローカライズされた文字列を含むサテライト DLL へのパス。<br /><br /> MPF はリフレクションを使用して正しいリソース<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>VSPackage を取得するため、クラスはこの引数を設定しません。 |
| 代替親 | REG_SZ | このカスタム設定ポイントを含む [ツール オプション] ページの下にあるフォルダの名前。 | 省略可能。<br /><br /> この値を設定する必要があるのは、オートメーション モデル**Tools Options**の状態を保存するメカニズムではなく、永続化メカニズム[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]を使用する Tools Options ページが設定実装でサポートされている場合のみです。<br /><br /> このような場合、代替親キーの値は、特定の`topic`**ツールオプション**ページ`topic.sub-topic`を識別するために使用される文字列のセクションです。 たとえば、[**ツール] オプション**ページ`"TextEditor.Basic"`の場合、代替親の値`"TextEditor"`は になります。<br /><br /> カスタム<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>設定ポイントを生成する場合、カテゴリ名と同じです。 |
