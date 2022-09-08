# WEST-Verification-Bot
A simple bot to verify WEST G-suite emails using IFTTT and python.

# Instructions

There are only a few things you need to take care of this bot. Ensure you have the following:

 - Discord Bot Account (you can get one [here](https://discord.com/developers/applications))
 - Discord server dedicated to bot debug (optional)
 - GMail account to send emails
 - IFTTT account to send emails
 - Hosting solution to run the python code, this can be a local PC or the cloud.  

Lets do a rundown of the things you need to do to setup the bot's code.

Firstly, [make an IFTTT account](https://ifttt.com/join). What you then want to do is make an applet with a webhook trigger and a gmail action. 

![This image is important later](https://github.com/AReallyGenericUsername/WEST-Verification-Bot/blob/main/img4.png)
![This is what it should look like once done](https://github.com/AReallyGenericUsername/WEST-Verification-Bot/blob/main/img3.png)

If we look at the code you will find the following line

    myobj = {'value1': RESp,'value3': code}

So in IFTTT you set the recepient address to value1 and the body of the email set to value3. Next you copy the webhook link and paste it in the first bit of code. You can generate the webhook link by going to the IFTTT [webhook integration](https://ifttt.com/maker_webhooks) and hit documentation. Just replace {event} with whatever you named your event when you where setting up the applet.

![copy the highlighted link](https://github.com/AReallyGenericUsername/WEST-Verification-Bot/blob/main/img5.png)

Copy the link that is highlighted and paste it in this section here.

    client = discord.Client(intents=intents)
    url = 'PASTE IT HERE!!!'
    versionstr = '1.4.5'

Secondly you need a discord server to debug with. This is so you can see if someone is messing with the bot and also so you can see if someone "cannot verify" ~~(usually this is fake)~~. Make at least two channels, one for the bot to log in and another for the bot to receieve emergency shutoff commands.

![make a server](https://github.com/AReallyGenericUsername/WEST-Verification-Bot/blob/main/img1.png)

Copy the channel ID and paste it in the corresponding channels

![copy the id like this](https://github.com/AReallyGenericUsername/WEST-Verification-Bot/blob/main/img2.png)


    @client.event
    async def on_ready():
        print('We have logged in as {0.user}'.format(client))
        channel = client.get_channel(PASTE LOG ID HERE)
        await channel.send('bot has come online')
    
    @client.event
    async def on_message(message):
        channel = client.get_channel(PASTE LOG ID HERE)
        cnc = client.get_channel(CNC ID HERE)

Next configure the match expression. For example if I only wanted to verify people with @outlook.com emails then I would put in "@outlook.com"

    RESp= response.content
            print(RESp)
            if str(!!!REPLACE THIS!!! ---> "@outlook.com") not in str(RESp):
                await message.author.dm_channel.send('The email is invalid.')
                await channel.send("!!!---------EVENT TRIGGERED: INVALID EMAIL---------!!!")
                return
            else:

You are now ready to run the bot. Simply type:

    Python3 WhateverYouNamedTheBotFile.py
And  let it run. Oh, also it goes without saying but you do need to run 

    pip install discord openpyxl requests

and also have python installed. If you have any questions then do contact me on discord (chances are that you know my discord if you are reading this...).
