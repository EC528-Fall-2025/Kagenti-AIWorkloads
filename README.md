# Kagenti

## Collaborators

| Name | Role | Email |
|-----------------|-----------------|-----------------|
| Mariusz Sabath        | Mentor       |    |
| Maia Iyer             | Mentor       |    |
| Kelly Abuelsaad       | Mentor       |    |
| Alan Cha              | Mentor       |    |
| Peter Zhao            | Developer    | <pyzhao@bu.edu>     |
| Sienna Chien          | Developer    | <siennac@bu.edu>    |
| Moumit Bhattacharjee  | Developer    | <moumitb@bu.edu>    |
| Derek Xu              | Developer    | <dxu0117@bu.edu>    |
| Ethan Levine          | Developer    | <elevine@bu.edu>    |
| Yena Yu               | Developer    | <yenayu@bu.edu>     |

## Sprint 1

[Presentation Recording](https://drive.google.com/file/d/1rMi2ut0vbHSCFu7aoKyDDVQ0NcfTJIcc/view?usp=sharing)
[Slides](https://docs.google.com/presentation/d/1Q7zPf_1gD-JVEll4ll9txz9Gi8lQ1h20SgNGf9KBg4g/edit?usp=sharing)

## Sprint 2

[Presentation Recording](https://drive.google.com/file/d/1Ws5P1HYi_0Eh39Vp2eBahGrvRop0VHuk/view?usp=sharing)
[Slides](https://docs.google.com/presentation/d/1clWzl1bMfUx0Ej4jhLKs9Yn2LVIGmSNEWRr-4E0mlvs/edit?usp=sharing)

## Sprint 3

[Presentation Recording](https://drive.google.com/file/d/1w0X_5yFam0ebonQKGJX5d5frd674fehy/view?usp=sharing)
[Slides](https://docs.google.com/presentation/d/1wjmABrLBNZYKQrAIwjuvawyGPtIRpFxrgofdjDMLDs4/edit?usp=sharing)

## Sprint 4

[Presentation Recording](https://drive.google.com/file/d/164a02O1zW5yKjKj8oFbZjh6WIIad6dCU/view?usp=sharing)
[Slides](https://docs.google.com/presentation/d/1B4KEPbvV_hVor-Dl8oDULmzbHrXop98_6-BZRtxOpCo/edit?usp=sharing)

## Sprint 5

[Presentation Recording](https://drive.google.com/file/d/1-ZNNhZwhhMXHGZP9U694Rxd8V5kWEFrh/view?usp=sharing)
[Slides](https://docs.google.com/presentation/d/1nRrseSFcb2bR9ZNJ3XFrKV0vlnBXF3tbtLkZq01KKAI/edit?usp=sharing)

## Final Presentation
[Presentation Recording](https://drive.google.com/file/d/1-ZNNhZwhhMXHGZP9U694Rxd8V5kWEFrh/view?usp=sharing)
[Slides](https://docs.google.com/presentation/d/1qY4szIqvHTzyvLFvIEJFfLbOhMBcw80oivYu0As3PRg/edit?usp=sharing)

# Completed Work

We created variety of agent and MCP examples that can be integrated into the Kagenti platform as well as contributions to the various Kagenti repositories.

## Installation and Setup

To install and run the Kagenti platform see [this document](https://github.com/kagenti/kagenti/blob/main/docs/kind-install.md), documentation for specific agents and MCP servers can be found below

## Agents and MCP servers

- Generic Agent (with flight tool and movie tool) - [Demo](https://github.com/kagenti/kagenti/pull/441)
- Shopping MCP - [PR](https://github.com/kagenti/agent-examples/pulls)
- Restaurant Reservation MCP and Agent - [PR](https://github.com/kagenti/agent-examples/pull/102)
- Image Agent and MCP - [Agent PR](https://github.com/kagenti/agent-examples/pull/104) [MCP PR](https://github.com/kagenti/agent-examples/pull/103)

## General Contributions

### Kagenti Dependencies Helm Chart

This contribution seeks to add Helm charts to easily install and manage a deployment of Kagenti. This PR specifically focuses on Kagenti's dependencies as these are components that must be installed first before other components such as the Kagenti Operator or MCP Gateway can be installed. After many issues with Helm charts not being able to support custom namespaces, the process is a little manual with the requirement of installing multiple Helm charts as opposed to a single one. However, it still maintains the configurability and management of Helm charts. These Helm charts are most often used in beefier installation scripts or in CI/CD pipelines.

**PR**: [here](https://github.com/kagenti/kagenti/pull/279).

- Please note that the instructions and expected results on this PR are outdated as further work has been done on the charts.

**Instructions**:

```bash
git clone https://github.com/kagenti/kagenti.git
```

1. Install [operator-sdk](https://sdk.operatorframework.io/docs/installation/)
2. Create a kind cluster with `kind create cluster -n agent-platform`
3. `operator-sdk olm install`
4. `kubectl create namespace istio-system`
5. `helm install -n kagenti-system kagenti-deps ./ -f ./values.yaml --create-namespace   --set openshift=false   --set tags.kubernetes=true   --set components.ingressGateway.enabled=true   --set components.gatewayApi.enabled=true`

You should see deployments in `kagenti-system` and `keycloak`. Previously there were also operators that were added to the `operators` namespace, but currently that is not the case and is most likely due to later code changes by other developers.

### Kagenti Operator Helm Chart

With the creation of a new operator called the kagenti-operator (as opposed to platform-operator), a new Helm chart was needed to install and manage this new operator. This PR adds these charts by emulating some of the existing platform-operator charts and modifying them to work with the new operator components and custom resource definitions (CRDs). Similar to the kagenti dependencies, these are mostly used in beefier installation scripts or in CI/CD pipelines.

**PR**: [here](https://github.com/kagenti/kagenti-operator/pull/108)

**Instructions**:

```bash
git clone https://github.com/kagenti/kagenti-operator.git
```

1. Create kind cluster with `kind create cluster -n agent-platform`

2. Install cert-manager

```bash
helm install   cert-manager oci://quay.io/jetstack/charts/cert-manager   --version v1.19.1   --namespace cert-manager-operator   --create-namespace   --set crds.enabled=true
```

3. Install kube-prometheus-stack

```bash
helm install kagenti-prometheus kube-prometheus-stack --repo=https://prometheus-community.github.io/helm-charts --create-namespace --namespace=monitoring
```

4. Install tekton-cd operator

```bash
kubectl apply -f https://storage.googleapis.com/tekton-releases/operator/latest/release.yaml
```

5. Install [ko](https://ko.build/install/)

6. Build container and install charts

```bash
cd kagenti-operator/kagenti-operator

make ko-local-build

make install-local-chart
```

You should see the controller manager in the `kagenti-system` namespace along with new CRDs (Agent and AgentBuild).

### MCP Gateway Tool Annotations and Observability Stack

This contribution involves adding MCP tool annotations to enhance observability within the MCP Gateway. By incorporating these annotations, we can provide better insights into the interactions between agents and tools, improving monitoring and debugging capabilities. This PR sets up an observability stack that includes tools such as Prometheus and Grafana and allows users to visualize and analyze the performance and behavior of the MCP Gateway.

**[PR](https://github.com/kagenti/mcp-gateway/pull/311)**

- Please note instructions or outcomes may be outdated as further work is done with telemetry in MCP Gateway.

**Instructions**:

```bash
git clone https://github.com/kagenti/mcp-gateway.git

```

1. `make local-env-setup`
2. `make inspect-gateway`
   - Ensure you are on the URL with the proper query parameters given from STDOUT.

3. Follow instructions [here](https://github.com/d0w/mcp-gateway/blob/tool-annotations/docs/guides/observability.md)
   - Try running some traffic by running some MCP requests to get logs with the annotation hints.

You should be able to get a dashboard in Grafana showing MCP Gateway tool calls.

### Keycloak Feature Flags

This adds configurability to Keycloak when adding new agents or tools to the Kagenti framework. Previously, adding a new client would automatically register itself with Keycloak as well as enable token exchange by default. You would then have to manually delete the Keycloak client or disable token exchange if you did not want those features. Now, with the inclusion of an environments ConfigMap (specific to a namespace), you can set flags to enable/disable creating a keycloak client or token exchange.

**PRs:**

- [kagenti/kagenti #399](https://github.com/kagenti/kagenti/pull/399)
- [kagenti/kagenti-operator #136](https://github.com/kagenti/kagenti-operator/pull/136)

**Instructions**:

```bash
git clone https://github.com/d0w/kagenti-operator.git # note this is a personal fork
cd kagenti-operator
git switch keycloak-flags

# in a separate terminal
git clone https://github.com/kagenti/kagenti.git
```

1. Follow the instructions [here](https://github.com/kagenti/kagenti/blob/main/docs/kind-install.md) and use `uv run kagenti-installer --skip-install operator` to skip the operator installation.
   - Ensure you have an ollama server listening
2. Go to the kagenti operator repository:

```bash
cd platform-operator

make ko-local-build

make install-local-chart
```

3. Edit a namespace's environments ConfigMap to and adjust the following flags as needed:

```bash
kubectl edit configmap environments -n team2
```

```yaml
KEYCLOAK_CLIENT_REGISTRATION_ENABLED: "true"
KEYCLOAK_TOKEN_EXCHANGE_ENABLED: "false"
```

4. Create tools/agents in the Kagenti UI (using the instructions in the Kagenti repository) and go to the Keycloak admin console -> clients -> newly created client. You should see that either the client does not exist or the standard token exchange checkbox is not checked.

# Project Description

## Vision and Goals

The project aims to expand the capabilities and adoption of [Kagenti](https://github.com/kagenti/kagenti/tree/main) by defining and implementing new use cases for the platform. This includes extending the core platform to support these new applications, such as integrating agents into enterprise Slack channels.

To facilitate adoption and demonstrate the platform's potential, we will create examples and demos that clearly showcase Kagenti's capabilities. The project will also contribute to the Kagenti project by improving its UI to enhance the user experience, adding new features to the platform, and fixing bugs or adding improvements based on open GitHub issues within the open-source repositories.

These goals are intended to ensure that Kagenti is a versatile, user-friendly, and effective tool that meets the needs of a wider range of users and use cases.

## Users/Personas

The project aims to expand the capabilities and adoption of Kagenti by defining and implementing new use cases for the platform as well as directly contributing to the project. This includes extending the core platform to support these new applications, such as integrating agents into enterprise Slack channels.

To facilitate adoption and demonstrate the platform's potential, we will create examples and demos that clearly showcase Kagenti's capabilities. The project will also enhance the Kagenti project by tackling fixing bugs, adding features, and other GitHub issues that come up.

These goals are intended to ensure that Kagenti is a versatile, user-friendly, and effective tool that meets the needs of a wider range of users and use cases.

### 1. Platform Engineers / DevOps Teams

As a platform engineer responsible for bringing AI agent workloads to production, I want an orchestration tool that simplifies deployment, lifecycle management, and secure integration of agents with my existing infrastructure, so that I can reliably scale, enforce security, and connect AI agents to tooling without manual overhead.

**Requirements**:

- Simplified deployment and lifecycle management of agents.
- A standardized operator that integrates agent workloads with infrastructure components like service meshes, gateways, and databases.
- Security enforcement (least privilege, identity propagation) across multi-agent workflows.

For these users, Kagenti needs to provide a standardized deployment and lifecycle manager through patterns such as Kubernetes operators. This will also meet their needs for properly scaled deployments. It will also need security enforcement for AI workloads connected to sensitive tooling while also monitoring traffic between AI agents and tooling effectively.

</br>

### 2. Enterprise Application Developers

As a developer building applications powered by AI agents, I want reliable and standardized APIs that abstract away deployment differences across agent frameworks, so that I can integrate agents into enterprise applications without worrying about infrastructure, scaling, or framework inconsistencies.

As an application developer that plans to create AI powered tooling, I want meaningful examples of how agents can be used with Kagenti in a variety of scenarios so that I can understand what value it provides to me and how easily I can deploy applications with the framework.

**Requirements**:

- Reliable APIs for embedding agents into enterprise apps such as Slack.
- A way to select frameworks fit for a use case without worrying about deployment inconsistencies.
- High availability, scaling, and fault-tolerance.
- Meaningful use case examples to demonstrate how effectively the project solves the developer’s problems.
  
Kagenti needs to standardize agent deployment across agentic frameworks such as LangGraph, CrewAI, or Llama Stack, ensure high-availability services, and provide consistent APIs according to a standard (A2A) in order to reduce integration effort and ease deployment of agent-driven applications.

</br>

### 3. Security Engineers

As a security specialist responsible for ensuring compliance of AI-driven workflows, I want continuous authentication and authorization between agents, tools, and human actors, so that I can eliminate static credentials, enforce least-privilege access, and reduce the attack surface of agentic workflows.

**Requirements**:

- Eliminate static credentials and enforce least-privilege access.
- Ensure continuous authentication and authorization for human and machine actors.
- Reduce the attack surface of agentic workflows.
  
Kagenti will need to implement an Agent and Tool authorization system that will continuously authenticate requests between agents and tools to reduce attack surfaces, eliminate credential spoofing to tooling through agents, and give security engineers a better understanding of requests being made with agentic workflows.

## Scope and Features

### In Scope

- **New Use Case Development**: We will design, build, and document new use cases for the Kagenti platform. This involves:
  - **Developing or Modifying AI Agents and Tools**: We will create or adapt agents to solve real-world problems. For example, we might develop an agent that integrates with email to automate communication processes.
  - **Proposing New Features**: If a use case requires a new feature to be added to the core platform, we will propose and document it. We will work with IBM engineers to implement these features and bring them to Kagenti.
- **Demos and Documentation**: We will create examples and demos that showcase Kagenti's capabilities, particularly for the new use cases we develop. This includes creating clear, step-by-step documentation to facilitate adoption and demonstrate the platform's potential.
- **UI Enhancements**: We will enhance the Kagenti UI to support new use cases. This includes improving usability, adding features that align with our project goals, and refining the overall design for a more intuitive user experience.
- **Platform Feature Developmen (all components)**: We will be building contributing directly via GitHub pull-requests into the Kagenti core platform (authorization pattern, MCP gateway, and operator) wherever the priorities of the IBM team lie. This includes but is not limited to fixing bugs, adding features, or developing scripts for installation.

### Out of Scope

- **Deep Technical Modifications to Existing Agents**: While we may modify agents to suit our use cases, we will not be undertaking major refactoring or deep technical work on the codebase of pre-existing agents outside the scope of our project.
- **Training Agents or Models**: We will not be training or optimizing models for specific use cases.
- **OpenShift Integration**: We will not be working on OpenShift integration for Kagenti, only vanilla Kubernetes.

## Solution Concept

![Alt text](images/weather-demo.png?raw=true)
We will adopt the existing Weather Demo architecture (above) as a reference point for our work. Our new demos will follow a similar pattern, ensuring alignment with Kagenti’s design principles while expanding its set of practical examples. We will also be working off this architecture when working on GitHub issues to extend the project's functionalities.

### Global Architecture Structure

The Kagenti platform provides the foundation for our work. Its Kubernetes operator, REST API, and built-in SPIRE integration allow us to securely orchestrate AI agents at scale. Building on this architecture, our contributions will extend the platform across multiple layers:

- **The Platform Layer**: Kagenti itself, with core features such as agent lifecycle management, workload identity through SPIRE, and a standardized API interface.
- **The application Layer**: The main focus of our contributions, where we design and implement new functionality.
- **Use cases & Demos**: We will develop interactive demos and real-world use cases using existing agents, ensuring they are well-documented and showcase end-to-end workflows on Kagenti.
- **New AI Agents**: We will design, containerize, and deploy AI agents tailored to practical scenarios, contributing both reusable code and templates for the community.
- **The user layer**: We will work directly on the UI, improving its design, adding new features as necessary, and enhancing usability. Our goal is to create an intuitive interface for developers to deploy and manage their agents.

### Design Implications

- **Emphasis on practicality**: We decided to focus on building real-world, tangible use-cases in order to validate Kangeti’s utility and demonstrate clear reasons for why developers should use it and what they can do with it.
- **Prioritizing user experience**: Our decision to work in-depth on the UI component is based on usability being a gateway for this powerful tool.E nhancing the interface will broaden accessibility, making it easier to deploy, monitor, and manage agents without deep platform expertise.
- **Building new agents**: Contributing new and diverse AI agents provides immediate value to the Kagenti community. These agents can serve both as functional demos and as templates for future development, encouraging further adoption and contributions.

## Acceptance criteria

### Minimum Acceptance Goals

- Use Case Development: Create 3 new use cases for Kagenti that demonstrate a range of Kagenti’s practical applications
  - Each use case will include complete documentation with setup instructions, architectural diagrams, and usage examples
  - At least one use case will demonstrate secure enterprise integration (e.g., Slack integration with proper access controls)
- Demo Creation:Develop 4 working demos showcasing Kagenti’s functionality
  - Each demo is fully functional and reproducible
  - Demos cover different aspects of Kagenti such as security, multi-agent workflows, and tool integration.
  - Include video walkthroughs for each demo
- Documentation: Produce a comprehensive documentation package for both MacOS and Windows
  - Step-by-step setup guides for each use case
  - API documentation for any new endpoints or integrations
  - Best practices guide for deploying agents with Kagenti
  - Troubleshooting guide for common issues
- UI Enhancements: Deliver improvements to the Kagenti UI
  - Implement at least 3 new UI features for the new use cases
  - Make UI more aesthetically pleasing/professional

### Stretch goals

Agent Development:

- Implement a production-ready agent with full error-handling and monitoring capabilities
- Core Platform Contributions:
  - Submit PRs to the Kagenti core repository with bug fixes or minor enhancements
  - Contribute to operator code base

## Release Planning

### Release #1 (by week 5)

- Research on Kagenti
- Running existing demo, adding any necessary documentation if needed
- Research MCP, Kubernetes. Find agents and tool to add to Kagenti

### Release #2 (by week 7)

- PR for UI changes to display env variables and other various improvements
- Finalize new use cases for Kagenti based on research
- PR for platform features in Kagenti, operator, or MCP Gateway

### Release #3 (by week 9)

- Create demos for showcasing Kagenti
- Add additional agents and tools to Kagenti
- PR for platform features in Kagenti, operator, or MCP Gateway

### Release #4 (by week 11)

- Create demos for showcasing kagenti
- Suggest to Kangti team new features based on our experience
- PR for platform features in Kagenti, operator, or MCP Gateway

### Release #5 (by week 13)

- Publish polished demos and tutorials
- Final demo recording and update readme.md
- PR for platform features in Kagenti, operator, or MCP Gateway
