---
title: コンテキスト パラメータ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- wizards, context parameters
- context parameters
ms.assetid: 1a062dcb-8a8f-40dd-bea9-3d10f9448966
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6673ad8f26c94165635b5f1bc652b91dcbbfd24f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709302"
---
# <a name="context-parameters"></a>コンテキスト パラメーター
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]統合開発環境 (IDE) では、ウィザードを **[新しいプロジェクト**]、[**新しい項目の追加**]、または **[サブ プロジェクトの追加]** ダイアログ ボックスに追加できます。 追加されたウィザードは、[**ファイル]** メニューまたは**ソリューション エクスプローラ**でプロジェクトを右クリックして使用できます。 IDE は、ウィザードの実装にコンテキストパラメータを渡します。 コンテキストパラメーターは、IDE がウィザードを呼び出すときのプロジェクトの状態を定義します。

 IDE のプロジェクトメソッドの<xref:Microsoft.VisualStudio.Shell.Interop.VSADDITEMOPERATION>呼び出しでフラグを設定してウィザードを<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.AddItem%2A>起動します。 設定すると、プロジェクトは、登録された`IVsExtensibility::RunWizardFile`ウィザード名または GUID と IDE が渡すその他のコンテキスト パラメーターを使用してメソッドを実行する必要があります。

## <a name="context-parameters-for-new-project"></a>新しいプロジェクトのコンテキスト パラメーター

| パラメーター | 説明 |
|-------------------------| - |
| `WizardType` | 登録済みウィザードの<xref:EnvDTE.Constants.vsWizardNewProject>種類 ( ) またはウィザードの種類を示す GUID。 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]この実装では、ウィザードの GUID は {0F90E1D0-4999-11D1-B6D1-00A0C90F2744} です。 |
| `ProjectName` | 一意[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]のプロジェクト名を表す文字列。 |
| `LocalDirectory` | 作業プロジェクト ファイルのローカルの場所。 |
| `InstallationDirectory` | のディレクトリ パス[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]はインストールです。 |
| `FExclusive` | プロジェクトが開いているソリューションを閉じるべきであることを示すブールフラグ。 |
| `SolutionName` | ディレクトリ部分または *.sln*拡張子を含まないソリューション ファイルの名前。 *suo*ファイル名も を使用`SolutionName`して作成されます。 この引数が空の文字列でない場合、ウィザード<xref:EnvDTE._Solution.Create%2A>は<xref:EnvDTE._Solution.AddFromTemplate%2A>プロジェクトを . この名前が空の文字列の場合は<xref:EnvDTE._Solution.AddFromTemplate%2A>、<xref:EnvDTE._Solution.Create%2A>を呼び出さずに使用します。 |
| `Silent` | ウィザードを **[完了]** をクリックした場合と同じようにサイレントモードで`TRUE`実行するかどうかを示すブール値 ( ) |

## <a name="context-parameters-for-add-new-item"></a>新しい項目の追加のコンテキスト パラメーター

| パラメーター | 説明 |
|-------------------------| - |
| `WizardType` | 登録済みウィザードの<xref:EnvDTE.Constants.vsWizardAddItem>種類 ( ) またはウィザードの種類を示す GUID。 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]この実装では、ウィザードの GUID は {0F90E1D1-4999-11D1-B6D1-00A0C90F2744} です。 |
| `ProjectName` | 一意[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]のプロジェクト名を表す文字列。 |
| `ProjectItems` | 作業プロジェクト ファイルを含むローカルの場所。 |
| `ItemName` | 追加する項目の名前。 この名前は、既定のファイル名か、ユーザーが **[項目の追加]** ダイアログ ボックスで入力するファイル名です。 名前は *、.vsdir*ファイルに設定されているフラグに基づいています。 名前には NULL 値を指定できます。 |
| `InstallationDirectory` | のディレクトリ パス[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]はインストールです。 |
| `Silent` | ウィザードを **[完了]** をクリックした場合と同じようにサイレントモードで`TRUE`実行するかどうかを示すブール値 ( ) |

## <a name="context-parameters-for-add-sub-project"></a>サブプロジェクトの追加のコンテキスト パラメータ

| パラメーター | 説明 |
|-------------------------| - |
| `WizardType` | 登録済みウィザードの<xref:EnvDTE.Constants.vsWizardAddSubProject>種類 ( ) またはウィザードの種類を示す GUID。 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]この実装では、ウィザードの GUID は {0F90E1D2-4999-11D1-B6D1-00A0C90F2744} です。 |
| `ProjectName` | 一意[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]のプロジェクト名を表す文字列。 |
| `ProjectItems` | ウィザードが`ProjectItems`動作するコレクションへのポインター。 このポインターは、プロジェクト階層の選択に基づいてウィザードに渡されます。 ユーザーは通常、項目を配置するフォルダーを選択し、プロジェクトの **[項目の追加**] ダイアログ ボックスを呼び出します。 |
| `LocalDirectory` | 作業プロジェクト ファイルのローカルの場所。 |
| `ItemName` | 追加する項目の名前。 この名前は、既定のファイル名か、ユーザーが **[項目の追加]** ダイアログ ボックスで入力するファイル名です。 名前は *、.vsdir*ファイルに設定されているフラグに基づいています。 名前には NULL 値を指定できます。 |
| `InstallationDirectory` | インストールの[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ディレクトリ パス。 |
| `Silent` | ウィザードを **[完了]** をクリックした場合と同じようにサイレントモードで`TRUE`実行するかどうかを示すブール値 ( ) |

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject2>
- [カスタム パラメータ](../../extensibility/internals/custom-parameters.md)
- [ウィザード](../../extensibility/internals/wizards.md)
- [ウィザード (.vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)
- [ウィザードを起動するためのコンテキスト パラメータ](https://msdn.microsoft.com/Library/051a10f4-9e45-4604-b344-123044f33a24)
