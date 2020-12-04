# Overview

The Defeasible-NLI dataset consists of three portions, extending the ATOMIC (Sap et al. 2019), SNLI (Bowman et al., 2015), and Social-Chemistry-101 (Forbes et al., 2020) datasets. These portions are called defeasible-atomic, defeasible-snli, and defeasible-social, respectively. (Or "delta-atomic," "delta-snli," and "delta-social" for short.)

```
└── data
    └── defeasible-nli
        ├── defeasible-atomic
        │   ├── dev.jsonl
        │   ├── test.jsonl
        │   └── train.jsonl
        ├── defeasible-snli
        │   ├── dev.jsonl
        │   ├── test.jsonl
        │   └── train.jsonl
        └── defeasible-social
            ├── dev.jsonl
            ├── test.jsonl
            └── train.jsonl
```

The train/dev/test splits are consistent with the original splits in each of these datasets.

# Data Format

Each line represents a JSON object with a single Premise-Hypothesis-Update tuple (or, in the case of delta-social, just Hypothesis-Update tuples), and additional fields for meta-data. Some fields are shared across all three sections, and others are dataset-specific.

## Shared Fields

**DataSource** :: The originating dataset.

**AssignmentIdAnon** :: Mechanical Turk assignment ID mapped to integers unique within the dataset.

**WorkerIdAnon** :: An anonymized integer ID for each Mechanical Turk annotator.

**Premise** :: The premise (P) sentence. Only present for ATOMIC and SNLI portions. For delta-atomic the premise is the antecedent event description. For delta-snli, the premise is straightforwardly the SNLI premise.

**Hypothesis** :: The hypothesis (H) sentence. Present for all three portions. For delta-atomic, it is the right-hand side inference. For delta-snli it is straightforwardly the SNLI hypothesis. For delta-social, it is the "rule of thumb" (and matches the "SocialChemROT" field identically.)

**Update** :: The update sentence (U) written by the annotator, which is either a strengthener or a weakener. (Novel to defeasible-NLI.)

**UpdateType** :: Indicates whether the update (U) is a strengthener or weakener. Values are "strengthener" or "weakener".

**UpdateTypeImpossible** :: Boolean indicating whether the annotator checked the "impossible" box. If true, the annotator found it impossible to write an update (of type UpdateType) for the given premise-hypothesis pair. If value is true, then Update field is empty.

**UpdateTypeImpossibleReason** :: If UpdateTypeImpossible field set to true, this is the annotator's free-form response to why the update was impossible to write.

## Dataset-Specific Fields

### delta-atomic

* **AtomicEventId**
* **AtomicEventRelationId**
* **AtomicRelationType**
* **AtomicInference**

### delta-snli

* **SNLIPairId**

### delta-social

* **SocialChemSituationUID**
* **SocialChemSituation**
* **SocialChemROT** (Note: same as Hypothesis field.)

# Important Note

For completeness, we have included instances where annotators indicated that writing an update strengthener or update weakener was impossible. These are indicated when the "UpdateTypeImpossible" field is set to "true". These instances are omitted from the experiments of Rudinger et al. 2020.

# Citing the Data

