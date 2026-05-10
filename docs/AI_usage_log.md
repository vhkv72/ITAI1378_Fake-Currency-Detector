# AI Usage Log — Fake Currency Detector
**Student:** Vy Vo | **Course:** ITAI 1378 | **Project:** Fake Currency Detector

---

## Log Entries

### Entry 1
- **Date:** Week 10
- **Tool:** ChatGPT (GPT-4)
- **Task:** Project proposal organization
- **Prompt used:** "Help me organize a computer vision project proposal for detecting fake currency using ResNet50"
- **How output was used:** Used as a starting template; rewrote all sections in my own words and added my specific dataset, metrics, and week-by-week plan
- **What I learned:** How to structure a technical proposal clearly

---

### Entry 2
- **Date:** Week 10
- **Tool:** ChatGPT (GPT-4)
- **Task:** GitHub README formatting
- **Prompt used:** "What sections should a good GitHub README have for a machine learning project?"
- **How output was used:** Used the suggested section list as a guide; wrote all content myself
- **What I learned:** The importance of including dataset instructions, how-to-run steps, and results tables in a README

---

### Entry 3
- **Date:** Week 11
- **Tool:** Claude (Anthropic)
- **Task:** Notebook structure and data augmentation strategy
- **Prompt used:** "What data augmentation techniques work best for currency image classification with a small dataset?"
- **How output was used:** Adopted the suggestion to use ColorJitter + RandomGrayscale in addition to standard flips/crops; verified each transform made sense for banknote images
- **What I learned:** ColorJitter helps simulate different lighting conditions on bills; RandomGrayscale forces the model to learn texture features, not just color

---

### Entry 4
- **Date:** Week 11
- **Tool:** Claude (Anthropic)
- **Task:** Understanding transfer learning layer freezing
- **Prompt used:** "In ResNet50 transfer learning, which layers should I freeze and which should I fine-tune for a binary classification task?"
- **How output was used:** Decided to freeze layers 1–3 and fine-tune layer4 + the new FC head based on the explanation; tested this against full fine-tuning and found it trained faster
- **What I learned:** Freezing early layers (which learn edges/textures) and only fine-tuning deeper layers (which learn task-specific patterns) is efficient for small datasets

---

### Entry 5
- **Date:** Week 11
- **Tool:** Claude (Anthropic)
- **Task:** Understanding early stopping and label smoothing
- **Prompt used:** "What is label smoothing in CrossEntropyLoss and why would I use it?"
- **How output was used:** Added `label_smoothing=0.1` to the loss function after understanding it prevents overconfident predictions
- **What I learned:** Label smoothing regularizes the model by softening the target distribution, which helps generalization

---

### Entry 6
- **Date:** Week 12
- **Tool:** ChatGPT (GPT-4)
- **Task:** Debugging ImageFolder class ordering
- **Prompt used:** "Why does torchvision ImageFolder sort classes alphabetically and how does this affect my class indices?"
- **How output was used:** Confirmed that `CLASS_NAMES = ['fake', 'real']` is correct (alphabetical), which matters for the confusion matrix labels
- **What I learned:** Always check `dataset.classes` output before assuming label order

---

### Entry 7
- **Date:** Week 12
- **Tool:** Claude (Anthropic)
- **Task:** Understanding why 100% accuracy might indicate overfitting
- **Prompt used:** "My model got 100% accuracy on a 100-image dataset. Is this overfitting or is it valid?"
- **How output was used:** Added analysis note in the notebook: with only 15 test images, 100% = 15/15 correct — a larger test set would give more reliable estimates. Noted this as a limitation.
- **What I learned:** Small test sets can produce misleading perfect scores; always report dataset size alongside metrics

---

### Entry 8
- **Date:** Week 13
- **Tool:** Claude (Anthropic)
- **Task:** Structuring the final project files per course requirements
- **Prompt used:** "What files does my GitHub repository need for a final computer vision project submission?"
- **How output was used:** Used as a checklist reference while organizing my repo; created the `docs/`, `results/`, `notebooks/`, and `src/` folders
- **What I learned:** A well-organized repo is as important as working code for professional credibility

---

### Entry 9
- **Date:** Week 14
- **Tool:** ChatGPT (GPT-4)
- **Task:** Writing the results summary section of README
- **Prompt used:** "How should I present machine learning results in a GitHub README professionally?"
- **How output was used:** Used the suggested table format; filled in my actual numbers (100% accuracy, 19.80ms inference)
- **What I learned:** Results tables with targets vs. achieved values are more readable than prose descriptions

---

### Entry 10
- **Date:** Week 14
- **Tool:** Claude (Anthropic)
- **Task:** Identifying future improvements for the project
- **Prompt used:** "What are realistic next steps to improve a fake currency detector beyond the current prototype?"
- **How output was used:** Selected 3 most practical suggestions (larger dataset, Grad-CAM, mobile deployment) and added them to README Future Improvements section with my own explanations
- **What I learned:** Grad-CAM is a technique I want to learn next — it makes model decisions interpretable by highlighting which pixels influenced the prediction

---

## Summary

| Metric | Value |
|--------|-------|
| Total AI tool uses | 10 |
| Tools used | ChatGPT (GPT-4), Claude (Anthropic) |
| Primary uses | Documentation, debugging, concept understanding |
| Code written by student | ~65% |
| Code AI-assisted | ~35% |

**Key principle followed:** AI was used to *understand* concepts and *improve* the work — not to replace thinking. Every AI suggestion was evaluated, tested, and adapted before being used.
