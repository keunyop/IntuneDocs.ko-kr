---
title: "Intune Azure Portal 미리 보기에서 그룹 시작"
titleSuffix: Intune Azure preview
description: "Intune Azure Portal 미리 보기의 그룹에 추가된 새로운 기능"
keywords: 
author: nathbarn
ms.author: nathbarn
manager: angerobe
ms.date: 01/18/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 323f384d-8a76-4adc-999b-e508d641bfa1
ms.custom: intune-azure
translationtype: Human Translation
ms.sourcegitcommit: 153cce3809e24303b8f88a833e2fc7bdd9428a4a
ms.openlocfilehash: 0b3ef70a54c5d91922cecbf07f864c94c559061e
ms.lasthandoff: 02/18/2017


---

# <a name="get-started-with-groups"></a>그룹 시작

[!INCLUDE[azure preview](../includes/azure_preview.md)]

Microsoft는 피드백을 경청하여 Microsoft Intune에서 그룹을 사용하는 방법을 변경했습니다.
Azure Portal에서 Intune을 사용하는 경우 Intune 그룹이 Azure Active Directory 보안 그룹으로 마이그레이션되었습니다.

이점은 이제 모든 Enterprise Mobility + Security 및 Azure AD 앱에 걸쳐 동일한 그룹 환경을 사용할 수 있다는 것입니다. 또한 PowerShell 및 Graph API를 사용하여 새 기능을 확장하고 사용자 지정할 수 있습니다.

Azure AD 보안 그룹은 사용자와 장치 모두에 대한 모든 유형의 Intune 배포를 지원합니다. 또한 제공하는 특성에 따라 자동으로 업데이트되는 Azure AD 동적 그룹을 사용할 수 있습니다. 예를 들어 iOS 9를 실행하는 장치 그룹을 만들 수 있습니다. iOS 9를 실행하는 장치를 등록할 때마다 장치가 동적 그룹에 자동으로 나타납니다.

## <a name="what-is-not-available"></a>사용할 수 없는 기능

이전에 사용한 Intune 그룹 기능 중 일부를 Azure AD에서 사용할 수 없습니다.

- **그룹화되지 않은 사용자** 및 **그룹화되지 않은 장치** Intune 그룹은 더 이상 사용할 수 없습니다.
- 그룹에서 **특정 구성원을 제외하는** 옵션이 Azure Portal에 존재하지 않습니다. 그러나 이 동작을 복제하는 고급 규칙과 함께 Azure AD 보안 그룹을 사용할 수 있습니다. 예를 들어 보안 그룹에 Sales 부서에 속한 모든 사람을 포함하되 직함에 "Assistant"라는 단어가 포함된 사람은 제외하는 고급 규칙을 만들려면 다음과 같은 고급 규칙을 만들 수 있습니다.

  `(user.department -eq "Sales") -and -not (user.jobTitle -contains "Assistant")`를 재정의하려면 선택합니다.
- Intune 콘솔의 **모든 Exchange ActiveSync 관리 장치** 그룹은 Azure AD로 마이그레이션되지 않았습니다. 그러나 Azure Portal에서 EAS 관리 장치에 대한 정보에 여전히 액세스할 수 있습니다.

## <a name="how-to-get-started"></a>시작하는 방법

