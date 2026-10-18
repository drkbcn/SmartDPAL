<div align="center">

# SmartDPAL

[![Downloads](https://img.shields.io/github/downloads/drkbcn/SmartDPAL/total?label=downloads&color=2EE6A6)](../../releases)
[![Latest release](https://img.shields.io/github/v/release/drkbcn/SmartDPAL?label=latest&color=3DA5FF)](../../releases/latest)

**An independent, alternative Android app for your Deepal.**
See your car's state at a glance, in a clean, modern interface.

<img src="screenshots/01-login.png" width="190"> <img src="screenshots/02-home.png" width="190"> <img src="screenshots/03-top-view-lights.png" width="190"> <img src="screenshots/04-home-details.png" width="190">

</div>

> **⚠️ Beta (1.1.0).** This version adds remote controls sent signed (climate, doors, lights, horn), session sharing by QR and the Deepal S07. These features are **experimental and have not been verified on a real car yet**; in particular, whether *lock/unlock* does what its label says. Use them with the car in front of you, and sign out and in once after updating to activate them.

> **Not affiliated with Changan or Deepal.** SmartDPAL is an unofficial community project. It is not sponsored, endorsed or supported by Changan Automobile Europe, Chongqing Changan Automobile, Deepal, or any of their subsidiaries or importers. See the [disclaimer](#disclaimer).

This repository only hosts the **compiled releases**. The source code is not published.

## Download

Get the latest APK from the [**Releases**](../../releases/latest) page and install it on your Android phone (Android 7.0 or newer). You will need to allow installing apps from your browser or file manager the first time.

SmartDPAL checks this page for new versions: when one is published you get a discreet notice in the app (and a manual *Check* button under **More → About**). Updates are installed over the existing app and keep your session.

Verify the download if you like. Every APK is signed with the same certificate:

```
SHA-256: c2:f2:4b:7d:02:d8:c5:04:0c:77:2b:a7:b4:5c:0f:33:33:86:60:2d:e4:a7:b2:18:95:ca:86:17:e4:0b:7a:13
```

`apksigner verify --print-certs SmartDPAL_*.apk` should print that digest.

## What it does today

**Sign in with your own Deepal / MyChangan (EU) account**
- Email + password sign-in, automatic session renewal, sign-out.
- The session is stored encrypted on the device (Android Keystore). Nothing is sent anywhere except to the manufacturer's own servers.
- The last known summary is cached encrypted, so the app opens instantly even before the network answers.

**Home — your car at a glance**
- Battery level with the charging time left next to it, electric / fuel / total range, interior temperature, odometer.
- Door, window and lock status, and the four tyre pressures.
- Your model name comes from your account, so it works for different models (tested on a **Deepal S05**; the S07 uses the same service and is expected to work, but its data has not been verified on a real S07).
- An animated hero image of the car for the **Deepal S05** (white, black, grey, silver, Andromeda blue) and the **Deepal S07** (white, orange, black, grey, green). Pick the model and colour in **More**. Lights react to the car's real state, and a welcome sequence plays when the app opens.
- Swipe for a **top view** with live tyre pressures and animated head/tail lights.
- Optionally use the photo of your own car from your account.
- **Quick access**: up to four commands of your choice (lock, unlock, climate, lights, horn…) right on the home screen. Tap the pencil to choose them.
- Shows how old the data is: the cloud keeps a cache, so the app says when it was last updated.

**Live data (⚡)**
- Ask the car for fresh telemetry over MQTT (read-only subscription): >100 properties such as range, charge state, tyres, lights and more.

**Data tab**
- Every value the car reports, grouped (energy, trips, access, climate, tyres, other), searchable, with a clear source tag (cloud cache vs live).
- Sensitive values (identifiers, location, tokens) are masked.
- A **Lab** mode that shows only the *structure* of the responses, without personal data, to help investigate new models.

**Remote controls (experimental)**
- Lock, unlock, **climate on/off with a temperature (16–30 °C)**, lights, horn, open the tailgate, close the windows — only the functions your car declares as available. Run them from **Quick access** or from the full **Controls** screen.
- Every order needs your **control PIN** and a deliberate **press-and-hold**, runs once (no automatic retries), and is logged in an in-app audit list without personal data.
- Climate, doors, lights and horn are sent **signed**, like the official app does: signing in now creates a signing key on your phone (stored encrypted). **After updating, sign out and sign in once** to activate them; until then the app asks you to.
- The command contract is community-documented and **not officially verified**. The meaning of *lock/unlock* has not been confirmed on a real car yet: the first time, try it with the car in front of you and check the result before relying on it.

**Share your session with a QR (More → Share configuration)**
- Shows your active session as an encrypted QR (protected by a password you choose) so another phone can use your car **without signing in**. It tells you what it implies and lets you pick how long it is valid: 1 hour, 24 hours, 7 days, or the **maximum** your own session allows (the app shows how much time it has left, about 90 days). The other phone never renews the session, so the server may end it earlier; if it does, ask for a new QR.
- Anyone with the QR **and** the password can see and control your car. Share it only with people you trust, and give them the password through another channel.
- On the other phone, open **Scan configuration QR** on the sign-in screen (it is for SmartDPAL's own QR, not the car's). That phone never renews the session: it shows who shared it and until when, and asks for a new QR when it ends. A shared session cannot be shared again.
- The shared session also ends as soon as anyone signs in with your account somewhere else.

**Bluetooth key, vehicle sharing and remote parking**
- Present in the app but **locked**. Bluetooth comfort commands exist behind a safety switch and have only been tested against a simulator; anything that could move the car is blocked on purpose. Remote parking only makes sense on cars that declare it (the author's S05 does not).

**Languages**
- English and Spanish, following your phone's language, with a language switch on the sign-in screen and under **More → Language**. More languages can be added without code changes.

**Everything else**
- Dark, accessible interface (large text and screen-reader friendly, reduced-motion aware).
- About screen with author links, update check, full disclaimer and open-source licences.
- No analytics, no ads, no tracking. Your data stays on your phone.

<div align="center">

<img src="screenshots/05-data.png" width="190"> <img src="screenshots/06-more.png" width="190"> <img src="screenshots/07-controls.png" width="190"> <img src="screenshots/08-about.png" width="190">

<img src="screenshots/09-home-s07.png" width="190"> <img src="screenshots/10-share-config.png" width="190">

</div>

*All screenshots use synthetic demo data.*

## Known limitations

- Developed and tested with a Deepal S05 PHEV (EU). Other models may show fewer values.
- Signing in here ends the session of the official app, and the other way round (the manufacturer allows one active session per account). It also ends any session you shared by QR.
- Remote controls need you to sign in again once after updating from a version older than 1.1.0.
- Position is not provided by the cloud's HTTP state; it only appears if the car reports it in live data.
- The services SmartDPAL talks to are not publicly documented. They can change or stop working at any time.

## Privacy

SmartDPAL talks to the manufacturer's servers (to sign in and read your own vehicle), to GitHub (to look for new versions and to show the author's avatar in *About*), and nowhere else. Credentials, tokens and the signing key are stored encrypted on your device and never shared. The camera is used only if you tap **Scan configuration QR**, to read a SmartDPAL QR; nothing is recorded or uploaded.

## Disclaimer

SmartDPAL is provided **"as is"**, without warranty of any kind. It relies on unofficial, undocumented services; data may be incomplete, outdated or wrong, and it does not replace the official app, the instrument cluster or the vehicle manual. Orders sent to the vehicle are executed **at your sole responsibility**: make sure the car and its surroundings are safe first. The author is not liable for damage to the vehicle or third parties, loss of warranty, suspension or lock of your account, or any other harm resulting from its use. Use it only with your own vehicle and your own account. Deepal, Changan and MyChangan are trademarks of their respective owners and are mentioned only to identify the compatible vehicle. This is not legal advice.

## Author

Made by [**drkbcn**](https://github.com/drkbcn). If you find it useful, you can [buy me a coffee on Ko-fi](https://ko-fi.com/drkbcn).
