# Ansible PAN-OS Policy Orchestration

This project is designed to help Firewall administrators manage incoming requests for PAN-OS security policy by
automating as much as the process as possible, in as maintainable a way as possible.

## Non-technical Requirements/Assumptions

The successful implementation of this project assumes some basics about the Firewall operating environment.

 1. When users/customers request network access, they are able to gather and provide basic technical details
    1. Source IP/DestinationIP/Application
 2. You have some mechanism for triggering this automation.
    1. Ansible EDA triggered by ITSM webhook
    2. Github or Gitlab CICD pipeline
    3. Manual or Cron based execution
 3. You are using a typical routed firewall environment (not transparent/switched)

## Other considerations

This automation is based on the idea that all PAN-OS configuration should be obvious to administrators of the devices.

For this reason, we don't use DAG objects, which means changes require commits and the overall process is less efficient
 but is more applicable to brownfield environments.

If that sounds good, proceed to [Configuring Preset Policy](preset_policy.md)

