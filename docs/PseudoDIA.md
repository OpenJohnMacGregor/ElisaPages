---
layout: default
title: "Pseudo-DIA: The Dance of the  5 Veils"
description: Discussion papers related to the Linux Foundation ELISA Project
---
> The relationship between the Linux Kernel Development Community and 
> the entities that use the Linux kernel plays a central role in 
> defining how the Linux development process conforms to ISO 26262.
> Lukas Bulwahn made a proposal to frame the relationship in terms 
> of a Development Interface Agreement <DIA), a construct the standard
> uses to allow the description of the relationship between an 
> organisation that develops elements and it suppliers.
> He termed it a "Pseudo-DIA"

> A long e-mail thread ensued, which contained a clarification of the 
> concept spread over 5 stages.
> With each stage of the clarification, a veil would fall - hence the title.

> This paper cleans up the thread and presents a unified concept for
> describing the "Pseudo-DIA".

# Prologue: Lukas' Proposal

Dear all,

(sorry, this has been way too long in my email draft folder... but it is also quite a lengthy email)


Elana, Jochen et al. has proposed a good structure to document the existing development process. This will help us to document our understanding, spread information among each other and determine the criticality of certain gaps/weaknesses in the development process. Then, we have a common plan what we would like to increase our shared efforts on address in the future wrt. development process in the Linux kernel development community.

As I said, while doing my part of the work (release planning), I hit an issue when defining release planning/releasing. I have observed the same, or at least similar, issue in the work of other topics as well, e.g., in management aspects, and impact analysis for new releases.

I simply was not sure if there is a common agreement/understanding on what we (each individual and we as common group) think "the Linux Kernel Development Community delivers" (what is the output of what the Linux Kernel Development Community) and "what the Linux Kernel Development Community requests from its Users" (how do they agree on that historically, how do you need to behave based on that agreement; what you would need to provide as input) and "what the Users need to do because they need to do it for their product development". 

So, I quickly tried to define the Linux Kernel Development Community and the User as terms in the glossary, but that only a very partial solution to the issue I faced.

Linux Kernel Development Community: The Linux Kernel Development Community is an organizational entity that encompasses all persons that have contributed (directly or indirectly) to changes to the Linux Kernel.
The main deliverable from the Linux Kernel Development Community is the Linux kernel source code repository (the tree in the git repository and its history), containing a pre-existing configurable software.

User: The User is an (abstract) organizational entity that develops a system, which includes one specific configuration of the pre-existing configurable software (Linux Kernel), and puts this system into the public space. The term User may incorporate multiple organizations in a supply chain up to the OEM, and it includes all phases of the system development, from system design, requirements engineering, configuring the kernel, building the kernel, HW-SW integration and to production, maintenance and decommission.

The definitions above are an extract from the Glossary
[Kernel Development Process WG Glossary][devWG glossary].  

For a better solution based on those definitions, I came up with this basic idea:

### Why describe the scope of Linux Kernel Development Community and its interface?

The motivation to describe the scope of Linux Kernel Development Community and its interface more precisely is:

1. initially, for us to improve our common understanding: When we talk about considering the execution of a process step (in the standards' understanding), do we mean: do we assume to the process step is executed by the Users or by the Community? What are expectations that come with that activity?
2. later, for anyone else trying to understand the basic assumptions what the user explicitly needs to do and what the user needs to check to hold (control they still hold) about what we state at a certain point in time about the development process (and which might not hold at a later point in time).
3. later, to motivate stakeholders to support certain procedural changes in the Linux kernel community (or actually, community suborganizations that are relevant to the stakeholders) or to engage in the community to implement this change.

### How to describe the scope of Linux Kernel Development Community and its interface?

To describe the scope of Linux Kernel Development Community and its interface, I propose to formulate a "pseudo DIA" (I would certainly like to find a better suitable term than that, and I am happy to hear any quickly brain-stormed suggestions in this mail thread).

First, we introduce the standards' definition of a development interface agreement (DIA), summarizing the expectation of and then explain the relevant difference of a "pseudo DIA" for an open-source development to a traditional (customer-supplier) DIA.

According to ISO 26262, Edition 2, Part 1, 3.32, a Development Interface Agreement (DIA) is an "agreement between customer and supplier in which the responsibilities for activities to be performed, evidence to be reviewed, or work products (3.185) to be exchanged by each party related to the development of items (3.84) or elements (3.41) are specified."

This definition includes the following characteristics:
1. a specification of the scope, i.e., the development of an item or element 
1. an agreement between two parties involved in the development of that scope
1. description of activities
1. assignment of activities to each party
1. acceptance of the responsibility on that activity by the assigned party
1. description of resulting evidences or work products that need to be created by one party and provided as input to the other party for a further activity.
{: .alphaList}

### Understanding the default agreement between the Kernel Community and its Users

When we consider a software delivery/release of the Linux kernel, the Linux Kernel Development Community makes the following offer to all its Users.
Concerning the legally binding offer, the GPL License clearly states (in capital letters):

>NO WARRANTY
>
> 11\. BECAUSE THE PROGRAM IS LICENSED FREE OF CHARGE,
THERE IS NO WARRANTY FOR THE PROGRAM, TO THE EXTENT PERMITTED BY APPLICABLE LAW. EXCEPT WHEN OTHERWISE STATED IN WRITING THE COPYRIGHT HOLDERS
AND/OR OTHER PARTIES PROVIDE THE PROGRAM "AS IS" WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESSED OR IMPLIED,
INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE.
THE ENTIRE RISK AS TO THE QUALITY AND PERFORMANCE OF THE PROGRAM IS WITH YOU. SHOULD THE PROGRAM PROVE DEFECTIVE,
YOU ASSUME THE COST OF ALL NECESSARY SERVICING, REPAIR OR CORRECTION.
>
> 12\. IN NO EVENT UNLESS REQUIRED BY APPLICABLE LAW OR AGREED TO IN WRITING WILL ANY COPYRIGHT HOLDER,
OR ANY OTHER PARTY WHO MAY MODIFY AND/OR REDISTRIBUTE THE PROGRAM AS PERMITTED ABOVE, BE LIABLE TO YOU FOR DAMAGES,
INCLUDING ANY GENERAL, SPECIAL, INCIDENTAL OR CONSEQUENTIAL DAMAGES ARISING OUT OF THE USE OR INABILITY TO USE THE PROGRAM
(INCLUDING BUT NOT LIMITED TO LOSS OF DATA OR DATA BEING RENDERED INACCURATE OR LOSSES SUSTAINED BY YOU OR THIRD PARTIES
OR A FAILURE OF THE PROGRAM TO OPERATE WITH ANY OTHER PROGRAMS), EVEN IF SUCH HOLDER OR OTHER PARTY
HAS BEEN ADVISED OF THE POSSIBILITY OF SUCH DAMAGES.
{: style="font-style: normal"}

[quoting Clause 11 & 12 of the GPL 2.0 License][gnu v2.0]

So, in short, the Linux kernel does what it does (there is no fitness for a particular purpose), comes with no claim of quality of any kind, and all risks are in the users sole responsibility.

However, the Linux kernel community also offers the following interface for the suggested development procedures for any User:

First, whenever a release candidate is published, Linus asks:

"Go out and test (and special thanks to people who already did, and started sending reports even during the merge window)"
[Linus Torvalds,  Linux 5.5-rc1][linus 5.5-rc1]  
"So peeps - go build it, install it and boot it, and report back any problems you see," 
[Linus Torvalds,  Linux 5.5-rc2][linus 5.5-rc2]  
"but please do use the down-time to do some extra testing instead, ok?"
[Linus Torvalds,  Linux 5.5-rc3][linus 5.5-rc3]  
"Scan the shortlog below if you are into that, but otherwise just go forth and test it out all," 
[Linus Torvalds,  Linux 5.5-rc6][linus 5.5-rc6]  
" Please do test, there should be nothing scary going on." 
[Linus Torvalds,  Linux 5.5-rc7][linus 5.5-rc7]   

It is probably an interesting of study of English literature to create a full list of quotes where Linus asks on various ways over and over for the one thing that he requests from the Users, namely to test the provided release candidate and report any issues. Then when the User sends back a report of a bug or regression, the Linux Kernel Development Community reacts to that feedback, and clear regressions (usually) lead to fixes or removal of the complete functionality causing the regression.

And with the final release, Linus asks as well:

"Anyway. Go out and test 5.5" [Linus Torvalds,  Linux 5.5-final][linus 5.5-final]   

But at this point, there is a consensus that the majority of the community has moved on, and the reports back on this version later are handled differently. Ultimately, it is up to the user to test during the release candidates and report back to the community, and nevertheless to test the final release on fitness for the user's purpose. For most users---although they may be unaware of it---, this agreement is sufficient to build products relying on these provided Linux kernel releases.

### Useful Interpretation of a DIA for the Linux kernel for specific environments

Specific environments, such as systems under certain regulations, critical environments, i.e., high-integrity, safety- or security-related systems, may intend or require a clear and formalized understanding of which activities of an assumed overall system and software development process, the kernel community is executing and which activities are to be executed by the user.
This description is often needed to estimate the risks of the kernel development process and to reduce those risks by further mitigating activities by the user.

A "Pseudo-DIA" includes the following characteristics:  
1. a specification of the scope, i.e., the development of an item or element
1. a definition of two parties involved in the development of that scope
1. description of activities
1. assignment of activities to each party,
1. evidences that the assignment meets the actual reality of executed activities among the two parties
1. description of resulting evidences or work products that need to be created by one party and provided as input to the other party for a further activity.
{: .alphaList}

In other words, a "Pseudo-DIA" can describe "a specific scenario between two parties in which activities are performed, evidences are reviewed, or work products (3.185) are exchanged between two parties related to the development of items (3.84) or elements (3.41) are specified."

### Difference between DIA and Pseudo-DIA

Compared to an DIA, the definition of a Pseudo-DIA differs in the following aspects:

An agreement between two parties involved in the development of that scope (DIA, b.) is replaced by a definition of two parties involved in the development of that scope (Pseudo-DIA, b.).

Acceptance of the responsibility on that activity by the assigned party (DIA, e.) is replaced by evidences that the assignment meets the actual reality of executed activities among the two parties (Pseudo-DIA, e.).

The difference is inherently due to the structure of the organization around an open-source project, and the common agreement among developers and users to exclude warranty of any kind, as far as legally permitted.

Hence, a Pseudo-DIA does not represent a signed agreement between two organizations. There is no one from the community as a representative that can sign this agreement, as a community comes to conclusion by merit-based consensus, not by strict enforcement from single individuals towards other peers within an organization (e.g., in a hierarchical structured organization, with enforced roles and capabilities to enforce behavior of others). Further, the individuals would not really sign such an agreement towards specific users without further contractual agreements, as there is no incentive to the signer in his role as representative of the community.

Note, in different roles and within different organizational structure, somebody might sign such agreement with another organization, but then it more likely to be in a setting similar to traditional customer-supplier relationships.

As a Pseudo-DIA only includes a definition, but not an agreement, the author of a Pseudo-DIA does not need to be affiliated in any way to any of the two parties that are described in the Pseudo-DIA.

### Value of a Pseudo-DIA

The value of such a pseudo-DIA is determined by the degree that the provided definition reflects the actual reality of the activities among the two parties, or is at least attractive and realistically achievable as envisioned development process to the two parties, which we will call Community and User in the following description.

The activity of creating or following a Pseudo-DIA, i.e., determining an assignment of activities/aspects to those two parties, the User can understand how the quality assurance/assessment of each specific activity could generally be used for an overall development process assessment:

1. in case you assign an activity to the User, the Pseudo-DIA author's recommendation is that the User needs to execute the whole activity within its organization.
2. in case you assign it to the Community, the Pseudo-DIA author's recommendation is that the User needs to observe if the Community actually executes the activity and determine if the activity is done with sufficient care and rigor for the User's interest.
(The development-process group might provide methods and tools to allow efficient observation of Community behavior.)

So, in any case, it is ALWAYS the User that needs to do something, but the activity is slightly different in the two cases.

Despite the difference to an DIA, an appropriate Pseudo-DIA can achieve a similar confidence of truth (or trust) in a development process assignment as a DIA. The agreement on a Pseudo-DIA, missing formally in the Pseudo-DIA artefact, consequently happens by an implicit consistent behavior of the two parties to the provided definition and by confident monitoring of the activities and relevant qualities of those activities with suitable and effective reactions in case the behavior of any of the two parties change. All information gathered while monitoring the activities and qualities can serve as evidence towards any third party.

### Example content for the Pseudo-DIA Description

To conclude the definition of a Pseudo-DIA, we describe one example of Pseudo-DIA activity descriptions and assignment for the Linux kernel.

Example: Management of Competence

ISO 26262, Part 2, Clause 5.4.4.1 states: The organization shall ensure that the persons involved in the execution of the safety lifecycle have a sufficient level of skills, competence and qualification corresponding to their responsibilities.

In the further example, the aspects are defined as follows:

1. A specification of the scope, i.e., the development of an item or element
: The scope of this Pseudo-DIA is the Linux kernel v5.5, ultimately integrated in Linus Torvalds git repository and tagged as v5.5 by Linus Torvalds during the release process of v5.5. This definition in this example excludes the later v5.5.y versions in the linux-stable repository.

1. A definition of two parties involved in the development of that scope
: The Linux Kernel Community and the User as defined above.

1. Description of the activities
: Basically, we assume the Linux Kernel Development Community is responsible for design, implementation and documentation of the functionality implemented in v5.5; that the requirements fit to the use case, testing, verification and validation is to the user. Hence, for this main responsibility, the sufficient level of skills, competence and qualification is knowledge of the C dialect used for kernel development and experience and knowledge in operating system design and implementation.
Ensuring that each person has sufficient level is split into the following activities: identification of competence for each contributor, clear documentation of the contributor's role within the development community and the contributions, determination if competence fits to contributor's role according to criticality of the functionality to the product safety.

1. Assignment of activities to each party
: The activities above are assigned as follows:
    - Identification of competence for each contributor is assigned to the Linux Kernel Development Community.
    - Clear documentation of the contributor's role within the development community and the contributions is assigned to the Linux Kernel Development Community.
    - Determination if competence fits to contributor's role according to criticality of the functionality to the product safety is assigned to the User.

1. Evidences that the assignment meets the actual reality of executed activities among the two parties
: The contributor's competence can be judged based on the previous contributions to the Linux kernel repository and their involvement in email review. All contributions by an individual are recorded and significant contributions of suggestions and review are recorded with further tags in the commit message. Continuous unhelpful review is eventually marked by the Linux kernel community by ignorance of those contributions. The role of central developers are recorded and maintained in the MAINTAINERS file.
The User has to check that the community continues to archive all contributions and email discussion and to maintain MAINTAINERS appropriately.

1. Description of resulting evidences or work products that need to be created by one party and provided as input to the other party for a further activity.
: The Linux Kernel Development Community provides a clear list of all contributors and their contributions, i.e., git history and email archives. The User needs to check availability of all recent information of all relevant sources. The User needs to make the judgement if the contributor had sufficient competence for the relevance of the contribution and mitigate with further activities if the competence if not considered sufficient. The User is responsible for mitigations of identified shortcomings with regard to competence management for the specific product usage. Note, at the moment, the gap from a practical view could to be that the current interface between Linux Kernel Development Community and the User is a "rather raw-data interface"; the User has not yet defined an interface that might be more suitable for the product-relevant competence judgement than the currently described interface.
{: .alphaList}

### Afterword

To be clear, this is NOT thought as replacement of the current plan and activity in the development process group, but as (possibly later) an addition---depending on the relevance of the Community-User interface for the topic of your investigation, which I hit quickly for release planning during the definition already. So, I will focus on describing release planning first, get that done and then assist wherever I can on the current tasks and then see how to progress with this work here. So far, here is only one example, I had further ones in mind but then I decided to get this email out first, and come up with further descriptions of example when needed.

Nevertheless, please comment and provide feedback. Especially, I would like to know if it helpful for you or not now or if we shall delay determining a consensus to a later point.

After I got some initial feedback on the mailing list, I will transfer the consensus of this discussion then into a first draft of a Google Doc (you can probably already see a first document structure in this email) and we can then work together on the details.

# Veil 1: Clarification

I was preparing a response to Lukas email, but I hit a dead-end and haven’t got back to it.

But, one of my first comments was simply to try to provide some background information for the uninitiated, especially those without access to ISO 26262. I’ll repeat it here, in case people want to prepare a bit for the discussion.

---

The uninitiated (like me) might like to read 26262-8 5.3 - 5.5 and 26262-8 Appendix B for those who have access to the standard.  A quick google revealed [1][2] which might be a start for those who don't (at least they're a quick read).  [3] offers a number of interesting insights into the general context.  Note that the clause is not applicable to OTS SW components (use clause 12 instead) as they are not built to order...

 

