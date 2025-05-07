# Set Custom Expires by Type on OpenLiteSpeed (OLS) | GridPane

# Set Custom Expires by Type on OpenLiteSpeed (OLS)

 

6 min read 

## Introduction

On your OpenLiteSpeed servers, there are 2 files that you can use to override expires by type at the server level or on a per-site basis:

The server-level file is pre-populated with the defaults. The site-level file doesn’t exist by default.

### Default Time

The default time is 1 year (31535990). You can change this to any time you’d prefer.

Below are the steps to get started.

 

## Step 1. SSH into Your Server

Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Step 2. Get Your MIME Type

The following command will show a list of acceptable MIME types directly on the server:

```
gpols get mime
```

For quick reference, here’s the list:

 

```
default = application/octet-stream
3gp     = video/3gpp
3g2     = video/3gpp2
ai, eps   = application/postscript
aif, aifc, aiff = audio/x-aiff
asc     = application/pgp-keys
asf     = video/asf
asx     = video/x-ms-asf
au      = audio/basic
avi     = video/x-msvideo
avif    = image/avif
bcpio   = application/x-bcpio
bmp     = image/bmp
bin     = application/octet-stream
bz, bz2 = application/x-bzip
cdf     = application/x-netcdf
class   = application/java-vm
cpio    = application/x-cpio
cpt     = application/mac-compactpro
crt     = application/x-x509-ca-cert
csh     = application/x-csh
css     = text/css
dcr,dir, dxr = application/x-director
dms     = application/octet-stream
doc     = application/msword
dtd     = application/xml-dtd
dvi     = application/x-dvi
eot     = application/vnd.ms-fontobject
etx     = text/x-setext
exe     = application/x-executable
ez      = application/andrew-inset
flv     = video/x-flv
gif     = image/gif
gtar    = application/x-gtar
gz, gzip  = application/gzip
hdf     = application/x-hdf
hqx     = application/mac-binhex40
htc     = text/x-component
html, htm    = text/html
ice     = x-conference/x-cooltalk
ico     = image/x-icon
ief     = image/ief
iges, igs    = model/iges
iso     = application/x-cd-image
java    = text/plain
jar     = application/java-archive
jnlp    = application/x-java-jnlp-file
jpeg, jpe, jpg    = image/jpeg
js      = application/x-javascript
js2     = application/javascript
js3     = text/javascript
json    = application/json
jsp     = text/plain
kar     = audio/midi
latex   = application/x-latex
lha, lzh = application/octet-stream
man     = application/x-troff-man
mdb     = application/vnd.ms-access
me      = application/x-troff-me
mesh    = model/mesh
mid, midi  = audio/midi
mif     = application/vnd.mif
movie   = video/x-sgi-movie
mov     = video/quicktime
mp2, mp3, mpga  = audio/mpeg
mpeg, mpe, mpg  = video/mpeg
mp4     = video/mp4
mpp     = application/vnd.ms-project
ms      = application/x-troff-ms
msh     = model/mesh
nc      = application/x-netcdf
oda     = application/oda
odb     = application/vnd.oasis.opendocument.database
odc     = application/vnd.oasis.opendocument.chart
odf     = application/vnd.oasis.opendocument.formula
odg     = application/vnd.oasis.opendocument.graphics
odi     = application/vnd.oasis.opendocument.image
odp     = application/vnd.oasis.opendocument.presentation
ods     = application/vnd.oasis.opendocument.spreadsheet
odt     = application/vnd.oasis.opendocument.text
ogg     = audio/ogg
otf     = application/x-font-woff
pbm     = image/x-portable-bitmap
pdb     = chemical/x-pdb
pdf     = application/pdf
pem     = application/x-pem-file
pgm     = image/x-portable-graymap
pgn     = application/x-chess-pgn
pls     = audio/x-scpls
png     = image/png
pnm     = image/x-portable-anymap
ppm     = image/x-portable-pixmap
ppt     = application/vnd.ms-powerpoint
ps      = application/postscript
qt,qtvr = video/quicktime
ra      = audio/x-realaudio
ram, rm = audio/x-pn-realaudio
rar     = application/x-rar-compressed
ras     = image/x-cmu-raster
rgb     = image/x-rgb
roff, t, tr    = application/x-troff
rpm     = application/x-redhat-package-manager
rss     = application/rss+xml
rsd     = application/rsd+xml
rtf     = application/rtf
rtx     = text/richtext
ser     = application/java-serialized-object
sgml, sgm    = text/sgml
sh      = application/x-sh
shar    = application/x-shar
shtml   = application/x-httpd-shtml
silo    = model/mesh
sit     = application/x-stuffit
skd, skm, skp, skt     = application/x-koan
smi,smil     = application/smil
snd     = audio/basic
spl     = application/x-futuresplash
sql     = text/x-sql
src     = application/x-wais-source
sv4cpio = application/x-sv4cpio
sv4crc  = application/x-sv4crc
svg, svgz = image/svg+xml
swf     = application/x-shockwave-flash
tar     = application/x-tar
tcl     = application/x-tcl
tex     = application/x-tex
texi, texinfo    = application/x-texinfo
tgz     = application/x-gtar
tiff, tif    = image/tiff
tsv     = text/tab-separated-values
ttf, ttc = application/x-font-ttf
txt     = text/plain
ustar   = application/x-ustar
vcd     = application/x-cdlink
vrml    = model/vrml
vxml    = application/voicexml+xml
wav     = audio/vnd.wave
wax     = audio/x-ms-wax
wbmp    = image/vnd.wap.wbmp
webm    = video/webm
webp    = image/webp
wma     = audio/x-ms-wma
wml     = text/vnd.wap.wml
wmlc    = application/vnd.wap.wmlc
wmls    = text/vnd.wap.wmlscript
wmlsc   = application/vnd.wap.wmlscriptc
woff    = application/font-woff
woff2   = font/woff2
woff3   = font/woff
woff4   = application/font-woff2
ttf2    = font/ttf
woff_o1 = application/x-font-woff
wtls-ca-certificate = application/vnd.wap.wtls-ca-certificate
wri     = application/vnd.ms-write
wrl     = model/vrml
xbm     = image/x-xbitmap
xhtml, xht   = application/xhtml+xml
xls     = application/vnd.ms-excel
xml, xsd, xsl = application/xml
xml2    = text/xml
xslt    = application/xslt+xml
xpm     = image/x-xpixmap
xwd     = image/x-xwindowdump
xyz     = chemical/x-pdb
xz      = application/x-xz
zip     = application/zip
z       = application/compress
```

