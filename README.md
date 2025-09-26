1
WatME: Towards Lossless Watermarking Through Lexical Redundancy
Authors: Liang Chen, Yatao Bian, et al.
Conference: ACL 2024
Link: [https://arxiv.org/abs/2311.09832v3](https://arxiv.org/abs/2311.09832v3)
Code: [https://github.com/ChanLiang/WatME](https://github.com/ChanLiang/WatME)
AI text often looks the same as human text, so we need watermarks to tell them apart.Old watermark methods (like Vanilla Watermark) can hurt text quality, especially in reasoning and knowledge tasks.WatME tries to add watermarks without lowering quality.LimitsText has little extra space, unlike images, so adding watermarks is harder.Vanilla often blocks whole groups of related words, making text worse.Abilities like reasoning and giving correct answers are more easily damaged by watermarks than simple fluency.Why Use Lexical RedundancyLanguage has groups of similar words (like ocean and sea).WatME splits these groups into red and green so not all words in a group are blocked.This keeps more word choices and makes text sound better.
￼<img width="351" height="291" alt="Question" src="https://github.com/user-attachments/assets/84961368-4c72-4d11-9d18-8df6270fa3f2" />

---

Method

Lexical Redundancy Construction

* Build synonym clusters (redundancy groups):

  * Dictionary-based: WordNet, Youdao, etc.
  * Prompt-based: Using LLMs like Llama2 for synonym mining.
  * Ensures semantic/grammatical consistency and addresses subword tokenization issues.

Core Algorithm

* Two-stage construction of green/red lists:

  * Stage 1: Apply the Mutual Exclusion Rule within synonym clusters.
  * Stage 2: Regular assignment for remaining vocabulary.
* During decoding, logits of green list words are biased by δ to guide sampling.

Mathematical Definition and Theory

* Semantic Entropy: measures lexical diversity.
* WatME increases semantic entropy in the green list, boosting expressiveness.
* Theorem: WatME is more likely than Vanilla to sample an “appropriate word.”

---

Experiments

Setup

* Models: Llama2-7B (unaligned), Vicuna-7B (aligned).
* Tasks:

  * Knowledge: TruthfulQA (truthful and informative answers).
  * Reasoning: GSM8K (math reasoning).
  * Fluency: C4 Perplexity.
* Metrics: Accuracy, AUROC, PPL, Truth × Info.

Key Results

| Model/Method    | GSM8K Accuracy | Truth × Info | AUROC Detection | Perplexity |
| --------------- | -------------- | ------------ | --------------- | ---------- |
| Llama2 baseline | 11.22%         | 88.23        | -               | 4.77       |
| +Vanilla        | ↓50.0%         | ↓45.4%       | 0.972           | ↑7.00      |
| +WatME (prompt) | ↓48.0%         | ↓42.9%       | 0.972           | ↑6.89      |
| +WatME (dict)   | ↓18.3%         | ↓30.7%       | 0.980           | ↑5.32      |

* WatME preserves emergent abilities better than Vanilla while maintaining detection performance.
* Prompt-based clustering favors informativeness, while dictionary-based favors semantic consistency.

---

System Mechanism

Robustness

* Tested under substitution attacks and paraphrasing attacks:

  * WatME remains more robust (still detectable).
  * Mutual exclusion reduces red-green flipping probability.
  * Cluster-based logic makes reverse-engineering harder.

Detection

* Uses z-score and AUROC for watermark detection.
* Increasing δ boosts detectability but affects quality.
* WatME consistently outperforms Vanilla across all δ settings, with higher detection curves.

---

Limitations

* Still not fully lossless (δ ≠ 0).
* Only tested in English.
* Low-entropy tasks (e.g., commonsense QA) pose robustness challenges.
* Prompt-based clustering quality depends on LLM sensitivity.

for our research:

WatME method synonym grouping red/green, mutual exclusion green + δ bias preserve expression space Visual analogy perceptual or task-equivalent elements grouped red/green mutual exclusion green + δ watermark keep quality

Redundancy types: - Appearance redundancy palette texture noise seed style vector - Geometric redundancy slight deformation LoD variants equivalent mesh fragments - Rendering redundancy lighting direction intensity color temperature camera trajectory perturbation anti-aliasing denoising settings - Feature redundancy VQ codebook tokens tri-plane voxel clusters attention head choices

Embedding only bias green logits with δ red untouched outputs statistically skew to green detectable signal keep equivalent options minimal quality loss
Detection reconstruct red/green via key count actual green hits vs random baseline z-score or AUROC significantly higher → watermark present

StoryBlender: Controllable 3D Storyboard Generation using 3D/Geometry aware VLM Agents

3D Storyboard Elements
* Story Flow: A series of pictures showing how the story moves from one moment to the next.
* Layout: Where people, objects, and background parts are placed to show depth and size.
* Camera: Where the camera is, how it moves or turns, and how it shows depth.
* Characters: Main poses and actions that show what people feel and do.
* Lighting: Notes on where the light comes from, how strong it is, and its color to set the mood.
* Sound: Space to add words, sound effects, or music that match the scene.
* Notes: Extra details like how long a shot lasts or if special effects are needed.

Advantages of 3D storyboarding
1. Storyboard design is similar to rough drafting, requiring less detailed models.
2. I currently have some 2D storyboard papers and products, and some work on 3D scene generation, but (probably) no 3D storyboarding. Piecing the two together will give me a rough idea.
3. Training data and models don't seem to be necessary; everything can be done using the API.
4. This will be helpful for future 3D animation generation.

https://github.com/ahujasid/blender-mcp
Configuring the local environment
￼
￼<img width="538" height="173" alt="Pasted Graphic 3" src="https://github.com/user-attachments/assets/115353b2-e7d8-455c-909c-ab1c218a75bf" />

￼<img width="472" height="352" alt="Pasted Graphic 4" src="https://github.com/user-attachments/assets/8fd3dc52-9b05-43b3-8585-aa6ff1560a52" />


￼<img width="540" height="344" alt="Pasted Graphic 6" src="https://github.com/user-attachments/assets/d48697c2-f01d-4783-bc97-0126f8d2cd18" />

<img width="307" height="202" alt="Pasted Graphic 5" src="https://github.com/user-attachments/assets/3b66d68a-5773-42f1-9382-c2f433ac3d4f" />

TODO
1. Overall, the project is engineering-oriented and lacks much academic innovation. Further work is needed (mathematics, graphics, CV).
	-1. Interactivity
	-2. Agent error accumulation
2. Blender MCP is still insufficient; a large number of additional features need to be implemented to meet the needs.
3. The dataset and evaluation metrics are not readily available.

