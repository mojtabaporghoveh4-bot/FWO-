# ATTUNE

## Learning transferable personal models of cognitive response to task interventions

Mojtaba Porghoveh | Scientific working revision | 18 September 2026

This revision develops the scientific core of ATTUNE in response to the closest literature. It tests whether personal cognitive-response dynamics are reproducible, whether a resource-aware task representation supports transfer, and whether useful intervention predictions survive removal of EEG from operational sensing. The original MSCA host, career and 24-month planning context is retained as source material. This is not a completed FWO application or a submission-formatted MSCA document.

# 1 Excellence

## 1 1 Research objectives and advance beyond the state of the art

People supervising robots or prioritizing time-critical requests must divide attention between concurrent activities. Assistance can reduce task demands, but can also introduce interruptions or compete with the resources needed for another activity [4,10]. A useful adaptive system must therefore predict how a feasible task intervention will affect workload and performance, while recognizing when its prediction is unreliable.

ATTUNE builds on my rolling-horizon task-allocation work [11]. Its scientific problem is whether a compact model identified for one operator captures reproducible response dynamics rather than the particular task and session used for calibration. This matters because a controller trained in one setting may otherwise give confident but misleading advice when the interface, task or available measurements change.

### Established capabilities and the remaining gap

Workload estimation from EEG and other physiological measurements, including subject-specific models, is established [1-3,8,9]. Predictive operator-state adaptation and personalized physiological control also have precedents [17,18]. ATTUNE therefore does not claim that moving from reactive monitoring to predictive adaptation is itself new.

Chand et al. combine personalized fatigue modelling, vision-based operational information, wearable indicators and fatigue-sensitive scheduling [14]. Xue et al. update fatigue-model parameters online, predict fatigue for candidate tasks and constrain allocation decisions [15]. Their reported simulation-based evaluation leaves open the empirical identification of cognitive dynamics from indirect measurements in people. Vallée formalizes causal digital twins and personalized intervention reasoning as a conceptual framework [16]. Together, these studies establish substantial overlap with the general monitor-personalize-predict-adapt architecture.

The gap targeted here is whether a small set of personal cognitive-response parameters can be identified reproducibly, improve predictions under experimentally assigned interventions, and remain useful across tasks when operational measurements are reduced to eye tracking and task information. The cited studies do not establish this combined capability. The contribution will be evidence about the conditions and limits of this capability, rather than a claim of universal transfer or first-ever predictive personalization.

### Why the task representation matters

The original task-demand variables - monitoring, attention switching, time pressure and decision difficulty - will remain candidate descriptors. They are not Wickens's four resource dimensions. Multiple-resource theory distinguishes processing stages, processing codes, sensory modalities and visual channels, and explains interference through demand and resource competition [4]. ATTUNE will test whether explicitly representing resource overlap adds information beyond demand magnitude. For example, matched monitoring tasks can impose different interference when they compete for focal visual processing. This theoretical explanation is a hypothesis to test, not a direct measurement of workload.

### Aim and hypotheses

The aim is to identify when personal cognitive-response models support reliable intervention predictions across sessions, tasks and sensing conditions. Workload is the primary state and performance is an independently evaluated outcome. Stress and mental fatigue are exploratory outcomes and will not expand the primary controller into a three-state model.

H1 Reproducibility. A recoverable subset of personal response parameters will improve held-out intervention predictions relative to shared population parameters, and retain useful predictive value on a separate day without parameter refitting.

H2 Transfer through task representation. A model using cognitive demands and resource overlap will preserve more of its personal predictive advantage in a second task than demand-only and task-specific representations, with personal dynamics fixed after calibration.

H3 Sensing sufficiency. Following multimodal calibration, an observer using eye tracking and task logs will retain useful intervention-prediction accuracy relative to independent workload and performance measurements. Comparisons will establish whether eye measurements and EEG teaching each add value beyond task information alone.

### Objectives and evidence of success

Objective 1 is to construct and test demand-only and resource-aware task representations. Success requires verified task contrasts, reproducible coding rules and improved held-out prediction when resource overlap is added. Failure to improve prediction will count against H2 rather than be hidden by retaining extra features.

Objective 2 is to identify the smallest useful personal model. Simulation-based parameter recovery, repeated-session prediction and held-out intervention accuracy will jointly determine which parameters are individualized. A parameter that cannot be recovered or adds no reliable predictive value will remain shared or be removed if its mechanism is unnecessary.

