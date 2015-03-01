# OpenPGP Keyserver Website - Lite

This repository holds the website for my OpenPGP Keyserver, but the lite version of it.

This is a static site using [bootstraps](http://getbootstrap.com/) v3.3.2.

## Using on your own site
This project is licensed under the [GNU General Public License, version 2](http://www.gnu.org/licenses/gpl-2.0.html), with this license, you are free to download, modify, and share this project, as long as you persurve those same rights for others.

The content of this repository may be dropped directly in your webserver's content directory, with minor modification to update the contact method.

If you wish to use this project, you will need to modify the `index.html` file slightly to remove my contact information.  First on [line 153](https://github.com/mattrude/pgpkeyserver-lite/blob/master/index.html#L153), change my name to your own. Then just below from [line 156]( https://github.com/mattrude/pgpkeyserver-lite/blob/master/index.html#L156) to [line 186](https://github.com/mattrude/pgpkeyserver-lite/blob/master/index.html#L186), remove my OpenPGP key and replace it with your own.  Lastly, on [line 246](https://github.com/mattrude/pgpkeyserver-lite/blob/master/index.html#L246), change my name to your own for the contact popup.

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
        server_name pgp.ipfire.org;
        server_name keys.gnupg.net;
        root /var/www/html;
        
        location ~ (.git|readme.md) {
            deny all;
            return 404;
        }
        
        location /pks {
            proxy_pass         http://127.0.0.1:11371;
            proxy_pass_header  Server;
            add_header         Via "1.1 <set-your-hostname>:11371 (nginx)";
        }
    }

## License

                  GNU GENERAL PUBLIC LICENSE
                     Version 2, June 1991

    Copyright (C) 2012-2015 Matt Rude <matt@mattrude.com>

    This program is free software; you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation; either version 2 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.
