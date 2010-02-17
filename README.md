# mabishu-apache-autoindex: An autoindex theme for Apache autoindex module with Mabishu Studio branding 

Index-Style is a set of html, css and image files designed to work together with
the mod_autoindex module to make the default Apache file listings look a little
nicer. The UI design is based almost entirely on the great work done by the guys
at [http://www.reposstyle.com/](Repos-Style), although the code itself is largely
done from scratch (as mod_autoindex doesn’t support XSLT).

## Installation

First, get a copy of the index-style folder – the easiest way is to change to
the document root of the domain you want to style, and check it out from
subversion (in my case the domain will be download.recurser.com ) :

 $ cd /var/www/YOUR.VHOST.LOCAL
 $ git clone http://github.com/frandieguez/mabishu-apache-autoindex.git

This should create an ‘index-style’ folder in your document root. Next, you
need to configure Apache to use the index-style files to style your directory
listings. I use the following config, which you’ll need to adjust to match your
particular setup – the ‘icons’ alias and the ‘mod_autoindex’ section are the 
main areas to pay attention to:

 <VirtualHost *:80>
    ServerName your.vhost.local
    DocumentRoot /var/www/your.vhost.local
    Alias /icons/ /var/www/your.vhost.local/index-style/icons/
 
    <Directory "/var/www/your.vhost.local">
        AllowOverride All
        Order allow,deny
        Allow from all
 
        <IfModule mod_autoindex.c>
            Options Indexes FollowSymLinks
            IndexOptions +FancyIndexing 
            IndexOptions +VersionSort 
            IndexOptions +HTMLTable 
            IndexOptions +FoldersFirst 
            IndexOptions +IconsAreLinks 
            IndexOptions +IgnoreCase 
            IndexOptions +SuppressDescription 
            IndexOptions +SuppressHTMLPreamble 
            IndexOptions +XHTML 
            IndexOptions +IconWidth=16 
            IndexOptions +IconHeight=16 
            IndexOptions +NameWidth=*
            IndexOrderDefault Descending Name
            HeaderName /include/header.html
            ReadmeName /include/footer.html
        </ifModule>
 
    </Directory>
 </VirtualHost>

You’ll need mod_autoindex for any of this to work – it should be installed by 
default with Apache in most linux distributions.

Disclaimer

The formatting relies on a few javascript hacks which may or may not work exactly
as intended if the output of your apache directory listings differs a lot from
what is expected. If the output appears strange, try playing around with the 
javascript formatting in header.html, or drop me a line if you need a hand.
