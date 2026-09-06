---
layout: default
title: Privacy Policy (version 2)
---

# Privacy Policy

- **Effective date:** 4 September 2026
- **Applies to:** MyJournal for Android (`br.com.schluter.myjournal`)
- **Developer:** Leonardo Schluter Leite
- **Privacy contact:** lschluterleite@gmail.com
- **In-app disclosure version:** 2 (see [Changes to this policy](#changes-to-this-policy))
- **Também disponível em:** [Português (Brasil)](https://lschluter.github.io/myjournal-site/privacy/pt/)

MyJournal is a voice and text journal. It is built by one person, and it has no server,
no account system, and no analytics. This policy describes what the app actually does, as
implemented — not what it intends to do.

## The short version

- Your journal stays **on your phone**, in an encrypted database.
- Speech is transcribed **on your device**. Audio is never recorded to a file and never
  uploaded.
- The developer receives **no data about you at all** — there is no backend to receive it.
- Journal text is sent to an AI provider **only** if you explicitly turn that on, and it is
  billed to **your own** account, not the developer's.

## What the app stores, and where

Everything below is stored only in the app's private storage on your device.

| Data | Purpose | Retention |
|---|---|---|
| Journal entries (typed or transcribed) | The journal itself | Until you delete them |
| TODOs, including AI-generated ones | The TODO feature | Until you delete them |
| Your OpenRouter API key | Authenticating your own AI requests | Until you delete it or erase app data |
| Settings (theme, language, app lock, model choice) | Preferences | Until you erase app data |
| Your cloud-consent record | Proving consent was granted, and for which version of this disclosure | Until you erase app data |

The journal database is encrypted with SQLCipher (AES-256). The encryption key is randomly
generated on your device, wrapped by the Android Keystore, and never leaves the device. Your
API key and consent record are held in encrypted preferences backed by the same Keystore.

Android's automatic cloud backup and device-to-device transfer are **disabled**
(`allowBackup="false"`), so your journal is not copied into your Google account.

## Microphone and speech

The app requests the **microphone** permission to transcribe what you say into text.

- Transcription runs **on your device**, using Android's on-device speech recogniser. This is
  why the app requires Android 13 (API 33) or later — the on-device-only API does not exist
  below that.
- **Audio is never written to a file and never transmitted.** Only the resulting text is kept,
  as a journal entry you can see and delete.
- If on-device recognition is unavailable on your device, the app **tells you and stops**. It
  does not quietly fall back to a network recogniser.
- There is one exception, and it is opt-in: a setting called **remote recognition**, off by
  default. If you turn it on, speech is sent to Google's speech service under Google's own
  privacy policy. Leave it off if you do not want that.

You can use the entire app by typing, without ever granting microphone access.

## Optional AI features, and the data they send

Two features can send journal text off your device: **Ask** (asking questions about your
journal) and **automatic TODO extraction**. Both are **off by default** and both are behind a
master switch — *"Allow any journal data to leave this device"* — which is also off by default.

Nothing is transmitted until you turn that master switch on *and* enable the specific feature.

**Recipient:** [OpenRouter](https://openrouter.ai), which routes the request to an AI model
provider (by default `google/gemini-2.5-flash-lite`). You choose the model in Settings.

**What is sent:**

- *Ask*: your question, plus your most recent journal entries, in full, as context. How many is a
  setting you control, and it defaults to 20. **No more than 20 entries are ever sent, whatever
  the setting shows** — the transmission cap is enforced in the code independently of the setting,
  so a larger number entered in Settings does not send more. Your display language is also sent
  (for example `Portuguese (Brazil) (pt-BR)`), so the answer comes back in the language you read
  the app in — that is the language setting itself, not a device identifier.
- *TODO extraction*: the full text of the entry you just saved, plus the text of your currently
  open TODOs, so the model can tell which are newly completed.

**What is not sent:** audio, your name, your email, device identifiers, location, contacts, or
any advertising ID. The app collects none of these in the first place.

**Billing and accounts:** you connect your own OpenRouter account through a browser sign-in.
The key issued belongs to you and usage bills to you. The developer never sees the key, never
sees your requests, and operates no server in the path.

**Privacy controls sent with every request:** each request asserts zero data retention
(`zdr`), refuses providers that collect data for training (`data_collection: "deny"`), and
disables silent fallback routing. These are sent per request rather than relying on your
account settings, because the app cannot read those. Requests may be processed outside your
country. OpenRouter's own terms and privacy policy govern what they do with the request; see
<https://openrouter.ai/privacy>.

**You can withdraw consent at any time.** Turning the master switch off blocks new requests
and cancels any request already in flight.

**An honest limitation:** deleting data locally cannot recall anything that has already been
sent. See [Data retention and deletion](#data-retention-and-deletion) for what deletion does and
does not reach.

## What the developer receives

Nothing. There is no server, no account, no analytics SDK, no crash-reporting SDK, and no
advertising. The developer never sees your requests and operates nothing in their path.

**Journal data goes to exactly one third party, OpenRouter, and only under the consent described
above.** For completeness, the app makes three other kinds of network request. None of them
carries journal content:

- **Connecting your OpenRouter account** — a browser sign-in and the key exchange that follows.
- **Loading the list of selectable AI models**, when you open the model picker in Settings. This
  sends no API key and no journal data, which is why it is allowed to run before you grant cloud
  consent — but it happens only when you open that picker, never on app start.
- **Speech audio to Google's speech service** — only if you turn on the optional *remote
  recognition* setting described under [Microphone and speech](#microphone-and-speech), which is
  off by default.

If the app is distributed through Google Play, Google collects its own installation and
crash statistics under [Google's privacy policy](https://policies.google.com/privacy). That is
Google's collection, not the developer's, and it contains no journal content.

## Data retention and deletion

**The retention rule is short, because there is only one place your data lives.** Everything the
app holds is stored on your device and nowhere else. The developer operates no server and no
database, so there is no copy to retain, no backup to expire, and no account record that outlives
the app. Data is kept for exactly as long as you keep it, and deleting it in the app deletes it.

There is therefore **no deletion request to submit and no account to close** — deletion is
something you do directly, in the app, at any time:

- **Delete** any single entry or TODO, with a brief undo window.
- **Delete all** journal entries, or all TODOs.
- **Erase all app data** — removes entries, TODOs, your API key, your consent record, and
  resets security settings.
- **Export** your journal, either as an encrypted backup file (AES-256-GCM, protected by a
  passphrase you choose) or as plain Markdown.
- **Import** an encrypted backup to restore.
- **Lock the app** with your fingerprint or device PIN, with a configurable inactivity timeout,
  and block screenshots and screen recording.

Because there is no account and no server copy, uninstalling the app removes your data. Keep an
export first if you want to retain it.

**Two things deletion cannot reach**, stated plainly rather than buried:

- Anything already sent to OpenRouter under the optional AI features above. Deleting locally
  cannot recall a request that has already been made. Every such request asks for zero retention
  at the provider, but that is a contractual assertion to a third party, not something this app
  can enforce or verify.
- Files you exported. Once written to your device or a cloud drive they are outside the app's
  control, and the Markdown export is not encrypted.

If you want the OpenRouter key itself revoked, do that in your OpenRouter dashboard — the app can
delete its local copy, but it cannot revoke a key on their side.

## Children

MyJournal is not directed at children and is not intended for use by anyone under 13.

## Security, and its limits

The app encrypts the journal at rest, keeps keys in the Android Keystore, disables cloud
backup, and can require biometric unlock. These protect against a lost or stolen device and
against someone copying files off the device.

They do **not** protect a device whose operating system has been compromised — a rooted phone
running malicious software with the screen unlocked can read the app's memory while the app is
running. No app-level encryption can prevent that.

To report a security problem, see the
[support page](https://lschluter.github.io/myjournal-site/support/) or email
lschluterleite@gmail.com.

## Changes to this policy

If what the app does with your data changes materially, the in-app consent disclosure is
versioned and you will be asked to review and grant consent again — a previously granted consent
does not carry over to a new disclosure. The effective date above changes too.

The number at the top of this page is that disclosure version, and each version keeps a permanent
URL so you can always read the text you actually agreed to, even after a newer one replaces it:

- Version 2 (current) — <https://lschluter.github.io/myjournal-site/privacy/v2/>

This page always shows the current version.

## Contact

Leonardo Schluter Leite — lschluterleite@gmail.com
