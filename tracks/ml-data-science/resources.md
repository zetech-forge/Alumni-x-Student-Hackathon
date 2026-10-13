---
title: Curated Resources
parent: Machine Learning & Data Science
nav_order: 2
---

# Curated Resources

A short list of well-chosen resources for the three challenges: **Climate Sentinel** (Challenge 1), **Malaria Atlas Lab** (Challenge 2) and **Product Copilot** (Challenge 3). Everything here is **free**. A few services need free registration or an application, which is marked "Free (registration)". Register early, because some approvals take days. The [Course](course.md) page explains the ideas, and these links are for going deeper. The "Used in" column shows which challenge the resource helps most.

## 1. Python and data wrangling

| Resource | Type | Free/Paid | Used in | Why it's useful |
|---|---|---|---|---|
| [The Python Tutorial](https://docs.python.org/3/tutorial/) | Official tutorial | Free | All | The standard beginner path through the language |
| [Google Colab](https://colab.research.google.com/) | Tool | Free (Google account) | All | Run notebooks in the browser with nothing to install, including free GPU time |
| [JupyterLab documentation](https://docs.jupyter.org/en/latest/) | Documentation | Free | All | Notebook tips and setup |
| [NumPy: Absolute Beginners](https://numpy.org/doc/stable/user/absolute_beginners.html) | Tutorial | Free | All | Arrays and fast maths, which every other library builds on |
| [10 minutes to pandas](https://pandas.pydata.org/docs/user_guide/10min.html) | Tutorial | Free | All | The fastest tour of tables in Python |
| [pandas: Merge, join, concatenate](https://pandas.pydata.org/docs/user_guide/merging.html) | Documentation | Free | All | Joins are the biggest source of silent bugs |
| [pandas: Time series](https://pandas.pydata.org/docs/user_guide/timeseries.html) | Documentation | Free | 1, 2 | Dates, resampling, lags and rolling windows |
| [Pro Git book](https://git-scm.com/book/en/v2) | Book | Free | All | Everything about Git; the first two chapters are enough for the event |
| [GitHub Docs: Get started](https://docs.github.com/en/get-started) | Documentation | Free | All | Repositories, commits and pull requests |

## 2. Visualization, dashboards and statistics

| Resource | Type | Free/Paid | Used in | Why it's useful |
|---|---|---|---|---|
| [Matplotlib quick start](https://matplotlib.org/stable/users/explain/quick_start.html) | Tutorial | Free | All | The base charting library |
| [Seaborn tutorial](https://seaborn.pydata.org/tutorial.html) | Tutorial | Free | 1, 2 | Statistical charts with little code |
| [Plotly Python](https://plotly.com/python/getting-started/) | Documentation | Free | 1, 2 | Interactive charts for dashboards |
| [Streamlit: Get started](https://docs.streamlit.io/get-started) | Documentation | Free | All | A dashboard or demo app from a Python file in minutes |
| [Gradio](https://www.gradio.app/guides/quickstart) | Documentation | Free | 3 | A demo app with microphone, image upload and chat built in |
| [Streamlit Community Cloud](https://docs.streamlit.io/deploy/streamlit-community-cloud) | Hosting | Free | All | Put your demo online so judges can open it |
| [SciPy statistics tutorial](https://docs.scipy.org/doc/scipy/tutorial/stats.html) | Tutorial | Free | 1, 2 | Compare groups and report the size of a difference |
| [statsmodels: Meta-analysis](https://www.statsmodels.org/stable/meta_analysis.html) | Documentation | Free | 2 | Pool results from several studies with fixed and random effects |

## 3. Open data: weather, climate and hazards (Challenge 1)

| Resource | Type | Free/Paid | Used in | Why it's useful |
|---|---|---|---|---|
| [Open-Meteo](https://open-meteo.com/en/docs) | API | Free | 1, 2 | Weather history and live forecasts, no key needed for light use |
| [CHIRPS](https://www.chc.ucsb.edu/data/chirps) | Dataset | Free | 1, 2 | Satellite and station rainfall since 1981, to cross-check Open-Meteo |
| [ERA5 (Copernicus Climate Data Store)](https://cds.climate.copernicus.eu/) | Dataset | Free (registration) | 1, 2 | Consistent global historical weather |
| [NOAA CPC: Oceanic Niño Index (ONI)](https://www.cpc.ncep.noaa.gov/data/indices/) | Dataset | Free | 1 | Monthly El Niño and La Niña index to use as a seasonal predictor |
| [IBTrACS](https://www.ncei.noaa.gov/products/international-best-track-archive) | Dataset | Free | 1 | Global archive of historical tropical cyclone tracks |
| [EM-DAT](https://www.emdat.be/) | Database | Free (registration) | 1 | Documented disaster events to validate your hazard indicators |
| [ReliefWeb API](https://apidoc.reliefweb.int/) | API | Free (registered app name) | 1 | Humanitarian reports of real floods, droughts and storms |
| [GDACS](https://www.gdacs.org/) | Alert feed | Free | 1 | See what real disaster alerts look like |
| [FEWS NET](https://fews.net/) | Reports and data | Free | 1 | Food security and drought outlooks to compare with your own |
| [WorldPop](https://www.worldpop.org/) | Dataset | Free | 1, 2 | Population grids to count people exposed or at risk |
| [geoBoundaries](https://www.geoboundaries.org/) | Dataset | Free | 1, 2 | Open administrative boundaries (districts, regions) for most countries |
| [NASA MODIS vegetation indices](https://modis.gsfc.nasa.gov/data/dataprod/mod13.php) | Dataset | Free | 1 | NDVI to confirm drought on the ground (stretch goal) |
| [WMO: Standardized Precipitation Index User Guide](https://library.wmo.int/idurl/4/39629) | Guide | Free | 1 | The official method for SPI (stretch goal) |
| [WMO: Early Warnings for All](https://wmo.int/earlywarningsforall) | Reference | Free | 1 | Guidance to cite in your playbook, and the role of national warning services |
| [UN SDGs](https://sdgs.un.org/goals) | Reference | Free | All | Goals and targets to link your solution to |

## 4. Open data: malaria and health (Challenge 2)

| Resource | Type | Free/Paid | Used in | Why it's useful |
|---|---|---|---|---|
| [Malaria Atlas Project](https://malariaatlas.org/) | Data and maps | Free | 2 | Parasite rate surveys, prevalence surfaces, vector occurrence and more |
| [malariaAtlas R package](https://cran.r-project.org/package=malariaAtlas) | Software | Free | 2 | Download MAP data in R, if a teammate uses R |
| [WWARN](https://www.wwarn.org/) | Data and tools | Free (registration) | 2 | Antimalarial efficacy and molecular marker data from clinical studies |
| [WHO Malaria Threats Map](https://apps.who.int/malaria/maps/threats/) | Data and maps | Free | 2 | Drug efficacy, resistance markers and vector resistance, by country and year |
| [MalariaGEN Pf7 data resource](https://www.malariagen.net/resource/34) | Genomic data | Free | 2 | Parasite genomes with resistance marker calls (stretch goal) |
| [WHO World Malaria Report](https://www.who.int/teams/global-malaria-programme/reports) | Report | Free | 2 | Official burden figures to compare with your model |
| [WHO Guidelines for malaria](https://www.who.int/teams/global-malaria-programme/guidelines-for-malaria) | Guidelines | Free | 2 | The documents your agent's guideline tool should cite |
| [WHO: Report on antimalarial drug efficacy, resistance and response](https://www.who.int/publications/i/item/9789241512817) | Report | Free | 2 | Background on efficacy studies and resistance markers |
| [DHS Program](https://dhsprogram.com/data/) | Household surveys | Free (registration, apply early) | 2 | Malaria indicator surveys. GPS cluster locations are a separate request |
| [OpenStreetMap: Downloading data](https://wiki.openstreetmap.org/wiki/Downloading_data) | Reference | Free | 2 | Health facilities, roads and rivers for access and covariates |
| [WorldClim](https://www.worldclim.org/data/index.html) | Dataset | Free | 2 | Temperature and rainfall climatologies as covariates |
| [SRTM elevation (USGS EarthExplorer)](https://earthexplorer.usgs.gov/) | Dataset | Free (registration) | 2 | Elevation covariate; highland malaria differs strongly from lowland |
| [GBIF](https://www.gbif.org/) | Database | Free | 2 | Presence-only occurrence records, a good model for the species-mapping task |

## 5. Geospatial tools

| Resource | Type | Free/Paid | Used in | Why it's useful |
|---|---|---|---|---|
| [GeoPandas introduction](https://geopandas.org/en/stable/getting_started/introduction.html) | Tutorial | Free | 1, 2 | Vector data and maps in Python |
| [GeoPandas: Managing projections](https://geopandas.org/en/stable/docs/user_guide/projections.html) | Documentation | Free | 1, 2 | Fixes the most common geospatial bug (measuring in degrees) |
| [GeoPandas: Interactive mapping](https://geopandas.org/en/stable/docs/user_guide/interactive_mapping.html) | Documentation | Free | 1, 2 | A map in one line of code |
| [Folium](https://python-visualization.github.io/folium/latest/getting_started.html) | Documentation | Free | 1, 2 | Custom interactive web maps |
| [Rasterio quickstart](https://rasterio.readthedocs.io/en/stable/quickstart.html) | Tutorial | Free | 1, 2 | Read and process raster data (population, rainfall, covariates) |
| [rasterstats](https://pythonhosted.org/rasterstats/) | Documentation | Free | 1, 2 | Add up raster values (such as people) inside polygons |
| [xarray: Quick overview](https://docs.xarray.dev/en/stable/getting-started-guide/quick-overview.html) | Documentation | Free | 1, 2 | Climate data cubes (NetCDF) |
| [PySAL](https://pysal.org/) | Library | Free | 2 | Spatial autocorrelation (Moran's I) and spatial statistics |
| [QGIS Training Manual](https://docs.qgis.org/latest/en/docs/training_manual/index.html) | Course | Free | All | Point-and-click GIS to check that layers line up |

## 6. Machine learning, forecasting and uncertainty

| Resource | Type | Free/Paid | Used in | Why it's useful |
|---|---|---|---|---|
| [scikit-learn: Getting started](https://scikit-learn.org/stable/getting_started.html) | Tutorial | Free | All | The standard workflow in code |
| [scikit-learn: Cross-validation](https://scikit-learn.org/stable/modules/cross_validation.html) | Documentation | Free | All | Time and group splits that avoid leakage |
| [scikit-learn: Common pitfalls](https://scikit-learn.org/stable/common_pitfalls.html) | Documentation | Free | All | The mistakes that ruin hackathon scores |
| [scikit-learn: Metrics and scoring](https://scikit-learn.org/stable/modules/model_evaluation.html) | Documentation | Free | All | Choosing the right metric, including the Brier score |
| [scikit-learn: Probability calibration](https://scikit-learn.org/stable/modules/calibration.html) | Documentation | Free | 1, 2 | Check that predicted probabilities mean what they say |
| [SHAP documentation](https://shap.readthedocs.io/en/latest/) | Documentation | Free | 1, 2 | Explaining which features drive a prediction |
| [Forecasting: Principles and Practice](https://otexts.com/fpp3/) | Free online book | Free | 1 | The best plain introduction to forecasting and lag features |
| [pymannkendall](https://pypi.org/project/pymannkendall/) | Library | Free | 1 | Trend significance tests for climate series |
| [climate_indices](https://github.com/monocongo/climate_indices) | Library | Free | 1 | SPI and other drought indices (stretch goal) |
| [MAPIE](https://mapie.readthedocs.io/) | Documentation | Free | 1, 2 | Prediction intervals for any model |

## 7. LLMs, agents, speech and vision

| Resource | Type | Free/Paid | Used in | Why it's useful |
|---|---|---|---|---|
| [Hugging Face LLM Course](https://huggingface.co/learn/llm-course/chapter1/1) | Course | Free | All | A complete, practical course on language models |
| [Hugging Face Agents Course](https://huggingface.co/learn/agents-course) | Course | Free | All | Builds agents with open models |
| [Prompt engineering overview (Anthropic)](https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/overview) | Documentation | Free | All | How to write clear, reliable prompts |
| [Building effective agents (Anthropic)](https://www.anthropic.com/engineering/building-effective-agents) | Article | Free | All | Why simple agent designs usually win |
| [Tool use overview (Anthropic)](https://docs.claude.com/en/docs/agents-and-tools/tool-use/overview) | Documentation | Free | All | How tool calling works in code |
| [Model Context Protocol](https://modelcontextprotocol.io/) | Specification | Free | 2, 3 | A standard way to connect tools and data |
| [Ollama](https://ollama.com/) | Tool | Free | All | Run open models on your own laptop |
| [Sentence Transformers](https://www.sbert.net/) | Library | Free | 2, 3 | Text and image embeddings (including CLIP models) for retrieval |
| [Chroma](https://docs.trychroma.com/) and [FAISS](https://github.com/facebookresearch/faiss/wiki) | Vector stores | Free | 2, 3 | Store embeddings and filter by metadata such as user role |
| [Ragas](https://docs.ragas.io/) | Evaluation library | Free | 2, 3 | Score retrieval and answer quality |
| [Whisper](https://github.com/openai/whisper) and [faster-whisper](https://github.com/SYSTRAN/faster-whisper) | Speech models | Free | 3 | Open speech-to-text, including multilingual models |
| [jiwer](https://github.com/jitsi/jiwer) | Library | Free | 3 | Compute word error rate for speech transcription |
| [Tesseract OCR](https://tesseract-ocr.github.io/tessdoc/) and [EasyOCR](https://github.com/JaidedAI/EasyOCR) | Tools | Free | 3 | Read nameplates, labels and scanned manual pages |
| [PyMuPDF](https://pymupdf.readthedocs.io/) and [pdfplumber](https://github.com/jsvine/pdfplumber) | Libraries | Free | 3 | Extract text, tables and page numbers from manuals |
| [Hugging Face Transformers](https://huggingface.co/docs/transformers/index) | Library | Free | 3 | Open vision-language and speech models |

## 8. Responsible AI and AI security

| Resource | Type | Free/Paid | Used in | Why it's useful |
|---|---|---|---|---|
| [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) | Reference | Free | 3 | The standard list of LLM risks to test against |
| [MITRE ATLAS](https://atlas.mitre.org/) | Knowledge base | Free | 3 | Real-world attack techniques against AI systems |
| [garak](https://github.com/NVIDIA/garak) | Tool | Free | 3 | Automated scanning of language models for weaknesses |
| [PyRIT](https://github.com/Azure/PyRIT) | Tool | Free | 3 | A toolkit for AI risk testing |
| [Presidio](https://microsoft.github.io/presidio/) | Tool | Free | 3 | Find and redact personal data |
| [Fairlearn user guide](https://fairlearn.org/main/user_guide/index.html) | Documentation | Free | All | Measure model errors across groups |
| [Model Cards for Model Reporting](https://arxiv.org/abs/1810.03993) | Paper | Free | All | The idea behind the model card you must submit |
| [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework) | Framework | Free | 3 | A structure for thinking about AI risk |
| [Creative Commons licenses](https://creativecommons.org/share-your-work/cclicenses/) | Reference | Free | All | Understand what you may do with open data, manuals and images |

## 9. Engineering and reproducibility

| Resource | Type | Free/Paid | Used in | Why it's useful |
|---|---|---|---|---|
| [Docker: Get started](https://docs.docker.com/get-started/) | Tutorial | Free | 2, 3 | One-command setup for the rebuild |
| [pytest: Get started](https://docs.pytest.org/en/stable/getting-started.html) | Tutorial | Free | 2, 3 | Simple tests that earn reproducibility marks |
| [FastAPI tutorial](https://fastapi.tiangolo.com/tutorial/) | Tutorial | Free | 3 | Expose your system as an API (stretch goal) |
| [DuckDB documentation](https://duckdb.org/docs/) | Documentation | Free | 2, 3 | A fast local database for specification and price tables |
| [Pandera](https://pandera.readthedocs.io/) | Library | Free | 2, 3 | Validate tables: ranges, types, units, duplicates |

## How to use these resources

- Start with the **Course** page. Open a link only when you need more detail on that exact topic.
- Check the **version** in the address ("stable" or "latest"). Old blog posts often show outdated code.
- If a link breaks, search for the page title on the tool's official site. Documentation sites sometimes reorganize.
- Always record your data sources, access dates and licenses in your README.