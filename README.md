# Persistent Identifier (PID) Knowledge Graph – Automated population of PID properties with LLMs


## Repository overview 
- [`query_api.ipynb`](query_api.ipynb): Notebook that feeds prompts requesting information about properties to LLM models via their API. Results in CSV files containing each model response with a unique identifier ([`llm_output_rich.csv`](data/llm_output_rich.csv) for the full responses, [`llm_output_small.csv`](data/llm_output_small.csv) for a concise version). 
- [`evaluate.ipynb`](evaluate.ipynb): Notebook that performs a (to be expanded) evaluation on the model outputs. Results in the file [`llm_evaluation.csv`](data/llm_evaluation.csv).  
- the [`data`](/data) folder holds the resulting LLM responses for each property-PID pair, as well as modified versions of it that make evaluation and inspection easier. 



## Project background
The goal of this experiment is to evaluate a selection of Large Language Models (LLMs) on the task of generating the values of three pre-defined properties of persistent identifiers. These properties and its categories are as follows: 
- Governance Mechanism: Community Governance, Membership Governance, Closed Governance, Unknown
- Prefixes and Identifier Structure: Allows User Semantics, Allows Managed Prefix, No Prefix, Predefined Identifier Structure, Unknown 
- Kernel Metadata Schema: No Metadata Schema Prescribed, Common Metadata Schema for Identifier, Metadata Schema per Entity, Custom/Non-Standard Schema, Unknown


Models were selected on the basis of performance, free or low-cost accessibility, and whether they are open-source. Two of three models used are open source. 
The following models were selected: 
- Sonar Pro
- LLAMA 3.1 Online (llama-3.1-sonar-small-128k-online)
- Mistral


## Evaluation 
Models were evaluated in terms of their agreement on a property. Agreement scores were assigned to each row (containing a prompt and three model responses, one for each model). The agreement score can have a value between 1 and 3. Here's what they mean: 
- 3: All three models gave the same response
- 2: Two models gave the same response
- 1: No model gave the same response

An additional value was added: 3: Unknown. This score means that all models agreed that the property information was unknown, thus not generating an answer that can be used in the knowledge base, but nevertheless a full agreement. 

Table 1 displays the agreement scores across the dataset. You can see that it’s relatively rare (n = 28) that three models fully agree on the answer. A majority vote is reached in many cases (n = 218), but for a considerable number of prompts, no agreement is reached at all (n = 142). 


| Agreement score | Count | 
| ---- | ---- | 
| 1 | 142 | 
| 2 | 218 | 
| 3 | 28 | 
| 3: Unknown | 8 | 

*Table 1: Agreement scores on all prompts.*

Note: This evaluation method is imperfect, because three lies do not make a truth. It could be possible that all models generate the same wrong answer. Nevertheless, the agreement score was taken as a metric for performance in this initial experiment as a quick first quality check. More robust evaluation can be done by annotating a handful of PIDs with the correct values of the properties and comparing it to the models’ responses. 

