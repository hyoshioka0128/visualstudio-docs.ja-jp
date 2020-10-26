---
title: UML モデル要素の種類 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML API, types
ms.assetid: 25345a53-7246-4eb7-8ad9-0b695aa171a2
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 54036b985c90be926eaa56f6ebe60d1f3903e0b2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72657324"
---
# <a name="uml-model-element-types"></a>UML モデル要素の型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

プログラミング インターフェイスによって UML モデルを読み取り、操作できます。 ここでは、要素型の階層構造について概説します。 階層構造は、UML 仕様で定義されているものと同じです。

 各型の詳細については、「 [API Reference FOR UML モデリング機能拡張](../modeling/api-reference-for-uml-modeling-extensibility.md)」を参照してください。

## <a name="element-types"></a>要素型
 これは、アセンブリ `Microsoft.VisualStudio.Uml.Interfaces.dll` で定義されている型のセットです。

 各項目の完全修飾名では、"`Microsoft.VisualStudio.Uml.`" の後に、リストされた名前が続きます。

 便宜上、このリストは継承階層として設定されています。 複数のスーパータイプを持つ型の場合は、コロン (:) の後に追加のスーパータイプが一覧表示されています。

```

Classes.IElement
|  Activities.IActivityGroup
|  Classes.IComment
|  Classes.IMultiplicityElement
|  |  CompositeStructures.IConnectorEnd
|  Classes.INamedElement
|  |  Deployments.IDeployedArtifact
|  |  Deployments.IDeploymentTarget
|  |  |  Classes.IInstanceSpecification
             : Deployments.IDeployedArtifact,
               Deployments.IDeploymentTarget
|  |  |  |  Classes.IEnumerationLiteral
|  |  Interactions.IInteractionFragment
|  |  |  Interactions.ICombinedFragment
|  |  |  |  Interactions.IConsiderIgnoreFragment
|  |  |  Interactions.IExecutionSpecification
|  |  |  |  Interactions.IActionExecutionSpecification
|  |  |  |  Interactions.IBehaviorExecutionSpecification
|  |  |  Interactions.IInteraction  : CommonBehaviors.IBehavior
|  |  |  Interactions.IInteractionOperand : Classes.INamespace
|  |  |  Interactions.IInteractionUse
|  |  |  Interactions.IOccurrenceSpecification
|  |  |  |  Interactions.IExecutionOccurrenceSpecification
|  |  |  |  Interactions.IMessageOccurrenceSpecification
                   : Interactions.IMessageEnd
|  |  |  |  |  Interactions.ILostFoundTarget
|  |  |  |  Interactions.IOperandOccurrenceSpecification
|  |  |  Interactions.IStateInvariant
|  |  Interactions.ILifeline
|  |  Interactions.IMessage
|  |  Interactions.IMessageEnd
|  |  Classes.INamespace
|  |  |  Classes.IPackage
             : Classes.IPackageableElement,
              AuxiliaryConstructs.ITemplateableElement
|  |  |  |  AuxiliaryConstructs.IModel
|  |  |  Activities.IState
|  |  Classes.IPackageableElement
                   : AuxiliaryConstructs.IParameterableElement
|  |  |  Classes.IConstraint
|  |  |  |  Interactions.IInteractionConstraint
|  |  |  CommonBehaviors.IEvent
|  |  |  |  Interactions.IExecutionEvent
|  |  |  |  CommonBehaviors.IMessageEvent
|  |  |  |  |  CommonBehaviors.ICallEvent
|  |  |  |  |  Interactions.IReceiveOperationEvent
|  |  |  |  |  Interactions.IReceiveSignalEvent
|  |  |  |  |  Interactions.ISendOperationEvent
|  |  |  |  |  Interactions.ISendSignalEvent
|  |  |  Classes.IType
|  |  |  |  Classes.IClassifier : Classes.INamespace, Classes.IRedefinableElement, AuxiliaryConstructs.ITemplateableElement
|  |  |  |  |  Deployments.IArtifact
                   : Deployments.IDeployedArtifact
|  |  |  |  |  |  Deployments.IDeploymentSpecification
|  |  |  |  |  CommonBehaviors.IBehavioredClassifier
|  |  |  |  |  |  UseCases.IActor
|  |  |  |  |  |  Classes.IClass
                         : CompositeStructures.IEncapsulatedClassifier
|  |  |  |  |  |  |  CommonBehaviors.IBehavior
|  |  |  |  |  |  |  |  Activities.IActivity
|  |  |  |  |  |  |  Components.IComponent
|  |  |  |  |  |  |  |  UseCases.ISubsystem
|  |  |  |  |  |  |  Deployments.INode : IDeploymentTarget
|  |  |  |  |  |  |  |  Deployments.IDevice
|  |  |  |  |  |  |  |  Deployments.IExecutionEnvironment
|  |  |  |  |  |  UseCases.IUseCase
|  |  |  |  |  Classes.IDataType
|  |  |  |  |  |  Classes.IEnumeration
|  |  |  |  |  |  Classes.IPrimitiveType
|  |  |  |  |  Classes.IInterface
|  |  |  |  |  CompositeStructures.IStructuredClassifier
|  |  |  |  |  |  CompositeStructures.IEncapsulatedClassifier
|  |  |  Classes.IValueSpecification : Classes.ITypedElement
|  |  |  |  Classes.IExpression
|  |  |  |  Classes.IInstanceValue
|  |  |  |  Classes.ILiteralSpecification
|  |  |  |  |  Classes.ILiteralBoolean
|  |  |  |  |  Classes.ILiteralInteger
|  |  |  |  |  Classes.ILiteralNull
|  |  |  |  |  Classes.ILiteralString
|  |  |  |  |  Classes.ILiteralUnlimitedNatural
|  |  |  |  Classes.IOpaqueExpression
|  |  Classes.IRedefinableElement
|  |  |  Activities.IActivityNode
|  |  |  |  Activities.IControlNode
|  |  |  |  |  Activities.IDecisionNode
|  |  |  |  |  Activities.IFinalNode
|  |  |  |  |  |  Activities.IActivityFinalNode
|  |  |  |  |  Activities.IForkNode
|  |  |  |  |  Activities.IInitialNode
|  |  |  |  |  Activities.IJoinNode
|  |  |  |  |  Activities.IMergeNode
|  |  |  |  Activities.IExecutableNode
|  |  |  |  |  Actions.IAction
|  |  |  |  |  |  Actions.IAcceptEventAction
|  |  |  |  |  |  Actions.ICreateObjectAction
|  |  |  |  |  |  Actions.IInvocationAction
|  |  |  |  |  |  |  Actions.ICallAction
|  |  |  |  |  |  |  |  Actions.ICallBehaviorAction
|  |  |  |  |  |  |  |  Actions.ICallOperationAction
|  |  |  |  |  |  |  Actions.ISendSignalAction
|  |  |  |  |  |  Actions.IOpaqueAction
|  |  |  |  Activities.IObjectNode  : Classes.ITypedElement
|  |  |  |  |  Activities.IActivityParameterNode
|  |  |  |  |  Actions.IPin : Classes.IMultiplicityElement
|  |  |  |  |  |  Actions.IInputPin
|  |  |  |  |  |  Actions.IOutputPin
|  |  |  UseCases.IExtensionPoint
|  |  |  Classes.IFeature
|  |  |  |  Classes.IBehavioralFeature  : Classes.INamespace
|  |  |  |  |  Classes.IOperation
                   : AuxiliaryConstructs.ITemplateableElement,
                   AuxiliaryConstructs.IParameterableElement
|  |  |  |  Classes.IStructuralFeature
              : Classes.IMultiplicityElement,
                Classes.ITypedElement
|  |  |  |  |  Classes.IProperty
                   : AuxiliaryConstructs.ITemplateableElement,
                   CompositeStructures.IConnectableElement,
                   Deployments.IDeploymentTarget
|  |  |  |  |  |  CompositeStructures.IPort
|  |  Classes.ITypedElement
|  |  |  CompositeStructures.IConnectableElement
             : AuxiliaryConstructs.IParameterableElement
|  |  |  Classes.IParameter  : Classes.IMultiplicityElement, CompositeStructures.IConnectableElement
|  AuxiliaryConstructs.IParameterableElement
|  Classes.IProfileInstance

|  Classes.IRelationship
|  |  Activities.IActivityEdge : Classes.IRedefinableElement
|  |  |  Activities.IControlFlow
|  |  |  Activities.IObjectFlow
|  |  Classes.IAssociation : IClassifier
|  |  |  Deployments.ICommunicationPath
|  |  CompositeStructures.IConnector
|  |  Classes.IDirectedRelationship
|  |  |  Classes.IDependency : Classes.IPackageableElement
|  |  |  |  Classes.IAbstraction
|  |  |  |  |  Deployments.IManifestation
|  |  |  |  |  Classes.IRealization
|  |  |  |  |  |  Classes.IInterfaceRealization
|  |  |  |  Deployments.IDeployment
|  |  |  |  Classes.IUsage
|  |  |  UseCases.IExtend : Classes.INamedElement
|  |  |  Classes.IGeneralization
|  |  |  UseCases.IInclude : Classes.INamedElement
|  |  |  Classes.IPackageImport
|  |  |  AuxiliaryConstructs.ITemplateBinding
|  Classes.IStereotypeInstance
|  Classes.IStereotypePropertyInstance
|  AuxiliaryConstructs.ITemplateableElement
|  AuxiliaryConstructs.ITemplateParameter
|  |  AuxiliaryConstructs.IClassifierTemplateParameter
|  |  AuxiliaryConstructs.IOperationTemplateParameter
|  AuxiliaryConstructs.ITemplateParameterSubstitution
|  AuxiliaryConstructs.ITemplateSignature
|  |  AuxiliaryConstructs.IRedefinableTemplateSignature
             : Classes.IRedefinableElement
```

## <a name="see-also"></a>参照
 [プロファイルの定義](../modeling/define-a-profile-to-extend-uml.md)uml [モデルの検証制約の定義](../modeling/define-validation-constraints-for-uml-models.md)uml [モデリング機能拡張の API リファレンス](../modeling/api-reference-for-uml-modeling-extensibility.md)
