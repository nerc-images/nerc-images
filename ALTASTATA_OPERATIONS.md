# AltaStata Image Stream Operations Guide

This document describes all the operations performed to add the new AltaStata Jupyter DataScience image stream to the NERC Images repository.

## Overview

Added a new OpenShift ImageStream for the AltaStata Jupyter DataScience image (`ghcr.io/sergevil/altastata/jupyter-datascience:2025d_latest`) to the NERC Images repository.

## Operations Performed

### 1. Repository Setup and Image Stream Creation

#### Created Directory Structure
```bash
mkdir -p imagestreams/altastata-jupyter-datascience
```

#### Created ImageStream Definition
**File:** `imagestreams/altastata-jupyter-datascience/imagestream.yaml`

```yaml
apiVersion: image.openshift.io/v1
kind: ImageStream
metadata:
  name: altastata-jupyter-datascience
  namespace: redhat-ods-applications
  labels:
    opendatahub.io/notebook-image: "true"
  annotations:
    opendatahub.io/notebook-image-url: >-
      https://github.com/SergeVil/altastata-python-package
    opendatahub.io/notebook-image-name: >-
      Altastata Jupyter DataScience
    opendatahub.io/notebook-image-desc: |-
      An OpenShift AI Image running Jupyter Lab for data science development.
      - Based on the Altastata Jupyter DataScience image.
      - Provides a comprehensive data science environment.
spec:
  lookupPolicy:
    local: true
  tags:
    - name: 2025d_latest
      annotations: null
      from:
        kind: DockerImage
        name: 'ghcr.io/sergevil/altastata/jupyter-datascience:2025d_latest'
      importPolicy:
        scheduled: true
      referencePolicy:
        type: Source
```

#### Created Kustomize Configuration
**File:** `imagestreams/altastata-jupyter-datascience/kustomization.yaml`

```yaml
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
resources:
  - imagestream.yaml
```

### 2. Documentation Updates

#### Updated README.md
Added entry for the new image stream:

```markdown
| [altastata-jupyter-datascience](https://github.com/SergeVil/altastata-python-package) | An OpenShift AI Image running Jupyter Lab for data science development at the AltaStata Fortified Data Lake. |
```

### 3. Git Operations

#### Initial Commit
```bash
git add imagestreams/altastata-jupyter-datascience/ README.md
git commit -m "Add altastata-jupyter-datascience image stream"
```

#### Push to Fork
```bash
git push
```

#### Update Description and Link
```bash
# Updated README.md description and link
git add README.md
git commit -m "Update AltaStata README link and description"
git push
```

### 4. Repository Visibility Management

#### Made AltaStata Repository Public
```bash
gh repo edit SergeVil/altastata-python-package --visibility public --accept-visibility-change-consequences
```

**Repository:** `https://github.com/SergeVil/altastata-python-package`
- ✅ **Public visibility** - Readable by everyone
- ✅ **Private write access** - Only owner can make changes
- ✅ **Forkable** - Anyone can fork for their own use

### 5. Pull Request Creation

#### Setup Upstream Repository
```bash
git remote add upstream https://github.com/nerc-images/nerc-images.git
git fetch upstream
```

#### Create Feature Branch
```bash
git checkout -b add-altastata-jupyter-datascience
git push -u origin add-altastata-jupyter-datascience
```

#### Create Pull Request
```bash
gh repo set-default SergeVil/nerc-images
gh pr create --repo nerc-images/nerc-images --title "Add altastata-jupyter-datascience image stream" --body "This PR adds a new image stream for the AltaStata Jupyter DataScience image.

## Changes
- Added new image stream for ghcr.io/sergevil/altastata/jupyter-datascience:2025d_latest
- Updated README.md with correct link to https://github.com/SergeVil/altastata-python-package
- Added proper OpenDataHub integration metadata

## Files Added
- imagestreams/altastata-jupyter-datascience/imagestream.yaml
- imagestreams/altastata-jupyter-datascience/kustomization.yaml

## Files Modified
- README.md - Updated with new image stream entry"
```

## Final Results

### ✅ Successfully Created
- **Pull Request:** [https://github.com/nerc-images/nerc-images/pull/19](https://github.com/nerc-images/nerc-images/pull/19)
- **Image Stream:** `altastata-jupyter-datascience:2025d_latest`
- **Source Image:** `ghcr.io/sergevil/altastata/jupyter-datascience:2025d_latest`
- **Documentation:** Updated README.md with correct link and description

### 📁 Files Added
- `imagestreams/altastata-jupyter-datascience/imagestream.yaml`
- `imagestreams/altastata-jupyter-datascience/kustomization.yaml`

### 📝 Files Modified
- `README.md` - Added new image stream entry with correct link

## Deployment Information

### OpenShift Integration
- **Namespace:** `redhat-ods-applications`
- **Image Stream Name:** `altastata-jupyter-datascience`
- **Tag:** `2025d_latest`
- **OpenDataHub Integration:** ✅ Enabled with proper metadata

### Access Information
- **Repository:** [https://github.com/SergeVil/altastata-python-package](https://github.com/SergeVil/altastata-python-package)
- **Visibility:** Public (readable by everyone, writable only by owner)
- **Description:** "An OpenShift AI Image running Jupyter Lab for data science development at the AltaStata Fortified Data Lake"

## Next Steps

1. **Review Process:** Wait for maintainers to review the pull request
2. **Deployment:** Once merged, the image stream will be available in the NERC OpenShift cluster
3. **Testing:** Verify the image stream works correctly in the OpenShift environment
4. **Documentation:** Update any additional documentation as needed

## Commands Reference

### Useful Git Commands
```bash
# Check status
git status

# View differences with upstream
git diff upstream/main

# View commit history
git log --oneline -5

# Check remotes
git remote -v
```

### Useful GitHub CLI Commands
```bash
# View PR status
gh pr view

# List PRs
gh pr list

# Check repository visibility
gh repo view --json visibility
```

---

**Created:** January 2025
**Repository:** [https://github.com/SergeVil/nerc-images](https://github.com/SergeVil/nerc-images)
**Pull Request:** [https://github.com/nerc-images/nerc-images/pull/19](https://github.com/nerc-images/nerc-images/pull/19)
