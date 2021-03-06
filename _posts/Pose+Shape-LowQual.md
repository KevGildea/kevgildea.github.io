#### 3D Human Shape and Pose from a Single Low-Resolution Image with Self-Supervised Learning

3D human shape and pose estimation from monocular images has been an active area of research in computer vision, having a
substantial impact on the development of new applications, from activity recognition to creating virtual avatars. Existing deep learning methods for 3D human shape and pose estimation rely on relatively highresolution input images; however, high-resolution visual content is not
always available in several practical scenarios such as video surveillance
and sports broadcasting. Low-resolution images in real scenarios can vary
in a wide range of sizes, and a model trained in one resolution does not
typically degrade gracefully across resolutions. Two common approaches
to solve the problem of low-resolution input are applying super-resolution
techniques to the input images which may result in visual artifacts, or
simply training one model for each resolution, which is impractical in
many realistic applications.
To address the above issues, this paper proposes a novel algorithm called
RSC-Net, which consists of a Resolution-aware network, a Self-supervision
loss, and a Contrastive learning scheme. The proposed network is able to
learn the 3D body shape and pose across different resolutions with a single model. The self-supervision loss encourages scale-consistency of the
output, and the contrastive learning scheme enforces scale-consistency of
the deep features. We show that both these new training losses provide
robustness when learning 3D shape and pose in a weakly-supervised manner. Extensive experiments demonstrate that the RSC-Net can achieve
consistently better results than the state-of-the-art methods for challenging low-resolution images.


http://www.ecva.net/papers/eccv_2020/papers_ECCV/papers/123540273.pdf

