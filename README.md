
# 🔄 Grid Forecast + Load Shedding Simulator

📌 **Project Title & Description**  
This simulator models a decentralized smart grid system capable of proactive load shedding. It leverages transformer-level forecast data, evaluates potential overloads using LLM reasoning, and escalates to an RL control agent to recommend shedding strategies. Users are notified using suggestion, request, or command formats compliant with the Beckn protocol.

---

👥 **Team Members**  
- Ashwin Thyagarajan  
- G Mohan  
- Rajkumar  

---

🧰 **Tech Stack**  
- 🧠 **OpenAI GPT-4.1** – Forecast evaluation, RL triggering, user action planning  
- 🧰 **Python** – Core simulation logic  
- 📦 **Gradio** – Interactive frontend  
- 📊 **Pandas** – Forecast data handling and DER mapping  
- 📐 **Pydantic** – LLM schema enforcement (structured outputs)

---

🚀 **Setup Instructions**

1. **Install dependencies**:
   ```bash
   pip install gradio openai pandas pydantic
   ```

2. **Set your OpenAI key**:
   ```bash
   export OPENAI_API_KEY="sk-..."
   ```

3. **Run the simulator**:
   ```bash
   python final_clean_gradio_simulator.py
   ```

This will launch a Gradio interface in your browser.

---

🎥 **Demo Video Link**  
# COMING SOON

▶️ [Add your Loom / YouTube / Drive link here]

---

📸 **Screenshots / Visuals**  

| Forecast Evaluation | RL Escalation | User-DER Map | Load Shedding Summary |
|---------------------|---------------|--------------|------------------------|
| ![forecast](screens/forecast_eval.png) | ![escalation](screens/escalation.png) | ![userder](screens/user_der_map.png) | ![summary](screens/load_summary.png) |

---

📚 **Challenges & Learnings**

- Designing consistent structured prompts for different roles (forecaster, RL agent, DER selector)
- Balancing user comfort with effective load control through message types (suggestion vs. command)
- Handling edge cases in user compliance and reward modeling
- Creating a meaningful reflection loop from logs using LLM self-assessment

---

🔗 **Useful Resources**

- [Beckn Protocol](https://becknprotocol.io)
- [OpenAI Function Calling](https://platform.openai.com/docs/guides/function-calling)
- [Gradio Documentation](https://gradio.app)
- [Pydantic](https://docs.pydantic.dev/latest/)
