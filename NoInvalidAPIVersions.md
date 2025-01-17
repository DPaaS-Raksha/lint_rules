<!-- This file is automatically generated by `cv doc`. Do not edit directly. -->

Known apiVersions match the following regular expression: `^(v1|.*/v1|.*/v1beta2|.*/v1beta1|.*/v2beta1|.*/v2beta2|.*/v1alpha|.*/v1alpha1)$`. Although most alpha apiVersions are not allowed because they are unstable and not meant for production use, the following alpha apiVersions ARE allowed: ["certmanager.k8s.io/v1alpha1"]. Resources that are instances of CustomResourceDefinitions defined in the same workload are not required to follow these requirements.


### Related Links
* [Alpha Features](https://playbook.cloudpaklab.ibm.com/alpha-features/)

### Linter Rule
**NoInvalidAPIVersions** - Only known, stable apiVersions may be used.

#### Severity
ERROR


#### Passing Examples

**Example: APIVersion is not alpha or unknown**

_crd.yaml (rendered from test default)_:

    apiVersion: apiextensions/v1beta1
    

<hr>


#### Failing Examples

**Example: APIVersion is alpha**

_crd.yaml (rendered from test default)_:

    apiVersion: apiextensions/v1alpha1
    



Messages:
* `[ERROR] crd.yaml: alpha API version "apiextensions/v1alpha1" not allowed (NoInvalidAPIVersions)`
<hr>

**Example: APIVersion is unknown**

_crd.yaml (rendered from test default)_:

    apiVersion: apiextensions/v1alpha2
    



Messages:
* `[ERROR] crd.yaml: unknown API version "apiextensions/v1alpha2" not allowed, known versions match ^(v1|.*/v1|.*/v1beta2|.*/v1beta1|.*/v2beta1|.*/v2beta2|.*/v1alpha|.*/v1alpha1)$ (NoInvalidAPIVersions)`
<hr>

#### Keywords
* [Alpha](../standards/Alpha.md)
