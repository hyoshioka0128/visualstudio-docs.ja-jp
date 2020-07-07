---
title: '方法: SharePoint プロジェクトの拡張機能を作成する |Microsoft Docs'
ms.date: 04/28/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- projects [SharePoint development in Visual Studio], extending
- SharePoint development in Visual Studio, extending projects
- SharePoint projects, extending
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 191f5d718064a4e094a2c28e3f584168b20fb3fc
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86017154"
---
# <a name="how-to-create-a-sharepoint-project-extension"></a>方法: SharePoint プロジェクトの拡張機能を作成する
  Visual Studio で開いている SharePoint プロジェクトに機能を追加する場合は、プロジェクトの拡張機能を作成します。 詳細については、「 [SharePoint プロジェクトシステムの拡張](../sharepoint/extending-the-sharepoint-project-system.md)」を参照してください。

### <a name="to-create-a-project-extension"></a>プロジェクトの拡張機能を作成するには

1. クラス ライブラリ プロジェクトを作成します。

2. 次のアセンブリへの参照を追加します。

    - Microsoft.VisualStudio.SharePoint

    - System.ComponentModel.Composition

3. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> インターフェイスを実装するクラスを作成します。

4. <xref:System.ComponentModel.Composition.ExportAttribute>をクラスに追加します。 この属性を使用すると、Visual Studio で実装を検出して読み込むことができ <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> ます。 型を <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 属性コンストラクターに渡します。

5. メソッドの実装では <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A> 、 *projectservice*パラメーターのメンバーを使用して拡張機能の動作を定義します。 このパラメーターは、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> インターフェイスで定義されたイベントへのアクセスを提供するオブジェクトです <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents> 。

