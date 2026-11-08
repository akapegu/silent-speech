# Skin-Mounted Silent Speech Interface — Research & Resource Index

**Updated:** 2026-11-08  
**Project stage:** Research / first sensing prototype  
**Long-term vision:** A small, removable, camera-free, glasses-free skin patch that translates intentional **silent articulation** into continuous, open-vocabulary text. It should not require audible speech. The final anatomical placement (temple, jaw, throat, or elsewhere) is **not decided**.

> **Core distinction:** A wearable that transcribes **voiced speech from body vibration** is not necessarily a wearable that can read **silent mouthing**, let alone subtle closed-mouth articulation. Many impressive papers report closed-vocabulary classification, not unrestricted dictation.

## 1. Research question and non-goals

**Main question:** Can a compact, skin-contact sensor (or combination of sensors) capture sufficient phonetic information during genuine silent articulation to decode previously unseen utterances, including after removing and repositioning the patch?

**Potential modalities:** high-rate skin acceleration, broadband contact vibration, local skin strain/deformation; possibly near-field RF transmission if contact sensing proves insufficient. Training may use synchronized conventional audio, but the intended product must run **without an airborne microphone at inference**.

**Do not confuse:**

| Condition | Meaning | Typical sensor opportunity |
|---|---|---|
| Voiced speech | Speech produced with vocal-fold vibration | Contact microphones, PMUTs, accelerometers |
| Whispering | Articulated speech with reduced/absent periodic vocal-fold vibration | Motion, friction/airflow, some contact signals |
| Silent mouthing | Speech articulation with no audible output | Tissue motion, strain, RF or other articulator sensing |
| Subtle closed-mouth articulation | Intentional tongue/jaw articulation with little visible motion | Difficult; not the same as pure imagined speech |
| Imagined speech | Words imagined without necessarily measurable articulation | Not a supported target of these contact-speech papers |

**First proof:** reproducible, session-held-out discrimination of confusable silent articulations. **Not:** >95% accuracy over ten prerecorded spoken sentences.

## 2. Read these first — core papers

### A. Directly useful for a skin-mounted prototype

1. **SAAS — Machine learning-assisted wearable sensing systems for speech recognition and interaction** (Nature Communications, March 2025)  
   Paper: https://www.nature.com/articles/s41467-025-57629-5  
   Code: https://github.com/DongxiaoLi93/ML-Assisted-Wearable-Speech-Sensing-Systems  
   **Hardware:** flexible throat patch; custom ScAlN PMUT array, low-noise front end, BLE. The paper reports a 10 Hz–20 kHz sensor response and strong classification results in selected voiced-speech tasks.  
   **Why it matters:** an advanced broadband sensing and flexible-packaging benchmark.  
   **Limit:** the prominent 99.8% number is classification of a fixed set of everyday sentences, **not** open-vocabulary silent-speech WER. A custom PMUT is not a sensible first purchase.

2. **STVS — Multimodal deep ensemble classification system with wearable vibration sensor for detecting throat-related events** (npj Digital Medicine, January 2025)  
   Paper: https://www.nature.com/articles/s41746-024-01417-w  
   Full text: https://pmc.ncbi.nlm.nih.gov/articles/PMC11706958/  
   Data: https://doi.org/10.5281/zenodo.12630148  
   Code: https://github.com/yonghunsong/Throat-related-events-classification  
   **Hardware:** soft skin-attached throat vibration sensor using a high-rate TDK IIM-42652 IMU, controller, battery and flexible interconnect.  
   **Why it matters:** practical hardware reference for acquiring throat vibration with a commercial sensor.  
   **Limit:** classifies coughing, swallowing, throat clearing, and speaking; it does **not** transcribe silent words. Reported ~95.96% is event classification accuracy.

3. **TAPS — Throat and Acoustic Paired Speech Dataset for Deep Learning-Based Speech Enhancement** (preprint 2025; subsequent dataset publication)  
   Preprint: https://arxiv.org/abs/2502.11478  
   Project: https://taps.postech.ac.kr  
   Data: https://huggingface.co/datasets/yskim3271/Throat_and_Acoustic_Pairing_Speech_Dataset  
   Hardware + firmware: https://github.com/yhsong06/taps_hardware  
   Baseline ML code: https://github.com/yskim3271/taps-baselines  
   **Hardware:** throat-mounted IMU PCB + synchronized acoustic microphone, STM32 acquisition; hardware includes Altium PCB files and firmware.  
   **Why it matters:** strongest reproducible acquisition reference and paired-signal learning starting point. Try speech-enhancement/representation-transfer baselines before novel models.  
   **Limit:** paired **voiced** speech; not direct proof of silent articulation decoding.