Objective 3 is to test intervention-response predictions and their decision value. Randomized feasible interventions will support comparisons of observed responses with pre-action forecasts. A subsequent counterbalanced controller experiment will test workload benefit and performance preservation under a prespecified noninferiority margin.

Objective 4 is to separate transfer of personal dynamics from transfer of the observation model. A frozen model will first be evaluated in a second task using rich measurements for diagnosis; operational predictions will separately use eye tracking and logs. Any recalibrated result will be reported as a distinct secondary analysis.

ATTUNE's intended advance is an experimentally tested relationship between task representation, reproducible personal dynamics and the sensing needed for useful adaptation. The control prototype provides a test of that knowledge. It does not by itself constitute the novelty claim.

## 1 2 Methodology

### Stage 1 Define demand and resource representations

Robot supervision is the primary experimental setting. Building-maintenance prioritization provides a bounded transfer test with different task content. Both will use a common manual defining monitoring requirements, switching events, time pressure and decision difficulty from task settings and logs [5]. The manual will additionally describe each concurrent activity's processing stage, code, modality and visual-channel demands where these can be meaningfully manipulated [4]. A prespecified overlap score will summarize the resources shared by concurrent activities; it will not be treated as a validated physiological workload scale.

Pilot contrasts will manipulate demand magnitude and resource overlap as independently as practicable. Candidate manipulations include presenting competing information through different channels, changing the concurrency of secondary monitoring, and altering task pacing. Interface content, alert salience and response requirements will be matched or recorded so that a modality effect is not automatically attributed to resource competition. Independent coding and participant manipulation checks will assess whether the intended contrasts were achieved. Correlated descriptors will be combined or removed before the main study.

Three representations will be compared: task-specific condition labels, the original demand descriptors, and demand descriptors plus resource overlap. The task-specific model serves as a within-task comparator; a transferable common-representation model is necessary for the frozen cross-task test. Adding action identity and relevant context to the demand-based models will test the assumption that the representation captures the effects of an intervention. Residual action effects would indicate missing mechanisms, such as interruption or changes in situation awareness.

### Stage 2 Calibrate and repeat across sessions

Approximately 25 adults remains a provisional feasibility target inherited from ATTUNE. Before recruitment is finalized, pilot-informed simulations will assess parameter recovery, the precision of the primary paired model comparison and the planned performance margin, allowing for participant loss and temporal dependence. Repeated sensor windows will not be counted as independent participants. If the feasible sample cannot support the proposed claims, the model and confirmatory contrasts will be reduced before preregistration.

Calibration will record synchronized EEG, eye tracking and task performance during randomized, balanced changes in demand and resource overlap. Brief workload ratings will be collected at fixed outcome points; NASA-TLX will assess whole-run workload [6]. Stress and fatigue ratings will remain exploratory. The observation protocol will record luminance, gaze geometry, head movement and tracking quality where relevant, because changes in these variables can alter eye measurements without equivalent changes in workload [8,9].

A separate-day session will evaluate predictions with personal dynamics fixed after the first calibration. This is the primary reproducibility test. Refitting a model to the repeat session may be used for a secondary stability analysis, but those estimates will not replace the frozen parameters in the primary test. Data-quality and missingness rules, visit burden and replacement recruitment will be fixed before confirmatory collection. Session-specific sensor baselines will be distinguished explicitly from personal dynamic parameters.

### Stage 3 Identify compact personal dynamics and operational sensing

The candidate model is a bounded nonlinear state-space model with workload as its primary latent state. In compact notation, x_i(t+1) = f(x_i(t), d_t, r_t; theta_i) + process noise, where d_t describes demand, r_t describes resource overlap and theta_i contains personal response parameters. For a candidate action, the forecast uses the corresponding future demand and overlap trajectory. Performance has a separate observation or prediction model; reducing predicted workload alone is not sufficient to select an action.

The starting personal dynamic model will have three candidate parameters: demand sensitivity, resource-overlap sensitivity and a workload response or recovery time constant. Shared coefficients will combine the retained demand descriptors. Additional personal gains will be considered only if the design supports recovery and they improve held-out prediction. Eye-observation baselines and scale parameters will be counted separately. This replaces the initial commitment to 21 candidate personal parameters across workload, stress and fatigue.

Workload-state scaling will be anchored by a prespecified measurement model and rating scale so that latent-state scale changes cannot masquerade as changes in personal sensitivity. Recovery tests will assess parameter confounding and uncertainty under the actual planned interventions and noise levels. These tests establish identifiability only within the tested model class; they do not prove that the model uniquely describes cognition. A hierarchical model will allow partial pooling, retaining shared values when individual estimates are weak.

