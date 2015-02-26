# OpenPGP Keyserver Site - Lite

This repository holds the source of my OpenPGP Keyservers website, but the lite version of it.

This site is a static site using [bootstraps](http://getbootstrap.com/).

## Nginx Configuration

    #----------------------------------------------------------------------
    # OpenPGP Public SKS Key Server
    #----------------------------------------------------------------------

    server {
        listen 80;
        listen [::]:80;
        listen <set-your-IP>11371;
        listen [set-your-IPv6-IP]:11371;
        server_name <set-your-hostname>;
        server_name pool.sks-keyservers.net;
        server_name *.pool.sks-keyservers.net;
        server_name pgp.mit.edu;
        server_name pgp.ipfire.org;
        server_name keys.gnupg.net;
        root /var/www/html;

        rewrite ^/stats /pks/lookup?op=stats;
        rewrite ^/s/(.*) /pks/lookup?search=$1;
        rewrite ^/search/(.*) /pks/lookup?search=$1;
        rewrite ^/g/(.*) /pks/lookup?op=get&search=$1;
        rewrite ^/get/(.*) /pks/lookup?op=get&search=$1;
        rewrite ^/d/(.*) /pks/lookup?op=get&options=mr&search=$1;
        rewrite ^/download/(.*) /pks/lookup?op=get&options=mr&search=$1;

        location /pks {
            proxy_pass         http://127.0.0.1:11371;
            proxy_pass_header  Server;
            add_header         Via "1.1 <set-your-hostname>:11371 (nginx)";
            proxy_ignore_client_abort on;
            client_max_body_size 8m;
        }
    }

## License

                  GNU GENERAL PUBLIC LICENSE
                     Version 2, June 1991

    Copyright (C) 2012-2014 Matt Rude <matt@mattrude.com>

    This program is free software; you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation; either version 2 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.
