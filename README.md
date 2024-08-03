<br>

<h1 align="center">Stage II - Building the SOC - Part 2</h1>

<br>

<h2 align="center"> Enable Microsoft Defender for Cloud</h2>

![Banner](https://github.com/user-attachments/assets/48a4e854-204f-422e-8287-301a1f768062)
<br />
<br />

<details close> 
<summary> <h2>1️⃣ Enable Microsoft Defender for Cloud for Log Analytics Workspace</h2> </summary>
<br>

Open Microsoft Defender for Cloud:

<br>

![azure portal](https://github.com/user-attachments/assets/ea9306fc-dea8-45d9-9a96-74da3b332516)

<br>

Go to **"Environment settings"** ➜ Expand the ```∨``` next to the **"Cyber Lab"** Subscription.

All the way on the right side of the **"LAW-Cyber-Lab"** line ➜ click on ```...``` ➜ and then **"Edit settings"**:

<br>

![azure portal](https://github.com/user-attachments/assets/ea9306fc-dea8-45d9-9a96-74da3b332516)

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

![azure portal](https://github.com/user-attachments/assets/ea9306fc-dea8-45d9-9a96-74da3b332516)

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

Again ➜ click the 💾 **Save** button:

<br>

  </details>

<h2></h2>

<details close> 
<summary> <h2>2️⃣ Enable Microsoft Defender for Cloud for the Subscription</h2> </summary>
<br>

Back to **MDC** ➜ **"Environment settings"** blade.

This time for the **"Azure subsription 1"** line ➜ click on ```...``` ➜ and then **"Edit settings"**:

<br>

![azure portal](https://github.com/user-attachments/assets/ea9306fc-dea8-45d9-9a96-74da3b332516)

<br>

Now we'll **Turn On** MDC for **"Servers"**, **"Databases"**, **"Storage"** & **"Key Vault"**.

<br>

>   <details close> 
>   
> **<summary> 💡 </summary>**
> 
> We'll create a **Storage Account** and **Key Vault** instances in a subsequent lab.
> 
>   </details>

<br>

Next to Databases ➜ Select Types ➜ make sure **"SQL servers on Machines"** is toggled **ON**.

All else toggled **OFF** ➜  then click **"Continue"**

<br>

![azure portal](https://github.com/user-attachments/assets/ea9306fc-dea8-45d9-9a96-74da3b332516)

<br>

Then click on **"Settings >"** under **"Monitoring coverage"** for the **Servers**.

We'll now click on **"Edit configuration"** for the **Log Analytics agent**.

And for the **Workspace** ➜ pick our actual ```LAW-Cyber-Lab``` Workspace.

>   <details close> 
>   
> **<summary> 💡 </summary>**
> 
> We don't want it to automatically create a new LAW ➜ we want to use the one we created.
> 
> We're basically onboarding our Virtual Machines to our LAW and then forward the Logs to it
> 
>   </details>

Make sure you click **"Apply"** and then 💾 **Continue**:

<br>

![azure portal](https://github.com/user-attachments/assets/ea9306fc-dea8-45d9-9a96-74da3b332516)

<br>

After that we'll click on the 💾 **Save** button to save the **Defender plans for the Subscription**

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

>   <details close> 
>   
> **<summary> 💡 </summary>**
> 
> Doing this will **Export Alerts into our LAW** so we can **Query Them Later**.
> 
> So if **Defender for Cloud** discovers there's some problem with our Environment, like a **Brute-Force Attack** going on, or there's a **Poor Configuration** for example ➜ MDC will **Export those Alerts into our LAW** ➜ which will let us **Query Them Later**
> 
>   </details>

![azure portal](https://github.com/user-attachments/assets/ea9306fc-dea8-45d9-9a96-74da3b332516)

So we'll enable ☑️ **Exported data types** for all of the following options:

>   <details close> 
>   
> **<summary> 💡 </summary>**
> 
> We haven't actually configured **"Regulatory compliance"** yet, but we'll do that in a future lab.
> 
> This will basically enable **NIST 800-53** for our Environment to see what controls are missing in certain areas.
> 
>   </details>

![azure portal](https://github.com/user-attachments/assets/ea9306fc-dea8-45d9-9a96-74da3b332516)

For the **"Export configuration"** option let's just configure it to our **Resource group** ```RG-Cyber-Lab```

And also for the **"Export target"** we'll select our **Target Workspace** ```LAW-Cyber-Lab-01```

>   <details close> 
>   
> **<summary> 💡 </summary>**
> 
> This is the target workspace where we want to **Export the Alerts to** ➜ so we have to select our **LAW**.
> 
>   </details>

We'll then click 💾 **Save**

![azure portal](https://github.com/user-attachments/assets/ea9306fc-dea8-45d9-9a96-74da3b332516)

<br>

  </details>

<h2></h2>

<br>

<br>

<br>

<br>

<br>
  
<br>