Multimodal calibration can supply teacher estimates for an eye-plus-logs student observer, but teacher outputs are uncertain estimates, not ground truth. Models will be evaluated on held-out subjective workload and task performance. Future ratings, future performance and post-intervention EEG will not enter a forecast made before the intervention. Any rich-sensing comparison must use only measurements available at that same decision time. Agreement with the teacher will be a diagnostic of information transfer, not the primary validity criterion.

The sensing comparisons are task logs alone, eye tracking plus logs learned without teacher supervision, eye tracking plus logs with multimodal teaching, and the rich-sensing model. They will use comparable model capacity and training budgets. This establishes whether operational eye sensing adds information and whether the EEG-based calibration step is necessary. If teaching gives no useful advantage, ATTUNE will report that result and retain the simpler calibration procedure.

Population structure and feature selection will be learned without the test participant's evaluation data. Personalization will use only that participant's designated calibration runs. Hyperparameter selection will be nested within training data. Entire runs and sessions will be held out, preventing leakage between adjacent windows. Parameter personalization requires recovery in simulation, repeat-session utility and improved held-out prediction, with uncertainty reported for each comparison.

### Stage 4 Test intervention predictions before testing control

At predefined eligible decision points, the system will forecast outcomes under each feasible reversible intervention and under no change. The primary horizon remains 60 seconds; 30 and 120 seconds are secondary horizons. The intervention set will be limited to pilot-validated changes in presentation, secondary-task demand and pacing. Broad changes in autonomy or allocation will not be included unless their effects can be represented and evaluated with the same protocol.

One eligible action will then be assigned at random with its assignment probability logged. Decision points will be spaced to avoid overlapping primary outcome windows, and intervening changes, carryover, prior actions and operator refusals will be recorded. The protocol will specify whether the assigned arrangement is maintained through the horizon, apart from safety or participant overrides. Outcome collection will follow the same timing in every condition.

The primary forecast assessment concerns the outcome under the action actually assigned. Action contrasts will also be evaluated across repeated randomized occasions, accounting for participant and session dependence. These data support intervention-effect estimates under the tested eligibility, adherence and carryover conditions. They do not reveal both potential outcomes for one person at one instant. Assignment-based effects are primary when refusal is possible; analyses based on the action received require additional assumptions and will be labelled secondary [16].

Comparators will include persistence, a shared-parameter dynamic model, a simple personalized linear dynamic model, and action-conditioned recurrent forecasting models such as LSTM or GRU. Forecasting models will receive the same available history, candidate-action information and training partitions. The prespecified comparison sequence will test personalization, then resource representation, then sensing reduction. Prediction error, calibration and uncertainty in between-model differences will be reported at the participant level. Exploratory comparisons will be identified separately.

In a subsequent counterbalanced experiment, participants will experience no-change, reactive and predictive control. Reactive and predictive controllers will have the same feasible action set and comparable access to current observations. Workload benefit will be evaluated with held-out ratings and run-level outcomes rather than solely with the controller's own workload score. Task errors and timely completion will be evaluated against pilot-justified noninferiority margins fixed before the main test. Absence of a statistically significant performance decline will not count as evidence of preservation.

The predictive controller will act only when the forecasted benefit is sufficiently certain and the performance constraint is met; otherwise it will retain the current arrangement. Interval calibration and the resulting action rate will be assessed on held-out sessions. Prespecified tracking-quality and out-of-support checks will trigger abstention. Coverage and failure rates will be reported again after task transfer, because source-task calibration does not guarantee valid uncertainty in a new context. Operators will be able to reject changes throughout.

### Stage 5 Separate dynamic transfer from sensing transfer

The same participants will complete the shorter building-maintenance task, prioritizing requests using urgency, deadlines and affected occupants without requiring technical repair knowledge. A separate pilot will fix the new task's demand and resource coding before transfer evaluation. Personal dynamics, operational observation parameters and preprocessing will remain frozen for the primary end-to-end test; permitted instrument calibration will be specified and will not use workload labels to update the model.

Transfer will be evaluated in two ways on the same planned task conditions. First, rich measurements will remain available for diagnostic evaluation of response dynamics and the measurement model. Second, the operational forecasts will use only eye tracking and logs. Diagnostic use of rich measurements does not constitute operational EEG use and will not provide future information to predictions. This separation helps identify whether a loss of accuracy reflects changed response dynamics, changed eye-state relationships or an inadequate task representation.