## <a name="example"></a>例
 次のコード例は、インターフェイスで定義されているほとんどの SharePoint プロジェクトイベントを処理する単純なプロジェクト拡張機能を作成する方法を示して <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents> います。 コードをテストするには、で SharePoint プロジェクトを作成 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] し、ソリューションにプロジェクトを追加するか、プロジェクトプロパティの値を変更するか、プロジェクトを削除または除外します。 拡張機能は、[**出力**] ウィンドウと [**エラー一覧**] ウィンドウにメッセージを書き込むことによって、イベントを通知します。

  ```vb
    Imports Microsoft.VisualStudio.SharePoint
    Imports System.ComponentModel
    Imports System.ComponentModel.Composition

    Namespace Contoso.ExampleProjectExtension
      <Export(GetType(ISharePointProjectExtension))> _
      Class ExampleProjectExtension
        Implements ISharePointProjectExtension

        Private WithEvents projectService As ISharePointProjectService

        Public Sub Initialize(ByVal projectService As ISharePointProjectService) _
            Implements ISharePointProjectExtension.Initialize
            Me.projectService = projectService
        End Sub

        ' A project was added.
        Private Sub projectService_ProjectAdded(ByVal sender As Object, ByVal e As SharePointProjectEventArgs) _
            Handles projectService.ProjectAdded
            Dim project As ISharePointProject = CType(sender, ISharePointProject)
            Dim message As String = String.Format("The following project was added: {0}", e.Project.Name)
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message)
        End Sub

        ' A project was loaded in the IDE.
        Private Sub projectService_ProjectInitialized(ByVal sender As Object, ByVal e As SharePointProjectEventArgs) _
            Handles projectService.ProjectInitialized
            Dim project As ISharePointProject = CType(sender, ISharePointProject)
            Dim message As String = String.Format("The following project is being initialized: {0}", e.Project.Name)
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message)
        End Sub

        ' The name of a property was changed.
        Private Sub projectService_ProjectNameChanged(ByVal sender As Object, ByVal e As NameChangedEventArgs) _
            Handles projectService.ProjectNameChanged
            Dim project As ISharePointProject = CType(sender, ISharePointProject)
            Dim message As String = String.Format("The project named {0} was changed to {1}.", e.OldName, project.Name)
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message)
        End Sub

        ' A project property value was changed.
        Private Sub ProjectPropertyChanged(ByVal sender As Object, ByVal e As PropertyChangedEventArgs) _
            Handles projectService.ProjectPropertyChanged
            Dim project As ISharePointProject = CType(sender, ISharePointProject)
            Dim message As String = String.Format("The following property of the {0} project was changed: {1}",
                project.Name, e.PropertyName)
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message)
        End Sub

        ' A project is being removed or unloaded.
        Private Sub projectService_ProjectRemoved(ByVal sender As Object, ByVal e As SharePointProjectEventArgs) _
            Handles projectService.ProjectRemoved
            Dim project As ISharePointProject = CType(sender, ISharePointProject)
            Dim message As String = String.Format("The following project is being removed or unloaded: {0}", e.Project.Name)
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message)
        End Sub

        ' A project was removed or unloaded.
        Private Sub projectService_ProjectDisposing(ByVal sender As Object, ByVal e As SharePointProjectEventArgs) _
            Handles projectService.ProjectDisposing
            Dim project As ISharePointProject = CType(sender, ISharePointProject)
            Dim message As String = String.Format("The following project was removed or unloaded: {0}", e.Project.Name)
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message)
        End Sub
      End Class
    End Namespace
    ```

    ```csharp
    using Microsoft.VisualStudio.SharePoint;
    using System;
    using System.ComponentModel;
    using System.ComponentModel.Composition;

    namespace Contoso.ExampleProjectExtension
    {
      [Export(typeof(ISharePointProjectExtension))]
      internal class ExampleProjectExtension : ISharePointProjectExtension
      {
        public void Initialize(ISharePointProjectService projectService)
        {
            projectService.ProjectAdded += projectService_ProjectAdded;
            projectService.ProjectInitialized += projectService_ProjectInitialized;
            projectService.ProjectNameChanged += projectService_ProjectNameChanged;
            projectService.ProjectPropertyChanged += projectService_ProjectPropertyChanged;
            projectService.ProjectRemoved += projectService_ProjectRemoved;
            projectService.ProjectDisposing += projectService_ProjectDisposing;
        }

        // A project was added.
        void projectService_ProjectAdded(object sender, SharePointProjectEventArgs e)
        {
            ISharePointProject project = (ISharePointProject)sender;
            string message = String.Format("The following project was added: {0}", e.Project.Name);
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message);
        }

        // A project is loaded in the IDE.
        void projectService_ProjectInitialized(object sender, SharePointProjectEventArgs e)
        {
            ISharePointProject project = (ISharePointProject)sender;
            string message = String.Format("The following project is being initialized: {0}", e.Project.Name);
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message);
        }

        // The name of a project was changed.
        void projectService_ProjectNameChanged(object sender, NameChangedEventArgs e)
        {
            ISharePointProject project = (ISharePointProject)sender;
            string message = String.Format("The project named {0} was changed to {1}.", e.OldName, project.Name);
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message);
        }

        // A project property value was changed.
        private void projectService_ProjectPropertyChanged(object sender, PropertyChangedEventArgs e)
        {
            ISharePointProject project = (ISharePointProject)sender;
            string message = String.Format("The following property of the {0} project was changed: {1}",
                project.Name, e.PropertyName);
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message);
        }

        // A project is being removed or unloaded.
        void projectService_ProjectRemoved(object sender, SharePointProjectEventArgs e)
        {
            ISharePointProject project = (ISharePointProject)sender;
            string message = String.Format("The following project is being removed or unloaded: {0}", e.Project.Name);
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message);
        }

        // A project was removed or unloaded.
        void projectService_ProjectDisposing(object sender, SharePointProjectEventArgs e)
        {
            ISharePointProject project = (ISharePointProject)sender;
            string message = String.Format("The following project was removed or unloaded: {0}", e.Project.Name);
            project.ProjectService.Logger.WriteLine(message, LogCategory.Message);
        }
     }
  }
  ```

この例では、SharePoint プロジェクトサービスを使用して、メッセージを [**出力**] ウィンドウと [**エラー一覧**] ウィンドウに書き込みます。 詳細については、「 [SharePoint プロジェクトサービスの使用](../sharepoint/using-the-sharepoint-project-service.md)」を参照してください。

 イベントとイベントの処理方法を示す例につい <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectMenuItemsRequested> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectPropertiesRequested> ては、「[方法: ショートカットメニュー項目を Sharepoint プロジェクトに追加](../sharepoint/how-to-add-a-shortcut-menu-item-to-sharepoint-projects.md)する」および「[方法: Sharepoint プロジェクトにプロパティを追加](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)する」を参照してください。

## <a name="compile-the-code"></a>コードのコンパイル
 この例では、次のアセンブリへの参照が必要です。

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>拡張機能のデプロイ
 拡張機能を配置するには、 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] アセンブリおよび拡張機能と共に配布するその他のファイル用の拡張機能 (VSIX) パッケージを作成します。 詳細については、「 [Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクトシステムの拡張](../sharepoint/extending-the-sharepoint-project-system.md)
- [方法: ショートカットメニュー項目を SharePoint プロジェクトに追加する](../sharepoint/how-to-add-a-shortcut-menu-item-to-sharepoint-projects.md)
- [方法: SharePoint プロジェクトにプロパティを追加する](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
- [チュートリアル: SharePoint プロジェクト拡張機能の作成](../sharepoint/walkthrough-creating-a-sharepoint-project-extension.md)
