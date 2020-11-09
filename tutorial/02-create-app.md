---
ms.openlocfilehash: 5164c68a78837c179636f685d28ddf61f93f8415
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823401"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="f1fb1-101">В этом руководстве описывается создание [клиентской веб-части SharePoint](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) , которая будет использовать Microsoft Graph для получения календаря пользователя за текущую неделю и предоставления пользователю возможности добавления события в календарь.</span><span class="sxs-lookup"><span data-stu-id="f1fb1-101">In this tutorial, you'll create a [SharePoint client-side web part](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) that will use Microsoft Graph to get the user's calendar for the current week and allow the user to add an event to their calendar.</span></span>

## <a name="create-a-web-part-project"></a><span data-ttu-id="f1fb1-102">Создание проекта веб-части</span><span class="sxs-lookup"><span data-stu-id="f1fb1-102">Create a web part project</span></span>

1. <span data-ttu-id="f1fb1-103">Откройте интерфейс командной строки (CLI) в пустом каталоге, в котором нужно создать проект.</span><span class="sxs-lookup"><span data-stu-id="f1fb1-103">Open your command-line interface (CLI) in an empty directory where you want to create the project.</span></span> <span data-ttu-id="f1fb1-104">Выполните следующую команду, чтобы запустить генератор Yeoman для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f1fb1-104">Run the following command to start the Yeoman SharePoint generator.</span></span>

    ```Shell
    yo @microsoft/sharepoint
    ```

1. <span data-ttu-id="f1fb1-105">Ответьте на приглашения следующим образом.</span><span class="sxs-lookup"><span data-stu-id="f1fb1-105">Respond to the prompts as follows.</span></span>

    - <span data-ttu-id="f1fb1-106">**Имя вашего решения**</span><span class="sxs-lookup"><span data-stu-id="f1fb1-106">**What is your solution name?**</span></span> `graph-tutorial`
    - <span data-ttu-id="f1fb1-107">**Какие базовые пакеты нужно выбрать для ваших компонентов?**</span><span class="sxs-lookup"><span data-stu-id="f1fb1-107">**Which baseline packages do you want to target for your component(s)?**</span></span> `SharePoint Online only (latest)`
    - <span data-ttu-id="f1fb1-108">**Где следует разместить файлы?**</span><span class="sxs-lookup"><span data-stu-id="f1fb1-108">**Where do you want to place the files?**</span></span> `Use the current folder`
    - <span data-ttu-id="f1fb1-109">**Предоставить ли администратору клиента возможность развернуть решение на всех сайтах сразу, не запуская развертывание компонентов или добавление приложений на сайтах?**</span><span class="sxs-lookup"><span data-stu-id="f1fb1-109">**Do you want to allow the tenant admin the choice of being able to deploy the solution to all sites immediately without running any feature deployment or adding apps in sites?**</span></span> `Yes`
    - <span data-ttu-id="f1fb1-110">**Будут ли компоненты в решении иметь разрешения на доступ к веб-API, которые являются уникальными и не являются общими для других компонентов в десяти АНТ?**</span><span class="sxs-lookup"><span data-stu-id="f1fb1-110">**Will the components in the solution require permissions to access web APIs that are unique and not shared with other components in the ten ant?**</span></span> `No`
    - <span data-ttu-id="f1fb1-111">**Какой тип клиентского компонента нужно создать?**</span><span class="sxs-lookup"><span data-stu-id="f1fb1-111">**Which type of client-side component to create?**</span></span> `WebPart`
    - <span data-ttu-id="f1fb1-112">**Как называется веб-часть?**</span><span class="sxs-lookup"><span data-stu-id="f1fb1-112">**What is your Web part name?**</span></span> `GraphTutorial`
    - <span data-ttu-id="f1fb1-113">**Опишите веб-часть.**</span><span class="sxs-lookup"><span data-stu-id="f1fb1-113">**What is your Web part description?**</span></span> `GraphTutorial description`
    - <span data-ttu-id="f1fb1-114">**Какую платформу нужно использовать?**</span><span class="sxs-lookup"><span data-stu-id="f1fb1-114">**Which framework would you like to use?**</span></span> `No JavaScript framework`

1. <span data-ttu-id="f1fb1-115">Выполните следующую команду, чтобы обновить версию TypeScript в проекте до 3,7.</span><span class="sxs-lookup"><span data-stu-id="f1fb1-115">Run the following command to update the TypeScript version in the project to 3.7.</span></span>

    ```Shell
    npm install @microsoft/rush-stack-compiler-3.7 --save-dev
    ```

1. <span data-ttu-id="f1fb1-116">Open **./tsconfig.js** и замените на `rush-stack-compiler-3.3` `rush-stack-compiler-3.7` .</span><span class="sxs-lookup"><span data-stu-id="f1fb1-116">Open **./tsconfig.json** and replace `rush-stack-compiler-3.3` with `rush-stack-compiler-3.7`.</span></span>

1. <span data-ttu-id="f1fb1-117">Откройте **./tslint.js** и удалите `"no-use-before-declare": true,` строку.</span><span class="sxs-lookup"><span data-stu-id="f1fb1-117">Open **./tslint.json** and remove the `"no-use-before-declare": true,` line.</span></span> <span data-ttu-id="f1fb1-118">`no-use-before-declare`Это правило является устаревшим и приводит к ошибке во время процесса построения.</span><span class="sxs-lookup"><span data-stu-id="f1fb1-118">The `no-use-before-declare` rule is deprecated and will cause an error during the build process.</span></span>

## <a name="install-dependencies"></a><span data-ttu-id="f1fb1-119">Установка зависимостей</span><span class="sxs-lookup"><span data-stu-id="f1fb1-119">Install dependencies</span></span>

<span data-ttu-id="f1fb1-120">Прежде чем переходить, установите некоторые дополнительные пакеты NPM, которые будут использоваться позже.</span><span class="sxs-lookup"><span data-stu-id="f1fb1-120">Before moving on, install some additional NPM packages that you will use later.</span></span>

- <span data-ttu-id="f1fb1-121">[Определения TypeScript Microsoft Graph](https://github.com/microsoftgraph/msgraph-typescript-typings) для предоставления IntelliSense для объектов Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="f1fb1-121">[Microsoft Graph TypeScript definitions](https://github.com/microsoftgraph/msgraph-typescript-typings) to provide Intellisense for Microsoft Graph objects.</span></span>
- <span data-ttu-id="f1fb1-122">[Набор средств Microsoft Graph](https://docs.microsoft.com/graph/toolkit/overview) для предоставления компонентов пользовательского интерфейса веб-части.</span><span class="sxs-lookup"><span data-stu-id="f1fb1-122">[Microsoft Graph Toolkit](https://docs.microsoft.com/graph/toolkit/overview) to provide UI components for the web part.</span></span>
- <span data-ttu-id="f1fb1-123">[Date — ФНС](https://date-fns.org/) для полезных функций для работы с датами.</span><span class="sxs-lookup"><span data-stu-id="f1fb1-123">[date-fns](https://date-fns.org/) for helpful functions for working with dates.</span></span>

```Shell
npm install @microsoft/microsoft-graph-types@1.17.0 --save-dev
npm install @microsoft/mgt@1.3.4 date-fns @2.16.0
```
