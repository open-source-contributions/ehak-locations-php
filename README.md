[![Actions Status](https://github.com/koren-software/ehak-locations-php/workflows/build/badge.svg)](https://github.com/koren-software/ehak-locations-php/actions)
[![Coverage Status](https://coveralls.io/repos/koren-software/ehak-locations-php/badge.svg?branch=master&service=github)](https://coveralls.io/github/koren-software/ehak-locations-php?branch=master)
[![Latest Stable Version](https://poser.pugx.org/koren-software/ehak-locations/v/stable)](https://packagist.org/packages/koren-software/ehak-locations)
[![Total Downloads](https://poser.pugx.org/koren-software/ehak-locations/downloads)](https://packagist.org/packages/koren-software/ehak-locations)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

# EHAK Locations

> PHP Library to convert location into EHAK classification code and vice-versa

# Install

```shell
composer require koren-software/ehak-locations-php
```

## Usage

```php
$ehak = new \Koren\EHAK\EHAK(); // init EHAK instance on latest data

// Get EHAK code from location
$countyCode = $ehak->getCode(EHAK::COUNTIES, 'EST', 'Harju maakond'); // 0037

$cityCode = $ehak->getCode(EHAK::CITIES, $countyCode, 'Tallinn'); // 0784
$ehak->getCode(EHAK::CITY_DISTRICTS, $cityCode, 'Haabersti linnaosa'); // 0176

$parishCode = $ehak->getCode(EHAK::PARISHES, $countyCode, 'Anija vald'); // 0141
$ehak->getCode(EHAK::VILLAGES, $parishCode, 'Aegviidu alev'); // 1088

// Get EHAK location from code
$ehak->getLocation(EHAK::COUNTIES, 'EST', '0037'); // Harju maakond

$ehak->getLocation(EHAK::CITIES, '0037', '0784'); // Tallinn
$ehak->getLocation(EHAK::CITY_DISTRICTS, '0784', '0176'); // Haabersti linnaosa

$ehak->getLocation(EHAK::PARISHES, '0037', '0141'); // Anija vald
$ehak->getLocation(EHAK::VILLAGES, '0141', '1088'); // Aegviidu alev
```

## Development

### Update / download data

`src/data` directory holds different versions of EHAK data. To save new version or update old, run:

```shell
bin/update.php --url "EHAK URL HERE"
```

#### Options

- `--output="FILENAME"` / `-o FILENAME` - set different output destination
- `--debug` / `-d` - enable debug