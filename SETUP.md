# Potluck Board — setup

Two parts:

- **The Google Sheet and its Apps Script** store everything, including private details. The script (`Code.gs`) is kept out of this repository.
- **`index.html`** is the page guests open, published with GitHub Pages.

## Where things live

All private details are in the Google Sheet, not in this repository:

| Tab | What it holds |
|---|---|
| **Dishes** | Every dish: Added, Name, Dish, Type, Dietary tags, Notes, ID, Serves, Remove key |
| **Dietary** | Dietary needs guests have shared: Added, Name, Dietary needs, ID, Remove key |
| **Event** | Event name, date, time, place, address, contact |
| **Private** | **Guest password**, which guests type to open the page. This tab is never sent to the page. |

You can change any of these by editing the sheet. Changes show on the page within about a minute.

## How the page works

- **Opening the page:** guests type the guest password once. Their browser remembers it.
- **Order:** the menu comes first, then "Add my dish", then "Dietary needs", then the Excel download.
- **Removing:** guests can remove their own dishes and dietary notes, but only on the phone or computer they used to add them. Each entry gets a secret remove key that only that browser knows.
- **Anything else:** to remove or fix any other entry, delete or edit its row in the sheet.
- **Excel:** the file has three sheets: Dishes, Summary and Dietary needs.

## Setting it up from scratch

1. Go to <https://sheets.new> and click **Extensions → Apps Script**.
2. Paste in `Code.gs`. Choose **setup** and click **Run**, then approve the permissions.
3. Fill in **Guest password** on the **Private** tab, and the event details on the **Event** tab.
4. Click **Deploy → New deployment → Web app**. Set **Execute as: Me** and **Who has access: Anyone**.
5. Put the `/exec` address in `POTLUCK_CONFIG.apiUrl` near the top of `index.html`.

## If you change `Code.gs` later

Saving isn't enough. Click **Deploy → Manage deployments**, then the pencil, set **Version: New version**, and click **Deploy**. The address stays the same.

## Limits

Each list (dishes and dietary needs) holds up to 200 entries.