The primary transfer result will compare frozen personal and population models and quantify degradation relative to the source task. Demand-only and resource-aware versions will test H2. Any later recalibration of the observer, dynamics or demand mapping will be performed separately and will report its data requirement. Successful transfer between these two tasks will support bounded reuse; it will not establish application-independent or workplace validity.

### Analysis integrity and responsible research

Hypotheses, primary contrasts, outcome timing, exclusions, performance margins, data splits and abstention rules will be preregistered. Workload ratings are imperfect measurements; performance and physiological measures will supply complementary evidence rather than be merged into an unquestioned reference score. Uncertainty estimates will account for repeated measures and participant clustering. Model complexity and claims will be reduced if the data cannot distinguish the intended mechanisms.

Human factors provides the resource-competition hypothesis; HCI supports manipulation validity and operator control; system identification tests personal dynamics; machine learning supports observation models and fair predictive comparisons. Recruitment will consider sex, gender and age where feasible, and corrective eyewear will be recorded with consent. Signal quality and model errors will be examined across these factors without claiming well-powered subgroup effects from a small study.

Studies will use controlled VR tasks with ethics review, breaks and stopping procedures for discomfort or excessive burden. Protocols, code, demand manuals, model cards and suitable derived or synthetic data will follow FAIR principles [7]. Physiological and behavioural data will be pseudonymized and stored under the host's approved governance. ATTUNE estimates task-related workload; it will not infer emotions or support employment scoring.


## 1 3 Supervision training and knowledge exchange

Supervision and scientific fit. Associate Professor Hendrik Knoche provides the expertise ATTUNE needs in human-computer interaction, human-robot interaction, participatory design, eye tracking, VR, BCI and experimental evaluation. His expertise complements my background in control, optimization and modeling. The Human Machine Interaction group and Human Robot Interaction laboratory provide the setting needed to turn my control method into a scientifically valid study with people. I am already a research visitor in CREATE, so the working relationship and local integration have begun. AAU has approved my affiliation on the MSCA platform; ethics and scientific approvals will follow normal AAU procedures.

Supervision and career mentoring. Knoche and I will meet every two weeks to review scientific decisions and current results. A monthly review will track tasks, data quality, decision gates and risks. Career progress will be reviewed every three months, supported by the Individual Career Development Plan agreed in M1 and formally reviewed in M6, M12, M18 and M24. I will also take part in group seminars and laboratory activities.

Training from the host to me. The training directly addresses the main gap in my profile: designing and evaluating human-centered systems.

- Human centered research: task analysis, participatory design, experimental HCI, counterbalancing and construct validation.

- Multimodal experiments: eye tracking and EEG preprocessing, synchronization, signal quality checks and uncertainty calibration.

- Responsible research: ethics for studies with people, GDPR, FAIR data, bias checks and transparent task changes.

- Career development: project management, supervision, teaching, grant writing, science communication and open source stewardship.

At least 40 hours of formal training will be documented. Each activity will produce evidence of use in the project, such as a validated protocol, an analysis plan, a teaching activity or a grant draft.

Knowledge from me to the host. I will bring optimization, rolling-horizon task assignment, control, signal processing, BCI prototyping and reproducible numerical modeling. I will share these skills through an internal tutorial in M2, reusable simulator components, quarterly code and design clinics, supervision of one MSc project and mentoring of one BSc project.

How knowledge will be exchanged. The host will train me in HCI study design, participatory methods, eye tracking, research governance and responsible deployment from M2 to M3 and through continued study reviews. A joint workshop in M12 and one guest lecture will connect the two research traditions. Tutorial material, simulator components and analysis guidance will remain in the group's repositories so the exchanged knowledge remains available after the fellowship.

No secondment or non academic placement is proposed. The focused 24 month plan already contains the complementary expertise and facilities needed at AAU.

## 1 4 Researcher experience competences and skills

Dual doctoral training. I hold a PhD in Mechanical Engineering from Shahid Chamran University of Ahvaz and am completing a second PhD in Autonomous Systems at Politecnico di Bari. My first PhD gave me depth in mechanical modeling, vibration and acoustics, robotics, control and optimization. My second PhD expanded this foundation toward autonomous decision-making and the interaction of people with robots and computer-based systems. This combination allows me to study ATTUNE at two connected levels: how the control layer makes and carries out decisions, and how those decisions affect the person working with the system.