[1] <https://automotive.wiki/index.php/Development_Interface_Agreement>

[2]  <https://link.springer.com/content/pdf/10.1007%2F978-3-658-26107-8_18.pdf>

[3] <http://www.specialoperationssummit.com/media/8516/14781.pdf>

---

# Veil 2: We're talking about an operating system here

We're talking about an Operating System here - and systems developers would never develop an operating system from scratch for their new embedded systems. Not Samsung or LineageOS for mobile phones, for example.  Not TP-Link or OpenWRT for routers...  They select the operating system flavor and version that best suits them "off the shelf" and integrate it into their products.

I dug out an old illustration of a bog-standard V-model for embedded systems(enclosed).  It could have been from a textbook i.e. [1]  but it's mostly compatible with the processes envisaged by safety standards. I added the operating system aspects.  I'm neglecting the hardware development process here as well.

![Bog-Standard V-Model](/assets/graphics/BogStandardVModel.svg){: .svgImg}

According to the textbook definition, the operating system-related part of the development process starts at the software architecture phase.  The system developer may initially have a set of operating system alternatives to choose from, say an RTOS or Linux or even BSD for all I know.  The basic application functionality and its (logical) requirements on the OS are defined in the architecture phase.  As processing aspects are considered, specific interfaces to the OS are identified at the technical design stage.  Probably at this stage at the latest, the alternatives have been narrowed down to one operating system.  Extraneous OS functionality, such as communication stacks or file systems can be eliminated and options can be chosen which defines a specific OS configuration.  Code may have to be developed to bring the OS up at run-time. 

