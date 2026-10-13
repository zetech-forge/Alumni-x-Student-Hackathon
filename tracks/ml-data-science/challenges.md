---
title: Challenges
parent: Machine Learning & Data Science
nav_order: 4
---

# Challenges

This track has **three challenges**. Each one is a mini-project that combines several disciplines in a single working system: **data engineering, geospatial analysis, machine learning, software engineering and AI agents**, plus a domain ingredient that changes with the challenge (climate science, epidemiology, or product and industrial knowledge).

Each challenge is designed to be a working prototype within the two-day event. **Day 1** is for ideation, data and a first working baseline. **Day 2** is for building the rest, testing, and preparing your pitch. Every challenge has:

- **Core requirements** that every team must complete, and
- **Stretch goals** for teams that finish early and want more points for depth.

A team that finishes the core requirements and demonstrates them well will score better than a team that attempts everything and finishes nothing.

| | Challenge 1 | Challenge 2 | Challenge 3 |


| **Name** | Climate Sentinel | Malaria Atlas Lab | Product Copilot |
| **Theme** | Cyclones, heavy rain and drought: analysis, early warning and response planning | Malaria mapping, parasite species patterns and drug effectiveness in Africa | A multimodal assistant that replaces printed product manuals for engineers and customers |
| **Data skills** | 30+ years of weather and hazard-event data, cleaned and aggregated | Fuse survey, surveillance, genomic and environmental data | Collect, clean and structure a company's product knowledge from text, images and audio |
| **Geospatial** | Hazard maps, exposure and risk zones | Prevalence mapping with spatial statistics | Optional: service-region and depot mapping (stretch) |
| **Machine learning** | Seasonal drought outlook, heavy-rain and cyclone-exposure models | Spatial prediction, drug-resistance marker prediction, species pattern modelling | Multimodal retrieval, speech and image understanding |
| **AI agent** | Early-warning and response-planning agent | Evidence-grounded surveillance briefing agent | Multimodal, role-aware agent (engineer and customer) |
| **Extra ingredient** | Climate statistics and disaster response planning | Epidemiology and uncertainty quantification | Information retrieval, evaluation and access control |




**Rules that apply to all three challenges.**

- Open data and free tools only. Free or open language models for any agent (for example a local model through Ollama, or a free API tier).
- Record every data source, access date and license in `DATA.md`.
- **The agent must not do arithmetic.** All calculations are done by code tools, and every number in an agent answer must trace to a tool result.
- Every agent must **log each tool call**, **say "I don't know" when data is missing**, and keep a **human in the loop** for any consequential output.
- No personal data. Do not pass private information into hosted AI tools. Anything that looks personal must be synthetic.
- Report **honest results**. A model that barely beats a simple baseline, and a team that says so, scores better than a model with a high score from a leaky test.

---

## Challenge 1

###  Climate Sentinel, Analysing Weather Behavior and Predicting Cyclone, Heavy-Rain and Drought Risk

*Default SDGs: 13 Climate Action, 2 Zero Hunger, 11 Sustainable Cities, 1 No Poverty. You may choose others.*

- **Scenario:** Disaster managers prepare for three very different kinds of weather hazard. **Drought** builds slowly over months of below-normal rain before crops fail and water runs short. **Heavy-rain floods** can arrive within days. **Cyclones** can arrive within hours of a warning and bring wind, storm surge and flooding together. Most districts do not have an analyst who can turn weather data into plain advice: *Is this season unusual? What is likely to happen next? Which districts are most exposed, and what should we prepare?* Your team will build **Climate Sentinel**, a system that learns how the weather in your chosen region normally behaves, detects when it is behaving abnormally, estimates seasonal drought risk and short-range heavy-rain risk, maps cyclone exposure, measures who is exposed, and uses an AI agent to write a short, evidence-backed advisory and response plan for disaster planners.

  **Choose a region** with at least 8 districts (or 8 evenly spread grid points), ideally one where at least two of the three hazards really matter. Cyclone work needs a coastal or near-coastal region; inland regions replace the cyclone requirement with a second flood or heat indicator (see step 6).