4. **Vibravox — A dataset of French speech captured with body-conduction audio sensors** (Speech Communication, 2025)  
   Dataset: https://huggingface.co/datasets/Cnam-LMSSC/vibravox  
   Hardware information: https://vibravox.cnam.fr/documentation/hardware/  
   **Sensors:** synchronized conventional microphone, forehead accelerometer, temple vibration pickup, throat microphone, and two in-ear setups.  
   **Why it matters:** an existing published basis for comparing body locations, bandwidth and speech information. **Do not spend days rediscovering those same voiced-speech results.**  
   **Important confound:** different body locations use different devices/contact methods. Better performance at one location does not establish the best anatomical site for the same future patch. Also not a silent-mouthing dataset.

5. **Wearable intelligent throat enables natural speech in stroke patients with dysarthria** (Nature Communications, January 2026)  
   https://www.nature.com/articles/s41467-025-68228-9  
   **Hardware/approach:** flexible sensing of throat-related physiological and movement signals combined with language-model processing for communication assistance.  
   **Why it matters:** multimodal sensing and assisted decoding, including what a language model may contribute.  
   **Limit:** a small clinical proof of concept does not imply unrestricted literal transcription of healthy users' silent speech; generated language must be distinguished from faithfully decoded words.

6. **Sensing technologies for silent speech interfaces** (Nature Sensors, January 2026; review)  
   https://www.nature.com/articles/s44460-025-00010-2  
   **Why it matters:** survey of acoustic, optical, strain, EMG, EEG, ultrasonic and other approaches; useful for locating predecessors, device configurations, and performance caveats.  
   **Limit:** review, **not** a new working wearable. Reported accuracies cover incomparable tasks/vocabularies.

### B. Intraoral and acoustic eyewear alternatives

7. **InvisiSpeech** (research project, Nov 2025–April 2026)  
   Project + hardware figures: https://www.yijingjiang.com/work/invisispeech  
   **Hardware visible in the project figures:** tooth-coupled VPU14DB01A voice-pickup unit, NINA-B306 BLE MCU, TPS71818 regulator, BQ25180 power management, 3.7 V / 100 mAh battery, flexible PCB, magnetic charging connector, custom dental brace.  
   **Why it matters:** concrete miniaturization example; a commercial VPU is a sensor candidate worth characterizing.  
   **Limits:** tooth coupling is not skin coupling. Do not assume the VPU works at the temple or that the project establishes unrestricted silent dictation. Do not DIY an intraoral battery device without specialist biocompatibility and electrical/mechanical safety work.

8. **EchoSpeech — acoustic-sensing eyeglasses for silent speech interaction** (Cornell, CHI 2023)  
   Paper: https://czhang.org/assets/pdf/EchoSpeech.pdf  
   Overview: https://news.cornell.edu/stories/2023/04/ai-equipped-eyeglasses-can-read-silent-speech  
   **Hardware:** tiny speakers and microphones on eyeglasses measuring acoustic echo changes from facial motion.  
   **Why it matters:** an independent camera-free silent-articulation path using accessible acoustic parts.  
   **Limit:** original experiments emphasize a constrained command vocabulary and digit sequences, not arbitrary dictation.

9. **SoniSpeech / Cornell open-vocabulary acoustic-sensing research** (2026 lead)  
   Dissertation resource: https://ecommons.cornell.edu/entities/publication/650e92a9-99e6-4053-b87e-4d6edd2a94de  
   **Why it matters:** research into moving from commands to a larger lexicon using acoustic eyewear.  
   **Status:** Revisit the exact paper, dataset availability, recording conditions and WER before using its reported figures as a baseline. This is a follow-up lead, not our selected skin-patch architecture.

10. **QuietSync — integrating multimodal signals for silent speech with head-worn devices** (Microsoft Research)  
    https://www.microsoft.com/en-us/research/publication/quietsync-integrating-multimodal-signals-for-accurate-silent-speech-interaction-with-head-worn-devices/  
    **Why it matters:** another sensor-fusion reference in head-worn silent control.  
    **Limit:** selected commands, not established consumer-grade open vocabulary.

