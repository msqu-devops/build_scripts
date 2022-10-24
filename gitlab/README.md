# Build Scripts > Gitlab

## Container images with Kaniko 

Add to .gitlab-ci.yml

```yaml

include:
  - remote: 'https://raw.githubusercontent.com/dhswt/build-scripts/master/gitlab/ContainerBuildKaniko.yml'

docker-image:
  extends: .BuildImageWithKaniko
  # stage: package

  # overwrite to change defaults for variables below
  # variables:
    # TAG_COMMIT_ENABLE: "true"
    # TAG_COMMIT_PREFIX: "commit-"
    # TAG_REF_SLUG_ENABLE: "true"
    # DOCKERFILE: "$CI_PROJECT_DIR/Dockerfile"
    # CONTEXT_DIR: "$CI_PROJECT_DIR"
    # ADDITIONAL_REGISTRY_DESTINATIONS: ""
    # ADD_GITLAB_REGISTRY_AUTH: "true"

  # add gitlab job dependencies
  # dependencies:
  #  - build

  # only build relevant branches/tags
  # only:
  #   refs:
  #     # - master
  #     - /^env\/.*$/i
  #     - /^v[0-9].*$/i

```

## Helm Charts

Add to .gitlab-ci.yml

```yaml

include:
  - remote: 'https://raw.githubusercontent.com/dhswt/build-scripts/master/gitlab/HelmChart.yml'

helm-lint:
  extends: .HelmChartLint

helm-publish:
  extends: .HelmChartPublish

# overwrite to change default variables below
#  variables:
#    HELM_STABLE_ENDPOINT: "$CI_API_V4_URL/projects/$CI_PROJECT_ID/packages/helm/stable"
#    HELM_DEVEL_ENDPOINT: "$CI_API_V4_URL/projects/$CI_PROJECT_ID/packages/helm/devel"
#    CHART_PATH: "$CI_PROJECT_DIR/chart/"
#    HELM_REPO_NAME: "$CI_PROJECT_NAME"
#    GITLAB_HELM_REPO_AUTH: "true"
#
#    TAG_COMMIT_ENABLE: "true"
#    TAG_COMMIT_BASE_VERSION: "0.0.0"
#    TAG_COMMIT_PREFIX: "commit-"
#
#    TAG_REF_SLUG_ENABLE: "true"
#    TAG_REF_SLUG_BASE_VERSION: "0.0.0"

helm-release:
  extends: .HelmReleaseTag

  # defaults to tags only:
  # only:
  # - tags

```

## Golang

Add to .gitlab-ci.yml

```yaml

include:
  - remote: 'https://raw.githubusercontent.com/dhswt/build-scripts/master/gitlab/GoBuild.yml'

build:
  extends: .GoBuild

# overwrite to change default variables below
#  variables:
#    BINARY_NAME: "$CI_PROJECT_NAME"
#    BINARY_DIR: "$CI_PROJECT_DIR/dist"
#
#    EXTRA_GO_BUILD_ARGS: ""
#    EXTRA_LD_FLAGS: ""
#    LD_FLAGS: "-s -w"
#    USE_UPX: "true"
#
#    GO_VERSION_VARIABLE: "" # package.variable to set to CI_COMMIT_REF_NAME
#    GO_VERSION_INFO_VARIABLE: "" # package.variable to set to additional data about release
#
#    PACKAGE_COMMIT_ENABLE: "true"
#    PACKAGE_COMMIT_PREFIX: "commit-"
#
#    PACKAGE_REF_SLUG_ENABLE: "true"
#
#    RUN_BINARY: "false"
#    RUN_BINARY_WITH_ARGUMENTS: ""

```