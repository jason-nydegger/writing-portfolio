---
layout: page
title: Setup Guide
permalink: /setup-guide/
---

*The following is a setup guide I wrote while working at UiPath. The target audience is familiar with the UiPath platform and its core concepts, but this may be their first time building a project. Its purpose is to show developers the process and steps to start using the feature set.*

*Typically I try to minimize or avoid adding detailed instructions and screen shots for third party applications given maintenance and accuracy concerns. However, after sitting with customers to walk through the process, I found they were more successful and appreciated the inclusion in this guide so I added them to improve their experience.*

*Note: Only the **bold** links are active to link across sections on this page.*

## Setup

To enable the Microsoft Office 365 activities, your app must be integrated with the [Microsoft identity platform](link) and have the correct [Microsoft Graph API](link) permissions assigned to it.

To integrate your application, assign permissions, and start building your automation project, complete the following steps:

1. [**Register your application**](#Register-you-application)

2. [**Add API permissions**](#add-api-permissions)

3. [**Build your project**](#build-your-project)

After registering your Microsoft Office 365 application, Azure Active Directory assigns a unique application (client) ID that you enter in the Microsoft Office 365 Scope activity along with the services that you assigned permissions to (for example, files, mail, calendar).

<img src="{{"/assets/setup-steps.jpg" | prepend: site.url}}" alt="Overview of the setup steps"/>

## Steps

### Register you application

1. Sign in to the [Azure portal](link) using your personal, work, or school Microsoft Office 365 account.

2. In the left-hand navigation panel, press **Azure Active Directory** and then **App registrations**.

3. In the top navigation bar, press **+ New registration**.

    <img src="{{"/assets/azure_application_registration_start.jpg" | prepend: site.url}}" alt="How to register new azure application"/>

4. Enter a **Name** for your application (for example, office365).

5. Under **Supported account types**, choose the option that applies to you.

6. Under **Redirect URI (optional)**, enter a URI address (if applicable).

7. Press **Register**.

    <img src="{{"/assets/azure_application_registration.jpg" | prepend: site.url}}" alt="Example application registration for Microsoft Office 365 activities"/>

### Add API permissions

1. From your registered application page **(Azure portal > Azure Active Directory > App registrations > AppName)**, choose **API permissions** in the left-hand navigation panel.

2. After the **API permissions** page opens, choose **+ Add a permission** (this opens the **Request API permissions** window).

3. Under **Select an API**, choose Microsoft APIs.

4. Under **Commonly used Microsoft APIs**, choose **Microsoft Graph**.

    <img src="{{"/assets/azure_graph_api_permissions_start.jpg" | prepend: site.url}}" alt="How to add API permissions to registered application"/>

5. Under **What type of permissions does your application require?**, choose **Delegated permissions**.

6. Under **Select permissions**, use the search bar or scroll down the alphabetical list and choose the following permissions:

    * **Calendar**
        * Calendars.Read
        * Calendars.ReadWrite
    * **Files**
        * Files.Read
        * Files.Read.All
        * Files.ReadWrite
        * Files.ReadWrite.All
    * **Mail**
        * Mail.Read
        * Mail.ReadWrite
        * Mail.Send

7. Press **Add permissions** (this returns you to your list of API permissions).

    <img src="{{"/assets/azure_graph_api_permissions_assign.jpg" | prepend: site.url}}" alt="How to choose API permissions for a registered application"/>

8. Verify your **API permissions** include your added **Calendars**, **Files**, and **Mail** permissions.

    <img src="{{"/assets/azure_graph_api_permissions_verify.jpg" | prepend: site.url}}" alt="List of chosen API permissions for a registered application"/>

### Build your project

1. Create a new automation project.

    1. Open **UiPath Studio**.

    2. Under **New Project**, press **Process** (this opens a **New Blank Process** window).

    3. Enter a project **Name**, **Location**, and **Description**.

    4. Press **Create**.

    <img src="{{"/assets/create_automation_project_start.jpg" | prepend: site.url}}" alt="How to create a new automation project in UiPath Studio"/>

2. Install the **UiPath.MicrosoftOffice365.Activities** package.

    1. In the **Design** ribbon, press **Manage Packages** (this opens the **Manage Packages** window).

    2. Under **All Packages**, press **Go!**.

    3. In the search bar, enter *Office365*.

    4. Choose **UiPath.MicrosoftOffice365.Activities** and press **I Accept** to accept the license for the activities.

    <img src="{{"/assets/create_automation_project_add_package.jpg" | prepend: site.url}}" alt="How to install the UiPath.MicrosoftOffice365.Activities package"/>

## Next steps

For a hands-on learning experience and to quickly start using the Microsoft Office 365 activities, see the [Quickstart](link) guides. These guides provide step-by-step instructions to help you create sample automation projects.

To learn more about the Microsoft Office 365 activities (including example property inputs/outputs), see the following activity pages for a complete activity list and links to the activity detail pages:

* [Excel](link)
* [Files](link)
* [Outlook](link)
* [Calendar](link)