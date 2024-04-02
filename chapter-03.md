# Quick Start Canvs Panel

- So, let's say we want to create a new dashboard, and we want to use the `Canvs` panel.
  - Click on `New Dashbaord`.
  - Click on `Add Visualization`.
  - Select `Prometheus`.
  - Than goto `Metrics Explorer`, and search for `node_filesystem_free_bytes`. This will give us the free space on the file system.
  - Than, under `Label Filters` select `mountpoint` and set value to `/System/Volumes/Update`
  - Hit `Run queries`. And, output should look something like this.
  
  ![](./imgs/Screenshot%202024-02-12%20at%202.29.46 AM.png)

  - Now, if we want to change the unit for these graphs, go on to the right hand side and search for bytes(IEC), and we can see the data in GBs now.

  - Now, we want to set the thresold. So, let's understand first what thresold is before defining the thresoldes for our case.

    - So, the thresold is any value above which we want to get alerted.

    - In our case let's say when the space oon our disk is more than 25% we want to show green. And, otherwise if below that red.

    - We will set the Thresold Mode to percentage, in that case. Now, we specify the `Base` Colour as `RED`, and the `thresold` Colour as `GREEN`.

    And, it would look something like this:

    ![](./imgs/Screenshot%202024-02-12%20at%202.47.18 AM.png)

    - Note, if in case you are entering values of thresold in absolute, you must enter it in bytes(IEC).

    - Set `Show Thresolds` to `As filled regions and lines`.

    - Click on `Apply`.

  - Once, we are done with this, duplicate it and go to `edit`. Now, change from `time series` to `canvas`. And, you would see something as follows:

  ![](./imgs/Screenshot%202024-02-12%20at%202.53.36 AM.png)

  - Now, Double Click to set the field, get the dropdown, and select `node_filesystem_free_bytes`, and it will show how much space is available in the form of a metric.

  - Now, if we scroll on the right hand side, we will see under layer, we have different elements. Rename the element to `FreeDiskSpace`, and for simplicity, keep the color under background tab to `Fixed Color`.

  - Click Apply.
  
  It would look something like this:

  ![](./imgs/Screenshot%202024-02-12%20at%203.03.50 AM.png)

  So, right now we are monitoring the highlighted server.

  If, now we crate a hugle random file of size 10 GB, it would cause the line graph to move to red zone and, the button as a result will turn red as well.

  Now, let's say we want to clear space on our system as soon as the space occupied reaches a certain thresold. We can automate this thing. Let's say we have ansible installed in our environment, or our owwn custom automation available, and some API available in order to perform space cleanup.

  - For that, we go to `Edit`, we goto `Layer` and than cllick on add item of `Button` type. Rename it as `Action` for the demo purpose.
  
  ![](./imgs/Screenshot%202024-03-10%20at%203.31.23 AM.png)

  - Now, select that `Action` Tab, change the value to `Perform Clean Up`.

  ![](./imgs/Screenshot%202024-03-10%20at%203.34.47 AM.png)

  - If you scroll below, you can see an option for API Endpoint, where you can specify the API endpoint for the cleanup.

  ![](./imgs/Screenshot%202024-03-10%20at%203.37.25 AM.png)

  Now, if you click Test API, this will launch an Ansible Job of performing the cleanup.

# Diagrams in Canvas Panel

- For the same dashbaord, Click on `Add`, than click `Visualization`