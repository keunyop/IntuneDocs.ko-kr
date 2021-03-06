---
title: Microsoft Intune을 사용하여 모바일 디바이스에 기본 제공 앱 추가
titleSuffix: ''
description: Intune을 사용하여 모바일 디바이스에 기본 제공 앱을 더 쉽게 설치하는 방법을 알아봅니다.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/08/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 0ec8de66-5a0f-4c8d-afbf-c2becc7d6eec
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a424655241f44125b51ef2f75cb6c537b10dd91d
ms.sourcegitcommit: 916fed64f3d173498a2905c7ed8d2d6416e34061
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66049529"
---
# <a name="add-built-in-apps-to-microsoft-intune"></a>Microsoft Intune에 기본 제공 앱 추가

*기본 제공* 앱 유형을 사용하면 Office 365 앱과 같이 엄격히 관리되는 앱을 iOS 및 Android 디바이스에 쉽게 할당할 수 있습니다. Excel, OneDrive, Outlook, Skype 등의 특정 앱을 이 앱 유형에 할당할 수 있습니다. 앱을 추가하면 *기본 제공 iOS 앱* 또는 *기본 제공 Android 앱* 중 하나로 앱 유형이 표시됩니다. 기본 제공 앱 유형을 사용하여 어떤 앱을 디바이스 사용자에게 게시할지 선택할 수 있습니다.

이전 버전의 Intune 콘솔에서 Intune은 Outlook, OneDrive 등의 몇 가지 관리되는 기본 Office 365 앱을 제공했습니다. 이 관리되는 앱의 앱 유형은 *관리되는 iOS 스토어 앱* 또는 *관리되는 Android 앱*으로 태그되었습니다. 이러한 앱 유형을 사용하는 대신 기본 제공 앱 유형을 사용하는 것이 좋습니다. 기본 제공 앱 유형을 사용하면 보다 유연하게 Office 365 앱을 편집하고 삭제할 수 있습니다.

>[!NOTE]
>*관리되는 iOS 스토어* 또는 *관리되는 Android 앱*으로 태그된 기본 Office 365 앱은 모든 할당이 삭제되면 앱 목록에서 제거됩니다.

## <a name="add-a-built-in-app"></a>기본 제공 앱 추가

Microsoft Intune에서 사용 가능한 앱에 기본 제공 앱을 추가하려면 다음을 수행합니다.
1. Azure Portal에 로그인합니다.
2. Microsoft Intune 창을 표시하려면 **추가 서비스** > **모니터링 + 관리** > **Intune**을 선택합니다.
3. **Intune** 창에서 **클라이언트 앱**을 선택합니다.
4. **클라이언트 앱** 창의 **관리** 아래에서 **앱**을 선택합니다.
5. **추가**를 선택합니다.
6. **추가** 앱 창의 **앱 유형** 목록에서 **기본 제공 앱**을 선택합니다.
7. **앱 선택**을 선택합니다.
8. **기본 제공 앱** 창에서 포함할 앱을 선택합니다.
9. **앱 추가** 창에서 **추가**를 선택합니다.


## <a name="configure-app-information"></a>앱 정보 구성

기본 제공 앱에 대한 정보를 수정할 수 있습니다. 이 정보를 사용하여 Intune에서 앱을 식별하고 사용자가 회사 포털에서 앱을 찾을 수 있습니다.
1. **클라이언트 앱 - 앱** 창에서 수정하려는 기본 제공 앱을 선택합니다.  
    기본 제공 앱에 대한 창이 표시됩니다.
2. **관리**에서 **속성** 옵션을 선택합니다.
3. 기본 제공 앱 정보를 수정하려면 **구성** 옵션을 선택합니다.
4. **앱 정보** 창에서 다음 정보를 수정할 수 있습니다.
    - **이름**: 회사 포털에 표시되는 기본 제공 앱의 이름을 입력합니다. 사용하는 모든 이름이 고유한지 확인합니다. 동일한 앱 이름을 두 번 사용하는 경우에는 회사 포털에서 앱 중 하나만 사용자에게 표시됩니다.
    - **설명**: 앱에 대한 설명을 입력합니다. 
    - **게시자**: 앱 게시자의 이름을 입력합니다.
    - **범주**: 필요한 경우 기본 제공 앱 범주를 하나 이상 선택합니다. 이 옵션을 설정하면 사용자가 회사 포털을 찾아볼 때 앱을 더 쉽게 찾을 수 있습니다.
    - **회사 포털에서 이 항목을 추천 앱으로 표시**: 사용자가 앱을 찾아볼 때 회사 포털의 기본 페이지에 앱을 쉽게 확인할 수 있도록 표시합니다.
    - **정보 URL**: 필요에 따라 이 앱에 대한 정보를 포함하는 웹 사이트의 URL을 입력합니다. URL은 회사 포털에서 사용자에게 표시됩니다.
    - **개인정보취급방침 URL**: 필요에 따라 이 앱에 대한 개인정보 관련 정보를 포함하는 웹 사이트의 URL을 입력합니다. URL은 회사 포털에서 사용자에게 표시됩니다.
    - **개발자**: 선택적으로, 앱 개발자의 이름을 입력합니다.
    - **소유자**: 필요한 경우 이 앱의 소유자 이름을 입력합니다(예: *HR 부서*).
    - **메모**: 이 앱과 연결할 모든 메모를 입력합니다.
    - **아이콘 업로드**: 사용자가 회사 포털을 찾아볼 때 앱과 함께 표시되는 아이콘을 업로드합니다.
4. **확인**을 선택합니다.
5. **속성** 창에서 **저장**을 선택합니다.

## <a name="next-steps"></a>다음 단계

- 이제 선택한 그룹에 앱을 할당할 수 있습니다. 자세한 내용은 [그룹에 앱 할당](apps-deploy.md)을 참조하세요.