There are then OS-related aspects to the validation activities which correspond to the various development phases.

==> The system developer selects, configures and tests an operating system: no development is involved, neither by the system developer nor by the operating system supplier, and by extension there is no need for a DIA.

There is of course, the possibility that the system developer needs custom OS functionality, a new feature (or, to use Chris Temple's terminology, a chunk).  In which case, if the system developer can afford it, either party can develop the feature or enhancement from scratch.  Consider what Google has done with off-tree development of Linux functionality for Android, which they sometimes got retroactively accepted upstream.  In this case, Google would be making a DIA with itself: between its Android and Linux organisations, which is foreseen in the definition of a DIA.

While a system developer must choose an operating system from the flavours and versions that are available at the time, what ELISA is actually looking at is the interaction between the user community and the Linux development community.  The user community has the possibility to specify its expectations on future operating system development: a DIA for future functionality in general rather than for a specific feature development effort.  The operating system developers then have the possibility of considering the needs of the user community when adding or modifying OS features.

Again, this holds for all systems, safety-critical or not.  I'll consider safety-critical systems in the next e-mail.

[1] <https://www.geeksforgeeks.org/software-engineering-sdlc-v-model/>

# Veil 3: Safety for Operating Systems involves functional and quality requirements

For this e-mail, I've enhanced the general V-Model with safety activities / processes.  This means that the diagramme covers the general development lifecycle as well as the safety lifecycle.  The standards are not so clear about that.  Rather than having a separate, parallel V for the safety lifecycle, I've inserted orange "safety" boxes in the nodes representing each development phase.

![V-Model with Safety](/assets/graphics/VModelWithSafety.svg){: .svgImg}

In the case of ISO 26262, there is the famous illustration of the 3 Vs superimposed over the overview of the standards series (Figure 1 in every standard) and Figures 2 & 3 in Part 4 which replace the hardware and software Vs with boxes.  The enclosed illustration seems generally compatible.

It's not generally included in the V-Model, but in the context of safety-critical systems, there should be backwards traceability between the requirements and the work products that implement them.

Two points are immediately noticeable:
1. The standards' requirements mostly only cover the tip of the iceberg of system development activities.  (Well, I have to admit I made the orange boxes small so that they wouldn't interfere with the phase titles, however (-:  ).
1. There is an overlap between safety functionality and operating system functionality.
{: .alphaList}

Those turquoise boxes represent the development process all application, middleware and, yes, operating system elements in the safety-critical system.  The system itself is composed of (using a somewhat arbitrary mixture of terminology):
1. newly-developed safety  elements
1. newly-developed non-safety elements
1. pre-existing safety elements that have been used in a similar domain
1. pre-existing safety elements that have been used in another context (at least from the 26262 perspective), i.e. another instance of the same product class
1. pre-existing non-safety elements
1. pre-existing safety components (hardware and software)
1. pre-existing non-safety components (hardware and software)

each of which may have a different certification or qualification route as well as different generic development processes.  The difference between elements and components seem nebulous to me and I'd rather call pre-existing things "off-the-shelf", whereby one might have to differentiate whose shelf they come from.

From the previous e-mail (which admittedly considered only non-safety-critical systems), a Linux that is currently being selected for use in an embedded system would belong to category 7 and that is the focus here.  It may soon be the case that safety-critical applications will use Linux.  There may come a time, where safety functionality has been brought upstream to the Kernel, but these are now not quite the case.

The safety-critical system development process starts by defining the safety-critical system and the environment (context) within which it operates.  A hazard and risk analysis is then performed to develop the safety requirements on the system and a corresponding functional safety concept.  A technical safety concept is developed in the system architecture phase, which ultimately results in safety requirements on the software architecture, and therefore on the operating system.

At this point the requirements on the operating system should be functional requirements, for safety mechanisms or safety functions, and / or requirements on the qualities of those functions (response time, resource consumption, etc.).  Safety functionality, or mechanisms, include such things as monitoring, periodic testing, diagnostic and logging functionalities, tolerance mechanisms for residual design faults in the hardware, environmental stresses, operator mistakes, residual software design faults, data communication errors and overload situations; things that may already exist in the operating system in some form.  Refer to 61508-3 7.2.2.10 a) for a better list.

