# ADR-006: Selection of Open-Source LLM for Commercial Use

## **Title**
Choosing an Open-Source LLM Model with Image-to-Text Support for Commercial Applications

## **Context**
The system requires a Large Language Model (LLM) to support **multimodal tasks** (text and image-to-text processing). Key requirements:
- **Open-source and free for commercial use**.
- **Performance**: High accuracy in text and image-to-text tasks.
- **Scalability**: Efficient utilization of a 320GB GPU.
- **Image-to-Text Support**: Native or community-driven capabilities for processing images.
- **Customization**: Support for fine-tuning and domain adaptation.

## **Decision**
Evaluate five open-source LLM families (**Mistral, Qwen, Phi-4, DeepSeek, Llama**) against an updated scoring model to select the best candidate.

---

## **Scoring Model**
Criteria (weighted 1–5, with 5 being most critical):

| Criteria                | Weight | Description                                                                 |
|-------------------------|--------|-----------------------------------------------------------------------------|
| **Licensing**           | 5      | Must allow free commercial use with minimal restrictions.                  |
| **Performance**         | 4      | Benchmarks on text and image-to-text tasks.                                |
| **Image-to-Text Support**| 4     | Native or community-driven image processing capabilities.                 |
| **Scalability**         | 4      | Efficient inference on 320GB GPU (supports large models).                 |
| **Customization**       | 4      | Tools and guides for fine-tuning and adaptation.                          |
| **Community Support**   | 3      | Active development, documentation, and ecosystem tools.                  |

---

## **Candidate Models**
### 1. **Mistral**
- **License**: Apache 2.0.
- **Image-to-Text**: Text-only base models. Community projects (e.g., LLaVA-like adaptations) required for image support.
- **Strengths**: High efficiency, Mixture-of-Experts (MoE) support.

### 2. **Qwen** (Alibaba)
- **License**: Apache 2.0.
- **Image-to-Text**: Native multimodal support via **Qwen-VL** (supports image understanding and OCR).
- **Strengths**: Large context window (32k tokens), multimodal.

### 3. **Phi-4** (Microsoft)
- **License**: MIT.
- **Image-to-Text**: Text-only. No native or community image processing tools.
- **Strengths**: Lightweight, optimized for reasoning.

### 4. **DeepSeek**
- **License**: Apache 2.0.
- **Image-to-Text**: Text-only. Focused on coding/mathematical tasks.
- **Strengths**: Specialized for technical domains.

### 5. **Llama** (Meta)
- **License**: Custom (commercial use permitted with Meta approval).
- **Image-to-Text**: Text-only base models. Community projects like **LLaVA** add vision capabilities.
- **Strengths**: SOTA performance, massive community support.

---

## **Comparison**

| Model       | Licensing | Performance | Image-to-Text | Scalability | Customization | Community Support | **Total** |
|-------------|-----------|-------------|---------------|-------------|---------------|--------------------|-----------|
| **Mistral** | 5         | 5           | 2             | 5           | 5             | 5                  | **23**    |
| **Qwen**    | 5         | 4           | **5**         | 5           | 4             | 3                  | **24**    |
| **Phi-4**   | 5         | 3           | 2             | 4           | 3             | 3                  | **18**    |
| **DeepSeek**| 5         | 4           | 2             | 4           | 4             | 2                  | **19**    |
| **Llama**   | 4         | 5           | 3             | 5           | 5             | 5                  | **23**    |

---

## **Recommendation**
**Qwen** is the top choice due to its:
1. **Native image-to-text support** (Qwen-VL).
2. **Permissive licensing** (Apache 2.0).
3. **Large context window** (32k tokens) for multimodal workflows.

**Llama** and **Mistral** are alternatives if community-driven vision extensions (e.g., LLaVA) are acceptable.

## **Consequences**
- **Pros**:
    - Qwen-VL provides out-of-the-box image analysis.
    - Avoids dependency on third-party vision adapters.
- **Cons**:
    - Limited community adoption of Qwen outside China.

## **Alternatives**
- **Llama + LLaVA**: Use if Meta’s licensing terms are acceptable and community-driven tools suffice.
- **Mistral + Custom Adapter**: For teams willing to build/maintain image-processing pipelines.
