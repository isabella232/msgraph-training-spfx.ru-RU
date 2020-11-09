---
ms.openlocfilehash: c239c1ea6daae99cc5a65b7b95508ccb2a1bf014
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823414"
---
<!-- markdownlint-disable MD002 MD041 -->

Платформа SharePoint Framework предоставляет [MSGraphClient](https://docs.microsoft.com/javascript/api/sp-http/msgraphclient?view=sp-typescript-latest) для совершения вызовов в Microsoft Graph. Этот класс служит оболочкой [клиентской библиотеки JavaScript Microsoft Graph](https://github.com/microsoftgraph/msgraph-sdk-javascript), предварительно прошедшему проверку подлинности в текущем вошедшем в систему пользователе.

Так как он упаковывает существующую библиотеку JavaScript, ее использование одинаково и полностью совместимо с определениями TypeScript Microsoft Graph.

## <a name="get-the-users-calendar"></a>Получение календаря пользователя

1. Откройте **./СРК/вебпартс/графтуториал/графтуториалвебпарт.ТС** и добавьте приведенные ниже `import` операторы в начало файла.

    ```typescript
    import { MSGraphClient } from '@microsoft/sp-http';
    import * as MicrosoftGraph from '@microsoft/microsoft-graph-types';
    import { startOfWeek, endOfWeek, setDay, set } from 'date-fns';
    ```

1. Добавьте указанную ниже функцию в класс **графтуториалвебпарт** , чтобы отобразить сообщение об ошибке.

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="renderGraphErrorSnippet":::

1. Добавьте указанную ниже функцию, чтобы распечатать события в календаре пользователя.

    ```typescript
    private renderCalendarView(events: MicrosoftGraph.Event[]) : void {
      const viewContainer = this.domElement.querySelector('#calendarView');
      let html = '';

      // Temporary: print events as a list
      for(const event of events) {
        html += `
          <p class="${ styles.description }">Subject: ${event.subject}</p>
          <p class="${ styles.description }">Organizer: ${event.organizer.emailAddress.name}</p>
          <p class="${ styles.description }">Start: ${event.start.dateTime}</p>
          <p class="${ styles.description }">End: ${event.end.dateTime}</p>
          `;
      }

      viewContainer.innerHTML = html;
    }
    ```

1. Замените имеющуюся функцию `render` указанным ниже кодом.

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="renderSnippet":::

    Обратите внимание на то, что делает этот код.

    - Он используется `this.context.msGraphClientFactory.getClient` для получения объекта **MSGraphClient** , прошедшего проверку подлинности.
    - Он вызывает `/me/calendarView` конечную точку, устанавливая `startDateTime` `endDateTime` Параметры и параметры запроса в начало и конец текущей недели.
    - Он используется `select` для ограничения числа возвращаемых полей, запрашивая только те поля, которые использует приложение.
    - Он используется `orderby` для сортировки событий по времени начала.
    - Он используется `top` для ограничения результатов до 25 событий.

## <a name="deploy-the-web-part"></a>Развертывание веб-части

1. Выполните две следующие команды в утилите CLI, чтобы создать и упаковать веб-часть.

    ```Shell
    gulp bundle --ship
    gulp package-solution --ship
    ```

1. Откройте браузер и перейдите к каталогу приложений SharePoint клиента. Выберите пункт меню **приложения для SharePoint** в левой части окна.

1. Отправьте файл **./шарепоинт/солутион/граф-туториал.сппкг** .

1. В приглашении **доверять...** убедитесь, что в запросе указаны 4 разрешения Microsoft Graph, заданные в **package-solution.jsдля** файла. Выберите **сделать это решение доступным для всех сайтов в Организации** , а затем нажмите кнопку **развернуть**.

1. Если вы еще не утвердили разрешения графов для веб-части, сделайте это сейчас.

    1. Откройте [центр администрирования SharePoint](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) с помощью учетной записи администратора клиента.

    1. В левом меню выберите **Дополнительно** , а затем — **доступ к API**.

    1. Выберите каждый из ожидающих запросов в пакете **Graph – Tutorial — клиентский — на стороне решения** и нажмите кнопку **утвердить**.

        ![Снимок экрана со страницей доступа к API центра администрирования SharePoint](images/api-access.png)

## <a name="test-the-web-part"></a>Тестирование веб-части

1. Перейдите на сайт SharePoint, на котором необходимо протестировать веб-часть. Создайте новую страницу для тестирования веб-части.

1. С помощью средства выбора веб-части найдите веб-часть **графтуториал** и добавьте ее на страницу.

    ![Снимок экрана: веб-часть Графтуториал в средстве выбора веб-частей](images/add-web-part.png)

1. Список событий за текущую неделю печатается в веб-части.

    ![Снимок экрана: веб-часть, отображающая список событий](images/calendar-list.png)
