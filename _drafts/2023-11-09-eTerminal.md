---
layout: post
title: e-01 in terminal
subtitle: python
categories: python
tags: [python, code]
---

## 터미널에서 숫자 표현

[CLIP](https://github.com/openai/CLIP)의 zero-shot 코드를 돌려보면 output으로 각 class별 확률이 나온다.

CLIP



```

text = clip.tokenize(["alder flycatcher", "acorn woodpecker", "white ibis"]).to(device)

with torch.no_grad():
    image_features = model.encode_image(image)
    text_features = model.encode_text(text)
    
    logits_per_image, logits_per_text = model(image, text)
    probs = logits_per_image.softmax(dim=-1).cpu().numpy()

print("Label probs:", probs)  # prints: [[0.9927937  0.00421068 0.00299572]]


# Acorn_Woodpecker/391427.jpg   ["a diagram", "a dog", "a cat", "a bird"]
# Label probs: [[5.9159915e-04 5.8533618e-04 3.9655867e-04 9.9842656e-01]]

# Acorn_Woodpecker/391427.jpg   ["a diagram", "a dog", "a cat", "a bird", "acorn woodpecker", "alder flycatcher"]).to(device)
# Label probs: [[3.2474959e-06 3.2131163e-06 2.1768501e-06 5.4807151e-03 9.8330700e-01 1.1203607e-02]]

# Alder_Flycatcher/532326.jpg   ["a diagram", "a dog", "a cat", "a bird", "acorn woodpecker", "alder flycatcher"]).to(device)
# Label probs: [[1.0838326e-07 2.5759209e-07 2.8152965e-07 6.2112155e-04 6.8263017e-09 9.9937820e-01]]

# CLIP.png  ["a diagram", "a dog", "a cat", "a bird"]
# Label probs: [[0.9911703  0.00420373 0.00299083 0.00163516]]


# ------

# Acorn_Woodpecker/391427.jpg  ["a bird", "acorn woodpecker", "alder flycatcher"]
# Label probs: [[0.00548077 0.98331547 0.01120377]]

# Acorn_Woodpecker/391545.jpg  ["a bird", "acorn woodpecker", "alder flycatcher"]
# Label probs: [[5.4990454e-04 9.9944514e-01 4.9911046e-06]]

# Acorn_Woodpecker/391906.jpg  ["alder flycatcher", "acorn woodpecker", "white ibis"]
# Label probs: [[6.1842417e-07 9.9999785e-01 1.5640782e-06]]


#-------

# White_winged_Crossbill/243912.jpg   ["a bird", "white winged crossbill", "white ibis"]
# Label probs: [[6.8848167e-05 4.9102495e-09 9.9993110e-01]]


```



