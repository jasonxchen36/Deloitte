  
Here's a brief explanation on how to create/change an index configured as type=Events as type=Metrics:

(**Note: You can't just edit the type of an index, in order to change an index into metrics you'll need to delete it and create it again as metrics**)
(**Note2: Also before deleting or adding any index, make sure to make a PR before making any changes into Cribl and wait for it to be appproved**)

We go to **Cribl**, into the prod instance of the region of the index we are about to create/change:

![==image_0==.png](/.attachments/==image_0==-7789e042-c463-4de1-b202-6c6cfab7b2a9.png) 

We'll go into the **Cribl Internal** source and select **CriblMetrics** ID, after that, into **configure>fields** option:

![==image_1==.png](/.attachments/==image_1==-f34c84da-cae1-423d-a258-68f612a92931.png) 

We select the "**Add Field**" option and add your index name, simple as that, we **save** and **commit** the changes into Cribl.

Here you can see the index integrated with the correct type=Metrics using an privileged account:

![Image](https://dev.azure.com/GlobalSOC/f9d27325-cf4e-42dc-b8b7-4a00c4042942/_apis/wit/attachments/fcf21774-0dbe-4360-9b5e-b271c8211362?fileName=image.png)

Remember to wait for the PR to be approved to begin this procedure.