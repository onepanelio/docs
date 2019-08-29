To create a workspace:

1. Go to a Project and click **Workspaces**.

2. Click **Create Workspace** in the top right corner.
![](../assets/img/create-170723.png)

3. Select an **Environment** and click **Next**.
![](../assets/img/create-194419.png)

4. Next, enter a workspace name. Workspace naming criteria are as follows:
    - 3 to 25 characters
    - Lower case alphanumeric, `-` or `_`
    - Must start and end with alphanumeric

5. Click **Select machine** to see a selection of machine types. A machine's price is displayed after you select it.
![](../assets/img/create-171530.png)

6. Optionally, you can select **Use spot machine** to select a [Spot Machine](machine-types/spot).
![](../assets/img/create-171832.png)

7. Select an existing or add a **Code Repository**, otherwise select **None**. The repository will be pulled into `/onepanel/code` folder. See [managing repositories](/projects/repositories/#add-a-repository-in-a-workspace-or-job) for more information.
![](../assets/img/create-193843.png)

8. Optionally, mount Datasets by clicking **Add Dataset**.
![](../assets/img/create-194943.png)

9. Optionally, change storage size by clicking **Change**. If you have selected Datasets, Onepanel will automatically adjust storage size based on total size of added Datasets plus an additional 50GB.
![](../assets/img/create-195238.png)

10. Click **Create** to create your Workspace. Depending on your machine type, this could take up to 5 minutes.