International and interdisciplinary trajectory. My research journey has taken me from Iran to Italy, Türkiye and Denmark. During these periods, I have worked with researchers in mechanical engineering, control, robotics, human-computer interaction, biology and chemical engineering. Working across institutions and fields has taught me to adapt to different research cultures, explain my methods to researchers outside my field and combine different forms of expertise around a common problem. This experience aligns with the MSCA emphasis on international mobility, interdisciplinary research and two-way knowledge exchange.

Research results. My research has produced results beyond conventional publications. In robotics, I contributed to Iranian patent IR 95162 for a controllable humanoid warning and tracking robot. In an environmental research project, I worked with biologists and chemical engineers to develop suitable experimental flow conditions for a Spirogyra biofilter. This collaboration contributed to the registration of a partial small-subunit ribosomal RNA sequence in the NCBI GenBank database under accession MW063644 [13]. The patent shows my ability to turn an engineering concept into a working system. The NCBI record demonstrates that I can make a productive technical contribution outside my original discipline.

Publications and scientific visibility. My publications cover nonlinear vibration, active noise control, acoustic reconstruction, robotics, optimization, autonomous systems, brain-computer interfaces and human-robot interaction. My recent work includes rolling-horizon task allocation for human-robot teams [11], a compact P300 interface for mission-level robot control and a review of optimization and control in robotized logistics. I have published in peer-reviewed journals and presented my research at international IEEE conferences. This record shows a consistent progression from modeling physical systems to designing autonomous systems that consider the people working with them.

Open science. I maintain two public code repositories. The Acoustic Enclosure Control repository contains material related to my acoustic modeling and control research. The Cognitive-State-Aware Task Allocation repository provides the base implementation of my rolling-horizon task-allocation research. These repositories will be further developed with clearer documentation, reproducible examples and suitable sample or synthetic data. ATTUNE will build on this practice by releasing documented code, task-demand rules and suitable derived or synthetic data when ethical and legal requirements allow.

Technical skills. I have experience obtaining useful results from limited and noisy experimental data. My methods include signal denoising, wavelet analysis, modal analysis, parameter estimation, feature extraction, feature selection and reducing the number of variables used by a model. I use Python, MATLAB, COMSOL and Fortran for modeling, simulation, data analysis and experimental validation. These skills are directly relevant to ATTUNE because each participant will provide only a limited amount of calibration data. The model must use these data to determine which response values genuinely need to be personalized.

Leadership and research independence. As first author on several studies, I have taken responsibility for mathematical formulation, programming, analysis, validation and manuscript preparation while coordinating contributions from collaborators. At Politecnico di Bari, I have connected control, logistics, BCI and human-robot interaction within productive collaborations. This experience shows that I can lead my research independently while also contributing constructively to an interdisciplinary team.

Scientific service, mentoring and teaching. I have reviewed manuscripts for Biomedical Signal Processing and Control. At Shahid Chamran University and Politecnico di Bari, I have taught technical subjects and supported students in modeling, optimization and programming. These activities have developed my ability to explain complex methods, guide technical work and contribute to a productive research environment. ATTUNE will build on these strengths while providing the systematic training in HCI study design, participatory methods and responsible human-centered control that I still need.

# 2 Impact

## 2 1 Career development and employability

This fellowship will strengthen my career prospects by combining advanced scientific training, structured mentoring and clear steps toward research independence. It will prepare me for academic careers in human-robot interaction, human-computer interaction and autonomous systems, as well as industrial research roles in robotics, decision support and human-centered AI.

In M1, I will prepare an Individual Career Development Plan with my supervisor. The plan will set measurable goals for research training, publications, teaching, student supervision, networking and future funding. We will review the plan in M6, M12, M18 and M24. At each review, we will record which goals have been completed, which are delayed and what action is needed next.

By the end of the fellowship, I will have led a preregistered VR robot-supervision experiment and a shorter transfer test in a different VR task. I will also have developed and evaluated a personal workload-prediction model, compared it with non-personal and learning-based alternatives, and tested how its predictions can guide decisions made by the control layer. From M18 to M24, I will prepare an independent funding application and a research statement on human-centered autonomous systems. These outputs will provide clear evidence of my ability to lead interdisciplinary research independently.

| Period | Career measure | Expected gain |
|---|---|---|
| M1-M6 | Baseline skills review; HCI and ethics training; first supervision task; publication and networking plan | A clear development gap and measurable plan |
| M7-M15 | Lead the robot-supervision experiment; present methods internally and internationally; mentor a student | Research leadership and teaching evidence |
| M16-M24 | Lead prediction and transfer tests; organize the stakeholder workshop; prepare an independent grant and research statement | Competitive academic or industrial research profile |

