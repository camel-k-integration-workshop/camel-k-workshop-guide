+++
title = "Intro"
weight = 1
+++

## Prerequisites
Before we start going through the workshop, make sure that you have **VSCode** or **VSCodium** installed on your machine.
For simplicity, we will reference the IDE as **VSCode** going forward.
> If you are familiar with Git, you can clone following GitHub Repository and open it with VSCode:
> https://github.com/nexus-Six/camelk-integration-workshop.git

We need to install the VSCode extensions -- **Extension Pack for Apache Camel by Red Hat** for later use.
{{< figure src="../images/extension_pack.png?width=50pc&classes=border,shadow" title="Click image to enlarge" >}}

### Telegram Account, Bot and Chat ID

> Note: if you haven't used telegram before, you can simply download the `Telegram` mobile app and create a new account there.  
Alternatively, you can follow [this link](https://telegram.org/) to get the desktop version. 

#### Create a telegram bot
&#9744; Search for username @BotFather \
&#9744; Start the chat (/start) \
&#9744; Send /newbot to @BotFather \
&#9744; Follow the instruction of @BotFather and create a name and username for the bot. \
&#9744; Once the bot is created, we will get a token to access the HTTP API, **keep the token secure and store it safely**. \
&#9744; You should search for your newly-created bot and click /start to initiate the conversation with the bot.

#### Get our Chat ID
&#9744; Search for username @RawDataBot with name `Telegram Bot Raw` \
&#9744; Start the chat (/start) \
&#9744; You will receive a message from the @RawDataBot, store the `"id"` in the `"chat"` section somewhere safe. 

{{% notice tip %}}
Once we get the telegram bot token and the chat ID, remember to save them somewhere safe and easily accessible. We will need them in the following examples.
{{% /notice %}}