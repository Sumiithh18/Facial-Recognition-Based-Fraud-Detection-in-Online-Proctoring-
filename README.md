Fraud detection using facial recognition in online proctoring

ABSTRACT:
Online examinations play a pivotal role in the realm of e-learning, having witnessed substantial growth in recent
times. However, the pervasive issue of cheating in online exams remains a global concern, transcending
developmental disparities. In response to this challenge, this paper introduces an innovative and robust face
liveness detection method aimed at discerning between authentic and fraudulent users, with a specific emphasis
on the identification of spoof attacks. The proposed system leverages the light reflection concept to effectively
distinguish between a genuine facial image and a photograph. This discrimination is especially crucial during
moments when examinees are recording videos or capturing images during examinations. The face detection
component of the system is implemented through the application of the Haar cascade technique, while Support
Vector Machines (SVM) are deployed for the purpose of face recognition. To enhance the overall accuracy of the
system, the Local Binary Pattern (LBP) filter technique is incorporated, specifically targeting the detection of light
reflection in images. This multi-faceted approach not only addresses the current challenges associated with online
exam integrity but also contributes to the advancement of face fraud detection methodologies in
educational technology.
INTRODUCTION
In the rapidly evolving landscape of education, online examinations have emerged as a pivotal component of e-
learning, witnessing unprecedented growth. The advent of online assessment platforms provides flexibility and
accessibility, especially in the face of global challenges like the COVID-19 pandemic. However, this convenience
brings forth a critical issue—cheating in online exams has become a pervasive concern worldwide, transcending
geographical and developmental boundaries.

The essence of remote examination processes lies in their feasibility, making them an attractive option for
primary, secondary, and higher education levels, particularly during the uncertainties presented by the COVID-19
situation. Yet, the absence of physical proctors and the remote nature of online exams create an environment
conducive to malpractice, challenging the authenticity of the results obtained through these assessments.

Traditional methods of ensuring exam integrity, such as on-site invigilation, become impractical in the digital
realm. As a result, institutions and educators are compelled to explore innovative solutions to mitigate the rising
tide of cheating during online assessments. In response to this imperative, the presented paper proposes a
comprehensive and sophisticated face fraud detection system tailored for online exams.

Face recognition, a widely adopted biometric approach, emerges as a potential solution to enhance
authentication processes in online exams. However, the susceptibility of face recognition systems to spoof attacks
poses a significant limitation. Spoof attacks involve presenting non-real faces, such as photographs, which can
deceive the system and compromise its integrity.

The authors introduce a robust face liveness detection method as a countermeasure to this vulnerability. This
method aims to discern between legitimate and illegitimate users by honing in on the critical task of identifying
spoof attacks. By leveraging the light reflection concept, the proposed system distinguishes between a genuine
facial image and a static photograph. This distinction becomes particularly crucial during the examination, where
examinees may attempt to manipulate the system by presenting fraudulent images or videos.

The system&#39;s approach integrates advanced techniques, including the Haar cascade for face detection and
Support Vector Machines (SVM) for face recognition. Additionally, the Local Binary Pattern (LBP) filter technique is

Fraud detection using facial recognition in online proctoring

employed to effectively detect light reflection in images, adding an extra layer of sophistication to the fraud
detection process.

As education increasingly relies on digital platforms, securing the integrity of online assessments becomes
paramount. The authors&#39; innovative approach not only addresses the current challenges associated with online
exam authenticity but also contributes to the ongoing evolution of face fraud detection methodologies within the
realm of educational technology. Through this paper, the authors seek to provide a robust and effective solution
to the pressing issue of cheating in online exams, ultimately fortifying the credibility of online education
assessments.
The objectives of the proposed work are as follows:
To implement the robust face liveness detection system for detection of spoof attacks.
To differentiation between legitimate and illegitimate examinee during examination.
To detect the photo image and real face of examinee during an examination.