11. **HPSpeech — silent-speech interaction for commodity headphones** (2023)  
    https://keli97.github.io/publication/2023-10-08-HPSpeech-Silent-Speech-Interface-for-Commodity-Headphones  
    **Why it matters:** detects jaw-related changes using headphone acoustics; an alternative form factor.  
    **Limit:** limited command experiments and different sensing geometry.

12. **CSL-EMG Array Corpus** (University of Bremen)  
    https://www.uni-bremen.de/en/csl/research/silent-speech-communication/csl-emg-array-corpus  
    **Why it matters:** continuous physiological signal-to-speech modeling/dataset reference.  
    **Limit:** EMG is **not** the selected sensing modality for this project; useful mainly for decoding methods and evaluation.

## 3. RF silent speech — relevant background, not the present first build

13. **Silent speech command word recognition using stepped frequency continuous wave radar** (Scientific Reports, 2022; Dresden)  
    https://www.nature.com/articles/s41598-022-07842-9  
    Referenced code: https://github.com/TUD-STKS/radar_based_command_word_recognition  
    **Why it matters:** RF measurements affected by vocal-tract configurations; published engineering precedent relevant to Subvocal's claimed sensing physics.  
    **Limit:** limited-vocabulary research, distinct from proving continuous consumer silent dictation. Read the full protocol carefully before comparing reported accuracy.

14. **Electromagnetic sensing of the vocal tract** (Birkholz et al., 2018)  
    https://www.vocaltractlab.de/publications/birkholz-2018-ieee-taslp.pdf  
    **Why it matters:** transmission/impedance sensing precedent; antenna positioning, dielectric coupling and frequency dependence.  
    **Status:** Confirm exact hardware specifications from the original text before choosing RF parts.

15. **Towards contactless silent speech recognition using IR-UWB radar** (2016)  
    https://pmc.ncbi.nlm.nih.gov/articles/PMC5134471/  
    **Why it matters:** earlier contactless lip/jaw motion-based silent-word recognition.  
    **Limit:** external articulator measurement, not necessarily internal tongue/soft-palate detail.

16. **Pushing the limits of remote RF sensing by reading lips under the face mask** (Nature Communications, 2022)  
    https://www.nature.com/articles/s41467-022-32231-1  
    **Why it matters:** Wi-Fi/radar vowel-related lip-motion recognition in a restricted setting.  
    **Limit:** five vowels plus a rest condition from a small group; not full phonetic decoding.

17. **The Subvocal Company — YC launch + founders' technical comments** (2026)  
    Launch: https://www.ycombinator.com/launches/Wf9-the-subvocal-company-talk-without-talking  
    Website: https://subvocal.company/  
    Founder discussion: https://news.ycombinator.com/item?id=50340088  
    Demo: https://www.youtube.com/watch?v=9QdX1eObVYI  
    **Founder-described approach:** low-noise RF sensing, fields through facial tissue, antenna geometry optimized for tongue/lips/soft palate, first face-mounted antennas, then rigid rig, then glasses; large pretraining dataset for cross-user generalization.  
    **Founder-reported negative result:** 60 GHz reflection radar did not provide sufficient internal articulator information for their objective.  
    **Limits:** precise RF frequency, transceiver, antenna layouts, dataset size, raw WER and end-user robustness have not been independently established here. Treat launches/demos as company claims, not peer-reviewed performance.

## 4. Companies and product context

| Organization | Link | Why to track | Caution |
|---|---|---|---|
| **Temple** | https://www.temple.com/vision | Skin-attached temple device; company says motion sensors read wearer-generated voice vibration without a conventional microphone | Public material does **not** establish decoding of fully silent articulation, nor its exact sensor/ASR stack |
| **Subvocal** | https://subvocal.company/ | RF silent articulation to text in glasses | Company-reported performance; different form factor |
| **AlterEgo** | https://www.alterego.io/ | MIT-origin silent speech / neuromuscular-interface precedent | Different sensor and ergonomic tradeoffs |
| **InvisiSpeech** | https://www.yijingjiang.com/work/invisispeech | Tiny dental form factor with commercial VPU and BLE | Research prototype, not an approved DIY dental product |
| **Skyted** | https://www.skyted.io/ | Alternative approach to more private/quiet voiced communication | Not equivalent to silent articulation |
| **Naqi Logix** | https://www.naqilogix.com/naqiplatform | Ear-based hands-free/voice-free control | Not established full speech transcription |
| **SilentSpeak** | https://silentspeak.io/ | Emerging facial biosignal silent interface | Independently verify maturity and actual results |
| **Silenzio** | https://silenzio.io/ | Emerging silent-language interface | Independently verify maturity and actual results |
| **Venuvo** | https://venuvo.co/ | Wearable voice-restoration adjacent concept | Independently verify maturity and actual results |

