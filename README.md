# PriceOnRecord

Static site for priceonrecord.com — fragrance deal claims, checked against recorded prices.
Four hand-written HTML pages, one stylesheet, no build step, no external requests.

## Local preview
    python3 -m http.server 8000
then open http://localhost:8000/

## Deploy (human steps, in order)
1. Register `priceonrecord.com`. At the registrar, set up email forwarding for
   `contact@priceonrecord.com` (the address on the about page).
2. Create a public GitHub repo (suggested name: `priceonrecord`), then:
       git remote add origin git@github.com:<user>/priceonrecord.git
       git push -u origin main
3. GitHub repo Settings → Pages → Source: deploy from branch `main`, folder `/ (root)`.
4. Add a `CNAME` file containing exactly `priceonrecord.com`, commit, push.
5. DNS at the registrar:
   - Apex `priceonrecord.com`: ALIAS/ANAME to `<user>.github.io` if supported, else four A records:
     185.199.108.153, 185.199.109.153, 185.199.110.153, 185.199.111.153
   - `www`: CNAME to `<user>.github.io`
6. Back in Pages settings: set custom domain `priceonrecord.com`, wait for the certificate,
   then tick "Enforce HTTPS".
7. Submit `https://priceonrecord.com` as the site in the CJ and Rakuten publisher applications.

## Editing rules
See SITE-NOTES.md — every factual claim on any page needs a row there (source or R label).
No scent vocabulary anywhere. No claimed measurements until the price pipeline is live.
