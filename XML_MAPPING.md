# XML Variable Mapping: DrugResistance_Interpretation to Sierra Format

## Overview
This document maps variables from the original HIVDB DrugResistance_Interpretation XML format to the new Sierra/GraphQL format.

---

## Algorithm Information

| Original XML Path | Original Value | New XML Path | New Value |
|---|---|---|---|
| `DrugResistance_Interpretation/algorithmName` | "HIVDB" | `currentVersion/family` | "HIVDB" |
| `DrugResistance_Interpretation/algorithmVersion` | "9.8" | `currentVersion/version` | "9.8" |

---

## Gene Data Mapping

### Gene Information
| Original XML Path | Original Value | New XML Path | New Value |
|---|---|---|---|
| `result/geneData/gene` | "PR", "RT", "IN" | `allGenes/name` | "PR", "RT", "IN" |
| `result/geneData/present` | true/false | *Not directly mapped* | *Implicit from structure* |
| `result/geneData/consensus` | Protein sequence | `allGenes/refSequence` | Reference sequence |

### Gene from Report
| Original XML Path | Original Value | New XML Path | New Value |
|---|---|---|---|
| `report/alignedGeneSequences/gene/name` | "IN" | `report/alignedGeneSequences/gene/name` | "IN" |

---

## Mutation Data Mapping

### Comment/Mutation Information
| Original XML Path | Original Value | New XML Path | New Value |
|---|---|---|---|
| `result/comment/gene` | "PR", "RT" | `report/alignedGeneSequences/mutations/primaryType` + `report/drugResistance/mutationsByTypes/drugClass` | Gene context derived |
| `result/comment/mutationString` | "M46I", "N88S" | `report/alignedGeneSequences/mutations/text` | "M46I", "N88S" |
| `result/comment/grouping` | "Major", "Accessory", "Other" | `report/alignedGeneSequences/mutations/primaryType` | "Major", "Accessory", "Other" |
| `result/comment/commentString` | Clinical interpretation | `allGenes/drugClasses/mutationTypes` | Referenced in drug class context |
| `result/comment/position` | Position number | `report/alignedGeneSequences/mutations/position` | Position number |

### Mutation Classification
| Original XML Path | Original Value | New XML Path | New Value |
|---|---|---|---|
| `result/geneData/mutation/classification` | "NRTI", "NNRTI", "OTHER" | `report/alignedGeneSequences/mutations/primaryType` | "Other", "NRTI", "NNRTI" |
| `result/geneData/mutation/position` | Position number | `report/alignedGeneSequences/mutations/position` | Position number |
| `result/geneData/mutation/mutationString` | "M184V" | `report/alignedGeneSequences/mutations/text` | "M184V" |
| `result/geneData/mutation/wildType` | "M" | `report/alignedGeneSequences/mutations/reference` | "M" |
| `result/geneData/mutation/translatedNA` | "V" | `report/alignedGeneSequences/mutations/AAs` | "V" |
| `result/geneData/mutation/nucleicAcid` | "GTG" | `report/alignedGeneSequences/mutations/triplet` | "GTG" |

---

## Drug Resistance Score Mapping

### Drug Score Information
| Original XML Path | Original Value | New XML Path | New Value |
|---|---|---|---|
| `result/drugScore/drugCode` | "ATV/r", "DRV/r" | `report/drugResistance/drugScores/drug/name` | "ATV", "DRV" |
| `result/drugScore/genericName` | "atazanavir/r" | `report/drugResistance/drugScores/drug/fullName` | "atazanavir/r" |
| `result/drugScore/type` | "PI", "NRTI", "NNRTI" | `report/drugResistance/drugScores/drugClass/name` | "PI", "NRTI", "NNRTI" |
| `result/drugScore/score` | 75, -5, 30 | `report/drugResistance/drugScores/score` | 75, -5, 30 |
| `result/drugScore/resistanceLevel` | 1, 2, 3, 4, 5 | `report/drugResistance/drugScores/level` | 1, 2, 3, 4, 5 |
| `result/drugScore/resistanceLevelText` | "Susceptible", "High-Level Resistance" | `report/drugResistance/drugScores/text` | "Susceptible", "High-Level Resistance" |
| `result/drugScore/threeStepResistanceLevel` | "S", "I", "R" | `report/drugResistance/drugScores/SIR` | "S", "I", "R" |