- 다음 항목을 읽고 Azure AD 보안 그룹 및 보안 그룹의 작동 방법을 자세히 알아봅니다.
    -  [Azure Active Directory 그룹을 사용하여 리소스에 대한 액세스 관리](https://azure.microsoft.com/en-us/documentation/articles/active-directory-manage-groups/)
    -  [Azure Active Directory에서 그룹 관리](https://azure.microsoft.com/en-us/documentation/articles/active-directory-accessmanagement-manage-groups/)
    -  [특성을 사용하여 고급 규칙 만들기](https://azure.microsoft.com/en-us/documentation/articles/active-directory-accessmanagement-groups-with-advanced-rules/)
-  그룹을 만드는 데 필요한 모든 관리자가 **Intune 서비스 관리자** Azure AD 역할에 추가되어 있는지 확인합니다. Azure AD 서비스 관리자 역할에는 **관리 그룹** 권한이 없습니다.
-  Intune 그룹에서 **다음의 특정 멤버를 제외** 옵션을 사용한 경우 배제하지 않고 이러한 그룹을 다시 설계할 수 있는지 여부 또는 비즈니스 요구 사항을 충족하기 위한 고급 규칙이 필요한지 여부를 결정합니다.


## <a name="what-happened-to-intune-groups"></a>Intune 그룹에 미치는 영향
그룹이 클래식 Intune 포털에서 Azure Portal의 Intune으로 마이그레이션되면 다음과 같은 규칙이 적용됩니다.

| Intune의 그룹|Azure AD의 그룹|
|-----------------------------------------------------------------------|-------------------------------------------------------------|
|정적 사용자 그룹|정적 Azure AD 보안 그룹|
|동적 사용자 그룹|Azure AD 보안 그룹 계층 구조가 있는 정적 Azure AD 보안 그룹|
|정적 장치 그룹|정적 Azure AD 보안 그룹|
|동적 장치 그룹|동적 Azure AD 보안 그룹|
|포함 조건이 있는 그룹|Intune의 포함 조건에서 모든 정적 또는 동적 구성원을 포함하는 정적 Azure AD 보안 그룹|
|제외 조건이 있는 그룹|마이그레이션되지 않음|
|기본 제공 그룹:<br>- **모든 사용자**<br>- **그룹 해제된 사용자**<br>- **모든 장치**<br>- **그룹 해제된 장치**<br>- **모든 컴퓨터**<br>- **모든 모바일 장치**<br>- **모든 MDM 관리 장치**<br>- **모든 EAS 관리 장치**|Azure AD 보안 그룹|

## <a name="group-hierarchy"></a>그룹 계층

클래식 Intune 콘솔에서는 모든 그룹에 부모 그룹이 있습니다. 그룹에는 해당 부모 그룹의 구성원만 포함될 수 있습니다. Azure AD에서 자식 그룹은 부모 그룹에 없는 구성원을 포함할 수 있습니다.

## <a name="group-attributes"></a>그룹 특성
특성은 그룹을 정의하는 데 사용될 수 있는 장치 속성입니다. 이 표에는 이러한 조건이 Azure AD 보안 그룹으로 마이그레이션되는 방법이 설명되어 있습니다.

| Intune의 특성|Azure AD의 특성|
|-----------------------------------------------------------------------|-------------------------------------------------------------|
|장치 그룹에 대한 OU(조직 구성 단위) 특성|동적 그룹에 대한 OU 특성.|
|장치 그룹에 대한 도메인 이름 특성|동적 그룹에 대한 도메인 이름 특성.|
|사용자 그룹에 대한 특성으로서의 보안 그룹|그룹은 Azure AD 동적 쿼리에서 특성일 수 없습니다. 동적 그룹은 사용자 관련 특성 또는 장치별 특성만 포함할 수 있습니다.|
|사용자 그룹에 대한 관리자 특성|동적 그룹의 *관리자* 특성에 대한 고급 규칙|
|부모 사용자 그룹의 모든 사용자|해당 그룹을 멤버로 포함하는 정적 그룹|
|부모 장치 그룹의 모든 모바일 장치|해당 그룹을 멤버로 포함하는 정적 그룹|
|Intune에서 관리하는 모든 모바일 장치|동적 그룹에 대한 값으로 'MDM'을 포함하는 관리 유형 특성|
|정적 그룹 내의 중첩 그룹 |정적 그룹 내의 중첩 그룹|
|동적 그룹 내의 중첩 그룹|중첩 수준이 하나인 동적 그룹|

## <a name="what-happens-to-policies-and-apps-you-previously-deployed"></a>이전에 배포한 정책 및 앱에 미치는 영향

정책 및 앱은 이전과 마찬가지로 그룹에 계속 배포됩니다. 그러나 이제 클래식 Intune 콘솔 대신 Azure Portal에서 이러한 그룹을 관리할 수 있습니다.
