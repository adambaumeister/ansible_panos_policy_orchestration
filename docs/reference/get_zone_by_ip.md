# get_zone_by_ip.yml

## Purpose
Determines the appropriate destination zone(s) for a given IP address by analyzing routing tables and interface configurations. This tasks file helps auto-calculate zones for new security policies.

## What it does
1. **Gets routing table** - Retrieves routing information (tries legacy then advanced routing)
2. **Extracts virtual routers** - Identifies all virtual routers from routing entries
3. **Performs FIB lookup** - Tests routing for the target IP against each virtual router
4. **Maps interfaces to zones** - Retrieves interface configurations and maps outbound interfaces to zones
5. **Updates destination zones** - Appends discovered zones to the destination_zones list

## Required Variables

| Variable | Description |
|----------|-------------|
| `provider` | PAN-OS connection details (ip_address, username, password) |
| `item.serial` | Target firewall serial number (from loop context) |

## Loop Variables

| Variable | Description |
|----------|-------------|
| `_target_ip` | IP address to find zones for (passed as loop variable) |

## Optional Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `destination_zones` | Existing zones list to append to | `[]` |

## Generated Variables

| Variable | Description |
|----------|-------------|
| `destination_zones` | Updated list including zones for the target IP |

## Dependencies
- Requires PAN-OS collection
- Must be called within a loop context providing `item.serial`
- Requires custom filters:
  - `panos_op_routing_result_to_interfaces`
  - `panos_op_get_zone_from_interface`
- Handles both legacy and advanced routing table formats