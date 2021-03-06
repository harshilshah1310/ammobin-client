# AmmoBin.ca [ ![Codeship Status for ammobinDOTca/ammobin-client](https://app.codeship.com/projects/992b88f0-d18a-0135-270c-42cf0d64356b/status?branch=master)](https://app.codeship.com/projects/262429) [![Greenkeeper badge](https://badges.greenkeeper.io/ammobinDOTca/ammobin-client.svg)](https://greenkeeper.io/) [![docker pulls](https://img.shields.io/docker/pulls/ammobindotca/ammobin-client.svg)](https://hub.docker.com/r/ammobindotca/ammobin-client 'DockerHub')

The meta search site for ammo prices across Canada. built with [nuxt.js](https://nuxtjs.org) (and thus vue.js).

![Screenshot-2017-9-27 The place to view the best online ammo prices across Canada.png](https://raw.githubusercontent.com/ammobinDOTca/ammobin-client/master/Screenshot-2017-9-27%20The%20place%20to%20view%20the%20best%20online%20ammo%20prices%20across%20Canada%20.png)

## how to run

1.  `docker run ammobindotca/ammo-bin-client -p 3000:3000`

## how to run locally

- `npm i`
- `PROD=true npm run dev` (will target prod api)

## todo

- https://github.com/WICG/BackgroundSync/blob/master/explainer.md

## contributing

- do some work
- submit pr

## vendors to add

- https://shop.triggersandbows.com/ammunition/centerfire/ +1
- https://shophighfalls.com/collections/rifle-ammo?view=ALL (css rules hinder pulling data. will need to update scraper)
- http://shop.sylvestresportinggoods.com/Rifle-Ammunition/?p=catalog&mode=catalog&parent=506&pg=1&CatalogSetSortBy=price
- https://www.tesro.ca/ammunition-and-pellets/smallbore-ammunition.html?limit=36
- http://www.grouseriver.com/Hunting-Shooting/Ammunition
- https://blue-wolf-firearms-canada.myshopify.com/collections/rimfire
- https://www.londerosports.com/firearms/ammunitions/rifle?limit=all
- https://gunworx.ca/collections/ammunition
- https://www.latulippe.com/en/our-stores/
- http://doctordeals.ca/product-category/smoking-gun/ammunition/rifle-ammo/
- http://store.easthilloutdoors.com/ammo/bulk-ammo
- http://www.armseast.ca/surplus_ammunition/

- https://www.siwashsports.ca/product-category/ammunition/centerfire-ammunition/ (cant buy things online as of dec 17 2017, will add once this feature is enabled on the site)
- http://www.danchasse.com/shop_free/index.php?categoryID=109 (je ne parle en francis)

# low priority

- http://greendiamondoutfitters.ca/home/products_grid/category/rifle-ammunition/P24
- http://practicalperformance.ca/accessories/ammunition/
- https://www.greatnorthprecision.com/collections/rifle-ammunition-1
- http://targetshootingproducts.com/index.php?cPath=10&osCsid=b5dd02944271605ca93e19ea903cd3d2
- http://www.thegunroom.ca/index.php?route=product/category&path=85 (6 items

## blocked

- http://westrifle.com/wrstore/index.php?main_page=index&cPath=2 (everything was sold out nov 2017)
- https://eccfirearms.blogspot.ca/2011/02/ammunition-ecc-firearms-has-widest.html (cant buy oneline as of feb 17 2018)
- https://tandtarms.com/product-category/ammo/
- http://www.armseast.ca/surplus_ammunition/ no items
- https://selectshootingsupplies.com/pages/ammunition no online sales

## skipped

- wholesalesports.com
- marstar.ca
- http://www.prairieshotammo.com/find-a-dealer-3.html (but should review these retailers to see if they have online shops)
- http://www.generalgun.ca/ammunition only 1 item
- https://www.kellysonline.ca/collections/ammunition only 1 item
- https://armtac.com/category/ammunition only one 1 item

## incomplete vendors

- none

## docker hub

https://hub.docker.com/r/ammobindotca/ammobin-client/
