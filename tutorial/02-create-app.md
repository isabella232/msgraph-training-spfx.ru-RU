---
ms.openlocfilehash: 5164c68a78837c179636f685d28ddf61f93f8415
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823401"
---
<!-- markdownlint-disable MD002 MD041 -->

В этом руководстве описывается создание [клиентской веб-части SharePoint](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) , которая будет использовать Microsoft Graph для получения календаря пользователя за текущую неделю и предоставления пользователю возможности добавления события в календарь.

## <a name="create-a-web-part-project"></a>Создание проекта веб-части

1. Откройте интерфейс командной строки (CLI) в пустом каталоге, в котором нужно создать проект. Выполните следующую команду, чтобы запустить генератор Yeoman для SharePoint.

    ```Shell
    yo @microsoft/sharepoint
    ```

1. Ответьте на приглашения следующим образом.

    - **Имя вашего решения** `graph-tutorial`
    - **Какие базовые пакеты нужно выбрать для ваших компонентов?** `SharePoint Online only (latest)`
    - **Где следует разместить файлы?** `Use the current folder`
    - **Предоставить ли администратору клиента возможность развернуть решение на всех сайтах сразу, не запуская развертывание компонентов или добавление приложений на сайтах?** `Yes`
    - **Будут ли компоненты в решении иметь разрешения на доступ к веб-API, которые являются уникальными и не являются общими для других компонентов в десяти АНТ?** `No`
    - **Какой тип клиентского компонента нужно создать?** `WebPart`
    - **Как называется веб-часть?** `GraphTutorial`
    - **Опишите веб-часть.** `GraphTutorial description`
    - **Какую платформу нужно использовать?** `No JavaScript framework`

1. Выполните следующую команду, чтобы обновить версию TypeScript в проекте до 3,7.

    ```Shell
    npm install @microsoft/rush-stack-compiler-3.7 --save-dev
    ```

1. Open **./tsconfig.js** и замените на `rush-stack-compiler-3.3` `rush-stack-compiler-3.7` .

1. Откройте **./tslint.js** и удалите `"no-use-before-declare": true,` строку. `no-use-before-declare`Это правило является устаревшим и приводит к ошибке во время процесса построения.

## <a name="install-dependencies"></a>Установка зависимостей

Прежде чем переходить, установите некоторые дополнительные пакеты NPM, которые будут использоваться позже.

- [Определения TypeScript Microsoft Graph](https://github.com/microsoftgraph/msgraph-typescript-typings) для предоставления IntelliSense для объектов Microsoft Graph.
- [Набор средств Microsoft Graph](https://docs.microsoft.com/graph/toolkit/overview) для предоставления компонентов пользовательского интерфейса веб-части.
- [Date — ФНС](https://date-fns.org/) для полезных функций для работы с датами.

```Shell
npm install @microsoft/microsoft-graph-types@1.17.0 --save-dev
npm install @microsoft/mgt@1.3.4 date-fns @2.16.0
```
