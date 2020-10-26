---
title: プロジェクト階層ノードの名前の変更 (C++) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- HierUtil7 sample [Visual Studio SDK], renaming project nodes
- project nodes, renaming in HierUtil7 sample
ms.assetid: cea5968e-e9f8-41a5-b068-622df542247c
caps.latest.revision: 12
manager: jillfra
ms.openlocfilehash: c7ad43fe1fd0e22cd94194d3079761de812b6ced
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65686583"
---
# <a name="renaming-project-hierarchy-nodes-c"></a>プロジェクト階層ノード (C++) の名前の変更
アンマネージ C++ の HierUtil7 プロジェクトフレームワークを使用して、プロジェクトフォルダー階層ノードの名前を変更できます。 詳細については、「 [HierUtil7 Sample](https://msdn.microsoft.com/29c15184-a70c-4813-86c2-fb1d47442d11)」を参照してください。  
  
## <a name="expanding-the-hierarchy-node"></a>階層ノードを展開する  
  
#### <a name="to-expand-the-hierarchy-node-and-rename-the-folder"></a>[階層] ノードを展開してフォルダーの名前を変更するには  
  
1. 次の方法を使用して、[階層] ノードを選択します。  
  
    ```  
    IfFailGo(pNode->ExtExpand(EXPF_SelectItem, GUID_MacroExplorer));  
    ```  
  
     `pNode` は、フォルダーに対応する階層コンテナーであり、 `EXPF_SelectItem` は <xref:Microsoft.VisualStudio.Shell.Interop.EXPANDFLAGS> 列挙体です。 `GUID_MacroExplorer`は、Vsshell .idl で定義されている GUID 定数であり、 `rguidPersistenceSlot` `ExtExpand` Hu_node で定義されているの関数シグネチャのの例です。  
  
    ```  
    HRESULT ExtExpand(EXPANDFLAGS expandflags, REFGUID rguidPersistenceSlot = GUID_SolutionExplorer) const;  
    ```  
  
     Files\VSIP ファイル Hu_node は、次のように EnvSDK\common\hierutil7 フォルダーに \<installation root> あります。  
  
2. を使用して名前の変更コマンドを投稿し、フォルダーの名前を変更します。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.PostExecCommand%2A>  
  
    ```  
    IfFailGo(srpVsUIShell->PostExecCommand(&guidVSStd97, cmdidRename, 0, NULL));  
    ```  
  
     `srpVsUIShell` は <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> ポインター `<IVsUIShell>``srpVsUIShell` です。 `guiVSStd97` は、コマンドが属するコマンドグループの一意の識別子で `cmdidRename` 、Vsshlids. h で定義されています。  
  
## <a name="see-also"></a>参照  
 [プロジェクトの種類の作成](../extensibility/internals/creating-project-types.md)   
 [VSSDK のサンプル](../misc/vssdk-samples.md)