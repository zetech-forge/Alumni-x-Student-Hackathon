---
title: Challenges
parent: Machine Learning & Data Science
nav_order: 4
---

# Machine Learning & Data Science: Challenges

All 24 challenges use open or free-registration data and map to at least one UN Sustainable Development Goal (SDG). Within each tier, challenges are ordered from simplest to hardest. Points rise with difficulty, so teams can choose between a safe finish and an ambitious attempt.

| Tier | Challenges | Point range | Suggested time |
|---|---|---|---|
| Beginner | 1-8 | 100-150 | 6 hours |
| Intermediate | 9-16 | 200-300 | 10 hours |
| Advanced | 17-24 | 400-600 | 16 hours |

**Common rules for every challenge**
- Use only open data, open-source tools or free tiers. Cite every data source.
- Submit a public or shared repository with a README that lets a judge rerun your work.
- Include a short "Limitations and ethics" section in the README. Never use real personal or patient data.
- Judging bonus (up to +5 points): a working deployed demo, or a team that attempts a challenge a tier above its experience.

---

## Beginner

### Challenge 1: Where Does the Waste Go? 
*SDG 11, 12 | Analytics + Geospatial | Waste management*
- **Scenario:** Global municipal waste is growing faster than many cities can manage. Where collection is weak, waste is burned or dumped, harming air, water and health. Policymakers need to see where collection, recycling and disposal fall short, and how this relates to income and urbanization.
- **Objectives:**
  - Compare waste generated per person, collection coverage and disposal methods across at least 30 countries or cities.
  - Show how income level relates to waste composition (organic, plastic, paper).
  - Map the 10 places with the largest gap between waste generated and waste safely managed.
  - Make one policy recommendation supported by your findings.
- **Constraints:** 6 hours. Python, R or a spreadsheet tool. Data: World Bank *What a Waste 2.0*, Our World in Data, Natural Earth boundaries. Be explicit about differences between "collected" and "safely managed", and flag any modelled or outdated figures.
- **Deliverable:** A notebook or report, a map, and a 3-minute data story with at least 3 visuals and one policy recommendation.
- **Points:** 100

### Challenge 2: The Education Equity Dashboard 
*SDG 4, 5 | Analytics + Dashboarding*
- **Scenario:** Enrollment has grown globally, but learning outcomes, completion rates and gender parity vary widely. Spending more does not always produce better results. Education ministries and donors need a clear view of who is being left behind.
- **Objectives:**
  - Combine at least 4 education indicators (for example completion rate, gender parity, spending per student, learning outcomes).
  - Identify which indicators correlate most strongly with learning outcomes.
  - Highlight 3 countries that over- or under-perform relative to their income level.
  - Write 3 key insights, noting where correlation should not be read as causation.
- **Constraints:** 6 hours. Dashboard tool of your choice (Streamlit, Power BI, Tableau Public). Data: World Bank EdStats or API, UNESCO UIS. Handle missing years and state how you did it.
- **Deliverable:** A link to a live or recorded interactive dashboard, the source code or workbook, and a one-page summary of the 3 insights.
- **Points:** 100

### Challenge 3: The Air We Breathe 
*SDG 3, 11 | Statistics + Storytelling | Satellite data option*
- **Scenario:** Air pollution is linked to millions of premature deaths each year. PM2.5 comes from traffic, cooking fuels, industry and burning, and varies by season, weekday and neighborhood. Many communities have no clear picture of how polluted their air is compared with health guidelines.
- **Objectives:**
  - Analyze PM2.5 for at least 3 cities, ideally on different continents, over at least one year.
  - Test at least one hypothesis statistically (for example weekday vs weekend, or dry vs rainy season).
  - Compare results with WHO air quality guidelines and explain the health implications.
- **Constraints:** 6 hours. Data: OpenAQ API, WHO Ambient Air Quality Database. Optional: NASA Earthdata (MODIS aerosol, TEMPO). Describe how you handled missing data, sensor faults and outliers.
- **Deliverable:** A notebook with the hypothesis test, and a 5-minute data story with at least 3 visuals.
- **Points:** 125

