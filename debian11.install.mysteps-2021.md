debian11 debian11 debian11
    netinstall iso
    gnome 

## entrar en root:
```bash
su -
```
## https://www.linuxtechi.com/things-to-do-after-installing-debian-10/

+: fix `sudo` 4 `ray` (`<username>`): `visudo /etc/sudoers` ; ALL ALL ALL ...

+: Wayland problem: modos graficos para root: sol: miniwrapper **`wsudo`** en $HOME/bin (already in $PATH in `~/.bashrc`)
```bash
#!/bin/sh
#Wayland sudo miniwrapper
xhost +local:
sudo $1 &
```

[**ufw**](https://www.linuxtechi.com/things-to-do-after-installing-debian-10/)
```bash
sudo apt install -y ufw
sudo ufw default deny  incoming
sudo ufw default allow outgoing
sudo ufw allow ssh
# sudo ufw allow 80   # if http  [web]server
# sudo ufw allow 443  # if https [web]server
sudo ufw enable
```

```bash
sudo apt install -y synaptic** (apt "grafico"; bueno para analizar dependencias y estructuras de paqueteria)
sudo apt install -y tree       # cli tool
sudo apt install -y meld       # gui 4 diff (git support)
sudo apt install -y thunar     # (buen bulk renamer)

sudo apt install -y gparted
sudo apt install -y git
```
## **sublime text 4**

from tarball: 
    deploy; 
    move to `/opt/`; `chown -R root:root /opt/sublime_text/`; 
    `sudo ln -s /opt/sublime_text/sublime_text /usr/local/bin/subl`  # **subl**
    `sudo ln -s /opt/sublime_text/sublime_text /usr/local/bin/s`     # **s**

    `cp /opt/sublime_text/sublime_text.desktop ~/.local/share/applications`)

alias: `s` n `subl` in `~/.bahsrc`.

### fix block comment toggle (fix ctl-/, ctl-shift-/) : 

En `~/.config/sublime-text/Packages/User/Default(Linux).sublime-keymap(ray)`

[
    { "keys": ["ctrl+keypad_divide"], "command": "toggle_comment", "args": { "block": false } },
    { "keys": ["ctrl+shift+keypad_divide"], "command": "toggle_comment", "args": { "block": true } },   
]

### package control: ctl+shift+p; ...

    - sidebar enhacements
    - Emmet?
    - Git?

## Must-Have Sublime Text 3 Packages:

### todo: off purchase advice

## **guake**

