  

**This documentation will include all the steps to perform on Splunk Cloud pushes.**

**APAC CLOUD push:**

First we need to go to the **pipelines tab** which is located on the left bottom of the menu in Devops as you can see here:
![==image_0==.png](/.attachments/==image_0==-a949aeb7-c3ea-4513-8467-5fe8bdba6354.png) 
Now in Pipelines tab, you'll see one of the Pipelines named **"PUSH Cloud"** , click on it.
![==image_1==.png](/.attachments/==image_1==-ee9cbd17-2434-4973-816f-574d9e599b5c.png) 
Inside the **"PUSH Cloud"** pipeline you'll see the previous runs and you can run a new one, click on **"Run Pipeline"** on the top right corner:
![==image_2==.png](/.attachments/==image_2==-524e6a27-74b3-44d5-9c12-c11130885432.png) 

Now you need to select:

- **Branch:** SHC_APAC
- **App Collection:** OnlyChanged

- **And then check:**

- [ ] Push Private Apps (App Collection)
- [ ] Check Indexes
- [ ] Create Tag
- [ ] Rolling Restart
- [ ] Show Banner

Then click on **"Run"** at the bottom right corner.
![==image_3==.png](/.attachments/==image_3==-9f5622e4-8bb8-4c2e-b111-9765e9015697.png) 

Now once you run the pipeline you'll see a menu:
![==image_4==.png](/.attachments/==image_4==-9ee8257f-8267-4dfc-8ec5-750fbc191967.png) 
If you scroll down to **"Jobs"** you'll be able to click on the job and will show a live log of the script:
![==image_5==.png](/.attachments/==image_5==-cc461945-06d7-446f-882c-e8915a2feb3a.png) 

![==image_6==.png](/.attachments/==image_6==-a739b392-991a-43fc-be2f-cb5c0ec0c573.png) 

Here you'll see the live log for the push and if there are any errors they will show up here.
Once the push is finished, go to SHC_APAC and check that the tag was was created and the changes were made.