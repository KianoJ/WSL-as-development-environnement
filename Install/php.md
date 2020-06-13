# Install latest PHP version

## Add the main PPA PHP to download the latest PHP version

```
sudo add-apt-repository ppa:ondrej/php
sudo apt update
```

## Install PHP

```
sudo apt install php -y
```

## Install PHP extension

```
sudo apt install php-[EXTENSTION_NAME] -y
# sudo apt install php-dom -y
```

## Errors fix

### The requested PHP extension dom is missing from your system

```
sudo apt install php-xml -y
```