### Challenge 4: City Pulse: The Mobility Story 
*SDG 11, 9 | Analytics + Storytelling | Smart cities*
- **Scenario:** Bike-share, bus and taxi data reveal commuting rhythms, service gaps and the effect of weather or events. Cities use this to decide where to add bike lanes, stations or bus frequency, yet residents rarely see these patterns.
- **Objectives:**
  - Analyze at least one year of trip or ridership data from an open source.
  - Identify peak hours, busiest stations or routes, and underserved areas.
  - Test how rain and temperature affect demand.
  - Recommend 3 concrete infrastructure or service changes backed by the data.
- **Constraints:** 6 hours. Data: open bike-share feeds (for example Citi Bike), NYC TLC trips, GTFS feeds from the Mobility Database, Open-Meteo weather. Account for seasonality and holidays. Do not attempt to identify individual riders.
- **Deliverable:** A notebook and a 5-minute presentation including a map and the 3 recommendations.
- **Points:** 125

### Challenge 5: Mind the Water Gap 
*SDG 6, 10 | Geospatial + Analytics*
- **Scenario:** Billions of people still lack safely managed drinking water. National averages hide large gaps between rural and urban areas and between rich and poor regions. Policymakers need maps showing where to act first.
- **Objectives:**
  - Build a choropleth map of drinking water access at the finest administrative level you can find.
  - Rank the 10 regions with the largest access gaps and estimate the population affected.
  - Show at least one inequality angle (rural/urban, income or gender).
- **Constraints:** 6 hours. Tools: Folium, Plotly or QGIS. Data: WHO/UNICEF JMP, WorldPop, Natural Earth or GADM boundaries. Document how you matched boundaries between datasets and which population year you used.
- **Deliverable:** An interactive map (HTML or QGIS project) and a one-page policy note.
- **Points:** 125

### Challenge 6: Predict the Harvest 
*SDG 2, 13 | Predictive modelling | Satellite data option*
- **Scenario:** Smallholder farmers and food planners depend on rainfall and temperature, and a drought can cut yields sharply. Early yield estimates help governments plan imports, aid and storage.
- **Objectives:**
  - Predict national or regional maize or wheat yield from rainfall and temperature features.
  - Compare a linear baseline with a tree-based model.
  - Evaluate with a time-aware split (train on early years, test on later years).
  - Explain which weather features matter most.
- **Constraints:** 6 hours. Data: FAOSTAT yields, NASA POWER, CHIRPS rainfall. Random train/test splits are not allowed. Account for long-term yield trends.
- **Deliverable:** A notebook reporting RMSE and R², a feature-importance explanation (for example SHAP), and a half-page summary of limits.
- **Points:** 150

### Challenge 7: Build the Sensor Data Pipeline 
*SDG 9, 11 | Data engineering | Smart cities*
- **Scenario:** Smart city projects fail more often from broken data plumbing than from weak models. Sensors go offline, send duplicates or report impossible values. A pipeline that detects and handles this is the foundation of every later analytics or AI system.
- **Objectives:**
  - Ingest data from at least one open sensor or weather API on a schedule.
  - Validate it (range checks, duplicates, missing intervals) and log data quality issues.
  - Store it in a queryable format (DuckDB, SQLite or Parquet) with a documented schema.
  - Serve a simple dashboard or API showing the data and its quality status.
- **Constraints:** 6 hours. Data: OpenAQ, Sensor.Community or Open-Meteo. The whole system must run with one command (for example Docker Compose or a Makefile). Reruns must not create duplicate records. Respect API rate limits.
- **Deliverable:** A repository with tests for the validation rules, a README with the one-command setup, and a short demo of the dashboard or API.
- **Points:** 150 (judged with the engineering criteria: 7 points reproducibility, 8 points engineering quality)

### Challenge 8: SDG Explainer Bot 
*SDG 16, 17 | Intro to LLMs and RAG*
- **Scenario:** Policy reports are long, technical and inaccessible to the citizens they affect. Retrieval-augmented generation (RAG) lets an LLM answer from specific documents instead of guessing. A trustworthy bot must also know when to say "I don't know."
- **Objectives:**
  - Build a RAG chatbot over a small set of open documents (UN SDG reports, WHO guidance or a national policy).
  - Return each answer with a citation to the exact source passage.
  - Write a 10-question test sheet that includes questions the documents cannot answer, and report accuracy and refusal behavior.
