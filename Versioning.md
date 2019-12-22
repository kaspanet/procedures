# Kaspa: Versioning Scheme

This document describes the versioning scheme that will be used in Kaspa repositories.

---
#### TL; DR
* *Public Release* versions are composed of three numbers (e.g. **1.0.0**, **2.4.16**)
* *Development branch* is the target version with a "-dev" suffix (e.g. **2.4.16-dev** for 2.4.16)
* *Development Build* is the target version with a "-" and the build number (e.g. **2.4.0-1**, **2.4.0-2**, ..., **2.4.16-325**)
* *Test Release* versions are composed of the target version suffixed by a dash and the readiness level, e.g. **1.2.3-alpha1** for first alpha, **1.2.3-beta3** for third beta, **1.2.3-rc2** for second release candidate.
---

## Version Types
There are three version types:  *Public Release*, *Test Release* and *Development Build*. 

## Public Release Versions
A *Release Version* describes a version that has been formally released.

### Version Structure
Each version is composed of 3 parts - i.e. *x.y.z*, where:
-  **x** (*major*) - a truly new generation of Kaspa.
-  **y** (*minor*) - new features added.
-  **z** (*revision*) - bug fixes and very minor changes

All three parts are zero based.

#### Examples
**3.0.0** is the first public version of a new Kaspa generation.
The first set of bug fixes, if required, will be released as **3.0.1**.
The next set of features will be released as **3.1.0**.

### Release Version Ordering
Given two versions **a.b.c** and **x.y.z**, the first is *earlier than* the latter if **a < x**, or - if they are identical - if **b < y**, or - if those, too, are identical - if **c < z**.

#### Examples
2.3.4 **<** 3.0.0
2.3.4 **<** 2.12.1
2.3.4 **<** 2.3.7

## Development

### Development Branch
Git development branches have the form **x.y.z-dev** where x.y.z is the target *release version*.

#### Examples
Once 1.0.0 is released, two development branches will be created:
**1.0.1-dev** for bug fixes, and
**1.1.0-dev** for adding new features.

### Development Build
Every build (that includes one or more new commits) has the form **x.y.z-w**, where **x.y.z** is the target *release version* and **w** is the *build number*. Build numbers starts at 1, rather than 0.

#### Examples
The first build on 1.3.0-dev will be **1.3.0-1**, then **1.3.0-2** and so on.

## Test Release Versions
Once most of the development towards a release version is done, it should be tested and stabilized. For this purpose, tests and fixes are to be defined on *test versions*, until the final version is approved to be released. 

### Version Maturity
There might be three maturity levels, denoted as follows (their exact definition is beyond the scope of this document):
* **alpha**
* **beta**
* **rc** (release candidate)

### Maturity Round
A version might have a few maturity rounds before it is increased to the next maturity stage.

### Test Version Structure
A *test release version* structure has the form **x.y.z-mr**, where 
* **x.y.z** is the target release version
* **m** is the maturity level (alpha|beta|rc)
* **r** is the round in that maturity level

The first round is round 1.

#### Examples
**1.4.0-alpha2** is the second alpha stage towards releasing 1.4.0
**2.1.7-rc1** is the first release candidate towards 2.1.7
**3.0.0-beta3** is the third beta stage towards 3.0.0

### Test Version Ordering
Given two *test versions* **x.y.z-mr** and **i.j.k-np** (where **x**, **y**, **z**, **r** and **i**, **j**, **k**, **p** are integers, and **m**, **n** are in **{alpha, beta, rc}**) then:
The first is *earlier than* the second if - 
**x.y.z** is earlier than **i.j.k**, 
or if - 
**x.y.z == i.j.k *and* m == n *and* r < p**,
or if -
**x.y.z == i.j.k *and* m < n *and* p > 1**;
it is *earlier than or equal* to the second if -
**x.y.z == i.j.k *and* m < n *and* p == 1**.
For that matter, **alpha** < **beta** < **rc**.

#### For example:
1.2.17-rc1 **<** 1.2.18-alpha1
1.2.17-beta2 **<** 1.2.17-beta3
1.2.17-alpha3 **<** 1.2.17-beta2
1.2.17-beta2 **<=** 1.2.17-rc1

## Special Versions

### Pre-TestNet
Working before TestNet is done linearly on **0.0.z**, as an exception to the above rules.

### TestNet-Only
*TestNet* will be launched as **0.1.0**.
Important new stages will be introduced as **0.2.0**, **0.3.0** etc.
However, during the beginning of that era, revision changes (the **z** part) might include functional changes as well.

### MainNet
*MainNet* will be launched as **1.0.0**.

From that point on, the versioning rules introduced above will take effect.

