# MQM-aug

Original MQM data contains **severity** and **location** for each error. i.e. each error $\mathbf{e}_i^{original}$ conatins $\\{\textbf{loc}_i, \textbf{sev}_i\\}$.   

We augment MQM data by prompting GPT-4o to produce **explanation** and **correct suggestions** for each error. i.e. each error $\mathbf{e}_i^{augmented}$ conatins $\\{\textbf{loc}_i, \textbf{sev}_i, \textbf{exp}_i, \textbf{sugg}_i \\}$.

Here is an example of the augmented MQM data:
```json
{"source":"市内一座商场同样倒塌，数百名居民赶到现场，等候亲友的音讯。",
"translation":"A shopping mall collapsed, and hundreds of residents rushed to the scene, waiting for the audio of friends and relatives." ,
"original errors":"There is a major error at \"audio\".",
"augmented errors":[{"location": \"audio\","severity": \"major\",
"explanation": \"The term '音讯' in the original text is misinterpreted as 'audio'. In this context, '音讯' means 'news' or 'information' regarding the safety of friends and relatives, not 'audio'.\",
"improvement": \"Change 'audio of friends and relatives' to 'news of friends and relatives'.\"}]
}
```

**Our augmentation manner implicitly incorporates a Chain-of-Thought (CoT) mechanism:** by requiring the model to first explain the error ($\textbf{exp}_i$) before generating a correction suggestion ($\textbf{sugg}_i$), we enforce a step-by-step reasoning process. **The model must understand the error (e.g., semantic mismatch, grammatical flaw, or cultural mistranslation) before proposing a fix**, mirroring the "diagnose-then-correct" workflow of human experts. This idea is also used in the design of xTower[1] .

[1] xTower: A Multilingual LLM for Explaining and Correcting Translation Errors. EMNLP Findings,2024.