- **What you will combine:**

  | Discipline | What you do |
  |---|---|
  | Data | Pull 30 years of daily weather and historical storm tracks, clean and aggregate them, and add a climate-driver index such as El Niño (ENSO) |
  | Statistics and climate analysis | Describe normal weather, seasons, trends and extremes, and build drought, heavy-rain and storm indicators |
  | Machine learning | Forecast unusually dry seasons and heavy-rain days, and test honestly against simple baselines |
  | Geospatial | Map hazard status by district, cyclone exposure and the people at risk |
  | AI agent | Build an early-warning agent that calls tools, writes a cited advisory and proposes a response plan |
  | Disaster planning and storytelling | A dashboard, an action playbook and a 5-minute pitch for decision makers |

- **Objectives (core requirements):**
  1. **Data.** Build a clean dataset with **at least 30 years of daily rainfall and temperature** (1991 to the present) for **at least 8 locations** in your region, from a free source such as the Open-Meteo historical weather API. Add district **boundaries**, a **population** raster, a monthly **El Niño index** (ENSO) and, for coastal regions, the **IBTrACS** historical storm-track archive. Record every source, access date and license in `DATA.md`. State clearly that the rainfall is a **model- or satellite-based estimate, not a rain gauge reading**, and what that means for accuracy.
  2. **Weather behavior analysis.** For each location, describe how the weather normally behaves:
     - the **monthly climatology** (normals for 1991 to 2020) and the rainy and dry seasons,
     - the **trend** in annual and seasonal rainfall and temperature, with a significance test and the size of the change,
     - **extremes**: the longest dry spell each year, the number of heavy-rain days (above the location's own 95th percentile of wet days), and the maximum 3-day rainfall each year.
  3. **Hazard indicators and validation.** Build a **drought indicator** (3-month rainfall as a percentage of normal, with drought classes you define and justify) and a **heavy-rain indicator** (3-day rainfall compared with the location's 99th percentile 3-day total). **Validate them against history:** list the 3 worst droughts and 3 worst heavy-rain periods your indicators flag, and check them against at least **2 documented real events** (for example from ReliefWeb, EM-DAT or national sources). Report what matched and what did not.
  4. **Cyclone exposure.** For coastal regions, use IBTrACS to count, for each district, how many tropical storms passed within 300 km in each season, and how that count has changed over decades. Map the result and rank districts by exposure. **Do not claim to predict cyclone paths.** Your system must point users to the official cyclone warning centre for any live storm.
  5. **Geospatial.** Make an interactive map of the current drought and heavy-rain status by district, with cyclone exposure as a second layer. Overlay **population** to report **how many people live in districts under each hazard level**. Use a projected coordinate system for any distance or area calculation.
  6. **Machine learning: a seasonal outlook.** At the end of each month, predict whether the **total rainfall for the next 3 months will be in the driest third** of history for that season (a "below-normal" outlook). Use features such as rainfall and temperature anomalies from recent months, the El Niño index (using only values that would have been known at the time), and the calendar month. Rules:
     - Use a **time-based split**: train on earlier years and test on at least the last 8 years.
     - Compute thresholds and anomalies from the **training years only**, so no test information leaks in.
     - Compare with **two baselines**: climatology (the one-in-three base rate) and persistence (if the last 3 months were dry, predict dry).
     - Report precision, recall and F1 for the below-normal class, **per location**, and at least one probability score (for example the Brier skill score against climatology).
     - **If your model has no skill over the baselines, say so.** An honest "no skill here, so we use climatology" is a valid result.

     *Inland teams:* replace the cyclone step with a **heat-stress indicator** or a second heavy-rain model, and state why.
  7. **Short-range watch.** Use a live forecast API to get the next 7 days of rainfall (and wind, for coastal regions) for each location, and flag any location whose forecast 3-day total passes its own 99th percentile threshold from step 3.
  8. **AI agent.** Build an early-warning agent with **at least 5 tools**: current climate status, the 7-day forecast watch, your seasonal outlook, the cyclone exposure lookup, the population exposure lookup, and a **playbook lookup** (see step 9). For any district, the agent writes a short advisory covering: *what is happening compared with normal, what is likely next (with probability and confidence), who is exposed, and what to prepare*. It must **cite the tool result behind every number**, log every tool call, **say "I don't know" when data is missing**, and always state that **official warnings from the national meteorological service take priority**. The advisory remains a **draft until a person approves it** (a simple approve button is enough). Test it with at least 5 questions, including: one it cannot answer (for example, exactly when it will rain on a particular farm), one about a district that does not exist, one asking it to predict the exact path of a cyclone, and one that tries to make it say there is no risk when the data says otherwise.
  9. **Playbook and limitations.** Write a one-page **action playbook**: for each hazard (drought, flood, cyclone) and hazard level (for example watch, warning, emergency), list 5 to 8 preparedness and response actions, **each taken from a cited guidance document** (for example from WMO, FAO, OCHA, your national disaster agency or humanitarian guidelines). The agent may only recommend actions from this playbook. Also write a one-page **limitations note**: where your data or model is weak, which districts or seasons you trust least, and who might be missed.
  10. **Story.** A dashboard or app with the hazard map, a chart of rainfall against normal for a chosen district, the seasonal outlook, cyclone exposure and the agent's advisory. Prepare a 5-minute pitch for a district disaster manager.

- **Stretch goals:**
  - Replace the drought indicator with the **Standardized Precipitation Index (SPI)**, the drought measure recommended by the World Meteorological Organization, and compare the two.
  - Add a **vegetation drought signal** (for example NDVI anomaly from MODIS or Sentinel-2) and check whether it confirms or contradicts the rainfall indicator.
  - Build a **compound-risk score** for districts that face two hazards in the same season (for example drought followed by flood).
  - Cross-check rainfall against a second source (for example CHIRPS) at two locations and report the difference.
  - Turn the outlook into three classes (below, near, above normal) and report calibration.
  - Add a plain-language summary in a local language.
  - Deploy the app online.

- **Constraints:**
  - Complete within the two-day event window.
  - **Data**  use publicly available data
  - This is a **planning-support tool**, not an official warning system. State this in the app and in your pitch.

- **Deliverable:** Submit all of the following:
  1. A **public repository** with a README (region, target users, chosen SDG, how to run), `requirements.txt` and `DATA.md`.
  2. A **weather behavior notebook**: climatology, seasons, trends, extremes, the hazard indicators, cyclone exposure and the validation against documented real events.
  3. A **forecasting notebook**: the seasonal outlook model against both baselines, with per-location metrics and a plain statement of where it has skill and where it does not.
  4. A **working app or dashboard** with the hazard map, exposure counts, outlook and the early-warning agent.
  5. The **agent log** for your 5 test questions, including the approval step.
  6. The **action playbook** (with citations) and the **limitations note**.
  7. A **5-minute live demo and pitch**.




## Challenge 

### Malaria Atlas Lab, Mapping Malaria, Parasite Species Patterns and Drug Effectiveness in Africa

*Default SDGs: 3 Good Health and Well-being, 10 Reduced Inequalities, 17 Partnerships. You may choose others (for example, 1 No Poverty or 13 Climate Action, if you focus on climate-driven transmission).*

- **Scenario:** A national malaria programme must decide where to send bed nets, spraying teams and test kits, and which first-line drugs to recommend. Three questions drive those decisions: **Where is malaria transmitted most and how is it changing? Which parasite species are present where? And are the drugs still working?** The data to answer them exists, but it is scattered across household surveys, health facility counts, clinical drug trials, parasite genetics and environmental layers, and each source is incomplete and biased in a different way. Your team will build **Malaria Atlas Lab**: a pipeline that maps malaria burden for a chosen set of African countries, models the geographic pattern of parasite species, estimates the **effectiveness of antimalarial drugs and the spread of resistance markers** from published study data, and presents the results, with uncertainty, through an **evidence-grounded briefing agent** for programme planners.

  **This is a research-support and planning tool. It is not a diagnostic or treatment tool and must never give clinical advice to individual patients.** State this in the app and in your pitch.

- **What you will combine:**

  | Discipline | What you do |
  |---|---|
  | Data | Fuse prevalence surveys, surveillance counts, drug-efficacy studies, resistance-marker data and environmental rasters into one documented dataset |
  | Geospatial | Build prevalence and risk surfaces, aggregate by district, and calculate population at risk |
  | Statistics and epidemiology | Handle sampling bias, spatial autocorrelation, confidence intervals and meta-analysis |
  | Machine learning | Spatial prediction of prevalence, prediction of resistance-marker frequency, species pattern modelling, all validated on unseen locations |
  | AI agent | A surveillance briefing agent that retrieves evidence and never invents numbers |
  | Public health communication | A dashboard, a limitations note and a 5-minute pitch for a programme manager |

- **Objectives (core requirements):**
  1. **Data.** Choose **at least 3 African countries** (or one large country with at least 15 districts or regions) and build a clean dataset from open sources. Minimum content:
     - **Parasite prevalence** survey points (for example *Plasmodium falciparum* parasite rate from the Malaria Atlas Project, or DHS and MIS surveys) with coordinates, year, sample size and age range,
     - **Environmental covariates** (rainfall, temperature, vegetation index, elevation, distance to water, population density, urban or rural),
     - **Drug efficacy and resistance data** (for example therapeutic efficacy studies and molecular marker surveys from WWARN, the WHO Malaria Threats Map or the MalariaGEN Pf7 genomic data set),
     - **Species information**: where each *Plasmodium* species (*falciparum*, *vivax*, *malariae*, *ovale*, *knowlesi*) has been recorded or reported.

     Record every source, access date and license in `DATA.md`. Document known biases (for example, surveys are more common near roads and cities) in `ASSUMPTIONS.md`.
  2. **Mapping malaria burden.** Produce an interactive map of **predicted parasite prevalence** (a continuous surface or district estimates) and the **estimated population living in each risk class**. Include a **companion uncertainty map**. Use a projected coordinate system for any distance or area work.
  3. **Spatial machine learning.** Predict prevalence at unsurveyed locations from the environmental covariates using at least one machine learning model (for example gradient boosting or random forest) and **one simple baseline** (for example a district average or an inverse-distance interpolation). Rules:
     - **Validate with spatial cross-validation** (hold out whole districts or spatial blocks, not random points). Random splits leak information between neighbouring points and will be marked down.
     - Report MAE or RMSE and a rank correlation, and show where the model is least reliable.
     - Give a **prediction interval** for each district (for example from quantile regression, an ensemble or bootstrap) and check that it covers the truth about as often as it claims.
  4. **Species pattern mapping.** For the causative agents, map the **geographic pattern of each species** in your region: where each is reported and the estimated **share of cases by species** per district or country, with the environmental and ecological reasons for the pattern (for example, *P. vivax* is rare where the Duffy-negative blood group is common). Treat species presence records as **presence-only data** and state the sampling bias. Fit a presence model with a method that accounts for that (for example background points with spatial blocking) and report how well it predicts held-out areas.
  5. **Drug effectiveness analysis.** From the efficacy and marker data:
     - Estimate **treatment efficacy** for at least one artemisinin-based combination therapy (for example artemether-lumefantrine) per country or sub-region, using the **PCR-corrected adequate clinical and parasitological response (ACPR)** at day 28 or 42 as your outcome. Combine studies with a **random-effects meta-analysis** or a hierarchical model, and give a confidence interval. Respect the WHO threshold: a treatment failure rate of 10% or more is the level at which a first-line drug policy should be reviewed.
     - Map the **frequency of validated resistance markers** (for example *pfkelch13* mutations linked to artemisinin partial resistance, and the marker for lumefantrine or partner-drug susceptibility) by region and year. Show the **trend over time** and test whether it is significant.
     - **Predict marker frequency** for a region and year without data, using spatial and temporal features, and validate on **held-out regions** and the **most recent years**. Compare to a simple baseline such as "last observed value".
     - Be explicit about the gap between **efficacy in a trial** and **effectiveness in the real world**, and about what a marker frequency does and does not tell you.
  6. **Evidence-grounded agent.** Build a surveillance briefing agent with **at least 4 tools**: prevalence lookup (with uncertainty), species pattern lookup, drug efficacy and resistance lookup, population-at-risk lookup, and a **guideline retrieval tool** that returns passages from cited WHO or national malaria guidelines. For any district, the agent writes a short brief: *burden and trend, dominant species, drug efficacy evidence and its quality, population at risk, and which programme options the guidelines support*. It must **cite the tool result or document behind every number and claim**, log every tool call, **report uncertainty and the number of studies behind each estimate**, and say "I don't know" when evidence is missing. A brief is a **draft until a person approves it**. Test it with at least 6 questions, including: one asking for a diagnosis or a dose for an individual patient (it must refuse and point to a health worker), one about a region with no data, one asking whether a drug "definitely works" when the evidence is mixed, and one that tries to get a single resistance study presented as national truth.
  7. **Dashboard.** Show the prevalence and uncertainty maps, species patterns, drug efficacy and resistance trends with confidence intervals, and the agent's briefs.

- **Stretch goals:**
  - Add a **seasonal transmission model**: relate monthly rainfall and temperature to case counts and give a 1 to 3 month outlook for a district.
  - Add **climate scenarios**: show how projected temperature or rainfall changes would shift the suitable area for transmission.
  - Add **vector data** (for example *Anopheles* species occurrence, including the invasive *An. stephensi*) and show where vector control resistance or invasion overlaps high burden.
  - Map **access to care**: estimate travel time to the nearest health facility and show where high burden and poor access overlap.
  - Use **genomic data** to cluster parasite populations and show whether resistance markers are spreading from one region or arising independently.
  - Estimate the **value of information**: which region's next drug study would reduce uncertainty the most?

- **Constraints:**
  - Complete within the two-day event window.
  - **Data **use publicly available data
  - Only publicly available, aggregated or anonymised data may be used. **No patient-level records.** Do not attempt to re-identify anyone.
  - Predictions are estimates for planning. Do not present a modelled map as a measured one, and do not present a drug-efficacy estimate as a treatment recommendation.

- **Deliverable:** Submit all of the following:
  1. A **public repository** with a README (countries, target users, chosen SDG, how to run), `requirements.txt`, `DATA.md` and `ASSUMPTIONS.md`. One command (or a short, clear sequence) must rebuild your main results.
  2. A **mapping notebook**: prevalence model, baseline, spatial cross-validation and uncertainty.
  3. A **species and drug notebook**: species pattern model, efficacy meta-analysis, resistance marker trends and prediction with validation.
  4. A **working dashboard** with maps, trends and the briefing agent.
  5. The **agent log** for your 6 test questions, including the approval step.
  6. A **model card and limitations note** (one to two pages): data gaps, biases, which countries or years you trust least, and what the tool must not be used for.
  7. A **5-minute live demo and pitch**.



## Challenge 3:

### Product Copilot, A Multimodal Assistant that Replaces Printed Product Manuals

*Default SDGs: 9 Industry, Innovation and Infrastructure, 12 Responsible Consumption and Production, 8 Decent Work and Economic Growth. You may choose others.*

- **Scenario:** A company sells products across several categories (for example pumps, generators, solar inverters, agricultural machines or medical equipment). It has two groups of people who depend on product knowledge. **Field engineers** install, service and repair equipment on site, often with poor connectivity, dirty hands and a stack of paper manuals in the truck. **Customers** want to know which product suits their need, what it costs and what they should buy. Today both groups depend on thick product manuals, spec sheets and phone calls to the head office. Your team will build **Product Copilot**: a **multimodal AI assistant** that understands **text, images and audio**, and serves **both groups from one system**. An engineer can photograph a nameplate or a fault, speak a question and get **technical information and a side-by-side comparison of products**. A customer can describe a need and get **advice, prices and a clear recommendation** to decide with confidence. Both get answers grounded in the company's own documents, never invented.

  **Pick a company.** Choose a real company that publishes open or permissively licensed product documentation, or build a **realistic fictional company** from open-licensed manuals and a synthetic price list. The company must sell products in **at least 3 categories** and **at least 15 products in total**. Do not scrape sites that forbid it. Record every source and license in `DATA.md`, and treat price data as **catalogue prices, not a live quote**.

- **What you will combine:**

  | Discipline | What you do |
  |---|---|
  | Data | Collect and structure product manuals, specifications, prices, images and audio into a clean knowledge base |
  | Multimodal ML | Speech to text, image understanding (nameplate and part recognition) and text embeddings for retrieval |
  | Software engineering | Retrieval pipeline, role-aware API, a simple app for the field and the customer |
  | AI agent | A tool-using agent that serves two roles with different permissions |
  | Evaluation and AI safety | Test answer accuracy, grounding, refusal and access control with a measured benchmark |
  | Industrial and product domain | Specifications, compatibility, safety warnings and total cost of ownership |

- **Objectives (core requirements):**
  1. **Data collection and knowledge base.** Collect the documentation for **at least 3 product categories and 15 products**: specification sheets, installation and maintenance manuals, troubleshooting guides, safety notices and a **price list**. Convert them to clean text and structured tables (for example specification fields as a table with units). Keep **page-level provenance** so any answer can point to a document and page. Include at least **30 product images** (product photos, nameplates, wiring diagrams or parts) with labels, and at least **15 audio questions** (recorded, synthetic speech or open-licensed audio) in the languages or accents your users would use. Document every source, license and cleaning step in `DATA.md`.
  2. **Structured product catalogue.** Build a **normalised specification table** with consistent units and fields per category (for example power rating, voltage, capacity, dimensions, warranty), plus a **price table** with currency, date and tax status. Validate it: show checks for missing values, unit errors and duplicate products.
  3. **Multimodal understanding.**
     - **Text:** retrieval over manuals and specifications with embeddings and a re-ranking or filtering step.
     - **Audio:** transcribe spoken questions with an open speech model (for example Whisper), and report the **word error rate** on your audio set.
     - **Image:** identify the product, model or part from a photo (a nameplate or a part photo). Use OCR, an open vision-language model or an image classifier, and report accuracy on a **held-out image set**.
     - Report how each modality changes the final answer quality, and where it fails (for example blurry images, noisy audio, accented speech).
  4. **Engineer mode.** For a field engineer, the agent must:
     - give **technical information** (specifications, installation steps, torque or wiring details, troubleshooting steps) with **page-level citations**,
     - **compare two or more products** in a table, using the structured specification data (not generated from memory), and highlight differences that matter for the stated task,
     - include **safety warnings** from the manual when the task involves them (for example electrical isolation or lifting), and
     - work with a **short, hands-free flow**: a spoken question and a photo should be enough.
  5. **Customer mode.** For a customer, the agent must:
     - ask **clarifying questions** about the need (budget, use case, power or capacity, location),
     - **recommend one or more products** and explain the trade-offs in plain language,
     - quote **catalogue prices** from the price table, calculate totals, taxes or running costs **using a code tool** (the model must not do arithmetic), and state clearly that the price is not a binding quote, and
     - **never reveal internal information** (see step 5).
  6. **Role-aware access control.** The same system serves both roles, with different permissions. Include at least **internal-only content** (for example cost margins, supplier prices, internal service bulletins, engineer-only repair procedures) and **customer-safe content**. Access control must be applied **before retrieval** (not only by instructing the model). Show that a customer cannot obtain engineer-only or internal data by asking, rephrasing or role-playing.
  7. **Evaluation benchmark.** Build a test set of **at least 60 questions**: at least 20 for engineers, 20 for customers, 10 multimodal (image or audio) and 10 adversarial (see below). Each must have a reference answer and the source page or table row. Report:
     - **answer accuracy** and **citation correctness** (does the cited page really support the answer?),
     - **comparison accuracy** (are the specification values in the table correct?),
     - **hallucination rate** (claims not found in any source),
     - **calculation correctness** (price and cost answers match the code tool),
     - **refusal quality**: correct refusals on out-of-scope or unsafe questions and the **over-refusal rate** on harmless ones.

     The **10 adversarial items** must include: a question about a product the company does not sell, a request for the wrong unit or a trick specification, a customer asking for internal margin data, a request to skip a safety step, and a prompt hidden inside an uploaded manual or image that tries to override the system.
  8. **App and engineering.** Deliver a simple **app** (web or mobile-friendly) with two entry points (engineer and customer), image upload, audio recording or upload, and a visible **source panel** that shows the document, page and image behind each answer. Log every tool call. Report **median response time** and the effect of **running offline or on a small local model** (the engineer is often on a weak connection). Provide a **one-command** way to rebuild the knowledge base and run the evaluation.
  9. **Human oversight.** For any answer that could affect safety (electrical, mechanical, pressure, hazardous substances) or a purchase above a threshold you define, the system must show a **confidence level**, state **"check the manual and follow local regulations"** and offer a **hand-off to a human expert**. Say how a wrong answer would be reported and corrected.

- **Stretch goals:**
  - Add **offline mode**: a small local model with a cached knowledge base, and report the accuracy drop compared with the full system.
  - Add **multilingual support** (for example English and Swahili, French or Arabic) for speech and text, and report accuracy by language.
  - Add a **fault-diagnosis flow**: from a photo and a spoken symptom, narrow down likely causes step by step, with parts and tools needed.
  - Add a **parts and compatibility checker** that lists spare parts, and warns when a part is not compatible with a given model.
  - Add **total cost of ownership** (price, energy use, service interval, spare parts over 5 years) as a code tool, so customers can compare products fairly.
  - Add **document change detection**: when a manual is updated, flag which answers and benchmark items become stale.
  - Add **service-region mapping**: show the nearest depot or service point for a customer location, using road distance.
  - Expose the system as an **API** with a health check and per-role rate limits.

- **Constraints:**
  - Complete within the two-day event window.
  - **Data** use publicly available data
  - Respect licenses and terms of use. Do not copy proprietary manuals you are not allowed to use.
  - Use **synthetic data** for anything that looks like customer, supplier or cost information. Attacks and tests must target only your own system.
  - The assistant is a **decision-support tool**. It does not replace manufacturer documentation, certified technicians or local safety regulations. State this in the app and in your pitch.

- **Deliverable:** Submit all of the following:
  1. A **public repository** with a README (company, target users, chosen SDG, architecture diagram, how to run), `requirements.txt`, `DATA.md`, and the **one-command** build and evaluation script (Docker or an equivalent).
  2. The **knowledge base**: structured specification and price tables, document text with provenance, images and audio, with a short data dictionary.
  3. A **multimodal report**: retrieval quality, word error rate, image identification accuracy, and failure cases for each modality.
  4. The **evaluation benchmark** (60 or more questions) with the results table and the **adversarial test results** before and after your defenses.
  5. A **working app** with engineer mode, customer mode, source panel and the agent's tool-call log.
  6. A **short security and access-control note**: what is restricted, how access is enforced before retrieval, and what attacks were tried.
  7. A **model card and limitations note**: products or topics where the assistant is weak, languages it handles poorly, and who might be misled.
  8. A **5-minute live demo and pitch**, with one engineer scenario and one customer scenario.

