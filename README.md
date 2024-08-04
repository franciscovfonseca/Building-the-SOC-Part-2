<br>

<h1 align="center">Stage II - Building the SOC - Part 2</h1>

<br>

<h2 align="center"> Enable Microsoft Defender for Cloud</h2>

![Banner](https://github.com/user-attachments/assets/72fb23aa-bc68-46ce-b60f-43d1cd5aa8a5)
<br />
<br />

<details close> 
<summary> <h2>1️⃣ Enable Microsoft Defender for Cloud for Log Analytics Workspace</h2> </summary>
<br>

Open Microsoft Defender for Cloud:

<br>

![azure portal](https://github.com/user-attachments/assets/075f495e-6c91-4b9a-996e-ebadfd86db66)

<br>

Go to **"Environment settings"** ➜ Expand the ```∨``` next to the **"Cyber Lab"** Subscription.

All the way on the right side of the **"LAW-Cyber-Lab"** line ➜ click on ```...``` ➜ and then **"Edit settings"**:

<br>

![azure portal](https://github.com/user-attachments/assets/55241b3a-6338-42e9-890e-f69c0f027472)

<br>

First we'll go to the **"Defender plans"** tab.

We'll **Turn On** MDC for **"Servers"** and also for **"SQL servers on machines"** ➜ since we do have a SQL Server instance.

<br>

>   <details close> 
>   
> **<summary> 💡 </summary>**
> 
> This will allow us to **Collect Logs** from these resources.
> 
>   </details>

<br>

Make sure you click the 💾 **Save** button:

Then we'll go to the **"Data collection"** tab ➜ and check **"All Events"**

<br>

![azure portal](https://github.com/user-attachments/assets/27dbab3a-ab4e-4d7e-8c7d-51f0b2e04e32)

<br>

>   <details close> 
>   
> **<summary> 💡 </summary>**
> 
> This will allow us to **Collect All Events from the Windows Security Log**.
> 
> Which is like the **Windows Event Viewer**, where we can see people attempting to **Log Into our Windows Machines over the Internet**.
> 
> We're going to be able to **Collect Logs** from that and then **Forward Them to this Log Analytics Workspace**.
> 
>   </details>

<br>

Again ➜ click the 💾 **Save** button.

<br>

  </details>

<h2></h2>

<details close> 
<summary> <h2>2️⃣ Enable Microsoft Defender for Cloud for the Subscription</h2> </summary>
<br>

Back to **MDC** ➜ **"Environment settings"** blade.

This time for the **"Cyber Lab"** Subscription line ➜ click on ```...``` ➜ and then **"Edit settings"**:

<br>

![azure portal](https://github.com/user-attachments/assets/997c7114-f007-459a-aa1c-020ef5116616)

<br>

Under the **"Defender Plans"** Blade ➜ we'll **Turn On** MDC for **"Servers"**, **"Databases"**, **"Storage"** & **"Key Vault"**.

<br>

>   <details close> 
>   
> **<summary> 💡 </summary>**
> 
> We'll create a **Storage Account** and **Key Vault** instances in a subsequent lab.
> 
>   </details>

<br>

![azure portal](https://github.com/user-attachments/assets/bfdebca1-ca31-49c6-88a0-3511c02c4d1a)

<br>

Next to **"Databases"** ➜ click on **"Select Types >"** ➜ make sure **"SQL servers on Machines"** is toggled **ON**.

All else toggled **OFF** ➜ then click **"Continue"**

<br>

![azure portal](https://github.com/user-attachments/assets/5d37e956-0721-4b59-94a3-c8e599d77a49)

<br>

We'll now configure **"Servers"** ➜ under the **"Monitoring coverage"** tab ➜ and click on **"Settings >"**

Make sure that all the way to the right ➜ the **"Status"** for all 4 Components is toggled **ON**

<br>

![azure portal](https://github.com/user-attachments/assets/1e299c5d-c9a4-43c7-9747-27f1caf8ec50)

<br>

Now still on that same page ➜ under **"Configuration"** for the **Log Analytics agent** ➜ click on **"Edit configuration"** 

And for the **Workspace selection** ➜ pick our actual ```LAW-Cyber-Lab``` Workspace.

<br>

>   <details close> 
>   
> **<summary> 💡 </summary>**
> 
> We don't want it to automatically create a new LAW ➜ we want to use the one we created.
> 
> We're basically onboarding our Virtual Machines to our LAW and then forward the Logs to it
> 
>   </details>

<br>

Make sure you click **"Apply"** and then 💾 **Continue**:

<br>

![azure portal](https://github.com/user-attachments/assets/c5515754-abd1-4416-b509-40ba54a0274e)

<br>

After that ➜ we'll click on the 💾 **Save** button to save the **Defender plans for the Subscription**

<br>

>   <details close> 
>   
> **<summary> 💡 Note</summary>**
> 
> If you accidentally saved before configuring the LAW agent: Go back and change to custom, then go through your resources and delete resources that were automatically provisioned in the processes. 
> 
> To avoid future mixups, make sure there is only ONE LAW.
> 
>   </details>

<br>

  </details>

<h2></h2>

<details close> 
<summary> <h2>3️⃣ Enable Microsoft Defender for Cloud Continuous Export in Environment Settings</h2> </summary>
<br>

Still inside the **"Edit settings"** for the Subscription ➜ we'll go to the **"Continous export"** blade now.

Click on the **"Log Analytics workspace"** tab ➜ and make sure **"Export enabled"** is **Turned On**:

<br>

>   <details close> 
>   
> **<summary> 💡 </summary>**
> 
> Doing this will **Export Alerts into our LAW** so we can **Query Them Later**.
> 
> So if **Defender for Cloud** discovers there's some problem with our Environment, like a **Brute-Force Attack** going on, or there's a **Poor Configuration** for example ➜ MDC will **Export those Alerts into our LAW** ➜ which will let us **Query Them Later**
> 
>   </details>

<br>

![azure portal](https://github.com/user-attachments/assets/cbd01204-5576-4fa0-bba3-02d0271b0b69)

<br>

So we'll enable ☑️ **Exported data types** for all of the following options:

<br>

>   <details close> 
>   
> **<summary> 💡 </summary>**
> 
> We haven't actually configured **"Regulatory compliance"** yet, but we'll do that in a future lab.
> 
> This will basically enable **NIST 800-53** for our Environment to see what controls are missing in certain areas.
> 
>   </details>

<br>

![azure portal](https://github.com/user-attachments/assets/ab98095e-5298-40ae-b74f-615e9a1ffdf2)

<br>

For the **"Export configuration"** option let's just configure it to our **Resource group** ```RG-Cyber-Lab```

And also for the **"Export target"** we'll select our **Target Workspace** ```LAW-Cyber-Lab-01```

<br>

>   <details close> 
>   
> **<summary> 💡 </summary>**
> 
> This is the target workspace where we want to **Export the Alerts to** ➜ so we have to select our **LAW**.
> 
>   </details>

<br>

We'll then click 💾 **Save**

<br>

![azure portal](https://github.com/user-attachments/assets/2b3f4190-ca2f-44c2-9013-a949d787e282)

  </details>

<h2></h2>

<br>

<br>

<br>

<br>

<br>

<br>

<br>
  
<br>
