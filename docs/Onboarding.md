---
layout: default
title: An Introduction to ELISA
description: Discussion papers related to the Linux Foundation ELISA Project
---
> This paper introduces the ELISA project and identifies central challenges
> that any safety-critical project using Linux needs to overcome.
> It presents our analysis of the challenges,
> outlines long and short term plans on how to overcome them in the framework of the ELISA group and finally,
> presents a collection of open building blocks that will emerge from those activities
> for reuse in safety-critical development projects using Linux.

## The Problem at Hand and Normative Considerations

Current safety standards have targeted systems which have low-complexity application software,
which do not use hardware concurrency (e.g. multicore processors),
and which use pre-existing and open-source software to a very limited extent. 
Hence, various domain safety standards (
[\[ISO 26262\]](#iso26262){: target="_self"},
[\[IEC 62304\]](#iec62304){: target="_self"},
[\[DIN/EN50128\]](#dinen51208){: target="_self"},
...)
do not consider pre-existing complex elements,
such as Linux and glibc, running on complex multi-core hardware. 
For example, ISO 26262 has no appropriate classification of Linux, which is a “pre-existing software  (Part 8-12).” 
But Linux continues to evolve and Part 8-12 applies only to unchanged SWCs (See ISO 26262-2 6-7.4.7). 
This specific mismatch already indicates that the ISO 26262 committee did not consider Linux-based systems.

John: A long, labourious, detailed, picky and totally irrelevant comment that only serves to fill space
and see if the text wraps a line.
{: .comment}

An example of the cultural mismatch between the methodology expected by safety
standards and the open-source work methodology 
is how change is handled: very conservative change management vs. encouraging dynamic change.
Hence, ISO 26262 fits poorly in that respect as well.

Therefore, a adjusted interpretation for open-source software is required,
either by interpreting IEC 61508 or by deriving a new domain standard,
e.g. extracting objectives from first principles and determining which adjusted
measures and techniques provide sufficient evidence of safety.

As a Linux-based system is by definition a mixed-criticality system with parts
classified as QM/SIL0 and others with safety classification,
there must be a clear definition and criteria for evalutating QM/SIL0 elements.
Lack of a definition of QM/SIL0 in the safety standards, e.g. ISO 26262 and IEC 61508,
has already led to some confusion.

Some safety standards do not provide rationales,
which limits the ability to interpret the objectives of the requirements without violating the intent.
Last but not least, the standards are closed.
This hinders their acquisition, use and acceptance in the open-source community

On the other side, open source projects frequently lack a formal description of
the development process they follow (safety plan) and explicit trace data between
the artefacts produced in each development phase (safety case).

To enable Linux to be incorporated in safety-critical systems,
the gap between the activities practiced in open source project 
and those required by safety standards needs to be precisely analysed
at both the technical and process levels.

All issues must either be mitigated by organisations using Linux or addressed by
process improvements on the Kernel development side.

# ELISA Strategy and Organization
This section describes the cornerstones of the ELISA strategy to enable Linux in safety applications and
the organizational structure of the ELISA effort.

## Working Groups

Currently ELISA has 5 working groups.
Their presence is spread over a convoluted combination of 
[ELISA Tech][elisa tech], [ELISA GDrive][elisa gdrive] and [ELISA GitHub][elisa github]
sites.
There are also a number of overarching subgroups.

### ELISA Tech WG
The Tech working group discusses overarching technical and organisational issues and supporty the TSC in this direction.
It holds bi-weekly telcos where the general public is invited to participate and where the TSC members are obligated to participate.
#### Technical Strategy Committee (TSC)
TBD
{: .todo}

### Automotive WG
TBD
{: .todo}

### Development Process WG
TBD
{: .todo}

#### Tool Investigation and Code Improvement SG
TBD
{: .todo}

### Medical Devices WG
TBD
{: .todo}

### Safety Architecture WG
TBD
{: .todo}

### ELISA Ambassadors SG
TBD
{: .todo}

### Ontology SG
TBD
{: .todo}

## Increasing Rigour Strategy
Due to the immense complexity and huge deviations from traditional V-model style
development processes as outlined in safety standards,
it makes sense to build from the bottom up and follow an increasingly rigourous approach:

This strategy pertains to all areas, including but not limited to:

**Standards**

* ISO/IEC 33000 series of standards [\[ISO 3300x\]](#iso3300x){: target="_self"}, [CMMI][cmmi], [ASPICE][aspice]
* [\[UL1998\]](#ul1998){: target="_self"}
* [\[ISO 9001\]](#iso9001){: target="_self"}
* [\[IEC 61508\]](#iec61508){: target="_self"} / [\[ISO 26262\]](#iso26262){: target="_self"}

As QM software development is a basic requirement for developing any good quality software and
to eliminate systematic faults to achieve safety, the approach can be to start small 
i.e, show that LINUX development meets the requirements of a basic software development process 
(e.g. ISO/IEC 33000 series of standards
[\[ISO 3300x\]](#iso3300x){: target="_self"}
Capability Maturity Model Integration (CMMI) (see [CMMI][cmmi])
or Automotive SPICE (see  [ASPICE][aspice]).
Once this is achieved the requirements of 
[\[UL 1998\]](#ul1998){: target="_self"}
(less rigorous requirements compared to IEC 61508 / ISO 26262) can be added, 
followed by requirements from 
[\[IEC 61508\]](#iec61508){: target="_self"}
and 
[\[ISO 26262\]](#iso26262){: target="_self"}

**Safety Claims**
ELISA will work on safety claims of increasing complexity.
The work will start with low complexity Linux based safety relevant systems 
which have no strict timing/performance requirements,
such as In Vehicle Infotainment (IVI) systems,
as opposed to most safety relevant automotive systems.
Once a satisfactory safety argumentation for simple example systems is found and documented,
it can be expanded to more complex systems.

**Architectures**
Aligned with the increasing rigor approach,
ELISA targets architectures of increasing complexity to keep the scope as limited as possible at first,
expanding to more complex architectures later on.

ToDo: Need examples.
This needs to address partitioning architectural measures, i.e. separate processor, hypervisor, AMP, etc.
{: .todo}

**POSIX API Levels / Application environment profiles**
There are several, increasingly complex standards that specify application interfaces that could be
used in safety-critical systems.
Only the safety-critical interfaces of the operating system must be certified according to safety standards.
The effort required to certify as system using Linux could therefore be reduced by
limiting the scope of the calls an application makes to the operating system.

The standards form the following hierarchy:

* PSE51
* PSE52
* PSE53
* PSE54
* Full POSIX
* LSB

The POSIX standard
[\[POSIX\]](#posix){: target="_self"}
outlines in part 13
[\[PSE5x\]](#pse5x){: target="_self"}
application environment profiles (Effectively minimal subsets of the POSIX APIs
required for typical realtime applications) in rising complexities.
Linux' API is a superset of the full POSIX standard and is specified as
[LSB: the Linux Standard Base][lsb]

```
ToDo: Disconnected inherited text of unknown origin :
	Propose liason process (like DO-178)
	Define SIL0/QM (ref: Clause 7-X  formalization as starting point)
	Qualify “convincing” parts of the examples  
```
{: .todo}

## Develop Safety Argumentation

### Process - Tailoring and Equivalence Argumentation

Since full compliance with any of the safety standards cannot be argued for the Kernel development process at the moment,
nor is it realistic to expect this to change in the near future,
an equivalence argumentation must be used to argue suitability of the Linux Kernel for safety application.
To that end, it is necessary to map terms and processes of the Kernel development to the corresponding
steps in the V- process of the safety standards
and find equivalence arguments as to why the Kernel development process fulfills the intention
behind the requirements of the safety standards.
<!--
  To close the interpretation gap it is necessary to map terms and processes to each other
  Identify rationales in the safety standards (domain specific or IEC 61508)
  Tailoring the safety standards according to the rationale
-->

This heavy tailoring/modification (beyond what is outlined within the safety standards as tailoring),
requires a systematic approach to achieve confidence in the tailoring arguments.
Such a methodology (including practical application examples) has already been developed for
tailoring of IEC 61508 within the SIL2LinuxMP project (see [Annex QR][annexQR]).

If such an argument cannot be made, a gap exists that has to be addressed by
modifying and or extending the Linux Kernel development process.

Once this tailoring has been outlined, ideally even earlier,
certification authorities should be brought to the table to make sure the argumentation
is acceptable from their perspective.
Annex QR was originally intended to be included into IEC 61508.
In the event that this happens in a future edition of the standard,
the described argumentation would then even be fully compliant.

This topic is addressed by the 
[development process working group](#development-process-wg){: target="_self"}

### Example Use Cases

The core of ELISA strategy is to exercise the construction of safety argumentation at the example of several use cases,
which then can be used as blueprints for further projects.
Analyzing use cases is crucial

* to stimulate the properties of Linux that need to have a safety capability and to allocate appropriate integrity levels,
* to introduce usecase-specific constraints/requirements for Linux without trivialising the utilisation of Linux,
* to use examples to advance certification capability from concrete implementations towards generic usecases,
since as we understand it Linux has not been certified in an application agnostic way,
* as a basis for applying open source methods and tools to establish a body of knowledge,
supporting the creation of critical products and systems based on Linux,
* as a destination for experimenting with software and designs in a safety-relevant context,
* as a means of attracting contributors into the ELISA community.

Beyond the two use cases already under consideration (
*\ref{sssec:OpenAPS}*{: .todo}
and
*\ref{sssec:OpenAPS} John: which one is this?*{: .todo},
a cooperation with AGL (Automotive Grade Linux) is currently being established
providing a third use case related to the IVI use case.

Steps:

* identify sources of usecases
* existing open source initiatives (eg Apollo/Autoware)
* proposed by sponsors
* classical safety architectures
* evaluate and score potential usecases
* select actual usecase(s)
* get started on usecases
* refinement
* scoping work
* Implementation (code examples, tools, and libraries)
* evidence evaluation
* See <https://github.com/elisa-tech/workgroups/issues/8>
* See <https://github.com/elisa-tech/workgroups/issues/9>
* See <https://github.com/elisa-tech/workgroups/issues/10>


The following sections go into more detail on the two use cases currently under investigation by the ELISA group.

**OpenAPS**
The OpenAPS project develops an artificial pancreas System to control insulin pumps.

**IVI**
The in vehicle Infotainment.

## Develop Open Building Blocks
The results of the ELISA activities is a collection of reusable building blocks and
instructions/examples on how to use them to construct safety argumentation for Linux-based systems.

## Marketing and Recruitment
The problem now is getting acceptance and formal approval that Linux is suitable
for use in safety-critical systems and applications.
We need to shift the focus to the idea that the whole system is safe and sane.
The end result has to be safe, not just that a form has been filled out.
Developers, safety experts and regulatory authorities all share the same goal of
wanting to make the world a safer place.
But safety experts and regulatory authorities have a visible gap of knowledge
in dealing with open source software, 
let alone community-based development, highly automated and newer development methodologies.
Also, open source developers often don’t understand best practices for designing
their software to be suitable for use in safety-critical systems.
Linux is already pervasive in our ecosystems as well as our devices 
and will be used even more in future, 
so Linux is a shared point of interest for the Linux and Safety communities.   

We need to reach out to both of these communities and get them talking
to another in order to bridge the gaps.
This will require marketing-related activities to raise awareness 
and motivate involvement that aligns with their interests.
Once they are engaged, this needs to be a community that they 
see as beneficial and enjoyable to participate in. 

To that end, the next step is the creation of educational, best practice and marketing material.
The gold deck can be used to explain the problem and need for participants:

* Pain problems
* Use Cases for ELISA
  * Medical equipment
  * Industry automation
  * Autonomous systems (vehicle, factories, robots)
* Why use Linux?
  * New technologies
  * No licensing fees
  * Total cost over life-cycle
* Wider community to draw on for security issues.
* ELISA builds a wider community focused on safety issues

AI:  Kate to take first pass; Nicole, Nicholas, Olaf to review.
{: .todo}

### How do we want to communicate?
* Good website (What content do we want to add?)
* What we have to offer
* Reasons to engage
* Areas to engage
* Perspectives to bring to play: We need people to have vision here, and willing to review
* Domain content
* Clear instructions on how to engage with workgroups of interest
* Standard LF code of conduct,  respect for individuals applies
* Social media engagement to raise awareness 
on a regular cadence of communication twitter channel
(need specific to ELISA)
* Use for frequent communication of events relative to community
* Public thanks for contribution are motivating for people
* Set up FLOCK for ELISA
* Free version available
* Selective licensing of individuals **investigate**
* LinkedIn for more technically-related related content
* (Whitepapers, content, press releases) Target 2 press releases a year
* Taget conferences to reach out to:
  * Embedded World Nuremberg
  * VDA Automotive SYS - annual meetup, by safety and security people.  (OpenSource)
  * VDI - IEEE in German,  engineering community and some safety
  * Bitcom - lobbying organization in Germany,  digitalization,  open source in sept,  smart,  hub conference in Berlin
  * OSS - LF events- Safety
  * Safetronic (other) or Safetech (TUEV SUED)
* Enable ambassadors for the project to speak at conferences/events/in-house/executives 
* Information material to help ambassadors (reference material online, including slides to walk through, whitepapers for offline reading)
	* Provide feedback to Kate on Gold Deck.
	* Outreach to media (once content is created),  classic press releases.
	* Trigger news sites to pick up.
	* Electronic Net newsletter,  headlines.

AI Nicole: Outreach to Bitkom Forum:  Provide overview at next working group meeting.
{: .todo}

### Strategies needed to build up organic communities,  rallying points

* Outreach to target participants for solving this.
	* Open Source Developers 
	* Safety Experts
	* Regulatory Authorities
	* Open Source Users 
	* Professional OEM:  EE systems like  Car Makers, Device Makers, Robot Makers, etc…)
	* Hobbyists with personal need:  \# OpenAPS codes
	* Academics interested in helping to solve hard problems
* Articulate the compelling rallying points to 
	* academics (hard problems), 
	* Hobbyists (personal interests),
	* commercial(safe products)    
* Create an open topic list of unsolved problems.  
* Grab your own problems:
* Topics that are safety relevant.    
* Get more people to contribute to papers,
3 or 4 people contributing - matching communication between industry review for academic research. 
* Interesting use cases are important. 

### Initial Thoughts
* Visible for customers, users and ones who might want to engage
* We want contributors and sponsors
* Want to bring right stakeholders to the discussions
* Car makers - not spending on licensing fees, but making Linux capable
* Certification companies engaged - part of handshake
* Approval that the whole system is safe and sane
* Be sure for self
* Want to make the world is a safer place - certification and developers both want same goal
* Knowledge of safety and technical properties of system you want to evaluate
* Gap of knowledge in dealing with software in safety domain,  let alone open source, community based development,  highly automated and newer development methodologies
* Developers building system want to make sure they are doing the right thing
* Want to avoid harm to people
* Did everyone do their job correctly?
* Informed and educated
* We have enough good experts working on this
* The person asked needs to know technical properties of system,  not just the contents of a filled out form
* End result has to be safe,  not just that a form has been filled out
* Formal safety process and standard are only a minimum,  
and blind reliance in standards, does not necessarily create a safe system.
* Linux is pervasive in our ecosystem and our devices already,
and will be more use in future
* Server farms with Linux uptimes are so much better than alternatives.   
* Problem now is getting acceptance and formal approval that Linux is suitable to be used in these safety-critical systems and applications 

# OSS-Specific Challenges
This section presents the major challenges ELISA faces.
The following section presents how they are being addressed.

## Updates and Change
Today, the majority of existing certified safety-related products 
are not updated in the field.
This is driven by the fact 
that reassessment of a safety-critical system is a time-consuming and complex process.
Products are developed to avoid hazards with sufficient level of confidence and
incremental changes are therefore seldom foreseen.
Safety (or security) updates necessary after development ends come with additional costs and risks, 
while their safety (and security) benefits are typically rated low and beyond an acceptable level.
Hence, in the end, optional or deferred updates are argued to be flawless and complete.
Also, existing infrastructure typically does not allow field updates over the air, 
which further increases the costs for potential updates. 

However, in contrast to traditional devices 
(e.g., an airbag ECU) 
nowadays everything else is being connected.
Cloud services are being introduced to all areas of life
with correspondingly increased risks of cyber attacks,
especially attacks involving system- and chipset-level exploits 
such as  Spectre/Meltdown/Rowhammer. 

To prevent security breaches, it is becoming mandatory 
to release updates within one day of publication, 
This contrasts strongly with current safety accreditation timeframes.
This is not only a problem limited to open source software or Linux, 
but is a principal challenge for all products
providing services in a connected world,
including the commercial proprietary ones.

In connected settings every unpatched system must be considered insecure. 
The same holds true with respect to functional safety 
for systems compromised by security vulnerabilities.

To conclude, updates are therefore a major challenge for connected safety-critical systems in general.


## Bug tracking
All OSS projects 
beyond a rudimentary maturity level 
have a bug tracking system.
However the bug tracking systms are only effective to a certain extent.
Tracking bugs is not the most rewarding or prestigious work and 
correspondingly there is always a shortage of volunteers.
Furthermore, depending on the bug tracking and the open source community, 
low quality bug reports are an issue that further increases
the work load without any gain for the project in question.
This is not so much a problem for the Kernel bug tracker
<span class="todo">[reference] </span>
but for the distributions downstream, (see the
[short and long-term solutions section](#bug-tracking-1){: target="_self"})
which absorb the bulk of low quality bug reports.

From a safety perspective, 
ignoring bug reports is not acceptable, however. 
A solution must therefore be found to organize bug reporting and tracking in such a way that is manageable.

## Regression tracking
A problem related to bug tracking is regression tracking, 
i.e. tracking bugs discovered after 
a version (i.e. an LTS kernel version) has been released
which exist in that version
and 
must fixed nonetheless.

While this is a general problem for LTS maintainers,
if the version is being used in a safety critical system, 
the developers must at least be aware that the bug exists.
Should the bug impact the safety integrity of the system, 
the fixes must be back-ported to the release branch for the safety-critical item, 
A safety impact analysis must be done and it may reveal that further mitigation measures are necessary..

## Freedom from Interference - Kernel Model
On the technical side, we need to understand better which safety claims can be made for the Linux kernel, 
and how to insulate against interference. 
This topic touches all use case working groups and the
[architecture working group](#safety-architecture-wg){: target="_self"}.
To create a Kernel model of sufficient granularity, 
several code analysis based approaches are being investigated in the
[tool investigation and code improvement sg](#tool-investigation-and-code-improvement-sg){: target="_self"}

## Linux Development Process Analysis
A big challenge is to argue the aforementioned equivalence with
the conventional development processes envisaged by the safety standards 

# Overcoming the Challenges
This section presents our plan to overcome the challenges outlined in the 
[OSS specific challenges](#oss-specific-challenges){: target="_self"}
section

## Updates and Change
As outlined in
[Updates and Change challenge description](#updates-and-change){: target="_self"}
timely updates are a major issue.
ELISA is working towards short and long term solutions as follows.

### Short term strategy
As a first step to close this gap, 
the solution concept has to be judged in a constrained environment (e.g a specific use case or subsystem).
In this way the solution's overall feasibility and its reception in safety community can be checked.
The potential of state-of-the-art update policies in security-critical systems and DevOps operations 
to increase software quality should be also be checked in parallel.
Emphasis should be placed on understanding which concepts affect reliability and stability.
An additional strategy is to discuss these ideas with proprietary software providers
as they must tackle the update challenge as well.

### Long term strategy
As a starting point to approach system updates,
the underlying software has to be arguably safe.

One way to reduce the effort of impact analysis and changes 
is to partition the system up-front and support the partitioning with a
freedom from interference argument for the non-safety-relevant parts.
This assumes that even 
when there are frequent changes to the complete software stack, 
the impact to safety relevant parts are minimised and become manageable. 

Nevertheless, for complex software like the Linux kernel,
a structured path during analysis and verification 
needs to be established and supported by automation.
An initial approach in this direction
could be analysing existing update policies 
which have hard requirements on system stability (e.g. for a Linux server) 
and DevOps approaches to improving product quality. 
Formalized classification of the type of change 
with respect to functionality or security fixes or new or updated functionality 
would help to identify the impact of the changes.
Each type may require different actions, 
but should not impact the overall process and strategy of updating a safety-critical system product. 
Investing in careful analysis will result in shorter verification cycles.
 
For the matter of completeness, not only software is subject to change and update,
but also the underlying tools (e.g. compiler or deployment tools). 
A common method of tool qualification includes testing the tool according to its use cases. 
It is assumed that a security or bug fix will not have impact to the tool's use cases and 
the tool qualification suite can be re-executed. 
In contrast to deployed product software, 
the tools' feature sets and use cases can be narrowed down to a limited set. 
This means that the approach towards tool updates most likely differs to the approach to updating product software in the field.

As the whole proposal for software update (e.g. in the field of security update of connected devices) 
is not yet sufficiently reflected in safety standards,
close collaboration with standardization authorities and safety community 
will be required to make fast software updates state of the art.
## Bug tracking

### Short term strategy

### Long term strategy
The downstream companies which build safety applications using the Linux kernel must have their own bug tracking systems.
These systems would be less prone to being flooded with irrelevant entries and 
the companies would have a strong incentive to fix the bugs and also bring the fixes upstream. 
Ignoring the existence of possibly safety-relevant bugs is not acceptable from a safety perspective 
unless a solid mitigation mechanism and corresponding rationale for doing so can be developed.

## Regression tracking

### Short term strategy

### Long term strategy}  

## Freedom from Interference - Kernel Model
ELISA is currently focusing its activities in the context of two use cases IVI and OpenAPS to understand
* the system's safety requirements that are allocated to the Kernel
* the impact an incorrectly functioning Kernel has on the safety claim itself 
The following assumptions have been made at the start of the investigations:

* 	Only certain functional layers of the Linux kernel are used for the specific use case. 
* 	It is possible to trace the Kernel functional layers used for the specific use case.
*   Those layers are a small subset of the entire Kernel architecture space..

If the above assumptions can be validated,
the "criteria for coexistence” as defined in ISO 26262 
could be used to demonstrate freedom from interference between
the safety-related and non-safety-related kernel functionalities
and isolate the safety functionality allocated to the Kernel. 
This reduces the scope of Linux that must be qualified.

### Short term strategy

*	Identify appropriate methodologies or tools which could be used to trace the control paths in the Kernel 
*	Identify safety-related and non-safety-related parts of the kernel for the specific use-case

### Long term strategy

*	Systematically identify the various interfaces between the safety-related and non-safety-related parts of the Kernel that could impact the safety functionality allocated to the kernel.
*	Prove that the interaction between the non-safety-related Kernel and the safety-related Kernel functions does not hinder the safety functionality

## Linux Development Process Analysis QM

### Short term strategy

* Audit process compliance in current development, 
* Talk to assessors about strategy
* ISO 9001 compliance route

### Long term strategy

* statistical analysis of mailing lists

# Open Building Blocks

## Problem Statement

Determining reference system architecture and understanding Kernel configuration for the use case

Linux is huge and understanding the configuration for example,
defining the scope of Linux Kernel to features based on the selected reference use case is key. 
While defining the configurations the following should be considered
i.e interfaces (APIs, power management), shared resources (system timer, PTP (Precision Time Protocol). 

A decision must also be made on whether the idea is to work towards a 
<span class="todo">ToDo: text lost here.</span>.

## Education and Best Practices Material

Currently, the awareness of safety in the wider open source community is poor . 
The  community is usually not aware of functional safety and related concepts. 
Most safety development guidelines are behind a closed curtain (not public domain)
and there are no public examples for functional safety systems.

To enable the ELISA community, the following materials are being created:

### Safety ‘101’ book

This introduction to functional safety for OSS developers gives an overview of the topic,
containing the following topics:

* What is Functional Safety (1 page ideally, no more than 5)
* Basic worked example that people can readily understand (e.g. train door)
* Specific system (e.g. Raspberry Pi) and context
* Identify possible hazards and losses
* Illustrate some chain of argumentation to be taken to make safe
* Introduce distinction between safety and security, and
mention things that are outside the safety context (e.g. reliability, robustness)
* Identify some common types of solution or safety strategies
* Perhaps Include a set of questions?
* Summarise concepts such as fail-safe and common strategies 
* Introduce standards and processes, avoid too much detail
* Reference to the specific standards and where /
if you can see them (or a more detailed summary / discussion)
* Plan for expert and non-expert readability review


### Open source ‘101’ for safety people

This introduction to OSS gives safety engineers, architects and legal people an overview of
open source software, the process by which it is developed and
how it differs from traditional software development as it is know in industry projects.

### Best practices for open source projects

* “Safety conscious” badge: considering safety as part of a project’s goals
* Identify a list of things that are used to build a safety argument that tend to be missing from open source projects
* Build on processes and principles that will be familiar to open source developers
* Template for patches to extract requirements e.g. Coding Guidelines, Coding review templates
* Understand how security considerations can also be applied to safety
* Show how “good” code fulfills the safety guidelines - “common sense” approach to safety
* One or more worked examples of systems using the solution
* Encourage consumers of a project to document how it is used in a particular situation
* Recruit some open source projects to try to apply these best practices and identify additional / alternative ideas

### Competition

* Come up with a safety use case for a Linux / open source project
* Linux Foundation will sponsor a ‘straw man’ pre-qualification project
* Gold badge and title!


## Kernel Dependency Analysis Tool

## Linux Kernel Model

To understand and systematically collect all plausible sources of interference that have
the potential to influence an application,
we need to get a thorough understanding of all the steps an application passes through
in its life cycle from startup to termination. 
In combination with shared resources,
a clearer picture should emerge on what can interfere with an application.

**Strategy towards a solution:**
Mapping the steps an application lives through at the example of a simple application
along with creating/identifying a model of what happens with Applications and the Kernel.  


## Tailoring techniques - Annex QR


## Managing artifacts for certification - PMT

## Linux and Quality Management

Quality management is the foundation on which all safety integrity is built.
Therefore the process by which the Linux Kernel is developed has to be completely
understood in oreder to make an equivalence argument towards Quality Management as it is
codified in QM standards such as ISO 9001.

**Strategy towards a solution**
Analogously to the route.pdf for the qualification argument, ISO 9001 should be read
and innterpreted in the context of the Linux development process.
Gaps should be identified and then rationalized or closed by extending the Process.

# Conclusion

TBD
{: .todo}

# Links

1. [Annex QR](https://sil2.osadl.org/user/data/SIL2LinuxMP/doc/other/AnnexQR/AnnexQR.pdf "Annex QR")
2. [ASPICE](http://www.automotivespice.com/ "Automotive SPICE")
2. [CMMI](https://cmmiinstitute.com/ "Capability Maturity Model")
2. [ELISA: ELISA tech](https://elisa.tech/ "ELISA - Advancing Open Source Safety-Critical Systems - ELISA")
2. [ELISA: GDrive](https://drive.google.com/drive/folders/1Y6Uwqt5VEDEZjpRe0CBCIibdtXPgDwlG "Technical Community - Google Drive")
2. [ELISA: GitHub](https://github.com/elisa-tech/workgroups "GitHub - elisa-tech/workgroups: Coordination between ELISA working groups, and repository for documentation based deliverables.")
2. [LSB](https://refspecs.linuxfoundation.org/lsb.shtml "Linux Foundation LSB Specification")


[annexQR]: https://sil2.osadl.org/user/data/SIL2LinuxMP/doc/other/AnnexQR/AnnexQR.pdf "Annex QR"
[aspice]: http://www.automotivespice.com/ "ASPICE"
[cmmi]: https://cmmiinstitute.com/ "Capability Maturity Model"
[elisa tech]: https://elisa.tech/ "ELISA - Advancing Open Source Safety-Critical Systems - ELISA"
[elisa gdrive]: https://drive.google.com/drive/folders/1Y6Uwqt5VEDEZjpRe0CBCIibdtXPgDwlG "Technical Community - Google Drive"
[elisa github]: https://github.com/elisa-tech/workgroups "GitHub - elisa-tech/workgroups: Coordination between ELISA working groups, and repository for documentation based deliverables."
[lsb]: https://refspecs.linuxfoundation.org/lsb.shtml "Linux Foundation LSB Specification"

# References

*[DIN 51028:2012]*{: #dinen51208}
:	**Bahnanwendungen - Telekomunikationstechnik, Signaltechnik und Datenverarbeitungssysteme -
	Software für Eisenbahnsteuerungs- und Überwachungssysteme**.
	Standard, 
	DIN Deutsches Institut für Normung E.V., March 2012

*[IEC 61508:2010]*{: #iec61508}
:	**Functional safety of electrical/electronic/programmable electronic safety-related systems**.
	Standard,
	IEC International Electrotechnical Commission,
	April 2010.

*[IEC 62304:2015]*{: #iec62304}
:	**Medical device software - 
	Software life cycle processes**.
	Standard,
	IEC/SC 62A Allgemeine Bestimmungen für elektrische Einrichtungen in medizinischer Anwendung,
	June 2015

*[IEEE POSIX:2017]*{: #posix}
:	**IEEE Standard for Information Technology -
	Portable Operating System Interface (POSIX(R)) Base Specifications**.
	Standard,
	IEEE The Institue of Electrical and Electronic Engineers,
	January 2017

*[IEEE PSE5x:2003]*{: #pse5x}
:	**Information Technology -
	Standardized application environment profile (AEP) -
	POSIX(R) realtime and embedded application support**.
	Standard,
	IEEE The Institute of Electrical and Electronic Engineers,
	January 2003

*[ISO 26262:2018]*{: #iso26262}
: 	**Road Vehicles - Functional safety**.
	Standard,
	International Organiszation for Standardization,
	Geneva, CH, December 2012
	
*[ISO 3300x:2015]*{: #iso3300x}
:	**Information Technology. Process Assessment**.
	Standard,
	ISO/IEC JTC 1/SC 7 Software and Systems Engineering,
	March 2015
	
*[ISO 9001:2015]*{: #iso9001}
:	**Quality management systems - 
	Requirements (ISO 9001:2015);
	German and English version
	EN ISO 9001:2015**.
	Standard,
	DIN-Normenausschusss Qualitätsmanagement, Statistik und Zertifizierungsgrundlagen (NQSZ),
	November 2015
	
*[UL 1998:2018]*{: #ul1998}
:	**Software in programmable components**.
	Standard,
	UL llc,
	September 2018

# Appendices

## License

Very unclear w.r.t. publication, what to do.

## Document History

| Version | Author | Changes |
| ------: | ------ | ------ |
| 0.1 | ELISA Group | Transferred from Google docs to LaTeX |
|  |  | Restructured Document |
|  |  | Added short term/ long term sections |
| 0.2 | ELISA Group | Transferred from LaTeX to markdown |

