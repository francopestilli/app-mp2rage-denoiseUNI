[![Abcdspec-compliant](https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg)](https://github.com/brain-life/abcd-spec)
[![Run on Brainlife.io](https://img.shields.io/badge/Brainlife-brainlife.app.506-blue.svg)](https://doi.org/10.25663/brainlife.app.506)

# app-mp2rage-denoiseUNI

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Denoises the UNI image of a Siemens MP2RAGE acquisition by robust combination with the two inversion images (Marques MP2RAGE scripts, compiled MATLAB), with a user-given or automatically selected regularisation parameter.**

Applies the RobustCombination background-noise suppression of O'Brien/Marques to the MP2RAGE UNI image using the INV1 and INV2 magnitude images. If reg_param is left empty, the App tries a range of values (1 to 96) within a brain mask (user-provided, or made with FSL robustfov and bet) and picks the one where the brain intensities stop changing, using acquisition parameters from the image metadata. Use it before computing T1 and R1 maps (app-mp2rage-calculateT1andR1). Only Siemens MP2RAGE data are supported.

| | |
|---|---|
| 📥 **Inputs** | `neuro/anat/mp2rage` · `neuro/mask` (optional) |
| 📤 **Outputs** | `neuro/anat/mp2rage` |
| 🐳 **Container** | `brainlife/fsl:5.0.9` |
| ⚙️ **Resources** | 1 CPUs |
| 🔗 **Run it** | [doi.org/10.25663/brainlife.app.506](https://doi.org/10.25663/brainlife.app.506) |

#### 📥 Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `neuro/anat/mp2rage` | `neuro/anat/mp2rage` | yes | Siemens MP2RAGE dataset: INV1 and INV2 magnitude images, the UNI image and their JSON sidecars. For automatic parameter selection the sidecars need MagneticFieldStrength, RepetitionTime, InversionTime, BaseResolution, PercentPhaseFOV, PartialFourier and FlipAngle. |
| `neuro/mask` | `neuro/mask` | no | Optional brain mask used when selecting the regularisation parameter; otherwise one is made with FSL bet. Must have the same dimensions as the UNI image. |

#### 📤 Outputs

| Output | Datatype | Description |
|---|---|---|
| `output` | `neuro/anat/mp2rage` | UNI image with noise removed, for use in estimating T1 and R1 values |

<details>
<summary><b>⚙️ Parameters</b> (2)</summary>

| Parameter | Type | Default | Description |
|---|---|---|---|
| `reg_param` | string | `16` | The regularization parameter that is best for your dataset depends on several factors. If you are not sure what regularization parameter to select, leave this field blank and we will select the best parameter for your dataset. |
| `slicesperslab` | number |  | Slices Per Slab should be available in the MRI sequence protocol. It is not always available in the image's header information. If you are sure that Slices Per Slab is available in the image's header information, you can leave this blank and we will get the value from there. Otherwise, please look up this value in the MRI sequence protocol and enter it here. |

</details>

📚 **References used by this App:**
- Marques J. P., Kober T., Krueger G., van der Zwaag W., Van de Moortele P.-F., Gruetter R. MP2RAGE, a self bias-field corrected sequence for improved segmentation and T1-mapping at high field. NeuroImage 49(2):1271-1281 (2010).
- Marques J. P., Gruetter R. New developments and applications of the MP2RAGE sequence - focusing the contrast and high spatial resolution R1 mapping. PLoS One 8(7):e69294 (2013).
- Avesani P. et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. Sci Data 6, 69 (2019). [doi:10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

<!-- brainlife-app:end -->

This app denoises an MP2RAGE_UNI image so that it can be used to calculate T1 and R1 maps (see app-mp2rage-calculateT1andR1). The app is capable of selecting the regularization parameter for the denoising step or the user may provide the parameter.

Currently, only MP2RAGE data collected on Siemens MRI scanners is supported.

# Author
- Sophia Vinci-Booher (svincibo@iu.edu)

Code was adapted for brainlife.io; original version of this code can be found here: 
https://github.com/JosePMarques/MP2RAGE-related-scripts

# Project director
- Franco Pestilli (pestilli@utexas.edu)

# Funding
[![NSF-BCS-1734853](https://img.shields.io/badge/NSF_BCS-1734853-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1734853)
[![NSF-BCS-1636893](https://img.shields.io/badge/NSF_BCS-1636893-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1636893)
[![NSF-ACI-1916518](https://img.shields.io/badge/NSF_ACI-1916518-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1916518)
[![NSF-IIS-1912270](https://img.shields.io/badge/NSF_IIS-1912270-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1912270)
[![NSF-SMA-2004877](https://img.shields.io/badge/NSF_SMA-2004877-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=2004877)
[![NIH-NIBIB-R01EB029272](https://img.shields.io/badge/NIH_NIBIB-R01EB029272-green.svg)](https://grantome.com/grant/NIH/R01-EB029272-01)
[![NIH-T32-HD007475](https://img.shields.io/badge/NIH_T32-HD007475-green.svg)](https://www.nichd.nih.gov/grants-contracts/training-careers/extramural/institutional)

# Citations.
We kindly ask that you cite the following articles when publishing papers and code using this code.

### brainlife.io platform Citations

Avesani, P., McPherson, B., Hayashi, S. et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. Sci Data 6, 69 (2019). https://doi.org/10.1038/s41597-019-0073-y

MIT Copyright (c) 2020 brainlife.io The University of Texas at Austin and Indiana University

### MP2RAGE Citations

Caan, M. W. A., Bazin, P.-L., Marques, J. P., de Hollander, G., Dumoulin, S. O., & van der Zwaag, W. (2019). MP2RAGEME: T1 , T2* , and QSM mapping in one sequence at 7 tesla. Human Brain Mapping, 40(6), 1786–1798.

Marques, J. P., & Gruetter, R. (2013). New Developments and Applications of the MP2RAGE Sequence-Focusing the Contrast and High Spatial Resolution R 1 Mapping. PloS One. https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0069294

Marques, J. P., & Gruetter, R. (2013). New developments and applications of the MP2RAGE sequence--focusing the contrast and high spatial resolution R1 mapping. PloS One, 8(7), e69294.

Marques, J. P., Kober, T., Krueger, G., van der Zwaag, W., Van de Moortele, P.-F., & Gruetter, R. (2010). MP2RAGE, a self bias-field corrected sequence for improved segmentation and T1-mapping at high field. NeuroImage, 49(2), 1271–1281.

### Dependencies

This App only requires singularity to run (https://singularity.lbl.gov/install-request). If you don't have singularity, you will need to install following dependencies:

MATLAB: https://www.mathworks.com/products/matlab.html