**guake -p**: do: { enlarge; set transparency; set F1 -not F12- to hide/show }
wayland problem? 
    I think the problem is GTK2 vs GTK3 shortcuts and how they're implemented (although I could be off-base here, that's just a rank guess). In any case, until this issue is fixed -- for anyone who loves guake and wants to keep using it, do this:
    Open the keyboard shortcuts for your environment (for Gnome, that's Settings::Keyboard::Shortcuts)
    Add a new shortcut named "Toggle Guake", with the command "guake -t", and set the hotkey for it

## **python 3**
No hay comando `python`. pero si un paquete `python3` -y otros `py*`- En su doc (`/usr/share/doc/python3/index.html`) dice:

   > The packages `python-is-python3` and `python-dev-is-python3` provide the **/usr/bin/python**, **/usr/bin/python-config** and **/usr/bin/pydoc** commands pointing to _Python3_. These packages can be installed by developers and users to use the unversioned commands. 
   NOTE: Locally installed sw not yet ported to Python3 is likely to break when installing these packages.

Instalo los dos &&:
```bash:
alias py3='python'
alias py='python '
```
E installo pip: 
```bash:
sudo apt install -y python3-pip
```
Hay **pip** (con dos accesos: `/usr/bin/pip3` y `/usr/bin/pip`  (try: diff)

##  **vlc** y **youtube-dl**
```bash:
sudo apt install -y vlc
sudo pip install youtube_dl               # https://ytdl-org.github.io/youtube-dl/download.html
sudo pip install --upgrade youtube_dl
```

## **brave-browser**:
**apt-transport-https** **curl** **gnupg**
    
https://mitrahosting.id/how-to-install-brave-browser-on-ubuntu-20-10-or-debian-11-bullseye-support-blocks-ads-and-website-trackers/

```bash:
wget -O- https://brave-browser-apt-release.s3.brave.com/brave-core.asc | gpg --dearmor | sudo tee /usr/share/keyrings/brave-browser-archive-keyring.gpg

echo "deb [arch=amd64] https://brave-browser-apt-release.s3.brave.com/ stable main" | sudo tee /etc/apt/sources.list.d/brave-browser-release.list

sudo apt update && sudo apt install brave-browser
```
## **typora**

got tarball;  { deploy, `mv /bin/` to `~`; add to `PATH` in `.bashrc` }

problem: libva error: /usr/lib/x86_64-linux-gnu/dri/iHD_drv_video.so init failed
fix: `export LIBVA_DRIVER_NAME=i965` :)

## to-do: **pandoc** _from haskell!_

1. from `.deb`: https://packages.debian.org/bullseye/pandoc 
    got pandoc: v 2.9.2.1

>   Some uses of Pandoc require additional packages: 
>    
>   SVG content in PDF output requires **librsvg2-bin**. (++) 
>   YAML metadata in TeX-related output requires **texlive-latex-extra**. (++)
>   `*.hs` filters not set executable requires ghc. 
>   `*.js` filters not set executable requires nodejs. 
>   `*.php` filters not set executable requires php.
>    `*.pl` filters not set executable requires perl.
>    `*.py` filters not set executable requires python.
>    `*.rb` filters not set executable requires ruby.
>    `*.r` filters not set executable requires **r-base-core**. (++)
>   LaTeX output, and PDF output via PDFLaTeX, require **texlive-latex-recommended**. (++)
>   XeLaTeX output, and PDF output via XeLaTeX, require **texlive-xetex**. (++) 
>   LuaTeX output, and PDF output via LuaTeX, require **texlive-luatex**. (++)
>   ConTeXt output, and PDF output via ConTeXt, require **context**. (texlive-full (++)) 
>   PDF output via wkhtmltopdf requires **wkhtmltopdf**. (--)
>   Roff man and roff ms output, and PDF output via roff ms, require **groff**. (--)
>   MathJax-rendered equations require **libjs-mathjax**. (++)
>   KaTeX-rendered equations require **node-katex**. (--)
>   option `--csl` may use **styles** in **citation-style-language-styles**. (--)

1. lo quito y lo instalo ahora **sobre haskell**:
    (howto:
    + https://ondiz.github.io/cursoLatex/Contenido/15.Pandoc.html
    + https://hackage.haskell.org/package/pandoc-1.16/src/INSTALL ( ++ path in `~/.bashrc` )

```bash:
sudo apt-get install haskell-platform   # ; cabal presente
```
see file:///usr/share/doc/haskell-platform/README.Debian: haskell-platform es un Debian meta-package 
Depending on all the haskell library packages (libghc's) (respectively haskell lib doc packages) 
and tools comprising of the Haskell Platform. It does not actually register a platform package with ghc-pkg and is a native Debian package.

```bash:
apropos haskell:
alex (1)             - the lexical analyser generator for Haskell
cabal (1)            - a system for building and packaging Haskell libraries and programs
ghc (1)              - the Glasgow Haskell Compiler
ghc-8.8.4 (1)        - the Glasgow Haskell Compiler
ghc-pkg (1)          - GHC Haskell Cabal package manager
ghc-pkg-8.8.4 (1)    - GHC Haskell Cabal package manager
ghci (1)             - the Glasgow Haskell Compiler
ghci-8.8.4 (1)       - the Glasgow Haskell Compiler
haddock (1)          - documentation tool for annotated Haskell source code
happy (1)            - the parser generator for Haskell
haskell-compiler (1) - the Glasgow Haskell Compiler
HsColour (1)         - generate colourised output for Haskell code
runghc (1)           - program to run Haskell programs without first having to compile them.
runhaskell (1)       - program to run Haskell programs without first having to compile them.
```

```bash:
cabal update                            # Actualizar lista de paquetes
cabal install pandoc                    # Instala pandoc 2.14.1 (!!)
cabal install pandoc-citeproc           # Instalar filtro de bibliografía
cabal install pandoc-crossref           # Instalar filtro de referencias cruzadas    
```
pd: ++ haskel :

```bash:
sudo add-apt-repository ppa:hvr/ghc
```
> 
    Convenient packages for GHC releases from http://www.haskell.org/ghc/ (plus cabal-install packages) which can be installed side by side for working/testing with multiple/older GHCs and/or with http://travis-ci.org

    This PPA usually provides packages for all non-EOL'ed Ubuntu releases
    (packages for EOL-ed Ubuntu LTS releases will be moved into  https://launchpad.net/~hvr/+archive/ubuntu/ghc-eol and eventually removed); see https://wiki.ubuntu.com/Releases for a list of current Ubuntu releases and their EOL status.
    
    GHC is split into 4 packages,
    
     ghc-$VER           (core package, contains ghc and executables such as haddock)
     ghc-$VER-dyn       (contains dynamic libraries for version prior to GHC 7.8)
     ghc-$VER-prof      (contains profiling libs)
     ghc-$VER-htmldocs  (contains generated HTML Haddock output)
    
    The GHC packages install into `/opt/ghc/$VER/` so in order to use them, one way is to bring a particular GHC version into scope by placing the respective `/opt/ghc/$VER/bin` folder early in the PATH environment variable.
    
    There's also a `/opt/ghc/bin` (& `/opt/cabal/bin`) folder which contains version-suffixed symlinks to installed GHC versions for convenient use with cabal (e.g. "cabal new-build -w ghc-7.8.4"), as well as symlinks managed by update-alternatives(1) which can be configured via
    
      sudo update-alternatives --config opt-ghc
      sudo update-alternatives --config opt-cabal
    
    Note that `/opt/ghc/bin` also contains a default symlink for `cabal`, so it's enough to include `/opt/ghc/bin` in your PATH to get access to both `cabal` and `ghc`.
    
    *NEW* You can find packages built specifically for Debian 9 (Stretch) at http://downloads.haskell.org/debian/
    *NEW* If you're using macOS, you can find a GHC distribution in the same spirit as this PPA over at https://haskell.futurice.com/
    *NEW* Packages optimised for Windows Subsystem for Linux (WSL) can be found at https://launchpad.net/~hvr/+archive/ubuntu/ghc-wsl
    *NEW* A GHCJS PPA is available at https://launchpad.net/~hvr/+archive/ubuntu/ghcjs
    
    See also https://github.com/hvr/multi-ghc-travis for reporting bugs/issues as well as for more information about this PPA
     More info: https://launchpad.net/~hvr/+archive/ubuntu/ghc
    Press [ENTER] to continue or ctrl-c to cancel adding it

## to-do: **texlive**

from synaptic: marcar texlive-full y quitar idiomas (español no)
then: gummi; texStudio

## to-do: ++swap:

1. etcher: https://balena.io/etcher
1. ready-bost: https://indaga.net/que-es-ready-boost-y-como-implementarlo-en-linux/
1. osboxes: https://www.osboxes.org/

## **pinta**
```bash:
# prerequisitos en https://github.com/PintaProject/Pinta &&
         git clone https://github.com/PintaProject/Pinta.git
```
to do: circular menus in gnome

fb: Fukerb3rg4s

# Emulacion y virtualizacion

<!-- ## gettings started w **qemu**

Tengo un .ova de juanda. Son tars. Lo despliego (`tar -xvf`) y tengo:
    - un .vmdk
    - un .ova
    - un .mf

con `qemu-img` convierto el `.vmdk` a `.qcow2` (formato qemu)

`convert -O qcow2 Docker-disk001.vmdk juanda.qcow2`

(si no es qemu es dogshit by Drew DeVault)[https://drewdevault.com/2018/09/10/Getting-started-with-qemu.html]

ejercicio con alpine-linux:
    ver `boot.it.sh`
    con `setup-alpine`, usar `lvm` y `sys`.

try boot.it2.sh el .https://foswiki.org/Support/HowToRunVirtualMachineImageOnKvmQemu

try https://github.com/virt-manager/virt-manager para usar el .ovf 
 -->

## docker y docker-compose: debian11: 
- [**util**](https://www.how2shout.com/linux/install-docker-ce-on-debian-11-bullseye-linux/)
- [util](https://www.digitalocean.com/community/questions/how-to-fix-docker-got-permission-denied-while-trying-to-connect-to-the-docker-daemon-socket)
- [oficial](https://docs.docker.com/engine/install/debian/)
- [docker-compose](https://dockertips.com/utilizando-docker-compose)

# to-do: openssh server

<!--stackedit_data:
eyJoaXN0b3J5IjpbMjAzMDc5MDU1MiwxOTg4NjY4MDQsMTQ2MT
g3MzM5NywtMTcwODkzMTYxXX0=
-->