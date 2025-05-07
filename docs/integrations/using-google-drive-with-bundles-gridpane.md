# Using Google Drive with Bundles | GridPane

# Using Google Drive with Bundles

 

2 min read
To add non-WordPress repository themes and plugins to your bundles, you can add your own custom links. We have a KB item for using Dropbox here and in this article we show how Google Drive can be used for the same.

Step 1: Create a folder where you are going to upload the bundle zip files in your GDrive either using the desktop/mobile app or the web interface.

Step 2: Change the share permissions of that folder so anyone with the link can access it.

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='437'%20height='331'%20viewBox='0%200%20437%20331'%3E%3C/svg%3E)
![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='687'%20height='421'%20viewBox='0%200%20687%20421'%3E%3C/svg%3E)![](https://gridpane.com/wp-content/uploads/2021/06/google-drive-gridpane-bundle1-1.png)
Step 3: Upload your plugin/theme zip file to this folder. Select the file and right click or click the Link icon and copy the share link for the file you want to add as a bundle in your GridPane account.

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1024'%20height='687'%20viewBox='0%200%201024%20687'%3E%3C/svg%3E)![](https://gridpane.com/wp-content/uploads/2021/06/google-drive-gridpane-bundle3-1024x687.png)
Step 4: Paste the link URL in a text editor.

Ex.:

```
https://drive.google.com/file/d/1YFfivWtDFkCcXQE0py2rQdL1x295s9IV/view?usp=sharing
```

Note the numeric part of the URL, this is the file ID. In the above example, it is 1YFfivWtDFkCcXQE0py2rQdL1x295s9IV.

Step 5: Using the following as your template, replace the “DRIVE_FILE_ID” with your file ID.

```
https://drive.google.com/uc?export=download&id=DRIVE_FILE_ID
```

Ex.:

```
https://drive.google.com/uc?export=download&id=1YFfivWtDFkCcXQE0py2rQdL1x295s9IV
```

Test the above URL by visiting it in your browser and it should begin to get downloaded. This is the URL that you can add in your bundle.

Repeat Step 3 onwards for as many files as you want to add to your bundle.

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

