## `crosstalk` Lesson

This repository contains a sample lesson on interactive R Markdown content with `crosstalk`. This lesson was prepared as part of the RStudio Instructor Certification exam process and has been modified for multiple forms. This lessons develops skills needed to build an browser-based application like the example shown [here](https://emilyriederer.github.io/demo-crosstalk/analysis/demo.html).

Contents include:

- `src`: Script to pull and prep CTA data used in lesson
- `data`: Datasets used in lesson (created by file in `src`)

For live teaching:

- `analysis`: 
  + `demo.{Rmd/html}`: Fully built-out demo (source creating link above)
  + `lecture-complete.Rmd`: A master version of the notebook to use in lesson with all code filled in
  + `lecture-partial.Rmd`: A version of lesson material with code chunks deleted for live coding
- `assessment`: `learnr` tutorial with two formative assessments
  + As of writing, this assessment is also available on [shinyapps.io](https://emilyriederer.shinyapps.io/crosstalk-assessment/)
  + If it is later removed, you may run it locally in RStudio from the `.Rmd` file in this repo

Related Google Slides are available [here](https://docs.google.com/presentation/d/1yH_T5erAkK7EVP3SlaLW9sNHN7r94UOZHKkVxOSi9x0/edit#slide=id.g95f687e584_0_1620)

For self-exploration:

- `tutorial`:
  + `tutorial-learnr.Rmd`: `learnr` tutorial that can be run locally or viewed on [shinyapps.io]() (hosted version may be removed in the future)
  + `tutorial-rmd.{Rmd/html}`: static tutorial which can be read [here](https://emilyriederer.github.io/demo-crosstalk/tutorial/tutorial-rmd.html)
