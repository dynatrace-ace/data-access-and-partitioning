## Intro

- Participants will start with a K8s cluster with multiple apps running on it (easytrade & hipstershop), with host group equals to "k8s_multi_prod". 

### TO DO
- Configure auto-tag & MZ based on host group, provision via monaco here: https://github.com/dynatrace-ace/data-access-and-partitioning/blob/main/roles/my-use-case/tasks/main.yml. Add config here: https://github.com/dynatrace-ace/data-access-and-partitioning/tree/main/roles/my-use-case/files/monaco
    - auto-tag
        - app: based on namespace
        - component: loginService, brokerService, etc..., based on workload
        - platform: k8s
        - environment: prod
    - mz
        - based on app
- Participants will have their auto-tags & MZ already present in the environment