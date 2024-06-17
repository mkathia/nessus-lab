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
![Screenshot 2024-06-01 191610](https://github.com/mkathia/malware-analysis/assets/113075504/8cc537e1-ea9a-4fd4-a18e-ef298838a13b)

Next, we proceed to obtain [Nessus Essentials](https://www.tenable.com/products/nessus/nessus-essentials) by filling out the form to get an activation key.
![image](https://github.com/mkathia/nessus-lab/assets/113075504/d84a4f27-ff91-42b5-9a4c-acede8a32d9a)

After obtaining this key, we proceed to the download page and download the application.
![image](https://github.com/mkathia/nessus-lab/assets/113075504/7cb32067-e150-43a6-ab8e-da850e11e838)

After downloading the application, we see this page.

![image](https://github.com/mkathia/nessus-lab/assets/113075504/a8b7a50d-a02c-43f7-9e39-6dc8644a04c2)

After proceeding through the steps and utilizing our activation code, 



