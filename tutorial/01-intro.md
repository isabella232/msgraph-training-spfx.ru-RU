---
ms.openlocfilehash: bb55b2bea2497628ceb2e09c889ce62e773d8e71
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823406"
---
<!-- markdownlint-disable MD002 MD041 -->

В этом руководстве рассказывается, как создать [клиентскую веб-часть SharePoint](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) , которая использует API Microsoft Graph для получения сведений о календаре для пользователя.

> [!TIP]
> Если вы предпочитаете просто скачать заполненный учебник, вы можете скачать или клонировать [репозиторий GitHub](https://github.com/microsoftgraph/msgraph-training-spfx).

## <a name="prerequisites"></a>Предварительные требования

Прежде чем приступить к работе с этим руководством, на компьютере для разработки должны быть установлены следующие средства.

- [Node.js](https://nodejs.org/en/download/releases/)
- [Yeoman](https://yeoman.io/)
- [Gulp](https://gulpjs.com/)
- [Генератор Yeoman для SharePoint](https://docs.microsoft.com/sharepoint/dev/spfx/toolchain/scaffolding-projects-using-yeoman-sharepoint-generator)

Дополнительные сведения о требованиях для разработки SharePoint Framework можно найти в странице [Настройка среды разработки SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-development-environment).

> [!IMPORTANT]
> Для SharePoint Framework требуется Node.js версии 10. x. Обязательно установите правильную версию.

Кроме того, у вас должна быть рабочая или учебная учетная запись Майкрософт с доступом к учетной записи глобального администратора в той же организации. Если у вас нет учетной записи Майкрософт, вы можете [зарегистрироваться в программе для разработчиков office 365](https://developer.microsoft.com/office/dev-program) , чтобы получить бесплатную подписку на Office 365.

Прежде чем приступить к работе с этим руководством, клиент Microsoft 365 должен быть [настроен для разработки SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant)с каталогом приложений и тестовым сайтом, созданным ранее.

> [!NOTE]
> Это руководство было написано в следующих версиях этих средств. Действия, описанные в этом руководстве, могут работать с другими версиями, но не тестировались.
>
> - Node.js 10.22.0
> - Yeoman 3.1.1
> - Gulp 4.0.2
> - 1.11.0 генератора Yeoman для SharePoint

## <a name="feedback"></a>Отзывы

Сообщите о нем в [репозиторий GitHub](https://github.com/microsoftgraph/msgraph-training-spfx).
