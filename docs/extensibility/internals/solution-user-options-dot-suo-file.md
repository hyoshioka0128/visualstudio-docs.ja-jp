---
title: ソリューションユーザーオプション (..Suo) File |Microsoft Docs
description: ソリューションユーザーオプション (.suo) ファイルについて説明します。このファイルには、バイナリ形式で格納された構造化ストレージファイルのユーザーごとのソリューションオプションが含まれています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- .suo files, VSPackages
- suo files, VSPackages
- solutions, .suo files
- solutions, user options
- solution user options (.suo) file
ms.assetid: 75258e0d-600d-4a3d-94f4-3d7ac12cb47c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 92e755053d3519212c27fd2567610baf189db309
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069362"
---
# <a name="solution-user-options-suo-file"></a>ソリューション ユーザー オプション (.Suo) ファイル
ソリューションユーザーオプション (.suo) ファイルには、ユーザーごとのソリューションオプションが含まれています。 このファイルをソースコード管理にチェックインしないでください。

 ソリューションユーザーオプション (.suo) ファイルは、バイナリ形式で格納された構造化ストレージ (複合ファイル) です。 ユーザー情報をストリームに保存します。ストリームの名前は、.suo ファイル内の情報を識別するために使用されるキーです。 ソリューションユーザーオプションファイルは、ユーザー設定を保存するために使用され、Visual Studio がソリューションを保存するときに自動的に作成されます。

 環境で .suo ファイルが開かれると、現在読み込まれているすべての Vspackage が列挙されます。 VSPackage がインターフェイスを実装している場合、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts> 環境は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.LoadUserOptions%2A> .suo ファイルからすべてのデータを読み込むように求める VSPackage のメソッドを呼び出します。

 VSPackage は、.suo ファイルに書き込まれたストリームを知る必要があります。 VSPackage は、書き込まれたストリームごとに、を介して環境にコールバックし、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.LoadPackageUserOpts%2A> キーによって識別される特定のストリーム (ストリームの名前) を読み込みます。 次に、環境は VSPackage にコールバックし、ストリームの名前とメソッドへのポインターを渡す特定のストリームを読み取り `IStream` <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.LoadPackageUserOpts%2A> ます。

 その時点で、もう1つの呼び出しが行われ、 `LoadUserOptions` .suo ファイルの別のセクションに読み取る必要があるかどうかが確認されます。 このプロセスは、.suo ファイル内のすべてのデータストリームが環境によって読み取られ、処理されるまで続きます。

 ソリューションが保存または閉じられると、環境はメソッド <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.SavePackageSolutionProps%2A> へのポインターを使用してメソッドを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.SaveUserOptions%2A> ます。 `IStream`保存するバイナリ情報を格納しているは、メソッドに渡され <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.WriteUserOptions%2A> ます。このメソッドは、.suo ファイルに情報を書き込み、もう一度メソッドを呼び出して、 `SaveUserOptions` .suo ファイルに書き込む情報の別のストリームがあるかどうかを確認します。

 これらの2つのメソッド ( `SaveUserOptions` と `WriteUserOptions` ) は、.suo ファイルに保存される情報のストリームごとに再帰的に呼び出され、へのポインターを渡し `IVsSolutionPersistence` ます。 これらは再帰的に呼び出され、.suo ファイルへの複数のストリームの書き込みを可能にします。 このようにすると、ユーザー情報はソリューションと共に保持され、次にソリューションを開いたときに確実に表示されます。

## <a name="see-also"></a>こちらもご覧ください
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>
- [ソリューション](../../extensibility/internals/solutions-overview.md)