## Step 3. Custom ExpiresByType Formatting

Steps 4a and 4b below detail how add your custom ExpiresByType. In both cases, the formatting is the same when editing their respective files.

The above list will give you the beginning you need. For example to target a jpeg/jpe/jpg file, you can use the following to set it to half a year (in seconds):

```
image/jpeg=A15552000
```

Wildcards will also work, for example, to target all image types you could use the following:

```
image/*=A15552000
```

Add one rule per line.

 

 

### Important

The time has to be set in seconds. The default is 31535990 which is the equivalent of approximately 1 year.
You also can't use fractions of a second or milliseconds (1.5 for example would not work).

## Step 4a. Add Your Custom ExpiresByType at the Server Level

To change this at the server level, edit the server config with this command:

```
nano /usr/local/lsws/conf/expires-by-type.conf
```

You’ll see the following:

```
application/font-woff=A31535990application/gzip=A31535990application/msword=A31535990application/rtf=A31535990application/vnd.ms-excel=A31535990application/vnd.ms-fontobject=A31535990application/vnd.ms-powerpoint=A31535990application/x-bzip=A31535990application/x-executable=A31535990application/x-font-ttf=A31535990application/x-font-woff=A31535990application/x-gtar=A31535990application/x-javascript=A31535990application/x-rar-compressed=A31535990application/x-shockwave-flash=A31535990application/x-tar=A31535990application/xml=A31535990application/zip=A31535990audio/midi=A31535990audio/ogg=A31535990audio/vnd.wave=A31535990font/woff2=A31535990image/bmp=A31535990image/gif=A31535990image/jpeg=A31535990image/png=A31535990image/svg+xml=A31535990image/webp=A31535990image/x-icon=A31535990text/css=A31535990text/html=A31535990video/mp4=A31535990video/ogv=A31535990
```

To add additional rules, add each on their own line.

Once you’ve made your edits, save the file with CTRL+O and then Enter, and then exit nano with CTRL+X. Now regenerate server conf and restart OpenLiteSpeed with:

```
gpols httpd
```

 

## Step 4b. Add Your Custom ExpiresByType for an Individual Site

To add custom ExpiresByType for an individual website, run the following command (replacing site.url with your URL):

```
nano /var/www/site.url/ols/expires-by-type.conf
```

Add one rule per line, and once you’ve made your edits, save the file with CTRL+O and then Enter, and then exit nano with CTRL+X.

Now reload the OpenLiteSpeed configuration with (replacing site.url with your sites URL) to set your changes live:

```
gpols site site.url
```

 

## Check Your Work

First, open up your website in an incognito window. Next, right-click and choose “Inspect“, select the “Network” tab, and then reload the page.

Now you can select your filetype from the lefthand column. In the images below you can see the cache-control max-age (which will display the expiry time you’ve just made) and the content type.

Here’s an example of a .png file:

Here’s an example of a CSS file:

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

