# Tutorials



In this section you'll find links to the individual tutorails and videos on our [YouTube channel](https://www.youtube.com/c/flltools)

## Getting started

In this section you will find some basic tutorials on how to get started with development for the software suite.
Most of it is tailored to get you familiar with creating loosely coupled modules. Don't worry, we start out slow.

For this section we even created some YouTube videos with lots of additional information:

### 1. Installation

[![Installation](https://img.youtube.com/vi/VfzPSmkNXWI/0.jpg)](https://www.youtube.com/watch?v=YVfzPSmkNXWI)

Episode 1. [Installation](https://www.youtube.com/watch?v=VfzPSmkNXWI)
A short introduction on how to get the code running on your own computer.

Links used:
* [nodejs.org](https://nodejs.org/)
* [Git for Windows](https://git-scm.com/download/win)
* [fllscoring](https://github.com/firstLegoLeague/fllscoring)


### 2. MHub

[![MHub](https://img.youtube.com/vi/TRSJUfSS_LM/0.jpg)](https://www.youtube.com/watch?v=TRSJUfSS_LM)

Episode 2. [MHub](https://www.youtube.com/watch?v=TRSJUfSS_LM)
Introduction into MHub

Links used:
* [MHub](https://npmjs.com/mhub)
* [displaySystem](https://github.com/firstLegoLeague/displaySystem)
* [clock](https://github.com/firstLegoLeague/clock)
* [mq-protocols](https://github.com/firstLegoLeague/mq-protocols)


### 3. Chat Application

[![Chat Application](https://img.youtube.com/vi/OVQxqZ4bQIM/0.jpg)](https://www.youtube.com/watch?v=OVQxqZ4bQIM)

Episode 3. [Chat Application](https://www.youtube.com/watch?v=OVQxqZ4bQIM)
create a basic communication between two independent modules.

Links used:
* [Visual Studio Code](https://code.visualstudio.com)
* [MHub documentation](https://github.com/poelstra/mhub)

Code used:
* index.js
```
var MClient = require("mhub").MClient;
var UI = require('./ui');

var client = new MClient("ws://localhost:13900");

var user = process.argv[2];

client.on("open", function() {
    client.subscribe("default");
});

var ui = new UI();
client.on("message", function(message) {
    ui.writeLine(message.data);
});

ui.on('line', function(line) {
    var data = '['+user+'] ' + line;
    client.publish('default', 'message', data);
});
```
* ui.js
```
var events = require('events');
var util = require('util');
var readline = require('readline');
 
 
function UI() {
    var self = this;
    this.rl = readline.createInterface({
        input: process.stdin,
        output: process.stdout
    });
    this.rl.setPrompt('-> ');
    this.rl.on('line', function(line) {
        readline.moveCursor(process.stdout, 0, -1);
        readline.clearLine(process.stdout, 0);
        self.emit('line', line);
    });
    this.rl.prompt(true);
}
 
util.inherits(UI, events.EventEmitter);
 
UI.prototype.writeLine = function(str) {
    process.stdout.clearLine();
    process.stdout.cursorTo(0);
    console.log(str);
    this.rl.prompt(true);
}
 
module.exports = UI;
```

### 4. Chat GUI

[![Chat GUI](https://img.youtube.com/vi/Yx1VF1vb6eA/0.jpg)](https://www.youtube.com/watch?v=Yx1VF1vb6eA)

Episode 4. [Chat GUI](https://www.youtube.com/watch?v=Yx1VF1vb6eA)
In this episode we extend the chat application to something that looks more like a real web application

Files used:
* index.js (changes from ep3)
```
var MClient = require("mhub").MClient;
var UI = require('./ui');

var client = new MClient("ws://localhost:13900");

var user = process.argv[2];

client.on("open", function() {
    client.subscribe("default");
});

var ui = new UI();
client.on("message", function(message) {
    var data = '['+message.data.user+'] ' + message.data.line;
    ui.writeLine(data);
});

ui.on('line', function(line) {
    var data = {
        user: user,
        line: line
    };
    client.publish('default', 'message', data);
});
```
* index.html
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>MHub chat</title>
    <style>
        .user {
            font-weight: bold;
        }
        .user::after {
            content: ': ';
        }
    </style>
</head>
<body>
    <div id="messages"></div>
    <form id="input">
        <input type="text" name="user">
        <input type="text" name="line">
        <button type="submit">Send</button>
    </form>
    <script src="main.js"></script>
</body>
</html>
```
* main.js
```
var ws = new WebSocket('ws://localhost:13900');

ws.onopen = function() {
    ws.send(JSON.stringify({
        type: "subscribe",
        node: "default"
    }));
};

ws.onmessage = function(raw) {
    var envelope = JSON.parse(raw.data);
    if (envelope.type === 'message') {
        var p = document.createElement('p');
        p.innerHTML = '<span class="user">'+envelope.data.user+'</span>'+envelope.data.line;
        document.getElementById('messages').appendChild(p);
    }
};

document.getElementById('input').addEventListener('submit',function(e) {
    var line = this.elements.line.value;
    var user = this.elements.user.value;
    ws.send(JSON.stringify({
        type: "publish",
        node: "default",
        topic: "message",
        data: {
            user: user,
            line: line
        }
    }));
    this.elements.line.value = '';
    e.preventDefault();
});
```
