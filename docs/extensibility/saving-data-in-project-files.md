---
title: プロジェクト ファイルへのデータの保存 |マイクロソフトドキュメント
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
ms.openlocfilehash: 5fd6cfaa450bc268665ae0f58109c99002da6152
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701353"
---
# <a name="save-data-in-project-files"></a>プロジェクト ファイルにデータを保存する
プロジェクト サブタイプは、プロジェクト ファイル内のサブタイプ固有のデータを保存および取得できます。 管理パッケージ フレームワーク (MPF) には、このタスクを実行するための 2 つのインターフェイスが用意されています。

- インターフェイス<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>は、プロジェクト ファイルの**MSBuild**セクションからプロパティ値にアクセスできます。 提供されるメソッドは<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>、ビルド関連データを読み込んだり保存したりする必要があるときはいつでも、どのユーザーからでも呼び出すことができます。

- <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>は、ビルド以外の関連データを自由形式 XML で永続化するために使用されます。 によって<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>提供されるメソッドは、プロジェクト[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)][!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]ファイルにビルド関連以外のデータを保持する必要がある場合に呼び出されます。

  ビルドとビルド以外の関連データを永続化する方法の詳細については、「 [MSBuild プロジェクト ファイルにデータを保持する](../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)」を参照してください。

## <a name="save-and-retrieve-build-related-data"></a>ビルド関連データの保存と取得

### <a name="to-save-a-build-related-data-in-the-project-file"></a>ビルド関連のデータをプロジェクト ファイルに保存するには

- プロジェクト<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetPropertyValue%2A>ファイルの完全パスを保存するには、メソッドを呼び出します。

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

### <a name="to-retrieve-build-related-data-from-the-project-file"></a>プロジェクト ファイルからビルド関連のデータを取得するには

- プロジェクト<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.GetPropertyValue%2A>ファイルの完全パスを取得するには、メソッドを呼び出します。

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

## <a name="save-and-retrieve-non-build-related-data"></a>ビルド以外の関連データを保存および取得する

### <a name="to-save-non-build-related-data-in-the-project-file"></a>ビルド以外の関連データをプロジェクト ファイルに保存するには

1. XML<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.IsFragmentDirty%2A>フラグメントが最後に現在のファイルに保存されてから変更されたかどうかを判断するメソッドを実装します。

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

2. プロジェクト<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Save%2A>ファイルに XML データを保存するメソッドを実装します。

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

### <a name="to-retrieve-non-build-related-data-in-the-project-file"></a>ビルド以外の関連データをプロジェクト ファイルから取得するには

1. プロジェクト拡張機能<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.InitNew%2A>のプロパティおよびその他のビルドに依存しないデータを初期化するメソッドを実装します。 プロジェクト ファイルに XML 構成データが存在しない場合、このメソッドが呼び出されます。

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

2. プロジェクト<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Load%2A>ファイルから XML データを読み込むメソッドを実装します。

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
> このトピックで提供されるすべてのコード例は、 [VSSDK サンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)の大きな例の一部です。

## <a name="see-also"></a>関連項目
- [MSBuild プロジェクト ファイルにデータを保存する](../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)
