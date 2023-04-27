# LiveSurgicalAid
Through the use of Augmented Reality (AR) and Deep Learning, I have developed a surgical aid that surgeons can use during minimally invasive brain tumor removals. This system first uses deep learning models I trained on 350+ MRIs to generate patient specific models of the tumor and cerebral vasculature or brain blood vessels. I then developed a Unity application to render these 3D models in the surgeons field of view, first building an application to an Android phnoe, and then using the head-mounted display known as the Microsoft Hololens. This system essentially gives the surgeon X-ray vision, allowing them to see the exact position of the tumor and blood vessels overlayed onto the patient like a hologram.

My live surgical aid has several parts: brain tumor segmentation, cerebrovascular segmentation, physical demonstration target creation and detection, and Unity app development. This project uses Python through Google Colab as well as Unity and C#. The pictures and data are shown and explained below.
![image](https://user-images.githubusercontent.com/86267840/234745354-18691b88-803b-4823-a781-3821a8107ada.png)

This image shows the slices of the MRI after being loaded in to the colab notebook through nibabel
![image](https://user-images.githubusercontent.com/86267840/234745452-8445f136-1e8a-4cd2-8736-c5117a8a60e9.png)

The labels are overlayed onto the data in different colors.
![image](https://user-images.githubusercontent.com/86267840/234745716-89b6d7a2-df1b-4eae-8fc7-64ac14f023a6.png)

A 3D U-Net was used as the algorithm for brain tumor segmentation, and was trained on 350+ MRIs from the BRATS dataset. The U-Net is the standard for medical segmentation; it features an encoder and a decoder.
![image](https://user-images.githubusercontent.com/86267840/234746140-b69da9d0-2ee1-4231-aac8-bf77614ba183.png)
![image](https://user-images.githubusercontent.com/86267840/234746159-0d059e63-4395-44ef-9951-3ffccbc396bf.png)

The ground truth as well as the AI's predictions after training can be seen in the above image. The accuracy of the segmentation was above 99%.
![image](https://user-images.githubusercontent.com/86267840/234747781-0cb15bb6-cccf-4bab-af3d-35cd53ec811c.png)

The image above shows the cerebrovascular data visualized in 3D Slicer, a medical utility.

![image](https://user-images.githubusercontent.com/86267840/234747868-e076d097-ff2f-4ebb-9855-929ba6944d26.png)
The RE Net is similar to the U-Net, as it is also utilized for medical segmentation.

![image](https://user-images.githubusercontent.com/86267840/234747949-edea9a45-80c2-49b5-9501-28046e7dc272.png)
After both models were trained and completed, MRIs from a test patient were uploaded into both models, and their outputs were converted to 3D models and imported into Unity.

![image](https://user-images.githubusercontent.com/86267840/234748042-50218ae9-ed81-4a9d-8459-077cd8f7cd82.png)
![image](https://user-images.githubusercontent.com/86267840/234748054-0260a323-2aa5-428c-8b87-866e7dbf7d84.png)

A 3D head was constructed to serve as the demonstration target, and a seperate deep learning model was trained on its CAD model.

![image](https://user-images.githubusercontent.com/86267840/234748899-c5a683e3-c6c9-43d9-9c7c-006256b8911c.png)

Lots of configuration was done in Unity, and utilizing Vuforia functionality, the system was built to the Android phone.

![image](https://user-images.githubusercontent.com/86267840/234749039-b9741d3e-8cde-4e96-95b9-65033d812ab2.png)

The system was later modified to be built as an application to the Hololens 2 using Universal Windows Platform, and a similar view can be seen through it.
