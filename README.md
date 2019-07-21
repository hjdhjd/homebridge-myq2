# homebridge-myq2
MyQ LiftMaster and Chamberlain Plugin for [HomeBridge](https://github.com/nfarina/homebridge) (API 2.0)

`homebridge-myq2` is a HomeBridge plugin to interact with MyQ Smart Garage door openers, made primarily by LiftMaster and Chamberlain.

There are two ways to be able to control a MyQ-compatible garage door opener through HomeKit:

1. LiftMaster and Chamberlain make a hardware HomeKit bridge also called Home Bridge (not to be confused with the open source [homebridge project](https://www.npmjs.com/package/homebridge)).
Unfortunately, some of us have encountered issues with the hardware bridge in a real world setting, where it either stops working or hangs for extended periods of time.
Others have encountered no issues and this solution works well.

2. A plugin for [homebridge](https://www.npmjs.com/package/homebridge) like this one that emulates the capabilities of a MyQ bridge.

Either solution will provide a complete solution to automating your garage door and you'll soon be automating your home with HomeKit like you always dreamed of. :)

# What makes this plugin different than the other plugins out there for MyQ support?
Both [homebridge-liftmaster2](https://github.com/luisiam/homebridge-liftmaster2) and [homebridge-chamberlain](https://github.com/caseywebdev/homebridge-chamberlain) exist as good
options, if you prefer. This plugin is based on `homebridge-liftmaster2` with additional bugfixes and contributions by others. The intent is to keep this plugin up-to-date and
incorporate additional capabilities as-needed without overly bloating it.

# Installation
If you are new to Homebridge, please first read the Homebridge [documentation](https://www.npmjs.com/package/homebridge).
If you are running on a Raspberry, you will find a tutorial in the [homebridge-punt Wiki](https://github.com/cflurin/homebridge-punt/wiki/Running-Homebridge-on-a-Raspberry-Pi).

Install homebridge:
```sh
sudo npm install -g homebridge
```
Install homebridge-myq2:
```sh
sudo npm install -g homebridge-myq2
```

# Configuration
Add the platform in `config.json` in your home directory inside `.homebridge`.

```js
"platforms": [{
    "platform": "MyQ2",
    "email": "email@email.com",
    "password": "password"
}]
```

### Advanced Configuration (Optional)
This step is not required. HomeBridge with API 2.0 can handle configurations in the HomeKit app.
```
"platforms": [{
    "platform": "MyQ2",
    "name": "MyQ",
    "email": "email@email.com",
    "password": "password",
    "openDuration": 15,
    "closeDuration": 25,
    "polling": true,
    "longPoll": 300,
    "shortPoll": 5,
    "shortPollDuration": 120,
    "gateways": ["My Home"]
}]

```

| Fields            | Description                                      | Default | Required |
|-------------------|--------------------------------------------------|---------|----------|
| platform          | Must always be `MyQ2`.                           |         | Yes      |
| name              | For logging purposes.                            |         | No       |
| email             | Your MyQ account email.                          |         | Yes      |
| password          | Your MyQ account password.                       |         | Yes      |
| openDuration      | Time in `s` to open garage door completely.      | 15      | No       |
| closeDuration     | Time in `s` to close garage door completely.     | 25      | No       |
| polling           | State polling.                                   | false   | No       |
| longPoll          | Normal polling interval in `s`.                  | 300     | No       |
| shortPoll         | Polling interval in `s` when door state changes. | 5       | No       |
| shortPollDuration | Duration in `s` to use `shortPoll`.              | 120     | No       |
| gateways          | Array of gateway IDs or names to add.            | []      | No       |