## 2 2 Dissemination exploitation and communication

The dissemination plan follows the project stages, linking the task and resource representation, personal model and validation evidence to scientific and public audiences.

Scientific dissemination and open outputs. Three open-access manuscripts will report the validated demand description and calibration study, the personal dynamic model, and the prediction and transfer results. Results will also be presented at suitable HCI, HRI, control and human-factors venues. Preregistrations, the demand manual, simulator, model code, model card and suitable derived or synthetic data will support verification and reuse.

Exploitation and protection. The main reusable results will be an open reference implementation and an integration guide for researchers and developers. Before release, AAU innovation support will check whether any result requires protection. No patent or company partner is assumed; if a protectable result appears, it will be assessed before public disclosure.

Communication. A project page and three short visual explainers will present the problem, method and limits in plain language. An AAU public-science activity and a stakeholder workshop will use a controlled demonstration to show what the system changes, what information it uses and how the operator can reject a change.

| Route | Measure | Audience | Timing |
|---|---|---|---|
| Dissemination | Three open-access manuscripts and suitable HCI, HRI, control and human-factors presentations | Researchers | M8-M24 |
| Open outputs | Preregistrations, demand and resource manual, simulator, code, model card and suitable data | Researchers and developers | M3-M24 |
| Exploitation | Reference implementation and integration guide following review of protectable results | Adaptive-system developers | M16-M24 |
| Communication | Project page, three explainers, AAU public-science activity and stakeholder workshop | Public, students, operators and stakeholders | M2-M24 |

Monitoring. Progress will be checked against three submitted manuscripts, reusable open outputs, at least 40 stakeholder-workshop participants and about 100 public participants or online viewers. At the M20 workshop, independent users will apply the demand manual to unseen task configurations. Their disagreements and requested clarifications will show where the manual still needs improvement.

Responsibilities. I will lead the manuscripts, repositories, tutorials and public materials. Knoche will provide scientific quality control and access to HCI and human-robot interaction networks. AAU services will support data protection, communication and any intellectual-property review before release.

Responsible communication. Every public message will state that ATTUNE predicts task-related workload under controlled conditions. It does not read emotions or judge workers. Consent, data protection and the limits of the evidence will take priority over visibility.

## 2 3 Expected scientific societal and technological contributions

Within the retained 24-month planning envelope, ATTUNE will deliver evidence about reproducibility, task representation and sensing requirements, together with a controlled prototype. Predictive adaptation and personalized control are established directions [14-18]; the contribution is to determine when experimentally identified cognitive-response dynamics remain useful outside their calibration conditions.

Scientific outputs will include a demand and resource-coding manual, randomized intervention-response data, parameter-recovery and repeated-session analyses, and a benchmark separating personalization, representation and sensing effects. Negative findings will specify which parameters should remain shared, which task changes defeat transfer and whether EEG teaching supplies useful information.

Technological value will be measured by the accuracy and calibration retained with eye tracking and task logs, the amount of recalibration required after transfer, and prospective workload benefit under a prespecified performance constraint. The prototype will expose uncertainty, abstention and operator veto. Laboratory results will not be presented as evidence of workplace effectiveness.

Societal relevance lies in transparent, rejectable assistance and explicit limits on inference about workers. Reporting tracking failures, refusals and variation in prediction error will support decisions about whether a later field study is justified. Dissemination will distinguish measured performance from hypothesized downstream economic or wellbeing benefits.

# 3 Quality and efficiency of implementation

## 3 1 Work plan decision gates and risks

The original 24 person-month envelope is retained. Resource coding, identifiability and independent outcome validation are integrated into the existing work packages. Stress and fatigue become exploratory, and the initial personal dynamic model is reduced to three candidate parameters to make room for the stronger repeat-session and transfer tests. The revised sequence and visit burden must be checked with the eventual host before conversion into an FWO work plan.