Latest Technique used and its Challenge :
TECHNIQUES (AS FOR 2022):
3D Facial Recognition:
Traditional 2D facial recognition can be vulnerable to spoofing attempts using printed photos. 3D facial
recognition technology uses depth information to create a more accurate representation of the face, making it
more resistant to such attacks.
Behavioral Biometrics:
This involves analyzing the user&#39;s behavioral patterns during the exam, such as typing speed, mouse movements,
and gaze direction. Deviations from the baseline behavior may trigger alerts for further investigation.
Multi-Modal Biometrics:
Combining multiple biometric modalities, such as facial recognition, voice recognition, and fingerprint scanning,
enhances the overall security of the online proctoring system. It makes it more challenging for fraudsters to
bypass the authentication process.
AI-Based Liveness Detection:
Leveraging artificial intelligence for liveness detection involves analyzing various facial expressions, eye
movements, and other factors to ensure that the person being monitored is actively participating in the exam and
not using pre-recorded videos or photos.

Challenges:
Spoofing and Presentation Attacks:
One of the persistent challenges is the ability of fraudsters to use sophisticated methods to spoof facial
recognition systems. This includes using high-quality photos, videos, or 3D masks to deceive the system.
User Privacy Concerns:
Facial recognition raises privacy concerns, and some users may be uncomfortable with the idea of having their
biometric data collected and stored. Striking a balance between security and privacy is crucial.

Fraud detection using facial recognition in online proctoring

Algorithm Bias and Fairness:
Facial recognition algorithms may exhibit biases, leading to inaccuracies or unfair treatment of certain
demographic groups. Addressing algorithmic bias is an ongoing challenge in the field of facial recognition.
Liveness Detection Accuracy:

While AI-based liveness detection has improved, there is still a need for highly accurate methods to differentiate
between genuine user interactions and sophisticated spoofing attempts.
Ethical Considerations:
The use of facial recognition in educational settings raises ethical concerns, including consent, transparency, and
the potential for misuse. Striking the right balance between security and ethical considerations is a complex
challenge.
Adversarial Attacks:
Adversarial attacks involve attempts to manipulate or deceive the facial recognition system by exploiting
vulnerabilities in the algorithm. Ongoing research is needed to develop more robust and resilient systems.
Regulatory Compliance:
Adhering to evolving data protection and privacy regulations worldwide is an ongoing challenge. Keeping up with
the legal landscape and ensuring compliance is crucial for the implementation of facial recognition in online
proctoring.

PROPOSED SYSTEM
System Design:
In face recognition systems, replay attacks where a pre-recorded video of the user is played and a printed
photograph is placed infront of the camera are the two most common ways to do the fraud while attending the
examination. The proposed solution helps todetect the fraud that happens in examination and maintain its
integrity and genuinity of the result in the online examination. Figure1 shows the design of the system

The module wise working of the proposed design is given below:
Image/Video from Live Camera:
The camera takes a live video and grabs images of examinees attending onlineexamination using a camera with a
specific time interval. The camera act as a sensor to collect the face biometricfor processing. The frame extraction
is done from the video and sends it to the application server for matching.
Face Detection:
The Haar cascade Classifier is used for face detection from images. The captured image isanalysed to determine
whether it is real or fake

Image Pre-Processing:
Image preprocessing techniques such as noise removal, normalization, or RGB to GrayScale Image are applied on
the detected face, to get fine tune image. The image is converted into Grayscale bytaking the average of each
pixel RGB.

Fraud detection using facial recognition in online proctoring

LBP (Local Binary Patterns Histograms) Feature Extraction:
The Gabor filters are used for feature extractionfrom an image. These features like Eyes, Nose, and Mouth
Location provide us the changes in the face due tolight reflection on an image.
Feature Extraction:
Recognition of the face is done by using SVM classifier on the LBP facial features. Byrecognizing the face,
difference between the actual face and the photograph is identified as the images that arecaptured from an
image or videos tend to have less colour when they are recaptured. The certain colour texture islost when an
image is captured from another image. Such change is identified by the SVM algorithm.
Alert Notification:
The system help us to detect fraud faces using light reflection patterns on a human face usingthe knowledge that
every object reflects light differently. It Identify Genuine/ Photograph Faces if such facedetected an alert
notification is send to the admin.
