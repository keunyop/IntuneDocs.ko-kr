---
title: "Intune 및 Zimperium 통합"
titleSuffix: Intune on Azure
description: "Intune과 Zimperium을 통합합니다."
keywords: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.date: 09/06/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 363fd280-1865-4a61-855b-eb75c3c62753
ms.reviewer: heenamac
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 1b4adb2db14c2e1c83be8e7b3644944c1910cb97
ms.sourcegitcommit: d434dfab7ef7a6c4082d675717fa22d5581b4f51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2017
---
# <a name="integrate-zimperium-with-intune"></a>Intune 및 Zimperium 통합

Intune과 Zuneperium Mobile Threat Defense 솔루션을 통합하려면 아래 단계를 수행해야 합니다.

## <a name="before-you-begin"></a>시작하기 전에

> [!NOTE]
> 아래 단계는 [Zimperium MTD 콘솔](https://staging2-console.zimperium.com)에서 수행해야 합니다.

Intune과 Zimperium을 통합하는 과정을 시작하기 전에 다음 항목이 있는지 확인합니다.

-   Microsoft Intune 구독

-   다음 권한을 부여할 Azure Active Directory 관리자 자격 증명

    -   로그인 및 사용자 프로필 읽기

    -   로그인한 사용자로 디렉터리에 액세스

    -   디렉터리 데이터 읽기

    -   Intune에 장치 정보 보내기

-   Zimperium MTD 콘솔에 액세스하기 위한 관리자 자격 증명

### <a name="zimperium-app-authorization"></a>Zimperium 앱 권한 부여

Zimperium 앱 권한 부여 프로세스는 다음과 같이 구성됩니다.

-   Zimperium 서비스에서 장치 상태와 관련된 정보를 Intune으로 다시 전달하도록 허용합니다.

-   Zimperium이 Azure AD 등록 그룹 멤버 자격과 동기화하여 해당 장치의 데이터베이스를 채웁니다.

-   Zimperium 관리 콘솔에서 Azure AD SSO(Single Sign-On)를 사용하도록 허용합니다.

-   Zimperium 앱에서 Azure AD SSO를 사용하여 로그인하도록 허용합니다.

## <a name="to-set-up-zimperium-integration"></a>Zimperium 통합 설정

1.  [Zimperium MTD 콘솔](https://staging2-console.zimperium.com)로 이동하여 자격 증명으로 로그인합니다.

2.  왼쪽 메뉴에서 **관리**를 선택합니다.

3.  **MDM 설정** 탭을 선택합니다.

4.  **MDM 추가**를 선택한 다음 **MDM 공급자** 목록에서 **Microsoft Intune**을 선택합니다.

5.  Microsoft Intune을 MDM 서비스로 설정하면 **Microsoft Intune 구성** 창이 표시되며, Zimperium에서 Azure AD Single Sign-On을 통해 Intune 및 Azure AD와 통신할 수 있도록 권한을 부여하려면 **Zimperium zConsole** 및 **zIPS iOS 및 Android 앱** 옵션 각각에 대해 **Azure Active Directory 추가**를 선택합니다.

    > [!IMPORTANT]
    > Intune과의 통합 프로세스를 완료하려면 Zimperium zConsole, zIPS iOS 및 Android 앱을 추가해야 합니다.

6.  **동의**를 선택하여 Intune 및 Azure Active Directory와 통신할 수 있는 권한을 Zimperium 앱에 부여합니다.

7.  Azure AD에 **Zimperium zConsole** 및 **zIPS iOS 및 Android** 앱을 추가하면 Azure AD 보안 그룹을 추가해야 Zimperium에서 Azure AD 보안 그룹과 서비스를 동기화할 수 있습니다.

8.  **마침**을 선택하여 구성을 저장하고 첫 번째 Azure AD 보안 그룹 동기화를 시작합니다.

## <a name="next-steps"></a>다음 단계

-   [Zimperium 앱 설정](mtd-apps-ios-app-configuration-policy-add-assign.md)