In other words, the safety-related requirements on the operating system should already be functional or quality requirements that should comparable to other requirements on the operating system.  

This principle has already been accepted by a number of accreditation agencies in the context of SafeScrum.  There, the hazard analyses result in hazard stories, which are stored in the product backlog.  The hazard stories reflect a certain functionality that enable the system to achieve or maintain a safe state in a certain hazard scenario.  During a sprint, the developers are instructed in the safety-critical aspects of the hazard story by accompanying safety personnel.  The developers develop the hazard functionality while monitoring the safety-related requirements.

In the context of the general development lifecycle of a safety-critical product, i.e. the turquoise boxes,  the system developer would again go through the selection and configuration process for an operating system as would be done in developing a conventional system.  The operating system has already been developed and therefore has the functionality and qualities that it delivers "off the shelf".  The developer must ensure that the operating system meets its functional and quality requirements.  Where there are alternatives, the system developer would have the option of choosing the candidate that best meets the requirements, perhaps with an emphasis on its systematic capability (i.e. the potential of an element to lead to a failure of a safety function).

Currently, Linux has not been developed for safety-critical applications, but it may be that it already possesses functionality to perform safety functions with adequate quality.  Otherwise, there is the possibility, as in the case with Google and Android,  that the system developer can develop, or commission the development of, the necessary functionality.  This is the only time there is a development process, and that is not for the operating system but for a feature of the operating system.

