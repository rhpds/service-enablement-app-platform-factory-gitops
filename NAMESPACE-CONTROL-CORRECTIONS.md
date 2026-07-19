# Namespace Control Corrections

This document tracks corrections to PR #19 (Control namespaces).

## Changes Required After PR #19 Merges

### 1. gitops-operator - Set create: false

**File**: `etx-infra-app/migrated-source/workloads/gitops-operator/values.yaml`

**Current (from PR #19)**:
```yaml
namespace:
  create: true  # INCORRECT
  name: openshift-gitops
```

**Corrected**:
```yaml
namespace:
  create: false  # openshift-gitops created by operator installation
  name: openshift-gitops
```

**Reason**: The openshift-gitops namespace is automatically created when the OpenShift GitOps Operator is installed cluster-wide. We should not attempt to create it.

---

### 2. vault-secrets-operator - Set create: false

**File**: `etx-infra-app/migrated-source/workloads/vault-secrets-operator/values.yaml`

**Current (from PR #19)**:
```yaml
namespace:
  create: true  # INCORRECT
  name: openshift-operators
```

**Corrected**:
```yaml
namespace:
  create: false  # openshift-operators is built-in OpenShift namespace
  name: openshift-operators
```

**Reason**: The openshift-operators namespace is a built-in OpenShift namespace that always exists. We should not attempt to create it.

---

## Implementation

These corrections will be applied in a follow-up PR after PR #19 merges.

**PR to create**: Fix namespace control defaults for pre-existing namespaces

**Changes**:
- gitops-operator: namespace.create = false
- vault-secrets-operator: namespace.create = false

**Impact**: Prevents unnecessary namespace creation attempts for namespaces that always pre-exist.
