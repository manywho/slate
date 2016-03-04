# Reporting

States can be set to send reporting data to an external endpoint that adheres to our Reporting API interface (a supported implementation is available [on GitHub](https://github.com/manywho/reporting)). This allows you to gain a greater insight into how and when flows are being uses, as well as the values being used inside a state.

<aside class="notice">Reporting only works with <strong>Permanent States</strong></aside>

### Setting your Endpoint

The endpoint for reporting can be set in the Draw Tool, under **Tenant -> Reporting -> URI**. The endpoint must adhere to our Reporting API interface.

### Enabling  

Inside your player, set `manywho["options"]["reportingMode"]` to one of the following:

* **PATH** - report only the information in the State that pertains to the path the user/users took through the Flow, including location information if provided
* **PATH_AND_VALUES** - report both ***PATH*** and ***VALUES*** information
* **VALUES** - report only the Values collected in the State as the user went through the Flow