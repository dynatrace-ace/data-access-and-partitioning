## Intro

- Participants will start with easytrade getting deployed, with host group equals to "onPrem_easytrade_staging"

### TO DO
- Configure auto-tag & MZ based on host group, provision via monaco here: https://github.com/dynatrace-ace/data-access-and-partitioning/blob/main/roles/my-use-case/tasks/main.yml. Add config here: https://github.com/dynatrace-ace/data-access-and-partitioning/tree/main/roles/my-use-case/files/monaco
    - auto-tag
        - bu: easytrade
        - app: loginService, brokerService, etc...
        - platform: onPrem
        - environment: staging
    - mz
        - based on bu
- Participants will have their auto-tags & MZ already present in the environment

### Objectives

- Present lab goal: they need to help an existing customer to upgrade to Dynatrace 3rd-Gen
- Present lab resources: tenant & customer's VM with apps