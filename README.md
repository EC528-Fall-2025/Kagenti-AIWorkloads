# EC528-Fall-2025-template-repo

## Vision and Goals


## Users/Personas
The project aims to expand the capabilities and adoption of Kagenti by defining and implementing new use cases for the platform. This includes extending the core platform to support these new applications, such as integrating agents into enterprise Slack channels.

To facilitate adoption and demonstrate the platform's potential, we will create examples and demos that clearly showcase Kagenti's capabilities. The project will also enhance the Kagenti UI by improving its usability, adding new features, and refining the overall design to create a more intuitive and powerful user experience.

These goals are intended to ensure that Kagenti is a versatile, user-friendly, and effective tool that meets the needs of a wider range of users and use cases.

### 1. Platform Engineers / DevOps Teams
These are engineers responsible for bringing AI agent workloads to production within organizations or for users. They own Kubernetes clusters, networking, security, and scaling, and handle the orchestration of connecting agents to tooling.

**Requirements**:
- Simplified deployment and lifecycle management of agents.
- A standardized operator that integrates agent workloads with infrastructure components like service meshes, gateways, and databases.
- Security enforcement (least privilege, identity propagation) across multi-agent workflows.

For these users, Kagenti needs to provide a standardized deployment and lifecycle manager through patterns such as Kubernetes operators. This will also meet their needs for properly scaled deployments. It will also need security enforcement for AI workloads connected to sensitive tooling while also monitoring traffic between AI agents and tooling effectively.

</br>

### 2. Enterprise Application Developers
Developers building end-user applications (e.g. customer support bots, RAG assistants, workflow automation tools) that rely on agent frameworks.

**Requirements**:
- Reliable APIs for embedding agents into enterprise apps such as Slack.
- A way to select frameworks fit for a use case without worrying about deployment inconsistencies.
- High availability, scaling, and fault-tolerance.
  
Kagenti needs to standardize agent deployment across agentic frameworks such as LangGraph, CrewAI, or Llama Stack, ensure high-availability services, and provide consistent APIs according to a standard (A2A) in order to reduce integration effort and ease deployment of agent-driven applications.

</br>

### 3. Security Engineers
Security specialists that need to ensure that AI-driven workflows comply with enterprise or regulatory security standards.

**Requirements**:
- Eliminate static credentials and enforce least-privilege access.
- Ensure continuous authentication and authorization for human and machine actors.
- Reduce the attack surface of agentic workflows.
  
Kagenti will need to implement an Agent and Tool authorization system that will continuously authenticate requests between agents and tools to reduce attack surfaces, eliminate credential spoofing to tooling through agents, and give security engineers a better understanding of requests being made with agentic workflows.
