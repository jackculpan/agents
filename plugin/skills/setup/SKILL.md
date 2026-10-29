---
name: setup
description: Set up Re-Pricer for the user's OnBuy account. It connects the Re-Pricer MCP server, checks that OnBuy API keys are saved, lists their listings, reports Buy Box status, and helps set safe price floors. Use when the user installs the plugin, asks to set up Re-Pricer, or asks to connect or reprice their OnBuy listings.
---

Take the user from nothing to "Re-Pricer is connected and I can see my listings and Buy Box status". Do not touch any price until the user agrees.

## Rules

- OnBuy consumer key and secret key are secrets. Never ask for them in chat. The user types them into https://re-pricer.com/api-keys in the browser.
- `update_listing_prices` changes live prices. Show the SKUs, old prices and new prices. Wait for a clear yes before each call.
- `update_listing_prices` checks a price against a listing's min and max only when that listing has a floor set. A listing with no floor accepts any price. You cannot see the floors, so you must not guess them.
- Writing prices may need an active trial or plan. If the tool refuses, tell the user and stop.

## Step 1: connect the MCP server

Check that the `re-pricer` MCP server is available. If its tools are missing, tell the user to run `/mcp`, select `re-pricer`, and sign in. New users must first sign up at https://re-pricer.com. Wait for them to finish.

## Step 2: OnBuy keys

Call `list_listings` with `limit: 5`.

- It returns listings: continue to step 3.
- It returns an error such as "OnBuy API request failed": the OnBuy keys are most likely missing or wrong. Tell the user to open https://re-pricer.com/api-keys, paste their OnBuy consumer key and secret key there, and save. They get the keys at https://seller.onbuy.com/inventory/integrations/onbuy-api/. Call `list_listings` again after they confirm.
- It returns zero listings: the account has no live listings on the selected OnBuy site. Say so and stop.

## Step 3: report what is there

1. Call `list_listings` with `limit: 100`. Report the count on that page. If the page is full, say "100 or more".
2. Call `check_winning` on up to 20 SKUs. Report how many win the Buy Box, how many lose, and for the losers the gap to the lowest competing price.
3. Give a table of the five biggest gaps: SKU, our price, lowest price.

Write the report in plain, short sentences.

## Step 4: price floors

Automatic repricing only moves a price inside each listing's min and max. A listing with no floor does not reprice.

Ask the user for one number: the lowest margin they accept, as a percentage below the current price, or a minimum profit after OnBuy fees. Tell them to set min and max prices in the Re-Pricer dashboard at https://re-pricer.com. Do not guess a floor.

## Step 5: manual reprice, only if asked

If the user asks to reprice now:

1. Pick losing SKUs. Ask the user for the lowest price they accept for each one.
2. Show a table: SKU, old price, new price.
3. Wait for a clear yes.
4. Call `update_listing_prices` with those updates.
5. Report accepted and rejected lines, with the reasons for rejected ones.

Then tell the user the next step: Re-Pricer keeps checking and repricing in the background once floors are set.