- **Constraints:** 6 hours. Open models or free API tiers only. Suggested tools: Hugging Face, LangChain or LlamaIndex, ChromaDB or FAISS. Document your chunking choices.
- **Deliverable:** A working demo (web or notebook), the 10-question test sheet with results, and a short note on hallucination risks.
- **Points:** 150

---

## Intermediate

### Challenge 9: Where Should the Mini-Grid Go? 
*SDG 7, 1 | Geospatial optimization | Satellite data*
- **Scenario:** Hundreds of millions of people lack electricity. Grid extension is costly in remote areas, so solar mini-grids are often the fastest option. The best sites are unelectrified, reasonably dense, high in solar potential and close to roads and markets. NASA Black Marble night lights show where electricity is already used.
- **Objectives:**
  - Identify unelectrified settlements in a chosen country or region.
  - Score sites on population, solar potential, road access and economic activity with transparent weights.
  - Produce a ranked top-20 site map.
  - Run a sensitivity analysis showing how rankings change when the weights change.
- **Constraints:** 10 hours. Data: NASA Black Marble (VNP46) or VIIRS, WorldPop, Global Solar Atlas, OpenStreetMap, GRID3. Night lights can miss small or dim electrification, so state how you handled this.
- **Deliverable:** A map of the top 20 sites, the scoring code, and a sensitivity analysis report.
- **Points:** 200

### Challenge 10: Urban Heat Island Mapper 
*SDG 11, 13, 3 | Geospatial ML | Smart cities, satellite data*
- **Scenario:** Dense concrete and little vegetation make parts of cities several degrees hotter than their surroundings, raising heat-related illness and energy use. The burden often falls on low-income areas.
- **Objectives:**
  - Derive land surface temperature for a chosen city across several hot-season dates.
  - Model the relationship between temperature and vegetation, built-up area and water.
  - Combine heat with population (children, elderly, income proxies) to build a heat-vulnerability index.
  - Recommend 10 priority sites for greening and estimate the potential cooling effect.
- **Constraints:** 10 hours. Data: Landsat 8/9 thermal bands, MODIS or ECOSTRESS, Sentinel-2 for NDVI, WorldPop, OpenStreetMap. Google Earth Engine is allowed. Explain the difference between land surface and air temperature.
- **Deliverable:** A vulnerability map, a notebook, and a one-page recommendation brief for a city planner.
- **Points:** 200

### Challenge 11: Outbreak Early Warning 
*SDG 3, 13 | Time-series forecasting*
- **Scenario:** Malaria, dengue and cholera are sensitive to rainfall, temperature and humidity. If health systems know weeks in advance, they can pre-position drugs, nets and staff.
- **Objectives:**
  - Forecast weekly or monthly cases 4 to 8 weeks ahead for a chosen region.
  - Include lagged climate features and compare against a simple seasonal baseline.
  - Provide prediction intervals, not only point forecasts.
  - Propose an early-warning threshold and evaluate it by backtesting (false alarms vs missed outbreaks).
- **Constraints:** 10 hours. Data: OpenDengue, Malaria Atlas Project or national dashboards, ERA5, NASA GPM or POWER. Use rolling-origin validation. No random splits.
- **Deliverable:** A forecasting notebook, backtest results, and a one-page early-warning proposal.
- **Points:** 250

### Challenge 12: Smart Bin Collection Optimizer 
*SDG 11, 12, 13 | Optimization + simulation | Waste management, smart cities*
- **Scenario:** Many cities send trucks on fixed routes, collecting half-empty bins while others overflow. Fill-level sensors and predictive routing can cut fuel use, cost and emissions. Real sensor data is scarce, so teams must simulate sensibly.
- **Objectives:**
  - Build a simulator that generates bin fill levels from population density and land use, stating your assumptions.
  - Predict which bins will be full by the next collection window.
  - Solve the vehicle routing problem on a real road network and compare with a fixed schedule.
  - Quantify savings in distance, time and estimated CO2.
- **Constraints:** 10 hours. Tools: OSMnx, Google OR-Tools, SimPy. Data: OpenStreetMap, WorldPop, published emission factors. Test on scenarios the simulator was not tuned on.
- **Deliverable:** Simulator and routing code, a comparison table (fixed vs optimized), and a short assumptions and limits note.
- **Points:** 250

