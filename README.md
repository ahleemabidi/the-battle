sudo dpkg --add-architecture i386

wget -qO - https://dl.winehq.org/wine-builds/winehq.key |
sudo apt-key add –

sudo apt-add-repository 'deb https://dl.winehq.org/winebuilds/ubuntu/ eoan main'
sudo apt update
sudo apt install --install-recommends winehq-stable
sudo apt install aptitude
sudo aptitude install winehq-stable ''''''siilya erreur

wine --version
wine-5.0
