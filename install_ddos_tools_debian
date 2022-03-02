#!/bin/bash
# Author: Byba
YELLOW='\033[1;33m'
NC='\033[0m'
GREEN='\033[0;32m'
RED='\033[0;31m'

if [[ $EUID -ne 0 ]]; then
   echo -e "${RED}This script must be run as root${NC}" 
   exit 1
fi

YELLOW='\033[1;33m'
NC='\033[0m'
GREEN='\033[0;32m'

function docker_install () {
    echo -e "${YELLOW}Docker Installation...${NC}"
    apt-get update
    apt-get install -y docker.io
    systemctl enable docker --now
    systemctl unmask docker.service
    systemctl unmask docker.socket
    systemctl start docker.service
}

function loic_install () {
    echo -e "${YELLOW}Wget Installation...${NC}"
    apt-get install -y wget
    echo -e "${YELLOW}Git Installation...${NC}"
    apt-get install -y git-core
    echo -e "${YELLOW}Mono installation...${NC}"
    apt-get update
    apt-get install -y apt-transport-https dirmngr gnupg ca-certificates
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
    echo "deb https://download.mono-project.com/repo/debian stable-buster main" | tee /etc/apt/sources.list.d/mono-official-stable.list
    apt-get update
    apt-get install -y mono-devel mono-complete ca-certificates-mono gnome-themes-standard
    echo -e "${YELLOW}Loic Installation...${NC}"
    wget https://github.com/nicolargo/loicinstaller/blob/master/loic.sh
    chmod +x loic.sh
    ./loic.sh install
    ./loic.sh update
    echo -e "${GREEN}Write \"./loic.sh run\", to start LOIC${NC}"
}

function dripper_install () {
    apt-get update
    echo -e "${YELLOW}Git Installation...${NC}" 
    apt-get install -y git
    echo -e "${YELLOW}Python Installation...${NC}"
    apt-get install -y python3 
    echo -e "${YELLOW}DRipper Installation...${NC}"
    git clone https://github.com/palahsu/DDoS-Ripper.git
    cd DDoS-Ripper
    ls
    echo -e "${GREEN}Dripper is installed"
}

function bombardier_install () {
    docker_install
    echo -e "${YELLOW}Bombardier Installation...${NC}"
    docker pull alpine/bombardier
    echo -e "${GREEN}Bombardier is installed"
}

function ddos-ripper_install () {
    docker_install
    echo -e "${YELLOW}ddos-ripper Installation...${NC}"
    docker pull nitupkcuf/ddos-ripper
    echo -e "${GREEN}ddos-ripper is installed"
}
echo "Choose DDoS program(1 - LOIC, 2 - DRipper, 3 - Bombardier, 4 - ddos-ripper, 5 - all"
read DPROGRAM
case "$DPROGRAM" in
    "1") # LOIC
        loic_install
        ;;
    "2") # DRipper
        dripper_install
        ;;
    "3") # Bombardier
        bombardier_install
        ;;
    "4") # ddos-ripper
        ddos-ripper_install
        ;;
    "5") # all
        loic_install
        dripper_install
        bombardier_install
        ddos-ripper_install
        ;;
esac        

