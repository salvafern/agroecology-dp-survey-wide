# Agroecology Survey Data: tabular, wide format

Recommendations for organizing survey data in the Agroecology partnership following a wide, spreadsheet format approach. This structure is inspired by the data structure American National Election Studies (ANES, 2022) and the recommendations of Zimmer et al. (2024), applying a tidy data approach (Wickham, 2014) with usability on mind and enabling a later transformation into Open Linked Data as structured in The Survey Ontology (Scrocca et al., 2021).

## Codebook

Codebooks contain all the information needed to explain the questions formulated in the survey. An unique identifier within the survey (a code) is assigned to each question, allowing later to link all the information about the question to the answers provided by the participants. Codebooks are typically stored as `pdf`, `docx` or `xlsx` files. For the sake of interoperability, we propose to use text delimited files. These type of files are largely used in data science. they have several advantages, including easy machine-readability and being an open format with no owner, which ensures data will remain readable and understandable by many different softwares for a long time. 

This is a `csv` file, delimited by semicolons `;`. We avoid colons `,` as these can be used in free text, open questions. They would affect the structure of the data. We recommend to prohibit the use of semicolons `;` in the answers provided by the participants, the questions, and in general in any use that is not deliming the columns of the table.

The codebook can be used as well during the design of the survey.

The example below shows an hypothetical survey codebook about the user satisfaction using an online platform. 

`./codebook.csv`

| Code            | Label        | Type    | QuestionText                             | Values                                                       | Cardinality | QuestionType |
| --------------- | ------------ | ------- | ---------------------------------------- | ------------------------------------------------------------ | ----------- | ------------ |
| Q1_age          | Age          | integer | What is your age?                        |                                                              | 1..1        | SingleChoice |
| Q2_gender       | Gender       | string  | What is your gender?                     | Female&#124;Male&#124;Other                                  | 1..1        | SingleChoice |
| Q3_satisfaction | Satisfaction | integer | How satisfied are you with the platform? | 1=Very unsatisfied&#124;2=Unsatisfied&#124;3=Neutral&#124;4=Satisfied&#124;5=Very satisfied | 1..1        | SingleChoice |
| Q4_improvement  | Improvement  | string  | What would you improve in the platform?  |                                                              | 0..n        | FreeText     |



Each row in the codebook describes a survey question. Below is an explanation of each column:

- **Code**: A unique identifier for the question. It must be unique within the survey.

- **Label**: A short, human-readable label or name for the variable that can be used in spreadsheets or statistical software.

- **Type**: The data type of the answer. Common types include "integer", "string", "boolean", or "date".

- **QuestionText**: The full text of the question as it was asked in the survey.

- **Values**: A list of possible values for closed questions. Options are separated by vertical bars (|), and value labels can be assigned using the equals sign (=). For open or free-text questions, this field is left empty.

- **Cardinality**: Indicates how many answers are allowed. The cardinality pattern is `min..max`, where the first number is the minimum required answers and the second is the maximum allowed.  `n` denotes “no fixed upper limit,” so `1..1` means exactly one answer, while `0..n` means the question may be skipped or answered multiple times.

- **QuestionType**: Describes the nature of the question. Typical values include "SingleChoice", "MultipleChoice" or "FreeText"



## Responses

Answers to the survey are recorded in another `responses.csv` file. Every row of this file corresponds to a participant, and every column is named after the `code` in `codebook.csv`. This allows to link easily the information about the questions without getting the responses file full of details that difficult the analysis.

| respondent_id | Q1_age | Q2_gender | Q3_satisfaction | Q4_improvement                          |
| ------------- | ------ | --------- | --------------- | --------------------------------------- |
| 001           | 34     | female    | 4               | I think the platform is user-friendly   |
| 002           | 29     | male      | 5               | Needs better support for collaboration. |

We recommend to include an unique identifier for every respondent, here named as `respondent_id`. This allows to annomymize the survey without loosing the link to the private information about the respondents that might have been collected (e.g. name, email, address) and that it must be treated according to the European Parliament Directive 95/46/EC (General Data Protection Regulation, or GDPR). Personal data collected in the Agroecology partnership must never be published or leaked in any form. 



## References

ANES (2020) Time Series Study Full Release: User Guide and Codebook.” https://electionstudies.org/wp-content/uploads/2022/02/anes_timeseries_2020_userguidecodebook_20220210.pdf.

Mario Scrocca, Damiano Scandolari, Gloria Re Calegari, Ilaria Baroni and Irene Celino. *The Survey Ontology: Packaging Survey Research as Research Objects*, Proceedings of the 2nd Workshop on Data and Research Objects Management for Linked Open Science - co-located with ISWC 2021, https://doi.org/10.4126/FRL01-006429412, 2021.

Wickham, H. . (2014). Tidy Data. *Journal of Statistical Software*, *59*(10), 1–23. https://doi.org/10.18637/jss.v059.i10

Zimmer, S. A., Powell, R. J., & Velásquez, I. C. (2024). *Exploring Complex Survey Data Analysis Using R: A Tidy Introduction with {srvyr} and {survey}*. Chapman & Hall: CRC Press.