# DSCI 522: Predicting tea category from its caffeine level

**DSCI 522 Team 12**

Authors: **Clarissa Nada Dahjan, Julia Gorospe, Kangju Sun, Yingwen Liu**

## Summary

We used the [Chinese Tea Dataset](https://chinatea.house/dataset/) to ask whether a Chinese tea's caffiene level can predict its category. The dataset describes 136 Chinese teas, and we compared three classifiers: a baseline that always predicts the most common category, a decision tree that uses only caffeine level (low / moderate / high), and a decision tree that also uses body and oxidation levels as features. Using a 3-fold cross-validation on the traiing data, the baseline reached 25.9% accuracy and the caffeine-only model had an accuracy of 44.4%. Adding body and oxidation level as feartures increased its accuracy to 88.0%, reaching 78.6% on the test set. From this, we see that caffeine level alone does a poor job of telling tea categories apart, mostly because most teas are labelled with "moderate" caffeine levels in this data set. 

## Report

The final report can be found [here in PDF format](analysis/tea-category-predictor.pdf).

## Dependencies

We use [Docker](https://www.docker.com/) to run the analysis with the same software and package versions. The image is published on Docker Hub at [xilillusion/dsci-522-predicting-tea-category-from-its-caffeine-level](https://hub.docker.com/r/xilillusion/dsci-522-predicting-tea-category-from-its-caffeine-level). This installs uv, Quarto, and Python with the packages listed in `pyproject.toml` where exact versions are locked in `uv.lock`.

## Running the Project

Please refer to the Dependencies section for Docker and Docker Image usage before proceeding with the next steps:

If this is your first time running the project, install and launch [Docker](https://www.docker.com/). 

Then, clone this repository and move into it:

   ``` bash
   git clone https://github.com/UBC-MDS-2026-27/DSCI-522-Predicting-tea-category-from-its-caffeine-level.git
   cd DSCI-522-Predicting-tea-category-from-its-caffeine-level
   ```

Once cloned, execute the following commands from the root of this repository.

1. If you don't have an ssh key yet, make one with the following command and press Enter at each question that it prompts you. This key is what gives you access to the Docker container.

``` bash
ssh-keygen -t ed25519
```

2. Download the [image](https://hub.docker.com/r/xilillusion dsci-522-predicting-tea-category-from-its-caffeine-level).

``` bash
docker compose pull
```

3. Run the analysis and render the report. 

``` bash
docker compose run -rm analysis-env uv run quarto render
```

Rendering runs each code block in the Quarto document, so it may take a few minutes to fully finish. There are data loading and manipulation blocks, so there will be expected changes to files in data/raw/ and data/processed/. The rendered report is written to analysis/tea-category-predictor.pdf, updating the version in the repository. The `-rm` tag allows the container to remove itself whenever the render is complete.


## AI Usage Statement

We used a mix of Claude and ChatGPT to help with data analysis, explain the logic, review our workflow, and check our code. All code and suggested changes were reviewed and tested by team members before being pushed to the repository. We take full responsibility for the content of this repository.

Example prompts:

- "Explain the logic of this code."
- "Check if our analysis steps make sense."
- "Check the Python code for errors."
- "Can you proofread this sentence to check if it makes sense, and if it is an effective statement?"

## License

Code within the Tea Category Predictor report is licensed under the MIT License, and the report's contents are licensed under the CC BY-NC-ND 4.0. If reusing or mentioning contents in this report, please provide attribution and link to this repository. Please see our [license document](LICENSE.md) for more details

## References
Chen, L., Liu, F., Yang, Y., Tu, Z., Lin, J., Ye, Y., Xu, P. (2021). Oxygen-enriched fermentation improves the taste of black tea by reducing the bitter and astringent metabolites. *Food Research International, 148, Article 110613. Available from: https://doi.org/10.1016/j.foodres.2021.110613

China Tea House. Chinese Tea Dataset. Accessed Nov 16, 2026. Available from: <https://chinatea.house/dataset/>

Oliveira, Rafaela. (2012). Quantification of catechins and caffeine from green tea (Camellia sinensis) infusions, extract, and ready-to-drink beverages. Food Science and Technology. 32. 163-166. 10.1590/S0101-20612012005000009. 

Yong, L., Song, Y., Xiao, X., Sui, H., Xu, H., Tan, R., Yang, X., Song, J., Li, J., & Wei, S. (2022). Quantitative probabilistic assessment of caffeine intake from tea in Chinese adult consumers based on nationwide caffeine content determination and tea consumption survey. *Food and Chemical Toxicology, 165*, Article 113102. <https://doi.org/10.1016/j.fct.2022.113102>

Zhang, S., Jin, J., Chen, J., Ercisli, S., & Chen, L. (2022). Purine alkaloids in tea plants: Component, biosynthetic mechanism and genetic variation. *Beverage Plant Research, 2*, Article 13. <https://doi.org/10.48130/BPR-2022-0013>

