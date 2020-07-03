---
title: プロパティページの追加と削除 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- property pages, adding
- property pages, project subtypes
- property pages, removing
ms.assetid: 34853412-ab8a-4caa-9601-7d0727b2985d
author: acangialosi
ms.author: anthc
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- vssdk
ms.openlocfilehash: fdc12f0938d3296cf1bfca37d0b9b01e0f2a704a
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903566"
---
# <a name="add-and-remove-property-pages"></a>プロパティページの追加と削除

プロジェクトデザイナーは、のプロジェクトプロパティ、設定、およびリソースを管理するための一元的な場所を提供し [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ます。 統合開発環境 (IDE: integrated development environment) には1つのウィンドウとして表示され、 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 左側のタブからアクセスできる、右側に多数のウィンドウがあります。 プロジェクトデザイナーのペイン (多くの場合、プロパティページと呼ばれます) は、プロジェクトの種類と言語によって異なります。 プロジェクトデザイナーは、[**プロジェクト**] メニューの [**プロパティ**] コマンドを使用してアクセスできます。

プロジェクトのサブタイプでは、プロジェクトデザイナーに追加のプロパティページを頻繁に表示する必要があります。 同様に、一部のプロジェクトのサブタイプでは、組み込みのプロパティページを削除する必要がある場合があります。 そのためには、プロジェクトのサブタイプがインターフェイスを実装し、メソッドをオーバーライドする必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> ます。 このメソッドをオーバーライドし、 `propId` 列挙体の値の1つを含むパラメーターを使用して、 <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> プロジェクトのプロパティをフィルター処理、追加、または削除できます。 たとえば、構成に依存するプロパティページにページを追加することが必要になる場合があります。 これを行うには、構成に依存するプロパティページをフィルター処理し、既存のリストに新しいページを追加する必要があります。

## <a name="add-and-remove-property-pages-in-project-designer"></a>プロジェクトデザイナーでのプロパティページの追加と削除

### <a name="remove-a-property-page"></a>プロパティページの削除

1. メソッドをオーバーライド `GetProperty(uint itemId, int propId, out object property)` して、プロパティページをフィルター処理し、リストを取得し `clsids` ます。

    ```vb
    Protected Overrides int GetProperty(uint itemId, int propId, out object property)
    Protected Overrides Function GetProperty(ByVal itemId As UInteger, ByVal propId As Integer, ByRef [property] As Object) As Integer
        'Use propId to filter configuration-independent property pages.
        Select Case propId
            ....
            Case CInt(Fix(__VSHPROPID2.VSHPROPID_PropertyPagesCLSIDList))
                'Get a semicolon-delimited list of clsids of the configuration-independent property pages
                ErrorHandler.ThrowOnFailure(MyBase.GetProperty(itemId, propId, [property]))
                   Dim propertyPagesList As String = ((String)[property]).ToUpper(CultureInfo.InvariantCulture)
                'Remove the property page here
                   ....
            ....
        End Select
            ....
        Return MyBase.GetProperty(itemId, propId, [property])
    End Function

    ```

    ```csharp
    protected override int GetProperty(uint itemId, int propId, out object property)
    {
        //Use propId to filter configuration-independent property pages.
        switch (propId)
        {
            . . . .

            case (int)__VSHPROPID2.VSHPROPID_PropertyPagesCLSIDList:
                {
                    //Get a semicolon-delimited list of clsids of the configuration-independent property pages
                    ErrorHandler.ThrowOnFailure(base.GetProperty(itemId, propId, out property));
                    string propertyPagesList = ((string)property).ToUpper(CultureInfo.InvariantCulture);
                    //Remove the property page here
                    . . . .
                }
             . . . .
         }
            . . . .
        return base.GetProperty(itemId, propId, out property);
    }
    ```

2. 取得したリストから [**ビルドイベント**] ページを削除し `clsids` ます。

    ```vb
    Private buildEventsPageGuid As String = "{1E78F8DB-6C07-4D61-A18F-7514010ABD56}"
    Private index As Integer = propertyPagesList.IndexOf(buildEventsPageGuid)
    If index <> -1 Then
        ' GUIDs are separated by ';' so if you remove the last GUID, also remove the last ';'
        Dim index2 As Integer = index + buildEventsPageGuid.Length + 1
        If index2 >= propertyPagesList.Length Then
            propertyPagesList = propertyPagesList.Substring(0, index).TrimEnd(";"c)
        Else
            propertyPagesList = propertyPagesList.Substring(0, index) + propertyPagesList.Substring(index2)
        End If
    End If
    'New property value
    property = propertyPagesList
    ```

    ```csharp
    string buildEventsPageGuid = "{1E78F8DB-6C07-4D61-A18F-7514010ABD56}";
    int index = propertyPagesList.IndexOf(buildEventsPageGuid);
    if (index != -1)
    {
        // GUIDs are separated by ';' so if you remove the last GUID, also remove the last ';'
        int index2 = index + buildEventsPageGuid.Length + 1;
        if (index2 >= propertyPagesList.Length)
            propertyPagesList = propertyPagesList.Substring(0, index).TrimEnd(';');
        else
            propertyPagesList = propertyPagesList.Substring(0, index) + propertyPagesList.Substring(index2);
    }
    //New property value
    property = propertyPagesList;
    ```

### <a name="add-a-property-page"></a>プロパティページの追加

1. 追加するプロパティページを作成します。

    ```vb
    Class DeployPropertyPage
            Inherits Form
            Implements Microsoft.VisualStudio.OLE.Interop.IPropertyPage
        'Summary: Return a stucture describing your property page.
        ....
        Public Sub GetPageInfo(ByVal pPageInfo As Microsoft.VisualStudio.OLE.Interop.PROPPAGEINFO())
            Dim info As PROPPAGEINFO = New PROPPAGEINFO()
            info.cb = CUInt(Marshal.SizeOf(GetType(PROPPAGEINFO)))
            info.dwHelpContext = 0
            info.pszDocString = Nothing
            info.pszHelpFile = Nothing
            info.pszTitle = "Deployment" 'Assign tab name
            info.SIZE.cx = Me.Size.Width
            info.SIZE.cy = Me.Size.Height
            If Not pPageInfo Is Nothing AndAlso pPageInfo.Length > 0 Then
                pPageInfo(0) = info
            End If
        End Sub
    End Class
    ```

    ```csharp
    class DeployPropertyPage : Form, Microsoft.VisualStudio.OLE.Interop.IPropertyPage
    {
        . . . .
        //Summary: Return a stucture describing your property page.
        public void GetPageInfo(Microsoft.VisualStudio.OLE.Interop.PROPPAGEINFO[] pPageInfo)
        {
            PROPPAGEINFO info = new PROPPAGEINFO();
            info.cb = (uint)Marshal.SizeOf(typeof(PROPPAGEINFO));
            info.dwHelpContext = 0;
            info.pszDocString = null;
            info.pszHelpFile = null;
            info.pszTitle = "Deployment";  //Assign tab name
            info.SIZE.cx = this.Size.Width;
            info.SIZE.cy = this.Size.Height;
            if (pPageInfo != null && pPageInfo.Length > 0)
                pPageInfo[0] = info;
        }
    }
    ```

2. 新しいプロパティページを登録します。

    ```vb
    <MSVSIP.ProvideObject(GetType(DeployPropertyPage), RegisterUsing = RegistrationMethod.CodeBase)>
    ```

    ```csharp
    [MSVSIP.ProvideObject(typeof(DeployPropertyPage), RegisterUsing = RegistrationMethod.CodeBase)]
    ```

3. `GetProperty(uint itemId, int propId, out object property)`プロパティページをフィルター処理したり、リストを取得 `clsids` したり、新しいプロパティページを追加したりするには、メソッドをオーバーライドします。

    ```vb
    Protected Overrides Function GetProperty(ByVal itemId As UInteger, ByVal propId As Integer, ByRef [property] As Object) As Integer
        'Use propId to filter configuration-dependent property pages.
        Select Case propId
            ....
            case CInt(Fix(__VSHPROPID2.VSHPROPID_CfgPropertyPagesCLSIDList)):
                'Get a semicolon-delimited list of clsids of the configuration-dependent property pages.
                ErrorHandler.ThrowOnFailure(MyBase.GetProperty(itemId, propId, [property]))
                'Add the Deployment property page.
                [property] &= ";"c + GetType(DeployPropertyPage).GUID.ToString("B")
        End Select
            ....
            Return MyBase.GetProperty(itemId, propId, [property])
    End Function
    ```

    ```csharp
    protected override int GetProperty(uint itemId, int propId, out object property)
    {
        //Use propId to filter configuration-dependent property pages.
        switch (propId)
        {
            . . . .
            case (int)__VSHPROPID2.VSHPROPID_CfgPropertyPagesCLSIDList:
                {
                    //Get a semicolon-delimited list of clsids of the configuration-dependent property pages.
                    ErrorHandler.ThrowOnFailure(base.GetProperty(itemId, propId, out property));
                    //Add the Deployment property page.
                    property += ';' + typeof(DeployPropertyPage).GUID.ToString("B");
                }
         }
            . . . .
        return base.GetProperty(itemId, propId, out property);
    }
    ```

## <a name="see-also"></a>関連項目

- [プロジェクトのサブタイプ](../extensibility/internals/project-subtypes.md)
