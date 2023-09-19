
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
`agentUnready()` Terminate agent from receive incoming call.
<!-- div:right-panel -->

```js
  this.sociomile.agentUnready()
```

<!-- div:title-panel -->
### Show list break
<!-- div:left-panel -->
`showBreaks()` Terminate agent from receive incoming call.
<!-- div:right-panel -->

```js
  this.sociomile.showBreaks()
```

<!-- div:title-panel -->
### Agent Begin break
<!-- div:left-panel -->
`beginBreak()` Terminate agent from receive incoming call.
<!-- div:right-panel -->

```js
  this.sociomile.beginBreak()
```

<!-- div:title-panel -->
### Ended break
<!-- div:left-panel -->
`endBreak()` Terminate agent from receive incoming call.
<!-- div:right-panel -->

```js
  this.sociomile.endBreak()
```


