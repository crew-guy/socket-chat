# socket-chat
Socket IO's "Hello world" project

- client side

    ```jsx
    const socket = io('ws://localhost:8080')

    socket.on('message', message =>
    {
        const li = document.createElement('li');
        li.innerText = message
        document.querySelector('ul').appendChild(li);
    })

    document.querySelector('button').onclick = () => {
        socket.emit('message', document.querySelector('input').value)
    };
    ```

- server side

    ```jsx
    const http = require('http').createServer();

    const io = require('socket.io')(http, {
        cors:{origin:"*"}
    })

    io.on('connection', (socket) =>
    {
        console.log('a user connected');
        socket.on('message', (message) =>
        {
            io.emit('message', `${socket.id.substring(0, 5)} said ${message} !`)
        })
    })

    http.listen(8080, () =>
    {
        console.log('Listening on port 8080');
    })
    ```