### Challenge 13: Trash Sorter on the Edge 
*SDG 12, 11 | Computer vision + edge deployment | Waste management, engineering*
- **Scenario:** Contamination, such as food-soiled plastic or mixed materials, ruins recyclable batches. Smart bins and sorting aids must run cheaply, offline and quickly, often on low-power hardware.
- **Objectives:**
  - Train an image classifier on open waste datasets (for example paper, plastic, glass, metal, organic).
  - Compress it (quantization, pruning or a small architecture) and export to TFLite or ONNX.
  - Report accuracy, model size and inference latency on real or emulated edge hardware.
  - Test on photos you take yourself and report the performance drop.
- **Constraints:** 10 hours. Data: TrashNet, TACO, Hugging Face waste datasets. Final model must be under 20 MB. Your own test photos must not be used in training.
- **Deliverable:** The exported model, a benchmark table (accuracy, size, latency), and a demo on a phone, Raspberry Pi or emulator.
- **Points:** 250 (judged with the engineering criteria)

### Challenge 14: Flood Footprint Mapper 
*SDG 13, 11 | Geospatial ML | Satellite data*
- **Scenario:** Floods are among the most frequent and costly disasters. Optical satellites are blocked by cloud, but radar (Sentinel-1 SAR) sees through it. Responders need to know quickly which roads, clinics and settlements are underwater.
- **Objectives:**
  - Choose a past flood event and build a flood segmentation model (thresholding or deep learning).
  - Report IoU or F1 against a reference flood map.
  - Overlay roads, health facilities and population to estimate exposure.
- **Constraints:** 10 hours. Data: Copernicus Sentinel-1/2, Sen1Floods11 or Global Flood Database, OpenStreetMap, WorldPop. Address permanent water bodies and radar speckle. Pre-downloaded scene subsets will be provided at the venue.
- **Deliverable:** A flood map, model scores, and a one-page situation summary listing exposed roads, facilities and people.
- **Points:** 300

### Challenge 15: Health Misinformation in Low-Resource Languages 
*SDG 3, 16 | NLP and LLMs*
- **Scenario:** Misinformation about vaccines, cures and outbreaks spreads quickly on messaging apps, often in local languages where moderation tools perform poorly. Most LLMs are trained mainly on English, so errors are higher exactly where they matter.
- **Objectives:**
  - Build or fine-tune a classifier, or design a prompt-based LLM pipeline, for misinformation detection in at least 2 languages (for example Swahili, Hausa, Amharic).
  - Report performance per language, not only overall.
  - Analyze false positives, especially where satire, religion or cultural context is wrongly flagged.
- **Constraints:** 10 hours. Data: Masakhane datasets, AfriSenti, AfriQA, Africa Check and other public fact-checks. If you translate or weakly label data, state the limits. Use open multilingual models or free tiers.
- **Deliverable:** The model or pipeline, and an evaluation report covering per-language results, bias, false positives and over-censorship risk.
- **Points:** 300

### Challenge 16: Food Security Analyst Agent 
*SDG 2, 1 | AI agents*
- **Scenario:** Analysts spend days combining price data, conflict reports, rainfall and crop statistics to assess hunger risk. An agent that calls data APIs, runs code and creates charts could speed this up, but only if its conclusions are traceable.
- **Objectives:**
  - Build an agent with at least 3 tools (data API access, code execution, chart generation).
  - Answer questions such as "Which East African countries face rising food insecurity, and why?"
  - Log every tool call and cite every number.
  - Compare 2 orchestration strategies (for example single agent vs planner-executor) on a small question set.
- **Constraints:** 10 hours. Data: FAOSTAT, World Bank API, FEWS NET, WFP HungerMap. Any open or free-tier LLM. Code execution must be sandboxed.
- **Deliverable:** The agent, a tool-use log for at least 5 questions, and a comparison of the 2 strategies (accuracy, cost, failures).
- **Points:** 300

---

## Advanced

