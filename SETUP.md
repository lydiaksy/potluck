# Potluck Board — setup

Two parts:

- **The Google Sheet and its Apps Script** store everything, including private details. The script (`Code.gs`) is kept out of this repository.
- **`index.html`** is the page guests open, published with GitHub Pages.

## Where things live

All private details are in the Google Sheet, not in this repository:

| Tab | What it holds |
|---|---|
| **Dishes** | Every sign-up: Added, Name, Dish, Course, Dietary tags, Notes, ID |
| **Event** | Event name, date, time, place, address, contact, and how many dishes each course needs |
| **Private** | **Guest password** (what guests type to open the page) and **Host passcode** (for Host login and removing dishes). This tab is never sent to the page. |

You can change any of these by editing the sheet. Changes show on the page within about a minute.

## How the page works

- **Opening the page:** guests type the guest password once. Their browser remembers it.
- **Host login:** at the bottom of the page. Enter the host passcode to edit event details.
- **Removing a dish:** click **Remove** next to it and enter the host passcode.
- **Excel:** "Download Excel file" saves a workbook with a Dishes sheet and a Summary sheet.

## Setting it up from scratch

1. Go to <https://sheets.new> and click **Extensions → Apps Script**.
2. Paste in `Code.gs`. Optionally add a `Seed.gs` file holding `PRIVATE_SEED` values.
3. Choose **setup** and click **Run**, then approve the permissions.
4. Fill in **Guest password** and **Host passcode** on the **Private** tab, if the seed didn't.
5. Click **Deploy → New deployment → Web app**. Set **Execute as: Me** and **Who has access: Anyone**.
6. Put the `/exec` address in `POTLUCK_CONFIG.apiUrl` near the top of `index.html`.

## If you change `Code.gs` later

Saving isn't enough. Click **Deploy → Manage deployments**, then the pencil, set **Version: New version**, and click **Deploy**. The address stays the same.

## Editing the sheet by hand

- **Course:** use one of Mains, Sides, Salads, Desserts, Drinks.
- **Dietary tags:** separate them with commas.
- **ID:** leave it blank. It's filled in on the next sign-up.

## Limits

- **Wrong passcodes:** after 20 wrong host passcodes, host actions pause for 15 minutes.
- **List size:** the list holds up to 200 dishes.
