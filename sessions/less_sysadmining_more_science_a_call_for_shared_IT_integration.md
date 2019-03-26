# Less sys-admining! More science! A call for cross-center IT integration 

## Computing hardware infrastructure
Generally, computing infrastructure we use can be divided into three tiers:

### Tier 1: Your own laptops
* Users have admin rights
* Easy to use for interactive work (e.g. RStudio, Jupyter Notebooks)
* Low compute capability
* Can't store sensitive data
* Not suited for long-running analyses
### Tier 2: Lab owned servers
* Users have admin rights or work closely with someone who has
* Easy to use for interactive work (e.g. RStudio, Jupyter Notebooks)
* Medium compute capability
* Typically can store sensitive data
* Suited for long-running analyses
* Typically under heavy load, long running analyses can interrupt work of others
### Tier 3: HPC installations (Computerome, DTU HPC)
* No admin rights
* Interactive work using RStudio/Jupyter is challenging or impossible
* High compute capability (many high memory, high cpu nodes)
* Typical can store sensitive data
* Suited for long-running analyses
* Use environment module system
  
## Sysadmin things that stand in way of doing science
### Installation and maintenance of software 
Simply takes a lot of time and effort. Big pain points are:
- complex interdependencies between scientific tools and their dependencies such as other tools or libraries
- irregular release cycles of scientific software
- lack of dedicated staff to run installations on *tier 1* and *tier 2* hardware
- difficult to make homogeneous environments across different tiers of infrastructure
- installation on *tier 3* requires action from HPC staff, takes time and may be tricky for non-domain experts
  
Partially alleviated by:
- use of docker/singularity. While very effective still requires the user to find the right images or create them (essentially requiring to go through the same pain). Installing and compiling software using bash commands is challenging for users with no sys-admin experience.
- use of python/R packages and virtual environment. These package managers only support packages of either language rather than deal with scientific software tools generally - f.e. samtools or plink
- use of anaconda. Very effective and simple if conflicting software interdependencies are not an issue within a project and conda packages are readily available. Otherwise require the installation effort.

### Making data-science sound experiments (slightly off-topic, bare with us)
Developing good experiments (from statistical, computational and software development perspectives) is hard, it is easy to make mistakes when planning projects

### Leveraging full range of computational infrastructure
Work on *tier 3* installations (queueing systems, handling data copying etc) can be challenging from newcomes and individuals without computational background

## So what can be done about this
### Better onboarding and training
Each center should introduce better procedures when onboarding new computational people - familiarizing them with computational infrastructure options, their use, best practices
Software carpentry course at center for biosustainability could alleviate some of these needs across centers. Possibly more focus in the course should be directed at use of queueing system and *tier 3* facilities effectively.

### Cross-center computational support staff
Inspired by Carol Goble talk and Research Software Engineers at University of Manchester who help to create software in a better/sustainable manner.
This could be arranged by hiring staff with relevant experience to rotate between centers and consult scientists when planning, starting and at critical points in projects life-cycle

There is a need to have cross-center support staff that could help scientists with:
- Data science consulting: Designing their experiments so that they are statistically and computationally sound
- Computational excellence consulting: Helping users with their current computational needs
  
### Shared software repository across NNF centers
Goals:
- Distribute pain of software installation and management
- Create a homogeneous software environment on *tier 2*, *tier 3* and using containers *tier 1* environments

This could be achieved in, likely, several ways. Proposed were using conda packages and a mix between environment modules and ansible.

Ansible & environment modules idea:
- inspired by https://github.com/MonashBioinformaticsPlatform/bio-ansible
- establish shared directory structure in software repositories
- define software compilation & installation procedure as ansible playbooks
  - ansible provides convenient abstractions over bash for software installation tasks
  - after developing ansible module for a piece of software, making one for new version would be trivial
  - ansible would create a module file as well
  - this could be partially automated by pulling software revisions from github repos etc.
- environment modules would enable dealing with software dependencies and provide compatibility with HPC facilities like Computerome
- making this repository available on Computerome and *tier 2* systems would be trivial
