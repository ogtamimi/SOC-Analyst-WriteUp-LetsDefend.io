# LECTURE2: Cyber Kill Chain
## 1) Introduction to Cyber Kill Chain


### Which organization was the Cyber Kill Chain model developed by?
> **ANSWER: Lockheed Martin**
### In what year was the organization that developed the Cyber Kill Chain model founded?
> **ANSWER: 1995**
### In what year was the Cyber Kill Chain model developed?
> **ANSWER: 2011**

## 2) Cyber Kill Chain Steps

```
There are several actions that an attacker can take before, during, and after a successful cyber attack. These actions are sequential, and if the attacker fails at one stage, it is not possible to execute the next step of the cyber attack. The Cyber Kill Chain model divides these stages of attackers into 7 steps. The steps of cyber attacks are depicted in the visual  below:

1.Reconnaissance
2.Weaponization
3.Delivery
4.Exploitation
5.Installation
6.Command & Control (C2)
7.Actions on Objectives

```
### How many steps does the Cyber Kill Chain model consist of?
> **ANSWER: 7**

## 3) Reconnaissance

```
The term "Passive Reconnaissance" refers to the collecting of information from sources about the target system without physically engaging with the target system. As an instance of this, Web archive websites can be used to obtain information that is no longer available on the target system's website.

"Active Reconnaissance" refers to the method of acquiring information about a target system by engaging with it directly. By submitting a request to a web server, for instance, version information about the web server may be acquired from the response.

```


The attacker can gather information from a variety of sources using a variety of approaches during the "Reconnaissance" process. At this phase, the attacker can perform the following operations:

* Obtaining version information of servers and software belonging to the target
* Obtaining information from open sources of information about the target has previously been released
* Obtaining e-mail addresses of employees of the organization
* Obtaining internal or personal information about employees of the organization using social networking platforms
* Detection of devices that are connected to the Internet
* Detection of security vulnerabilities on servers open to access on the Internet
* Identifying the IP address block belonging to the organization
* Identification of vendors that the organization cooperates with

### What is the step in the Cyber Kill Chain model where the information gathering takes place?
> **ANSWER: Reconnaissance**

###  The Real-life attack Scenario items above explain an aspect of an actual cyber attack. Based solely on this information, what is the number of distinct actions taken during the "Reconnaissance" phase, which is the first step of the Cyber Kill Chain?
> **ANSWER: 3**

## 3) Weaponization

```
The "Weaponization" is the second step in the Cyber Kill Chain. 
At this stage, the attacker uses the information obtained in the previous stage to access the tools needed for the attack or develops the tool/script directly.
At this stage, preparation for a cyber-attack may differ depending on the sort of attack. 
For example, if a phishing-type cyber attack is to be carried out,
an exploit can be constructed in response to a recognized security vulnerability, or malicious email content can be generated.
If the tools for the cyber attack are ready, the attacker completes this phase quickly and moves on to the next phase of the cyber attack.
At this point, the attack has not yet commenced, and the victim is generally unaware of the attacker.

```
### How many separate activities were performed in the "Weaponization" phase, the second step of the Cyber Kill Chain, according to the Attack Scenario items above?
> **ANSWER: 2**


## 4) Delivery

```
The third step of the Cyber Kill Chain is the "Delivery" stage.
At this stage, the attacker executes the cyber attack that he prepared for in the preceding phases. 
This is the stage where the first interaction with the victim happens. For instance, malware is uploaded to the proper environment at this step, and the victim downloads the malware from the uploaded environment to their systems. Malicious content can be conveyed to the victims' devices in various ways during the delivery phase.
The methods used for delivering malicious content may differ depending on the type of attack. For instance, using email for a phishing attack may be preferred, or the malicious content in the email can be uploaded to a web address.
```
### According to the Attack Scenario items above, how many different actions were performed in the "Delivery" phase, the third step of the Cyber Kill Chain?
> **ANSWER: 2**
### How many separate activities were performed in the "Weaponization" phase, the second step of the Cyber Kill Chain, according to the Attack Scenario items above?
> **ANSWER: 2**

## 5) Exploitation

The attacker has some basic knowledge about the program or system intended to be exploited in the target and has prepared the appropriate attack tools beforehand in the "Exploitation" stage. This is the step the attacker's exploit or tool is run/tested. This step may be failed if the exploit or tool is not suitable to be utilized on the victim's system. At this level, the attacker can perform the following operations:

* Executing the exploit that exploits the hardware vulnerability
* Executing the exploit that exploits the vulnerability of the software or operating system
* Running malware

> **ANSWER: CHECK**

## 6) Installation

```
The fifth phase of the Cyber Kill Chain is the "Installation" phase.
At this stage, the attacker attempts to maintain persistence on the target system that was exploited. 
The attacker attempts to gain an access path that can be accessed at any time by installing a backdoor on the system. 
Because the exploited vulnerability will be patched and rendered inoperable after a certain time, 
the attacker must use a different method to gain access to the target system. 
At this point, the malware to be installed on the target device can alternatively 
be placed with the help of a dropper. At this point, the attacker may attempt to acquire access 
to a highly authorized user account in the system via privilege escalation tactics in order to assure system persistence.
This is the stage at which attack preparations are carried out to achieve the ultimate aims once the cyber attack has begun.
```
### According to the detection scenario above, in which step of the Cyber Kill Chain did the attacker fail, leading to the detection of the attack?
> **ANSER: 4**

## 7) Command and Control (C2)
> The attacker can send remote commands to the system and execute them at this step.

### According to the scenario above, what is the final Cyber Kill Chain step in which the attacker succeeded?
> **ANSER: 6**


## 8) Actions on Objectives

### At what stage of the Cyber Kill Chain did the APT group "Cobalt Group" use the Sdelete tool to delete data?
> **ANSWER: 7**
