## Installation
```shell 
pip install pybungie
```

## Features
* Painless interaction with the Bungie.net API
* Supports most calls and enumeration types, later versions will expand functionality
* OAuth2 implementation*

<sup><sub>*Not suitable for production code</sup></sub>

## Getting Started
In your working directory, after installing pybungie, edit the ini file before getting started. The file should be located here.

External Libraries \
|— site-packages \
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|— pybungie \
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|— config \
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|— pybungie.ini

This is essential to generate a self-sign certificate in order to use OAuth2 required api calls.
## Usage
```python
from pybungie import BungieAPI, MembershipType, VendorHash, Components

my_membership_type = MembershipType.STEAM
bungie_api = BungieAPI(api_key="api_key")
bungie_api.input_xbox_credentials(xbox_live_email="example@example.com", xbox_live_password="password")
bungie_api.start_oauth2(client_id="client_id", client_secret="client_secret")
membership_id = bungie_api.search_destiny_player(membership_type=my_membership_type, display_name="Hayden23")[0]['membershipId']
character_id = bungie_api.get_profile(membership_type=my_membership_type, membership_id=membership_id,
                                     components=Components.Profiles)['profile']['data']['characterIds'][0]
zavala = bungie_api.get_vendor(membership_type=my_membership_type, membership_id=membership_id,
                              character_id=character_id, vendor_hash=VendorHash.ZAVALA.value,
                              components=Components.VendorSales)
bungie_api.close_oauth2()
```