# Bot

Possibly the minimum rule based chatbot implementation in plain JavaScript.

[Demo](https://paladin-t.github.io/)

## Usage

### Pattern configuration

```js
function setUserName (bot, matched) {
  bot.setUserName(matched[matched.length - 1]);
  bot.post('Call me Toby.');
}

var patterns = [
  {
    request: [ 'greetings' ],
    response: [ 'Hi.', 'Hello.' ],
    callback: function (bot) {
      if (!bot.getUserName()) {
        bot.setNextFailureHandler({
          response: [ 'Nice to meet you {USER_NAME}.' ],
          callback: setUserName
        });
        bot.post('What\'s your name?');
      }
    }
  },
  {
    request: [ 'hi' ],
    alias: [ 'greetings' ]
  },
  {
    request: [ 'hello' ],
    alias: [ 'greetings' ]
  },

  {
    request: [ 'what', 'your', 'name' ],
    response: [ 'Call me Toby.', 'I\'m Toby.' ]
  },

  {
    request: [ 'my', 'name' ],
    response: [ 'Nice to meet you {USER_NAME}.' ],
    callback: setUserName
  },
  {
    request: [ 'call', 'me' ],
    alias: [ 'my', 'name' ]
  }
];
```

### Chat

```js
var bot = new Bot.Bot();
patterns.forEach(function (pattern) {
  bot.learn(pattern);
});

bot.think('Hi!', function (rsp) {
  console.log(rsp);
});
```
