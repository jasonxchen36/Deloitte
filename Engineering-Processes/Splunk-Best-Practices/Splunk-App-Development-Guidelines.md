# **Recommendations for App Development**

## **Searches**

- Dedup is a resource intensive command, utilize stats count instead where possible. Simplified example in a 4 hour window:

![image.png](/.attachments/image-ef70b21d-62cc-44be-b6e1-aef0db17c144.png)

![image.png](/.attachments/image-7e40840f-21d9-48e4-9677-af379f603a67.png)

## **Dashboards**

- Feed multiple panels with base searches to avoid excessive resource utilization. Assigning a token to your base search will also retain drill down functionality. 

Creating the base search:
![image.png](/.attachments/image-d7310f16-5f14-41b0-b1d2-f30af258f414.png)

Using the base search in a panel:
![image.png](/.attachments/image-0c131519-1d51-4456-abc2-9305d3981201.png)