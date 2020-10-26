---
title: BscMake タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- vc.task.bscmake
- VC.Project.VCBscMakeTool.PreserveSBR
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBuild (Visual C++), tasks
- BscMake task (MSBuild (Visual C++))
ms.assetid: bb98fc67-cad8-43a7-9598-60df6d734db2
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7ed246255fc20b9660d24f234767fdeb451102f8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65684545"
---
# <a name="bscmake-task"></a>BscMake タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

重要]
> Visual Studio IDE では、bscmake は使用されなくなりました。 Visual Studio 2008 以降、ブラウザー情報は、ソリューション フォルダーの sdf ファイルに自動的に格納されます。  
  
 Microsoft Browse Information Maintenance Utility ツール (bscmake.exe) をラップします。  bscmake.exe ツールは、コンパイル時に作成されるソース ブラウザー ファイル (.sbr) からブラウザー情報ファイル (.bsc) をビルドします。 .bsc ファイルを表示するには、**オブジェクト ブラウザー**を使用します。 詳細については、「 [BSCMAKE リファレンス](https://msdn.microsoft.com/library/b97ad994-1355-4809-98db-6abc12c6fb13)」を参照してください。  
  
## <a name="parameters"></a>パラメーター  
 **BscMake** タスクのパラメーターの説明を次の表に示します。 タスク パラメーターの大部分は、コマンド ライン オプションに対応します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|**AdditionalOptions**|省略可能な **文字列** パラメーターです。<br /><br /> コマンド ラインで指定するオプションのリストです。 たとえば、"/*オプション 1*  / *option2*  / *option #*" のように指定します。 他の **BscMake** タスク パラメーターでは表されないオプションを指定する場合は、このパラメーターを使用します。<br /><br /> 詳細については、「 [BSCMAKE オプション](https://msdn.microsoft.com/library/fa2f1e06-c684-41cf-80dd-6a554835ebd2)」のオプションを参照してください。|  
|**OutputFile**|省略可能な **文字列** パラメーターです。<br /><br /> 既定の出力ファイル名をオーバーライドするファイル名を指定します。<br /><br /> 詳細については、「 [BSCMAKE オプション](https://msdn.microsoft.com/library/fa2f1e06-c684-41cf-80dd-6a554835ebd2)」の「 **/o**オプション」を参照してください。|  
|**PreserveSBR**|省略可能な **ブール型** パラメーターです。<br /><br /> `true` の場合、ノンインクリメンタル ビルドを強制的に実行します。 フル ノンインクリメンタル ビルドは .bsc ファイルが存在するかどうかに関係なく実行され、.sbr ファイルの切り詰めは行われません。<br /><br /> 詳細については、「 [BSCMAKE オプション](https://msdn.microsoft.com/library/fa2f1e06-c684-41cf-80dd-6a554835ebd2)」の **/n**オプションを参照してください。|  
|**Sources**|省略可能な **microsoft.build.framework.itaskitem> 型 []** パラメーター。<br /><br /> タスクで使用および生成できる MSBuild ソース ファイル アイテムの配列を定義します。|  
|**SuppressStartupBanner**|省略可能な **ブール型** パラメーターです。<br /><br /> `true` の場合、タスクの開始時に著作権およびバージョン番号のメッセージが表示されないようにします。<br /><br /> 詳細については、「 [BSCMAKE オプション](https://msdn.microsoft.com/library/fa2f1e06-c684-41cf-80dd-6a554835ebd2)」の **/nologo**オプションを参照してください。|  
|**TrackerLogDirectory**|省略可能な **文字列** パラメーターです。<br /><br /> トラッカー ログのディレクトリを指定します。|  
  
## <a name="remarks"></a>注釈  
  
## <a name="see-also"></a>参照  
 [タスクリファレンス](../msbuild/msbuild-task-reference.md)
