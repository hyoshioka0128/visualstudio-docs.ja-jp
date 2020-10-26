---
title: Visual C++ に固有の MSBuild タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, tasks specific to Visual C++
ms.assetid: 05410f0c-7356-4692-bc00-20664421c9ff
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 452c3b408ab6471963124e61bc803e99eb6be80d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65686904"
---
# <a name="msbuild-tasks-specific-to-visual-c"></a>Visual C++ に固有の MSBuild タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

タスクでは、ビルド プロセスの間に実行するコードを指定します。 Visual C++ をインストールすると、次のタスクは [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] にインストールされたタスク以外に使用できます。 詳細については、「[MSBuild (Visual C++) の概要](https://msdn.microsoft.com/library/dd258f6f-ab51-48d9-b274-f7ba911d05ca)」を参照してください。  
  
 タスクごとのパラメーターのほか、すべてのタスクに以下のパラメーターがあります。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`Condition`|省略可能な `String` 型のパラメーターです。<br /><br /> このタスクが実行されるかどうかを [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] エンジンが決定するために使用する `Boolean` 式です。 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] でサポートされる条件の詳細については、「[MSBuild Conditions](../msbuild/msbuild-conditions.md)」(MSBuild の条件) を参照してください。|  
|`ContinueOnError`|省略可能なパラメーターです。 次の値のいずれかを含めることができます。<br /><br /> -   **WarnAndContinue** または **true**。 タスクが失敗すると、[Target](../msbuild/target-element-msbuild.md) 要素の後続のタスクとビルドの実行が継続し、タスクのすべてのエラーが警告として扱われます。<br />-   **ErrorAndContinue**。 タスクが失敗すると、`Target` 要素の後続のタスクとビルドの実行が継続し、タスクのすべてのエラーがエラーとして扱われます。<br />-   **ErrorAndStop** または **false** (既定)。 タスクが失敗すると、`Target` 要素の残りのタスクとビルドは実行されず、`Target` 要素全体とビルドは失敗したと見なされます。<br /><br /> バージョン 4.5 より前の .NET Framework では、`true` 値と `false` 値のみがサポートされます。<br /><br /> 詳細については、「[方法: タスクで発生したエラーを無視する](../msbuild/how-to-ignore-errors-in-tasks.md)」を参照してください。|  
  
## <a name="related-topics"></a>関連トピック  
  
|Title|説明|  
|-----------|-----------------|  
|[BscMake タスク](../msbuild/bscmake-task.md)|Microsoft Browse Information Maintenance Utility ツール (bscmake.exe) をラップします。|  
|[CL タスク](../msbuild/cl-task.md)|Visual C++ コンパイラ ツール (cl.exe) をラップします。|  
|[CPPClean タスク](../msbuild/cppclean-task.md)|Visual C++ プロジェクトのビルド時に MSBuild によって作成される一時ファイルを削除します。|  
|[LIB タスク](../msbuild/lib-task.md)|Microsoft 32-Bit Library Manager ツール (lib.exe) をラップします。|  
|[リンクタスク](../msbuild/link-task.md)|Visual C++ リンカー ツール (link.exe) をラップします。|  
|[MIDL タスク](../msbuild/midl-task.md)|Microsoft インターフェイス定義言語 (MIDL: Microsoft Interface Definition Language) コンパイラ ツール (midl.exe) をラップします。|  
|[MT タスク](../msbuild/mt-task.md)|Microsoft マニフェスト ツール (mt.exe) をラップします。|  
|[RC タスク](../msbuild/rc-task.md)|Microsoft Windows リソース コンパイラ ツール (rc.exe) をラップします。|  
|[SetEnv タスク](../msbuild/setenv-task.md)|指定された環境変数の値を設定または削除します。|  
|[VCMessage タスク](../msbuild/vcmessage-task.md)|ビルド時の警告メッセージおよびエラー メッセージをログに記録します。|  
|[XDCMake タスク](../msbuild/xdcmake-task.md)|XML ドキュメント ツール (xdcmake.exe) をラップします。このツールは、XML ドキュメント コメント (.xdc) ファイルを .xml ファイルにマージします。|  
|[XSD タスク](../msbuild/xsd-task.md)|ソースからスキーマまたはクラス ファイルを生成する XML スキーマ定義ツール (xsd.exe) をラップします。|  
|[MSBuild リファレンス](../msbuild/msbuild-reference.md)|MSBuild システムの要素について説明します。|  
|[タスク](../msbuild/msbuild-tasks.md)|タスクについて説明します。タスクはコードの単位であり、組み合わせることでビルドを生成できます。|  
|[タスクの作成](../msbuild/task-writing.md)|タスクを作成する方法を説明します。|
