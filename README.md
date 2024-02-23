# Development of a Novel Live Surgical Aid using Augmented Reality and Deep Learning

## About
Brain cancer poses a formidable challenge as tumors infiltrate the fragile and critical
 structures of the brain, resulting in a bleak 36% 5-year survival rate. The primary challenge in
 brain surgery lies in the limited access to 3D information about the tumor and surrounding
 critical structures such as blood vessels and white matter that often interfere with surgical
 removal. Currently, vital information and scans are displayed on separate 2D monitors, diverting
 focus, compromising precision, and hampering the surgeon’s ability to navigate brain anatomy.
 To address these challenges, NeuroLens presents a novel augmented reality (AR) based surgical
 aid for the visualization of patient-specific tumor, vasculature, and white matter tract models
 directly on the patient with millimeter accuracy. First, several deep learning models were trained
 on Magnetic Resonance Images (MRI) from more than 1000 patients for the delineation of these
 critical structures in 3D. Second, a comprehensive AR application was programmed in Unity and
 deployed to the Microsoft Hololens 2. This AR application featured an unprecedented 6DOF
 tracking algorithm able to superimpose the 3D surgical guide models from any orientation in
 real-time onto a patient phantom head with less than 2 millimeters of error. Third, additional
 modalities powered by AR for nervous mapping, detailed anatomical analysis, and voice
 recognition were programmed into the application to facilitate ease of use in a surgical
 environment. By creating and visualizing a live 3D map of critical brain anatomy, NeuroLens has
 the potential to revolutionize brain surgery and significantly improve surgical outcomes for
 millions of patients

## Method

The methodology for this project waws divided into two main parts. The first is a novel-python based system containing several deep learning algorithms to segment or outline patient anatomy such as the tumor, blood vessels, and white matter, from patient MRIs. This system produces a 3D model of patient-specific anatomy, converted to a mesh, normalized to a reference MRI, and decimated to reduce rendering costs. The second part is a Unity application to render these 3D models in augmented reality (AR) directly onto the patient. This is done through a tracking algorithm to recognize markers on the patient and accordingly superimpose their anatomy. The AR application also poses other modes to allow for ease of use and readily available data during surgery.
### Brain Tumor Segmentation
An encoder-decoder model (3D U-Net) was implemented to segment, or outline, the 3D geometry of the patient's brain tumor from their MRI. 

