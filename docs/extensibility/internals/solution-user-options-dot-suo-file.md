---
title: ソリューション ユーザー オプション (.Suo) ファイル |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- .suo files, VSPackages
- suo files, VSPackages
- solutions, .suo files
- solutions, user options
- solution user options (.suo) file
ms.assetid: 75258e0d-600d-4a3d-94f4-3d7ac12cb47c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9469663d3ac258e1c568778894d8584c68c13632
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705319"
---
# <a name="solution-user-options-suo-file"></a>ソリューション ユーザー オプション (.Suo) ファイル
ソリューション ユーザー オプション (.suo) ファイルには、ユーザーごとのソリューション オプションが含まれています。 このファイルはソース コード管理にチェックインしないでください。

 ソリューション ユーザー オプション (.suo) ファイルは、バイナリ形式で格納された構造化ストレージファイル(複合ファイル)です。 ストリームの名前が .suo ファイル内の情報を識別するために使用されるキーであるストリームにユーザー情報を保存します。 ソリューション ユーザー オプション ファイルは、ユーザー設定の保存に使用され、Visual Studio がソリューションを保存するときに自動的に作成されます。

 環境は、.suo ファイルを開くと、現在読み込まれているすべての VSPackages を列挙します。 VSPackage がインターフェイスを実装<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>する場合、環境は VSPackage のメソッドを<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.LoadUserOptions%2A>呼び出して、.suo ファイルからすべてのデータを読み込むように要求します。

 .suo ファイルに書き込んだストリームを知るのは VSPackage の責任です。 VSPackage は、書き込んだストリームごとに、キーによって識別される<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.LoadPackageUserOpts%2A>特定のストリーム (ストリームの名前) を読み込むために、環境に対して呼び出しを行います。 次に、環境は VSPackage を呼び出して、ストリームの名前とメソッドへのポインター`IStream`を渡す<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.LoadPackageUserOpts%2A>特定のストリームを読み取ります。

 その時点で、別の呼び出`LoadUserOptions`しが行われ、.suo ファイルの別のセクションが読み取られる必要があるかどうかを確認します。 このプロセスは、.suo ファイル内のすべてのデータ ストリームが環境によって読み取られ、処理されるまで続きます。

 ソリューションが保存または閉じられると、環境はメソッドへの<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.SavePackageSolutionProps%2A>ポインターを使用してメソッドを<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.SaveUserOptions%2A>呼び出します。 保存`IStream`するバイナリ情報を含む情報が<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.WriteUserOptions%2A>メソッドに渡され、その情報が .suo ファイルに書き込まれ`SaveUserOptions`、メソッドを再度呼び出して、.suo ファイルに書き込む情報が別に流れるかどうかを確認します。

 これら 2`SaveUserOptions`つの`WriteUserOptions`メソッドと と は、情報のストリームごとに再帰的に呼び出され、.suo ファイル`IVsSolutionPersistence`に保存され、ポインタを渡します。 suo ファイルに複数のストリームを書き込むために再帰的に呼び出されます。 このようにして、ユーザー情報はソリューションと共に保持され、次回ソリューションを開いたときに存在することが保証されます。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>
- [ソリューション](../../extensibility/internals/solutions-overview.md)
