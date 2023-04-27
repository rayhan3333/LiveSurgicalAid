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
