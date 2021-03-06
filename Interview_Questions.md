## Activity File: Interview Questions

- This first project covers a wide range of topics including cloud, network security, and logging and monitoring.

- When networking and talking to potential employers, you should be able to reference the work done on this project to answer specific interview questions or demonstrate your skills within a specific domain. 

- You will choose a domain that you're interested in pursuing as a career and answer mock questions based on the suggested response format. 
​
### Instructions 

1. Choose one of the following domains:
    - Network security
    - Cloud security
    - Logging and monitoring

    If you are unsure of which domain you want to focus on, that's okay. You can either choose the one you're most comfortable discussing, or complete the tasks in two or all three domains.

2. Select one domain and one question. 

    - Questions are provided for each domain. Choose one to answer from your chosen domain. 
​
3. Write a one-page response that answers the question using specific examples from your work on Project 1. Your response should flow and read like a presentation while keeping the general structure of the technical question response guidelines. 

    You will submit this one-page response. 

#### Reminder: Response Guidelines
As a reminder,  good responses do the following. 
​
1. Restate the problem.
2. Provide a concrete example scenario.
3. Explain the solution requirements.
4. Explain the solution details.
5. Identify advantages and disadvantages of the solution​.
​
Including each of these components will ensure you prove your competency of subject matter and critical thinking. 
​
### Interview Questions by Domain

Below you will find a list of questions, grouped by specific domains. Select one question to answer. 
​ 

For each question, where appropriate, we have provided you with specific prompts to consider as you structure each section of your response. Feel free to use these prompts or your own examples. 



#### Domain: Cloud Security

**Question 1: Cloud Access Control**

How would you control access to a cloud network?

1. Restate the Problem
	- What are effective measures to control access to a cloud network. 
2. Provide a Concrete Example Scenario

	In my project, I deployed my assets onto a cloud network. In Microsoft Azure, a designer has the ability to create a network security
	group and subsequently add specific rules, including those that restrict access. To begin, I created a 'Default:Deny' rule that restriced
	traffic from all ports until more nuanced rules were in place. From there, I restricted various avenues of access to the virtual network
	, including limiting access to specific ports, specific ip addresses, and enabling an encrypted public key only shared from the host device
	to the jumpbox. 

3. Explain the Solution Requirements

    - In Project 1, what kinds of access controls did you have to implement? Consider:
        - NSGs around the VNet? Around the VMs?
        - Local firewalls (ufw, etc.) on each VM?
        - Protocol allow/deny lists?

    - What did each access control achieve, and why was this restriction necessary for the project?

	- For my main Network Security Group, I implented the following access controls(Listed in order of priority):
		- Allow-HTTP-From-Home-Network
			- This rule allowed access to the network loadbalancer from my homenetwork
		- Allow-SSH-From-Home-Network
			- This rule allowed access to the virtual network through secureshell traffic arriving from my home netowork ip address
			 only.  
	- These firewalls and protocalls ensured that the backend of my virtual network could be accessed only in a very specific set of parameters 
	were met, parameters that, in this case, were limited to one specific network. 
	
	- It was necessary to employ such a stringent architecture for this project since the jump-box that was set up gave a great amount of access
	to our resources.  
4. Explain the Solution Details

	- Port access rules are set up on each NSG in the network. 

	- To access the jump-box, the secureshell request must be made from my home network on a device that contains my public key that was created
	and shared with the jump-box resource in Azure. 
	
	- To access the webservers from the jump box, a user must use docker to start the Ansible container. From inside Ansible, ssh access to web
	servers 1 & 2 is available. 

5. Identify Advantages/Disadvantages of the Solution

	- Scalability is an issue with my current solution. If more servers are added and additional teammates brought in to assist with server maintenance,
	it is unreasonable to expect all parties to use my home network or to add addtional NSG rules to allow access for their individual IP addresses. 
	This would not be secure as well. 

	- A more scalable solution would be a VPN that could create a secure connection to the virtual network. 

	- VPN Advantages: Secure connection for remote work, provide safety through anonymity, cost-effective
	
	- VPNs should be used anytime a public network is being used or remote work is being attempted. 

**Question 2: Corporate VPN**

What are the advantages and disadvantages of using a corporate VPN, and under what circumstances is using one appropriate?

1. Restate the Problem
	- There are different pros and cons to implementing a corporate VPN security solution - these help to decide when using one may be 
	best practice. 
