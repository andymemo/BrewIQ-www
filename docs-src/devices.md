# Devices

The **Devices** page has three tabs: **Fermentation**, **Temp Control**, and **Integration**. What you see depends on your permissions.

Two important framing points before you connect anything:

- BrewIQ does **not** talk Bluetooth or discover hardware on your local network. Fermentation sensors (Tilt, iSpindel, RAPT Pill) connect by having your own bridge/app POST readings to a BrewIQ URL - you configure the device's *own* app to point at BrewIQ, not the other way around.
- Two temperature-controller brands are supported: **Grainfather** (the Glycol Chiller Adapter) and the **RAPT WiFi Temperature Controller**. There's no generic or vendor-neutral controller support (for example Inkbird).

## Integration tab - set this up first

### Device API Key (for Tilt / iSpindel / RAPT Pill)

![The Devices Integration tab showing the Device API Key panel and Grainfather MQTT Account panel](images/devices-integration.png)

Click **Generate Key** to create your device API key. This gives you a set of copyable **Device URLs**, one per device type:

```
{your BrewIQ URL}/api/devices/ingest/tilt/{key}
{your BrewIQ URL}/api/devices/ingest/ispindel/{key}
{your BrewIQ URL}/api/devices/ingest/rapt/{key}
```

Copy the URL for your device type and paste it into that device's own app/bridge wherever it asks for a logging or webhook URL:

- **Tilt** - use the Tilt app's "Custom function"/custom logging URL field (the same mechanism apps like Brewer's Friend use), or a Bluetooth relay such as TiltPi configured the same way.
- **iSpindel** - its HTTP upload configuration.
- **RAPT Pill** - its cloud webhook configuration.

The key is embedded in the URL itself, because most of these devices/bridges only support a single URL field with no separate header field. If your tool *does* support a custom header, you can instead POST to the bare `/api/devices/ingest/{type}` path with the key in an `X-Api-Key` header.

Anyone with one of these URLs can post readings to your account, so treat them like a password. Click the eye icon to reveal the full key when you need to copy it. If a key ever leaks, click **Regenerate Key** (you'll need to re-confirm your password, and every device's URL changes immediately).

There's no "add a Tilt" step beyond this - a Tilt (or iSpindel/RAPT Pill) shows up automatically on the **Fermentation** tab the first time it successfully posts a reading.

### Grainfather MQTT Account

To use Grainfather temperature control, connect your Grainfather account first:

1. Open the **Grainfather User ID** field and enter the numeric account ID shown in the Grainfather app.
2. Click **Save**.
3. Once connected, the panel shows a status badge - **Connected**, **Disconnected**, or **Paused** - and buttons to **Connect**/**Disconnect** the link or **Remove Account** entirely.

This connects your *account*, not an individual device - you still need to register each device (below).

### RAPT Account

To use a RAPT temperature controller, connect your RAPT account first:

1. In the RAPT app, go to **My Account → API Secrets** and create an API Secret. RAPT shows it only once, so copy it straight away.
2. In BrewIQ, enter your **RAPT account username** (usually your email address) and paste the **API Secret**.
3. Click **Save**.
4. Once connected, the panel shows a **Connected** or **Disconnected** badge, with buttons to **Connect**/**Disconnect** the link or **Remove Account** entirely.

As with Grainfather, this connects your *account*, not an individual controller. You then import the controllers you want from the **Temp Control** tab (below). If the account won't connect, check that both the username and the API Secret are filled in.

### Debug panels

There are collapsible **debug panels** on this tab - a **Live Ingestion Log** for gravity devices, a **MQTT Connection Log** for Grainfather, and a log of **RAPT API calls**. They're useful when you're setting up hardware for the first time and want to confirm readings are actually arriving. They only show the most recent activity; they aren't a permanent history.

## Fermentation tab

![The Fermentation tab showing device cards for a RAPT Pill and several Tilts](images/devices-fermentation.png)

Every gravity/temperature sensor (Tilt, iSpindel, RAPT Pill) shows up here as a card once it's reported at least one reading. Each card shows:

