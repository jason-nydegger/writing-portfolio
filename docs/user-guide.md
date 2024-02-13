---
layout: page
title: User Guide
permalink: /user-guide/
---

*The following is a Quickstart guide I wrote while working at UiPath. The target audience is familiar with the UiPath platform and its core concepts, but may be new to creating an automation project.*

*For this Quickstart guide, I defined the following use case to create a working scenario:*

*As an HR team member, you're tasked with welcoming a group of new employees on a weekly basis. To give your new teammates a warm welcome and introduce them to their fellow "newbies", you create dedicated Slack channels for each cohort and send a welcome message.*

*Instead of manually creating the channels, inviting each new hire, and sending your welcome message, you can create an automation project using the Slack Scope, Create Channel, Invite to Channel, and Send Message activities.*

*UiPath documentation did not have Quickstart guides and only a handful of examples. I took the opportunity to introduce these standards to help our customers develop faster and with more confidence. My goal for all Quickstart guides was to provide customers with not only the steps to create a sample automation project, but steps to test their work so they could verify they were successful; this also gives them an idea of how they may verify their own designs.*

*Note: The links in this example are placeholders (not active), to demonstrate how a customer would learn more about a given topic*

## Quickstart - Channels and Messages

The purpose of this guide is to help you create a sample automation project using different Slack activities, including [Slack Scope](link), [Create Channel](link), [Invite to Channel](link), [Send Message](link), and [Get Messages](link).

This sample enables you to quickly verify the connection to your Slack workspace and get familiar with the included activity's input/output datatypes. After completing the steps in this guide, you'll have an automation sequence that does the following:

1. Establishes a connection to your Slack workspace (**Slack Scope**).

2. Creates a new channel in your Slack workspace (**Create Channel**).

3. Invites a user to your new channel (**Invite to Channel**).

4. Sends a message to the channel (**Send Message**).

5. Verifies the results of the **Create Channel**, **Invite to Channel**, and **Send Message** activities by outputting the channel's messages and user information (**Get Messages**, **For Each**, **If**, and **Write Line**).

The following is the example automation sequence you will create, including the input/output data types, and the applicable Slack APIs that are being called.

<img src="{{"/assets/quickstart_overview.jpg" | prepend: site.url}}" alt="Example automation sequence, its input/output data types, and the applicable Slack APIs that are being called"/>

## Prerequisites

Before you begin, complete the [Slack Setup](link) guide.

## Steps

### Build your project

1. Add the [Slack Scope](link) activity to your project.

    1. Enter the **ClientID** and **ClientSecret** for your Slack app. For more information about the Client ID and Client Secret, see [Create new Slack app](link) in the **Setup** guide.

    2. In the **Scopes** drop-down list, choose all the listed scopes.

    3. Press **Connect** in the **Design** canvas.

2. Add the [Create Channel](link) activity after the **Slack Scope** activity.

    1. Create and enter a `string` variable for the **ChannelName** (for example, *channelName* with a default value of *“slack_quickstart”*). For more information about the allowed values, see [Channel Name](link) in the **Create Channel** activity details page.

    2. Create and enter a `string` variable for your **ChannelID** (for example, *newChannel*).

3. Add the [Invite to Channel](link) activity after the **Create Channel** activity.

    1. In the **Channel** property, enter the `string` variable you created for the **ChannelID** in the previous step (for example, *newChannel*).

    2. Enter a Slack user that you want to invite to the channel using the Slack's username syntax (for example, *"Jean.Grey"*). 

4. Add the [Send Message](link) activity after the **Invite to Channel** activity.

    1. In the **Conversation** property, enter the `string` variable you created for the **ChannelID** property in the **Create Channel** activity (for example, *newChannel*).

    2. Create and enter a `string` variable for the **Text** property (for example, *messageText* with default value of *"Welcome to "+channelName*).

<img src="{{"/assets/quickstart_create_project.jpg" | prepend: site.url}}" alt="Example automation project using Slack activities"/>

Your automation project is now ready. To verify that it works, let’s test your project.

### Test your project

1. To verify that your new channel was created, the users invited, and the message was sent successfully, add the [Get Messages](link) activity after the **Send Message** activity.

    1. In the **Conversation** property, enter the `string` variable you created for the **ChannelID** property in the **Create Channel** activity (for example, *newChannel*).

    2. For the **Messages** output property, create and enter a `message[]` variable, choosing **UiPath.Slack.Models.Message[]** as the variable type (for example, *slackMessages*).

2. To process and see the output of your sent message, after the **Get Messages** activity, add the [For Each](link) activity with the [If](link) and [Write Line](link) activities.

    1. For the **For Each** activity **TypeArgument** property, choose **UiPath.Slack.Models.Message**.

    2. In the **Values** property, enter the `message[]` variable you created for the **Messages** output property in the **Get Messages** activity (for example, *slackMessages*).

    3. For the **If** activity **Condition** statement, enter the following parameters to narrow down the **Get Messages** output to the message you sent with the **Send Message** activity: *item.Text.Equals(messageText)*.

    4. In the **Then** statement box, add the **Write Line** activity.

    5. For the **Write Line** activity **Text** property, enter *item.User+" : "+item.Text* to output the message text and your user ID for verification in the output window.

    6. In the **Else** statement box, add another **Write Line** activity.

    7. For the second **Write Line** activity **Text** property, enter *item.User+" : "+item.Text* to see all the user IDs that "joined" from the **Invite to Channel** activity.

3. Press **Start** and verify the results in the **Output** window.

<img src="{{"/assets/quickstart_test_project.jpg" | prepend: site.url}}" alt="Example of a successfully executed automation project using Slack activities"/>

You're done!

When you're ready, try the other [Quickstart](link) guides to get more familiar with the different Slack activities.

To learn more about the Slack activities (including example property inputs/outputs), see the [Activities](link) page for a complete activity list and links to the activity detail pages.