In the context of safety, I could foresee see possible Kernel development activities related to new drivers and for the safety functionality.

The point here is that Linux has always (up to now) been developed as functionality.  It may be possible to isolate the safety-related parts of that functionality and, as part of the systems engineering part of the development process, attach quality requirements to them and validate that the requirements have been achieved.  For me, this would be the development interface for the DIA.

# Veil 4: Developers are users too!

The world is not so clear-cut.  The developers are also users.  But...  not all users are developers.

It should be clear that at least some of the developers contributing code to Linux work for companies that develop Linux-based systems.  All probably develop on Linux-based systems.  Some users are pure users and just use the code in their systems and don't contribute to the Linux Kernel.  Some developers may work on deep, general issues 

In the group's discussion about whether the upper group should be called downstream developers or users, I would tend to using the term users.  It may be a tired, ambiguous, oft-used term, but it describes what I see with a brutal clarity: by my definition, the users are users because they use the software (i.e. without modification), nothing more.

What you have proposed[1] is a model and from a process perspective, "users" and "development community" are roles.  The terms are a little confusing as I think of users as being individuals, not organisations.  Of course, the same person can be both a user and a Linux developer.


From your original e-mail:

> However, the Linux kernel community also offers the following interface for the suggested
> development procedures for any User:
> release candidate is published, Linus asks: ... "Go out and test...

