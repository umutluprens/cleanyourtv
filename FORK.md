# Snug TV

*Your TV, snug and ad-free.*

Snug TV is an unofficial fork of [CleanYourTV](https://github.com/Gathin23/cleanyourtv), the launcher by Gathin
and its contributors. It is not made or supported by the CleanYourTV project, so report problems here and not
upstream.

Almost all of Snug TV is CleanYourTV's launcher code, unchanged. The list below is everything the fork changes.

The fork ships the launcher as one release-signed APK under its own package, `io.github.umutluprens.tvhome`. It
installs beside the reference launcher (`com.gathin.tvhome`) rather than over it. Turn on only one of the two Home
helpers in the accessibility settings.

## What it changes

- **Stock home redirect for more launchers.** `stock_home_redirect` takes a comma-separated list. The fork sends
  Google TV's `launcherx`, Android TV's `tvlauncher` and `leanbacklauncher`, and Xiaomi PatchWall
  (`com.mitv.tvhome`) back to Snug TV, 150 ms after the stock home opens.
- **Assistant results stay on screen.** A result the Assistant opens through the stock launcher is not closed by
  the redirect.
- **Card tiles for phone apps.** Apps without a TV banner get a card tile (`bannerless_card_tiles`).
- **Held volume keeps repeating.** `key_filter` is off by default.
- **Its own name and look.** The app is called Snug TV, with its own icon and banner. The accessibility helpers
  are named "Snug TV Home" and "Snug TV Input button".

It adds no permissions and no network access. The Home redirect uses the launcher's existing accessibility
service.

## Install

Download page with pictures (Turkish): https://umutluprens.github.io/snug-tv/

Or download the APK and its `.sha256` file from
[Releases](https://github.com/umutluprens/snug-tv/releases) and check the hash.

- **Android TV:** install the APK with a file manager or Downloader, then pick Snug TV when the TV asks for a
  home app.
- **Google TV:** after installing, turn on Settings > Accessibility > Snug TV Home. On Google TV with Android 13
  or later, Play Protect can block a sideloaded APK, and restricted settings can keep that switch from turning
  on. Installing with `adb install` avoids both.

There is a step-by-step guide in Turkish: [docs/KURULUM-TR.md](docs/KURULUM-TR.md).

## Tested on

Google TV Streamer, Google TV (Android 14).

## Credit and licence

Snug TV is built on CleanYourTV and keeps its MIT licence ([LICENSE](LICENSE)).
