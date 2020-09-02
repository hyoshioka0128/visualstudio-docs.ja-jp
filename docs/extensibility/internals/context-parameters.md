---
title: コンテキストパラメーター |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80709302"
---
# <a name="context-parameters"></a>コンテキスト パラメーター
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]統合開発環境 (IDE) では、[**新しいプロジェクト**]、[**新しい項目の追加**]、または [**サブプロジェクトの追加**] ダイアログボックスにウィザードを追加できます。 追加したウィザードは、[ **ファイル** ] メニューまたは **ソリューションエクスプローラー**でプロジェクトを右クリックして表示できます。 IDE は、ウィザードの実装にコンテキストパラメーターを渡します。 IDE がウィザードを呼び出すと、コンテキストパラメーターによってプロジェクトの状態が定義されます。

 IDE では、 <xref:Microsoft.VisualStudio.Shell.Interop.VSADDITEMOPERATION> プロジェクトのメソッドに対する ide の呼び出しのフラグを設定することにより、ウィザードが起動し <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.AddItem%2A> ます。 設定した場合、プロジェクトは、 `IVsExtensibility::RunWizardFile` 登録されているウィザードの名前または GUID、および IDE によって渡されるその他のコンテキストパラメーターを使用して、メソッドを実行する必要があります。

## <a name="context-parameters-for-new-project"></a>新しいプロジェクトのコンテキストパラメーター

| パラメーター | 説明 |
|-------------------------| - |
| `WizardType` | 登録されたウィザードの種類 ( <xref:EnvDTE.Constants.vsWizardNewProject> )、またはウィザードの種類を示す GUID。 実装で [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] は、ウィザードの GUID は {0F90E1D0-4999-11D1-B6D1-00A0C90F2744} です。 |
| `ProjectName` | 一意のプロジェクト名を表す文字列 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 |
| `LocalDirectory` | 作業プロジェクトファイルのローカルの場所。 |
| `InstallationDirectory` | のディレクトリパス [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] がインストールされています。 |
| `FExclusive` | プロジェクトが開いているソリューションを閉じる必要があることを示すブール型のフラグ。 |
| `SolutionName` | ディレクトリ部分または *.sln* 拡張子のないソリューションファイルの名前。 *.Suo*ファイル名は、を使用して作成することもでき `SolutionName` ます。 この引数が空の文字列でない場合、ウィザードは <xref:EnvDTE._Solution.Create%2A> を使用してプロジェクトをに追加 <xref:EnvDTE._Solution.AddFromTemplate%2A> します。 この名前が空の文字列の場合は、を呼び出さずにを使用し <xref:EnvDTE._Solution.AddFromTemplate%2A> <xref:EnvDTE._Solution.Create%2A> ます。 |
| `Silent` | ウィザードを **[完了** ] がクリックされたかのようにサイレントモードで実行するかどうかを示すブール値 `TRUE` です ()。 |

## <a name="context-parameters-for-add-new-item"></a>[新しい項目の追加] のコンテキストパラメーター

| パラメーター | 説明 |
|-------------------------| - |
| `WizardType` | 登録されたウィザードの種類 ( <xref:EnvDTE.Constants.vsWizardAddItem> )、またはウィザードの種類を示す GUID。 実装で [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] は、ウィザードの GUID は {0F90E1D1-4999-11D1-B6D1-00A0C90F2744} です。 |
| `ProjectName` | 一意のプロジェクト名を表す文字列 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 |
| `ProjectItems` | 作業中のプロジェクトファイルが格納されているローカルの場所。 |
| `ItemName` | 追加する項目の名前。 この名前は、[ **項目の追加** ] ダイアログボックスでユーザーが入力する既定のファイル名またはファイル名のいずれかになります。 この名前は、 *.vsdir* ファイルに設定されているフラグに基づいています。 名前には null 値を指定できます。 |
| `InstallationDirectory` | のディレクトリパス [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] がインストールされています。 |
| `Silent` | ウィザードを **[完了** ] がクリックされたかのようにサイレントモードで実行するかどうかを示すブール値 `TRUE` です ()。 |

## <a name="context-parameters-for-add-sub-project"></a>サブプロジェクトの追加のコンテキストパラメーター

| パラメーター | 説明 |
|-------------------------| - |
| `WizardType` | 登録されたウィザードの種類 ( <xref:EnvDTE.Constants.vsWizardAddSubProject> )、またはウィザードの種類を示す GUID。 実装で [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] は、ウィザードの GUID は {0F90E1D2-4999-11D1-B6D1-00A0C90F2744} です。 |
| `ProjectName` | 一意のプロジェクト名を表す文字列 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 |
| `ProjectItems` | `ProjectItems`ウィザードが動作するコレクションへのポインター。 このポインターは、プロジェクト階層の選択に基づいてウィザードに渡されます。 ユーザーは、通常、項目を配置するフォルダーを選択してから、プロジェクトの [ **項目の追加** ] ダイアログボックスを呼び出します。 |
| `LocalDirectory` | 作業プロジェクトファイルのローカルの場所。 |
| `ItemName` | 追加する項目の名前。 この名前は、[ **項目の追加** ] ダイアログボックスでユーザーが入力する既定のファイル名またはファイル名のいずれかになります。 この名前は、 *.vsdir* ファイルに設定されているフラグに基づいています。 名前には null 値を指定できます。 |
| `InstallationDirectory` | インストールのディレクトリパス [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 |
| `Silent` | ウィザードを **[完了** ] がクリックされたかのようにサイレントモードで実行するかどうかを示すブール値 `TRUE` です ()。 |

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject2>
- [カスタムパラメーター](../../extensibility/internals/custom-parameters.md)
- [ウィザード](../../extensibility/internals/wizards.md)
- [ウィザード (.vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)
- [ウィザードを起動するためのコンテキストパラメーター](https://msdn.microsoft.com/Library/051a10f4-9e45-4604-b344-123044f33a24)
