# p2000-with-rtlsdr
p2000 berichten decoderen met linux en een rtl_sdr stick

https://salsa.debian.org/debian-hamradio-team/multimon-ng
mkdir build
cd build
cmake ..
make
sudo make install

test je rtlstick met rtl_fm, indien dit goed werkt copieer en plak onderstaande regel
voor berichten van p2000
rtl_fm -o 4 -A lut  -s 22050  -f 169.650M - | multimon-ng -t raw  -a POCSAG512 -a POCSAG1200 -a POCSAG2400 -a FSK9600 -a FLEX -f alpha /dev/stdin 

voor andere semafoon berichten te ontvangen verander dan de frequentie naar 172.450 dus
rtl_fm -o 4 -A lut  -s 22050  -f 172.450M - | multimon-ng -t raw  -a POCSAG512 -a POCSAG1200 -a POCSAG2400 -a FSK9600 -a FLEX -f alpha /dev/stdin

indien ook nog een scope van de signalen wilt zien voeg dan -a SCOPE toe in de regel

rtl_fm -o 4 -A lut  -s 22050  -f 172.450M - | multimon-ng -t raw  -a SCOPE -a POCSAG512 -a POCSAG1200 -a POCSAG2400 -a FSK9600 -a FLEX -f alpha /dev/stdin



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
