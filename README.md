Cloud-Native CI/CD Pipeline & Microservices Deployment

Project Overview

This repository demonstrates the design and end-to-end implementation of an automated Continuous Integration and Continuous Delivery (CI/CD) workflow. The project leverages GitHub Actions for upstream linting and unit testing, and Tekton / Red Hat OpenShift Pipelines alongside GitOps (Argo CD) for cloud-native containerized delivery.

Architecture & Technology Stack

Runtime & Language: Python (Flask/Gunicorn) / Node.js

Source Code Management: Git & GitHub (Social Coding, feature branching, PR automation)

CI Automation: GitHub Actions (flake8, nosetests / pytest)

Containerization: Buildah / Docker

Pipeline Orchestration: Tekton Pipelines / Red Hat OpenShift Pipelines

Continuous Delivery & GitOps: Argo CD & Kubernetes Custom Resource Definitions (CRDs)

Infrastructure & Storage: Kubernetes PersistentVolumeClaims (skills-network-learner storage class)

Pipeline Workflow Structure

The OpenShift pipeline execution graph consists of six sequential and parallel stages:

[ cleanup ] ──► [ git-clone ] ──► [ flake8 / eslint ] ──► [ nose / jest ] ──► [ buildah ] ──► [ deploy ]


cleanup: Clears previous build artifacts and resets the pipeline workspace on the PVC.

git-clone: Clones the targeted branch and commit from the upstream Git repository.

flake8 / eslint: Executes static code analysis and linting checks.

nose / jest: Runs automated unit and integration tests.

buildah: Builds the application container image and pushes it to the image registry.

deploy (openshift-client): Applies deployment manifests and rolls out updates to the target environment.

Directory Structure

├── .github/
│   └── workflows/
│       └── workflow.yml          # GitHub Actions CI definition (lint & test)
├── .tekton/
│   └── tasks.yml                 # Reusable Tekton Task definitions (cleanup & test)
├── pipeline/
│   ├── pipeline.yaml             # Tekton Pipeline definition linking tasks
│   └── pipelinerun.yaml          # PipelineRun configuration binding workspaces & PVC
├── tests/
│   └── test_routes.py            # Unit and regression test suite
├── app.py                        # Core microservice application
├── requirements.txt              # Application and testing dependencies
└── README.md                     # Project documentation


Verification & Artifacts

GitHub Actions Validation: Recorded in cicd-github-validate.

OpenShift PVC Verification: Saved under oc-pipelines-console-pvc-details.png.

OpenShift Pipeline Graph: Saved under oc-pipelines-oc-final.png.

Application Runtime Logs: Verified in oc-pipeline-application-logs confirming active execution (SERVICERUNNING on port 8000).

License

This project is licensed under the Apache 2.0 License.
