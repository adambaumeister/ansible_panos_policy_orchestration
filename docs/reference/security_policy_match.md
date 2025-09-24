# security_policy_match.yml

## Purpose
Executes the PAN-OS `test security-policy-match` command to determine if specific traffic is already permitted by existing security policies. Includes fallback logic for parameter compatibility.

## What it does
1. **Primary test** - Attempts to run security-policy-match with all provided parameters
2. **Fallback test** - If primary test fails, retries with default SSL/HTTPS parameters
3. **Result processing** - Converts the XML response to a boolean result

## Required Variables

| Variable | Description |
|----------|-------------|
| `source_ip` | Source IP address for the test |
| `destination_ip` | Destination IP address for the test |
| `application` | Application name for the test |
| `protocol` | IP protocol number for the test |
| `destination_port` | Destination port for the test |
| `provider` | PAN-OS connection details (ip_address, username, password) |
| `item.serial` | Target firewall serial number (from loop context) |

## Optional Variables

| Variable | Description | Default |
|----------|-------------|---------|
| N/A | All variables are required when called | N/A |

## Generated Variables

| Variable | Description |
|----------|-------------|
| `security_policy_match_result` | Raw XML response from the test command |
| `matches_existing_policy` | Boolean result of policy match test |

## Dependencies
- Requires PAN-OS collection
- Must be called within a loop context providing `item.serial`
- Requires custom filter `panos_op_policy_match_result_to_bool`
- Fallback uses hardcoded values: application=`ssl`, protocol=`6`, destination-port=`443`