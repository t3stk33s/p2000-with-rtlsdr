# pocsag / p2000 (dutch pager system) / semafoon berichten -with-rtlsdr
p2000 berichten decoderen met linux en een rtl_sdr stick,

wat heb je nodig
1. een rtlsdr stick bijvoorbeeld : https://www.ebay.ie/itm/203134008519?hash=item2f4bbafcc7:g:RIwAAOSwL1pfMVeS&amdata=enc%3AAQAHAAAA4Np4NTWb2s%2F%2BL%2BVg8OI3Yyus3XTyqGWQIYkffoZ0jXj%2FIrm%2F%2B%2Fogn5UieymknpX3lgKVXWCsbjEbLBwnIeOX%2BbnRPEa6ayOCGXKPli9bkg3cg81ze1whL58DorxwiYLr0z07lQWmPq%2FyOLzzgrD6pWCHOON%2BaS2JZJJYz6neLRKFy3UpZo4OqNJgzlsL2e7pO7EeowwDQuuPY8kZiKi%2Fzh3L1wcojClvaizwcxc0%2Fw5ySVxqnvqj4Ibh4KDsMvCwPeV2Xu8eK9%2BtQ2MyUhH5vgGCLjA9YyS%2BCQcBfYd6Bh5D%7Ctkp%3ABk9SR67OlaTkYQ
2. een pc / raspberry pi met linux ( ik gebruik zelf Kali )
3. volg onderstaande stappen
4. soms gebeurt het dat je een foutmelding krijg, haal dan even de usbstick uit je computer

https://salsa.debian.org/debian-hamradio-team/multimon-ng
mkdir build
cd build
cmake ..
make
sudo make install

test je rtlstick met rtl_fm, indien dit goed werkt copieer en plak onderstaande regel
voor berichten van p2000 eventueel meet een scope om het signaal te zien plaats dan -a SCOPE in de regel ertussen

rtl_fm -o 4 -A lut  -s 22050  -f 169.650M - | multimon-ng -t raw  -a POCSAG512 -a POCSAG1200 -a POCSAG2400 -a FSK9600 -a FLEX -f alpha /dev/stdin 

voor andere semafoon berichten te ontvangen verander dan de frequentie naar 172.450 dus
rtl_fm -o 4 -A lut  -s 22050  -f 172.450M - | multimon-ng -t raw  -a POCSAG512 -a POCSAG1200 -a POCSAG2400 -a FSK9600 -a FLEX -f alpha /dev/stdin

rtl_fm -o 4 -A lut  -s 22050  -f <change for your frequntie> - | multimon-ng -t raw  -a POCSAG512 -a POCSAG1200 -a POCSAG2400 -a FSK9600 -a FLEX -f alpha /dev/stdin

multimon-ng is the successor of multimon. It decodes the following digital transmission modes:

POCSAG512 POCSAG1200 POCSAG2400
FLEX
EAS
UFSK1200 CLIPFSK AFSK1200 AFSK2400 AFSK2400_2 AFSK2400_3
HAPN4800
FSK9600
DTMF
ZVEI1 ZVEI2 ZVEI3 DZVEI PZVEI
EEA EIA CCIR
MORSE CW
X10
