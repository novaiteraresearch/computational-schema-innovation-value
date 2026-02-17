## Summary

- **Multi-factor scoring model:** Evaluates research artifacts across five weighted dimensions (Component Complexity 0-30, Type Sophistication 0-25, Format Structure 0-20, Tag Diversity 0-15, Purpose Depth 0-10) to produce a 0-100 score
- **Nine-tier classification taxonomy:** Maps total scores to discrete asset types ranging from INITIAL_BRAINDUMP (<15) to PROPRIETARY_SYSTEM (≥85)
- **Formula implementation:** Uses nested `lets()` and `ifs()` functions to compute scores from database properties (Components, Type, Format, Tags, Purpose)
- **Threshold-based classification:** Employs hard cutoffs at 15, 25, 35, 45, 55, 65, 75, and 85 points to assign asset type labels
- **Open-source release structure:** Includes Apache-2.0 license, NOTICE file, CITATION.cff, and YAML metadata with UTC timestamps for provenance tracking
- **Explicit attribution requirements:** Mandates retention of NOTICE, LICENSE, and YAML metadata in any redistribution or derivative work