Who is he addressing here? Isn't it the Linux Development Community, not a user per your definition?

> the Linux Kernel Development Community reacts to that feedback, and clear regressions (usually) 
> lead to fixes or removal of the complete functionality causing the regression.

Again the Development Community is involved... and the result is source code.  But, as with patches that make it to staging, the development community generates some activity on the mailing lists that reflect design or architectural decisions.

The first impression I had was that the development community just contributed the to the main deliverable, the source code repository.  I see a class of user-developers that conceive enhancements / modifications / new features for the kernel.  There would then be 3 roles in the process:
1. The pure developers which submit code to the repository,
1. The user-developers which may or may not contribute code but who also contribute enhancements with architecture / design implications and
1. Users, who as the name says, just use Linux, as in select and configure the available code.

For this e-mail, I've enhanced the safety-critical lifecycle diagramme with 3 corresponding communities (enclosed).  The line of demarcation between the "pure" development community and the user-development community is somewhat arbitrary.  As a first guess,  I've put it above module design.  The upper group might be called "user community", but I think that if they were indeed a community, they band together and get involved in the development.  Per definition, that is not what I intend.

![Communities](/assets/graphics/Communities.svg){: .svgImg}

In the next e-mail, I'll discuss the implications of this perspective on the work in the group and ELISA's position in the community.

[1] [Kernel Development Process WG Glossary][devWG glossary]

# Veil 5: Discussion and Conclusions

So, back to the original question with respect to the development interface:
Who does which parts of the development process and with which responsibility?

Take a look at the communities diagramme from 4/5.  You can define a development interface on any edge of the diagramme.  If necessary, you can divide the nodes in two and define an interface between the halves.  Each node has processes or activities, with corresponding roles.  The activities can have responsibilities split on the user and Kernel side.

For me, there are two Pseudo-DIAs: one between the user(aka system integrator) community and the user-developer community and another between the user-developer community and the developer community. I don't know if the split is worth the effort.  Another possibility would be to combine the user-developer and developer communities and just have one Pseudo-DIA.

Taking a look at your original e-mail, I've recognized that the intent could have been to take the process areas that the group has defined and refine them with splitting the roles and activities between the users and the Kernel development community.  I'm not sure what that would mean without a fundamental understanding of what parts of a safety-critical Kernel are used (i.e. selected and configured) and which are developed.  Only the parts that are developed need be characterized in the development process.... a tautology indeed.  Over and above there are, of course, parts of the kernel, drivers, instruction architectures and maybe some communication stacks, perhaps, that are irrelevant to safety and/or embedded systems in general and could be excluded from consideration entirely.

It can also well be that the desired hardware / safety architecture can affect which development process is used.  Hypervisor-based? AMP or SMP? Separate single-processor chip?

For this e-mail, I've extracted the communities layer from the diagramme and refined the concept of user-developers.  It's conceivable that we could identify or organize a safety community that manages the safety-related issues and Linux features.  There are other user-developer communities as well:
- The Android community (take a look at what Google has done for the Kernel),
- The security community (take a look at what [Google again, DARPA? (SELinux), seccomp or grsecuity] have done),
- The container community(Docker, lxc/lxd, etc.).

Each of these communities contribute subsystem architectures / designs to the Kernel.  The user-developer / developer split seems to make sense.  That being said, getting intermediate work products, like design documentation for integration testing might be incredibly difficult.

![Linux Communities](/assets/graphics/LinuxCommunities.svg){: .svgImg}

The fundamental problem: the process being used has to be documented and adherence has to be demonstrated.  This is quality stuff not safety stuff.


So, there we have it.  The last veil has fallen and we see the Pseudo-DIA in all its splendor.  Don't forget to admire it.   It was a great idea.

# Bibliography

## Links

### External

