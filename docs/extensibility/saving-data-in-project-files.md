---
title: プロジェクトファイルへのデータの保存 |Microsoft Docs
description: プロジェクトファイル内のサブタイプ固有のデータを保存および取得するために、マネージパッケージフレームワークによって提供されるインターフェイスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- data [Visual Studio], saving in project files
- project files
- project files, saving data
ms.assetid: a3d4b15b-a91e-41ba-b235-e62632d11bc5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4746ebb4a92d5c2688063336cb3772de8d72ee1b
ms.sourcegitcommit: 94a57a7bda3601b83949e710a5ca779c709a6a4e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/21/2020
ms.locfileid: "97715692"
---
# <a name="save-data-in-project-files"></a>プロジェクトファイルにデータを保存する
プロジェクトのサブタイプは、プロジェクトファイル内のサブタイプ固有のデータを保存および取得できます。 Managed Package Framework (MPF) には、このタスクを実行するための2つのインターフェイスが用意されています。

- インターフェイスは、が <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> プロジェクトファイルの **MSBuild** セクションからプロパティ値にアクセスできるようにします。 によって提供されるメソッドは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> ユーザーがビルド関連のデータを読み込んだり保存したりする必要があるときに、任意のユーザーが呼び出すことができます。

- は、 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> ビルドに関連しないデータを自由形式の XML で保持するために使用されます。 によって提供されるメソッド <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> は、 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] がビルド以外の関連データをプロジェクトファイルに保持する必要がある場合に、によって呼び出されます。

  ビルドおよびビルドに関連しないデータを保持する方法の詳細については、「 [MSBuild プロジェクトファイルのデータを保持](../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)する」を参照してください。

## <a name="save-and-retrieve-build-related-data"></a>ビルド関連データを保存および取得する

### <a name="to-save-a-build-related-data-in-the-project-file"></a>ビルド関連のデータをプロジェクトファイルに保存するには

- メソッドを呼び出して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetPropertyValue%2A> プロジェクトファイルの完全パスを保存します。

    ```
    private SpecializedProject project;
    IVsBuildPropertyStorage projectStorage = (IVsBuildPropertyStorage)project;
    string newFullPath = GetNewFullPath();
    // Set a full path of the project file.
    ErrorHandler.ThrowOnFailure(projectStorage.SetPropertyValue(
        "MSBuildProjectDirectory",
        String.Empty,
        (uint)_PersistStorageType.PST_PROJECT_FILE, newFullPath));
    ```

### <a name="to-retrieve-build-related-data-from-the-project-file"></a>プロジェクトファイルからビルド関連のデータを取得するには

- メソッドを呼び出して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.GetPropertyValue%2A> プロジェクトファイルの完全パスを取得します。

    ```
    private SpecializedProject project;
    IVsBuildPropertyStorage projectStorage = (IVsBuildPropertyStorage)project;
    string fullPath;
    // Get a full path of the project file.
    ErrorHandler.ThrowOnFailure(projectStorage.GetPropertyValue(
        "MSBuildProjectDirectory",
        String.Empty,
        (uint)_PersistStorageType.PST_PROJECT_FILE, out fullPath));
    ```

## <a name="save-and-retrieve-non-build-related-data"></a>ビルド以外のデータを保存および取得する

### <a name="to-save-non-build-related-data-in-the-project-file"></a>ビルドに関連しないデータをプロジェクトファイルに保存するには

1. メソッドを実装し <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.IsFragmentDirty%2A> て、XML フラグメントが現在のファイルに最後に保存されてから変更されたかどうかを確認します。

    ```
    public int IsFragmentDirty(uint storage, out int pfDirty)
    {
        pfDirty = 0;
        switch (storage)
        {
            case (uint)_PersistStorageType.PST_PROJECT_FILE:
            {
                if (isDirty)
                    pfDirty |= 1;
                break;
            }
            case (uint)_PersistStorageType.PST_USER_FILE:
            {
                // We do not store anything in the user file.
                break;
            }
        }

        // Forward the call to inner flavor(s)
        if (pfDirty == 0 && innerCfg != null && this.innerCfg is IPersistXMLFragment)
            return ((IPersistXMLFragment)this.innerCfg).IsFragmentDirty(storage, out pfDirty);

        return VSConstants.S_OK;

    }
    ```

