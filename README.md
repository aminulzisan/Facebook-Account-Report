# Facebook Account Reporter — CLI Tool

A standalone CLI tool for reporting Facebook accounts and groups. Supports managing multiple Facebook accounts, fetching UIDs from profile URLs, and running concurrent reports.

## Quick Start

```bash
# 1. Install dependencies
npm install

# 2. Run the tool
node cli.js

# 3. From the menu → [1] Manage Accounts → [1] Add account (paste cookies)
# 4. From the menu → [2] Login All Saved Accounts
# 5. From the menu → [3] Report a Profile  OR  [4] Report a Group
```

## Prerequisites & Installation

1. **Install Node.js**: Ensure you have Node.js installed on your computer.
2. **Download or Clone the Project**.
3. **Install Dependencies**: Open a terminal in the project directory and run:
   ```bash
   npm install
   ```

## Termux Installation & Setup (Android)

If you are using an Android phone, you can run this tool entirely inside **Termux**. Follow these exact steps:

1. **Install Termux**: Download it from [F-Droid](https://f-droid.org/packages/com.termux/) *(Do not use the Google Play Store version as it is outdated)*.
2. **Update Packages & Install Dependencies**:
   Open Termux and run the following commands:
   ```bash
   pkg update -y && pkg upgrade -y
   pkg install nodejs -y
   pkg install unzip -y
   ```
3. **Grant Storage Permission**:
   ```bash
   termux-setup-storage
   ```
   *(A popup will appear asking for storage access. Tap "Allow".)*
4. **Extract and Setup the Tool**:
   Assuming you downloaded `massreport.zip` to your phone's default Downloads folder, run:
   ```bash
   # Copy the zip from your Downloads folder to the Termux home directory
   cp ~/storage/downloads/massreport.zip ~/
   
   # Unzip the folder
   unzip massreport.zip -d massreport
   
   # Navigate into the extracted folder
   cd massreport
   
   # Install required Node.js libraries
   npm install
   ```
5. **Run the Tool**:
   ```bash
   node cli.js
   ```

## How to Get Facebook Cookies (Kiwi Browser)

To log into your Facebook accounts securely, you'll need your session cookies.
We recommend using the **Kaguya Extension** on mobile (Kiwi Browser) or desktop.

1. **Install Kiwi Browser**: Download and install [Kiwi Browser](https://play.google.com/store/apps/details?id=com.kiwibrowser.browser) on your Android device (or use a normal browser on PC).
2. **Download Kaguya Extension**: Download the extension zip file from here: [KaguyaExtension-master.zip](https://github.com/ttkienn/KaguyaExtension/releases/download/Kaguya/KaguyaExtension-master.zip).
3. **Install Extension**:
   - Open Kiwi Browser, tap the three dots menu, and go to **Extensions**.
   - Enable **Developer mode** (toggle in the top right).
   - Tap **+(from .zip/.crx/.user.js)** and select the downloaded `KaguyaExtension-master.zip` file.
4. **Get Your Cookies**:
   - Go to [Facebook](https://www.facebook.com) and log into your account.
   - Open the Kiwi Browser menu, scroll down to the bottom, and tap on **Kaguya**.
   - Your cookies will be displayed. Copy the entire cookie string or JSON array.

## Running the Tool

Start the interactive CLI by running:
```bash
node cli.js
```

### Main Menu Overview

| Option | Description |
|--------|-------------|
| `[1]` | 📂 Manage Accounts (add / remove / list) |
| `[2]` | 🔑 Login All Saved Accounts |
| `[3]` | 👤 Report a Profile |
| `[4]` | 👥 Report a Group |
| `[5]` | ⚡ Quick Report — All Types (Profile) |
| `[6]` | ⚡ Quick Report — All Types (Group) |
| `[7]` | ♾️ Infinite Report (Profile) |
| `[8]` | ♾️ Infinite Report (Group) |
| `[9]` | 📋 View Report Types |
| `[10]` | 🔍 Get UID from Profile URL |
| `[0]` | Exit |

---

### [1] Managing Accounts

1. Select **[1] Manage Accounts** from the main menu.
2. You will see a sub-menu:

| Sub-option | Description |
|------------|-------------|
| `[1]` | Add account by pasting cookies |
| `[2]` | Login a specific saved account |
| `[3]` | Login ALL saved accounts |
| `[4]` | Remove an account |
| `[5]` | Import from `account.txt` |

**Adding an account:**
1. Select `[1] Add account (paste cookies)`.
2. Paste your Facebook cookies (JSON array or cookie string format).
3. Give the account a name. The tool validates login and saves it to `accounts/<name>.json`.

**Importing from account.txt:**
- Place your cookies in a file named `account.txt` in the project root.
- Select `[5] Import from account.txt` to automatically import and login.

*Tip: Add multiple accounts to run batch reports on a single target simultaneously.*

---

### [2] Login All Saved Accounts

Logs in every account saved in the `accounts/` directory at once. Refreshed cookies are saved automatically. Always do this before reporting.

---

### [3] & [4] Report a Profile / Group

1. Select **[3] Report a Profile** or **[4] Report a Group**.
2. Choose which account(s) to use — pick one, or type **`A`** to use **ALL accounts** concurrently.
3. Enter the **target UID** (profile) or **GID** (group), or paste the full Facebook URL directly.
4. Enter the **number of rounds** (default: 1).
5. Select a **report type**:
   - `[0]` — Random type each round
   - `[1]` — All available types per round (22 for profile, 16 for group)
   - Or pick a specific type from the numbered list.
6. Reports are submitted and a success/failure summary is shown.

---

### [5] & [6] Quick Report — All Types

Same as reporting with type set to **All**, but skips the type-selection step for speed.

1. Select **[5]** (Profile) or **[6]** (Group).
2. Choose account(s), enter target UID/GID, and set round count.
3. The tool immediately fires all report types.

---

### [7] & [8] Infinite Report

Reports continuously until you press **Ctrl+C**.

1. Select **[7]** (Profile) or **[8]** (Group).
2. Choose account(s) and enter the target UID/GID.
3. Select type: `[0]` Random or `[1]` All types per round.
4. The tool loops forever, printing a progress update every 10 rounds.
5. Press **Ctrl+C** to stop gracefully.

---

### [9] View Report Types

Displays all available report type keys and their labels for both Profile and Group — useful when scripting with the CLI argument mode.

---

### [10] Getting a Facebook UID

If you only have a profile link (e.g., `https://www.facebook.com/zuck`), convert it to a numeric UID here.

1. Select **[10] Get UID from Profile URL**.
2. Choose an active account.
3. Paste the profile URL.
4. The tool returns the exact numeric UID (e.g., `4`).

---

### Submitting Reports — Tips

- You can paste a **full Facebook URL** instead of a UID anywhere a UID is asked — the tool resolves it automatically.
- Using **All accounts** (`A`) runs reports from every logged-in account in parallel, multiplying your report volume.
- A **2-second delay** is added between rounds to avoid rate-limiting. On failures, the delay extends to **5 seconds**.

## Advanced CLI Mode (Automation)

For automated usage without the interactive menu, you can pass arguments directly:

```bash
# Report a profile (1x random type using all logged-in accounts)
node cli.js <UID>

# Report 5 rounds with random types
node cli.js <UID> --count 5

# Report with all 22 types, 1 round
node cli.js <UID> --type all

# Specific type
node cli.js <UID> --type fake_account

# Infinite mode (runs forever until you press Ctrl+C)
node cli.js <UID> --infinite

# Report a group
node cli.js group <GID> --type all --count 5

# List all available report types
node cli.js --types

# Help menu
node cli.js --help
```

## Available Report Types

### Profile (22 types)
`fake_account`, `harassment_me`, `harassment_someone`, `violence`, `violence_death`, `hate_speech`, `nudity`, `nudity_threats`, `impersonation`, `pretending_me`, `pretending_friend`, `pretending_someone`, `pretending_business`, `terrorism`, `scam`, `spam`, `suicide`, `child_nudity_threats`, `child_bullying`, `restricted_items`, `drugs`, `intellectual_property`

### Group (16 types)
`grp_bullying`, `grp_sexual_exploitation`, `grp_violence_death`, `grp_credible_threat`, `grp_trafficking`, `grp_terrorism`, `grp_violence`, `grp_hate_speech`, `grp_child_abuse`, `grp_animal_abuse`, `grp_weapons`, `grp_animals`, `grp_scam`, `grp_spam`, `grp_nudity`, `grp_suicide`