**Why Subvocal attracted attention despite earlier research:** accessible consumer pitch (dictation without speaking), apparent continuous-language demonstration, compact prospective product, and YC distribution. Going viral does not establish scientific novelty or field-leading measured WER.

## 5. Components and hardware reference list (candidates, not an approved BOM)

| Component / platform | Source | Purpose / caution |
|---|---|---|
| **TDK IIM-42652** | STVS + TAPS papers; TAPS hardware repo | High-rate accelerometer reference for skin vibration; verify exact supported ODR, filtering, throughput and available boards before purchase |
| **VPU14DB01A** | InvisiSpeech project diagrams | Tooth-coupled digital voice-pickup unit; verify datasheet, availability, mounting, interface, and usefulness on **skin** |
| **ADXL1002** | https://www.analog.com/en/products/adxl1002.html | Analog wideband acceleration baseline; sensor noise, analog conditioning and coupling require testing |
| **STM32 + high-rate acquisition** | https://github.com/yhsong06/taps_hardware | Reference synchronized wearable acquisition and firmware |
| **Piezo/contact pickup + high-impedance analog front end** | Experimental alternative | Test bandwidth and mechanical coupling, not just datasheet specs |
| **Deformation / strain sensor** | Intelligent Throat + review | Potentially useful when there is no vocal-fold vibration; first validate its phonetic discrimination contribution |
| **Custom ScAlN PMUT array** | SAAS paper | Advanced research benchmark; **not** an initial purchasing/fabrication choice |
| **Near-field coherent RF measurement** | Dresden/Birkholz/Subvocal references | Backup sensing pathway if contact-only information proves insufficient; avoid buying 60 GHz radar simply because it is available |

**Safety:** Use safe, isolated/battery-powered body-contact measurement systems with suitable skin-contact materials. Do not put mains-referenced experimental electronics on the body; do not self-build an intraoral powered device; assess RF exposure/compliance before head-mounted transmitters.

## 6. ML and evaluation resources

**Useful code/data:**
- TAPS model baselines: https://github.com/yskim3271/taps-baselines
- TAPS paired dataset: https://huggingface.co/datasets/yskim3271/Throat_and_Acoustic_Pairing_Speech_Dataset
- Vibravox dataset: https://huggingface.co/datasets/Cnam-LMSSC/vibravox
- SAAS released code: https://github.com/DongxiaoLi93/ML-Assisted-Wearable-Speech-Sensing-Systems
- STVS event-classification code: https://github.com/yonghunsong/Throat-related-events-classification
- Speech-decoding alternatives to investigate: temporal CNN/TCN, Conformer + CTC, transducer decoders, teacher/student transfer from ordinary audio, sensor-only sequence-to-text evaluation.

**Evaluation rules:**
1. Separate normal voiced, whispered, silently mouthed and subtle closed-mouth conditions.
2. Start with deliberately confusable phonetic pairs, not five easy commands.
3. Hold out sessions with full sensor removal/repositioning; do not leak adjacent windows between splits.
4. For open vocabulary, hold out **sentences** and include numbers, names, uncommon words and negative activity.
5. Report balanced accuracy for controlled tasks, phoneme error rate and word error rate for sequential language, false activations/hour, latency and rewearing drop.
6. Evaluate raw sensor models **before** language-model correction; check whether plausible model outputs match the actual spoken intention.
7. During collection, conventional audio is permitted as synchronized **training reference** where appropriate. Remove it completely from the final inference path.
8. A larger model cannot recover a distinction not present in the measured physical signal.

## 7. What we have decided / what remains unknown