2. <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Save%2A>XML データをプロジェクトファイルに保存するには、メソッドを実装します。

    ```
    public int Save(ref Guid guidFlavor, uint storage, out string pbstrXMLFragment, int fClearDirty)
    {
        pbstrXMLFragment = null;

        if (IsMyFlavorGuid(ref guidFlavor))
        {
            switch (storage)
            {
                case (uint)_PersistStorageType.PST_PROJECT_FILE:
                {
                    // Create XML for our data.
                    XmlDocument doc = new XmlDocument();
                    XmlNode root = doc.CreateElement(this.GetType().Name);

                    XmlNode node = doc.CreateElement(targetsTag);
                    node.AppendChild(doc.CreateTextNode(this.TargetsToExecute));
                    root.AppendChild(node);

                    node = doc.CreateElement(updateTargetsTag);
                    node.AppendChild(doc.CreateTextNode(this.UpdateTargetList.ToString()));
                    root.AppendChild(node);

                    doc.AppendChild(root);
                    // Get XML fragment representing our data
                    pbstrXMLFragment = doc.InnerXml;

                    if (fClearDirty != 0)
                        isDirty = false;
                    break;
                }
                case (uint)_PersistStorageType.PST_USER_FILE:
                {
                    // We do not store anything in the user file.
                    break;
                }
            }
        }

        // Forward the call to inner flavor(s)
        if (this.innerCfg != null && this.innerCfg is IPersistXMLFragment)
            return ((IPersistXMLFragment)this.innerCfg).Save(ref guidFlavor, storage, out pbstrXMLFragment, fClearDirty);

        return VSConstants.S_OK;
    }
    ```

### <a name="to-retrieve-non-build-related-data-in-the-project-file"></a>プロジェクトファイル内のビルド以外の関連データを取得するには

1. メソッドを実装して、 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.InitNew%2A> プロジェクトの拡張プロパティとその他のビルドに依存しないデータを初期化します。 このメソッドは、プロジェクトファイルに XML 構成データが存在しない場合に呼び出されます。

    ```
    public int InitNew(ref Guid guidFlavor, uint storage)
    {
        //Return,if it is our guid.
        if (IsMyFlavorGuid(ref guidFlavor))
            return VSConstants.S_OK;

        //Forward the call to inner flavor(s).
        if (this.innerCfg != null && this.innerCfg is IPersistXMLFragment)
            return ((IPersistXMLFragment)this.innerCfg).InitNew(ref guidFlavor, storage);

        return VSConstants.S_OK;
    ```

2. <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Load%2A>プロジェクトファイルから XML データを読み込むメソッドを実装します。

    ```
    public int Load(ref Guid guidFlavor, uint storage, string pszXMLFragment)
    {
        if (IsMyFlavorGuid(ref guidFlavor))
        {
            switch (storage)
            {
                case (uint)_PersistStorageType.PST_PROJECT_FILE:
                {
                    // Load our data from the XML fragment.
                    XmlDocument doc = new XmlDocument();
                    XmlNode node = doc.CreateElement(this.GetType().Name);
                    node.InnerXml = pszXMLFragment;
                    if (node == null
                        || node.FirstChild == null
                        || node.FirstChild.ChildNodes.Count == 0
                        || node.FirstChild.ChildNodes[0].Name != targetsTag)
                        break;
                    this.TargetsToExecute = node.FirstChild.ChildNodes[0].InnerText;

                    if (node.FirstChild.ChildNodes.Count <= 1
                        || node.FirstChild.ChildNodes[1].Name != updateTargetsTag)
                        break;
                    this.UpdateTargetList = bool.Parse(node.FirstChild.ChildNodes[1].InnerText);
                    break;
                }
                case (uint)_PersistStorageType.PST_USER_FILE:
                {
                    // We do not store anything in the user file.
                    break;
                }
            }
        }

        // Forward the call to inner flavor(s)
        if (this.innerCfg != null && this.innerCfg is IPersistXMLFragment)
            return ((IPersistXMLFragment)this.innerCfg).Load(ref guidFlavor, storage, pszXMLFragment);

        return VSConstants.S_OK;
    }
    ```

> [!NOTE]
> このトピックで説明するすべてのコード例は、 [Vssdk サンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)の大きな例の一部です。

## <a name="see-also"></a>関連項目
- [MSBuild プロジェクトファイルのデータを保持する](../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)
