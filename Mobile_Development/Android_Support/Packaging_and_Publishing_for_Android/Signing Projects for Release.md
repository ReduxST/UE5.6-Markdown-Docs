# Signing Projects for Release

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/signing-android-projects-for-release-on-the-google-play-store-with-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/signing-android-projects-for-release-on-the-google-play-store-with-unreal-engine)  
**Processed:** 2025-06-14 16:50:30

---

Windows macOS Linux

In the following document, we will cover what you need to do in order to get your UE mobile project ready to be released on the Google Play store.

Please keep in mind that this document will only focus on items that are relevant to getting UE based projects on the Google Play store. If you are looking for more general information about the Google Play store, please consult the official [Google Developer Console Help](https://support.google.com/googleplay/android-developer#topic=3450986).

## Generating Key

Before you can submit or even upload your project to the Google Play store, you will need to generate a Keystore. A keystore is a unique key that will ensure that your project will be linked to your Google Play account and no one else's. In the following section we will go over how you generate this key as well as where it needs to be placed to ensure that your project will use it when being packaged.

1.  Open a Command Line prompt window and navigate to the directory where Android Studio installed the `keytool.exe` file. This will be the `\jre\bin` folder if you are using default installation directories.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/45bae0b6-5eb9-4f53-a9c7-99ab560645b2/01.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2400e227-8705-4696-9942-f29f2ed6727c/01_mac.png)
2.  With the Command Line prompt window now open, input the following Command Line argument and then press the Enter key.
    
    ```
             `keytool -genkey -v -keystore ExampleKey.keystore -alias MyKey -keyalg RSA -keysize 2048 -validity 10000`
    Copy full snippet
    ```
    keytool -genkey -v -keystore ExampleKey.keystore -alias MyKey -keyalg RSA -keysize 2048 -validity 10000 ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a7a3299-b63b-45e9-bb5e-b76827346b5d/02.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f17a6743-1743-4c83-a20f-acd710ef9cb1/02_mac.png)
    
    Instead of typing this in by hand you can also copy the above text and then click with the right mouse button to paste what you copied into the Command Line argument window.
    
3.  Now enter a password for your Key Store. Make sure that this is something you will remember as you will have to enter it one more time after this. For this example, we will be using **123password** for our Keystore password.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5779346f-63ea-40d1-8316-d8a842c48cba/03.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7576aaa-afc6-4fb1-8c89-d9821cb5cea6/03_mac.png)
4.  Next you will need to enter a First and Last name into the Command Line window. For this example, input the name **TestGuy** and then press the Enter key.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1e5af796-ba35-4af4-93ac-f53328fb181d/04.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82744c32-218d-434d-9fba-ec43c85acb88/04_mac.png)
5.  Now enter the name of your Organizational Unit. For this example, input the name **MyCompany** and then press the Enter key to continue.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a6fcafb5-097b-4f60-afef-c810a0beb14e/05.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d016174-e511-46e9-8621-3135b78b7b82/05_mac.png)
6.  Then enter the name of your organization. For this example, input **MyGame** and then press the Enter key to continue.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad8bcee4-e5ce-43ef-8d53-06e49a34386c/06.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/60899ed8-887f-4e9a-bbb8-c885a295f128/06_mac.png)
7.  Now enter the name of the City or Locality you are in. For this example, input **MyCity** and then press the Enter key to continue.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e32136c-15b6-45d4-867c-8fb8b92f610f/07.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/15899a39-d117-4a51-92a1-3328ac460d5f/07_mac.png)
8.  Then enter the name of the State or Province that city is located. For this example, input **NC** and then press the Enter key to continue.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d97965b2-328a-47f6-9c9e-9b16fa285827/08.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bf484b3e-9ca3-4d3e-9643-45dd918cf7ac/08_mac.png)
9.  Now input the country code where the city and state are located. For this example, input **00** and then press the Enter key to continue.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e2d7da29-69ff-4a8c-8cba-8b72e5e876c6/09.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dd11cf6f-e8e8-422d-bb46-c9025a875e32/09_mac.png)
10.  You will now be asked to verify that all the information that you have entered is correct. Type **Yes** or **Y** into the Command Line window and then press the Enter key to continue.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7f0bf823-6a00-497a-a586-969f9b0f416a/10.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a5cd3035-c022-4a34-a8f3-37743c59e43d/10_mac.png)
11.  Because we are only storing a single key into this Keystore, all you need to do next is press the Enter key when asked to enter a password.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/78eb6e3b-b172-490c-ada9-171e0fdc96e1/11.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/249f5edc-0818-4b0b-ab73-891ef542c2a9/11_mac.png)
12.  The last line in the Command Line window should now say, **\[Storing ExampleKey.keystore\]** if everything has been setup correctly.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c65ddc30-ee11-4960-a542-338c21d36f92/12.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dd562663-5ba2-49d8-b06e-2ce725c712ac/12_mac.png)

