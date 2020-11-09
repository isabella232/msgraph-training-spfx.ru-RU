---
ms.openlocfilehash: 19bd57df9f349d67e9f10e7dd70f02231950b010
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823422"
---
<!-- markdownlint-disable MD002 MD041 -->

SharePoint Framework исключает необходимость регистрации приложения в Azure AD для получения маркеров доступа к Microsoft Graph. Он обрабатывает проверку подлинности для пользователя, зарегистрированного в SharePoint, позволяя веб-части получать маркеры пользователей. Веб-части необходимо указать, какие [области разрешений на доступ к графике](https://docs.microsoft.com/graph/permissions-reference) необходимы, а администратор клиента может утверждать эти разрешения во время установки.

## <a name="configure-permissions"></a>Настройка разрешений

1. **package-solution.jsOpen./config/**.

1. Добавьте следующий код в `solution` свойство.

    ```json
    "webApiPermissionRequests": [
      {
        "resource": "Microsoft Graph",
        "scope": "Calendars.ReadWrite"
      },
      {
        "resource": "Microsoft Graph",
        "scope": "User.ReadBasic.All"
      },
      {
        "resource": "Microsoft Graph",
        "scope": "Contacts.Read"
      },
      {
        "resource": "Microsoft Graph",
        "scope": "People.Read"
      }
    ]
    ```

`Calendars.ReadWrite`Разрешение позволяет веб-части получать календарь пользователя и добавлять события с помощью Microsoft Graph. Остальные разрешения используются компонентами в наборе инструментов Microsoft Graph для отображения информации о участниках событий и организаторов.

## <a name="optional-test-token-acquisition"></a>Необязательно: получение тестового маркера

> [!NOTE]
> Остальные действия на этой странице являются необязательными. Если вы предпочитаете немедленно вернуться к написанию кода Microsoft Graph, вы можете перейти к [просмотру календаря](/graph/tutorials/spfx?tutorial-step=3).

Добавим в веб-часть временный код, чтобы проверить получение маркера.

1. Откройте **./СРК/вебпартс/графтуториал/графтуториалвебпарт.ТС** и добавьте приведенный ниже `import` оператор в начало файла.

    ```typescript
    import { AadTokenProvider } from '@microsoft/sp-http';
    ```

1. Замените имеющуюся функцию `render` указанным ниже кодом.

    ```typescript
    public render(): void {
    this.context.aadTokenProviderFactory
      .getTokenProvider()
      .then((provider: AadTokenProvider)=> {
      provider
        .getToken('https://graph.microsoft.com')
        .then((token: string) => {
          this.domElement.innerHTML = `
          <div class="${ styles.graphTutorial }">
            <div class="${ styles.container }">
              <div class="${ styles.row }">
                <div class="${ styles.column }">
                  <span class="${ styles.title }">Welcome to SharePoint!</span>
                  <p><code style="word-break: break-all;">${ token }</code></p>
                </div>
              </div>
            </div>
          </div>`;
        });
      });
    }
    ```

### <a name="deploy-the-web-part"></a>Развертывание веб-части

1. Выполните две следующие команды в утилите CLI, чтобы создать и упаковать веб-часть.

    ```Shell
    gulp bundle --ship
    gulp package-solution --ship
    ```

1. Откройте браузер и перейдите к каталогу приложений SharePoint клиента. Выберите пункт меню **приложения для SharePoint** в левой части окна.

1. Отправьте файл **./шарепоинт/солутион/граф-туториал.сппкг** .

1. В приглашении **доверять...** убедитесь, что в запросе указаны 4 разрешения Microsoft Graph, заданные в **package-solution.jsдля** файла. Выберите **сделать это решение доступным для всех сайтов в Организации** , а затем нажмите кнопку **развернуть**.

1. Откройте [центр администрирования SharePoint](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) с помощью учетной записи администратора клиента.

1. В левом меню выберите **Дополнительно** , а затем — **доступ к API**.

1. Выберите каждый из ожидающих запросов в пакете **Graph – Tutorial — клиентский — на стороне решения** и нажмите кнопку **утвердить**.

    ![Снимок экрана со страницей доступа к API центра администрирования SharePoint](images/api-access.png)

### <a name="test-the-web-part"></a>Тестирование веб-части

1. Перейдите на сайт SharePoint, на котором необходимо протестировать веб-часть. Создайте новую страницу для тестирования веб-части.

1. С помощью средства выбора веб-части найдите веб-часть **графтуториал** и добавьте ее на страницу.

    ![Снимок экрана: веб-часть Графтуториал в средстве выбора веб-частей](images/add-web-part.png)

1. Маркер доступа печатается под знаком **Добро пожаловать в SharePoint!** сообщение в веб-части. Вы можете скопировать этот маркер и проанализировать его [https://jwt.ms/](https://jwt.ms/) , чтобы убедиться в том, что он содержит области разрешений, необходимые веб-части.

    ![Снимок экрана: веб-часть, отображающая маркер доступа](images/access-token.png)