### Partial Score Information
| Original XML Path | Original Value | New XML Path | New Value |
|---|---|---|---|
| `result/drugScore/partialScore/mutation` | "K20T" | *Not directly in new format* | Inferred from drug resistance mutations |
| `result/drugScore/partialScore/score` | 5, 10, 60 | *Not directly in new format* | Available in scoreTable context |

---

## Sequence and Quality Data

### Input Sequence
| Original XML Path | Original Value | New XML Path | New Value |
|---|---|---|---|
| `result/inputSequence/md5sum` | Hash value | `report/inputSequence/MD5` | Hash value |
| `result/inputSequence/name` | "K071380" | `report/inputSequence/header` | "K071380" |
| `result/inputSequence/sequence` | Nucleic acid sequence | `report/inputSequence/sequence` | Nucleic acid sequence |

### Aligned Sequences
| Original XML Path | Original Value | New XML Path | New Value |
|---|---|---|---|
| `result/geneData/alignedNASequence` | Aligned NA | `report/alignedGeneSequences/alignedNAs` | Aligned NA |
| `result/geneData/alignedAASequence` | Aligned AA | `report/alignedGeneSequences/alignedAAs` | Aligned AA |
| `result/geneData/firstAA` | 1, 6 | `report/alignedGeneSequences/firstAA` | 1, 6 |
| `result/geneData/lastAA` | 99, 288 | `report/alignedGeneSequences/lastAA` | 99, 288 |

### Sequence Quality
| Original XML Path | Original Value | New XML Path | New Value |
|---|---|---|---|
| `result/sequenceQualityCounts/insertions` | 0 | *Not directly in report* | Available in sequenceQualityCounts |
| `result/sequenceQualityCounts/deletions` | 0 | *Not directly in report* | Available in sequenceQualityCounts |
| `result/sequenceQualityCounts/ambiguous` | 0 | *Not directly in report* | Available in sequenceQualityCounts |
| `result/sequenceQualityCounts/stops` | 0 | *Not directly in report* | Available in sequenceQualityCounts |
| `result/sequenceQualityCounts/frameshifts` | 0 | *Not directly in report* | Available in sequenceQualityCounts |

---

## Subtype Information

### Subtype Data
| Original XML Path | Original Value | New XML Path | New Value |
|---|---|---|---|
| `result/geneData/subtype/type` | "C (4.93%)" | `report/bestMatchingSubtype/display` | "C (3.47%)" |
| `result/geneData/subtype/percentSimilarity` | 95.1 | `report/bestMatchingSubtype/distance` | 0.0347 (as decimal) |

---

## Drug Classes and Mutations

### Drug Class Information
| Original XML Path | Original Value | New XML Path | New Value |
|---|---|---|---|
| `result/geneData/drugClasses/name` | "PI", "NRTI", "NNRTI" | `allGenes/drugClasses/name` | "PI", "NRTI", "NNRTI" |
| `result/geneData/drugClasses/drugs/name` | "ATV", "DRV" | `allGenes/drugClasses/drugs/name` | "ATV", "DRV" |
| `result/geneData/drugClasses/drugs/fullName` | "atazanavir/r" | `allGenes/drugClasses/drugs/fullName` | "atazanavir/r" |
| `result/geneData/drugClasses/drugs/displayAbbr` | "ATV/r" | `allGenes/drugClasses/drugs/displayAbbr` | "ATV/r" |

---

## Mutation Prevalence

### Prevalence Mapping
| Original XML Path | Original Value | New XML Path | New Value |
|---|---|---|---|
| *Not in original* | N/A | `report/mutationPrevalences/boundMutation/text` | "D25E", "V31I" |
| *Not in original* | N/A | `report/mutationPrevalences/matched/subtypes/subtype/name` | "A", "B", "C" |
| *Not in original* | N/A | `report/mutationPrevalences/matched/subtypes/percentageNaive` | 57.13 |
| *Not in original* | N/A | `report/mutationPrevalences/matched/subtypes/percentageTreated` | 59.52 |

---

## Summary of Key Structural Changes

1. **Hierarchical Organization**: Original XML uses flat `comment` and `geneData` arrays; new XML uses nested `drugResistance` and `alignedGeneSequences` structures.

2. **GraphQL Schema**: New format follows GraphQL conventions with `__typename` fields for type identification.

3. **Enhanced Metadata**: New format includes mutation prevalence data not present in original.

4. **Algorithm Versioning**: Moved from direct `algorithmVersion` to nested structure under `currentVersion`.

5. **Drug Information**: Enhanced with `displayAbbr` and more detailed drug class associations.

6. **Report Structure**: Original uses `result` root; new format uses `report` with more comprehensive data organization.

