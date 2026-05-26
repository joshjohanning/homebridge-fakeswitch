# "Dummy Switches" Plugin

> [!TIP]
> This is a drop-in replacement for the original [`homebridge-fakeswitch`](https://github.com/thncode/homebridge-fakeswitch) plugin with explicit Homebridge 2 support. See [Migrating from `homebridge-fakeswitch`](#migrating-from-homebridge-fakeswitch) for setup steps.

Example config.json:

```json
    "accessories": [
        {
          "accessory": "FakeSwitch",
          "name": "My Switch 1"
        }
    ]

```

With this plugin, you can create any number of fake switches that will do nothing when turned on (and will automatically turn off right afterward, simulating a stateless switch). This can be very useful for advanced automation with HomeKit scenes.

For instance, the Philips Hue app will automatically create HomeKit scenes for you based on Hue Scenes you create. But what if you want to create a scene that contains both Philips Hue actions and other actions (like turning on the coffee maker with a WeMo outlet)? You are forced to either modify the Hue-created scene (which can be a HUGE list of actions if you have lots of lights) or build your own HomeKit lighting scenes.

Instead, you can link scenes using these dummy switches. Let's say you have a Hue Scene called "Rise and Shine" that you want to activate in the morning. And you have also setup the system HomeKit scene "Good Morning" to turn on your coffee maker and disarm you security system. You can add a single dummy switch to your Good Morning scene, then create a Trigger based on the switching-on of the dummy switch that also activates Rise And Shine.

## Stateful Switches

The default behavior of a dummy switch is to turn itself off one second after being turned on. However you may want to create a dummy switch that remains on and must be manually turned off. You can do this by passing an argument in your config.json:

```json
    "accessories": [
        {
          "accessory": "FakeSwitch",
          "name": "My Stateful Switch 1",
          "stateful": true
        }
    ]

```

## Reverse Switches

You may also want to create a dummy switch that turns itself on one second after being turned off. This can be done by passing the 'reverse' argument in your config.json:

```json
    "accessories": [
        {
          "accessory": "FakeSwitch",
          "name": "My Stateful Switch 1",
          "reverse": true
        }
    ]

```

## Migrating from `homebridge-fakeswitch`

This package can be used as a drop-in replacement for the original [`homebridge-fakeswitch`](https://www.npmjs.com/package/homebridge-fakeswitch) plugin.

This fork still registers the Homebridge accessory as:

```json
"accessory": "FakeSwitch"
```

Existing Homebridge config entries can stay the same. Your existing HomeKit accessories should keep their identity as long as you do not delete cached accessories, rename existing switches, or remove/re-pair the Homebridge bridge.

### Safe migration steps

1. Back up Homebridge from the Homebridge UI.
2. Stop Homebridge:

   ```bash
   sudo hb-service stop
   ```

3. Remove the original plugin:

   ```bash
   sudo hb-service remove homebridge-magichome-dynamic-platform
   ```

4. Install this fork:

   ```bash
   sudo hb-service add @joshjohanning/homebridge-magichome-dynamic-platform
   ```

5. Start Homebridge:

   ```bash
   sudo hb-service start
   ```

6. Check the Homebridge logs:

   ```bash
   sudo hb-service logs
   ```

7. Verify your existing MagicHome lights still work in Apple Home.

### Important notes

Do not change existing plugin config from `FakeSwitch` during migration.

Do not remove cached FakeSwitch accessories from Homebridge unless you intentionally want HomeKit to recreate them. Removing cached accessories may break room assignments, scenes, and automations that reference those switches.

### Updating this fork

When a new version is published to npm, update it from the Homebridge UI, or run:

```bash
sudo hb-service add @joshjohanning/homebridge-fakeswitch
sudo hb-service restart
```
