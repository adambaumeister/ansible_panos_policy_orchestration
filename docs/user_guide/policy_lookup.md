# Testing Security Policies

This automation uses the PAN-OS `test security-policy-match` command for testing the existing of matching security
rules in the security rulebase.

For this to work most accurately, every new rule request should provide:

 * Source IP
 * Destination IP
 * Application (DEFAULT: ssl)
 * Protocol (DEFAULT: 6)
 * Destination-Port (DEFAULT: 443)

The lookup is performed on a **per-firewall basis**, by default, the test command will be run on all connected devices in Panorama.

You can change this behavior by populating the `default_test_policy_serial_number` variable.