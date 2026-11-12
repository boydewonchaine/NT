# NEAT

**Pay and get paid by scanning a QR. Your own wallet, your own keys, a name instead of an address.**

Version **0.1.2** · NEAR **Testnet** only · installable web app (PWA)

> ## Try it now: <https://neat-012.vercel.app>
>
> That is the live test deployment of NEAT 0.1.2. Open it on a phone or a computer and follow [Try it in five minutes](#try-it-in-five-minutes). It runs on **NEAR Testnet**: every token is free test money with no real-world value, but every payment is a real transaction that you can look up on a public block explorer. Nothing here is audited. Do not point it at real money.

This README is the complete guide to NEAT 0.1.2: what it is, how to use every screen, how to test it properly with two wallets, how fees and receipts work, how to back up and restore, what can go wrong and what to do about it, and, for whoever runs a deployment, how to set one up.

## Contents

- [What NEAT is about](#what-neat-is-about)
- [What is in 0.1.2, and what is not](#what-is-in-012-and-what-is-not)
- [Try it in five minutes](#try-it-in-five-minutes)
- [Install it on your phone](#install-it-on-your-phone)
- [Create your wallet](#create-your-wallet)
- [Choose your name](#choose-your-name)
- [The Home screen](#the-home-screen)
- [Receive money](#receive-money)
- [Send money](#send-money)
- [Receipts and status words](#receipts-and-status-words)
- [Fees: the stamp fee](#fees-the-stamp-fee)
- [Activity](#activity)
- [Settings, locking and auto-lock](#settings-locking-and-auto-lock)
- [Back up and restore](#back-up-and-restore)
- [Security in plain words](#security-in-plain-words)
- [A proper test with two wallets](#a-proper-test-with-two-wallets)
- [Troubleshooting](#troubleshooting)
- [Known limits](#known-limits)
- [Glossary](#glossary)
- [Run your own deployment](#run-your-own-deployment)
- [Under the hood](#under-the-hood)
- [What is verified and what is not](#what-is-verified-and-what-is-not)
- [Development](#development)
- [Version history](#version-history)

---

## What NEAT is about

NEAT is a payment app built around one gesture: **scan a QR**.

Most crypto wallets begin with a ritual: connect an extension, copy a long address, paste it somewhere, and hope every character survived. NEAT removes the ritual.

- **You make a wallet inside the app.** No extension, no external wallet to connect, no account with us.
- **You pick a name**, such as `mira.testnet`. That name is your public identity. Nobody has to read, copy or type a 64-character address.
- **To get paid, you show a QR. To pay, you scan one.** The app checks that the QR is genuine, shows who you are paying and exactly what the payment will cost, and asks you to authorize it.
- **You get a receipt that tells the truth.** A payment says "Completed" only when the network itself has reported it final and successful, and the amount shown as received is the amount the network reports.

NEAT runs on **NEAR Testnet**, the practice network of the NEAR blockchain. The tokens are free and worthless, which makes it a safe place to build, test and learn the experience before anything real is at stake.

### The principles

| Principle | What it means in practice |
| --- | --- |
| **Self-custodial** | Your wallet's key is created on your device and stays there, encrypted. NEAT's servers never see your key or your sentence. Nobody, including the people who built NEAT, can reset your sentence or recover your wallet for you. |
| **QR first** | You send and receive by QR and nothing else. There is no copy-address button, no paste-address box and no payment link to pass around. (You can share a QR *image*.) |
| **Names, not addresses** | Your identity is a registered name ending in `.testnet`. |
| **Testnet only** | NEAT talks to NEAR Testnet and nothing else. Moving to a real network would be a separate, deliberate decision that has not been taken. |
| **Honest status** | A name is "registered" only when the chain shows your key on it. A payment is "completed" only when the network reports it final and successful. A failure is shown as a failure, including any fee that was still charged. NEAT never shows a success it has not confirmed. |
| **Real transactions** | Balances, fees and transactions are real testnet ones. Nothing in the app is simulated. |

---

## What is in 0.1.2, and what is not

**In 0.1.2**

- Create a wallet protected by a personal sentence; the key is encrypted on your device
- Register a real `name.testnet` account
- Receive by QR: a standing **My QR**, or a one-off **Request amount** (amount, note, expiry, optional fixed amount)
- Send by scanning with the camera, or by uploading a photo or screenshot of a QR
- A **Review** screen before every payment: exact recipient, amount, estimated stamp fee, total
- Live payment status and a printed-slip style receipt with the date, time and the network's own evidence
- An Activity list of payments sent and received, and of your requests
- Auto-lock, an encrypted backup file, restore on another device, erase
- An installable app that opens offline (payments still need a connection)
- Light and dark appearance, following your device

**Not in 0.1.2**

- Any asset other than NEAR. There is no USDC, USDT or other token yet.
- Any network other than NEAR Testnet. No mainnet, no other chains.
- A NEAT service fee. The stamp fee is the NEAR network fee alone.
- Copy or paste of addresses and links. That is deliberate.
- Recovering a wallet without its backup file and its sentence. That is deliberate and unavoidable.
- Contacts, several accounts in one wallet, or syncing one wallet across devices.

Other assets, such as USDC and USDT, and a NEAT service fee are wishes for later versions. Neither exists in 0.1.2, and NEAT stays testnet-only until that is decided explicitly.

---

## Try it in five minutes

**Test deployment: <https://neat-012.vercel.app>**

### What you need

- A phone or computer with a current Chrome, Edge, Safari or Firefox. NEAT uses the browser's built-in Ed25519 signing; if your browser can't do that, the Create screen says *"This browser does not support Ed25519 signing. Use a current Chrome, Edge, Safari or Firefox."*
- An internet connection. NEAT opens offline, but it can't check a QR, show a balance or pay without one.
- For the full send-and-receive test, **two wallets**: two devices, a phone and a computer, or two different browsers. A wallet lives in one browser profile, so a second wallet needs a second browser or device. See [A proper test with two wallets](#a-proper-test-with-two-wallets).

### The shortest path

1. Open <https://neat-012.vercel.app>.
2. On a phone, [install it](#install-it-on-your-phone) first and create your wallet inside the installed app. (Skipping this works, but read the iPhone note.)
3. **Create wallet**: choose a sentence of at least 20 characters and 4 words, repeat it, tap **Create wallet**.
4. **Choose your name**, tap **Continue**, then **Register name**. After a few seconds you land on your Home screen with a starting balance of test NEAR.
5. To get paid, tap **Receive** and show the QR to the other wallet. To pay, tap **Send** and scan theirs.

```
 Receiver                                        Payer
 Receive -> My QR  ----------- shown on screen -----------> Send -> scan
 (or Request amount)                                         Amount -> Review -> Authorize payment
                                                                     |
                                                       signed on the payer's device
                                                                     v
                                                          NEAR Testnet (final)
                                                                     |
 Balance rises, Activity shows it,  <---------------------  Receipt: Completed (verified)
 a request turns Paid
```

---

## Install it on your phone

NEAT is a web app that installs like an app. Installing is optional but recommended on a phone.

**iPhone and iPad (Safari)**

1. Open <https://neat-012.vercel.app> in **Safari**.
2. Tap the **Share** button (the square with an arrow).
3. Choose **Add to Home Screen**, then **Add**.
4. Open NEAT from its icon on your Home Screen and create your wallet there.

> **Important on iPhone.** The Home Screen app and Safari keep *separate* storage. A wallet created in a Safari tab is not visible inside the installed app, and the other way round. Pick one place. If you already made a wallet in Safari and want it in the installed app, download its encrypted backup in Safari (**Settings** → **Download encrypted backup**) and restore it in the installed app (**Restore from a backup file**).

**Android (Chrome)**: open the menu (the three dots), then **Install app** (or **Add to Home screen**).

**Computer (Chrome or Edge)**: use the install icon in the address bar, or the browser menu, then **Install NEAT**.

**Why install?**

- Safari can erase the data of websites you haven't opened for about a week. Apps added to the Home Screen are exempt. Your wallet lives in that data, so an installed app is safer to keep. (A backup is safer still.)
- It opens full-screen, like any other app.
- It opens instantly, and the shell works offline.

Settings also has an **Install** section, with the right instructions for your device and an **Install NEAT** button where the browser supports one.

---

## Create your wallet

The first time you open NEAT you see **Create your wallet**. (If you already have a backup file, tap **Restore from a backup file** instead; see [Back up and restore](#back-up-and-restore).)

1. **Personal sentence.** Type a sentence only you would remember.
   - At least **20 characters** and **4 words**, at most **100 characters**.
   - Not too repetitive, and not a common password.
   - A three-bar meter shows how strong it is. **Show** reveals what you typed; **Hide** hides it again.
2. **Repeat it.** The line under the second box says *Matches.* when both are the same.
3. Read the **No reset** note. Tap **How it works** for the full explanation.
4. Tap **Create wallet**. For a moment the button says *Securing your wallet…*. That pause is deliberate: turning your sentence into an encryption key is made slow on purpose, so that guessing it is slow too.

**What just happened.** Your device generated a random signing key. Your sentence was used only to *encrypt* that key (it is not the key). NEAT then checked that the sentence really decrypts what it just made, and only then saved the encrypted copy in the browser. Nothing was sent anywhere. You have a wallet, but no name yet.

**Choosing a good sentence**

- Four or more unrelated words are far safer than one clever phrase. Picture something silly and specific.
- Don't use a famous quote, a lyric, or anything that appears on your social media.
- Write it down and keep it somewhere safe. It is the only thing that unlocks your wallet, and NEAT cannot remind you of it. It is not shown again.

---

## Choose your name

Right after creating the wallet you see **Choose your name**: *"This is how people pay you. It's your public NEAT identity on NEAR Testnet."*

1. Type a name. It is shown with `.testnet` after it.
   - 3 to 32 characters
   - lowercase letters, numbers, `-` and `_`
   - start and end with a letter or a number
   - no doubled `-` or `_`
   - not a 64-character hex string (that would look like an address)
2. As you type, NEAT asks the network: *"mira.testnet is available."* or *"mira.testnet is taken."*
3. Tap **Continue**. A sheet asks *"Register mira.testnet?"* and explains that this creates a real account on NEAR Testnet, controlled only by the key on this device, that NEAT's testnet funder pays the creation cost and gives the account a starting balance of free test tokens, and that **you can't change the name afterwards**.
4. Tap **Register name**.
5. The **Registering** screen shows a spinner while the network confirms. NEAT shows the name as yours only when the chain shows *your* key on that account. At that moment it opens your Home screen and a short message says *"mira.testnet is registered"*.

**If it takes a while.** After about a minute you may see **Not confirmed yet**: the request was sent, but the network hasn't shown the account yet. Nothing is registered until it does. **Check again** looks again and never sends a second request. **Choose a different name** starts over.

**If it fails.** You see **Not registered**, the reason, and **Try again** (or **Change name** / **Choose another name** when the name was taken). See [Troubleshooting](#troubleshooting) for what the messages mean.

**Starting balance.** Each new account starts with free testnet NEAR from NEAT's funder (1 NEAR unless the person running the deployment chose another amount). Whatever your Home screen shows is the truth.

---

## The Home screen

- **Your name** with `.testnet`, a greeting, and your **balance** in NEAR. The balance is read from the network and refreshed every 15 seconds while the screen is open. When the device is offline it says *"offline · may be out of date"*.
- **Send** and **Receive**, the two things you do most.
- **Recent**: your latest four payments, each showing the other person, *Sent* or *Received*, how long ago, the amount, and a status. **See all** opens [Activity](#activity). Tap a payment to open its receipt.
- The top bar has a **Testnet** badge, a **Lock** button and a **Settings** button.

Anything still in flight (a payment that was sent but not yet final) is re-checked every time you open Home, so it settles by itself.

---

## Receive money

Tap **Receive**. There are two kinds of QR.

### My QR (standing code)

Your name as a QR. Anyone with NEAT can scan it and **choose the amount themselves**. It never expires and can be paid again and again: it is a standing "pay me" code.

- The screen says *"Ask them to scan this with NEAT. They choose the amount."*
- **Save image** saves the QR as a picture. Where your browser supports it, **Share image** lets you send that picture through your usual apps.

### Request amount (one-off request)

A QR for a specific amount.

1. Open the **Request amount** tab.
2. **Amount** (up to 6 decimal places).
3. **Note**: optional and short (up to about 40 characters). The payer sees it before paying and it appears on the payer's receipt.
4. **Expires**: **15 minutes**, **1 hour** (the default), **24 hours** or **Never**.
5. **Sender can't change the amount**: on by default. Turn it off to let the payer adjust the amount (it is then shown to them as a *suggested* amount).
6. Tap **Create request**.

The screen then shows the QR, the amount, a status badge (**Open**), and a countdown. While you keep it open NEAT watches your balance, and when a matching, network-verified payment arrives the badge turns **Paid** and a message says *"Payment received and verified."* You can then open the receipt.

- **Cancel request** stops NEAT tracking it. A request is only a QR, so anyone who already has the QR could still pay it until it expires. (The confirmation says exactly that.)
- **New request** makes another.

A request is marked **Paid** only by a verified incoming transfer that is at least the requested amount and was made after the request. NEAR transfers carry no memo, so two open requests for the same amount at the same time can't be told apart; the oldest is matched first.

### What is inside a QR

Only public information: your name, your public key, the amount (if any), a note, the time and an expiry, all **signed by your wallet's key**. Nothing secret. The signature is what lets the payer's NEAT prove the QR really came from the owner of that account and wasn't altered.

---

## Send money

Tap **Send**. The browser asks permission to use the camera the first time.

### 1. Scan

- Point the camera at a NEAT QR. The status line says *"Point the camera at a NEAT QR"*.
- No camera, or you blocked it? Tap **Upload QR image** and choose a photo or screenshot of the QR.

NEAT then says *"Checking this QR on NEAR Testnet…"* and verifies it before showing you anything: it must be a NEAT QR, made for NEAR Testnet, not yours, not expired, correctly signed, and the signing key must really control the named account on the network. If any of that fails you get a plain message instead (see [Troubleshooting](#troubleshooting)), and **Scan again**.

### 2. Amount

You see **Paying** and the recipient's name, with *"Verified: this QR was issued by the owner of this account"*, and the note, if there is one. **Always check the name.** The signature proves who issued the QR, not that you meant to pay them.

- Type the amount in NEAR (up to 6 decimal places).
- **Use max** fills in the most you can send after fees.
- *"Available … NEAR after fees"* shows what you can spend.
- If the request has a fixed amount, the field is read-only (**Requested amount**). If it only suggests an amount (**Suggested amount**), you may change it.
- If the amount is more than you can afford, **Review** stays disabled and says why.

Tap **Review**.

### 3. Review

Nothing has been signed or sent yet. You see:

| Row | Meaning |
| --- | --- |
| To / Account | The recipient's name, and their account in short form |
| Amount | What you are paying |
| Stamp fee (estimated) | The network fee, worked out from the live network. See [Fees](#fees-the-stamp-fee) |
| Total cost to you | Amount plus stamp fee |
| They receive | What lands in their account: the full amount |
| Network | NEAR Testnet |

A note explains the small *hold* the network sets aside while the payment runs; the unused part comes back. If your balance can't cover it, you see **Not enough balance** and how much you *can* spend.

Tap **Authorize payment** to sign it, or **Cancel**. If the fee moved while you were looking (it re-checks if you wait more than half a minute), NEAT tells you and asks you to review again rather than signing against old numbers.

### 4. Sending

**Sending payment** shows three steps: *Signing on this device*, *Sending to NEAR Testnet*, *Confirming on the network*. You can leave the screen safely: the transaction is saved before it is sent, and its status is always on Home and in Activity.

Confirmation usually takes seconds. When the network reports the payment final, NEAT opens the receipt.

If it is slow you may see **Still waiting**. Don't pay again. **Check again** looks at the network; if the network has never heard of the transaction, **Resend the same payment** sends the *identical* transaction again, which can only ever be executed once.

### 5. Receipt

See the next section.

---

## Receipts and status words

The receipt is a small printed slip in a plain typewriter face: the date and the time (in your own time zone, shown on the slip), the names in bold, the amounts, the network's own evidence, and a boxed status stamp at the bottom.

| Line | Meaning |
| --- | --- |
| Headline | **Payment sent**, **Payment received**, **Payment failed**, **Not confirmed yet** or **Processing**, with the amount (minus for sent, plus for received) |
| Date, Time | When the payment was made, with your time zone |
| From, To | The two names |
| Amount | What was paid |
| Stamp fee | The fee. Marked **(est.)** with a "≈" while it is still an estimate, and exact once the network has charged it |
| Total | Amount plus stamp fee, shown once the payment is complete |
| They received / Received | The amount **the network reports** was delivered, marked **(verified)**. *Nothing delivered* if it failed; *Not yet verified* while in flight |
| Note | The request's note, if any |
| Network | NEAR Testnet |
| Evidence | The transaction (a short form of its hash), the network's own **Network status** (for example `FINAL`), and the block that included it |
| Stamp | The status, boxed |
| **View on NearBlocks** | Opens the public block explorer for this transaction, so you don't have to take NEAT's word for it |

Buttons: **Refresh status** (while unresolved), **Resend the same payment** (only if the network hasn't reported the transaction at all), **Done**. An unresolved receipt also re-checks by itself every few seconds.

### Status words

| Word | Meaning | What to do |
| --- | --- | --- |
| **Not confirmed sent** (headline: *Not confirmed yet*) | Signed on your device, but the network hasn't reported it. It may be on its way, or dropped. | **Don't pay again.** Refresh the status. If it still doesn't appear, **Resend the same payment**. |
| **Submitted** | The network accepted it. | Wait. |
| **Confirming** | It is being processed, but isn't final yet. | Wait. |
| **Completed** | The network reports it successful, every step executed, and final. The money moved. | Nothing. |
| **Failed** | It was rejected, or it ran and failed. The amount was **not** delivered. | Read the message. If it ran on-chain, the stamp fee was still charged, and the message says so. |

---

## Fees: the stamp fee

You see **one** fee line everywhere: the **stamp fee**.

In 0.1.2 the stamp fee is the **NEAR network fee**: what the network charges to process the payment. NEAT adds **no fee of its own** in this version, and none is hidden in the amounts.

- **It is computed live.** NEAT reads the network's current fee schedule and gas price and works out this payment's fee from them. No fee is hard-coded. At the time of writing a plain transfer costs a small fraction of a thousandth of a NEAR.
- **Estimated, then exact.** The Review screen shows an estimate. The receipt shows the fee the network *actually charged* once the payment is complete.
- **Total cost to you** is the amount plus the stamp fee. **They receive** is the full amount.
- **The hold.** To be safe the network sets aside a little more than the fee while a transaction runs, and refunds what it didn't use. Your balance must be able to cover the amount **plus** that hold, which is why *Available … after fees* is a touch lower than your balance. A tiny part of every account's balance is also locked by the network to pay for the account's storage.
- **Receiving costs nothing.** The payer pays the fee.
- **A failed payment can still cost the fee.** If the network accepted a payment and it then failed (for example the recipient's account was deleted), the network still charged for the work. NEAT says so.

---

## Activity

**See all** on Home (or the Activity screen) has two tabs.

**Payments**: everything sent and received, newest first, with filters **All**, **Received** and **Sent**. Tap one for its receipt. The refresh button at the top re-checks the network.

- Payments you made are known immediately. Payments you *received* are found through a public index (NearBlocks) that nominates candidate transactions, and **every fact is then re-read from the network itself**: who sent it, how much, whether it succeeded, whether it is final. Anything that isn't exactly one plain transfer to you is discarded.
- The note under the list says so: *"Incoming payments come from the NearBlocks index and are re-verified on the network. This shows recent activity, not complete history."*
- The index has a small free quota, so NEAT rations its use: it asks when you open a screen that lists payments, soon after your balance rises, and on a slow timer, and it backs off when told to slow down. If the index is unavailable, the note says so, and your balance still updates from the network.

**Requests**: the QR requests you created, with their status (**Open**, **Paid**, **Expired**, **Cancelled**). A paid request opens its receipt; an open one takes you to Receive.

---

## Settings, locking and auto-lock

Open **Settings** (the gear on Home).

- **Lock now.** Drops the signing key from memory and asks for your sentence again. The lock button on Home does the same.
- **Auto-lock**: after **1**, **5** (default), **15** or **30 minutes**, or **Only when I lock**. NEAT also locks when you come back to it after having been away longer than that, because phones pause timers in the background.
- **Download encrypted backup**: see [Back up and restore](#back-up-and-restore).
- **How your sentence works**: the plain explanation.
- **Install**: instructions or an install button for your device.
- **Network**: *Connected · block …* when the network answers, and which RPC server NEAT is using.
- **About**: the version, and the reminder that testnet tokens have no monetary value, that payments here are real testnet transactions, and that NEAT never holds your keys.
- **Danger zone** → **Erase wallet from this device**: see below.

### Unlocking

When NEAT is locked it shows **Locked** and your name. Type your sentence and tap **Unlock**.

- A wrong sentence says *"That sentence doesn't match this wallet."* and clears the box.
- From the **third** wrong attempt NEAT makes you wait: 5 seconds, then 10, 20, 40 and so on, up to 15 minutes. The wait is shown as a countdown. (This is a deterrent on your own device; see [Security in plain words](#security-in-plain-words) for what it does and doesn't protect against.)
- **A failed unlock never creates a new wallet.**

### Forgot your sentence?

NEAT can't reset or recover it. Your sentence and key never leave your device. A backup is locked with the same sentence, so it doesn't help either. The last resort is **Erase this wallet…**: any funds in it stay on the testnet but become unreachable. NEAT never creates a new wallet for you unless you ask.

### Erasing a wallet

**Settings** → **Erase wallet from this device**, or **Forgot your sentence?** at the lock screen. The sheet *"Erase this wallet?"* tells you it can't be undone, offers **Download encrypted backup first**, and makes you type your name to confirm (or the word `erase` if you never got a name). After erasing you are back at **Create your wallet**.

---

## Back up and restore

Your wallet exists in one place: this browser, on this device. If the device is lost, broken, wiped, or the browser clears its data, the wallet goes with it. **Your sentence alone cannot restore a wallet on another device.** The backup file is what makes recovery possible.

### Back up

1. **Settings** → **Download encrypted backup**.
2. A file named like `neat-mira.neat` is downloaded. Keep it somewhere safe: your files, a cloud drive, an email to yourself. It is useless without your sentence.
3. Do this right after you create your name, and again before you erase anything.

The file holds only your encrypted key and its public details. It contains no history, balances or requests.

### Restore

1. On the first screen, tap **Restore from a backup file** (on a device with no wallet yet).
2. Tap **Choose backup file** and pick your `.neat` file. NEAT says *"Backup found. Enter its sentence."* (or *"That isn't a NEAT backup file."*).
3. Enter the sentence you chose when you made the wallet and tap **Restore wallet**.
4. NEAT unlocks the file and checks with the network that your key still controls your name. **A name is shown only when the chain confirms it.** If it does, you land on Home. If the network can't be reached, nothing is restored and you are asked to try again.

Wrong sentences count toward the same wait described above.

> Restoring puts the same key on a second device. Use one device at a time for payments, to keep things simple. Each device keeps its own payment history.

---

## Security in plain words

- **Nobody can reset your sentence**, including us. It never leaves your device, and no server holds anything that could recover it.
- **Your sentence is not your key.** The key is random, made on your device. The sentence only encrypts it. That is why you can't derive the wallet from a sentence alone, and why a backup file is needed.
- **A weak sentence is the weak point.** Anyone who gets your backup file (or your browser's data) can try to guess sentences offline, and the slow key derivation only slows that down. A long sentence of unrelated words is the defence. The wait after wrong attempts is a deterrent on your own device, not protection against someone holding the stored data.
- **Browsers can delete site data.** Clearing site data does. Safari also clears data of sites it hasn't seen for about a week, unless installed to the Home Screen. Install the app and keep a backup.
- **A QR proves who issued it, not who you meant to pay.** Always check the name on the Amount screen.
- **What the registration service sees:** the name you chose, your *public* key, and your IP address. It has no authority over your account after creating it.
- **What others see:** the network providers and the payment index see your account name and your IP address when the app asks about it. There is no analytics, no tracker, and no third-party script.
- **Transactions are signed locally and saved before they are sent**, so a refresh, crash or lost connection can never produce a second, different payment. NEAT never signs or sends while offline.

---

## A proper test with two wallets

You need two wallets, here called **A** (the payer) and **B** (the receiver). Use two devices, or a phone and a computer, or two different browsers (for example Safari and Chrome: each browser keeps its own wallet). Open <https://neat-012.vercel.app> in both.

> **With only one device?** Make wallet A in one browser and wallet B in another. B taps **Receive** and **Save image** (or **Share image**); A taps **Send** → **Upload QR image** and picks that picture.

| # | Test | Steps | You should see |
| --- | --- | --- | --- |
| 1 | Create wallet A | Create wallet, choose a name, **Register name** | Home with your name and a starting balance; the message *"…testnet is registered"* |
| 2 | Create wallet B | Same, in the other browser or device | Home for B |
| 3 | Pay a standing QR | B: **Receive** → **My QR**. A: **Send**, scan, enter `0.1`, **Review**, **Authorize payment** | Review shows the stamp fee and a total of amount plus fee. Receipt: **Payment sent**, stamp **Completed**, *They received 0.1 NEAR (verified)*, Network status `FINAL`. B's balance rises within about 15 seconds; B's Activity (refresh) lists it as Received |
| 4 | Check it on the chain | On A's receipt tap **View on NearBlocks** | The same transaction, the same amount, successful |
| 5 | Pay a request | B: **Receive** → **Request amount**, `0.05`, note `lunch`, 1 hour, fixed. A scans it | A sees the note and a read-only **Requested amount**. After A pays, B's badge turns **Paid** and says *"Payment received and verified."* (This step relies on the payment index, which can lag; B's balance rises either way.) |
| 6 | Single use | A scans the same request QR again | *"You've already paid this request."* |
| 7 | Your own QR | A scans A's own My QR | *"That's your own QR. Ask someone else to show theirs."* |
| 8 | Not a NEAT QR | Scan any other QR code (a website, a Wi-Fi code) | *"This isn't a NEAT payment QR."* |
| 9 | Too much | A enters more than *Available* | **Review** disabled with *"Your balance can't cover this amount plus the network fee."* |
| 10 | Use max | A taps **Use max**, reviews, pays | It goes through; a few thousandths of a NEAR stay behind for storage and the hold |
| 11 | Interruption | A authorizes a payment and immediately closes or reloads the page. Reopen and unlock | The payment settles and shows on Home. There is exactly **one** transaction on NearBlocks |
| 12 | Offline | Turn on airplane mode, then try to scan a QR. (Or go offline while on the Review screen.) | A banner *"You're offline. Payments need a connection."* Scanning says *"You're offline. NEAT needs a connection to verify the QR."*; at Review, *"You're offline. You need a connection to send."* and **Authorize payment** is disabled. Nothing is signed offline |
| 13 | Lock and unlock | **Lock**, unlock with the wrong, then the right, sentence | *"That sentence doesn't match this wallet."*; from the third wrong attempt, a countdown |
| 14 | Back up and restore | A: **Download encrypted backup**. **Erase wallet** (type the name). **Restore from a backup file**, choose the file, enter the sentence | Back on Home with the same name and balance, confirmed with the network |
| 15 | Expiry | B makes a 15-minute request. Wait, then have A scan it | *"This payment request has expired. Ask for a new QR."* |
| 16 | Install | Install the app (see above), open it from its icon, unlock | Works like the browser version, full screen |

**Reporting a problem.** Send the exact message you saw, the step you were on, the time, and the **transaction** from the receipt (the transaction is public). Never send your sentence or your backup file to anyone.

---

## Troubleshooting

### Registration

| You see | What it means and what to do |
| --- | --- |
| *Name registration isn't set up on this deployment yet* | The deployment's registration service is missing its funder settings (the line under the message says which). It is the owner's job to fix: see [Run your own deployment](#run-your-own-deployment). Nothing is wrong with your wallet. |
| *Name registration is set up incorrectly on this deployment* | A funder setting is malformed, or its key doesn't belong to the funder account. Owner's job; the line under the message says which. |
| *…the funder account hasn't been given any testnet tokens* | The funder account doesn't exist on the network yet. The owner must send it testnet NEAR. |
| *NEAT's testnet funder has run out of tokens* | The funder can't pay for another name. The owner must refill it (or lower the starting balance). Not your balance. |
| *…is taken* / *…was just taken* | Someone else has that name. Choose another. |
| **Not confirmed yet** | The request was sent but the network hasn't shown the account. **Check again** (it never sends a second request). |
| *The NEAT registration service didn't answer properly* | The reply didn't come from the registration service. Try again; if it persists, tell the owner. |

### Scanning and sending

| You see | What it means and what to do |
| --- | --- |
| *Camera access was blocked…* | Allow the camera for this site in your browser or phone settings, or use **Upload QR image**. |
| *Camera isn't available here…* / *Couldn't start the camera…* | Use **Upload QR image**. |
| *No QR code found in that image* | Use a sharper, closer photo, or a screenshot of the QR. |
| *This isn't a NEAT payment QR.* | NEAT reads only NEAT QRs, not wallet addresses or other apps' codes. |
| *This QR is damaged or isn't a NEAT payment.* | Rescan, or ask for the QR again. |
| *This QR was made by a newer version of NEAT, or for another network…* | NEAT 0.1.2 supports NEAR Testnet only. |
| *That's your own QR.* | Scan someone else's. |
| *You've already paid this request.* | A request with an amount is single-use from the wallet that paid it. |
| *This payment request has expired. Ask for a new QR.* | Ask the receiver to make a new request. |
| *This QR's signature is invalid. Don't pay it.* / *This QR wasn't issued by the owner of … Don't pay it.* | The QR was altered, or isn't from that account's owner. **Do not pay.** |
| *… doesn't exist on testnet.* | The QR names an account that doesn't exist. |
| *Couldn't reach NEAR Testnet…* | Check your connection and try again. Nothing was signed or sent. |
| *Not enough balance.* | The amount plus the stamp fee and hold exceeds what you can spend. The message says the most you can send. |
| *The fee changed. Review it and authorize again.* | The network's fee moved while you waited. Check the new numbers. |
| **Still waiting** / **Not confirmed yet** | Don't pay again. Check again; **Resend the same payment** only re-sends the identical transaction. |
| **Payment failed.** | Read the reason. If it ran on the network, the stamp fee was still charged and the message says so. The amount was not delivered. |

### Everything else

| You see | What it means and what to do |
| --- | --- |
| My balance is lower than I expected | The network locks a tiny amount for your account's storage, and *Available* also leaves room for the fee hold. Past payments' stamp fees are included in what left your account. |
| A payment I received isn't in Activity yet | The payment index can lag behind the network, and its free quota is small. Your balance still updates from the network. Wait a little and use the refresh button on Activity. |
| My request is still **Open** after I was paid | Same: it is marked **Paid** only after the payment is found *and* verified on the network. Keep **Receive** open, or check Activity. |
| The wallet is gone / NEAT asks me to create a wallet | The browser's data was cleared, or you opened a different browser or the installed app instead of the one that holds the wallet (on iPhone they are separate). Look in the other place, or **Restore from a backup file**. |
| *That sentence doesn't match this wallet.* | The sentence has to match exactly, spaces and punctuation aside. After the third miss there's a wait. If you truly can't remember it, see **Forgot your sentence?** |
| Times on a receipt look wrong | They use your device's date, time and time zone. |
| The app looks stale after an update | Close and reopen it; the new version loads when you reopen it. |

---

## Known limits

- One key per wallet and one wallet per browser profile. No syncing between devices, no key rotation, no social recovery.
- Received-payment history is "recent activity" from an index, not a complete record. NEAR transfers carry no memo, so two open requests for the same amount at the same time can't be told apart.
- "Single-use" requests and **Cancel request** are enforced by the app on your own device. A QR is only a QR: anyone who has it can pay it until it expires.
- Timers pause in background tabs, so auto-lock also checks elapsed time when you come back.
- Camera scanning uses the browser's built-in detector where there is one, and NEAT's own slower decoder otherwise (notably on iPhone). In poor light, glare, or at a distance it is less forgiving; **Upload QR image** is the fallback.
- The wrong-sentence wait is a deterrent on your own device, not a defence against someone who has your stored data.
- The registration service's per-address rate limit is best-effort on serverless hosting.

---

## Glossary

| Term | Meaning |
| --- | --- |
| **NEAR** | The blockchain NEAT runs on, and the name of its token. |
| **Testnet** | NEAR's practice network. Tokens are free and worthless. |
| **Name** | Your NEAT identity, such as `mira.testnet`. A real account on the network that only your key controls. |
| **Key** | The secret that signs your payments. Random, created on your device, never shown, never sent. |
| **Sentence** | What unlocks (decrypts) your key on this device. Not the key. Can't be reset. |
| **Encrypted backup** | A `.neat` file containing your encrypted key. Useless without the sentence. |
| **Stamp fee** | The single fee line you see. In 0.1.2, the NEAR network fee. |
| **Hold** | A bit more than the fee that the network sets aside while a transaction runs and then refunds. |
| **Final / `FINAL`** | The network's word for "this can no longer change". NEAT says *Completed* only at this point. |
| **Transaction (hash)** | The public identifier of a payment. You can look it up on a block explorer. |
| **Funder** | The account run by whoever deploys NEAT. It pays to create new names. |
| **RPC** | The server NEAT asks about balances, fees and transactions. |
| **Index (NearBlocks)** | A public service that lists an account's recent transactions. NEAT uses it only to *discover* incoming payments, then verifies them itself. |
| **PWA** | A website that installs like an app. |

---

## Run your own deployment

This section is for whoever hosts NEAT. If you only want to use it, you can stop reading. The live test deployment of 0.1.2 is <https://neat-012.vercel.app>.

NEAT is a zero-dependency static web app (vanilla TypeScript, bundled by esbuild) plus **one** small serverless function that registers names. It needs Node 20 or newer to build.

> **Testnet only.** Testnet tokens have no monetary value. Nothing here is audited. Do not point it at mainnet.

### Vercel (what the repository is set up for)

1. Import the repository. Framework preset: *Other*. `vercel.json` already sets the build command (`node scripts/build.mjs`) and output directory (`dist`).
2. Create the registration funder (the account that pays for new names):
   ```bash
   npm run funder-keygen
   ```
   It prints `NEAT_FUNDER_ID` (a 64-hex testnet account) and `NEAT_FUNDER_KEY` (its secret key). **Never put them in the repository or the app.**
3. **Fund the account.** A 64-hex (implicit) account does not exist on the network until it first receives NEAR, and until then NEAT reports that the funder hasn't been given any testnet tokens. NEAR's documentation describes funding one by sending NEAR to it from any account that already has testnet tokens, for example with near-cli (`near tokens "$SENDER_ID" send-near "$NEAT_FUNDER_ID" '5 NEAR' network-config testnet sign-with-keychain send`). The [NEAR testnet faucet](https://docs.near.org/getting-started/faucet) may accept the id directly, but its documentation doesn't say whether it accepts 64-hex ids, so if it refuses, fund a named testnet account first and send from that. Each new name costs `NEAT_STARTING_BALANCE` (default 1 NEAR) plus a few thousandths of a NEAR in gas, and faucet grants are small, so for a faucet-funded funder set `NEAT_STARTING_BALANCE` lower (for example `0.5`).
4. In the Vercel project open **Settings → Environment Variables**. In the newer dashboard that is **Settings → Environments → Production → Project** (not the *Shared* tab, which is for team-wide variables). Add `NEAT_FUNDER_ID` and `NEAT_FUNDER_KEY` (type *Secret*, called *Sensitive* in older dashboards) and, if you lowered it, `NEAT_STARTING_BALANCE`. Make sure **Production** is ticked. Enter each value on its own, exactly as printed, without the `NAME=` part (stray quotes, spaces and a leading `NAME=` are tolerated, but nothing else is).
5. **Redeploy.** Vercel applies environment variables only to deployments made *after* they were added: open **Deployments**, the three dots on the latest one, **Redeploy**.
6. Open the readiness check (below). When it says `"ready": true`, register a name in the app.

> **One Vercel project per version?** Environment variables belong to a *project*. If you create a new project for a new version (for example one for 0.1.1 and another for 0.1.2), add the funder variables to that project too, and redeploy it. A project without them can't register names.

Serve over HTTPS. The camera, WebCrypto Ed25519 and the service worker all require a secure context. Other hosts work too: `dist/` is a plain static site, and the only server code is `handleRegister(body, env, ip, rpc)` in `src/server/register.ts`, which has no framework dependency. Wrap it in your function runtime and point `NEAT_REGISTER` at it.

### Check that registration is ready

Open **<https://neat-012.vercel.app/api/register>** (or `/api/register` on your own site) in any browser. It registers nothing and shows no secret. It checks the funder settings and the funder account on the network and says what to fix:

```json
{ "ready": true, "network": "testnet", "funder": "…", "balance": "4.9 NEAR", "perName": "1 NEAR" }
```

If `ready` is `false`, `code` says which of these it is, and `detail` says what to do. The registration screen in the app shows the same words.

| `code` | Meaning | Fix |
| --- | --- | --- |
| `unconfigured` | `NEAT_FUNDER_ID` and/or `NEAT_FUNDER_KEY` aren't set for this deployment (`missing` lists which) | Add them to the project that serves this address, with **Production** ticked, then redeploy |
| `funder_config` | They are set but a value is malformed: not an account id, not a whole `ed25519:…` key, a key whose two halves don't match (a character was lost), or a `NEAT_STARTING_BALANCE` that isn't a plain number | Enter the value again exactly as `npm run funder-keygen` printed it |
| `funder_unfunded` | The settings are fine, but the funder account has never been given any testnet NEAR, so it doesn't exist yet | Send it testnet NEAR (step 3) |
| `funder_key` | The account exists, but `NEAT_FUNDER_KEY` isn't one of its full-access keys | Use the id and key that were printed together |
| `funder_empty` | The account holds less than one name costs (`balance` and `perName` show the numbers) | Send it more testnet NEAR, or lower `NEAT_STARTING_BALANCE` |
| `network` | The function couldn't reach NEAR Testnet; `detail` says why (for example `RPC 429` or `RPC 401` means the RPC provider refused it) | Set `NEAT_RPC` and `NEAT_RPC_KEY` (see below) |

The check confirms the funder is in working order; it can't prove `testnet.create_account` accepts the call, which only a real registration (or `live-check -- --spend`) shows.

### Configuration

Set in the environment of the build (`NEAT_RPC`, `NEAT_REGISTER`, `NEAT_INDEX`, `NEAT_SW`, `NEAT_OUT`) and of the function (`NEAT_FUNDER_*`, `NEAT_STARTING_BALANCE`, `NEAT_RPC`, `NEAT_RPC_KEY`). `.env.example` lists them all.

| Variable | Where | Meaning |
| --- | --- | --- |
| `NEAT_FUNDER_ID`, `NEAT_FUNDER_KEY` | function only | Funder account and its secret key. Required for name registration |
| `NEAT_STARTING_BALANCE` | function only | NEAR given to each new account (default `1`) |
| `NEAT_RPC` | build and function | Comma-separated JSON-RPC URLs, tried in order. Also sets the Content-Security-Policy `connect-src`. Default: FastNEAR, then `rpc.testnet.near.org` |
| `NEAT_RPC_KEY` | function only | Optional key the function sends as `Authorization: Bearer` |
| `NEAT_REGISTER` | build | Registration endpoint (default `/api/register`) |
| `NEAT_INDEX` | build | Payment-index base URL (default `https://api-testnet.nearblocks.io`) |
| `NEAT_SW` | build | `0` turns the service worker off (not recommended) |
| `NEAT_OUT` | build | Output directory, relative to the project (default `dist`) |

**Notes on the network services** (checked against their documentation in October 2026; none could be called from the build sandbox):

- *RPC.* FastNEAR (`rpc.testnet.fastnear.com`) is the default. Its documentation says to send an API key as `Authorization: Bearer` or `?apiKey=`; whether the free tier works without one for your traffic is something `live-check` will tell you. `rpc.testnet.near.org` is documented as deprecated and limited to about 30 requests a minute, so it is only a last-resort fallback. Other providers are listed at <https://docs.near.org/api/rpc/providers>; verify CORS with `live-check` before choosing one. **A key placed in a `NEAT_RPC` URL is baked into the public bundle**, so use one restricted to your domain.
- *Payment index.* NearBlocks' free tier is documented as about 6 calls a minute, 333 a day and 10,000 a month, with attribution required and personal use only. NEAT is built around that (see [Activity](#activity)). A production deployment should use a paid plan through a small proxy that keeps the key server-side (`NEAT_INDEX` then points at the proxy).

### Verify against the real testnet

Run this from any machine with internet access. It uses NEAT's own code paths.

```bash
npm run live-check                    # read-only: RPC reachable, testnet, CORS, fee schedule, index shape, funder balance
npm run live-check -- --spend         # also registers two throw-away names, pays between them, verifies, returns the funds
```

Useful settings: `NEAT_RPC`, `NEAT_INDEX`, `NEAT_ORIGIN` (the origin you will serve from, for the CORS checks, for example `https://neat-012.vercel.app`), `NEAT_FUNDER_ID`, `NEAT_FUNDER_KEY`. The script prints PASS, WARN or FAIL for each finding and exits non-zero on a FAIL. `--spend` only spends testnet tokens, and sends nearly all of them back to the funder at the end. It checks what the build sandbox could not: that your RPC endpoints answer as `testnet` and allow browser requests (CORS); that the fee schedule parses and the numbers are sane; that the payment index returns the shape NEAT reads and its hashes resolve over RPC; that the funder key is a full-access key with enough balance; and, with `--spend`, that `testnet.create_account` works, that a payment reaches FINAL, that the network-reported amount and fee match, and that the recipient's device discovers it through the index.

---

## Under the hood

**Identity and keys.** On the first run NEAT generates an Ed25519 key with the browser's CSPRNG. Your personal sentence (up to 100 characters, at least 20 characters and 4 words) is *not* the key. It is run through PBKDF2-HMAC-SHA256 (600,000 iterations, random 16-byte salt) and used with AES-256-GCM to encrypt the key. The additional authenticated data binds the ciphertext to the public key. Only the ciphertext, salt, IV and public key are stored. The sentence, the derived key and the private key are never stored in plaintext, never logged, and never sent anywhere. While unlocked, the key is held as a non-extractable WebCrypto signing key.

**Names.** A NEAT name is a real NEAR account, `<label>.testnet`, controlled only by your key. When you confirm a name, the browser sends the label and your *public* key to `/api/register`. The function calls the registrar contract (`testnet.create_account`) from the funder account, attaching the starting balance. The app then polls the chain and shows the name as yours only when it sees your key as a full-access key on that account; at that moment it opens your dashboard (there is no interim screen). If the network rejects it, the screen says so and shows the failed transaction. If it is slow, the screen says it is still waiting, and a reload resumes the wait without ever submitting twice.

**Receiving.** *My QR* is a standing code for your account. *Request amount* makes a single-use request with an amount, an optional note and an expiry. Each code is signed by your account key (`NEAT1.` followed by a compact binary payload and the signature). There is no copy button for an address or link, anywhere.

**Paying.** *Scan* reads a code with the native `BarcodeDetector` where the browser has one, and a bundled software decoder otherwise (or you can upload a photo of a code). Before showing an amount the app checks the expiry, the signature, and that the signing key is a full-access key on the named account on the network. Then: amount, review, authorize, send.

**Fees.** One fee line, the *stamp fee*. Today it is the NEAR network fee, computed from the live protocol configuration (`EXPERIMENTAL_protocol_config`) and the current gas price. NEAT adds no charge of its own, and none is invented. The Review screen shows the stamp fee (estimated), the total, and what the recipient gets. Your balance must cover the amount plus the amount the network holds up front. The receipt shows the fee the network actually charged.

**Transactions.** The transaction is signed on your device and the signed bytes are written to storage *before* they are sent, so a refresh, crash or timeout can only ever re-send the identical transaction (same hash, so it executes at most once). The app tracks it over RPC and shows distinct states: signed, submitted, processing, completed, failed. A payment is "completed" only when the network reports the transaction successful, all receipts executed, and finality `FINAL`; the amount shown as received is the amount the *network* reports. A transaction that fails on-chain is shown as failed, with the fee that was still charged.

**Incoming payments.** NEAR RPC cannot list an account's history, so a NearBlocks-compatible index nominates candidate transaction hashes. Every fact shown (who, how much, whether it succeeded, whether it is final) is re-read from the network; anything that is not exactly one plain transfer to you is discarded. Coverage is recent activity, not full history, and the screen says so.

**PWA.** Web manifest, maskable icons, a service worker that precaches the shell (the app opens offline; payments need a connection and are never signed or submitted offline), a strict CSP (`default-src 'none'`, scripts and styles from the app's own origin only, `connect-src` limited to your RPC, index and registration origins), and no third-party scripts or analytics. There is no fake install button: install uses the browser's own prompt.

**Design.** Monochrome, derived from the logo (ink `#292a2f` on paper `#eee`, with a dark theme). The receipt is set in a plain typewriter face. The chevron in `public/logo.svg` is a vector traced from the supplied logo image; if you have the original vector, replace that file (and the path in `scripts/make-icons.mjs`, then `npm i -D sharp && npm run icons`). Animations honour *reduce motion*. WCAG AA contrast is enforced by tests in both themes.

---

## What is verified and what is not

NEAT was built in a sandbox that could not reach NEAR, so almost everything was tested against a **simulated NEAR chain** (`tests/mock-chain.ts`). That chain decodes and signature-checks real Borsh transactions and speaks the same JSON-RPC shapes, so it proves NEAT is internally consistent. It cannot prove NEAT matches the real network. The owner has since used a live Vercel deployment on testnet (2026-11-09, reported with screenshots, on the 0.1.1 deployment): the rows marked *Confirmed live* come from that. 0.1.2 changes how the receipt and the screen after registration look; it does not change signing, fees or networking. 0.1.2's own live deployment is <https://neat-012.vercel.app>.

| Area | Status |
| --- | --- |
| Wallet creation, sentence unlock, encrypted backup and restore, lockout, erase | Tested (unit and browser) |
| QR payloads: encode, scan, signature, expiry, tamper and wrong-network rejection | Tested; encoder and decoder cross-checked against OpenCV and the QR spec tables |
| Ed25519 keys and signatures | Byte-identical to an independent implementation (tweetnacl), including the way validators verify a NEAR transaction |
| Borsh transaction layout | Checked against bytes assembled by hand from the protocol specification, and accepted by the simulated chain. **Confirmed live:** a payment signed by NEAT reached `FINAL` on real testnet |
| Fee estimate from live protocol parameters, balance check, estimate-versus-actual reconciliation | Tested against the simulated chain's parameters. **Confirmed live:** the fee charged matched the estimate |
| Payment lifecycle (signed, submitted, processing, completed or failed), timeouts, safe resend of identical bytes | Tested, including drops, timeouts, reloads, revoked keys and drained balances |
| Incoming payments (index hint, every fact re-read over RPC) | Tested against a NearBlocks-shaped fixture. **Not confirmed** against the real NearBlocks index. Run `live-check` |
| PWA: manifest, installability audit, offline shell, CSP, reduced motion, light and dark, 320 px | Tested in Chromium |
| `name.testnet` registration through the real `testnet.create_account` call | **Confirmed live:** names were registered through the deployed funder function |
| Real RPC providers (availability, CORS, API keys) | **Confirmed live** from a phone browser |
| Real phone cameras; iOS Safari and Android | **Not systematically tested.** The app has been used on an iPhone (registration and a payment); camera scanning specifically hasn't been reported on. In the automated tests scanning is exercised with a synthetic camera feed and with uploaded images |
| The Vercel function on Vercel itself | **Confirmed live** once the funder variables were set and the funder was funded. Use the readiness check after any change |

---

## Development

Needs Node 20 or newer. Developed and tested on Linux with Node 22; the npm scripts use POSIX shell globbing, so on Windows use WSL.

```bash
npm install
npm run typecheck        # tsc, strict, no unused code
npm test                 # unit tests (about 15 seconds)
npm run build            # → dist/  (the static site)
npx playwright install chromium
npm run e2e              # builds a test bundle and runs the three browser suites (several minutes)
```

To try the app locally, serve `dist/` over `http://localhost` (a secure context is required for WebCrypto, the camera and the service worker):

```bash
npx --yes serve dist -l 4173
```

Without a funder configured, creating a name stops with an honest "registration isn't set up" message that names what is missing.

| Suite | What it covers | Run with |
| --- | --- | --- |
| Unit (`tests/*.test.ts`) | Crypto and vault, Borsh and signing (cross-checked with tweetnacl), QR encoder and decoder (cross-checked with OpenCV), payload signing, fees, transaction lifecycle and recovery, registration, index rationing, accessibility tokens (WCAG AA), code-hygiene rules enforced on the source tree (nothing is logged, no clipboard or text sharing, no dynamic code, storage only through the store, network only through the sanctioned modules, testnet only), the live-check script, the funder key generator, each way the funder can be misconfigured and its readiness check, "no secrets in the build" | `npm test` |
| `tests/e2e.mts` | The core journey in a real browser: create, name, receive, scan, review, authorize, receipt, restore, offline | `npm run e2e` |
| `tests/e2e-failures.mts` | Cancelled authorization, revoked key, drained balance, on-chain failure, double clicks, ten kinds of bad QR, registration failure and retry, lockout, erase, plus a real-DOM accessibility audit of every screen | `npm run e2e` |
| `tests/e2e-platform.mts` | Installability, CSP enforcement, camera (including denial), auto-lock on a fake clock, reduced motion, and a search of everything sent or stored for secrets | `npm run e2e` |

All of these run against the simulated chain (`tests/mock-chain.ts`, `tests/e2e-server.ts`). They are the evidence for NEAT's own logic; `live-check` is the evidence for the network.

```
src/core/     chain-agnostic logic: vault, near (Borsh, signing), rpc, fees, pay, identity, history, payload, qr, qrdecode, store
src/ui/       the app: app shell and routing, views, dom helpers, scanner, styles.css
src/server/   register.ts: the only server logic (framework-free)
api/          register.ts: Vercel adapter, with its own tsconfig (CommonJS)
public/       index.html, manifest, icons, service-worker template
scripts/      build.mjs, e2e.mjs, live-check.ts, funder-keygen.mjs, make-icons.mjs
tests/        unit tests, the simulated chain, and the browser suites
```

`CLAUDE.md` lists the non-negotiable product rules and the traps to know before changing code.

---

## Version history

| Version | What changed |
| --- | --- |
| **0.1.2** | The receipt is a small printed slip (contained, typewriter face, date and time, names in bold, boxed status stamp). Registering a name goes straight to Home. The fee line is called **Stamp fee**. |
| 0.1.1 | Registration problems are reported specifically (each funder problem has its own message and code) and a readiness check at `/api/register` says whether a deployment can register names. |
| 0.1.0 | First build: wallet, names, QR receive and send, receipts, activity, backup and restore, installable app. |