![image](https://user-images.githubusercontent.com/86267840/234745354-18691b88-803b-4823-a781-3821a8107ada.png)

This image shows the slices of the MRI after being loaded in to the colab notebook through nibabel

![image](https://user-images.githubusercontent.com/86267840/234745452-8445f136-1e8a-4cd2-8736-c5117a8a60e9.png)

The labels are overlayed onto the data in different colors.

![image](https://user-images.githubusercontent.com/86267840/234745716-89b6d7a2-df1b-4eae-8fc7-64ac14f023a6.png)

A 3D U-Net was used as the algorithm for brain tumor segmentation, and was trained on 350+ MRIs from the BRATS dataset. The U-Net is the standard for medical segmentation; it features an encoder and a decoder.

![image](https://user-images.githubusercontent.com/86267840/234746140-b69da9d0-2ee1-4231-aac8-bf77614ba183.png)
![image](https://user-images.githubusercontent.com/86267840/234746159-0d059e63-4395-44ef-9951-3ffccbc396bf.png)

The ground truth as well as the AI's predictions after training can be seen in the above image. The accuracy of the segmentation was above 99%.

### Cerebrovascular Segmentation
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

### White Matter Tractography
White matter tractography is a three-dimensional modeling technique employed for the
 visualization of nerve tracts obtained through diffusion MRI. These models play an
 important role in neurosurgical contexts, particularly in the removal of brain tumors, as
 they aid in preserving functional connectivity around eloquent neurological structures and
 essential nerve pathways. Furthermore, a patient-specific white matter tractogram
 significantly enhances surgical planning by providing insights into potential obstructions,
 thereby minimizing the risk of neurological damage.
 ![image](https://github.com/rayhan3333/LiveSurgicalAid/assets/86267840/7ed55925-bf76-4325-ab73-0aeaa9ae1c40)


 At each voxel instance of the diffusion MRI, water diffusion is recorded,
 encompassing both direction and magnitude measurements. The Deterministic Maximum
 Direction Getter (DMDG) algorithm is employed to generate multiple modalities of
 tractography, extracting optimal information. The fractional anisotropy, a quantifiable metric of
 the degree of diffusion, is calculated for every diffusion tensor. White matter tracts,
 characterized by anisotropic diffusion influenced by the myelin sheath barrier, exhibit
 higher fractional anisotropy values in contrast to lower values indicative of isotropic
 diffusion.
 Seed points, selected through a uniform predefined procedure referencing anatomical
 landmarks, play a pivotal role as starting points for the trajectory mapping undertaken by
 the DMDG. This mapping follows the most probable pathway within predefined
 constraints, such as the region of interest. The outcome is a bundle of streamlines
 representing the white matter tractogram, formatted in a vector-based structure
 compatible with widely used 3D visualization software.

 ![image](https://github.com/rayhan3333/LiveSurgicalAid/assets/86267840/df40af26-f073-494c-918e-73e9bfc70f90)

### Augmented Reality Tracking Algorithm
## References

Chidambaram, S., Anthony, D., Jansen, T., Vigo, V., & Fernandez, J. C. (2023). Intraoperative 
augmented reality fiber tractography complements cortical and subcortical mapping. 
World Neurosurgery: X, 20, 100226–100226. 
https://doi.org/10.1016/j.wnsx.2023.100226

Contreras López, W. O., Navarro, P. A., & Crispin, S. (2019). Intraoperative clinical application 
of augmented reality in neurosurgery: A systematic review. Clinical Neurology and 
Neurosurgery, 177, 6–11. https://doi.org/10.1016/j.clineuro.2018.11.018

Fick, T., van Doormaal, J. A. M., Tosic, L., van Zoest, R. J., Meulstee, J. W., Hoving, E. W., & 
van Doormaal, T. P. C. (2021). Fully automatic brain tumor segmentation for 3D 
evaluation in augmented reality. Neurosurgical Focus, 51(2), E14. 
https://doi.org/10.3171/2021.5.focus21200

Fraz, M. M., Remagnino, P., Hoppe, A., Uyyanonvara, B., Rudnicka, A. R., Owen, C. G., & 
Barman, S. A. (2012). Blood vessel segmentation methodologies in retinal images – A 
survey. Computer Methods and Programs in Biomedicine, 108(1), 407–433. 
https://doi.org/10.1016/j.cmpb.2012.03.009

Gsaxner, C., Li, J., Pepe, A., Dieter Schmalstieg, & Egger, J. (2021). Inside-Out Instrument 
Tracking for Surgical Navigation in Augmented Reality. 
https://doi.org/10.1145/3489849.3489863

Hanna, M. G., Ahmed, I., Nine, J., Prajapati, S., & Pantanowitz, L. (2018). Augmented Reality 
Technology Using Microsoft HoloLens in Anatomic Pathology. Archives of Pathology & 
Laboratory Medicine, 142(5), 638–644. https://doi.org/10.5858/arpa.2017-0189-oa

Hart, M. G., Price, S. J., & Suckling, J. (2016). Connectome analysis for pre-operative brain 
mapping in neurosurgery. British Journal of Neurosurgery, 30(5), 506–517. 
https://doi.org/10.1080/02688697.2016.1208809

Hiroshi Iseki, Yoshitaka Masutani, Makoto Iwahara, Takagi, T., Yoshihiro Muragakı, Taira, T., 
Takeyoshi Dohi, & K Takakura. (1997). Volumegraph (Overlaid Three-Dimensional 
Image-Guided Navigation). Stereotactic and Functional Neurosurgery, 68(1-4), 18–24. 
https://doi.org/10.1159/000099897

Jud, L., Fotouhi, J., Andronic, O., Aichmair, A., Osgood, G., Navab, N., & Farshad, M. (2020). 
Applicability of augmented reality in orthopedic surgery – A systematic review. BMC 
Musculoskeletal Disorders, 21(1). https://doi.org/10.1186/s12891-020-3110-2

Kees, J., Marike L D Broekman, Steven De Vleeschouwer, Philippe Schucht, Nahed, B. V., 
Berger, M. S., & Vincent, A. (2022). Safe surgery for glioblastoma: Recent advances and 
modern challenges. Neuro-Oncology Practice, 9(5), 364–379. 
https://doi.org/10.1093/nop/npac019

Lazar, M. (2010). Mapping brain anatomical connectivity using white matter tractography. NMR 
in Biomedicine, 23(7), 821–835. https://doi.org/10.1002/nbm.1579 
Lin, D., Wang, M., Chen, Y., Gong, J., Chen, L., Shi, X., Lan, F., Chen, Z., Xiong, T., Sun, H., 
& Wan, S. (2021). Trends in Intracranial Glioma Incidence and Mortality in the United 
States, 1975-2018. Frontiers in Oncology, 11, 748061. 
https://doi.org/10.3389/fonc.2021.748061

Livne, M., Rieger, J., Aydin, O. U., Taha, A. A., Akay, E. M., Kossen, T., Sobesky, J., Kelleher, 
J. D., Hildebrand, K., Frey, D., & Madai, V. I. (2019). A U-Net Deep Learning 
Framework for High Performance Vessel Segmentation in Patients With Cerebrovascular 
Disease. Frontiers in Neuroscience, 13. https://doi.org/10.3389/fnins.2019.00097

Ma, L., Huang, T., Wang, J., & Liao, H. (2023). Visualization, registration and tracking 
techniques for augmented reality guided surgery: a review. Physics in Medicine and 
Biology, 68(4). https://doi.org/10.1088/1361-6560/acaf23

Meola, A., Cutolo, F., Carbone, M., Cagnazzo, F., Ferrari, M., & Ferrari, V. (2016). Augmented 
reality in neurosurgery: a systematic review. Neurosurgical Review, 40(4), 537–548. 
https://doi.org/10.1007/s10143-016-0732-9

Mikhail, M., Mithani, K., & Ibrahim, G. M. (2019). Presurgical and Intraoperative Augmented 
Reality in Neuro-Oncologic Surgery: Clinical Experiences and Limitations. World 
Neurosurgery, 128, 268–276. https://doi.org/10.1016/j.wneu.2019.04.256

Mohamed Amine Guerroudji, Amara, K., Lichouri, M., Zenati, N., & Mostefa Masmoudi. 
(2023). A 3D visualization‐based augmented reality application for brain tumor 
segmentation. Computer Animation and Virtual Worlds. https://doi.org/10.1002/cav.2223

Naceur, M. B., Saouli, R., Akil, M., & Kachouri, R. (2018). Fully Automatic Brain Tumor 
Segmentation using End-To-End Incremental Deep Neural Networks in MRI images. 
Computer Methods and Programs in Biomedicine, 166, 39–49. 
https://doi.org/10.1016/j.cmpb.2018.09.007

Nils Daniel Forkert, Schmidt-Richberg, A., Fiehler, J., Illies, T., Dietmar Möller, Säring, D., 
Heinz Handels, & Ehrhardt, J. (2013). 3D cerebrovascular segmentation combining fuzzy 
vessel enhancement and level-sets with anisotropic energy weights. Magnetic Resonance 
Imaging, 31(2), 262–271. https://doi.org/10.1016/j.mri.2012.07.008

Ragnhildstveit, A., Li, C., Zimmerman, M. H., Michail Mamalakis, Curry, V. N., Holle, W., 
Baig, N., Ahmet Kaan Uğuralp, Layth Alkhani, Zeliha Oğuz‐Uğuralp, Romero-García, 
R., & Suckling, J. (2023). Intra-operative applications of augmented reality in glioma 
surgery: a systematic review. Frontiers in Surgery, 10. 
https://doi.org/10.3389/fsurg.2023.1245851

Shan, Q., Doyle, T. E., Samavi, R., & Al-Rei, M. (2017). Augmented Reality Based Brain 
Tumor 3D Visualization. Procedia Computer Science, 113, 400–407. 
https://doi.org/10.1016/j.procs.2017.08.356

Syed, T. A., Siddiqui, M. S., Abdullah, H. B., Jan, S., Namoun, A., Alzahrani, A., Nadeem, A., 
& Alkhodre, A. B. (2023). In-Depth Review of Augmented Reality: Tracking 
Technologies, Development Tools, AR Displays, Collaborative AR, and Security 
Concerns. Sensors, 23(1), 146. https://doi.org/10.3390/s23010146

Wang, G., Li, W., Ourselin, S., & Vercauteren, T. (2019). Automatic Brain Tumor Segmentation 
Based on Cascaded Convolutional Neural Networks With Uncertainty Estimation. 
Frontiers in Computational Neuroscience, 13. https://doi.org/10.3389/fncom.2019.00056

Wu, H., Lin, Q., Yang, R., Zhou, Y., Zheng, L., Huang, Y., Wang, Z., Lao, Y., & Huang, J. 
(2019). An Accurate Recognition of Infrared Retro-Reflective Markers in Surgical 
Navigation. Journal of Medical Systems, 43(6). https://doi.org/10.1007/s10916-019
1257-x

Zhang, H., Xia, L., Song, R., Yang, J., Hao, H., Liu, J., & Zhao, Y. (2020). Cerebrovascular 
Segmentation in MRA via Reverse Edge Attention Network. Lecture Notes in Computer 
Science, 66–75. https://doi.org/10.1007/978-3-030-59725-2_7

