# Forenote
Images seem small in the page, but can be clicked to expand. 


# Project Overview
This project is based on Josh Madakor's ["Nessus Tutorial"](https://www.youtube.com/watch?v=lT6Px9zJM3s&list=PLBGe27gFBzHTZ28rbovKBDczFyzQOGLS_&index=3). The goal of this project will be to improve our understanding of vulnerability scanning and vulnerability remediation. We will be using Nessus Essentials to scan a local virtual machine running the Windows 10 Enterprise operating system. We are going to run credentialed scans to discover vulnerabilities, remediate remediate them, and finally rescan to verify. 

# Setup

As previously mentioned, our target system will be running the Windows 10 Enterprise operating system. Thus, our first step was obtaining the ISO. To do this, we go on Microsoft's website and download the 64-bit Enterprise ISO.
![win10ISO](https://github.com/mkathia/malware-analysis/assets/113075504/27755319-71da-48d1-ad18-027e8360d9d2)

We then give Virtualbox the ISO, and go through all the standard configuration steps. This includes allocating space (in my case, 75 gigabytes), memory (8 gigabytes), and processors (6 cores).

![win10storage](https://github.com/mkathia/malware-analysis/assets/113075504/1d2a124c-8c74-4a49-a6d5-c58dea1fd2f3)
![win10memory](https://github.com/mkathia/malware-analysis/assets/113075504/3f6a8252-2fec-46c0-bfa9-695aae17b4ce)
![win10processors](https://github.com/mkathia/malware-analysis/assets/113075504/4fb8f41d-7e3d-477b-81e1-e15a231c978c)

After this setup, we go through Windows' setup steps. Then, we have our functional virtual machine.
![image](https://github.com/mkathia/nessus-lab/assets/113075504/c02e3597-fa26-4f16-9514-d4bee8ad26d9)

Next, we proceed to obtain [Nessus Essentials](https://www.tenable.com/products/nessus/nessus-essentials) by filling out the form to get an activation key.
![image](https://github.com/mkathia/nessus-lab/assets/113075504/d84a4f27-ff91-42b5-9a4c-acede8a32d9a)

After obtaining this key, we proceed to the download page and download the application.
![image](https://github.com/mkathia/nessus-lab/assets/113075504/7cb32067-e150-43a6-ab8e-da850e11e838)

After downloading the application, we see this page.

![image](https://github.com/mkathia/nessus-lab/assets/113075504/4665b0f2-c622-4ee0-b48c-969ff89e071c)

After proceeding through the steps and utilizing our activation code, we see this page.
![image](https://github.com/mkathia/nessus-lab/assets/113075504/69546c92-d2a6-42a4-b861-e03be65cd5bf)

This confirms that our webapp is functional. 

# Establishing Connectivity

The first step towards establishing connectivity between our host and guest system is to set the guest system's network adapter to host-only.
![image](https://github.com/mkathia/nessus-lab/assets/113075504/32aa11b8-0e2c-4095-84f7-d275f0b781fe)

We also need to disable Windows defender. We do this by going into the policy settings.

![image](https://github.com/mkathia/nessus-lab/assets/113075504/3077c108-345f-4c9d-9e68-2caf4ac40323)

We then disable the three profiles' firewalls, domain, private, and public.

![image](https://github.com/mkathia/nessus-lab/assets/113075504/a7585838-f5b3-40cf-991a-6a98cfaceda1)

This allows us to communicate between them. This can be verified with a simple ping test.

![image](https://github.com/mkathia/nessus-lab/assets/113075504/98d5dd9b-b6c9-4448-b9ae-2d50e985bff4)

As we can see, the host system can talk to the guest system. This means we can proceed with vulnerability scans. 

# Nessus Scans

As previously mentioned, this is the page we see with Nessus.
![image](https://github.com/mkathia/nessus-lab/assets/113075504/69546c92-d2a6-42a4-b861-e03be65cd5bf)

To begin, we press the "New Scan" button, and that brings us to this page.
![image](https://github.com/mkathia/nessus-lab/assets/113075504/a85b45dd-3a5d-472e-b027-8bcc904dd01b)

We are going to use "Basic Network Scan", and fill out the page provided.
![image](https://github.com/mkathia/nessus-lab/assets/113075504/d8640ee3-8755-427e-bbc2-d3d386dc49aa)

The IP address we gave as a target is that of our guest system.

Note the "Credentials" page, we will be using that later. For now, that is all the settings we will change.

Pressing "save" brings us to this page, where we can see our newly created scan.

![image](https://github.com/mkathia/nessus-lab/assets/113075504/875f5ef3-ce16-45f8-af57-dd17ece230b0)

We are going to go ahead and run this scan.
![image](https://github.com/mkathia/nessus-lab/assets/113075504/53ad496d-c0a2-456c-a925-8c5fae8d0546)

Once completed, we come across this screen.
![image](https://github.com/mkathia/nessus-lab/assets/113075504/37e4c17f-9b85-44f7-8ec5-79782c623841)

This "Hosts" screen gives us a high-level overview of the scan results. When we go to vulnerabilities, we get a more specific view of what was found. 
![image](https://github.com/mkathia/nessus-lab/assets/113075504/860e9a84-03cb-41c3-9853-537003804604)

When we click on the specific issues, we can get an even more specific analysis. For example, if we click on "SMB Signing not required", we see this.
![image](https://github.com/mkathia/nessus-lab/assets/113075504/525ff134-644d-4474-9312-6b7594a2c7f3)

This is a basic introduction into scanning. Our next step is to ensure that Nessus can properly crawl through our system.

# Enabling Credentialed Scans

Some modifications need to be made to ensure Nessus can properly search through our system. The first thing we need to do is enable remote registry. We do this through services.msc.
![image](https://github.com/mkathia/nessus-lab/assets/113075504/e825cd42-995c-4213-ad3d-c4852a0f3a1a)

I proceed to find it, enable automatic startup, and start the service.
![image](https://github.com/mkathia/nessus-lab/assets/113075504/08d17f25-7893-432d-8478-91ec05bc7ffe)

Next, we ensure network discovery and file/printer sharing are on, through the Control Panel.
![image](https://github.com/mkathia/nessus-lab/assets/113075504/6be0ea9f-64e9-4119-900f-a5921cce3e9a)

We're also going to add a key to registry editor to allow the remote account to connect.
![image](https://github.com/mkathia/nessus-lab/assets/113075504/b0de1e9a-44f7-46e7-941f-9e1b10963ad0)

At this point, we restart our virtual machine.

# 1st Credentialed Scan

After rebooting our machine, we need to modify Nessus to have credentialed scans. We provide it our login credentials so it can search through our virtual machine.
