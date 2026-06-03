# OCPL-Model Extension

**Version:** 1.0  
**Applies to:** AI model projects — trained model weights, fine-tuned models, embedding models, and inference infrastructure where the trained artifact (not just source code) is the primary value.  
**Use alongside:** OCPL v1.1 core  
**Declaration:** `OCPL-1.1 + OCPL-Model-1.0`

---

## Additional Conditions

### M1. Weight Availability

Any model weights covered by this license must be made available for download at no charge, in a format usable without proprietary software, for any individual, researcher, or organization that requests them for non-commercial or research purposes.

Commercial inference services may charge for API access. The weights themselves must remain freely downloadable.

### M2. Training Data Lineage

The training data used to produce the covered model must be documented with sufficient specificity to allow independent verification of:
- The categories of data sources used
- The data collection and filtering methodology
- Any known biases, gaps, or quality issues
- Attribution for datasets that require it under their own licenses

Full dataset release is not required, but the lineage must be documented such that a researcher can assess the model's likely behaviors, capabilities, and limitations.

### M3. Inference Access

If the covered model is made available as a hosted inference service, a reasonable free tier must be provided for individual researchers, students, and public-good mission contributors. The free tier must be sufficient for:
- Evaluating the model's capabilities
- Research and non-commercial experimentation
- Contributions to public-good missions

### M4. Derivative Model Attribution

Any model derived from a covered model (fine-tuned, distilled, merged, or otherwise derived) must attribute the covered model in its documentation, model card, and any published research. Attribution must include the covered model's name, version, and this license.

### M5. No Behavioral Lock-in

Hosted inference services using covered models may not:
- Return outputs in proprietary formats that cannot be processed without the operator's additional software
- Require accepting proprietary terms that restrict the use of outputs for implementing compatible services
- Prevent users from switching to alternative inference providers for the same model

---

## Example: OpenKO LLM

The openko-base, openko-small, and openko-embeddings models would adopt OCPL-1.1 + OCPL-Model-1.0:
- Weights freely downloadable for research and non-commercial use
- Commercial inference services may charge CU per token
- Training data lineage documented in the model card
- Outputs may not be locked to the OpenKO inference endpoint

---

## Declaration

```toml
[project]
license = "OCPL-1.1+Model"

[capabilities]
contributes = ["compute.inference", "knowledge.embeddings"]

[economics.modes]
weights_download = "free"    # always free for research
primary_mode     = "hosted-inference"
```