2. Provide a Concrete Example Scenario
   
    - In Project 1, which VMs did you have on the network?
    - Which tools did you use to control access to and from the network?
    - If you didn't use a VPN, what did you use?
    - What disadvantage(s) did your non-VPN solution have?
    - What advantage(s) did your non-VPN solution have?
	
	- In my project, there were a total of four VMs on network. To control access to these machines, a variety of controls and rules were implemented 
	by my network security group. The most notable solution was using a ssh protocol for access rather than a VPN solution. While this does have a 
	few draw backs, such as being restricted to a single network, it also represents a simple, elegant solution that provides ease of access to a 
	network that only needs one user. 

3. Explain the Solution Requirements

    - Would a VPN meet the access control requirements you had for Project 1?
    - How would a VPN protect the network just as well, or better, than your current solution?
	I believe that, if properly set up, a VPN could potentially meet the control requirements for the project. The main access point in question was
	to the jump-box, as that allows access to the web servers and elk-stack. If a VPN could be set up specifically for access to that jump-box, that 
	could satisify the requiements in my opinion. 

	- An additional pro that a VPN would bring is a protected, anonymous network tunnel. These could provide additional protection while accessing my 
	virtual network. 


4. Explain the Solution Details


	The Azure VPN Client created by the Microsoft Corporation seems like the most natural fit if a VPN were to be added. This product allows secure
	connection to Azure from anywhere in the world. 
	
	To onboard users, they could be added throught the Azure active directory. 


5. Identify Advantages and Disadvantages of the Solution

    - I don't believe for this project that a VPN was the most prudent solution. 
	Because of the small nature of the virtual network, with only one user needing access, a combonation of rules and access controls managed
	throught the network security seemed the most prudent solution. 


**Question 3: Containers**

When is it appropriate to use containers in cloud deployments, and what are the security benefits of doing so?

1. Restate the Problem
	- Under what circumstances does it make sense to deploy containers within the cloud and are there any addtional security benefits from their use?
2. Provide a Concrete Example Scenario

    - Within my project, containers were used both within the Jump-box (Ansible) and the Web-Servers (DVWA)

3. Explain the Solution Requirements
	
	- Containers are useful when wanting to run what is essentially a lightweight VM. Rather than creating another entire VM with an OS, RAM, storage, 
	etc, containers may be used to employ what is essentially only an OS and whatever service you would like them to run. In the case with the container
	within the jump-box, that container "contained" an OS and the Ansible service. 
	
	- Using containers also provides security benefits, as it limits the attach surface on which bad actors could attempt to exploit. 

4. Explain the Solution Details

	- In order to run containers, the Docker tool had to first be installed onto the VMs. With Docker, the latest Ansible container was then installed by running
	sudo docker pull cyberxsecurity/ansible. After that we start the container with Docker and use a list command to ensure it is running as designed. 
	

5. Identify Advantages/Disadvantages of the Solution

    - How would you have achieved the same thing without containers?
    - What are the advantages to doing it without containers?
    - What are the disadvantages?

	- Technically, this project could have been completed without containers. Additional VMs for Ansible and DVWA could be created and configured individually. 
	This would allow those resources to have a complete, virtualized device. 

	- However, this would have major disadvantages. Virtualizing an entire device when only a small portion is needed is both a waste of time and financial 
	resources. Each device would have to be individually configured, missing out on Ansible's greatest asset, and the scalability is greatly reduced.  


**Question 4: Cloud Infrastructure as Code**

What are the security benefits of defining cloud infrastructure as code?


1. Restate the Problem
	- Are there any benefits, in a security sense, to cloud infrastructure as code?
2. Provide a Concrete Example Scenario

	- During my project I used IaC when utilizing the Ansible container to configure multiple VMs with the DVWA at once. 

3. Explain the Solution Requirements

    - Were there any alternatives to IaC?
    - What benefits does IaC have over alternative approaches?

	- An alternative would be to go into each VM one at a time and configure them as desired. 

	- IaC greatly streamlines this process and makes it so one user can configure hundreds or even thousands of containers in a very short amount of time. 


4. Explain the Solution Details

    - In Project 1, which specific configurations did your IaC set up?
    - How did you run and test these configurations?

	- In my project IaC was used to set up the DVWA servers. The IaC was run through a playbook created on the Ansible container and then subsequently tested by 
	accessing the DVWA site through my virtual networks load balancer. 


5. Identify Advantages/Disadvantages of the Solution

    - Are there any disadvantages to using IaC over the "traditional" approach?

	- By providing a streamlined provisioning method, quick destruction and redeployment and freeing up employee time, I do not feel there are any disadvantages of 
	IaC over the traditional approach. 





---

© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.  
