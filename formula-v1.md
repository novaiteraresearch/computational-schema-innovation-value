lets(
  /* Score based on component complexity (0-30 points) */
  componentScore, prop("Components").length() * 3,
  
  /* Score based on type sophistication (0-25 points) */
  typeScore, ifs(
    prop("Type") == "System Prompt", 25,
    prop("Type") == "Metaprompt", 22,
    prop("Type") == "Schema", 20,
    prop("Type") == "Chain of Thought", 18,
    prop("Type") == "Instruction Set", 15,
    prop("Type") == "Evaluation Prompt", 15,
    prop("Type") == "Prompt Template", 12,
    prop("Type") == "Few-Shot Example", 8,
    5
  ),
  
  /* Score based on format structure (0-20 points) */
  formatScore, ifs(
    prop("Format") == "METADATA CLASSIFIER", 20,
    prop("Format") == "TAXONOMY", 20,
    prop("Format") == "Schema", 18,
    prop("Format") == "Table", 16,
    prop("Format") == "Structured Overview", 15,
    prop("Format") == "Step-by-Step Guide", 13,
    prop("Format") == "Structured Summary", 12,
    prop("Format") == "Report", 10,
    prop("Format") == "Q&A", 8,
    prop("Format") == "Bullet Points", 6,
    prop("Format") == "Conversation", 4,
    5
  ),
  
  /* Score based on tag diversity (0-15 points) */
  tagScore, min(15, prop("Tags").length() * 2.5),
  
  /* Score based on purpose depth (0-10 points) */
  purposeScore, if(empty(prop("Purpose")), 0, min(10, prop("Purpose").length() / 30)),
  
  /* Aggregate total score (0-100 scale) */
  totalScore, round(componentScore + typeScore + formatScore + tagScore + purposeScore, 0),
  
  /* Map score to asset classification */
  assetType, ifs(
    totalScore >= 85, "PROPRIETARY_SYSTEM",
    totalScore >= 75, "COMPREHENSIVE_FRAMEWORK",
    totalScore >= 65, "STRUCTURED_METHODOLOGY",
    totalScore >= 55, "OPERATIONAL_WORKFLOW",
    totalScore >= 45, "SYSTEMATIC_SCHEMA",
    totalScore >= 35, "REFINED_CONCEPT",
    totalScore >= 25, "DEVELOPED_IDEA",
    totalScore >= 15, "STRUCTURED_THOUGHT",
    "INITIAL_BRAINDUMP"
  ),
  
  /* Return classification and score in system format */
  "[" + assetType + "] Score: " + format(totalScore) + "/100"
)