- Name - Tilt devices also show a colour swatch matching the physical Tilt's colour
- Online/offline status (a device is considered online if it's reported within the last 30 minutes)
- Device type and ID (e.g. "Tilt · Red")
- Current gravity and temperature
- For Tilt: the "Beer" name set in the Tilt app (Tilt has no battery sensor, so this fills that slot). For iSpindel/RAPT Pill: battery %
- First seen / last seen timestamps
- A **Linked Brew Session** selector

Icon buttons per card let you: toggle email alerts (bell), view the raw reading history (list), view a fermentation graph if it's linked to a session with readings (line chart), rename the device (pencil), or delete it (trash). Deleting keeps the reading history by default - there's a separate "also permanently delete history" option if you want it fully gone.

### Linking a device to a brew session

Use the **Linked Brew Session** dropdown on the device card to attach it to an active session (anything not yet packaged). Once linked, every gravity reading that comes in is logged against that session and can automatically kick off fermentation tracking on it - see [Brew Sessions](brew-sessions.md).

## Temp Control tab

Both brands of temperature controller appear together here, one card each. A brew session can be linked to only **one** controller at a time (Grainfather *or* RAPT), so to switch a session to a different controller, unlink the first one.

### Adding a device

Click **Add Device** and choose the brand.

**Grainfather** - fill in:

- **Serial (esp_chip_id)** - copy this exactly from the Grainfather app
- **Friendly name** - whatever you want to call it (e.g. "GCA1")
- **Type** - **Temp Controller** (a Glycol Chiller Adapter) or **Brew Unit** (a G70). Note: Brew Unit devices are tracked for identification only - BrewIQ doesn't send them commands.

There's no auto-discovery for Grainfather - you have to register the serial manually.

**RAPT** - connect your RAPT account first (see the Integration tab above), then choose **RAPT**. BrewIQ lists the controllers on your RAPT account that haven't been added yet. Tick the ones you want and import them. A controller you removed earlier reappears in this list so you can add it back.

### Grainfather: monitoring and control

![Two Temp Control device cards, one online and cooling, one offline in manual mode](images/devices-temp-control.png)

Each Temp Control card shows current temp, target temp, a linked gravity reading (if you've paired one), and a status icon for heating/cooling/paused/idle. Click **View & control** to open the full device detail view, where you can:

- Click the target temperature to open **Set Target Temperature** and change it
- Use the +/- buttons for quick nudges (changes commit to the device after a short delay)
- Set **Temp Mode**: Heating & Cooling, Cooling Only, Heating Only, or Pause Heating & Cooling
- Adjust **Hysteresis** and **Temperature Calibration**
- Pick a **Gravity source** - link a Fermentation-tab device so its gravity reading shows alongside temperature
- Set a **Linked Brew Session**
- View a **Temperature & gravity history** chart (logged roughly every 15–30 minutes)

If a Grainfather-app brew session is actively controlling the device, BrewIQ shows controls as read-only until that session ends. If you've manually overridden the schedule, a **Resume schedule** button clears the override.

![The Grainfather device detail view showing current temperature, device settings and a temperature history chart](images/devices-temp-control-detail.png)

### Grainfather: fermentation schedule

This device-level schedule is a BrewIQ-side schedule, not something synced to the device's own onboard programming. You add steps (label, target temp, duration, optional note), and advance through them yourself with a **Skip to {step}** button - clicking it pushes that step's target temperature to the device immediately. It's a manual aid for following a plan, not an automated timer.

If you'd rather have BrewIQ run the schedule for you, build it on the brew session instead and turn on **Managed Mode** - see [Fermentation Steps](brew-sessions.md#fermentation-steps-the-schedule). That works with either brand of controller.

### RAPT controllers

A RAPT controller card shows an **ONLINE** or **OFFLINE** badge and when it was last seen. Click it to open a view that mirrors the controller's own screen: the current temperature, and the **Target Temp** with +/- buttons and a **Set Target Temperature** dialog. From the detail view you can also rename the controller, pick a **Gravity source**, set a **Linked Brew Session**, and see a **Temperature & gravity history** chart (logged roughly every 5 minutes).

RAPT works differently from Grainfather in a few ways:

- **Settings are read-only.** The **Device settings** panel shows whether heating and cooling are **Enabled** or **Disabled**, but these are configured on the physical unit and can't be changed from BrewIQ. BrewIQ can only set the target temperature.
- **Steps are limited to Heating & Cooling or Off.** RAPT can't be told to heat only, cool only or pause from outside. A brew session linked to a RAPT controller can only use those two modes in its fermentation steps. If any step (or the conditioning temperature) is set to heating-only or cooling-only, BrewIQ refuses the link until you change it.
- **It checks in about once an hour.** RAPT controllers sleep between check-ins, so BrewIQ counts one as online if it has been seen within the last 90 minutes. BrewIQ refreshes RAPT data about every 5 minutes, so what you see can lag slightly behind the controller.

## Notifications

The bell icon on a device card subscribes you to an email when that device goes **online or offline** - there's no gravity-stall or temperature-out-of-range alert. Enable/disable this default behavior per device type in [Account & Preferences](account-preferences.md).