| Work package | Timing and effort | Activities and deliverable | Decision gate and response |
|---|---|---|---|
| WP1 Task representation and design | M1-M5; 4 PM | Demand and resource manual; pilot contrasts; recovery and precision simulations; ethics and preregistration. D1 is the locked protocol and coding manual. | Retain only interpretable contrasts. If overlap cannot be separated from difficulty, redesign or narrow H2 before confirmatory testing. |
| WP2 Calibration and reproducibility | M4-M10; 5 PM | Synchronized recordings, first-session calibration and frozen-parameter repeat-day evaluation. D2 is the linked dataset and measurement specification. | Verify signal quality, event alignment and feasible burden. Reduce exploratory outcomes before primary contrasts. |
| WP3 Personal dynamics and sensing | M8-M16; 6 PM | Recovery, partial pooling, leakage-controlled model selection and sensing comparisons. D3 is the frozen benchmark and model set. | Personalize only recoverable, useful parameters. If EEG teaching adds no value, simplify calibration; if personalization fails, retain a population result and narrow the claim. |
| WP4 Intervention and transfer tests | M14-M22; 6 PM | Randomized intervention predictions; counterbalanced control; transfer with rich diagnostic and operational sensing views. D4 is the evaluation report and prototype. | Require calibrated prediction gains before enabling predictive adaptation. Transfer failure limits reuse claims. Recalibrated analyses remain separate. |
| WP5 Management training and dissemination | M1-M24; 3 PM | Data management, career reviews, manuscripts, stakeholder communication and reusable outputs. | Monthly scientific reviews and quarterly scope reviews trigger documented changes when feasibility or precision is inadequate. |

Main data collection depends on the WP1 protocol gate. Model development can overlap with collection, but evaluation outcomes will remain inaccessible for tuning. WP4 prediction tests begin only after model selection and uncertainty rules are frozen. The second task will be piloted early enough to verify resource coding, while its evaluation data remain held out.

Scientific progress will be reviewed every two weeks with the supervisor, and data quality, effort, visit burden and risks monthly. Any failed gate will lead to a documented reduction in the supported claim. A shorter prediction horizon may be investigated after a failure at 60 seconds, but it will not replace the failed primary result without being labelled exploratory.

| Main risk | Early evidence | Planned response |
|---|---|---|
| Demand and resource overlap remain confounded | Pilot contrasts change content or difficulty together with overlap | Match interfaces, record residual differences, simplify descriptors and narrow the tested mechanism. |
| Personal parameters are unstable or unidentifiable | Recovery failures, broad intervals or poor repeat-day prediction | Use shared parameters or partial pooling; remove unsupported personal gains. |
| The observer imitates measurement bias | Teacher agreement without independent outcome improvement | Evaluate against held-out ratings and performance; retain logs-only and no-teacher comparators. |
| Reduced sensing is inadequate | Eye-plus-logs forecasts add little or have poor calibration | Report the sensing limit; retain a rich-sensing result without claiming routine eye-based adaptation. |
| Transfer or uncertainty calibration fails | New-task error, low interval coverage or excessive abstention | Restrict claims to the source task; distinguish observation recalibration from dynamic refitting. |
| Study precision or participant burden is inadequate | Pilot simulations or visit completion contradict the initial plan | Reduce confirmatory contrasts and exploratory measures; revise recruitment within ethical and resource limits before preregistration. |
| Ethics or recruitment is delayed | Milestones slip | Advance simulation, coding and analysis preparation while participant work awaits approval. |

This plan retains a primary robot-supervision experiment and one shorter transfer test. It does not add a workplace trial or a separate large clinical-style validation study. Host facilities and recruitment capacity inherited from the MSCA proposal require reconfirmation if the project is moved to another institution.


## 3 2 Host capacity and hosting arrangements

Hosting arrangements and integration. I will receive workspace, computing access, software and access to the VR and sensing infrastructure from the start of the fellowship. My current research visit to CREATE means that the working relationship, local procedures and scientific integration have already begun. During the fellowship, integration will continue through HMI group meetings, seminars, shared experimental work and student supervision. The scientific review every two weeks and the monthly review of outputs, data quality and risks described in Section 1.3 will connect the hosting arrangements directly to project delivery.

Project-specific scientific capacity. AAU provides the combination required by ATTUNE: human-centered interaction research, eye tracking, human-robot interaction facilities and experience with EEG, BCI, VR and participant studies. Calibration recordings will use the Brain, Behavior, Architecture Research laboratory of Assoc. Prof. Zakaria Djebbara, which holds Waveguard EEG caps with ANT Neuro eego Sports amplifiers, Meta Quest Pro headsets with integrated eye tracking, and Lab Streaming Layer synchronization across all equipment. Synchronized multimodal recording is therefore already established rather than built for this project. The laboratory has already completed a related Whack-a-Mole study with 25 adults, providing practical evidence that a participant study of similar scale can be completed with the available facilities and support.

Institutional and administrative capacity. AAU has established procedures for research ethics, data protection, data management, open science, innovation review and EU project administration. AAU Research Services will support grant administration and reporting. The relevant institutional units will support consent and data-protection procedures, secure handling of participant data, open-output decisions and review of any potentially protectable result before release. AAU's approval of my host affiliation on the MSCA submission platform confirms the administrative hosting arrangement; scientific and ethics approvals will follow the normal AAU procedures.