### Agreed working choices
- Target a **skin-mounted patch**, not a pair of glasses, a camera device or an EMG-only interface.
- Initial prototype should test **high-rate acceleration/contact vibration**, with slow deformation as a possible complementary modality.
- Use the IIM-42652 **research implementation** in STVS/TAPS as an acquisition reference rather than immediately fabricating a new MEMS sensor.
- Published Vibravox analyses already cover much of the **voiced speech** body-position comparison; do not blindly replicate them.
- Begin with meaningful **signal information** and sensor-only phonetic discrimination; delay flex-PCB, BLE, battery optimization and model scaling.

### Open questions that decide whether this is a viable startup
1. Does a small skin contact point capture sufficient **genuinely silent** articulatory information?
2. If yes, which location—jaw, throat, temple or other—has the best information/comfort tradeoff?
3. Does a second sensor (strain/another vibration position) recover critical missing phonetic classes?
4. Is it robust after remounting, sweat, head movement, eating and prolonged wear?
5. Can a model transcribe unconstrained, never-seen sentences with practical WER and minimal user calibration?
6. Would users prefer a patch over glasses enough to tolerate adhesives, cleaning/charging and placement?

## 8. Reading order / immediate next action

1. **STVS + TAPS hardware:** inspect exact IMU ODR, data path, sensor mounting, board schematics, isolation and part sourcing.  
2. **SAAS:** inspect how its broadband PMUT captures information that the IMU may miss; note that its high reported classification accuracy is not continuous dictation.  
3. **Intelligent Throat + silent-speech review:** inspect strain modalities and task definitions, especially silent vs voiced conditions.  
4. **InvisiSpeech:** inspect VPU integration/physical coupling; **do not** assume tooth-mount results transfer to a temple patch.  
5. **Build a purchase-ready, *minimal* acquisition BOM** only after checking the actual IMU board/module options. Then collect our own genuine silent articulation recordings across two or three placements and at least three independent sessions.

**Decision rule:** If silent articulatory distinctions are not stable after remounting, change sensor placement/coupling/modality *before* expanding the ML model or buying miniaturization hardware.

---

## 9. Additional resources encountered (secondary / not all deeply audited)

These came up while exploring broader form factors and alternate sensing physics. They are useful context, **not** endorsements or first-build dependencies.

- **Temple vision / microphone-free voiced interface:** https://www.temple.com/vision
- **Microsoft QuietSync:** https://www.microsoft.com/en-us/research/publication/quietsync-integrating-multimodal-signals-for-accurate-silent-speech-interaction-with-head-worn-devices/
- **HPSpeech:** https://keli97.github.io/publication/2023-10-08-HPSpeech-Silent-Speech-Interface-for-Commodity-Headphones
- **Cornell EchoSpeech:** https://czhang.org/assets/pdf/EchoSpeech.pdf
- **Cornell SoniSpeech research:** https://ecommons.cornell.edu/entities/publication/650e92a9-99e6-4053-b87e-4d6edd2a94de
- **Bremen CSL-EMG corpus:** https://www.uni-bremen.de/en/csl/research/silent-speech-communication/csl-emg-array-corpus
- **TAPS release:** https://taps.postech.ac.kr
- **Dresden RF project code (verify availability):** https://github.com/TUD-STKS/radar_based_command_word_recognition
- **CMU Pantœnna antenna-impedance facial sensing (paper lead):** https://www.futureinterfaces.com/research
- **SilentWear sEMG (alternative sensing, not current plan):** https://github.com/pulp-bio/SilentWear
- **UWB and Wi-Fi facial motion papers:** listed in §3

### Verification legend

- **Directly checked in this README preparation:** SAAS, STVS, silent-speech review, Intelligent Throat, TAPS hardware/baselines, Vibravox dataset card, InvisiSpeech project, the 2022 Dresden RF paper, 2016 IR-UWB radar paper, 2022 masked RF lip-reading paper, and Temple's public vision statement.
- **Discussed in our earlier research; revisit originals before making component or performance decisions:** select acoustic wearables, SoniSpeech dissertation details, 2018 vocal-tract electromagnetic engineering specifics, secondary companies' maturity, and some model-specific benchmark claims.

*This is a working research index, not a validated parts list, patent freedom-to-operate opinion, or evidence that the proposed silent-speech patch has already been demonstrated.*
