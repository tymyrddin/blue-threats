# Installation and basic use on Linux

## Package

    sudo apt update -y && sudo apt upgrade -y
    sudo apt install yara

## From source

Use if installing package does not work.

    sudo apt update -y && sudo apt upgrade -y

Install dependencies:

    sudo apt install automake libtool make gcc flex bison libssl-dev libjansson-dev libmagic-dev pkg-config

[Download the latest release](https://github.com/virustotal/yara/releases) (at time of writing is 4.2.3):

    wget https://github.com/VirusTotal/yara/archive/v4.2.3.tar.gz

Extract the `tar.gz`:

    tar -zxvf v4.2.3.tar.gz

Compile and install:

    cd yara-4.2.3
    chmod +x configure
    ./configure
    chmod +x bootstrap.sh
    ./bootstrap.sh
    make
    sudo make install

## Resources

[YARA's documentation](https://yara.readthedocs.io/en/stable/)
