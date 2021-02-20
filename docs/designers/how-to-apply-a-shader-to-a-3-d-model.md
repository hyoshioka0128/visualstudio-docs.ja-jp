---
title: '方法: シェーダーを 3D モデルに適用する'
description: モデル エディターを使用して、Directed Graph Shader Language シェーダーを 3D モデルに適用して魅力的な外観にする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: a3877bd6-abd8-4a9d-842c-6848b6c2f335
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: bdaf4b86bfc773df678c03875a9ec260cd72084f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99917078"
---
# <a name="how-to-apply-a-shader-to-a-3d-model"></a>方法: シェーダーを 3D モデルに適用する

この記事では、モデル エディターを使用して、Directed Graph Shader Language (DGSL) シェーダーを 3D モデルに適用する方法を説明します。

## <a name="apply-a-shader-to-a-3d-model"></a>シェーダーを 3D モデルに適用する

シェーダー効果を 3D モデルに適用して、魅力的な外観にすることができます。

開始する前に、**[プロパティ]** ウィンドウが表示されていることを確認します。

1. まず 1 つ以上のモデルを含む 3D シーンを使用します。 適切な 3D シーンがない場合、「[方法:基本 3D モデルを作成する](../designers/how-to-create-a-basic-3-d-model.md)」に従って作成します。 また、モデルに適用できる DGSL シェーダーを使用する必要があります。 適切なシェーダーがない場合、「[方法: 基本カラー シェーダーを作成する](../designers/how-to-create-a-basic-color-shader.md)」に従って作成し、ファイルに保存してから続行してください。

2. **選択** モードで、シェーダーを適用するモデルを選択します。その後、**[プロパティ]** ウィンドウを開き、**効果** プロパティ グループの **Filename** プロパティで、モデルに適用する DGSL シェーダーを指定します。

基本色の効果を適用したモデルはこちらです。

![基本色の効果を表示する 3D シーン](../designers/media/digit-3d-model-effect.png)

シェーダーをモデルに適用した後、それをシェーダー デザイナーで開くには、モデルを選択します。その後、**[プロパティ]** ウィンドウを開き、**効果** プロパティ グループの **(詳細設定)** プロパティで省略記号 (**...**) ボタンを選択します。

## <a name="see-also"></a>関連項目

- [方法: 基本 3D モデルを作成する](../designers/how-to-create-a-basic-3-d-model.md)
- [方法: 基本カラー シェーダーを作成する](../designers/how-to-create-a-basic-color-shader.md)
- [モデル エディター](../designers/model-editor.md)
- [シェーダー デザイナー](../designers/shader-designer.md)
