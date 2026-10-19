# My Android TV

My own copy of [tv-detox](https://github.com/Ansub/tv-detox) (MIT, by Ansub Khan),
customized for my TV. See [README.md](README.md) for the full upstream docs.

## What's different from upstream

- **apps.txt**: YouTube, Netflix, Prime Video and Disney+ on the top row.
  Hulu and Max are dropped (not available in Malaysia). Any other TV apps
  installed (Astro GO, Viu, iQIYI, unifi TV…) are added after these.
- **my-tv.txt**: my list of changes, so `check.sh --fix my-tv.txt` puts them
  back after a system update.

## Important: run it from a laptop at home

The TV can only be controlled from a computer on the **same Wi-Fi** as the TV.
Claude in the cloud or the Claude phone app can't reach it. Use
[Claude Code](https://claude.com/claude-code) on a laptop at home.

## Steps

1. On the TV: **Settings → Device Preferences → About**, press **Build** 7 times.
   Then in **Developer options** turn on **USB debugging** (and **Network/Wireless
   debugging** if you see it).
2. Find the TV's IP: **Settings → Network & Internet →** your Wi-Fi.
3. On the laptop, clone this repo and open Claude Code in it:
   ```sh
   git clone https://github.com/alfath80-ai/aquila-saujana-rawang
   cd aquila-saujana-rawang
   claude
   ```
4. Paste this (fill in the brackets):
   ```text
   Help me clean up my Android TV and make it faster.
   My TV is a <brand and model>, at IP <TV_IP>.

   1. Connect to my TV over Wi-Fi. Walk me through anything I need to tap on the TV.
   2. Before changing anything, list every app in plain English: safe to turn off,
      needed by the TV, and apps I use. Check free memory.
   3. Ask me before every change. Turn apps off instead of deleting them.
      Write each change to my-tv.txt.
   4. Never turn off: Google Play services (com.google.android.gms), Google Play,
      Settings, System UI, setup apps, the keyboard, Bluetooth, my HDMI inputs,
      the TV's input and tuner framework, or anything else the TV needs to start.
      Keep casting (Chromecast built-in) on. If you're not sure, leave it on.
   5. Install the home screen: run sh install.sh <TV_IP> "" "bluetooth,sound,picture"
   6. Turn off animations and the screensaver, and make the TV sleep after 5 minutes.
   7. Wait 30 seconds after the last change, then restart the TV once and check it
      starts up normally. Show me free memory before and after.
   ```

## Later

```sh
sh check.sh <TV_IP> --fix my-tv.txt   # after a TV update
sh undo.sh <TV_IP>                    # back to the TV's own home screen
```

Change the apps on the home screen with the remote: hold **OK** on an app.

Upstream version: tv-detox `52644cd`.