Completeness of the hosting environment. No external secondment is required because the complementary expertise, participant-study facilities, computing support and institutional services needed for ATTUNE are available at AAU. This keeps responsibility for the scientific work, participant protection and project management within one coordinated host environment. Further institutional details and relevant infrastructure are provided in Part B-2.

# References

[1] Aricò P et al. Adaptive Automation Triggered by EEG-Based Mental Workload Index. Frontiers in Human Neuroscience 10 (2016) 539. doi:10.3389/fnhum.2016.00539.

[2] Kingphai K, Moshfeghi Y. Mental Workload Assessment Using Deep Learning Models From EEG Signals: A Systematic Review. IEEE Transactions on Cognitive and Developmental Systems 17(1) (2025) 40-60.

[3] Pang L et al. Subject-specific mental workload classification using EEG and stochastic configuration network. Biomedical Signal Processing and Control 68 (2021) 102711. doi:10.1016/j.bspc.2021.102711.

[4] Wickens CD. Multiple Resources and Mental Workload. Human Factors 50(3) (2008) 449-455. doi:10.1518/001872008X288394.

[5] Monsell S. Task switching. Trends in Cognitive Sciences 7(3) (2003) 134-140. doi:10.1016/S1364-6613(03)00028-7.

[6] Hart SG, Staveland LE. Development of NASA-TLX: Results of empirical and theoretical research. In: Human Mental Workload. North-Holland, 1988, 139-183.

[7] Wilkinson MD et al. The FAIR Guiding Principles for scientific data management and stewardship. Scientific Data 3 (2016) 160018. doi:10.1038/sdata.2016.18.

[8] Charles RL, Nixon J. Measuring mental workload using physiological measures: A systematic review. Applied Ergonomics 74 (2019) 221-232. doi:10.1016/j.apergo.2018.08.028.

[9] Ahlstrom U, Friedman-Berg FJ. Using eye movement activity as a correlate of cognitive workload. International Journal of Industrial Ergonomics 36(7) (2006) 623-636. doi:10.1016/j.ergon.2006.04.002.

[10] Parasuraman R, Sheridan TB, Wickens CD. A model for types and levels of human interaction with automation. IEEE Transactions on Systems, Man, and Cybernetics - Part A 30(3) (2000) 286-297. doi:10.1109/3468.844354.

[11] Porghoveh M, Carli R, Dotoli M. Rolling-Horizon Task Allocation for Human-Robot Teams with Mental-State Awareness. 12th International Conference on Control, Decision and Information Technologies (CoDIT), 2026. doi:10.1109/CoDIT70676.2026.11630849.

[12] Breque M, De Nul L, Petridis A. Industry 5.0: Towards a sustainable, human-centric and resilient European industry. European Commission, Directorate-General for Research and Innovation, Publications Office of the European Union, 2021. doi:10.2777/308407.

[13] National Center for Biotechnology Information. Spirogyra sp. isolate gh-2 small subunit ribosomal RNA gene, partial sequence. GenBank accession MW063644, 2020.

[14] Chand S, Zheng H, Lu Y. A vision-enabled fatigue-sensitive human digital twin towards human-centric human-robot collaboration. Journal of Manufacturing Systems 77 (2024) 432-445. https://doi.org/10.1016/j.jmsy.2024.10.002

[15] Xue J, Li X, Zhang N. Safe reinforcement learning with online filtering for fatigue-predictive human-robot task planning and allocation in production. Journal of Manufacturing Systems 84 (2026) 561-583. https://doi.org/10.1016/j.jmsy.2025.12.019. Reviewed manuscript: https://arxiv.org/abs/2604.12667v2

[16] Vallée A. From prediction to intervention: causal digital twins for personalized clinical decision support. Journal of Translational Medicine 24 (2026) 441. https://doi.org/10.1186/s12967-026-07895-8

[17] Yang S, Zhang J. An adaptive human-machine control system based on multiple fuzzy predictive models of operator functional state. Biomedical Signal Processing and Control 8(3) (2013) 302-310. https://doi.org/10.1016/j.bspc.2012.11.003

[18] Zhang et al. Feasibility study of personalized speed adaptation method based on mental state for teleoperated robots. Frontiers in Neuroscience 16 (2022) 976437. https://doi.org/10.3389/fnins.2022.976437
