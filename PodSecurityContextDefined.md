<!-- This file is automatically generated by `cv doc`. Do not edit directly. -->

In order to be declarative about their security posture, Pods must define every parameter available in its `securityContext` and each container's `securityContext`. For Pods, this includes `hostNetwork`, `hostPID`, and `hostIPC`. For each container, this includes `privileged`, `readOnlyRootFilesystem`, `allowPrivilegeEscalation`, and at least one element in `capabilities.add` or `capabilities.drop`. The `runAsNonRoot` and `runAsUser` parameters may be defined on each container individually or on the Pod to apply it to all containers. If either is not defined on a container, then it must be defined on the Pod. When linting in the context of an OpenShift cluster, `runAsUser` is not required. Some parameters have specific requirements regarding the acceptable values, but it is most important that each is defined in order to be declarative about the product's security posture.


### Related Links
* [Pod Security Guidance](https://playbook.cloudpaklab.ibm.com/pod-security-guidance#linter-rule)

### Linter Rule
**PodSecurityContextDefined** - The securityContext under each Pod must be fully declared in order to clearly communicate the workload's security posture.

#### Severity
ERROR


#### Passing Examples

**Example: All keys defined**

_pod.yaml (rendered from test default)_:

    kind: Pod
    spec:
      containers:
      - securityContext:
          allowPrivilegeEscalation: false
          capabilities:
            drop:
            - ALL
          privileged: false
          readOnlyRootFilesystem: true
          runAsNonRoot: true
          runAsUser: 1001
      hostIPC: false
      hostNetwork: false
      hostPID: false
      securityContext:
        runAsNonRoot: true
        runAsUser: 1001
    

<hr>


#### Failing Examples

**Example: Missing hostNetwork**

_pod.yaml (rendered from test default)_:

    kind: Pod
    spec:
      containers:
      - securityContext:
          allowPrivilegeEscalation: false
          capabilities:
            drop:
            - ALL
          privileged: false
          readOnlyRootFilesystem: true
          runAsNonRoot: true
          runAsUser: 1001
      hostIPC: false
      hostPID: false
      securityContext:
        runAsNonRoot: true
        runAsUser: 1001
    



Messages:
* `[ERROR] pod.yaml: keys for pod security context not defined: spec.hostNetwork (PodSecurityContextDefined)`
<hr>

**Example: Missing privileged on initContainer**

_pod.yaml (rendered from test default)_:

    kind: Pod
    spec:
      hostIPC: false
      hostNetwork: false
      hostPID: false
      initContainers:
      - securityContext:
          allowPrivilegeEscalation: false
          capabilities:
            drop:
            - ALL
          readOnlyRootFilesystem: true
          runAsNonRoot: true
          runAsUser: 1001
      securityContext:
        runAsNonRoot: true
        runAsUser: 1001
    



Messages:
* `[ERROR] pod.yaml: keys for pod security context not defined: spec.initContainers[0].securityContext.privileged (PodSecurityContextDefined)`
<hr>

**Example: Missing runAsUser**

_pod.yaml (rendered from test default)_:

    kind: Pod
    spec:
      containers:
      - securityContext:
          allowPrivilegeEscalation: false
          capabilities:
            drop:
            - ALL
          privileged: false
          readOnlyRootFilesystem: true
          runAsNonRoot: true
      hostIPC: false
      hostNetwork: false
      hostPID: false
      securityContext:
        runAsNonRoot: true
    



Messages:
* `[ERROR] pod.yaml: keys for pod security context not defined: spec.securityContext.runAsUser OR spec.containers[0].securityContext.runAsUser (PodSecurityContextDefined)`
<hr>

#### Keywords
* security