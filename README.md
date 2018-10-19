gbin
=====

gbin is a client side encrypted pastebin.  The server has zero knowledge of pasted data.  Data is encrypted/decrypted in the browser using 256 bits AES.

**DEMO: https://paste.itunix.eu/**

gbin is a Go port of [0bin](https://github.com/sametmax/0bin/) (written in Python).  0bin in turn is an implementation of the [ZeroBin](https://github.com/sebsauvage/ZeroBin/) project (written in PHP).

How it works
------------

When pasting a text into gbin:

![Encryption image](https://raw.githubusercontent.com/modInfo/gbin/master/encryption.png)

 * You paste your text in the browser and click the “Submit” button.
 * A random 256 bits key is generated in the browser.
 * Data is compressed and encrypted with AES using Javascript libraries.
 * Encrypted data is sent to the server and stored.
 * The browser displays the final URL with the key.
 * The key is never transmitted to the server, which therefore cannot decrypt data.

When opening a gbin URL:

![Decryption image](https://raw.githubusercontent.com/modInfo/gbin/master/decryption.png)

 * The browser requests encrypted data from the server
 * The decryption key is in the anchor part of the URL (#…) **which is never sent to the server**.
 * Data is decrypted in the browser using the key and displayed.

Install
-------

Clone this repository, build it and run it.

    go get github.com/dchest/captcha
    git clone https://github.com/modInfo/gbin
    cd gbin
    go build
    ./gbin

To run gbin on a different port, modify the Port setting in config.json.

The configuration of gbin can also be reloaded by sending a HUP signal to the process.

    kill -HUP [PROCESS ID]

Other
-----

This project modifies the Python implementation and cleans things up to make them more generic.  It has the following changes:

 * Remove extra header links.
 * Remove extra link options.
 * Remove extra layout details.

Here are some items which are in the Python implemention which have not been implemented.

 * Paste counter - Display a tiny counter for pastes created
 * Names/links to insert in the menu bar
 * Paste ID length
 * Clone paste

Copyright (c) 2016 Julian Yap  
Copyright (c) 2018 Sebastian Korotkiewicz


[MIT License](https://github.com/modInfo/gbin/blob/master/LICENSE)

