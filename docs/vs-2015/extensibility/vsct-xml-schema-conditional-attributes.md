---
title: VSCT XML スキーマの条件付き属性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, conditional attributes
- conditional attributes (VSCT XML schema)
ms.assetid: 754d4f32-319b-44c9-915f-f7c60e53222e
caps.latest.revision: 6
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6294ee8027b61840149096561efc91b8a4a3c3ec
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62422162"
---
# <a name="vsct-xml-schema-conditional-attributes"></a>VSCT XML スキーマの条件付き属性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

条件付き属性は、すべてのリストおよび項目に適用できます。 論理演算子と記号の展開式は、true または false に評価されます。 True の場合、関連付けられているリストまたは項目が結果の出力に含まれます。  
  
 トークンの展開は、他のトークンの展開または定数に対してテストできます。 関数 Defined () は、値がない場合でも、特定の名前が定義されているかどうかをテストするために使用されます。  
  
 条件属性がリストに適用されると、条件はリスト内のすべての子要素に適用されます。 子要素自体に Condition 属性が含まれている場合、その条件は AND 演算によって親式と結合されます。  
  
 値1、' 1 '、' true ' は true と評価され、0、' 0 '、および ' false ' が false と評価されます。  
  
## <a name="operators"></a>演算子  
 次の演算子は、条件式の評価に使用できます。  
  
|演算子|定義|  
|--------------|----------------|  
|(,)|グループ化|  
|!|論理 NOT|  
|\<, >, \<=, >=, ==, !=|関係と比較|  
|および|Boolean|  
|または|Boolean|  
  
## <a name="examples"></a>例  
  
```  
<Menu Condition="Defined(DEBUG)" …  
</Menu>  
  
<Menu Condition="%(SKU_MODE) = 'Demo'" …  
</Menu>  
  
<Menus Condition="Defined(DEBUG)">  
    <Menu …  
    </Menu>  
</Menus>  
  
<Menus Condition="Defined(DEMO_SKU)">  
    <Menus Condition="!Defined(DEBUG)">  
        <Menu …  
        </Menu>  
    </Menus>  
  
    <Menu …  
    </Menu>  
</Menus>  
  
<Menus Condition="(Defined(DEMO_SKU) or Defined(SAMPLE_SKU))   
and !Defined(DEBUG)">  
    <Menu …  
    </Menu>  
</Menus>  
```  
  
## <a name="see-also"></a>参照  
 [Visual Studio Command Table (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