### Challenge 17: Mapping Poverty Fairly 
*SDG 1, 10 | Predictive modelling + responsible AI | Satellite data*
- **Scenario:** Household surveys are expensive and infrequent, so ML models using satellite imagery and geodata fill the gaps. If such models are less accurate in remote, minority or data-poor regions, aid could be misdirected.
- **Objectives:**
  - Predict local wealth (for example a relative wealth index or survey-derived asset index) from geospatial features.
  - Provide calibrated uncertainty estimates.
  - Audit errors across rural/urban, region and data-density groups.
  - Write a model card with clear recommendations on appropriate and inappropriate uses.
- **Constraints:** 16 hours. Data: Meta Relative Wealth Index, DHS Program (register in advance), NASA Black Marble, WorldPop, OpenStreetMap. Use spatial cross-validation. Account for DHS location jitter.
- **Deliverable:** The model, an uncertainty calibration plot, a fairness audit report, and a model card.
- **Points:** 400

### Challenge 18: Red-Team the Public Health Assistant 
*SDG 3, 16 | AI security*
- **Scenario:** Health chatbots can be tricked into leaking private data, giving dangerous advice or following instructions hidden in documents. As governments and NGOs deploy such assistants, security testing is a requirement.
- **Objectives:**
  - Build a RAG assistant over open health guidelines with synthetic patient-style records.
  - Attack it with prompt injection, data exfiltration, jailbreaks and poisoned documents, mapped to the OWASP LLM Top 10.
  - Implement defenses (input and output filtering, PII redaction, retrieval permissions, least-privilege tools).
  - Measure attack success before and after defenses, plus the cost to legitimate users (over-refusal).
- **Constraints:** 16 hours. Data: WHO and CDC open guidelines and synthetic records only. No real patient data. Tools may include Garak, PyRIT and Presidio. Attacks must target only your own system.
- **Deliverable:** The assistant, an attack library, a threat model, and an attack-and-defense report with before/after metrics.
- **Points:** 400

### Challenge 19: Illegal Fishing Detector 
*SDG 14, 12 | Anomaly detection + trajectories*
- **Scenario:** Illegal, unreported and unregulated fishing depletes stocks and harms coastal communities. Vessels may turn off AIS transponders, loiter, or meet other ships at sea. With limited patrol resources, authorities need a short, reliable list of vessels to investigate.
- **Objectives:**
  - Engineer trajectory features (AIS gaps, loitering, speed patterns, encounters, time inside protected areas).
  - Detect anomalies with unsupervised, graph or semi-supervised methods.
  - Evaluate with precision-focused metrics on labeled events, since false accusations are costly.
  - Deploy a scoring API with monitoring and explainable flags.
- **Constraints:** 16 hours. Data: Global Fishing Watch (free non-commercial registration, sign up in advance), Marine Regions, Sentinel-1 vessel detections, MPAtlas. Treat AIS gaps in poor-coverage areas as possibly innocent.
- **Deliverable:** Flagged-vessel maps, an evaluation report, a running scoring API, and a note on legal and diplomatic sensitivity.
- **Points:** 450

### Challenge 20: Illegal Dumpsite Detection from Space
*SDG 11, 12, 3 | Remote sensing + weak supervision | Waste management, satellite data*
- **Scenario:** Unmanaged dumps release methane, leach toxins into groundwater and attract disease. Authorities rarely know where they all are, and ground surveys are slow and costly. Labeled examples are scarce, so methods must work with limited supervision.
- **Objectives:**
  - Build a detector or classifier for dumpsites using imagery and open labeled sets.
  - Use at least one technique for limited labels (self-supervised pretraining, few-shot learning or weak labels from OSM).
  - Evaluate with spatial cross-validation and report precision at a fixed review budget (for example top 100 flags).
  - Produce a ranked inspection list with confidence scores and a human-review workflow.
- **Constraints:** 16 hours. Data: AerialWaste (where available), Sentinel-2, OpenStreetMap, Google Open Buildings. Address look-alikes (quarries, construction, informal markets) and the social impact of flagging informal settlements.
- **Deliverable:** The model, a ranked inspection list for a test region, an evaluation report, and a short human-review protocol.
- **Points:** 450

