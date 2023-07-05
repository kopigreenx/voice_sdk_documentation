
# Avalaible Feature
## Instance function
<!-- panels:start -->
<!-- div:title-panel -->
### Dial / make new call session
<!-- div:left-panel -->
`dial()` Makes an outgoing multimedia call.

- number: `String`  => **required**    (Phone number)
- internal_id: `String` => **optional** (Internal ID optional to sent back via webhook)
- params: `Object` => **optional**

<!-- div:right-panel -->

```js
  const session = this.sociomile.dial('082xxxxxx','')
```


<!-- div:title-panel -->
### Hangup
<!-- div:left-panel -->
`hangup(session)` Terminate the current session regardless its direction or state.

- session: `Object`  => **required**
<!-- div:right-panel -->

```js
  const session = this.sociomile.dial('082xxxxxx','',{})
  this.sociomile.hangup(session)
```


<!-- div:title-panel -->
### DTMF
<!-- div:left-panel -->
`sendDTMF(session,code)`  Send one or multiple DTMF tones making use of SIP INFO method.

- session: `Object`  => **required**
- code: `String`  => **required**
<!-- div:right-panel -->
<!-- tabs:start -->
#### **Send DTMF code in one action**
```js
  const session = this.sociomile.dial('082xxxxxx','',{})
  this.sociomile.sendDTMF(session,'*123#')
```
#### **Send DTMF with step**
```js
  const session = this.sociomile.dial('082xxxxxx','',{})
  this.sociomile.sendDTMF(session,'*')
  this.sociomile.sendDTMF(session,'1')
  this.sociomile.sendDTMF(session,'2')
  this.sociomile.sendDTMF(session,'3')
  this.sociomile.sendDTMF(session,'*')
```
<!-- tabs:end -->


<!-- div:title-panel -->
### Hold
<!-- div:left-panel -->
`hold(session)` Puts the call on hold by sending a Re-INVITE or UPDATE SIP request.

- session: `Object`  => **required**
<!-- div:right-panel -->

```js
  const session = this.sociomile.dial('082xxxxxx','',{})
  this.sociomile.hold(session)
```


<!-- div:title-panel -->
### Unhold
<!-- div:left-panel -->
`unhold(session)`  Resumes the call from hold by sending a Re-INVITE or UPDATE SIP request.

- session: `Object`  => **required**
<!-- div:right-panel -->

```js
  const session = this.sociomile.dial('082xxxxxx','',{})
  this.sociomile.unhold(session)
```
<!-- panels:end -->



