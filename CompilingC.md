## Compiling Source code for language C in Linux

I decided to compile [netboot.xyz](https://github.com/antonym/netboot.xyz) (of a great Linux and IPXE scripter, Antony Messerli) for our group project. I had some help in [one of his scripts](https://github.com/antonym/netboot.xyz/blob/master/script/prep-release.sh), where I could observe, how the compiling is done.
It's achieved by using the command `make`, assuming we have all neccesary libraries downloaded in our computer. 

At first, I tried to run the command `make` with the specification _what kind_ of file I need, _my script_ that I need to embed and _certificates_ he was adding into the compilation.
The command looked somewhat like this: `make <filename.type I need> EMBED=<myscript> TRUST=<certificate1>.crt,<certificate2>.crt`. Unfortunately, this **didn't work**, because I didn't have the mentioned certificates available. Another developer, iPXE head engineer Micheal Brown advised, that I can _skip_ the certificates in the compilation and so I did.

Next problem I ran into was "`fatal error: lzma.h: No such file or directory. Compilation terminated.`". It looked like I was missing a library, even though I tried to download all of them, including _lzma_. As it turned out (after googling for a while), I found out the library I needed was called _liblzma-dev_. I had to install it by using:
`sudo apt-get install -y liblzma-dev`.

Now the compilation worked _almost_ all the way to the end, but not entirely... This time I was missing a boot image 'isolinux.bin'. That wasn't a library. But it was a vital necessity for creating **.iso** files, which I needed. I didn't know what to do. But after googling the exact problem, I found out that someone before me already solved it. I had to download and extract 'syslinux-6.03.zip' from a specific spot on the Internet and then, already having the access to the required file, I had to '_feed_' it to the `make` command.
It looked like this: `make <desired program>.iso ISOLINUX_BIN=/<the absolute path to isolinux.bin>/isolinux.bin EMBED=/<the absolute path to my embedded script>/<filename of the embedded script>`.

That **finally** worked, error free! :-)

