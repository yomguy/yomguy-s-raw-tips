################################
# YomGuy's Linux Ultra Fast Tips
################################
======================================
YomGuy's Linux Ultra Fast Tips (1/1)
======================================

♫♪♫♪ ╔╦╦╦═╦╗╔═╦═╦══╦═╗ ♫♪♫♪♫♪
♫♪♫♪ ║║║║╩╣╚╣═╣║║║║║╩╣ ♫♪♫♪♫♪
♫♪♫♪ ╚══╩═╩═╩═╩═╩╩╩╩═╝ ♫♪♫♪♫♪

This is a list of my short command line tips to get some various,
sometimes advanced, functions on GNU/Linux systems, especially on Debian.



RENAME
======
rename more than  1 file ::

 rename 's/\_wav_/\_/g' *.pdf
 rename 's/\./\_/g' *.pdf; rename 's/\_pdf/\.pdf/' *


REPLACE
=======
replace a string in a file::

 sed -ie 's/old/new/' *.txt
 sed -i -e 's/cellar/deefuzz/g' deefuzz_cellar_mp3_234.xml

replace string in a var::
 ${var/Pattern/Replacement}
First match of Pattern, within var replaced with Replacement.
If Replacement is omitted, then the first match of Pattern is replaced by nothing, that is, deleted.
 ${var//Pattern/Replacement}
Global replacement. All matches of Pattern, within var replaced with Replacement.

 ${var/#Pattern/Replacement}
If prefix of var matches Pattern, then substitute Replacement for Pattern.
 ${var/%Pattern/Replacement}
If suffix of var matches Pattern, then substitute Replacement for Pattern.


FIND & RM
=========
find and remove::

    find ./ -iname "*.pyc" -exec rm {} \;
    find . -name ".svn" -type d -exec rm -rf {} \;
    find . -name 'test*' -mtime +30 -type f -print0 |xargs -0 rm -f
    sudo find . -mtime +480 -exec rm {} \;

FIND & CP
=========
find and copy some files::

    find -iname *.pdf -exec cp \{\} /data/pellerin/castem/pdf/ \;


FIND & LN
=========

find and link some files::

    find /data/these/simuls/ -iname *.pdf > pdf.log -exec ln -s {} \;
    find /home/momo/data/these/simuls/castax_isov_pdf/t02/* -iname *.pdf -exec ln -s {} \;


FIND & RENAME
==============
_::

    for i in ./*; do cd $i; rename 's/\./\_/g' *; cd ..; done
    for i in ./*; do cd $i; rename 's/\_pdf/\.pdf/' *; cd ..; done


FIND & MV
=========
_::

    #isof=( 46_1 25_1 )
    #isof=( 35 55 107 191 )
    isof=( p_ c_ r_ vy_ vx_ tr_ hv_ hx_ hy_ )
    #isof=( paxe vaxe iaxe v_sor p_sor p_ent v_ent t_par pp00 pp05 pp10 pp12 vp00
    vp10 residus v_col p_col tpar ppar q- )
    nf=${#isof[*]}
    for (( j = 0; j <= ($nf - 1); j++ )); do
    if [ ! -d ${isof[$j]} ]; then
    mkdir ${isof[$j]}
    fi
    mv *${isof[$j]}* ${isof[$j]}
    done


SIX CHs:
========
_::

sudo chmod -R 664 *; sudo chmod -R +rX *


LGRIND
======
_::

    lgrind -i -lmatlab ttt.m > ttt.tex
    lgrind -i -lf ttt.dgibi > ttt.tex

ICONV
=====
_::

    convmv -r --notest -f iso-8859-1 -t UTF-8 *

EXPAND
=======
_::

    expand -t4 acpi.py > acpi2.py

OCR
====
_::

    mogrify -format pbm *.png
    for i in *.pbm; do ocrad --charset=iso-8859-15 -o $i.txt $i; done

SOX
=====
_::

    for i in *.wav; do sox $i -s -w $i.wav; mv $i.wav converted/$i; done
    sox Jano_B-Homosapiens.mp3 -r 44100 -b 16 -s -t wav - | flac - -o Jano_B-Homosapiens.flac
    sox 0001\ Labelle\ -\ Nightbirds.wav -S -2 0001\ Labelle\ -\ Nightbirds.flac

CONVERT
=======
_::

    convert -density 150x150 telecaster_video01.eps telecaster_video01.png
    for i in `ls *.eps`; do convert -density 200x200 $i $i.png; done

crop::
    convert waveform_homosapiens.png -crop 100x50% waveform_homosapiens2.png
    http://www.imagemagick.org/Usage/crop/#crop_percent

to pdf::
    convert *.png -adjoin -page A4+0+300 k.parrot_id.pdf
    convert *.jpeg -adjoin -page A4 reunica_parisson_2011_1t.pdf

pdfjam --paper a4paper openerp_uXkqY2.pdf Parisson-Annexe_2-Synthese.pdf Parisson-Annexe_3-Fonctions.pdf Parisson-Annexe_4-UseCase_PB.pdf 


GCC
===
_::

    gcc -Wall -o random rand2.c
    gcc -Wall recapture.c -o recapture -ljack -lpthread -lrt -lsndfile

HDPARM
=======
_::

    sudo hdparm -c1 -d1 -a256 -u1 /dev/hdc


DVDBACKUP:
===========

_::

    dvdbackup -F -n DVD_TITLE -i/dev/dvd -o/home/karine/video/dvd/


BEAGLE:
=======
_::

    sudo apt-get install beagle; beagled --fg --debug
    best


UMOUNT (FORCE)
==============
_::

    umount -l /dev/cdrom


RAR
===
_::

    rar a -m0 -v100000 CellarMixLive_050615_mp3.rar  CellarMixLive_050615_mp3.wav
    rar a -m3 -v15000 Ce	llarMixLive_050615_mp3.rar  CellarMixLive_050615_mp3.wav


SSH
===
_::
    ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa

Remote::

    ssh -R 2222:localhost:22 parisson.com

Permanent connexion::

autossh -q -f -N -R 2201:localhost:22 augustins.pre-barreau.com


ECASOUND
========
ecasound -a:1 -i foo1.wav -a:2 -i foo2.wav -o jack_alsa
cat f*.wav | ecasound -i stdin -o concat.wav


APT
===
Le dï¿œpï¿œt maï¿œtre de chez debian

wget http://ftp-master.debian.org/ziyi_key_2006.asc -O - | sudo apt-key add -

-  Le dï¿œpï¿œt debian-marillat

gpg --keyserver hkp://wwwkeys.eu.pgp.net --recv-keys 1F41B907
gpg --armor --export 1F41B907 | sudo apt-key add -

-  Le dï¿œpï¿œt volatile

wget http://volatile.debian.net/ziyi-2005.asc -O - | sudo apt-key add -

echo "deb http://debian.parisson.org binary/" | sudo tee -a /etc/apt/sources.list


WAITING FOR PROCESS:
======================
_::

    dt=10
    prog1="psextract.sh"
    prog2="/home/pellerin/castax/bin/psextract.sh /data/pellerin/castem/t02 8 /home/pellerin/castax_res/castax_isov_pdf/t02"

    while [ ! -z `pgrep $prog1` ]; do
    sleep $dt
    date
    echo "waiting for $prog1 to finish..."
    done &&

    echo "$prog1 finished, launching $prog2"
    $prog2


MYSQL:
=======

root pass:
sudo /usr/bin/mysqladmin -u root password 'washnc.....'


mysql> create database forum;
mysql> GRANT ALL PRIVILEGES ON forum.* TO 'moderateur'@localhost
mysql> GPG 'mot_de_passe_du_moderateur';


The following will create a database named "intranet".

mysqladmin -p create intranet

Next, create the database user account that will be used to access the database.

mysql -p --user=root intranet

mysql> GRANT ALL PRIVILEGES ON *.* TO intranet@localhost
IDENTIFIED BY 'webcal01' WITH GRANT OPTION;
mysql> FLUSH PRIVILEGES;
mysql> QUIT

If you will be accessing MySQL from a different machine than the one running the web server, repeat the command above and replace 'localhost' with the hostname of the other machine.

Create the calendar tables using the supplied tables-mysql.sql file:

mysql -p intranet < tables-mysql.sql

In the above example, "intranet" is the name of your database.

CHANGE ROOT PASS
 Alternativement, sur toutes les plate-formes, vous pouvez aussi choisir le nouveau mot de passe en utilisant le client mysql :

   1. Stoppez et redï¿œmarrez mysqld avec l'option --skip-grant-tables comme dï¿œcrit plus haut.
   2. Connectez vous au serveur mysqld avec :

      shell> mysql -u root mysql

   3. Exï¿œcutez la commande suivante dans le client mysql :

      mysql> UPDATE user SET Password=PASSWORD('nouveaumotdepasse')
          ->             WHERE User='root';
      mysql> FLUSH PRIVILEGES;

   4. Aprï¿œs cela, vous devriez pouvoir vous connecter avec le nouveau mot de passe.

backup:
    mysqldump -u username -p dbname table1 > dump.sql

set value:
    use novatix000501;
    update div_royreport SET montant=0.0 ;


create database askbot DEFAULT CHARACTER SET UTF8 COLLATE utf8_general_ci;
grant all privileges on dbname.* to dbuser@localhost identified by 'dbpassword';


TRANSCODE
=========
_::

    ls -1 | grep .png > image_list.txt

    transcode -i image_list.txt -x imlist,null -g 720x480 --use_rgb -z -y ffmpeg,null -F mpeg4 -o test1.avi -H 0 -f 29.97

    transcode -z -M 2 -x v4l,v4l -i /dev/video0 --import_v4l 0,38 -p /dev/dsp -y xvid -o test.avi -w 1500 -e 32000 -E 44100 -b 96 -s 7 -c 0-250 -g 360x288 -j 0,4

    ffmpeg -i video.mp4 -vn -acodec pcm_s16le -ar 44100 -ac 1 bleriot11.wav

    ffmpeg -ss 80 -t 10 -i test_xvid.avi -f flv -vcodec flv -vb 500k -ab 96k -ar 44100 -y test.flv

remuxing::

   ffmpeg -i in.webm -vcodec copy -acodec copy -f webm -y out.webm

ffmpeg -i input -vcodec libx264 -preset fast -tune film -profile main -crf 22 -threads 0 output

KERNEL CUSTOM
=============

apt-get install kernel-package libncurses5-dev fakeroot wget bzip2

patch::

export patch="snd-usb-audio-FTP-2.6.39-yomguy.patch"; echo "Signed-off-by: Guillaume Pellerin <yomguy@parisson.com>" > ../$patch; diff -urB -x*.o -x*.cmd -x*.mod.c -x*.order -x*.ko -x*.c.orig  ../tmp/linux-source-2.6.39/sound/usb sound/usb >> ../$patch & ./checkpatch.pl ../$patch

    # diff -uprN linux-2.6.15 linux-2.6.15-rt1 > patch-2.6.15-rt1-1
    patch -p0 linux-2.6.15 > patch-2.6.15-rt1-1

    api linux-source-2....
    cd /usr/src/linux/

ou:

bzip2 -dc /usr/src/patch-2.6.31.4-rt14.bz2 | patch -p1 --dry-run

If you didn’t get any errors (which you shouldn’t) then do:
bzip2 -dc /usr/src/patch-2.6.31.4-rt14.bz2 | patch -p1

Now the kernel source is patched with the real time preemption code by Ingo Molnar.

Next is the M-Audio USB Fast Track Pro patch:
patch -p1 /usr/src/linux/sound/usb/usbaudio.c < /usr/src/usbaudio-ftp-2.6.31.4.patch

MT :
export CONCURRENCY_LEVEL=4


Then run the following commands (please note that make dep is not needed any more for kernel 2.6)::

    make-kpkg clean

    make-kpkg --rootcmd fakeroot --initrd --revision=1 --append-to-version=-amd64-yomguy kernel_image kernel_headers


CROSS i386
------------------
Install 32bit tools (ia32-libs, lib32gcc1, lib32ncurses5, libc6-i386, util-linux, maybe some other ones)
Download & unpack your kernel sources
run "linux32 make menuconfig" and configure your kernel for your new machine
clean your build dirs "make-kpkg clean --cross-compile - --arch=i386" (only needed on consecutive compiles)
compile your kernel "nice -n 100 fakeroot linux32 make-kpkg --cross-compile - --arch=i386 --revision=05test kernel_image" for faster compilation on multi-CPU machines run "export CONCURRENCY_LEVEL=$((`cat /proc/cpuinfo |grep "^processor"|wc -l`*2))" first
At this point you have a 32bit kernel inside a package labeled for 64bit arch. We need to fix this, run "fakeroot deb-reversion -k bash ../linux-image-2.6.35.3_05test_amd64.deb". Open the file DEBIAN/control with vim/emacs and change "Architecture: amd64" to "Architecture: i386" exit the bash process with ctrl+d
That's it, now just transfer the re-generated deb to destination machine and install it.

export CONCURRENCY_LEVEL=6
linux32 make menuconfig
linux32 make-kpkg --cross-compile - --arch=i386 --rootcmd fakeroot --initrd --revision=1 --append-to-version=-i386-yomguy kernel_image kernel_headers

or in CHROOT:
export CONCURRENCY_LEVEL=6
export LANGUAGE=fr_FR.UTF-8
export LC_ALL=fr_FR.UTF-8
export DEB_HOST_ARCH=i386 
export ARCH=i386 
make-kpkg --rootcmd fakeroot --initrd --append-to-version=-yomguy-ftp kernel_image kernel_headers

At this point you have a 32bit kernel inside a package labeled for 64bit arch. We need to fix this, run "

fakeroot deb-reversion -k bash ../linux-image-2.6.35.3_05test_amd64.deb

Open the file DEBIAN/control with vim/emacs and change "Architecture: amd64" to "Architecture: i386" exit the bash process with ctrl+d

That's it, now just transfer the re-generated deb to destination machine and install it.


HELP!

If the compilation stops with an error, run::

    make clean

and then re-run the previous commands starting with::

    make menuconfig

Change the kernel configuration where the error occurs. If no error occurs you will find the new kernel as a Debian package called kernel-image-2.6.8.1_custom.1.0_i386.deb under /usr/src::

    cd ../

Now you have to install some packages that are needed by kernel 2.6. Add the following line to /etc/apt/sources.list::

    deb http://www.backports.org/debian/ woody module-init-tools initrd-tools procps

Then run::

    apt-get update
    apt-get install module-init-tools initrd-tools procps

If you are asked the following question:
"If you really want to remove modutils type 'yes':"
type yes.

It might also be necessary to update packages like bind9, quota, etc. - depending on your configuration. If you have problems with your existing packages try to get the appropriate package from www.backports.org.
Install your new kernel::

    dpkg -i kernel-image-2.6.8.1_custom.1.0_i386.deb

OPTION:

Create a ramdisk of your new kernel (otherwise your system will most likely not boot)::

    cd /boot/
    mkinitrd -o /boot/initrd.img-2.6.8.1 2.6.8.1

LILO:

We are almost finished now. Edit the image=/vmlinuz stanza of your /etc/lilo.conf and add the line  initrd=/boot/initrd.img-2.6.8.1::

    ###
    # Boot up Linux by default.
    #
    default=Linux
    #
    image=/vmlinuz
            label=Linux
            read-only
            initrd=/boot/initrd.img-2.6.8.1
    #        restricted
    #        alias=1
    ###

Run::

    lilo

to update your boot loader and reboot your machine::

    shutdown -r now

and if everything is ok your machine should come up with the new kernel. You can run::

    uname -a


RT TEST
========

~/dev/linux/rt-tests/cyclictest  -t1 -p 80 -n -i 10000 -l 10000


DEBOOTSTRAP
==========

sudo cdebootstrap --arch i386 squeeze chroot/debian32 http://mirror.ovh.net/debian/
sudo cdebootstrap --arch amd64 sid chroot/sid64 http://mirror.ovh.net/debian/

SSH KEYS
========

www.linuxjournal.com/article/8400

!! home user dir MUST be 770 !!



GPG APT KEYS
=============
_::

    sudo su
    gpg --keyserver hkp://keyring.debian.org --recv-keys F1D53D8C4F368D5D
    gpg --armor --export 010908312D230C5F | apt-key add -


DEBMIRROR
=========
_::

    wget http://ftp-master.debian.org/ziyi_key_2006.asc

Avoir une partition avec de la place, par exemple /mnt/mirror (~20 Go)::

    # apt-get install debmirror

Pour creer / mettre a jour le miroir (pour les 3 distribs, par exemple) :
$ debmirror /mnt/mirror --arch=i386 --dist=woody,sarge,sid -h ftp.fr.debian.org --nosource --verbose --progress
Ensuite, dans /etc/apt/sources.list :
deb file:/mnt/mirror sid main non-free contrib
Et ï¿œvidemment faire un apt-get update pour mettre ï¿œ jour.


WIFI
====

kismet airsnort aircrack wmwave wpasupplicant kwirelessmonitor macchanger swscanner wavemon wireless-tools
wifi-radar iwconfig iwlist


ZOPE
=====

api python2.3-zodb

Backup:
python2.3 repozo.py -Bzv -r /nfs/place/where/backup/files/go  -f /path/to/Data.fs

Recover
python2.3 repozo.py -Rv -r /nfs/place/where/backup/files/go  -o /path/to/Data.fs

ou

Backup:/home/momo/data/tmp/test
sudo python2.3 /usr/lib/zope2.8/bin/repozo.py -Bzv -r /home/momo/backups/parisson_zope -f  /var/lib/zope2.8/instance/parisson.com/var/Data.fs
sudo python2.3 /usr/lib/zope2.7/bin/repozo.py -Bzv -r /home/momo/backups/ev/plone/ -f /var/lib/zope2.7/instance/plone_EV/var/Data.fs

Recover:
sudo python2.3 /usr/lib/zope2.8/bin/repozo.py -Rvz -r /home/momo/backups/parisson_zope -o /var/lib/zope2.8/instance/parisson.com/var/Data.fs
sudo python2.3 /usr/lib/zope2.7/bin/repozo.py -Rvz -r /home/momo/backups/ev/plone -o  /var/lib/zope2.7/instance/plone_EV/var/Data.fs

SHELL

svn co http://svn.plone.org/svn/collective/dotipython/trunk/ipy_profile_zope.py .
sudo su zope
./bin/zopectl shell
ipython2.4 -p zope

>> for id,val in obj.objectItems():
...     try: val.getId()
...     except POSKeyError: break

# "id" should now contain the id with the broken object.

9. You can now delete the "bad" object:

>> obj.manage_delObjects(id)
>> get_transaction().commit()

# The second line is necessary to save your change.

10. In my case, I needed to re-create the bad user folder object:

>> obj.manage_addUserFolder('acl_users')
>> get_transaction().commit()

If you needed to re-create a bad DTMLMethod, it would be something like:

>> obj.manage_addDTMLMethod('method_id')
>> get_transaction().commit()




PLONE 3 / BUILDOUT
===================
_::

    easy_install -U ZopeSkel
    paster create --list-templates
    paster create -t plone3_buildout myproject
    cd myproject
    python bootstrap.py
    ./bin/buildout
    vi buildout.cfg
    ./bin/instance fg


OV511
=====
_::

    sudo modprobe ov511
    sudo modprobe ovcamchip


FUSERMOUNT
==========
_::

    encfs /path/.test /path/test
    (chmod 4755 /usr/bin/fusermount)
    sudo mount -a
    fusermount -u /path/test



KERNEL REALTIME
================
_::

    api realtime-lsm-source
    sudo module-assistant
    sudo modprobe realtime gid=29


AWSTATS
=======
_::

    sudo /usr/share/doc/awstats/examples/awstats_buildstaticpages.pl -update \
    -config=/etc/awstats/awstats.conf \
    -dir=/var/www/pypix.com/stats/ \
    -awstatsprog=/usr/lib/cgi-bin/awstats.pl


CSS
====
_::

    #header { background: url(/images/main_header_bg.gif) repeat-x 0 0; line-height: 0.8;}


GNUMP3D
========
song_format = $TRACK - $ARTIST - $ALBUM - $SONGNAME [ $GENRE - $LENGTH / $SIZE ] $NEW


NVIDIA Debian
=============
_::

    nvidia-installer --uninstall
    apt-get install xserver-xorg-dev

ou::

    ./nvidia***.run --x-module-path=/usr/lib/xorg/modules/

http://wiki.debian.org/NvidiaHowTo
http://www.nvnews.net/vbulletin/showthread.php?t=75175
ftp://download.nvidia.com/


WAV 2 MODEM
===========
    _::
    sox file00.wav -r 7200 file.wav
    wavtopvf file.wav | pvftormd Rockwell 4 > standard.rmd


PROXY
=====
apt::
	export http-proxy=http://adresse_proxy:port_proxy
	export "http_proxy=http://login:motdepasse@adresse_proxy:port_proxy"

firefox::
	foxyproxy


COUNT
======
_::

    ls -1 | wc -l


PDF
====
_::
    pdf2pdf

    pdfcrop --margins '5 10 5 20' --clip toto.pdf toto_c.pdf
    pdf270 toto_c.pdf 

FLUMOTION
==========
_::

 flumotion-manager -v -T tcp ../webm.xml 
 flumotion-worker -v -T tcp -u user -p test
 flumotion-admin 
 sudo /usr/bin/flumotion-worker -D --daemonize-to /var/cache/flumotion -n default /etc/flumotion/workers/default.xml

DOCBOK SGML2HTML
================
_::

    db2html -o html telemeta.sgml


EPSTOPDF
=========
_::

    epstopdf sch_thev_1.ps
    pdfcrop --margins '5 10 5 20' --clip sch_thev_1.pdf sch_thev_1.pdf


DIFF
====
_::

    diff -urNp ./  /home/momo/zope2.9/pre-barreau/Products/PloneTranslations/i18n/ > /home/momo/backups/pre-barreau/i18n.patch


PYTHON
=======
_::
    import time
    time.strftime("%Y_%m_%d-%H_%M_%S")


Exemple 10.6. openAnything ::


    def openAnything(source):                  1
        # try to open with urllib (if source is http, ftp, or file URL)
        import urllib
        try:
            return urllib.urlopen(source)      2
        except (IOError, OSError):
            pass

        # try to open with native open function (if source is pathname)
        try:
            return open(source)                3
        except (IOError, OSError):
            pass

        # treat source as string
        import StringIO
        return StringIO.StringIO(str(source))  4



JAVA
====
_::

    fakeroot make-jpkg jre-1_5_0_11-linux-i586.bin
    update-alternatives --config java


DJANGO / TELEMETA
==================
_::
    python manage.py syncdb
    python manage.py sql telemeta
    sqlite3 test.db
    .list
    .schema

    ALTER TABLE "table_name"
    [alter specification]

[alter specification] is dependent on the type of alteration we wish to perform.
For the uses cited above, the [alter specification] statements are:

    * Add a column: ADD "column 1" "data type for column 1"
    * Drop a column: DROP "column 1"
    * Change a column name: CHANGE "old column name" "new column name" "data type for new column name"
    * Change the data type for a column: MODIFY "column 1" "new data type"

locales::

    cd telemeta

    django-admin makemessages -l fr
    django-admin makemessages -d djangojs -l fr
    django-admin compilemessages

South::

 ./manage.py syncdb
 ./manage.py schemamigration telemeta --initial
 ./manage.py migrate telemeta --fake
 ./manage.py migrate telemeta

./manage.py schemamigration telemeta --auto
./manage.py migrate telemeta


QUCS
====
_::

    ps2epsi sch_exam_ex1.ps


OGG2MP3
=======
_::

    oggdec -o - test.ogg | lame -V 6 - test.mp3


INSTALL DEBIAN SERVER
=====================
_::

    sudo apt-get install apache2 php5 mysql-server postfix icecast2 zope2.9 libapache2-mod-php5 arno-iptables-firewall python htop munin munin-node fail2ban python-imaging python-zodb


POUTRER UN SITE (!)
===================
_::

    sudo /usr/sbin/ab -n 1000000 -c 100 http://www.redevanceculturelle.net/


FTP RECURSIVE
===============
_::

    yafc domain.com:/home
    get -rp *

WEP
===
_::

    sudo airodump-ng --write yomix.cap --channel 9 eth1
    sudo airodump-ng --write yomix.cap --bssid 00:14:A5:8B:AF:0A --channel 9 eth1
    sudo aireplay-ng -3 -e yomix -a 00:0C:F1:3B:3D:B5 -b 00:0C:F1:3B:3D:B5 -h 00:0C:F1:3B:3D:B5 eth1
    sudo aircrack-ng -z yomix.cap

CHROOT
======
_::

    chroot ./
    mount -t proc none /proc

SSL (apache)
=============
_::

    sudo openssl genrsa -out privkey.pem 2048
    sudo openssl req -new -key privkey.pem -config /etc/ssl/openssl.cnf -days 3650 -out cert.csr
    cp server.key server.key.org
    openssl rsa -in server.key.org -out server.key

MENCODER
========
Mov to Flv

Pour passer du format .mov ï¿œ .flv il suffit d'utiliser cette commande::

    mencoder nom_de_la_video_encoder.mov -ofps 15 -ovc lavc -lavcopts vcodec=flv:acodec=mp3 -vop scale=largeur:hauteur -ffourcc FLV1 -oac mp3lame -o nom_de_sortie_de_la_video.flv

(Note : Expliquer l'utilitï¿œ de -ofps xx)
N'oublier pas de modifier la commande avec vos valeur de hauteur et de largeur .

Mkv to Avi
Pour passer du format .mkv ï¿œ .avi , il existe deux commande possible via mencoder::

    mencoder nom_du_fichier.mkv -ovc copy -oac copy -o nom_du_fichier.avi

    for fichier in `ls *.mkv`; do mencoder $fichier -ovc copy -oac copy -o $fichier.avi; done

    mencoder -oac mp3lame -lameopts cbr=128 -ovc xvid -xvidencopts bitrate=900 nom_du_fichier.mkv -o nom_du_fichier_final.avi


WIRED
======
_::

    sudo apt-get install gettext cvs autotools-dev libxml2-dev libwxgtk2.6-dev wx-common libsoundtouch1-dev libsndfile1-dev libsamplerate0-dev dssi-dev libflac++-dev libvorbis-dev libasound2-dev

    export LD_LIBRARY_PATH=/usr/local/lib

DJANGO
========

RESET PASS
Deep:/opt/webapps/invisible bruce$ ./manage.py shell
Python 2.5 (r25:51918, Sep 19 2006, 08:49:13)
Type "copyright", "credits" or "license" for more information.

IPython 0.7.2 -- An enhanced Interactive Python.
?       -> Introduction to IPython's features.
%magic  -> Information about IPython's 'magic' % functions.
help    -> Python's own help system.
object? -> Details about 'object'. ?object also works, ?? prints more.

In [1]: from django.contrib.auth.models import User

In [2]: users = User.objects.all()

In [3]: users
Out[3]: [<User: admin>]

In [4]: users[0].set_password('whatever');

In [5]: users[0].save()

TELEMETA IMPORT WAV
===================
_::
    ./manage.py shell
    from telemeta.models import MediaItem
    MediaItem.objects.filter(id='BM.2006.002.001--25__01-01')
    i = MediaItem.objects.get(id='BM.2006.002.001--25__01-01')
    i.file=('items/2008/09/01/CNRSMH_2006_002_001_01.wav')
    i.save()


SVN
====
_::

    svn propdel svn:executable mp3player.swf
    svn merge -r 119:head http://svn.parisson.org/svn/deefuzzer/trunk/
    svn merge -r174:175 trunk/ tags/telecaster-0.4.0+rc1/
    svn propedit svn:externals .

        deefuzzer http://svn.parisson.org/svn/deefuzzer/trunk



DIFF
====
_::

    diff -Naur olddir newdir > new-patch

PATCH
=====
_::
    patch -p0 <new-patch
    patch -p1 <new-patch

SVN
====
_::
    svn-buildpackage --svn-builder="pdebuild --debsign-k yomguy@altern.org"

ALIOTH
=======
_::
    svn co svn+ssh://yomguy-guest@alioth.debian.org/svn/pkg-icecast/
    http://alioth.debian.org/account/

DEBUILD
=========
_::
    svn-buildpackage --svn-builder="pdebuild --debsign-k yomguy@altern.org"

MGE
====
 MGE UPS SYSTEMS distributes the PSP package for Debian GNU/Linux through the APT method.

To install Personal Solution Pac on Debian or Ubuntu, add the following line in the "/etc/apt/sources.list"

    * deb http://opensource.mgeups.com/stable/debian binary/

Then, type the following commands, in a console as root:

    * apt-get update
    * apt-get install mgeups-psp

Note that you can also use the graphical method through Synaptic, Adept, Kynaptic and Kpackage.

Launch Personal Solution Pac from the menu "System" and enter the root password when prompted.

FFMPEG DVDGRAB
===============
_::

    ffmpeg2theora -f avi -x 320 -y 240 --deinterlace -v 4 -a -1 -o test.ogg video.avi

    dvgrab --format raw - | ffmpeg2theora -f dv -x 320 -y 240 --deinterlace -v 4 -a -1 -o /dev/stdout | oggfwd yourserver yourport yourpass /yourmountpoint.ogg

    sudo dvgrab - | vlc --no-sub-autodetect-file - :demux=rawdv ":sout=#transcode{vcodec=mp4v,vb=256,scale=1,deinterlace}:duplicate{dst=display,dst=std{access=http,mux=ts,dst=:1234}}"

    dvgrab -buffers 1 - | ffmpeg -f dv -i - -f jack -i ffmpeg -vcodec libtheora -b 400k -s 768x480 -aspect 16:9 -acodec libvorbis -ab 64000 -f ogg - -map 0.0 -map 1.0 | oggfwd -d "pb_video_live" -g "Teaching"  -n "pb_video_live" localhost 8000 source2parisson /pb_video_live.ogg &

    sleep 3
    jack_connect jack_rack:out_1 ffmpeg:input_1
    jack_connect jack_rack:out_2 ffmpeg:input_2


OPENERP
=======

initialize the database::

    sudo su - postgres -c "createdb -q --encoding=UNICODE parisson"
    sudo su - postgres -c "createuser -q --createdb --adduser parisson"


DEBIAN MUTIMEDIA
==================

cinelerra dvd-slideshow dvdrip libmjpegtools0 libquicktimehv mandvd mjpegtools ogmrip-mpeg pytube subtitleripper transcode

RE
==

file:///home/momo/doc/python/diveintopython-5.4/html/regular_expressions/summary.html

    * ^ reconnaï¿œt le dï¿œbut d'une chaï¿œne.
    * $ reconnaï¿œt la fin d'une chaï¿œne.
    * \b reconnaï¿œt la limite d'un mot.
    * \d reconnaï¿œt un chiffre.
    * \D reconnaï¿œt un caractï¿œre non-numï¿œrique.
    * x? reconnaï¿œt un caractï¿œre x optionnel (autrement dit, il reconnaï¿œt un x zï¿œro ou une fois).
    * x* reconnaï¿œt zï¿œro ou plus x.
    * x+ reconnaï¿œt un ou plusieurs x.
    * x{n,m} reconnaï¿œt un caractï¿œre x au moins n fois, mais pas plus de m fois.
    * (a|b|c) reconnaï¿œt soit a soit b soit c.
    * (x) en gï¿œnï¿œral est un groupe identifiï¿œ. Vous pouvez obtenir la valeur de ce qui a ï¿œtï¿œ reconnu ï¿œ l'aide de la mï¿œthode groups() de l'objet retournï¿œ par re.search.

Patitions deefuzzer
====================
/boot   300 MB
/       20 GB
/home   136.7 GB
swap    3 GB


CLONING CLONE
=============

install grub2

sfdisk -d /dev/sda | sfdisk /dev/sdb

SSD on /dev/sda::

  root 10 Go XFS BOOTABLE
  home 35 Go XFS
  data 15 Go XFS

USB Disk on /dev/sdb::

    root 5 Go XFS
    home 10 Go XFS

Master machine system /dev/sda to USB external Ghost /dev/sdb (Check hdparm / sdparm before)::

 su

 mkdir /mnt/root
 mount /dev/sdb1 /mnt/root
 mount /dev/sdb2 /mnt/root/home

 rsync -a --delete --one-file-system / /mnt/root/
 rsync -a --delete --one-file-system /home/ /mnt/root/home/
 sync

 umount /mnt/root/home
 umount /mnt/root

Live Install ISO on USB Disk /dev/sdb BOOT

Ghost on USB Disk /dev/sdc

Destination SSD /dev/sda::

 (AUTO)
 su
 mkdir /mnt/root
 mount /dev/sda1 /mnt/root
 mount /dev/sda2 /mnt/root/home
 mount /dev/sdc1 /mnt/ghost_root
 mount /dev/sdc2 /mnt/ghost_home
 if updating::
	 rsync -a --one-file-system -exclude=/etc/fstab -exclude=/etc/hosts -exclude=/etc/hostname /mnt/ghost_root/
else::
	 rsync -a --one-file-system /mnt/ghost_root/ /mnt/root/

 /mnt/root/
 rsync -a /mnt/ghost_home/ /mnt/root/home/
 sync
 umount  /mnt/ghost_root/
 umount  /mnt/ghost_home/
 mount -o bind /dev /mnt/root/dev
 mount -t proc none /mnt/root/proc
 chroot /mnt/root/
 ls -alh /dev/disk/by-uuid

(MANU)
 nano /etc/fstab
 (edit to get right UUID, save)

(AUTO)
 grub-install /dev/sda
 update-grub
update-initramfs -u -k all
 exit
 umount /mnt/root/proc
 umount /mnt/root/dev
 umount /mnt/root/home
 umount /mnt/root
 reboot


OR ?::
    grub-install /dev/sda
        grub
        root (hd0,1)
        setup (hd0)
    quit

By default grub2 in debian will not add 'resume=/dev/swap-partition' option.
But if you want to perform this by default you can edit /etc/grub.d/10_linux file and make some changes there:
Replace


linux  ${rel_dirname}/${basename} root=${linux_root_device_thisversion} ro ${args}
with this

linux  ${rel_dirname}/${basename} root=${linux_root_device_thisversion} ro ${args} resume=`swapon -s | grep '/dev/sd.[0-9]' -o`
This will add your first swap partition to all found linux entries.

http://wiki.debian.org/Grub

http://linux.derkeiler.com/Mailing-Lists/Debian/2008-05/msg01890.html

keep your packages::

    sudo dpkg --get-selections > packages.txt
    sudo dpkg --set-selections < packages.txt
    sudo apt-get dselect-upgrade


TC NET BACKUP
=========

ssh root@192.168.0.13 -c "mount /dev/sdb1 /mnt/backup" 
sudo rsync -a --exclude=trash --exclude=/proc/ --exclude=/dev/ --exclude=/sys/ --delete / root@192.168.0.13:/mnt/backup/

rsync -a --exclude=etc/fstab --exclude=etc/hosts --exclude=etc/hostname /mnt/backup/ /mnt/custom/



AMAROK
=======
libxine1-ffmpeg

PLONE 3
=========
python2.4
pil
zodb
elementree
iw.fss ?

RSYNC
=====
_::

    rsync -ra --update
    sudo rsync -a --include="*/" --include="*/Maildir/*"  --exclude="*" /home/ root@jimi.parisson.com:/home/tmp/


SDPARM
========
_::

    sdparm --command=ready /dev/sdc # check ready state
    sdparm --command=start /dev/sdc # start a sleeping disk
    sdparm --command=stop /dev/sdc # put a disk in standby
    sdparm -al -f /dev/sdc # list all known mode flags
    sdparm -6 -p po --clear=STANDBY /dev/sdc # turn off standby feature
    sdparm -6 -p po --defaults /dev/sdc # establish it again

ANDROID
==========

Tetherbot tunnel::

    ./adb forward tcp:4444 localabstract:Tunnel

    android create avd -n my_android1.5 -t 2
    emulator -avd my_android1.5

Running Scripts Externally

Start python terminal::

    $ adb forward tcp:4321 tcp:<AP_PORT>
    $ export AP_PORT=4321

    $ python2.6
        Python 2.6
        Type "help", "copyright", "credits" or "license" for more information.
        >>> import android  # The ASE android.py module should be on your sys.path.
        >>> droid = android.Android()
        >>> droid.makeToast("Hello from my computer!")
        >>> droid.speak('Hello')

Proxy::
    connect phone
    $ sudo /etc/init.d/udev restart
    $ adb forward tcp:8081 tcp:8081



CONEXTANT
=========
_::

    sh cnxtinstall.run -- --tty
    pppd call free

http://www.linuxant.com/drivers/hsf/full/archive/hsfmodem-7.80.02.04full/hsfmodem_7.80.02.04full_k2.6.28_13_server_ubuntu_i386.deb.zip



FFMPEG H264 Android
===================
Convert a video to MP4 compatible with Android / Iphone::

    ffmpeg -i inputfilename.ext -aspect 3:2 -s 480x320 -vcodec h264 -b 480k -r 23.976 -acodec aac -ab 96k -sameq -pass 1 outputfilename.mp4
    Here is the command for a 4:3 aspect ratio video.
    ffmpeg -i inputfilename.ext -aspect 3:2 -s 400x300 -vcodec h264 -b 480k -r 23.976 -acodec aac -ab 96k -padtop 10 -padbottom 10 -padleft 40 -padright 40 -sameq -pass 1 outputfilename.mp4
    And here is the command for a 16:9 aspect ratio video.
    ffmpeg -i inputfilename.ext -aspect 3:2 -s 480x270 -vcodec h264 -b 480k -r 23.976 -acodec aac -ab 96k -padtop 24 -padbottom 26 -sameq -pass 1 outputfilename.mp4

ffmpeg -i barbapapa_vol4.ogv -t 00:01:00 -vcodec mpeg4 -s 480x320 -b 340k  -acodec libfaac -ab 96k barbapapa_vol4.mp4

for i in *.ogv; do ffmpeg -i $i -vcodec mpeg4 -s 480x320 -b 340k -acodec libfaac -ab 64k $i.mp4; done


Extracting all frames from a video file is easily achieved with FFmpeg.

Here's a simple command line that will create 25 PNG images from every second of footage in the input DV file. The images will be saved in the current directory.::

    ffmpeg -i input.dv -r 25 -f image2 images%05d.png

The newly created files will all start with the word "images" and be numbered consecutively, including five pre-appended zeros. e.g. images000001.png.

From a video that was 104 seconds long, for a random example, this command would create 2600 PNG files! Quite messy in the current directory, so instead use this command to save the files in a sub-directory called extracted_images::

    ffmpeg -i input.dv -r 25 -f image2 extracted_images/images%05d.png

Moving on, let's say you just wanted 25 frames from the first 1 second, then this line will work::

    ffmpeg -i input.dv -r 25 -t 00:00:01 -f image2 images%05d.png

The -t flag in FFmpeg specifies the length of time to transcode. This can either be in whole seconds or hh:mm:ss format.

Making things a little more complex we can create images from all frames, beginning at the tenth second, and continuing for 5 seconds, with this line::

    ffmpeg -i input.dv -r 25 -ss 00:00:10 -t 00:00:05 -f image2 images%05d.png

The -ss flag is used to denote start position, again in whole seconds or hh:mm:ss format.

Maybe extracting an image from every single frame in a video, resulting in a large number of output files, is not what you need. Here's how to create a single indicative poster frame, of the video clip, from the first second of footage::

    ffmpeg -i input.dv -r 1  -t 00:00:01 -f image2 images%05d.png

Notice that the -r flag is now set to 1.

If you want the poster frame from a different part of the clip, then specify which second to take it from using the -ss tag, in conjunction with the line above.

Lastly, if you wanted to create a thumbnail story board, showing action throughout the entire length of the video clip, you'll need to specify the output image dimensions. Use the following line::

    ffmpeg -i input.dv -r 1 -f image2 -s 120x96 images%05d.png

My original file was 720x576, so the image dimensions are a whole division of this.

RST
===
reStructured text to HTML::

    rst2html -stg tips.txt tips.html
    rst2s5 --theme medium-black tips.txt tips.html
    rst2html -stg --stylesheet="lsr.css" --traceback tips.txt tips.html

http://rst2a.com/gallery/html/


TELEMETA
========

apply the same wav file for all items (mysql)::

    update media_items set filename = 'items/test.wav';


FUNIONFS
========
merge multiple dirs ::

    funionfs -o dirs=1001:mama -o allow_other NONE media


ICEDOVE
========
user_pref("network.protocol-handler.app.http", "/usr/bin/google-chrome");
user_pref("network.protocol-handler.app.https", "/usr/bin/google-chrome");


POSTFIX
========
postqueue -p
postcat -q 9DF7520804A

MAC ADDRESS (windows)
=====================
c:\ping 192.168.0.2
c:\arp -a

Xorg
====
Xorg -configure
Xorg -config xorg.conf.new


GIT
===

$ cd /var/cache/git/

$ mkdir project.git

$ cd project.git

$ git init

$ echo "Short project's description" > .git/description

$ git config --global user.name "Your Name"

$ git config --global user.email "you@example.com"

$ git commit -a

$ git push upload master

$ git archive master | gzip > latest.tgz

$ git log --graph --oneline --all



# On branch master
git checkout gh-pages
git checkout master -- myplugin.js
git commit -m "Update myplugin.js from master"
 


GIT-SVN
======

mkdir deefuzzer.git
cd deefuzzer.git
git svn init http://svn.parisson.org/svn/deefuzzer/trunk --no-metadata
vi ../authors.txt (yomguy = Guillaume Pellerin <yomguy@parisson.com>)
git config svn.authorsfile ../authors.txt
git svn fetch

git clone git+ssh://parisson.com/var/git/deefuzzer.git deefuzzer.git

BRZ-GIT
======
mkdir telemeta.git
cd telemeta.git
git init
bzr fast-export --export-marks=../marks.bzr ../telemeta-unstable | git fast-import --export-marks=../marks.git
bzr fast-export --export-marks=../marks.bzr --git-branch=crem ../telemeta-crem  | git fast-import --import-marks=../marks.git --export-marks=../marks.git 
git config --global user.name "yomguy"
git config --global user.email "yomguy@parisson.com"
git remote add origin git+ssh://angus.parisson.com/var/git/telemeta.git
git push origin master
git pull origin master

Fix wrong author:

git filter-branch --commit-filter '
        if [ "$GIT_COMMITTER_EMAIL" = "" ];
        then
                GIT_COMMITTER_NAME="yomguy";
                GIT_AUTHOR_NAME="yomguy";
                GIT_COMMITTER_EMAIL="yomguy@parisson.com";
                GIT_AUTHOR_EMAIL="yomguy@parisson.com";
                git commit-tree "$@";
        else
                git commit-tree "$@";
        fi' HEAD


on repo::
git update-server-info


GITHUB
======

Global setup:
 Set up git
  git config --global user.name "Guillaume Pellerin"
  git config --global user.email yomguy@parisson.com
      
Next steps:
  mkdir Telemeta
  cd Telemeta
  git init
  touch README
  git add README
  git commit -m 'first commit'
  git remote add origin git@github.com:yomguy/Telemeta.git
  git push -u origin master
      
Existing Git Repo?
  cd existing_git_repo
  git remote add origin git@github.com:yomguy/Telemeta.git
  git push -u origin master

delete github branch:

   git push github :crem


GIT TRAC
========
git clone --bare http://vcs.parisson.com/git/telemeta.git
sudo trac-admin /var/trac/telemeta resync
git remote add origin http://vcs.parisson.com/git/telemeta.git
git fetch --all   

SWAP (clean)
================
sudo swapoff -a && sudo swapon -a


JACK
=====

Jackd, performances and harddisks

2010.11.30
So you have your sample loading working in a separate thread to your realtime audio code and the interface i/o communication is also tucked away in it’s own thread. You have a lock free mechanism for communicating between all threads and still, sometimes – when loading data from disk jackd chucks your program off for blocking – usually during a live performance, and you have to fumble around restarting the audio server. What’s going on?

Well, it turns out that when your hard drive goes to sleep, the spin up resulting from a disk access request (such as mid-performance sample loading) can cause the kernel to block, which causes jackd to panic and either stop entirely or detach your client. This is even with jackd running with the –nozombies switch, so it must be the watchdog thread at work.

The solution is simply to prevent your drive spinning down when you are performing, by adding “hdparm -S 0 /dev/yourharddisk” to your live audio startup script. Thanks to ClaudiusMaximus for helping me fix this at Piksel – it’s been bothering me for ages.

Categories : howto   slub

URLLIB
========
import urllib.request
url='http://www.c64.com/games/download.php?id=1495'
f=urllib.request.urlopen(url)
filename=f.info().get_filename()
urllib.request.urlretrieve(url, filename)

git-svn
======

git-svn can be used to import as well. Note that there may be issues if you have branches or tags (they won’t be imported over). If you only have a trunk, like many svn repositories, this method should work for you without issue.
First, be sure to create your repository on GitHub
$ git svn clone -s SVN_REPO_URL LOCAL_DIR
$ cd LOCAL_DIR
$ git remote add origin git@github.com:GITHUB_USERNAME/REPO_NAME.git
$ git push origin master
Note that the -s switch implies that your svn repo is set up with the standard branches/tags/trunk structure.
git-svn adds a note to every commit message it copies over from svn. To get rid of that note, add --no-metadatato the command.
You can pull in later commits by running git-svn rebase from within your repo. If you ever lose your local copy, just run the import again with the same settings and you’ll get another working directory with all the necessary git-svn settings saved.
Author mapping
When migrating a Subversion repository to Git, you can map the Subversion users to Git users. You have to create an authors file which contains the mappings:
tekkub = Tekkub <tekkub@github.com>
The format is svnuser = gituser_name <gituser_email>. To automatically generate an authors file, check outthis guide.
Once your authors file is complete, clone the subversion repository with the authors file:
$ git svn --authors-file=path/to/authors_file clone SVN_REPO_URL LOCAL_DIR


TRAC
====

for i in `seq 13 52`; do sudo trac-admin /var/trac/CNAQ ticket remove $i; done


BZR
===
yomguyparisson
Je8gN5km9nY7

= nested tree =
bzr split telemeta/htdocs/timeside
cd telemeta/htdocs/timeside
bzr bind https://timeside.googlecode.com/svn/trunk/timeside/ui
bzr checkout https://timeside.googlecode.com/svn/trunk/timeside/ui
bzr up

bzr export --format=tgz ../telemeta-crem-0.8.3.tag.gz

bzr push --remember svn+ssh://parisson.com/var/svn/deefuzzer/trunk



PO to MO
=======
api gettext
msgfmt fichier.po -o fichier.mo

XFS
====
xfs_check /dev/sda1
xfs_repair -L /dev/sda1

XFS: Filesystem dm-9 has duplicate UUID - can't mount
mount -o nouuid /dev/sdc9 /mnt/misc/
xfs_admin -U generate /dev/sdc9


Keyboard
======
The Debian way is:
dpkg-reconfigure keyboard-configuration
dpkg-reconfigure console-data

To make the change visible in X (else reboot):
/etc/init.d/hal restart


GPG
===
gpg -ae -r pellerin@parisson.com files.tar.gz


GSTREAMER
========

taginject
videomixer
videoflip

gst-launch autovideosrc ! videoscale ! video/x-raw-yuv,width=320  ! videomixer name=mix sink_1::xpos=20 sink_1::ypos=20 sink_1::alpha=0.5 ! ffmpegcolorspace ! xvimagesink videotestsrc ! video/x-raw-yuv, framerate=\(fraction\)25/1, width=800, height=600 ! mix.

gst-launch v4l2src ! videoscale ! video/x-raw-yuv, width=320 ! videomixer name=mix sink_1::xpos=20 sink_1::ypos=20 sink_1::alpha=0.5 ! queue !  theoraenc quality=30 ! oggmux name=muxout ! shout2send mount=/telecaster_live_video.ogg port=8000 password=source2parisson ip=127.0.0.1 videotestsrc ! video/x-raw-yuv, framerate=\(fraction\)25/1, width=480, height=320 ! mix.

gst-launch v4l2src ! videoscale ! video/x-raw-yuv, width=320 ! videomixer name=mix sink_1::xpos=20 sink_1::ypos=20 sink_1::alpha=0.5 ! queue !  theoraenc quality=30 ! oggmux name=muxout ! shout2send mount=/telecaster_live_video.ogg port=8000 password=source2parisson ip=127.0.0.1 ximagesrc ! video/x-raw-yuv ! mix.


gst-launch souphttpsrc location=http://192.168.0.12:8080/videofeed ! jpegparse ! jpegdec ! xvimagesink sync=false

gst-launch -v filesrc location=canon.avi ! decodebin name=d  ffmux_flv name=mux ! filesink location=output.flv d. ! queue ! videoscale !  video/x-raw-yuv,width=320,height=256 ! ffenc_flv ! mux.

gst-launch v4l2src ! queue ! videorate ! video/x-raw-yuv,framerate=25/1 ! videoscale !  video/x-raw-yuv,width=320,height=256 ! ffenc_flv ! mux. ffmux_flv name=mux ! filesink location=output.flv

gst-launch tcpclientsrc host=192.168.0.14 port=9000 ! queue ! matroskademux name=demux ! queue ! vp8dec ! ffmpegcolorspace ! ximagesink demux. ! queue ! vorbisdec ! audioconvert ! alsasink


DISTUTILS (PYPI)
============
sudo python setup.py register
sudo python setup.py sdist upload

RAID
====

cat /proc/mdstat
sudo mdadm --create /dev/md5 --level=1 --raid-devices=2 /dev/sda5 /dev/sdb5
sudo mdadm --run /dev/md5
sudo mdadm --stop /dev/md5
sudo mdadm --add /dev/md5 /dev/sdb5

SWAP
=====
sudo mkswap /dev/sda5
sudo mkswap /dev/sdb5

/etc/fstab::
 /dev/sda5       swap    swap   defaults,pri=1           0       0
 /dev/sdb5       swap    swap   defaults,pri=1           0       0

SM2
====
<script>
   soundManager.onready(function(){
   if (soundManager.supported()) {
   // inlineplayer should exist now
    soundPlayer.autoPlay = false;
    soundPlayer.init();
    soundPlayer.togglePause();return false
}
});
</script>


IRC
=====


/msg nickserv register password* e-mail

/msg nickserv identify password

RESCUECD
=========
/etc/init.d/autofs stop
mount -o loop,exec /path/to/systemrescuecd-x86-x.y.z.iso /tmp/cdrom
cd /tmp/cdrom
bash ./usb_inst.sh

boot..
enter
fr
passwd

ARDOUR
======

!!! WARNING !!! - Your system seems to use frequency scaling.
This can have a serious impact on audio latency. You have two choices:
(1) turn it off, e.g. by chosing the 'performance' governor.
(2) Use the HPET clocksource by passing "-c h" to JACK
(this second option only works on relatively recent computers)

REPREPRO
=========

cd /var/www/debian/
reprepro -vb . includedeb stable /home/momo/src/linux-image-3.2.0-rc2-yomguy-rt3_3.2.0-rc2-yomguy-rt3-10.00.Custom_amd64.deb

FAST TRACK PRO
=============

# IMPORTANT: DO NOT COPY CONTENTS OF THIS FILE TO TEXT EDITOR IF VIEWING FROM WEB BROWSER, JUST SAVE THE FILE TO YOUR COMPUTER!!!
# OR VIEW THIS FILE IN UNICODE (UTF-8) MODE IF YOU REALLY WANT TO COPY AND PASTE
# OTHERWISE YOU WILL GET FORMATTING ERRORS AND THE FILE WILL NOT WORK
#
# The first configuration line will put the FastTrack Pro at device number 5 with 24bit mode, max. 48kHz sampling mode, 2 inputs and 4 outputs.
#
# The second configuration line will run the FastTrack pro also in 24 bit mode but with sampling rate above 48KHz (Only Playback mode works above this rates).
# Probably good only for mastering at high resolution.
#
# Only uncomment one line (remove # at start of line) depending how you are going to use your FastTrack Pro
# and remember to reboot your system for changes to take effect. Although the default setting should be good for recording and playback at the same time.
#
# Instead of rebooting you can also try unloading and reloading the snd-usb-audio module by doing the following in a terminal:
#
#       MAKE SURE TO POWER OFF THE FAST TRACK PRO AND OTHER USB AUDIO DEVICES BEFORE RUNNING THE FOLLOWING COMMANDS
#       OR YOU WILL GET AN ERROR MESSAGE SAYING THAT THE SPECIFIC MODULE IS IN USE
#
#       sudo modprobe -r snd-usb-audio
#       sudo modprobe snd-usb-audio
#
# If that doesn't work then just reboot to play it safe
#
# According to the patch, the possible values for the device_setup parameter are the sum of the following numbers:
#
#    * 0×01 : use the device_setup parameter, always needed
#    * 0×02 : enable digital output (channels 3,4)
#    * 0×04 : use 48kHz-96kHz sampling rate, 8-48 kHz if not used
#    * 0×08 : 24bit sampling rate
#    * 0×10 : enable digital input (channels 3,4)
#
#===========================================================================================================================================
#
# CONFIGURATION LINES:

options snd-usb-audio index=2,3 vid=0x46d,0x763 pid=0x81d,0x2012 device_setup=0x00,0x08 enable=1
#options        snd_usb_audio   vid=0x763 pid=0x2012 device_setup=0x5 index=5 enable=1


PYTHON PACKAGE INDEX
==================

sudo python setup.py register

platform independant:
sudo python setup.py sdist upload

platform dependant:
sudo python setup.py bdist upload



ARDOUR
=======

!!! WARNING !!! - Your system seems to use frequency scaling.
This can have a serious impact on audio latency. You have two choices:
(1) turn it off, e.g. by chosing the 'performance' governor.
(2) Use the HPET clocksource by passing "-c h" to JACK
(this second option only works on relatively recent computers)


BASH
======
Clear and Disable Bash History

Need to clear your Bash history?
Use the Bash builtin history command:
history -c
To stop the writing of your Bash history to a file when you log out:
unset HISTFILE



FUSER
====

fuser /dev/snd/pcmC0D0p


curl - Identify remote web server
Type the command as follows:
$ curl -I http://www.remote-server.com/
$ curl -I http://vivekgite.com/
Output:
HTTP/1.1 200 OK
Content-type: text/html
Content-Length: 0
Date: Mon, 28 Jan 2008 08:53:54 GMT
Server: lighttpd



GOURCE
=======

gource -1280x720 -o - | ffmpeg -y -r 60 -f image2pipe -vcodec ppm -i - -vcodec libvpx -b 10000K gource.webm
gource -1280x720 -o - | ffmpeg -y -r 30 -threads 4 -f image2pipe -vcodec ppm -i - -vcodec libvpx ~/tmp/telemeta_gource.webm
gource  -1280x720 -s 0.15 -p 0.5 -o - | ffmpeg -y -r 30 -threads 4 -f image2pipe -vcodec ppm -i - -vcodec libvpx ~/tmp/telemeta_gource.webm


VBOX
====

Kernel driver not installed (rc=-1908)

The VirtualBox Linux kernel driver (vboxdrv) is either not loaded or there is a permission problem with /dev/vboxdrv. Please reinstall the kernel module by executing

'/etc/init.d/vboxdrv setup'

as root. If it is available in your distribution, you should install the DKMS package first. This package keeps track of Linux kernel changes and recompiles the vboxdrv kernel module if necessary.


