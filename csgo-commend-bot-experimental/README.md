# CSGO Commend Bot
**You are viewing an experimental branch including a commend bot rewrite. Use with caution.**

If you're a developer and want to know how to fix your own commend bot its very simple. Just set `steam_id_gs` to a valid server steam ID, on your target's account & bot accounts. Switch after 20 commends and repeat.

# Restrictions
Valve changed it so that you now need to *be* on a server before you can commend someone. There also is a limit of the amount of commends you can send per server, that limit is set to 20. Due to this you need your targets Steam details, so you can login and change server after 20 commends. This also **heavily** impacts speed.

# **This version has a major issue**
Typically after ~20 commends it stops working all together, despite closing Steam connection and relogging. Sometimes it works for a little more, most of the time it doesn't. You can do another 20 after restarting the script.

# Future
- Add back the colors
- Add the ability to remove commends
- Add the ability to commend three times with one account per 24 hours instead of once every 8 hours

# Requirements
- [NodeJS **v11 or later**](https://nodejs.org/)
- [Little bit of JSON knowledge](https://www.json.org/)

# Installation
1. Download this repository (Alternatively use `git` to clone recursively, then you can skip step 2)
2. Click on the `protobufs` folder and download that as well, extract the content inside the `protobufs` folder.
3. Put it all in a folder
4. Open a command prompt *inside* the folder
5. Enter `npm install`
6. Rename `config.json.example` to `config.json` and adjust it ([See below](#config))
7. Add accounts using the [Database Manager](#database-manager)
8. Run `node index.js`

# Config
- commend:
  - friendly `Boolean`: Whether or not to commend as friendly
  - teaching `Boolean`: Whether or not to commend as teaching
  - leader `Boolean`: Whether or not to commend as leader
- account:
  - username `String`: Username of the account you want to boost
  - password `String`: Pasword of the account you want to boost
  - sharedSecret `String`: Optional shared secret if the account has two factor authentication
- method `String`: Define the method - Valid values: `LOGIN` & `SERVER` - [Read More](#botting-method)
- target `String`: SteamID/VanityURL/ProfileURL of target
- serverID `String`: ServerID **or** IP of the server - [Read More](#server-id)
- matchID `String`: Optional match ID, typically just `"0"` anyways - I always use `"0"`.
- toSend `Number`: Amount of commends you want to send
- cooldown `Number`: Cooldown in milliseconds to not reuse accounts - Currently set to 8 hours
- betweenChunks `Number`: Cooldown in milliseconds between chunks - (I recommend a minimum of `240000` (4 minutes))
- steamWebAPIKey `String`: Steam Web API key from [here](https://steamcommunity.com/dev/apikey)

# Database Manager
- `Export account list`: Export all accounts in a `username:password` format
- `List commends for user`: List **all** accounts which have commended a specific user
- `Reset commends for user`: Delete **all** commend entries from the database of a specific user
- `Remove account from database`: Delete a specific account from the database including commend history
- `Add account(s) to database`: Add accounts to the database, import from JSON file, import from `username:password` file or manually add accounts
- `List not working accounts`: List **all** accounts which are marked as inoperational by the script
- `Reset Database`: Will clear out **all** content of the database, resetting it to the default
- `Exit`: Safely close database before exiting process

Then simple run it via `node databaseManager.js`, use the arrow keys & enter to navigate. Read on-screen instructions for more details.

# Botting Method
You can choose between two botting methods, `LOGIN` and `SERVER`.

- `LOGIN` will log into the targets account and automatically grab a server. `account` object **must** be filled with account details. Will ignore `target` & `serverID`.
- `SERVER` will assume the target is on the defined server. `serverID` **must** be either a ServerIP including port or a direct ServerID. Will ignore `account`.

# Server ID
The `serverID` field allows for either ServerIP or ServerID. Server IP is self explanatory. ServerID can be found by entering `status` into the console ingame. On a community server it will look like this: `1.37.0.1/13701 934/7508 secure  [A:1:1297634312:12708]` > `[A:1:1297634312:12708]`. On a Valve server it will look like this: `Connected to =[A:1:3849827331:12657]:0` > `[A:1:3849827331:12657]`.

Make sure to **only** include the stuff between the brackets and the brackets themselves.
