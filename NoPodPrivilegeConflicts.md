<!-- This file is automatically generated by `cv doc`. Do not edit directly. -->

When securityContext.privileged=true and securityContext.allowPrivilegeEscalation=false on any container in a Pod, the Pod will fail to start with an error that there is a mismatch between these two values.


### Related Links
* [Pod Security Guidance](https://playbook.cloudpaklab.ibm.com/pod-security-guidance)

### Linter Rule
**NoPodPrivilegeConflicts** - If securityContext.privileged is set to true for a container, then securityContext.allowPrivilegeEscalation must also be true.

#### Severity
ERROR


#### Passing Examples

**Example: Pod with no privilege conflicts**

_pod.yaml (rendered from test default)_:

    spec:
      containers:
      - securityContext:
          allowPrivilegeEscalation: true
          privileged: true
    

<hr>


#### Failing Examples

**Example: A pod containing a pod privilege conflict**

_pod.yaml (rendered from test default)_:

    spec:
      containers:
      - securityContext:
          allowPrivilegeEscalation: false
          privileged: true
    



Messages:
* `[ERROR] pod.yaml: securityContext.privileged=true and securityContext.allowPrivilegeEscalation=false not allowed on container at spec.containers[0] (NoPodPrivilegeConflicts)`
<hr>

#### Keywords
* [PodSecurity](../standards/Security/PodSecurity.md)