### Challenge 21: Deforestation Early Warning 
*SDG 15, 13 | Spatiotemporal deep learning | Satellite data*
- **Scenario:** Forests store carbon, protect biodiversity and support livelihoods. Most monitoring is reactive, detecting loss after it happens. Predicting risk months ahead lets rangers and authorities focus patrols.
- **Objectives:**
  - Predict forest loss risk for the next 3 to 6 months in a chosen region (for example Congo Basin, Amazon or Southeast Asia).
  - Use time-series imagery plus roads, fire, terrain and protected-area features.
  - Validate with spatial cross-validation to avoid leakage between nearby pixels.
  - Write an MLOps plan covering drift monitoring and retraining.
- **Constraints:** 16 hours. Data: Hansen Global Forest Change, Global Forest Watch alerts, NASA FIRMS, Landsat, Sentinel-2, OpenStreetMap. Handle severe class imbalance and cloud cover. Pre-downloaded tiles will be provided.
- **Deliverable:** A risk map, the trained model, an evaluation report with spatial CV results, and the MLOps plan.
- **Points:** 450

### Challenge 22: Reinforcement Learning for Traffic Signals 
*SDG 11, 13, 9 | Reinforcement learning + simulation | Smart cities, engineering*
- **Scenario:** Most traffic signals run on fixed timings, wasting time and fuel. RL can adapt to live traffic, but controllers trained in simulation often break in the real world, and a failed controller can cause gridlock or safety risks.
- **Objectives:**
  - Build an RL controller for a multi-intersection network in an open traffic simulator.
  - Compare it with fixed-time and actuated baselines on waiting time, queue length and estimated emissions.
  - Stress-test with sensor dropouts, noisy detectors and demand surges.
  - Implement a safe fallback (for example revert to fixed timing when confidence is low) and measure its effect.
- **Constraints:** 16 hours. Tools: SUMO or CityFlow, Stable-Baselines3 or RLlib. Road networks from OpenStreetMap or the RESCO benchmark. Check that side roads are not unfairly delayed.
- **Deliverable:** The trained controller, a results table (baselines vs RL vs RL with fallback), and a robustness report.
- **Points:** 500 (judged with the engineering criteria)

### Challenge 23: Real-Time Urban Digital Twin Under Attack 
*SDG 9, 11, 16 | Streaming engineering + AI security | Smart cities, engineering*
- **Scenario:** Smart cities depend on live feeds for traffic, air quality and public transport. If an attacker or faulty device injects false readings, automated decisions such as rerouting traffic or issuing health alerts can go wrong.
- **Objectives:**
  - Build a streaming pipeline (for example Kafka or Redpanda) ingesting at least 3 live or replayed feeds and maintaining a live city-state view.
  - Define latency and availability targets and measure them under load.
  - Simulate attacks (spoofed sensors, replayed data, drift, flooding) and detect them with anomaly detection and cross-sensor consistency checks.
  - Report detection rates, false alarms, and what the system does when it distrusts a feed.
- **Constraints:** 16 hours. Data: GTFS-Realtime, OpenAQ, Open-Meteo, Sensor.Community, public IoT security datasets (for example ToN-IoT). Observability with Grafana or Prometheus is expected. Attacks must target only your own system.
- **Deliverable:** A repository with one-command setup, a dashboard, load-test results, and an attack-and-detection report.
- **Points:** 500 (judged with the engineering criteria)

### Challenge 24: Multi-Agent Disaster Response Coordinator 
*SDG 11, 13, 17 | Agents + geospatial | Satellite data*
- **Scenario:** When an earthquake, cyclone or flood strikes, responders are overwhelmed by alerts, social media and satellite feeds. Coordination, not information, is often the bottleneck. A multi-agent system could monitor alerts, estimate impact and draft plans, but errors in a crisis are costly and need human oversight.
- **Objectives:**
  - Build agents for monitoring, impact estimation (affected population and infrastructure), logistics (candidate routes and facilities) and communications (situation report).
  - Ingest at least one live or replayed hazard feed.
  - Require human approval before any recommendation is "released."
  - Document failure modes (stale data, conflicting reports, hallucinated locations) and how the system handles them.
- **Constraints:** 16 hours. Data: GDACS, USGS feeds, ReliefWeb API, NASA FIRMS, OpenStreetMap, WorldPop. Test on a replayed historical event, never on a live emergency. Open or free-tier LLMs.
- **Deliverable:** A working prototype, agent traces for at least one event, a sample situation report, and a failure-mode analysis.
- **Points:** 600
