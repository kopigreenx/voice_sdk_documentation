## SDK Library

you need ask first for requesting SDK library to Ivosights for `sociomileVoice-1.0.0.min.js`

```html
  <script src='./sociomileVoice-1.0.0.min.js'></script>
```

## Example usage

this is example SDK using `vue.js` 

```html
<!-- index.html -->

<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Sociomile Voice SDK</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-9ndCyUaIbzAi2FUVXJi0CjmCapSmO7SnpJef0486qhLnuZ2cdeRhO02iuK6FUUVM" crossorigin="anonymous">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/prism/9000.0.1/themes/prism-tomorrow.min.css" integrity="sha512-kSwGoyIkfz4+hMo5jkJngSByil9jxJPKbweYec/UgS+S1EgE45qm4Gea7Ks2oxQ7qiYyyZRn66A9df2lMtjIsw==" crossorigin="anonymous" referrerpolicy="no-referrer" />
  </head>
  <body>
    <nav class="navbar navbar-expand-md navbar-dark fixed-top bg-dark mb-2">
      <div class="container">
        <a class="navbar-brand" href="#">Sociomile Voice SDK</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <a class="nav-link active" aria-current="page" href="#">Home</a>
            </li>
          </ul>
          <form class="d-flex" role="search">
            <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
            <button class="btn btn-outline-success" type="submit">Search</button>
          </form>
        </div>
      </div>
    </nav>

    <div class="container" style="margin-top:80px;">
      <div id="app">
        <h2>Example Usage</h2>
        <div class="col-lg-8 px-0">
          <div class="bd-example-snippet bd-code-snippet"><div class="bd-example m-0 border-0">
            <div class="input-group">
              <span class="input-group-text">Endpoint & Secret Key</span>
              <input type="text" aria-label="Endpoint" class="form-control" v-model="endPoint">
              <input type="text" aria-label="Secret Key" class="form-control" v-model="secretKey">
              <button class="btn btn-primary" @click="connect" type="button" :disabled="isAuth && isRegistered">Connect</button>
            </div>  
          </div>
          <hr class="col-12 my-4" v-if="isAuth && isRegistered">
          <div class="input-group" v-if="isAuth && isRegistered">
            <span class="input-group-text">Phone number</span>
            <input type="text" aria-label="number" class="form-control" v-model="phoneNumber" :disabled="isDial">
            <!-- DIAL FUNCTION-->
            <button href="javascript:void(0)" @click="dial" class="btn btn-primary" :disabled="isDial || !isAuth || !isRegistered">Dial</button>
            <!-- HANGUP FUNCTION-->
            <button href="javascript:void(0)" @click="hangup" class="btn btn-danger" :disabled="!isDial || !isAuth || !isRegistered">Hangup</button>
            <!-- HOLD FUNCTION-->
            <button href="javascript:void(0)" @click="holdUnhold" class="btn btn-outline-warning" :disabled="!callConnected">{{ isOnHold ? 'Unhold' : 'Hold'}}</button>
          </div> 
        </div> 
      </div> 
    </div> 

    <script src='./dist/sociomileVoice-1.0.0.min.js'></script>
    <script src="https://cdn.jsdelivr.net/combine/npm/vue@2.6.10,npm/vue-i18n@8.21.0/dist/vue-i18n.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js" integrity="sha384-geWF76RCwLtnZ8qwWowPQNguL3RmwHVBC9FhGdlKrxdiJJigb/j/68SIy3Te4Bkz" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/@editorjs/editorjs@latest"></script>
    
    <script src="https://cdnjs.cloudflare.com/ajax/libs/prism/9000.0.1/prism.min.js" integrity="sha512-UOoJElONeUNzQbbKQbjldDf9MwOHqxNz49NNJJ1d90yp+X9edsHyJoAs6O4K19CZGaIdjI5ohK+O2y5lBTW6uQ==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/prism/9000.0.1/components/prism-javascript.min.js" integrity="sha512-yvw5BDA/GQu8umskpIOBhX2pDLrdOiriaK4kVxtD28QEGLV5rscmCfDjkrx52tIgzLgwzs1FsALV6eYDpGnEkQ==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
    <script src="https://momentjs.com/downloads/moment.js" crossorigin="anonymous" referrerpolicy="no-referrer"></script>

    <script type="module">
      new Vue({
        el: "#app",
        data: () => ({
          endPoint: '<ENDPOINT>',
          secretKey: '<SECRET_KEY>',
          phoneNumber: '',
          isAuth: false,
          isRegistered: false,
          isDial : false,
          callConnected : false,
          isOnHold : false,
          callSession: null,
          sociomile: null
        }),
        mounted() {
          
        },
        methods: {
          connect(){
            var self = this
            this.sociomile = new SocioVoice.Init({
                base_url:`${self.endPoint}`,secret_key:`${self.secretKey}`
            })
            
            this.sociomile.on('sociomileEvent',function (event) {
              // ALL EVENT WILL FIRE HERE
              console.log('sociomileEvent', event)
              var el = document.getElementById('statusText')
              el.prepend(`(${event.event_group})`+event.type + ' => ' + event.message+ ' ('+ moment().format('DD/MM/YYYY, H:mm:ss')+')\n');

              if(event.event_group === 'ended' || event.event_group === 'failed'){
                self.isDial = false
                self.callConnected = false
              }
              if(event.event_name === 'on_registered'){
                self.isRegistered = true
              }
              if(event.event_name === 'on_disconnected'){
                self.isRegistered = false
              }
              if(event.event_name === 'accepted'){
                self.callConnected = true
              }
              if(event.event_group === 'authentication'){
                self.isAuth = event.data.authenticated
              }
            })
            this.sociomile.start()
          },
          dial(){
            this.callSession = this.sociomile.dial(this.phoneNumber,'asdadasas111',{abc:'asdsad',dfg:'asdasd'})
            if(this.callSession){
                this.isDial = true
                this.callSession.connection.addEventListener('track', (e) => {
                    const audi = new Audio()
                    audi.srcObject = e.streams[0]
                    audi.play()
                })
            }
          },
          hangup () {
            this.sociomile.hangup(this.callSession)
            this.isDial = false
          },
          holdUnhold () {
            if(this.isOnHold){
              this.sociomile.unhold(this.callSession)
              this.isOnHold = false
            } else {
              this.sociomile.hold(this.callSession)
              this.isOnHold = true
            }
          }
        },
      })
    </script>
  </body>
</html>
```

