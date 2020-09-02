---
title: ソリューションユーザーオプション (..Suo) File |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- .suo files, VSPackages
- suo files, VSPackages
- solutions, .suo files
- solutions, user options
- solution user options (.suo) file
ms.assetid: 75258e0d-600d-4a3d-94f4-3d7ac12cb47c
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1a9825fabe08940e8950cf88a1dbf2bc149af0b2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68197340"
---
# <a name="solution-user-options-suo-file"></a>ソリューション ユーザー オプション (.Suo) ファイル
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ソリューションユーザーオプション (.suo) ファイルには、ユーザーごとのソリューションオプションが含まれています。 このファイルをソースコード管理にチェックインしないでください。  
  
 ソリューションユーザーオプション (.suo) ファイルは、バイナリ形式で格納された構造化ストレージ (複合ファイル) です。 ユーザー情報をストリームに保存します。ストリームの名前は、.suo ファイル内の情報を識別するために使用されるキーです。 ソリューションユーザーオプションファイルは、ユーザー設定を保存するために使用され、Visual Studio がソリューションを保存するときに自動的に作成されます。  
  
 環境で .suo ファイルが開かれると、現在読み込まれているすべての Vspackage が列挙されます。 VSPackage がインターフェイスを実装している場合、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts> 環境は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.LoadUserOptions%2A> .suo ファイルからすべてのデータを読み込むように求める VSPackage のメソッドを呼び出します。  
  
 VSPackage は、.suo ファイルに書き込まれたストリームを知る必要があります。 VSPackage は、書き込まれたストリームごとに、を介して環境にコールバックし、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.LoadPackageUserOpts%2A> キーによって識別される特定のストリーム (ストリームの名前) を読み込みます。 次に、環境は VSPackage にコールバックし、ストリームの名前とメソッドへのポインターを渡す特定のストリームを読み取り `IStream` <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.LoadPackageUserOpts%2A> ます。  
  
 その時点で、もう1つの呼び出しが行われ、 `LoadUserOptions` .suo ファイルの別のセクションに読み取る必要があるかどうかが確認されます。 このプロセスは、.suo ファイル内のすべてのデータストリームが環境によって読み取られ、処理されるまで続きます。  
  
 ソリューションが保存または閉じられると、環境はメソッド <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.SavePackageSolutionProps%2A> へのポインターを使用してメソッドを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.SaveUserOptions%2A> ます。 `IStream`保存するバイナリ情報を格納しているは、メソッドに渡され <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.WriteUserOptions%2A> ます。このメソッドは、.suo ファイルに情報を書き込み、もう一度メソッドを呼び出して、 `SaveUserOptions` .suo ファイルに書き込む情報の別のストリームがあるかどうかを確認します。  
  
 これらの2つのメソッド ( `SaveUserOptions` と `WriteUserOptions` ) は、.suo ファイルに保存される情報のストリームごとに再帰的に呼び出され、へのポインターを渡し `IVsSolutionPersistence` ます。 これらは再帰的に呼び出され、.suo ファイルへの複数のストリームの書き込みを可能にします。 このようにすると、ユーザー情報はソリューションと共に保持され、次にソリューションを開いたときに確実に表示されます。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>   
 [ソリューション](../../extensibility/internals/solutions-overview.md)
