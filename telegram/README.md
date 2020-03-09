# bisqoffersbot-telegram

## Goal

Create an inline Telegram bot that returns the offerbook (bids and asks) quickly and conveniently.

## Background

This tool is experimental, and a minimal version should be released as soon as possible to start testing usefulness with users. 

Hypothesis: making the Bisq offerbook more easily available (particularly within group chats on Telegram) could increase trading on Bisq.

If this hypothesis is proven to be false, we should cease allocating growth resources to the effort / pass it to the community to take over.

## Requirements

A first version should only include bare minimum functionality.

- one function: get offers in a particular market
- inline mode is most critical, but regular mode could also be released in v1 if it only requires minimal extra work
- bot should auto-suggest key markets to avoid user typos (if the Telegram UX makes this feasible)
    - key markets: btc_usd, btc_eur, xmr_btc, btc_brl, l-btc_btc, btc_gbp, bsq_bt
    - see appendix below for video of UX suggestion using InlineQueryResultArticle
        - upshot of this approach is that results are sent with the suggestions so it's lightnin-quick
        - another option is sending a custom keyboard with markets listed there
- upon specifying a market, results should include:
    - bids and asks
        - might be nice to separate bids and asks with an InlineKeyboardMarkup, so more bids/asks can be show, but this is _not_ necessary for v1 (probably better if not included, to save time)
    - each offer should show: 
        - trade size (including range, if applicable)
        - price (in btc _and_ altcoin/fiat, including corresponding range, if applicable)
        - ordered by spread % (if possible?)
            - need to check if api can be changed to include this in /offers endpoint

Sample response:

⬇️ XMR/BTC - _Bids_ ⬇️

💱 0.00739230 BTC (-2%)

Offer Size: **13.528 XMR** / 0.01 BTC

💱 0.00759230 BTC (0%)

Offer Size: **136.596 XMR** / 1 BTC - **272.596 XMR** / 2 BTC

⬇️ XMR-BTC - _Asks_ ⬇️

💱 0.00739930 BTC (1%)

Offer Size: **13.528 XMR** / 0.04 BTC

💱 0.00740230 BTC (1%)

Offer Size: **201.381 XMR** / 1.5 BTC

_Note the second bid above with a range...some offers have ranges and some don't._

## Notes

1. Spread percentage is not yet available in `/offers` endpoint, so probably cannot be implemented at the moment.
2. Markdown spacing sucks, so it's hard to see that there should be no spacing between price and offer size lines in sample response above, which should make readability better.

## Desired Due Date

TBD

## Deployment

Ideally on an existing VPS somewhere, otherwise TBD.

## Appendix

![](bisq-tgbot-pre.gif)
