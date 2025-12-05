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

# Completed Work

A variety of agent and MCP examples that can be integrated into the Kagenti platform as well as contributions to the various Kagenti repositories.

## Simple Setup

This does not encompass all the work done, but it gets the Kagenti platform up and running with a simple agent and tool. Contributions will have links to the relevant documentation or instructions.

1. ...

## Agents

- Agent 1
   1. instructions ...

## MCP Servers

## General Contributions

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
