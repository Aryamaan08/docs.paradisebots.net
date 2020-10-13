---
title: Paradise Python Library
---

This is our official Python Library for Paradise Bots, if you have any issues please submit an issue on our github or join our discord
* [Github Link](https://github.com/ParadiseBotList)
* [Discord Link](https://discord.gg/Cqy99Pt)

---
To start using server counts on a bot, 
* Go to your bot edit page, 
* Click the Authorization Token link at the bottom of the page. This will generate an auth token.

---

## Example
Example with Automatic Server Count
```Python
url = "https://paradisebots.net/api/v1/bot/:botid" # Replace :botid with your bot ID

payload = "{\"server_count\": 1500}" # Replace this number with the server count
headers = {
  'authorization': 'YOUR_AUTH_TOKEN',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data = payload)
print(response.text.encode('utf8'))

```

---

## User-Made API

There is a user-made API for Python as well. The gist (with an example) is found here: https://gist.github.com/Aryamaan08/6833f31218b00f7792dc900728b0db01

---

## User-Made API Example

Copy the code in the gist and save it as `paradise.py`.

Here's an example to see how many users have voted for a bot. In this case, `client.user` is the bot user. For other bots, you can supply the bot ID. It can be either a string or an int, so if you're confused, don't bother converting.

```py
from paradise import Paradise
@client.command()
async def votecount(ctx):
  b = Paradise(client.user.id)
  await ctx.send(f"I have `{b.votes}` votes. Vote for me at https://paradisebots.net/bots/{client.user.id} now!")
```

If you're making, say, an eval command, and you want to see if the user is an owner, instead of doing this:

```py
if ctx.author.id == 1234567890 or ctx.author.id == 0987654321 or ctx.author.id == 99999999:
```

You can do:

```py
if b.is_owner(ctx.author.id):
```

`is_owner` is a class method so you don't have to get the list of owners and manually search them yourself (This assumes that the owner is listed as one on the bot page).

If you want to get the long description of a given Bot ID, you can do:

```py
@client.command()
async def long(ctx, *, botid=None):
    if not botid:
        await ctx.send("Please specify a Bot ID!")
    else:
        tr
            b = Paradise(botid)
            e = discord.Embed(
                title=b.username,
                description=b.long_description,
                color=0x008080
            )
            await ctx.send(embed=e)
        except ValueError:
            await ctx.send("Sorry, Invalid Bot ID!")
```

Since making an API request is very slow, you can immediately rule out Bot IDs which aren't ints, aren't 18 characters, or have too many repeating digits.
You may do something similar for other aspects of a bot, maybe even have a `botinfo` command. Go wild with your creations!

## What can I do with this API Wrapper?

(Note that these have to be used like so: `b.property` where b is an object of class `Paradise`.

You can get the:

- tags
- votes
- owner
- additional_owners
- prefix
- description
- long_description
- username
- website
- github
- donations
- support_server
- bot_library
- total_servers
- total_shards
