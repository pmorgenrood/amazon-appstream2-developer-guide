# Default Application and Windows Settings and Application Launch Performance<a name="customizing-appstream-images"></a>

 You can create default application and Windows settings to enable your users to get started with their applications quickly, so that they won't need to create or configure the settings themselves\.

AppStream 2\.0 optimizes the launch performance of your applications for your users' streaming sessions\. To ensure that all of the required files are included in this process, you may need to manually add certain files and folders to the optimization manifest\.

**Topics**
+ [Creating Default Application and Windows Settings for Your AppStream 2\.0 Users](#creating-default-app-Windows-settings)
+ [Optimizing the Launch Performance of Your Applications](#optimizing-app-launch-performance)

## Creating Default Application and Windows Settings for Your AppStream 2\.0 Users<a name="creating-default-app-Windows-settings"></a>

Application and Windows settings that are saved to the Windows user profile folder or the user registry hive can be set as defaults\. When you save the default settings by using Image Assistant, AppStream 2\.0 replaces the Windows default user profile with the profile that you configure\. The Windows default user profile is then used to create the initial settings for users in the fleet instance\. If the application or Windows settings that you configure don't work in the fleet, confirm that they are saved in the Windows user profile\. For more information, see Step 3: Create Default Application and Windows Settings in [Tutorial: Create a Custom AppStream 2\.0 Image](tutorial-image-builder.md)\.

Default settings that you can create and configure include:
+ Application preferences, including a browser home page, toolbar customizations, and security settings\.
+ Application data settings, including browser bookmarks and connection profiles\.
+ Windows experience settings, including displaying file name extensions and hidden folders\.

Additionally, you can modify or disable Internet Explorer security settings, such as Enhanced Security Configuration \(ESC\)\. For more information, see [Disable Internet Explorer Enhanced Security Configuration](customize-fleets.md#customize-fleets-disable-ie-esc)\.

## Optimizing the Launch Performance of Your Applications<a name="optimizing-app-launch-performance"></a>

When you create an image, AppStream 2\.0 requires that you optimize the launch performance of your applications for your users' streaming sessions\. When your applications are opened during this process, make sure that they use the initial components required by your users\. Doing so ensures that these components are captured by the optimization process\. In some cases, not all of the files required for the optimizations are detected\. Examples of such files would be plug\-ins or components that aren't opened in the image builder\. To ensure that all of the files and folders needed for your application are captured, you can include them in the optimization manifest\. Adding files and folders to the optimization manifest may increase the time it takes for fleet instances to be created and made available for users\.

To optimize a folder and its contents, open the command prompt as an administrator and use the following PowerShell command: 

```
dir -path "C:\Path\To\Folder\To\Optimize" -Recurse -ErrorAction SilentlyContinue | %{$_.FullName} | Out-File "C:\ProgramData\Amazon\Photon\Prewarm\PrewarmManifest.txt" -encoding UTF8 -append
```