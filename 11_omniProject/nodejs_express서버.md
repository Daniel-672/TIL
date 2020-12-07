### - server.js

```bash
const express = require('express')
const path = require('path')
const { get } = require('request')

const app = express()

app.use(express.json())
app.use(express.urlencoded({ extended: true }))


app.use(express.static(path.join(__dirname, './models')))
app.use(express.static(path.join(__dirname, './dist')))
app.use(express.static(path.join(__dirname, '/')))

app.get('/index', (req, res) => res.sendFile(path.join(viewsDir, 'index.html')))

app.listen(4000, () => console.log('Listening on port 4000!'))

function request(url, returnBuffer = true, timeout = 10000) {
  return new Promise(function(resolve, reject) {
    const options = Object.assign(
      {},
      {
        url,
        isBuffer: true,
        timeout,
        headers: {
          'User-Agent': 'Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.181 Safari/537.36'
        }
      },
      returnBuffer ? { encoding: null } : {}
    )

    get(options, function(err, res) {
      if (err) return reject(err)
      return resolve(res)
    })
  })
}
```



### - 실행

```bash
npm install express
npm install request --save

npm init -y
npm i jquery
```

