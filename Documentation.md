# blooket

Documentation for the node.js Blooket library

## Documentation

- [Basic Usage](https://github.com/glixzzy/blooket-wrapper/blob/main/Documention.md#basic-usage)
- [Functions](https://github.com/glixzzy/blooket-wrapper/blob/main/Documention.md#functions)
- [Events](https://github.com/glixzzy/blooket-wrapper/blob/main/Documention.md#events)

### Usage
```js
const Blooket = require('blooket')

const client = new Blooket();

client.joinGame('342865', 'twst', 'Dog')

client.on('Joined', data => {
    console.log(`Joined game with name: ${data.name} \nJoined game with blook: ${data.blook}`)
});
```

## Functions
- **`addTokens(tokenAmount, xpAmount, blooketName, blooketAuthToken)`** - Adds tokens and XP to your account

**Returns `Promise`**

#### Parameters:
| name | description |
|-|-|
|*tokenAmount*|Amount of tokens you want (max 500 allowed) - **Number**|
|*xpAmount*|Amount of XP you want (max 300 allowed) - **Number**|
|*blooketName*|Your Blooket account name - **String**|
|*blooketAuthToken*|Your auth token is like your login info - **String**|

Example:
```js
const Blooket = require('blooket');

const client = new Blooket();

(async () => {
    const login = await client.login('myEmail@gmail.com', 'myPassword123');
    const authToken = login.token;

    const account = await client.getAccountData(authToken);
    const name = account.name;

    const tokenAmount = 500;
    const xpAmount = 300;

    const addTokens = await client.addTokens(tokenAmount, xpAmount, name, authToken);

    console.log(addTokens);
    console.log('Added ' + tokenAmount + ' tokens and ' + xpAmount + ' XP to your account.');
})();
```

- **`createGame(hostName, isPlus, gameSetId, t_a, gameMode, blooketAuthToken)`**
### Parameters:
| name | description |
|-|-|
|*hostName*|Your Blooket Name - **String**|
|*isPlus*|Does your Blooket account have plus? - **`true` or `false`**|
|*gameSetId*|game set Id used to create a game - **String**|
|*t_a*|t = Time or a = Amount - **`Time` or `Amount`**|
|*blooketAuthToken*|Your auth token is like your login info - **String**|

Example:
```js
const Blooket = require('blooket');

const client = new Blooket();

(async () => {
    const login = await client.login('myemail@gmail.com', 'mypasssowrd123');
    const authToken = login.token;

    const account = await client.getAccountData(authToken);

    const hostName = account.name;
    const isPlus = account.plus == "Starter" ? false : true;
    const gameSetId = "600b1491d42a140004d5215a"; //https://www.blooket.com/set/600b1491d42a140004d5215a

    client.createGame(hostName, isPlus, gameSetId, 'Time', 'Gold', authToken);

    client.on('gameCreated', data => {
        console.log('Game created: ' + data.gamePin);
    });
})();
```

- **`createSet(authorName, description, isPrivate, title, blooketAuthToken)`**

**Returns `Promise`**

### Parameters:
| name | description |
|-|-|
|*authorName*|Your Blooket name - **String**|
|*description*|Write description about the game set - **String**|
|*isPrivate*|Set your game to private - **`true` or `false`**|
|*title*|Set a title for your game set - **String**|
|*blooketAuthToken*|Your auth token is like your login info - **String**|

Example:
```js
const Blooket = require('blooket')

const client = new Blooket();

(async () => {
    const login = await client.login('email', 'passwod');
    const authToken = login.token;

    const account = await client.getAccountData(authToken);

    const author = account.name;
    const desc = 'created from nodejs';
    const isPrivate = false;
    const title = 'created from nodejs';

    const set = await client.createSet(author, desc, isPrivate, title, authToken);

    console.log(set);    
})();
```

- **``favoriteSet(setId, blooketName, blooketAuthToken)``**

**Returns `Promise`**

### Parameters:
| name | description |
|-|-|
|*setId*|Game set Id - **String**|
|*blooketName*|Your Blooket account name - **String**|
|*blooketAuthToken*|Your auth token is like your login info - **String**|

Example:
```js
const Blooket = require('blooket')

const client = new Blooket();

(async () => {
    const login = await client.login('email', 'password');
    const authToken = login.token;

    const account = await client.getAccountData(authToken);
    
    const name = account.name;

    const setId = "619ffa8f76a076b181439489";
    
    const favorite = await client.favoriteSet(setId, name, authToken);
    
    console.log(favorite);
})();
```

- **``floodGames(gamePin, amount)``**
### Parameters:
| name | description |
|-|-|
|*gamePin*|Game pin to join a game - **String**|
|*amount*|Amount of bots you want to send - **Number**|

Example:
```js
const Blooket = require('blooket')

const client = new Blooket();

client.floodGames('972506', 100);

client.on('flood', data => {
    console.log('Joined game with name: ' + data.player);
});
```

- **`getAnswers(gamePin)`**

**Returns `Promise`**

### Parameters:
| name | description |
|-|-|
|*gamePin*|Game pin that is used to join a game - **String**|

Example:
```js
const Blooket = require('blooket')

const client = new Blooket();

(async () => {
    const gamePin = "753617";

    const answers = await client.getAnswers(gamePin);
    
    answers.forEach(answer => {
        console.log(answer);
    });
})();
```

- **`joinGame(gamePin, botName, blook)`**
### Parameters:
| name | description |
|-|-|
|*gamePin*|Game pin used to join a game - **String**|
|*botName*|Bot name used to join a game - **String**|
|*blook*|Blook used to play a game - **String**|

Example:
```js
const Blooket = require('blooket')

const client = new Blooket();

client.joinGame('342865', 'twst', 'Dog')

client.on('Joined', data => {
    console.log(`Joined game with name: ${data.name} \nJoined game with blook: ${data.blook}`)
});
```

- **``login(email, password)``**

**Returns `Promise`**

### Parameters:
| name | description |
|-|-|
|*email*|you can either put your blooket email or username to login - **String**|
|*password*|password used to logging into your blooket account - **String**|

Example:
```js
const Blooket = require('blooket')

const client = new Blooket();

(async () => {
    const login = await client.login('myemail@gmail.com', 'MyPassword123');

    console.log(login.token);
})();
```

- **`spamPlayGame(setId, blooketName, blooketAuthToken, amount)`**
### Parameters:
| name | description |
|-|-|
|*setId*|Game set Id - **String**|
|*blooketName*|Your Blooket account name - **String**|
|*blooketAuthToken*|Your auth token is like your login info - **String**|
|*amount*|Amount of bots you want to send - **Number**|

Example:
```js
const Blooket = require('blooket')

const client = new Blooket();

(async () => {
    const login = await client.login('email', 'password');
    const authToken = login.token;

    const account = await client.getAccountData(authToken);
    
    const setId = "619ffd8626263900c33b3db8";
    const name = account.name;


    client.spamPlayGame(setId, name, authToken, 100);

    client.on('spamPlays', data => {
        console.log('Played game: ' + data.setId);
    });
})();
```

- **``getAccountData(blooketAuthToken)``**

**Returns `Promise`**

### Parameters:
| name | description |
|-|-|
|*blooketAuthToken*|Your auth token is like your login info - **String**|


Example:
```js
const Blooket = require('blooket');

const client = new Blooket();

(async () => {
    const login = await client.login('email', 'password');
    const authToken = login.token;

    const getAccountData = await client.getAccount(authToken);

    console.log(getAccountData);
})();
```

- **``getGameData(gamePin)``**

**Returns `Promise`**

### Parameters:
| name | description |
|-|-|
|*gamePin*|Game pin used to join a game with - **String**|

Example:
```js
const Blooket = require('blooket');

const client = new Blooket();

(async () => {
    const gamePin = "352291";

    const gameData = await client.getGameData(gamePin);

    console.log(gameData);
})();
```

- **``getHistories(blooketAuthToken)``**

**Returns `Promise`**

### Parameters:
| name | description |
|-|-|
|*blooketAuthToken*|Your auth token is like your login info - **String**|

Example:
```js
const Blooket = require('blooket');

const client = new Blooket();

(async () => {
    const login = await client.login('email', 'password');
    const authToken = login.token;

    const histories = await client.getHistories(authToken);

    console.log(histories)
})();
```

- **``getHomeworks(blooketAuthToken)``**

**Returns `Promise`**

### Parameters:
| name | description |
|-|-|
|*blooketAuthToken*|Your auth token is like your login info - **String**|

Example:
```js
const Blooket = require('blooket');

const client = new Blooket();

(async () => {
    const login = await client.login('email', 'password');
    const authToken = login.token;

    const homeworks = await client.getHomeworks(authToken);

    console.log(homeworks)
})();
```

- **``deleteHomework(setId, blooketAuthToken)``**

**Returns `Promise`**

### Parameters:
| name | description |
|-|-|
|*setId*|Game set Id - **String**|
|*blooketAuthToken*|Your auth token is like your login info - **String**|

Example:
```js
const Blooket = require('blooket');

const client = new Blooket();

(async () => {
    const login = await client.login('email', 'password');
    const authToken = login.token;

    const setId = "";

    const deleteHomework = await client.deleteHomework(setId, authToken);

    console.log(deleteHomework)
})();
```

- **``getBlooks(blooketAuthToken)``**

**Returns `Promise`**

### Parameters:
| name | description |
|-|-|
|*blooketAuthToken*|Your auth token is like your login info - **String**|

Example:
```js
const Blooket = require('blooket');

const client = new Blooket();

(async () => {
    const login = await client.login('email', 'password');
    const authToken = login.token;

    const blooks = await client.getBlooks(authToken);

    console.log(blooks)
})();
```

- **``getTokens(blooketAuthToken)``**

**Returns `Promise`**

### Parameters:
| name | description |
|-|-|
|*blooketAuthToken*|Your auth token is like your login info - **String**|

Example:
```js
const Blooket = require('blooket');

const client = new Blooket();

(async () => {
    const login = await client.login('email', 'password');
    const authToken = login.token;

    const tokens = await client.getTokens(authToken);

    console.log(tokens)
})();
```

- **``getStats(blooketAuthToken)``**

**Returns `Promise`**

### Parameters:
| name | description |
|-|-|
|*blooketAuthToken*|Your auth token is like your login info - **String**|

Example:
```js
const Blooket = require('blooket');

const client = new Blooket();

(async () => {
    const login = await client.login('email', 'password');
    const authToken = login.token;

    const blooks = await client.getBlooks(authToken);

    console.log(blooks)
})();
```

- **``getUserData(name, blooketAuthToken)``**

**Returns `Promise`**

### Parameters:
| name | description |
|-|-|
|*name*|the name of the person you want to get user data for - **String**|
|*blooketAuthToken*|Your auth token is like your login info - **String**|

Example:
```js
const Blooket = require('blooket');

const client = new Blooket();

(async () => {
    const login = await client.login('email', 'password');
    const authToken = login.token;

    const userData = await client.getUserData('glizzz_y', authToken);

    console.log(userData)
})();
```

- **``giveGold(gamePin, playerName)``**
### Parameters:
| name | description |
|-|-|
|*gamePin*|Game pin used to join a game with - **String**|
|*playName*|Player name to give gold to - **String**|

**Note: This function only works for gold quest game mode!**

Example:
```js
const Blooket = require('blooket');

const client = new Blooket();

client.giveGold('189789', 'glizzy');

client.on('goldGiven', data => {
    console.log('Gold given to player: ' + data.player);
});
```

- **``stealGold(gamePin, playerName)``**
### Parameters:
| name | description |
|-|-|
|*gamePin*|Game pin used to join a game with - **String**|
|*playName*|Player name to steal gold from - **String**|

**Note: This function only works for gold quest game mode!**

Example:
```js
const Blooket = require('blooket');

const client = new Blooket();

client.stealGold('773710', 'glixzzy');

client.on('goldStolen', data => {
    console.log('Gold stolen from player: ' + data.player);
});
```

- **``endGame(gamePin)``**
### Parameters:
| name | description |
|-|-|
|*gamePin*|Game pin used to join a game with - **String**|

**Note: This function only works for racing game mode!**

Example:
```js
const Blooket = require('blooket');

const client = new Blooket();

client.endGame('861432');

client.on('gameEnded', data => {
    console.log('Ended game: ' + data.pin);
});
```

## Events
`gameCreated` - [createGame()](https://github.com/glixzzy/blooket-wrapper/blob/main/Documention.md#parameters-1)

- Emitted when the client creates a live game.
    - Returns an `Object`

`flood` - [floodGames()](https://github.com/glixzzy/blooket-wrapper/blob/main/Documention.md#parameters-5)

- Emitted when the client flood a game.
    - Returns an `Object`

`Joined` - [joinGame()](https://github.com/glixzzy/blooket-wrapper/blob/main/Documention.md#parameters-7)

- Emitted when the client joins a game.
    - Returns an `Object`

`spamPlays` - [spamPlayGame()](https://github.com/glixzzy/blooket-wrapper/blob/main/Documention.md#parameters-8)

- Emitted when the client spam plays a game.

`goldGiven` - [giveGold()](https://github.com/glixzzy/blooket-wrapper/blob/main/Documention.md#parameters-9)

- Emitted when the client gives gold to a user.
    - Returns an `Object`

`goldStolen` - [stealGold()](https://github.com/glixzzy/blooket-wrapper/blob/main/Documention.md#parameters-10)

- Emitted when the client steal gold from a player.
    - Returns an `Object`

`gameEnded` - [endGame()](https://github.com/glixzzy/blooket-wrapper/blob/main/Documention.md#parameters-11)

- Emitted when the client ends a game.
    - Returns an `Object`