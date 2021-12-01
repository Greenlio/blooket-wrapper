# blooket-wrapper

## About
A node.js wrapper for the Blooket API

The documentation can be found [here](https://github.com/glixzzy/blooket-wrapper/blob/main/Documentation.md)

## Installation

```sh-session
npm install discord.js
```

# Usage

```js
const Blooket = require('blooket')

const client = new Blooket();

client.joinGame('342865', 'twst', 'Dog')

client.on('Joined', data => {
    console.log(`Joined game with name: ${data.name} \nJoined game with blook: ${data.blook}`)
});
```