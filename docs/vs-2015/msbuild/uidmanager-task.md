---
title: UidManager タスク | Microsoft Docs
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
- UidManager task [WPF MSBuild]
- UidManager task [WPF MSBuild], parameters
- managing UIDs when localizing XAML elements [WPF MSBuild]
- localizing XAML elements [WPF MSBuild], managing UIDs
- checking UIDs when localizing XAML elements [WPF MSBuild]
ms.assetid: 4fc7b5a5-11b0-46ca-9656-8c2a0b08d1fe
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5fd8175911def7fb1b63dc63d967c404d649e9e4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65703690"
---
# <a name="uidmanager-task"></a>UidManager タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

<xref:Microsoft.Build.Tasks.Windows.UidManager> タスクでは、ソース [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] ファイルに含まれるすべての [!INCLUDE[TLA#tla_xaml](../includes/tlasharptla-xaml-md.md)] 要素をローカライズするために、一意識別子 (UID) をチェック、更新、または削除します。  
  
## <a name="task-parameters"></a>タスク パラメーター  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`IntermediateDirectory`|省略可能な **String** 型のパラメーターです。<br /><br /> **MarkupFiles** パラメーターで指定されるソース [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] ファイルをバックアップするために使用されるディレクトリを指定します。|  
|`MarkupFiles`|必須の **ITaskItem[]** 型のパラメーターです。<br /><br /> UID のチェック、更新、または削除の対象となるソース [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] ファイルを指定します。|  
|`Task`|必須の **String** 型のパラメーターです。<br /><br /> 実行する UID 管理タスクを指定します。 有効なオプションは **Check**、**Update**、または **Remove** です。|  
  
## <a name="example"></a>例  
 次の例では <xref:Microsoft.Build.Tasks.Windows.UidManager> タスクを使用して、指定されたソース [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] ファイルに、適切な UID を持つ [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] 要素が含まれていることをチェックします。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <UsingTask   
    TaskName="Microsoft.Build.Tasks.Windows.UidManager"   
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />  
  <Target Name="UidManagerTask">  
    <UidManager  
      Task="Check"  
      MarkupFiles="Page1.xaml;Page2.xaml"  
      IntermediateDirectory="c:\UidManagerIntermediateDirectory" />  
  </Target>  
</Project>  
```  
  
## <a name="see-also"></a>参照  
 [WPF MSBuild リファレンス](../msbuild/wpf-msbuild-reference.md)   
 [タスクリファレンス](../msbuild/wpf-msbuild-task-reference.md)   
 [MSBuild リファレンス](../msbuild/msbuild-reference.md)   
 [タスクリファレンス](../msbuild/msbuild-task-reference.md)   
 [WPF アプリケーションのビルド (WPF)](https://msdn.microsoft.com/library/a58696fd-bdad-4b55-9759-136dfdf8b91c)   
 [方法: アプリケーションをローカライズする](https://msdn.microsoft.com/library/5001227e-9326-48a4-9dcd-ba1b89ee6653)