1. [Kernel Development Process WG Glossary](https://docs.google.com/document/d/1d91Znr2IWPI3pgDk_Nz2BcVNWHQgyBxk_18dAqnskiw/edit?usp=sharing "Kernel Development Process WG Glossary")<br/>
1. [GPL 2.0 License](https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html "GPL 2.0 License")<br/>
1. [Linus Torvalds,  Linux 5.5-rc1](https://lwn.net/Articles/806771/ "Linus Torvalds,  Linux 5.5-rc1")<br/>
1. [Linus Torvalds,  Linux 5.5-rc2](https://lwn.net/Articles/807349/ "Linus Torvalds,  Linux 5.5-rc2")<br/>
1. [Linus Torvalds,  Linux 5.5-rc3](https://lwn.net/Articles/808000/ "Linus Torvalds,  Linux 5.5-rc3")<br/>
1. [Linus Torvalds,  Linux 5.5-rc6](https://lwn.net/Articles/809255/ "Linus Torvalds,  Linux 5.5-rc6")<br/>
1. [Linus Torvalds,  Linux 5.5-rc7](https://lwn.net/Articles/810011/ "Linus Torvalds,  Linux 5.5-rc7")<br/>
1. [Linus Torvalds,  Linux 5.5-final](https://lwn.net/Articles/810579/ "Linus Torvalds,  Linux 5.5-final")<br/>
{: .citation .bracketsAround .decimal}

[devWG glossary]: https://docs.google.com/document/d/1d91Znr2IWPI3pgDk_Nz2BcVNWHQgyBxk_18dAqnskiw/edit?usp=sharing. "Kernel Development Process WG Glossary"
[gnu v2.0]: https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html "GPL 2.0 License"
[linus 5.5-rc1]: https://lwn.net/Articles/806771 "Linus Torvalds,  Linux 5.5-rc1"
[linus 5.5-rc2]: https://lwn.net/Articles/807349 "Linus Torvalds,  Linux 5.5-rc1"
[linus 5.5-rc3]: https://lwn.net/Articles/808000 "Linus Torvalds,  Linux 5.5-rc1"
[linus 5.5-rc6]: https://lwn.net/Articles/809255 "Linus Torvalds,  Linux 5.5-rc1"
[linus 5.5-rc7]: https://lwn.net/Articles/810011 "Linus Torvalds,  Linux 5.5-rc1"
[linus 5.5-final]: https://lwn.net/Articles/810579 "Linus Torvalds,  Linux 5.5-final"

### E-Mail Thread

1. <https://lists.elisa.tech/g/development-process/message/200>
1. <https://lists.elisa.tech/g/development-process/message/214>
1. <https://lists.elisa.tech/g/development-process/message/216>
1. <https://lists.elisa.tech/g/development-process/message/217>
1. <https://lists.elisa.tech/g/development-process/message/218>
1. <https://lists.elisa.tech/g/development-process/message/222>
1. <https://lists.elisa.tech/g/development-process/message/223>
1. <https://lists.elisa.tech/g/development-process/message/225>
1. <https://lists.elisa.tech/g/development-process/message/226>
1. <https://lists.elisa.tech/g/development-process/message/227>
1. <https://lists.elisa.tech/g/development-process/message/228>
1. <https://lists.elisa.tech/g/development-process/message/229>
1. <https://lists.elisa.tech/g/development-process/message/230>
1. <https://lists.elisa.tech/g/development-process/message/234>
1. <https://lists.elisa.tech/g/development-process/message/239>
1. <https://lists.elisa.tech/g/development-process/message/243>
1. <https://lists.elisa.tech/g/development-process/message/245>
1. <https://lists.elisa.tech/g/development-process/message/246>
1. <https://lists.elisa.tech/g/development-process/message/247>
1. <https://lists.elisa.tech/g/development-process/message/248>
1. <https://lists.elisa.tech/g/development-process/message/250>
1. <https://lists.elisa.tech/g/development-process/message/252>
1. <https://lists.elisa.tech/g/development-process/message/253>
1. <https://lists.elisa.tech/g/development-process/message/256>
1. <https://lists.elisa.tech/g/development-process/message/260>
1. <https://lists.elisa.tech/g/development-process/message/267>
1. <https://lists.elisa.tech/g/development-process/message/269>
1. <https://lists.elisa.tech/g/development-process/message/340>
1. <https://lists.elisa.tech/g/development-process/message/592>
{: .citation .bracketsAround .decimal}

## References

None, at the moment.

*[OTS]: Off the shelf
*[OS]: Operating System