Once the key has been created it will be placed in the `\jre\bin` folder containing `keytool.exe`.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56332a04-ca7e-49ee-a24d-4426d48cfb2c/keystore_location.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/006fb2c3-44f9-4762-8bf9-d8a4cbe37084/keystore_location_mac.png)

## Placing the Key

Once you have the key generated, it will need to be placed in the following location inside of your UE project.

```
	`(Your Game Folder)\Build\Android`
Copy full snippet
```
(Your Game Folder)\\Build\\Android ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4bac7259-faed-48c5-ac96-e0c9aadcc09b/keystore_build_location.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/94897f22-e70f-42d5-85b8-31ee78561322/keystore_build_location_mac.png)

## Applying the Key

After the key has been placed in your **(Your Game Folder)\\Build\\Android** folder, you will need to apply it to your UE project by doing the following.

1.  Inside of UE, go to **Edit > Project Settings > Platforms > Android**.
    
    ![Navigate to the Distribution Signing section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9a5e2201-b43a-4e8a-8617-d32e741f1c91/ue5_1-01-distribution-signing.png "Navigate to the Distribution Signing section")
2.  Under the **APK Packing** section, make sure to set the **Store Version** to the number one if this is the first time you are uploading the project to the store.
    
    ![Set the Store Version of the application](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9195c9e8-7a77-4334-bd19-006e8317b440/ue5_1-02-store-version.png "Set the Store Version of the application")
    
    Each time you re-cook your project to re upload to the store, you will need to increase the Store Version number. If you do not do this, your new APK file will fail to be uploaded over the old one.
    
3.  Next under **Distribution Signing**, make sure the following fields are filled in with the Keystore information that was used above to generate the Keystore.
    
    ![Setup of the Distribution Signing section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb3e253c-de4f-46c4-b48d-dcbaecca02a1/ue5_1-03-distribution-signing-setup.png "Setup of the Distribution Signing section")
    
    | Property Name | Description | Name used in example |
    | --- | --- | --- |
    | **Key Store** | This is the name given to the .Keystore file. | ExampleKey.keystore |
    | **Key Alias** | This is the name of the .Keystore file. - ExampleKey.keystore | MyKey |
    | **Key Store Password** | The password that was used to secure the key | 123password |
    
4.  Once all of this has been filled, go to the **Packaging** section of your project and under the **Project** section make sure that both **Full Rebuild** and **For Distribution** are enabled.
    
    ![Setup of the Project Packaging](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58d7becf-ddc8-470d-9613-ed13ec1740e6/ue5_1-04-project-packaging-setup.png "Setup of the Project Packaging")

## Deploying to the Google Play Store

Now all that is left is to upload your project to the Google Play store. For a full breakdown of how to upload your project to the Google Play store, please check out the official [Google Developer Console](https://support.google.com/googleplay/android-developer#topic=3450986) help page.