The companion paper for the Defeasible-NLI dataset is [*Thinking Like a Skeptic: Defeasible Inference in Natural Language*](https://www.aclweb.org/anthology/2020.findings-emnlp.418/) by Rudinger et al., 2020. Please use the following citation:

```
@inproceedings{rudinger-etal-2020-thinking,
    title = "Thinking Like a Skeptic: Defeasible Inference in Natural Language",
    author = "Rudinger, Rachel  and
      Shwartz, Vered  and
      Hwang, Jena D.  and
      Bhagavatula, Chandra  and
      Forbes, Maxwell  and
      Le Bras, Ronan  and
      Smith, Noah A.  and
      Choi, Yejin",
    booktitle = "Findings of the Association for Computational Linguistics: EMNLP 2020",
    month = nov,
    year = "2020",
    address = "Online",
    publisher = "Association for Computational Linguistics",
    url = "https://www.aclweb.org/anthology/2020.findings-emnlp.418",
    doi = "10.18653/v1/2020.findings-emnlp.418",
    pages = "4661--4675"
}
```

If you use this data, **please also be sure to cite all three of the original datasets on which Defeasible-NLI is built.**

* Sap et al., 2019. [ATOMIC: An Atlas of Machine Commonsense for If-Then Reasoning](https://ojs.aaai.org//index.php/AAAI/article/view/4160)
* Bowman et al., 2015. [A large annotated corpus for learning natural language inference](https://www.aclweb.org/anthology/D15-1075/)
* Forbes et al., 2020. [Social Chemistry 101: Learning to Reason about Social and Moral Norms](https://www.aclweb.org/anthology/2020.emnlp-main.48/)

```
@article{Sap_Le Bras_Allaway_Bhagavatula_Lourie_Rashkin_Roof_Smith_Choi_2019, title={ATOMIC: An Atlas of Machine Commonsense for If-Then Reasoning}, volume={33}, url={https://ojs.aaai.org/index.php/AAAI/article/view/4160}, DOI={10.1609/aaai.v33i01.33013027}, abstractNote={&lt;p&gt;We present ATOMIC, an atlas of everyday commonsense reasoning, organized through 877k textual descriptions of inferential knowledge. Compared to existing resources that center around taxonomic knowledge, ATOMIC focuses on inferential knowledge organized as typed &lt;em&gt;if-then&lt;/em&gt; relations with variables (e.g., â&lt;em&gt;if&lt;/em&gt; X pays Y a compliment, &lt;em&gt;then&lt;/em&gt; Y will likely return the complimentâ). We propose nine &lt;em&gt;if-then&lt;/em&gt; relation types to distinguish causes vs. effects, agents vs. themes, voluntary vs. involuntary events, and actions vs. mental states. By generatively training on the rich inferential knowledge described in ATOMIC, we show that neural models can acquire simple commonsense capabilities and reason about previously unseen events. Experimental results demonstrate that multitask models that incorporate the hierarchical structure of &lt;em&gt;if-then&lt;/em&gt; relation types lead to more accurate inference compared to models trained in isolation, as measured by both automatic and human evaluation.&lt;/p&gt;}, number={01}, journal={Proceedings of the AAAI Conference on Artificial Intelligence}, author={Sap, Maarten and Le Bras, Ronan and Allaway, Emily and Bhagavatula, Chandra and Lourie, Nicholas and Rashkin, Hannah and Roof, Brendan and Smith, Noah A. and Choi, Yejin}, year={2019}, month={Jul.}, pages={3027-3035} }
```

```
@inproceedings{bowman-etal-2015-large,
    title = "A large annotated corpus for learning natural language inference",
    author = "Bowman, Samuel R.  and
      Angeli, Gabor  and
      Potts, Christopher  and
      Manning, Christopher D.",
    booktitle = "Proceedings of the 2015 Conference on Empirical Methods in Natural Language Processing",
    month = sep,
    year = "2015",
    address = "Lisbon, Portugal",
    publisher = "Association for Computational Linguistics",
    url = "https://www.aclweb.org/anthology/D15-1075",
    doi = "10.18653/v1/D15-1075",
    pages = "632--642"
}
```

```
@inproceedings{forbes-etal-2020-social,
    title = "Social Chemistry 101: Learning to Reason about Social and Moral Norms",
    author = "Forbes, Maxwell  and
      Hwang, Jena D.  and
      Shwartz, Vered  and
      Sap, Maarten  and
      Choi, Yejin",
    booktitle = "Proceedings of the 2020 Conference on Empirical Methods in Natural Language Processing (EMNLP)",
    month = nov,
    year = "2020",
    address = "Online",
    publisher = "Association for Computational Linguistics",
    url = "https://www.aclweb.org/anthology/2020.emnlp-main.48",
    doi = "10.18653/v1/2020.emnlp-main.48",
    pages = "653--670"
}
```

# Contact

For questions, please contact Rachel Rudinger at `lastname@umd.edu`.
