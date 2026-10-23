# My Android TV

My own copy of [CleanYourTV](https://github.com/Gathin23/cleanyourtv) (MIT, by Gathin), taken at
upstream commit `0cd7c27` (23 Oct 2026). See [README.md](README.md) for the full upstream docs and
[PROMPT.md](PROMPT.md) for the procedure the AI assistant follows.

Left out from upstream: the maintainer's PR review bot workflow (it needs their API keys and would run
every 6 hours here) and their sponsor button. Everything else is unchanged.

## Before you start

- **Use a laptop at home.** The TV can only be controlled from a computer on the **same Wi-Fi** as the
  TV. Claude in the cloud or the Claude phone app can't reach it. Use
  [Claude Code](https://claude.com/claude-code) on the laptop.
- **The laptop needs:** Python 3, `adb` (Android platform tools), Java 17 and the Android SDK to build
  the home screen. Installing [Android Studio](https://developer.android.com/studio) gives you the SDK
  and Java in one go. The assistant can help install these.
- **The TV needs Android 8 or newer.** Older TVs get the cleanup only, not the new home screen.

## Steps

1. On the TV: **Settings → Device Preferences → About**, press OK on **Build** 7 times. Go back to
   **Developer options** and turn on **USB debugging** (and **Network/ADB debugging** or
   **Wireless debugging** if you see it).
2. On the laptop:
   ```sh
   git clone https://github.com/alfath80-ai/aquila-saujana-rawang
   cd aquila-saujana-rawang
   git checkout claude/android-tv-customization-8zm0p6
   claude
   ```
3. Paste this into Claude Code (fill in the brackets):
   ```text
   I cloned the CleanYourTV repo; this folder is my copy of it. Read AGENTS.md, then follow
   PROMPT.md exactly on my real TV, reusing tools/ and launcher/.

   My TV model is: <brand and model>. It's in Malaysia.
   Apps I use: <e.g. YouTube, Netflix, Prime Video, Disney+ Hotstar, Astro GO, Viu, unifi TV>.
   Keep Chromecast/casting on.

   Before building the launcher, run `gradle wrapper --gradle-version 8.9` in launcher/
   (or check gradle-wrapper.jar's checksum against Gradle's official one) so the build uses
   the official Gradle wrapper.

   When we're done, switch off USB and network debugging, reboot, and confirm with
   tools/adb-closed.py that the port is closed.
   ```
4. Answer its checklist questions on the TV and in the chat: which apps you use, how many dock slots
   and in what order, and whether to keep the voice assistant, Chromecast and firmware updates.

## Later

- **Undo everything:** `TV_HOST=<TV_IP> tools/restore.sh <the debloat list it used>` (see README,
  "Restore").
- **Change the dock or look:** edit `launcher/app/src/main/res/values/config.xml` and run
  `launcher/build-and-install.sh`, or push a theme from `themes/` with `tools/theme.sh`.
- **After a TV update:** see "Firmware updates" in README.md. Some updates switch apps back on.
- **Updating from upstream:** wait for a version that's been out a while rather than taking every
  change. The project is new and changes quickly.