## Explanation of the example above

<!-- panels:start -->
<!-- div:title-panel -->
### Load SDK Library

<!-- div:left-panel -->
First thing first you need the SDK library to include in your project  
<!-- div:right-panel -->
```html
<!-- index.html -->

<script src='./sociomileVoice-1.0.0.min.js'></script>
```
<!-- panels:end -->

<!-- panels:start -->
<!-- div:title-panel -->
### Define state variable

<!-- div:left-panel -->
you can use any name you want this state variable based on example

<!-- div:right-panel -->
```js
data: () => ({
  endPoint: '<ENDPOINT>',
  secretKey: '<SECRET_KEY>',
  phoneNumber: '',
  isAuth: false,
  isRegistered: false,
  isDial : false,
  callConnected : false,
  isOnHold : false,
  callSession: null,
  sociomile: null
})
```
<!-- panels:end -->
<!-- panels:start -->
<!-- div:title-panel -->
### Initialize SDK instance

<!-- div:left-panel -->
add Instance `new SocioVoice.Init` to state variable `sociomile` you can use any name you want
- base_url: `String`
- secret_key: `String`
<!-- div:right-panel -->
```js
this.sociomile = new SocioVoice.Init({
  base_url:`${self.endPoint}`,
  secret_key:`${self.secretKey}`
})
```
<!-- panels:end -->

<!-- panels:start -->
<!-- div:title-panel -->
### Listening event 
<!-- div:left-panel -->
this function is mandatory to add cause all event like authentication, call progress ETC goes here.

Structure Event

- type: `String`
- event_group: `String`
- event_name: `String`
- message: `String`
- data: `Object`
<!-- div:right-panel -->
```js
this.sociomile.on('sociomileEvent',function (event) {
  // ALL EVENT GOES HERE
  // 
  //{
  // "type": "auth",
  // "event_group": "authentication",
  // "event_name": "on_auth_success",
  // "message": "Authentication success",
  // "data": {
  //   "authenticated": true
  //}
})
```

<!-- panels:end -->
### Event list

<!-- tabs:start -->

#### **Structure**

```text
└── event_group
    └── event_name
```

#### **Events**

```text

└── authentication
    ├── on_auth_success       => success authentication will fire when has valid endpoint & secret key
    └── on_auth_failed        => failed authentication will fire when secret key or endpoint not valid

└── register
    ├── on_connecting         => Process connecting telephony system
    ├── on_connected          => successfully connected telephony system
    ├── on_registered         => successfully registered to telephony sytem
    ├── on_unregistered       => will fire when connection issue
    ├── on_registrationFailed => will fire when wrong credential on backend
    └── on_disconnected       => will fire when connection issue

└── progress
    ├── on_initiate_failed    => will fire when authentication failed and still want to dial
    ├── on_initiate_success   => will fire when start dial & authentication success
    ├── on_newRTCSession      => in this event we can define is incoming call / outgoing call see on `data` object
                                  'data': {
                                    "originator": "local", local /remote
                                    "direction": "outgoing"
                                  }

                                  local : outgoing
                                  remote : incoming

    ├── on_connecting         => call connecting
    ├── on_sending            => call sending
    └── on_progress           => Phone will be start ringing

└── established
    ├── on_confirmed          => call confirmed by customer
    └── on_accepted           => call successfully accept on local 

└── failed
    ├── on_rejected           => call rejected
    └── on_cancelled          => call cancelled

└── hold
    ├── on_start_hold         => call hold
    └── on_end_hold           => call unhold

└── ended
    ├── on_remote_ended       => call ended by customer
    └── on_local_ended        => call ended by agent
```

<!-- tabs:end -->



