# sirup: simple IP rotation using python

[![github license badge](https://img.shields.io/github/license/ivory-tower-private-power/sirup)](https://github.com/ivory-tower-private-power/sirup)
[![RSD](https://img.shields.io/badge/rsd-sirup-00a3e3.svg)](https://www.research-software.nl/software/sirup) 
[![workflow pypi badge](https://img.shields.io/pypi/v/sirup.svg?colorB=blue)](https://pypi.python.org/project/sirup/)
<!-- [![DOI](https://zenodo.org/badge/DOI/<replace-with-created-DOI>.svg)](https://doi.org/<replace-with-created-DOI>)  -->
<!-- [![workflow cii badge](https://bestpractices.coreinfrastructure.org/projects/<replace-with-created-project-identifier>/badge)](https://bestpractices.coreinfrastructure.org/projects/<replace-with-created-project-identifier>)  -->
[![fair-software badge](https://img.shields.io/badge/fair--software.eu-%E2%97%8F%20%20%E2%97%8F%20%20%E2%97%8F%20%20%E2%97%8F%20%20%E2%97%8B-yellow)](https://fair-software.eu)
[![workflow scq badge](https://sonarcloud.io/api/project_badges/measure?project=ivory-tower-private-power_sirup&metric=alert_status)](https://sonarcloud.io/dashboard?id=ivory-tower-private-power_sirup)
[![workflow scc badge](https://sonarcloud.io/api/project_badges/measure?project=ivory-tower-private-power_sirup&metric=coverage)](https://sonarcloud.io/dashboard?id=ivory-tower-private-power_sirup)
[![Documentation Status](https://readthedocs.org/projects/sirup/badge/?version=latest)](https://sirup.readthedocs.io/en/latest/?badge=latest)
[![build](https://github.com/ivory-tower-private-power/sirup/actions/workflows/build.yml/badge.svg)](https://github.com/ivory-tower-private-power/sirup/actions/workflows/build.yml)
[![cffconvert](https://github.com/ivory-tower-private-power/sirup/actions/workflows/cffconvert.yml/badge.svg)](https://github.com/ivory-tower-private-power/sirup/actions/workflows/cffconvert.yml)
[![sonarcloud](https://github.com/ivory-tower-private-power/sirup/actions/workflows/sonarcloud.yml/badge.svg)](https://github.com/ivory-tower-private-power/sirup/actions/workflows/sonarcloud.yml) 
[![markdown-link-check](https://github.com/ivory-tower-private-power/sirup/actions/workflows/markdown-link-check.yml/badge.svg)](https://github.com/ivory-tower-private-power/sirup/actions/workflows/markdown-link-check.yml)

A wrapper around the openvpn CLI to connect to VPN servers and rotate the IP address in python programs. 



## What is required
- An account with a VPN service that supports openvpn (for instance ProtonVPN or surfshark)
- A linux OS with superuser rights
- `openvpn` for linux. [Installation](https://community.openvpn.net/openvpn/wiki/OpenvpnSoftwareRepos).

The project setup is documented in [project_setup.md](project_setup.md). Feel free to remove this document (and/or the link to this document) if you don't need it.

## How to install

To install sirup from GitHub repository, do:

```console
python -m pip install 'sirup @ git+https://github.com/ivory-tower-private-power/sirup'
```

## How to use sirup

The package has two functionalities: connecting to a VPN server, and rotating the IP address. 

Before using the package, have a look at ["Preventing DNS leaks"](https://github.com/ivory-tower-private-power/sirup/blob/main/docs/dns_leaks.rst) to make sure the VPN service works properly.


**1. Start up**

This step is necessary for both functionalities.

```python
import os 
import getpass
import time 

seed = 123
mypass = "/path/to/credentials.txt" # the user name and password credentials from your user account with the VPN service
config_path = "/path/to/config/files/" # the .opvn configuration files from your VPN service
```

**Functionality 1: Connecting to a single VPN server**

The `sirup.VPNConnector.VPNConnector` class has two methods: `connect` and `disconnect`. They are used as follows.

```python
from sirup.VPNConnector import VPNConnector

config_file = os.path.join(config_path, "name-of-one-config-file.ovpn")
pwd = getpass.getpass()

connector = VPNConnector(auth_file=mypass, config_file=config_file)

connector.connect(pwd=pwd)

time.sleep(10)
connector.disconnect(pwd=pwd)
```

**Functionality 2: Using the IP rotation feature**

The `sirup.IPRotator.IPRotator` class has three methods: `connect()`, `rotate()`, `disconnect()`. They are used as follows.

```python
from sirup.IPRotator import IPRotator

rotator = IPRotator(auth_file=mypass, config_location=config_path, seed=seed) # will ask for the sudo password

rotator.connect()
print(rotator.connector.current_ip)

rotator.rotate()
print(rotator.connector.current_ip)

rotator.disconnect()
```

## Documentation

The documentation of sirup can be found on [Read the Docs](https://sirup-vpn.readthedocs.io/en/latest/).


## Contributing

If you want to contribute to the development of sirup,
have a look at the [contribution guidelines](CONTRIBUTING.md).

## Credits

This package was created with [Cookiecutter](https://github.com/audreyr/cookiecutter) and the [NLeSC/python-template](https://github.com/NLeSC/python-template).
