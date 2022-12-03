+++
title = "Adguard Home & Adguard Home Sync docker-compose"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2019-11-08T05:00:00Z
description = "adguard home sync"
categories = ["technology"]
type = "post"

+++
#### Adguard Home

```
version: "2"
services:
  adguardhome:
    image: adguard/adguardhome
    container_name: adguardhome
    ports:
      - 53:53/tcp
      - 53:53/udp
      - 67:67/udp
      - 68:68/tcp
      - 68:68/udp
      - 853:853/tcp
      - 3000:3000/tcp
      - 80:80/tcp
    volumes:
      - /srv/Configs/AdGuard/workdir:/opt/adguardhome/work
      - /srv/Configs/AdGuard/confdir:/opt/adguardhome/conf
    restart: unless-stopped
```

#### Adguard Home - Sync

```
version: "2.1"
services:
  adguardhome-sync:
    image: quay.io/bakito/adguardhome-sync
    container_name: adguardhome-sync
    command: run
    environment:
      - ORIGIN_URL=http://192.168.1.26:85 #change as necessary
      - ORIGIN_USERNAME=dbtech #change as necessary
      - ORIGIN_PASSWORD=password #change as necessary
      - REPLICA_URL=http://192.168.1.27 #change as necessary
      - REPLICA_USERNAME=dbtech #change as necessary
      - REPLICA_PASSWORD=password #change as necessary
      - REPLICA1_URL=http://192.168.1.4 #change as necessary
      - REPLICA1_USERNAME=username #change as necessary
      - REPLICA1_PASSWORD=password #change as necessary
      - CRON=*/1 * * * * # run every 1 minute
      - RUNONSTART=true
    ports:
      - 8080:8080 #change as necessary
    restart: unless-stopped  
```

Original Source:
`https://github.com/bakito/adguardhome-sync`

#### AdGuard Dark Theme

*gistfile1.txt*


```
body
  {
    background-color: #222222;
    color: #eeeeee;
  }

  a
  {
    color: #3d74b7;
  }

  .header
  {
    background-color: #3d74b7;
    color: #fff;
  }
  .header a {
    color:#fff !important
  }

  .footer
  {
    background-color: #3d74b7;
  }

  .footer a:not(.btn)
  {
    color: #aaffaa;
  }

/***
NAVIGATION
*/
  div.header__column.mobile-menu
  {
    background-color: inherit;
  }

  div.header__column:not(.mobile-menu--active) .nav-tabs .nav-item
  {
    width: 120px;
    text-align: center;
  }

  div.header__column:not(.mobile-menu--active) .nav-tabs .nav-item a:not(.dropdown-item)
  {
    width: min-content;
    text-align: center;
    margin: 0 auto;
  }

  .nav-tabs .nav-item.show
  {
    background-color: #334433;
  }

  .nav-tabs .nav-item:not(.show) .nav-link
  {
    color: #fff;
    font-weight: bold;
  }

  .nav-tabs .nav-item.show .nav-link
  {
    background-color: inherit;
  }

  .nav-tabs .nav-item.show .dropdown-menu.show
  {
    background-color: #222;
    color: #fff;
  }

  .nav-tabs .nav-item.show .dropdown-menu.show .dropdown-item
  {
    background-color: #222;
    color: #fff;
  }

  .nav-tabs .nav-item.show .dropdown-menu.show .dropdown-item:hover,
.nav-tabs .nav-item.show .dropdown-menu.show .dropdown-item.active
  {
    background-color: #334433;
    color: #fff;
  }
  .header .dropdown-menu {
    margin-top: 0px;
}
.dropdown-menu {background: #111}
.dropdown-menu a:hover {background:#222}
.dropdown-menu-arrow:after {
    position: absolute;
    top: -5px;
    left: 12px;
    display: inline-block;
    border-right: 5px solid transparent;
    border-bottom: 5px solid #111;
    border-left: 5px solid transparent;
    content: "";
}
.dropdown-menu-arrow:before 
  .nav-tabs .nav-item .nav-link.active
  {
    color: #fff;
  }

  .header-toggler.d-lg-none.ml-lg-0.collapsed
  {
    color: #5eba00;
  }

  div.header__column.mobile-menu.mobile-menu--active
  {
    background-color: #222;
  }

  div.header__column.mobile-menu.mobile-menu--active .nav-item.border-bottom.d-lg-none
  {
    border-bottom: 5px solid #fff !important;
  }

  div.header__column.mobile-menu.mobile-menu--active .nav-tabs .nav-item .nav-link:not(.active)
  {
    color: #fff;
  }

  div.header__column.mobile-menu.mobile-menu--active .nav-tabs .nav-item .nav-link.active
  {
    text-decoration: underline;
  }

/***
INTERFACE
*/
  .card,
.rt-tr
  {
    background-color: #333333;
  }

  .card-table tr td,
.card-table tr th
  {
    border-color: #555555;
  }

  .card.red,
.rt-tr.red
  {
    background-color: #4f3333;
  }

  .card.green,
.rt-tr.green
  {
    background-color: #334433;
  }

  .card.blue,
.rt-tr.blue
  {
    background-color: #233645;
  }

  .rt-tr.-even
  {
    filter: brightness(85%);
  }

  .service
  {
    border-color: #336633;
  }

  .service__icon
  {
    color: #336633;
  }

  .ReactModal__Overlay.ReactModal__Overlay--after-open
  {
    background-color: rgba(0, 0, 0, 0.75) !important;
  }

  .modal-content,
.tab__control
  {
    background-color: #333333;
    color: #eeeeee;
  }

  .overlay.overlay--visible
  {
    background-color: rgba(0, 0, 0, 0.8) !important;
    color: #336633;
  }

  .loading::before,
.ReactTable .-loading,
.card-body--loading::before
  {
    background-color: rgba(0, 0, 0, 0.6) !important;
  }

/***
ALERTS
*/
  .alert-info
  {
    background-color: #132948;
    border-color: #0c192d;
    color: #467fcf;
  }

  .alert-info .container a
  {
    color: #66b574;
  }

/***
INPUTS
*/
  .ReactTable .rt-thead.-filters input,
.ReactTable .rt-thead.-filters select,
.ReactTable .-pagination input,
.ReactTable .-pagination select,
.ReactTable .-pagination .-btn,
.custom-select,
.btn-secondary,
.custom-switch-indicator,
.select.select--language,
.form-control--textarea,
.form-control,
.form-control:focus,
.form-control:disabled,
.form-control[readonly],
.form__group div.basic-multi-select .select__control,
.form__group div.basic-multi-select .select__menu
  {
    background-color: transparent;
    color: #eeeeee;
  }

  .form__group div.basic-multi-select .select__multi-value,
.form__group div.basic-multi-select .select__multi-value__label,
.form__group div.basic-multi-select .select__menu div div.select__option.select__option--is-focused
  {
    background-color: #334433;
    color: #d4d4d4;
  }

  .form__group div.basic-multi-select .select__multi-value__remove:hover
  {
    background-color: #4f3333;
  }

  .btn-secondary
  {
    background-color: #336633;
  }

  .checkbox__label-subtitle,
.form__desc
  {
    color: #aaaaaa;
  }

  .logs__input-wrap .tooltip-custom--logs
  {
    filter: invert(0.9) saturate(5) hue-rotate(50deg);
  }

  .rt-td .logs__action,
.rt-td .table__action,
.rt-td div[class$="__action"]
  {
    background-color: transparent;
  }
  .logs__text {
    color:#fff !important
  }
```







