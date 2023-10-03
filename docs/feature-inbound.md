
# Avalaible Feature
## Instance function
<!-- panels:start -->
  ```js 
  this.sociomile = new SocioVoice.Init({
    base_url:`${self.endPoint}`,secret_key:`${self.secretKey}`
  })
  ```

<!-- div:title-panel -->
### Agent Ready (Receive incoming call)
<!-- div:left-panel -->
`agentReady()` Makes an agent ready to receive incoming.
<!-- div:right-panel -->

```js
  this.sociomile.agentReady()
```


<!-- div:title-panel -->
### Agent Unready
<!-- div:left-panel -->
`agentUnready()` Unready agent become offline.
<!-- div:right-panel -->

```js
  this.sociomile.agentUnready()
```

<!-- div:title-panel -->
### Show list break
<!-- div:left-panel -->
`showBreaks()` Fetch list breaks options.
<!-- div:right-panel -->

```js
  this.sociomile.showBreaks()
```

<!-- div:title-panel -->
### Agent Begin break
<!-- div:left-panel -->
`beginBreak(idBreak)` Begin break based on break selected ID.
<!-- div:right-panel -->

```js
  this.sociomile.beginBreak(idBreak)
```

<!-- div:title-panel -->
### Ended break
<!-- div:left-panel -->
`endBreak()` End break agent become available.
<!-- div:right-panel -->

```js
  this.sociomile.endBreak()
```

<!-- div:title-panel -->
### Hangup incoming call
<!-- div:left-panel -->
`iHangup()` Terminate agent from receive incoming call.
<!-- div:right-panel -->

```js
  this.sociomile.iHangup()
```


